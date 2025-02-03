# Validate
- Cài đặt validate
```ts
npm i --save class-validator class-transformer
```
- Tạo dto để validate và sử dụng các decorator của thư viện trên. Có thể sử dụng nhiều decorator validate trên 1 field
```ts
import { IsNumber, IsString } from "class-validator";

export class CreatePropertyDto {
  @IsString()
  @Length(2, 10, {message: 'error on length'})
  name: string;
  @IsString()
  description: string;
  @IsNumber()
  area: number;
}
```
- Để sử dụng, chúng ta cần truyền vào phần body + sử dụng decorator `@UsePipes(new ValidationPipe)`
```ts
@Post()
@UsePipes(new ValidationPipe())
create(@Body() body: CreatePropertyDto) {
  return body;
}
```
- Có thể sử dụng option whitelist `@UsePipes(new ValidationPipe({ whitelist: true }))` để loại bỏ các field thừa trong body
- Cũng có thể sử dụng `forbidNonWhitelisted: true` để báo trường nào bị thừa ra
- Cũng có thể loại bỏ `@UsePipes` và đưa thẳng vào `@Body()`
```ts
@Post()
create(@Body(
  new ValidationPipe({ whitelist: true, forbidNonWhitelisted: true, groups: ['create'] })
) body: CreatePropertyDto) {
  return body;
}
```
## Validate group
- Trường hợp mà cùng 1 field mà chúng ta muốn khi create thì áp dụng 1 kiểu, update thì sử dụng 1 kiểu
- Sửa trong dto
```ts
import { IsNumber, IsString, Length } from "class-validator";

export class CreatePropertyDto {
  @IsString()
  name: string;
  @IsString()
  @Length(2, 10, {groups: ['create']})
  @Length(1, 15, {groups: ['update']})
  description: string;
  @IsNumber()
  area: number;
}
```
- Sử dụng trong controller
```ts
@Post()
create(@Body(
  new ValidationPipe({ whitelist: true, forbidNonWhitelisted: true, groups: ['create'] })
) body: CreatePropertyDto) {
  return body;
}

@Patch(':id')
update(@Body(
  new ValidationPipe({ whitelist: true, forbidNonWhitelisted: true, groups: ['update'] })
) body: CreatePropertyDto) {
  return body
}
```
- Chúng ta cũng có thể sử dụng option `alway:true` để yêu cầu luôn luôn phải xác thực
```ts
@IsString({always: true})
name: string;
```
## Validate global
- Chúng ta có thể thêm vào `main.ts` để áp dụng validate cho toàn bộ app
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { ValidationPipe } from '@nestjs/common';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true
    })
  )
  await app.listen(3000);
}
bootstrap();
```
- Cũng có thể áp dụng global cho 1 vài module cụ thể, chúng ta có thể đặt danh sách provider và bên trong danh sách này, ta truyền vào 1 object 
```ts
import { Module, ValidationPipe } from '@nestjs/common';
import { PropertyController } from './property.controller';
import { APP_PIPE } from '@nestjs/core';

@Module({
  controllers: [PropertyController],
  providers: [
    {
      provide: APP_PIPE,
      useValue: new ValidationPipe({
        whitelist: true, 
        forbidNonWhitelisted: true
      })
    }
  ]
})
export class PropertyModule {}
```
## Validation for params and search queries
- Với những trường hợp truyền id lên, phần validate của chúng ta đang nhận định nó là 1 chuỗi, nên khi chúng ta đặt là @IsNumber() sẽ gặp lỗi
```ts
import { IsInt, IsPositive } from "class-validator";

export class IdPramDto {
  @IsInt()
  @IsPositive()
  id: number;
}
```
- Để fix, ở trong validate chúng ta đặt `transform: true` và bật `enableImplicitConversion` trong transformOptions lên
```ts
import { Module, ValidationPipe } from '@nestjs/common';
import { PropertyController } from './property.controller';
import { APP_PIPE } from '@nestjs/core';

@Module({
  controllers: [PropertyController],
  providers: [
    {
      provide: APP_PIPE,
      useValue: new ValidationPipe({
        whitelist: true, 
        forbidNonWhitelisted: true,
        transform: true,
        transformOptions: {
          enableImplicitConversion: true
        }
      })
    }
  ]
})
export class PropertyModule {}
```
## Custom transform Pipes
- Chúng ta có thể tự custom được validate transform pipes bằng cách tạo ra 1 file riêng. Ví dụ chúng ta tạo ra 1 file `parseIdpipe.ts`
```ts
import { ArgumentMetadata, BadRequestException, PipeTransform } from "@nestjs/common";

export class ParseIdPipe implements PipeTransform<string, number> {
  transform(value: string, metadata: ArgumentMetadata): number {
      const val = parseInt(value, 10);
      if (isNaN(val)) throw new BadRequestException('id must be a number')
      if (val <= 0) throw new BadRequestException('id must be positive')
        return val;
  }
}
```
- Sau đó sử dụng ở bên ngoài
```ts
@Patch(':id')
update(
  @Param('id', ParseIntPine) id,
  @Body() body: CreatePropertyDto) {
  return body
}
```
- Lưu ý, trường hợp muốn sử dụng ngoài module thì cần phải sử dụng `@Injectable` - learn ở phần sau
## Validation with ZOD
- Install
```ts
npm i zod
```
