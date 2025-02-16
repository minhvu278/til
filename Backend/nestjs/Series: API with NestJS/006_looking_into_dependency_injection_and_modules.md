> https://wanago.io/2020/06/15/api-with-nestjs-6-looking-into-dependency-injection-and-modules/
# Looking into dependency injection and modules
-  NestJs cố gắng tập chung vào khả năng maintain và test của code. Để làm như vậy, nó triển khai nhiều cơ chế khác nhau như DI. Trong bài này, chúng ta sẽ kiểm tra cách NestJs có thể giải quyết các dependency bằng cách xem xét đầu ra của TS. Chúng tôi cũng nỗ lực tìm hiểu kiến trúc modul mà NestJs được xây dựng

# Reasons to implement Dependency Injection
- Đây là ví dụ về TS Express. Nó áp dụng cách tiếp cận khá đơn giản để giải quyết các dependencies
```ts
import { Router } from 'express';
import Controller from '../interfaces/controller.interface';
import AuthenticationService from './authentication.service';
 
class AuthenticationController implements Controller {
  public path = '/auth';
  public router = Router();
  public authenticationService = new AuthenticationService();
 
  // (...)
}
```
- Thật không may, có 1 vài nhược điểm đối với những điều trên. Mỗi khi chúng ta tạo 1 phiên bản của `AuthenicationController` chúng ta cũng tạo 1 `AuthenticationService` mới. Nếu chúng ta sử dụng phương pháp trên trong tất cả các controller cần `AuthenticationService`, mỗi controller sẽ nhận được 1 phiên bản riêng. Có thể khó maintain theo thời gian
- Ngoài ra khả năng test bị ảnh hưởng. Mặc dù có thể mô phỏng AuthenticationService trước khi khởi tạo controller ở trên nhưng đây không phải là giải pháp lý tưởng
- Một trong những nguyên tắc SOLID được gọi là IoC. Nguyên tắc này nêu rằng các module cấp cao không nên phụ thuộc vào các module cấp thấp. Cách đơn giản để đạt được điều đó là tạo ra các phiên bản phụ thuộc trước, sau đó cung cấp chúng thông qua 1 hàm tạo
```ts
import { Router } from 'express';
import Controller from '../interfaces/controller.interface';
import AuthenticationService from './authentication.service';
 
class AuthenticationController implements Controller {
  public path = '/auth';
  public router = Router();
  public authenticationService: AuthenticationService;
 
  constructor(authenticationService: AuthenticationService) {
    this.authenticationService = authenticationService;
  }
 
  // (...)
}
const authenticationService = new AuthenticationService();
 
const authenticationController = new AuthenticationController(
  authenticationService
);
```
- Mặc dù cách trên có thể giúp chúng ta khắc phục những vấn đề đã nêu, nhưng nó lại không hề tiện. Đây là lý do NestJs triển khai cơ chế DI cung cấp tất cả các dependency cần thiết 1 cách tự động

# Dependency Injection in NestJS under the hood
- Hãy cùng xem xét 1 controller tương tự mà chúng tôi đã xây dựng trong phần 3 
```ts
import { Controller, } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
 
@Controller('authentication')
export class AuthenticationController {
  constructor(
    private readonly authenticationService: AuthenticationService
  ) {}
  
  // (...)
}
```
  - Nhờ sử dụng `private readonly`, chúng ta không cần gán `authenticationService` trong phần thân của constructor
- `@Controller` đảm bảo rằng dữ liệu về class của chúng ta được lưu. `@Injectable` cũng thực hiện việc này
```ts
import { Injectable } from '@nestjs/common';
import { UsersService } from '../users/users.service';
import { JwtService } from '@nestjs/jwt';
import { ConfigService } from '@nestjs/config';
 
@Injectable()
export class AuthenticationService {
  constructor(
    private readonly usersService: UsersService,
    private readonly jwtService: JwtService,
    private readonly configService: ConfigService
  ) {}
 
  // (...)
}

```
- TS compiler phát ra metadata mà NestJs sau này có thể sử dụng để tìm ra những dependencies nào chúng ta cần. Hãy cùng kiểm tra đầu ra của AuthenticationService
```ts
AuthenticationService = __decorate([
    common_1.Injectable(),
    __metadata("design:paramtypes", [users_service_1.UsersService,
        jwt_1.JwtService,
        config_1.ConfigService])
], AuthenticationService);
```
- `design:paramtypes` là key mô tả parameter type metadata. Nhờ đó, chúng ta có thể có được 1 mảng các tham chiếu đến các class mà chúng ta cần trong constructor của `AuthenticationService`. Chúng ta có thể hiểu nó như việc trích xuất các dependency của `AuthenticationService` tại thời điểm biên dịch. NestJs sử dụng package `reflect-metadata` để làm việc với metadata ở trên
- Khi NestJs khởi động, nó sẽ giải quyết tất cả các metadata mà `AuthenticationController` cần. Nó có thể trở nên khá phức tạp bên trong, vì nó có thể xử lý các phụ thuộc circular

# Modules
- Là 1 thành phần của ứng dụng chứa các chức năng xoay quanh 1 tính năng cụ thể
- Mỗi ứng dụng NestJs đều có module gốc, nó đóng vai trò là điểm khởi đầu cho NestJs khi tạo ứng dụng
```ts
//app.module.ts
import { Module } from '@nestjs/common';
import { PostsModule } from './posts/posts.module';
import { ConfigModule } from '@nestjs/config';
import { DatabaseModule } from './database/database.module';
import { AuthenticationModule } from './authentication/authentication.module';
import { UsersModule } from './users/users.module';
 
@Module({
  imports: [
    PostsModule,
    ConfigModule.forRoot({
     /// ...
    }),
    DatabaseModule,
    AuthenticationModule,
    UsersModule,
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```
- NestJs sử dụng module gốc để giải quyết các module khác cùng với các dependency của nó. Ví dụ chúng ta có `AuthenticationModule` đảm nhiệm việc xác thực trong ứng dụng của chúng ta
```ts
├── authentication
│   ├── authentication.controller.ts
│   ├── authentication.module.ts
│   ├── authentication.service.ts
│   ├── dto
│   │   ├── logIn.dto.ts
│   │   └── register.dto.ts
│   ├── jwtAuthentication.guard.ts
│   ├── jwt.strategy.ts
│   ├── localAuthentication.guard.ts
│   ├── local.strategy.ts
│   ├── requestWithUser.interface.ts
│   └── tokenPayload.interface.ts
```
- Có thể thấy từ thư mục `authentication`, 1 module có thể chứa nhiều thứ. Trong trường hợp trên, nó bao gồm controller, service và 1 số file khác được kết nối với quy trình authentication
- Trong quá trình authentication, chúng ta cũng cần phải đọc và tạo user. Đóng gói quy trình này, chúng tôi đã tạo ra 1 UsersModule riêng biệt. Điều này cho thấy các module hữu ích trong việc chia ứng dụng của chúng tôi thành các phần hoạt động cùng nhau
- Hãy cùng kiểm tra cách chúng ta có thể sử dụng `UsersService` trong `AuthenticationModule`. Để làm vậy, trước tiên chúng ta cần xem xét UsersModule
```ts
// users/users.module.ts
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
- Phần quan trọng ở đây là các `providers` và `exports`
- Provider là thứ có thể chèn các dependency. Một ví dụ về điều đó là service. Chúng ta đặt `UsersService` vào `providers` array của `UsersModule` để thông báo rằng nó thuộc về module đó
- 1 module cũng có thể import các module khác bằng cách đưa `UsersService` vào mảng exports, chúng ta chỉ ra rằng module sẽ hiển thị nó. Chúng ta có thể coi nó như 1 public interface của 1 module
```ts
// authentication/authentication.module.ts
import { Module } from '@nestjs/common';
import { AuthenticationService } from './authentication.service';
import { UsersModule } from '../users/users.module';
import { AuthenticationController } from './authentication.controller';
import { LocalStrategy } from './local.strategy';
import { JwtStrategy } from './jwt.strategy';
 
@Module({
  imports: [
    UsersModule,
    // (...)
  ],
  providers: [AuthenticationService, LocalStrategy, JwtStrategy],
  controllers: [AuthenticationController]
})
export class AuthenticationModule {}
```
- Bây giờ khi chúng ta import `UsersModule` chúng ta có thể truy cập vào tất cả các providers đã export. Nhờ đó chúng ta có thể sử dụng `UsersService` trong `AuthenticationService`
- Điều quan trọng là trong NestJs, các module là các `singletons`. Điều này có nghĩa là phiên bản của UsersService được chia sẻ trên tất cả các module. Những điều trên đặc biệt quan trọng khi xem xét các kỹ thuật như in-memory caching
## The @Global() decorator
- Mặc dù việc tạo các module global có thể không được khuyến khích và được coi là tệ nhưng nó hoàn toàn có thể làm được
- Khi chúng ta muốn có 1 tập hợp các providers có sẵn ở mọi nơi, chúng ta có thể sử dụng `@Global`
```ts
@Global()
@Module({
  imports: [TypeOrmModule.forFeature([User])],
  providers: [UsersService],
  exports: [UsersService]
})
export class UsersModule {}
```
- Bây giờ chúng ta không cần phải import `UsersModule` để sử dụng `UsersService`
- Chúng ta chỉ nên register 1 module toàn cục một lần và nơi tốt nhất để thực hiện là root module
# Summary
- Đào sâu hơn vào cách NestJs hoạt động với các modile và cách giải quyết các dependency của chúng. Chúng tôi đã kiểm tra 1 chút về nguyên tắc hoạt động của DI. Tìm hiểu về 1 số cơ chế bên trong khuôn khổ có thể giúp chúng ta hiểu rõ hơn về nó và do đó, tạo ra 1 cấu trúc ứng dụng phức tạp hơn


