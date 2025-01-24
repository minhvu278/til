# Overview
## Install
- Cài đặt global
```ts
npm i -g @nestjs/cli
```
- Tạo 1 dự án mới
```ts
nest new tenduan
```
- Chạy dự án
```ts
npm run start:dev
```
- Tạo mới 1 module
```ts
nest g module property
```
- Tạo mới 1 controller
```ts
nest g co property
```
## Các decorator cơ bản và cách sử dụng
- `@Controller('property')` - Prefix mặc định sẽ là /property (localhost:3000/property)
- `@Get()` - Request Get
```ts
@Get()
  findAll() {
    return 'All properties';
  }
```
- `@Get(':id')` - Tìm theo tham số
- `@Param('id')` - Giá trị của tham số
- `@Query('sort')` - Lấy phần query sau ?
```ts
@Get(':id')
findOne(@Param('id', ParseIntPipe) id, @Query('sort', ParseBoolPipe) sort) {
  console.log(typeof id);
  console.log(typeof sort);
  return id;
}
```
- `@Post()` - Request Post
- `@Body()` - Body truyền lên
- `@HttpCode(202)`- Thay đổi code trả về
```ts
@Post()
@HttpCode(202)
create(@Body() body) {
  return body;
}
```
