> https://wanago.io/2020/06/08/api-nestjs-serializing-response-interceptors/
# Serializing response interceptors
- Đôi khi chúng ta cần thực hiện các thao tác bổ sung trên dữ liệu đầu ra. Chúng ta có thể không muốn phơi bày các property cụ thể hoặc sửa đổi response theo 1 cách nào đó khác. Hãy cùng tìm hiểu cách để có thể làm được điều đó

# Serialization
- Điều đầu tiên cần xem xét là serialization (tuần tự hoá). Đây là quá trình chuyển đổi dữ liệu response trước khi trả về người dùng
- Trong các phần trước của loạt bài này, chúng ta đã xoá mật khẩu trong nhiều phần khác nhau của API. Một cách tiếp cận tốt hơn sẽ là sử dụng `class-transformer`
```ts
// users/user.entity.ts
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
import { Exclude } from 'class-transformer';
 
@Entity()
class User {
  @PrimaryGeneratedColumn()
  public id?: number;
 
  @Column({ unique: true })
  public email: string;
 
  @Column()
  public name: string;
 
  @Column()
  @Exclude()
  public password: string;
}
 
export default User;
```
- NestJs có sẵn `ClassSerializerInterceptor` sử dụng class-transformer bên trong. Để sử dụng transformation trên, chúng ta cần sử dụng nó ở trong controller của mình
```ts
@Controller('authentication')
@UseInterceptors(ClassSerializerInterceptor)
class AuthenticationController
```
- Nếu chúng ta cần thêm nó vào nhiều controller, chúng ta có thể cấu hình trên global
```ts
main.ts
import { NestFactory, Reflector } from '@nestjs/core';
import { AppModule } from './app.module';
import * as cookieParser from 'cookie-parser';
import { ClassSerializerInterceptor, ValidationPipe } from '@nestjs/common';
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(new ValidationPipe());
  app.useGlobalInterceptors(new ClassSerializerInterceptor(
    app.get(Reflector))
  );
  app.use(cookieParser());
  await app.listen(3000);
}
bootstrap();
```
- Theo mặc định, tất cả các entities của chúng ta đều được hiểu thị. Chúng ta có thể thay đổi bằng cách cung cấp các option bổ sung cho class-transformer. Để làm như vậy, chúng ta cần sử dụng decorator `@SerializeOption()`
```ts
@Controller('authentication')
@SerializeOptions({
  strategy: 'excludeAll'
})
export class AuthenticationController

// users/user.entity.ts
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
import { Expose } from 'class-transformer';
 
@Entity()
class User {
  @PrimaryGeneratedColumn()
  public id?: number;
 
  @Column({ unique: true })
  @Expose()
  public email: string;
 
  @Column()
  @Expose()
  public name: string;
 
  @Column()
  public password: string;
}
 
export default User;
```
- Decorator `@SerializeOptions()` có nhiều option hơn mà bạn có thể thấy hữu ích. Nó khớp với các option mà bạn có thể cung cấp cho method `classToPlain` trong `class-transformer`
- class-transformer library có khá nhiều tính năng hữu ích. Một tính năng đáng chú ý khác là khả năng chuyển đổi giá trị. Để test thử, chúng ta hãy tạo 1 cột có thể null
```ts
@Entity()
class Post {
  // ...
 
  @Column({ nullable: true })
  public category?: string;
}
```
- Vì category có thể null nên sẽ trả về null trong response
- Hành vi trên có thể được coi là không mong muốn và cách đơn giản nhất để khắc phục là sử dụng `@Transform` bằng null. Nếu là null thì không gửi response
```ts
@Column({ nullable: true })
@Transform(value => {
  if (value !== null) {
    return value;
  }
})
public category?: string;
```
## Issues with using the @Res() decorator
- Trong phần trước của loạt bài này, chúng ta đã sử dụng decorator `@Res()` để truy cập Express Response object. Nhờ đó chúng ta có thể đính kèm cookie vào response
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
- Sử dụng decorator `@Res()` sẽ loại bỏ 1 số lợi thế khi sử dụng NestJs. Thật không may nó lại can thiệp vào `ClassSerialzerInterceptor`. Để ngăn chặn điều đó chúng ta nên làm theo lời khuyên của người tạo ra nest. Nếu chúng ta sử dụng object request.res thay vì decorator `@Res()`, chúng ta sẽ không dưa NestJs vào chế độ express-specific
```ts

@HttpCode(200)
@UseGuards(LocalAuthenticationGuard)
@Post('log-in')
async logIn(@Req() request: RequestWithUser) {
  const {user} = request;
  const cookie = this.authenticationService.getCookieWithJwtToken(user.id);
  request.res.setHeader('Set-Cookie', cookie);
  return user;
}
```
# Custom interceptors
- Ở trên chúng ta đã sử dụng `@Transform` để bỏ qua 1 property duy nhất nếu nó bằng null. Làm như vậy đối với mọi property có thể null có vẻ không phải là cách tiếp cận rõ ràng
- May mắn thay, ngoài việc sử dụng `ClassSerializerInterceptor`, chúng ta có thể tạo ra các interceptor của riêng mình. Interceptor có thể phục vụ nhiều mục đích khác nhau và trong số đó là thao tác request/response
```ts
// utils/excludeNull.interceptor.ts
import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from '@nestjs/common';
import { Observable } from 'rxjs';
import { map } from 'rxjs/operators';
import recursivelyStripNullValues from './recursivelyStripNullValues';
 
@Injectable()
export class ExcludeNullInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    return next
      .handle()
      .pipe(map(value => recursivelyStripNullValues(value)));
  }
}
```
- Mỗi interceptor cần phải triển khai NestInterceptor và do đó, method intercept cần 2 đối số
  - `ExecutionContext`: Cung cấp thông tin về context hiệ tại
  - `CallHandler`: Nó chứa method xử lý gọi router handler và trả về 1 `RxJs Observable`
- Method `intercept` bao bọc luồn request/response và chúng ta có thể thêm logic trước và sau khi thực thi route handler. Trong đoạn code trên, chúng ta gọi router handle và sửa đổi response
- Vì có khá nhiều nơi trong NestJs sử dụng `RxJs` nên trình khởi chạy Ts chính thức đã sử dụng công cụ này
```ts
// utils/recursivelyStripNullValues.ts
function recursivelyStripNullValues(value: unknown): unknown {
  if (Array.isArray(value)) {
    return value.map(recursivelyStripNullValues);
  }
  if (value !== null && typeof value === 'object') {
    return Object.fromEntries(
      Object.entries(value).map(([key, value]) => [key, recursivelyStripNullValues(value)])
    );
  }
  if (value !== null) {
    return value;
  }
}
```
- Trong hàm trên, chúng ta duyệt đệ quy cấu trúc dữ liệu và chỉ bảo toàn các giá trị nếu chúng khác với null. Nó hoạt động với cả mảng và object thuần tuý

# Summary
- Trong bài viết này, chúng ta đã xem xét cách chúng ta có thể sửa response mà chúng tôi gửi lại cho người dùng. Mặc dù cách đơn giản nhất để thực hiện là sử dụng `ClassSerializerInterceptor`, chúng ta cũng có thể tạo interceptor của riêng. Chúng ta cũng đã xem xét cách để có thể bỏ qua vấn đề sử dụng `@Res()`
