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
