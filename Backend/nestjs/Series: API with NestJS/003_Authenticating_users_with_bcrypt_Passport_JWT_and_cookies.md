> https://wanago.io/2020/05/25/api-nestjs-authenticating-users-bcrypt-passport-jwt-cookies/
# Authenticating users with bcrypt, Passport, JWT, and cookies
- Xác thực là một phần quan trọng trong hầu hết các trang web. Chúng ta sẽ tìm hiểu về **passport**, đây là ứng dụng xác thực Nodejs phổ biến nhất. Chúng ta đăng ký người dùng và bảo mật mật khẩu của họ bằng cách sử dụng **hashing**
# Defining the User entity
- Điều đầu tiên cần làm khi cân nhắc xác thực là đăng ký người dùng của chúng ta. Để làm như vậy, chúng ta cần xác định 1 entity cho người dùng của mình
- users/user.entity.ts
```ts
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
 
@Entity()
class User {
  @PrimaryGeneratedColumn()
  public id?: number;
 
  @Column({ unique: true })
  public email: string;
 
  @Column()
  public name: string;
 
  @Column()
  public password: string;
}
 
export default User;
```
- Điều mới duy nhất ở trên là `unique flag`. Không nên có 2 người dùng cùng 1 email. Chức năng này được tích hợp vào PostgresSQL và chúng tôi giúp duy trì tính nhất quán của dữ liệu
- Chúng ta cần thực hiện 1 số thao tác trên người dùng của mình. Để làm được điều đó, hãy tạo 1 service
- users/users.service.ts
```ts

import { HttpException, HttpStatus, Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import User from './user.entity';
import CreateUserDto from './dto/createUser.dto';
 
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>
  ) {}
 
  async getByEmail(email: string) {
    const user = await this.usersRepository.findOne({ email });
    if (user) {
      return user;
    }
    throw new HttpException('User with this email does not exist', HttpStatus.NOT_FOUND);
  }
 
  async create(userData: CreateUserDto) {
    const newUser = await this.usersRepository.create(userData);
    await this.usersRepository.save(newUser);
    return newUser;
  }
}
```
- users/dto/createUser.dto.ts
```ts

export class CreateUserDto {
  email: string;
  name: string;
  password: string;
}
 
export default CreateUserDto;
```
- Tất cả các điều trên được gói gọn trong 1 module
- users/users.module.ts
```ts

import { Module } from '@nestjs/common';
import { UsersService } from './users.service';
import { TypeOrmModule } from '@nestjs/typeorm';
import User from './user.entity';
 
@Module({
  imports: [TypeOrmModule.forFeature([User])],
  providers: [UsersService],
  exports: [UsersService]
})
export class UsersModule {}
```
# Handling passwords
- Không nên lưu mật khẩu ở dạng text, vì nếu db bị xâm phạm, mật khẩu sẽ bị lộ. Để làm cho mật khẩu an toàn hơn, chúng ta sử dụng `hash`. Thuật toán hash biến đổi chuỗi thành 1 chuỗi khác, nếu thay đổi 1 ký tự trong chuỗi, chuỗi sẽ hoàn toàn khác
- Thao tác trên chỉ có thể thực hiện theo 1 cách và không dễ đảo ngược - nghĩa là chúng tôi không biết mật khẩu của người dùng. Khi người dùng đăng nhập, chúng ta cần thực hiện thao tác này 1 lần nữa, sau đó so sánh với kết quả được lưu trong CSDL
- Vì việc hashing 1 chuỗi 2 lần sẽ cho cùng 1 kết quả, chúng ta sử dụng `salt`. Nó chặn được những người dùng có cùng mật khẩu có cùng hash. `Salt` là 1 chuỗi ngẫu nhiên được thêm vào mật khẩu gốc để đạt được kết quả khác nhau sau mỗi lần

## Using bcrypt
- Sử dụng thuật toán bcrypt. Thuật toán này xử lý việc hash các chuỗi, so sánh các chuỗi thuần tuý với các hàm hash và thêm salt
- Sử dụng bcrypt khá tốn CPU. Khá may mắn đó là việc triển khai bcrypt của chúng tôi sử dụng 1 nhóm luồng cho phép nó chạy trong 1 luồng bổ sung, nhờ đó app của chúng ta có thể thực hiện việc khác trong khi tạo hàm hash
```ts
npm install @types/bcrypt bcrypt
```
- Khi sử dụng bcrypt, chúng tôi xác định các vòng salt. Nó là yếu tố chi phí và kiểm soát thời gian cần thiết để nhận được kết quả. Tăng nó lên 1 thì thời gian sẽ tăng gấp đôi. Yếu tố chi phí càng lớn thì việc đảo ngược hàm băm bằng phương pháp brute-forcing càng trở nên khó khăn. Nói chung, 10 salt là đủ
- Salt dùng để hash là 1 phần của kết quả, vì vậy không cần phải giữ riêng
```ts
const passwordInPlaintext = '12345678';
const hash = await bcrypt.hash(passwordInPlaintext, 10);
 
const isPasswordMatching = await bcrypt.compare(passwordInPlaintext, hashedPassword);
console.log(isPasswordMatching); 
```
## Creating the authentication service
- Với các kiến thức trên, chúng ta có thể triển khai basic login & logout. Để thực hiện, chúng ta cần 1 authentication service
  - Authentication: Kiểm tra danh tính người dùng, xác thực người dùng là ai
  - Authorization: Người dùng có được thực hiện thao tác này không
- authentication/authentication.service.ts
```ts
export class AuthenticationService {
  constructor(
    private readonly usersService: UsersService
  ) {}
 
  public async register(registrationData: RegisterDto) {
    const hashedPassword = await bcrypt.hash(registrationData.password, 10);
    try {
      const createdUser = await this.usersService.create({
        ...registrationData,
        password: hashedPassword
      });
      createdUser.password = undefined;
      return createdUser;
    } catch (error) {
      if (error?.code === PostgresErrorCode.UniqueViolation) {
        throw new HttpException('User with that email already exists', HttpStatus.BAD_REQUEST);
      }
      throw new HttpException('Something went wrong', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
  // (...)
}
```
  - `createdUser.password = undefined` không phải là cách tốt nhất để không gửi password vào response. Trong các phần tiếp theo chúng ta sẽ tìm hiểu các cách khác
- Một vài điều đáng chú ý ở trên là chúng ta tạo hàm hash và truyền nó đến method `usersService.create` cùng với phần còn lại của dữ liệu.
- Để hiểu lỗi, chúng ta cần xem docs [PostgreSQL Error Codes documentation page.](https://www.postgresql.org/docs/9.2/errcodes-appendix.html)
- Vì code cho uniqe_violation là 23505, chúng ta tạo enum để xử lý một cách rõ ràng
```ts
//database/postgresErrorCodes.enum.ts
enum PostgresErrorCode {
  UniqueViolation = '23505'
}
```
- Việc còn lại là triển khai login
```ts
// authentication/authentication.service.ts
export class AuthenticationService {
  constructor(
    private readonly usersService: UsersService
  ) {}
 
  // (...)
 
  public async getAuthenticatedUser(email: string, hashedPassword: string) {
    try {
      const user = await this.usersService.getByEmail(email);
      const isPasswordMatching = await bcrypt.compare(
        hashedPassword,
        user.password
      );
      if (!isPasswordMatching) {
        throw new HttpException('Wrong credentials provided', HttpStatus.BAD_REQUEST);
      }
      user.password = undefined;
      return user;
    } catch (error) {
      throw new HttpException('Wrong credentials provided', HttpStatus.BAD_REQUEST);
    }
  }
}
```
- Code ở trên đều trả về 1 lỗi dù email hoặc password sai. Làm như vậy sẽ ngăn chặn được một số cuộc tấn công nhắm đến danh sách email đã đăng ký trong CSDL
- Chúng ta cũng có thể refactor đoạn code trên tách riêng phần xác minh password
```ts

public async getAuthenticatedUser(email: string, plainTextPassword: string) {
  try {
    const user = await this.usersService.getByEmail(email);
    await this.verifyPassword(plainTextPassword, user.password);
    user.password = undefined;
    return user;
  } catch (error) {
    throw new HttpException('Wrong credentials provided', HttpStatus.BAD_REQUEST);
  }
}
 
private async verifyPassword(plainTextPassword: string, hashedPassword: string) {
  const isPasswordMatching = await bcrypt.compare(
    plainTextPassword,
    hashedPassword
  );
  if (!isPasswordMatching) {
    throw new HttpException('Wrong credentials provided', HttpStatus.BAD_REQUEST);
  }
}
```
# Integrating our authentication with Passport
- Passport cung cấp cho chúng ta 1 sự trừu tượng về xác thực, giúp chúng ta đỡ các công việc nặng nhọc
- Các ứng dụng có cách tiếp cận khác nhau để xác thực. Passport gọi những cơ chế đó là `strategies`. Đầu tiên hãy thử `passport-local` - Xác thực người dùng bằng username & password
```ts
npm install @nestjs/passport passport @types/passport-local passport-local @types/express
```
- Để setting 1 strategy, chúng ta cần cung cấp các option cụ thể cho 1 strategy. Trong NestJs, chúng ta thực hiện nó bằng cách extend class `PassportStrategy`
```ts
// authentication/local.strategy.ts
import { Strategy } from 'passport-local';
import { PassportStrategy } from '@nestjs/passport';
import { Injectable } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
import User from '../users/user.entity';
 
@Injectable()
export class LocalStrategy extends PassportStrategy(Strategy) {
  constructor(private authenticationService: AuthenticationService) {
    super({
      usernameField: 'email'
    });
  }
  async validate(email: string, password: string): Promise<User> {
    return this.authenticationService.getAuthenticatedUser(email, password);
  }
}
```
- Đối với mỗi strategy, Passport gọi hàm xác thực bằng cách sử dụng các tham số cụ thể. Đối với local, Passport cần 1 method có tên username và password. Trong trường hợp này, email đóng vai trò là username
- Chúng ta cần cấu hình `AuthenticationModule` để sử dụng passport
```ts
// authentication/authentication.module.ts
import { Module } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
import { UsersModule } from '../users/users.module';
import { AuthenticationController } from './authentication.controller';
import { PassportModule } from '@nestjs/passport';
import { LocalStrategy } from './local.strategy';
 
@Module({
  imports: [UsersModule, PassportModule],
  providers: [AuthenticationService, LocalStrategy],
  controllers: [AuthenticationController]
})
export class AuthenticationModule {}
```
## Using built-in Passport Guards
- Module trên sử dụng AuthenticationController. Bây giờ chúng ta hãy tạo những điều cơ bản của nó
- Chúng ta sử dụng `Guards`. Guard chịu trách nhiệm xác định router handler có xử lý request không. Về bản chất, nó tương tự như middleware ExpressJs nhưng mạnh hơn
```ts
// authentication/authentication.controller.ts
import { Body, Req, Controller, HttpCode, Post, UseGuards } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
import RegisterDto from './dto/register.dto';
import RequestWithUser from './requestWithUser.interface';
import { LocalAuthenticationGuard } from './localAuthentication.guard';
 
@Controller('authentication')
export class AuthenticationController {
  constructor(
    private readonly authenticationService: AuthenticationService
  ) {}
 
  @Post('register')
  async register(@Body() registrationData: RegisterDto) {
    return this.authenticationService.register(registrationData);
  }
 
  @HttpCode(200)
  @UseGuards(LocalAuthenticationGuard)
  @Post('log-in')
  async logIn(@Req() request: RequestWithUser) {
    const user = request.user;
    user.password = undefined;
    return user;
  }
}
```
```ts
// authentication/localAuthentication.guard.ts
import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';
 
@Injectable()
export class LocalAuthenticationGuard extends AuthGuard('local') {}
```
  - Truyền trực tiếp tên strategy vào `AuthGuard` có thể coi là cách tiếp cận không tốt. Thay vào đó, chúng ta nên tạo class riêng
```ts
// authentication/requestWithUser.interface.ts
import { Request } from 'express';
import User from '../users/user.entity';
 
interface RequestWithUser extends Request {
  user: User;
}
 
export default RequestWithUser;
```
- Route `log-in` đã được Passport xử lý. Data người dùng được đính kèm vào request và đây là lý do mở rộng Request Interface
# Using JSON Web Tokens
- Chúng ta muốn hạn chế 1 số phần của ứng dụng - chỉ những người đã xác thực mới được vào ứng dụng. Chúng ta không muốn họ phải xác thực cho mọi request. Thay vào đó, chúng ta cần 1 cách để người dùng chỉ ra rằng họ đã login thành công
- Một cách đơn giản để thực hiện là sử dụng JSON Web Token. JWT là 1 chuỗi được tạo trên server bằng secret key và chỉ chúng tôi mới có thể giải mã được. Chúng tôi muốn cung cấp cho người dùng khi login có thể gửi lại cho mỗi request, chúng tôi có thể tin tưởng vào danh tính người dùng
```ts
npm install @nestjs/jwt passport-jwt @types/passport-jwt cookie-parser @types/cookie-parser
```
- Đầu tiên chúng ta cần thêm 2 biến mới là `JWT_SECRET` và `JWT_EXPIRATION_TIME`.
- Có thể dùng bất cứ chuỗi nào làm secret key, quan trọng là phải giữ bí mật và không share nó - nên mã hoá nó
- Thêm phần thời gian hết hạn tính bằng giây để tăng tính bảo mật. Nếu token bị lấy mất, hacker có thể truy cập như có mật khẩu
```ts
// app.module.ts
ConfigModule.forRoot({
  validationSchema: Joi.object({
    //...
    JWT_SECRET: Joi.string().required(),
    JWT_EXPIRATION_TIME: Joi.string().required(),
  })
})
```
## Generating tokens
- Trong bài này, chúng tôi muốn người dùng lưu trữ JWT trong `cookies`. Có 1 số lợi thế nhất định so với việc lưu status code vào bộ nhớ web nhờ vào `HttpOnly`
- Không thể truy cập trực tiếp Js thông qua browser, giúp nó an toàn hơn và chống lại các `cross-site scripting`
- Bây giờ chúng ta hãy cấu hình `JwtModule`
```ts
// authentication/authentication.module.ts
import { Module } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
import { UsersModule } from '../users/users.module';
import { AuthenticationController } from './authentication.controller';
import { PassportModule } from '@nestjs/passport';
import { LocalStrategy } from './local.strategy';
import { JwtModule } from '@nestjs/jwt';
import { ConfigModule, ConfigService } from '@nestjs/config';
 
@Module({
  imports: [
    UsersModule,
    PassportModule,
    ConfigModule,
    JwtModule.registerAsync({
      imports: [ConfigModule],
      inject: [ConfigService],
      useFactory: async (configService: ConfigService) => ({
        secret: configService.get('JWT_SECRET'),
        signOptions: {
          expiresIn: `${configService.get('JWT_EXPIRATION_TIME')}s`,
        },
      }),
    }),
  ],
  providers: [AuthenticationService, LocalStrategy],
  controllers: [AuthenticationController]
})
export class AuthenticationModule {}
```
- Và giờ chúng ta có thể sử dụng JwtService trong AuthenticationService
```ts
// authentication/authentication.service.ts
@Injectable()
export class AuthenticationService {
  constructor(
    private readonly usersService: UsersService,
    private readonly jwtService: JwtService,
    private readonly configService: ConfigService
  ) {}
 
  // ...
 
  public getCookieWithJwtToken(userId: number) {
    const payload: TokenPayload = { userId };
    const token = this.jwtService.sign(payload);
    return `Authentication=${token}; HttpOnly; Path=/; Max-Age=${this.configService.get('JWT_EXPIRATION_TIME')}`;
  }
}
```
```ts
// authentication/tokenPayload.interface.ts
interface TokenPayload {
  userId: number;
}
```
- Chúng ta cần gửi token được tạo bởi method `getCookieWithJwtToken` khi người dùng đăng nhập thành công. Chúng ta thực hiện bằng cách gửi Set-cookie header. Để thực hiện, chúng ta cần sử dụng trực tiếp object Response
```ts
@HttpCode(200)
@UseGuards(LocalAuthenticationGuard)
@Post('log-in')
async logIn(@Req() request: RequestWithUser, @Res() response: Response) {
  const {user} = request;
  const cookie = this.authenticationService.getCookieWithJwtToken(user.id);
  response.setHeader('Set-Cookie', cookie);
  user.password = undefined;
  return response.send(user);
}
```
- Khi trình duyệt nhận request này, nó sẽ thiết lập cookie để sử dụng sau
## Receiving tokens
- Để đọc cookie 1 cách dễ dàng, chúng ta sử dụng `cookie-parser`
```ts
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as cookieParser from 'cookie-parser';
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.use(cookieParser());
  await app.listen(3000);
}
bootstrap();
```
- Bây giờ, chúng ta cần đọc token từ Cookie header khi người dùng request data. Để làm được điều đó, chúng ta cần 1 strategy passport thứ 2
```ts
// authentication/jwt.strategy.ts
import { ExtractJwt, Strategy } from 'passport-jwt';
import { PassportStrategy } from '@nestjs/passport';
import { Injectable } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';
import { Request } from 'express';
import { UsersService } from '../users/users.service';
import TokenPayload from './tokenPayload.interface';
 
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor(
    private readonly configService: ConfigService,
    private readonly userService: UsersService,
  ) {
    super({
      jwtFromRequest: ExtractJwt.fromExtractors([(request: Request) => {
        return request?.cookies?.Authentication;
      }]),
      secretOrKey: configService.get('JWT_SECRET')
    });
  }
 
  async validate(payload: TokenPayload) {
    return this.userService.getById(payload.userId);
  }
}
```
- Ở trên, chúng tôi đã extend default JWT strategy mặc định bằng cách đọc token từ cookie. Khi chúng ta truy cập thành công vào token, chúng ta sử dụng id của người dùng được mã hoá bên trong. Với nó chúng ta có thể lấy được toàn bộ dữ liệu người dùng thông qua method `userService.getById()`. Chúng ta cần thêm nó vào UserService của mình
```ts
// users/users.service.ts
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>
  ) {}
 
  async getById(id: number) {
    const user = await this.usersRepository.findOne({ id });
    if (user) {
      return user;
    }
    throw new HttpException('User with this id does not exist', HttpStatus.NOT_FOUND);
  }
 
  // (...)
}
```
- Nhờ method `validate` chạy ngầm khi token được mã hoá, chúng tôi có thể truy cập vào tất cả dữ liệu người dùng
- Bây giờ, chúng ta có thể thêm `JwtStrategy` mới của mình vào AuthenticationModule
```ts
// authentication/authentication.module.ts
@Module({
  // (...)
  providers: [AuthenticationService, LocalStrategy, JwtStrategy]
})
export class AuthenticationModule {}
```
## Requiring authentication from our users
- Bây giờ, chúng ta có thể yêu cầu người dùng xác thực khi gửi request đến API của chúng ta. Để làm như vậy trước tiên chúng ta cần tạo `JWTAuthenticationGuard`
```ts
authentication/jwt-authentication.guard.ts
import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';
 
@Injectable()
export default class JwtAuthenticationGuard extends AuthGuard('jwt') {}
```
- Bây giờ chúng ta có thể sử dụng nó mỗi khi chúng ta muốn người dùng xác thực trước khi request. Ví dụ chúng ta có thể muốn làm như vậy khi tạo bài post thông qua API của mình
```ts
// posts/posts.controller.ts
import { Body, Controller Post, UseGuards } from '@nestjs/common';
import PostsService from './posts.service';
import CreatePostDto from './dto/createPost.dto';
import JwtAuthenticationGuard from '../authentication/jwt-authentication.guard';
 
@Controller('posts')
export default class PostsController {
  constructor(
    private readonly postsService: PostsService
  ) {}
 
  @Post()
  @UseGuards(JwtAuthenticationGuard)
  async createPost(@Body() post: CreatePostDto) {
    return this.postsService.createPost(post);
  }
 
  // (...)
}
```
# Logging out
- JWT là stateless. Chúng ta không thể thay đổi token thành không hợp lệ theo cách đơn giản. Các dễ nhất để thực hiện logout là xoá token khỏi browser. Vì chúng tôi thiết kế là `HttpOnly` nên chúng tôi cần tạo endpoint để xoá cookie này
```ts
// authentication/authentication.service.ts
export class AuthenticationService {
  // (...)
 
  public getCookieForLogOut() {
    return `Authentication=; HttpOnly; Path=/; Max-Age=0`;
  }
}
```
```ts
// authentication/authentication.controller.ts
@Controller('authentication')
export class AuthenticationController {
  // (...)
  @UseGuards(JwtAuthenticationGuard)
  @Post('log-out')
  async logOut(@Req() request: RequestWithUser, @Res() response: Response) {
    response.setHeader('Set-Cookie', this.authenticationService.getCookieForLogOut());
    return response.sendStatus(200);
  }
}
```
# Verifying tokens
- Một chức năng quan trọng cần bổ sung là xác minh JWT và trả về data người dùng. Bằng cách đó, trình duyệt có thể kiểm tra xem token hiện tại có hợp lệ hay không và lấy dữ liệu của người dùng đang đăng nhập
```ts
@Controller('authentication')
export class AuthenticationController {
  // (...)
  @UseGuards(JwtAuthenticationGuard)
  @Get()
  authenticate(@Req() request: RequestWithUser) {
    const user = request.user;
    user.password = undefined;
    return user;
  }
}
```
# Summary
- Trong bài viết này, chúng ta đã đề cập đến việc login, logout. Để thực hiện chúng, chúng tôi đã sử dụng bcrypt để hash password để bảo mật chúng. Để xác thực người dùng, chúng tôi đã sử dụng JWT. Vẫn còn nhiều cách để cải thiện tính năng trên
