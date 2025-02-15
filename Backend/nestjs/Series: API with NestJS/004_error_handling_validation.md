> https://wanago.io/2020/06/01/api-nestjs-error-handling-validation/
# Error handling and data validation
- NestJs nổi tiếng khi nói đến việc xác thực và xử lý data, phần lớn là sử dụng decorators. Chúng ta hãy cùng tìm hiểu các tính năng mà NestJs cung cấp chẳng hạn như Exception filter và Validation pipes
# Exception filters
- Nest có exception filter xử lý các lỗi trong ứng dụng. Bất cứ khi nào chúng ta không tự xử lý exception, exception filter sẽ thực hiện điều đó thay chúng ta. Nó xử lý exception và gửi nó dưới dạng response theo định dạng thân thiện với người dùng
- Exception filters mặc định gọi là `BaseExceptionFilter`. Chúng ta có thể xem source của NestJs và kiểm tra hành vi của nó
```ts
nest/packages/core/exceptions/base-exception-filter.ts
export class BaseExceptionFilter<T = any> implements ExceptionFilter<T> {
  // ...
  catch(exception: T, host: ArgumentsHost) {
    // ...
    if (!(exception instanceof HttpException)) {
      return this.handleUnknownError(exception, host, applicationRef);
    }
    const res = exception.getResponse();
    const message = isObject(res)
      ? res
      : {
          statusCode: exception.getStatus(),
          message: res,
        };
    // ...
  }
 
  public handleUnknownError(
    exception: T,
    host: ArgumentsHost,
    applicationRef: AbstractHttpAdapter | HttpServer,
  ) {
    const body = {
      statusCode: HttpStatus.INTERNAL_SERVER_ERROR,
      message: MESSAGES.UNKNOWN_EXCEPTION_MESSAGE,
    };
    // ...
  }
}
```
- Mỗi khi có lỗi trong ứng dụng của chúng ta, method `catch` sẽ chạy. Có 1 vài điều cần thiết mà chúng ta có thể nhận được từ đoạn code trên
## HttpException
- Nest mong đợi chúng ta sử dụng class HttpException. Nếu không nó sẽ diễn giải lỗi là không cố ý phản hồi bằng lỗi 500
- Chúng ta đã sử dụng khá nhiều HttpException trong loạt bài này
```ts
throw new HttpException('Post not found', HttpStatus.NOT_FOUND);
```
- Nhận 2 đối số bắt buộc: Body response & status code. Đối với phàn sau, chúng ta có thể sử dụng HttpStatus enum được cung cấp
- Nếu chúng ta cung cấp 1 chuỗi làm định nghĩa cho response, NestJs sẽ tuần tự hoá nó thành object chứa 2 thuộc tính
  - `statusCode`: Chứa code HTTP đã chọn
  - `message`: Mô tả mà chúng ta đã cung cấp
- Chúng ta thường thấy mình đưa ra những ngoại lệ tương tự nhau nhiều lần. Để tránh lặp lại, chúng ta có thể custom lại. Để làm được chúng ta cần extend class HttpException
```ts
// posts/exception/postNotFund.exception.ts
import { HttpException, HttpStatus } from '@nestjs/common';
 
class PostNotFoundException extends HttpException {
  constructor(postId: number) {
    super(`Post with id ${postId} not found`, HttpStatus.NOT_FOUND);
  }
}
```
- `PostNotFoundException` custom của chúng ta gọi constructor của `HttpException`. Do đó, chúng ta có thể dọn dẹp code của mình bằng cách không phải định nghĩa thông báo mỗi khi chúng ta muốn đưa ra lỗi
- NestJs có 1 tập hợp các exception extend `HttpException`. Một trong số đó là `NotFoundException`. Chúng ta có thể cấu trúc lại code trên và sử dụng nó
```ts
// posts/exception/postNotFund.exception.ts
import { NotFoundException } from '@nestjs/common';
 
class PostNotFoundException extends NotFoundException {
  constructor(postId: number) {
    super(`Post with id ${postId} not found`);
  }
}

```
- Đối số đầu tiên của class NotFoundException là 1 thuộc tính bổ sung. Theo cách này, thông báo của chúng ta sẽ được định nghĩa bởi NotFoundException dựa trên trạng thái
## Extending the BaseExceptionFilter
- `BaseExceptionFilter` mặc định có thể xử lý hầu hết các trường hợp thông thường. Tuy nhiên, chúng ta có thể muốn sửa đổi nó theo 1 cách nào đó. Cách dễ nhất là tạo ra 1 filter mới và extend lại nó
```ts
// utils/exceptionsLogger.filter.ts
import { Catch, ArgumentsHost } from '@nestjs/common';
import { BaseExceptionFilter } from '@nestjs/core';
 
@Catch()
export class ExceptionsLoggerFilter extends BaseExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    console.log('Exception thrown', exception);
    super.catch(exception, host);
  }
}
```
- Decorator `@Catch()` có nghĩa là chúng ta muốn filter bắt được tất cả các exception. Chúng ta có thể cung cấp cho nó 1 exception duy nhất hoặc 1 danh sách
- AgrumentHost cung cấp cho chúng ta quyền truy cập vào context thực thi của ứng dụng - chúng ta sẽ tìm hiểu sau
- Chúng ta có thể sử dụng filter mới theo 3 cách. Đầu tiên là sử dụng global trong tất cả các router thông qua `app.useGlobalFilters`
```ts
// main.ts
import { HttpAdapterHost, NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as cookieParser from 'cookie-parser';
import { ExceptionsLoggerFilter } from './utils/exceptionsLogger.filter';
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
 
  const { httpAdapter } = app.get(HttpAdapterHost);
  app.useGlobalFilters(new ExceptionsLoggerFilter(httpAdapter));
 
  app.use(cookieParser());
  await app.listen(3000);
}
bootstrap();
```
- Một cách tốt hơn để inject filter của chúng ta trên global là thêm nó vào `AppModule` của chúng ta. Nhờ đó, chúng ta có thể inject các dependency bổ sung vào filter của mình
```ts
import { Module } from '@nestjs/common';
import { ExceptionsLoggerFilter } from './utils/exceptionsLogger.filter';
import { APP_FILTER } from '@nestjs/core';
 
@Module({
  // ...
  providers: [
    {
      provide: APP_FILTER,
      useClass: ExceptionsLoggerFilter,
    },
  ],
})
export class AppModule {}
```
- Cách thứ 3 để liên kết filter là đính kèm decorator @UseFilters. Chúng ta có thể cung cấp cho nó filter duy nhất hoặc danh sách các filter
```ts
@Get(':id')
@UseFilters(ExceptionsLoggerFilter)
getPostById(@Param('id') id: string) {
  return this.postsService.getPostById(Number(id));
}
```
- Cách trên không phải cách tốt nhất để ghi log exception. NestJs có tích hợp Logger, chúng ta sẽ tìm hiểu sau
## Implementing the ExceptionFilter interface
- Nếu chúng ta cần 1 hành vi tuỳ chỉnh hoàn toàn cho các lỗi, chúng ta có thể xây dựng filter của mình từ đầu. Cần phải implement `ExceptionFilter`
```ts
import { ExceptionFilter, Catch, ArgumentsHost, NotFoundException } from '@nestjs/common';
import { Request, Response } from 'express';
 
@Catch(NotFoundException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: NotFoundException, host: ArgumentsHost) {
    const context = host.switchToHttp();
    const response = context.getResponse<Response>();
    const request = context.getRequest<Request>();
    const status = exception.getStatus();
    const message = exception.getMessage();
 
    response
      .status(status)
      .json({
        message,
        statusCode: status,
        time: new Date().toISOString(),
      });
  }
}
```
- Ở trên, vì chúng ta sử dụng decorator `@Catch(NotFoundException)`, filter này chỉ chạy cho NotFoundException
- Method `host.switchToHttp` trả về object HttpAgrumentHost có thông tin về context Http
# Validation
- Để validate dữ liệu, chúng ta cần sử dụng thư viện `class-validator`. NestJs đi kèm với `pipes` tích hợp sẵn. Các pipe thường được sử dụng để chuyển đổi dữ liệu đầu vào hoặc xác thực dữ liệu đó
- Để bắt đầu validate data, chúng ta cần `ValidationPipe`
```ts
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as cookieParser from 'cookie-parser';
import { ValidationPipe } from '@nestjs/common';
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(new ValidationPipe());
  app.use(cookieParser());
  await app.listen(3000);
}
bootstrap();
```
- Trong phần đầu của loạt bài, chúng ta đã tạo DTO. Chúng xác định định dạng data được gửi trong request. Chúng là nơi hoàn hảo để đính kèm validate
```ts
npm install class-validator class-transformer
```
- Để `ValidationPipe` hoạt động, chúng ta cần thư viện class-transformer
```ts
// auth/dto/register.dto.ts
import { IsEmail, IsString, IsNotEmpty, MinLength } from 'class-validator';
 
export class RegisterDto {
  @IsEmail()
  email: string;
 
  @IsString()
  @IsNotEmpty()
  name: string;
 
  @IsString()
  @IsNotEmpty()
  @MinLength(7)
  password: string;
}
 
export default RegisterDto;
```
- Nhờ vào việc chúng ta sử dụng `RegisterDto` ở trên với decorator @Body(), `ValidationPipe` hiện sẽ kiểm tra dữ liệu
```ts
@Post('register')
async register(@Body() registrationData: RegisterDto) {
  return this.authenticationService.register(registrationData);
}
```
## Validating params
- Chúng ta cũng có thể sử dụng `class-validator` để xác thực tham số
```ts
utils/findOneParams.ts
import { IsNumberString } from 'class-validator';
 
class FindOneParams {
  @IsNumberString()
  id: string;
}
@Get(':id')
getPostById(@Param() { id }: FindOneParams) {
  return this.postsService.getPostById(Number(id));
}
```
- Chúng ta không sử dụng `@Param('id')` ở đây, thay vào đó chúng ta sẽ giải cấu trúc vào toàn bộ prams object
# Handling PATCH
- Cách trực tiếp nhất để xử lý PATCH là truyền `skipMissingProperties` vào `ValidationPipe` của chúng ta
```ts
app.useGlobalPipes(new ValidationPipe({ skipMissingProperties: true }))
```
- Việc này sẽ bỏ qua các property bị thiếu trong tất cả các DTO. Chúng ta không muốn làm điều đó khi tạo mới. Thay vào đó chúng ta có thể thêm `IsOptional` vào tất cả các property khi cập nhật
```ts
import { IsString, IsNotEmpty, IsNumber, IsOptional } from 'class-validator';
 
export class UpdatePostDto {
  @IsNumber()
  @IsOptional()
  id: number;
 
  @IsString()
  @IsNotEmpty()
  @IsOptional()
  content: string;
 
  @IsString()
  @IsNotEmpty()
  @IsOptional()
  title: string;
}
```
- Cách trên chưa phải cách clean nhất, chúng ta sẽ tìm hiểu thêm sau
# Summary
- Trong bài này, chúng ta đã tìm hiểu cách xử lý lỗi và validate trong NestJs, sử dụng ValidationPipe để validate
