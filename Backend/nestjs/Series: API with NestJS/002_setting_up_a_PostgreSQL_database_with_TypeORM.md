# Setting up a PostgreSQL database with TypeORM
- Điều quan trọng tiếp theo khi học cách tạo API là lưu trữ data. Trong bài viết này, chúng ta sẽ xem xét cách thực hiện điều đó với PostgreSQL và NestJs. Để quản lý CSDL thuận tiện hơn, chúng ta sử dụng `Object-relational mapping(ORM)` có tên là `TypeORM`. Để hiểu rõ hơn, chúng ta cũng xem xét một số truy vấn SQL. Bằng cách đó, chúng ta có thể nắm bắt được những lợi thế mà ORM mang lại
- Bạn có thể tìm được toàn bộ code trong link này [this repository](https://github.com/mwanago/nestjs-typescript)

# Creating a PostgreSQL database
- Cách đơn giản nhất để bắt đầu phát triển CSDL Postgres là sử dụng docker
- Đầu tiên cần làm là cài đặt [install docker](https://docs.docker.com/get-started/get-docker/) và [docker compose](https://docs.docker.com/compose/install/). Bây giờ, chúng ta cần tạo 1 file docker-compose và chạy nó
- docker-compose.yml
```ts
version: "3"
services:
  postgres:
    container_name: postgres
    image: postgres:latest
    ports:
    - "5432:5432"
    volumes:
    - /data/postgres:/data/postgres
    env_file:
    - docker.env
    networks:
    - postgres
 
  pgadmin:
    links:
    - postgres:postgres
    container_name: pgadmin
    image: dpage/pgadmin4
    ports:
    - "8080:80"
    volumes:
    - /data/pgadmin:/root/.pgadmin
    env_file:
    - docker.env
    networks:
    - postgres
 
networks:
  postgres:
    driver: bridge
```
- Điều hữu ích về cấu hình trên là nó cũng khởi động 1 pgAdmin console. Nó cho phép chúng ta xem trạng thái CSDL và tương tác với nó
- Để cung cấp thông tin xác thực được sử dụng bởi các container Docker, chúng ta cần tạo file `docker.env`
- docker.env
```ts
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin
POSTGRES_DB=nestjs
PGADMIN_DEFAULT_EMAIL=admin@admin.com
PGADMIN_DEFAULT_PASSWORD=admin
```
- Sau khi thiết lập xong tất cả các mục trên, chúng ta cần khởi động các container
```ts
docker-compose up
```
# Environment variables
- Một điều quan trọng để chạy app là thiết lập các biến môi trường. Bằng cách sử dụng chúng để lưu trữ dữ liệu cấu hình, chúng ta có thể cấu hình dễ dàng. Ngoài ra việc lưu trữ những dữ liệu nhạy cảm cũng dễ dàng hơn
- Trong Express TS, chúng tôi sử dụng 1 thư viện tên là dotenv để inject các biến của mình. Trong NestJs, chúng ta có 1 `ConfigModule` mà chúng ta có thể sử dụng trong ứng dụng của mình. Nó sử dụng dotenv ở chế độ nền
```npm install @nestjs/config
```
- app.module.ts
```ts
import { Module } from '@nestjs/common';
import { PostsModule } from './posts/posts.module';
import { ConfigModule } from '@nestjs/config';
 
@Module({
  imports: [PostsModule, ConfigModule.forRoot()],
  controllers: [],
  providers: [],
})
export class AppModule {}
```
- Ngay cả khi chúng ta tạo .env ở thư mục gốc của app, Nest sẽ đưa chúng vào ConfigService mà chúng ta sẽ sớm sử dụng
- .env
```ts
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin
POSTGRES_DB=nestjs
PORT=5000
```
## Validating environment variables
- Validate biến môi trường của chúng ta trước khi chạy ứng dụng là 1 ý tưởng tuyệt vời. Trong EP TS chúng tôi có sử dụng 1 thư viện là `envalid`
- `ConfigModule` được tích hợp sẵn trong NestJs hỗ trợ `@hapi/joi` mà chúng ta có thể sử dụng để xác định validation schema
```ts
npm install @hapi/joi @types/hapi__joi
```
- app.module.ts
```ts
import { Module } from '@nestjs/common';
import { PostsModule } from './posts/posts.module';
import { ConfigModule } from '@nestjs/config';
import * as Joi from '@hapi/joi';
 
@Module({
  imports: [
    PostsModule,
    ConfigModule.forRoot({
      validationSchema: Joi.object({
        POSTGRES_HOST: Joi.string().required(),
        POSTGRES_PORT: Joi.number().required(),
        POSTGRES_USER: Joi.string().required(),
        POSTGRES_PASSWORD: Joi.string().required(),
        POSTGRES_DB: Joi.string().required(),
        PORT: Joi.number(),
      })
    })
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```
# Connecting a NestJS application with PostgreSQL
- Điều đầu tiên chúng ta cần làm khi chúng ta chạy CSDL là xác định kết nối giữa app và CSDL. Để thực hiện, chúng ta sử dụng `TypeOrmModule`
```ts
npm install @nestjs/typeorm typeorm pg
```
- Để giữ cho code của chúng ta luôn clean, chúng ta nên tạo ra 1 module CSDL
- database.module.ts
```ts
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { ConfigModule, ConfigService } from '@nestjs/config';
 
@Module({
  imports: [
    TypeOrmModule.forRootAsync({
      imports: [ConfigModule],
      inject: [ConfigService],
      useFactory: (configService: ConfigService) => ({
        type: 'postgres',
        host: configService.get('POSTGRES_HOST'),
        port: configService.get('POSTGRES_PORT'),
        username: configService.get('POSTGRES_USER'),
        password: configService.get('POSTGRES_PASSWORD'),
        database: configService.get('POSTGRES_DB'),
        entities: [
          __dirname + '/../**/*.entity.ts',
        ],
        synchronize: true,
      })
    }),
  ],
})
export class DatabaseModule {}
```
- Một điều cần thiết ở trên là chúng ta sử dụng `ConfigModule` và `ConfigService`. Method `useFactory` có thể truy cập các biến môi trường nhờ cung cấp các mảng `imports` và `inject`. Chúng tôi sẽ trình bày chi tiết hơn về những cơ chế này trong các phần tiếp theo của loạt bài này
- Bây giờ, chúng ta cần import `DatabaseModule` của mình
- app.module.ts
```ts
import { Module } from '@nestjs/common';
import { PostsModule } from './posts/posts.module';
import { ConfigModule } from '@nestjs/config';
import * as Joi from '@hapi/joi';
import { DatabaseModule } from './database/database.module';
 
@Module({
  imports: [
    PostsModule,
    ConfigModule.forRoot({
      validationSchema: Joi.object({
        POSTGRES_HOST: Joi.string().required(),
        POSTGRES_PORT: Joi.number().required(),
        POSTGRES_USER: Joi.string().required(),
        POSTGRES_PASSWORD: Joi.string().required(),
        POSTGRES_DB: Joi.string().required(),
        PORT: Joi.number(),
      })
    }),
    DatabaseModule,
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```
# Entities
- Khái niệm quan trọng nhất cần nắm bắt khi sử dụng TypeORM là `entity`. Đây là 1 class ánh xạ đến 1 bảng CSDL. Để tạo ra nó, chúng ta sử dụng `@Entity()` decorator
- post.entity.ts
```ts

import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
 
@Entity()
class Post {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public title: string;
 
  @Column()
  public content: string;
}
 
export default Post;
```
- Một điều tuyệt vời về TypeORM là nó tích hợp tốt với TS vì nó được viết bằng TS. Để xác định các column, chúng ta có thể sử dụng nhiều decorator khác nhau
## @PrimaryGeneratedColumn()
- Khoá chính để xác định duy nhất 1 hàng trong bảng. Mặc dù chúng ta có thể sử dụng 1 cột hiện có và biến nó thành cột chính, nhưng chúng ta thường tạo 1 cột id. Bằng cách chọn @PrimaryGeneratedColumn() từ TypeORM, chúng ta tạo 1 cột chính số nguyên có giá trị được tạo tự động
## @Column()
- Decorator `@Column()` đánh dấu 1 property là 1 cột. Khi sử dụng nó, chúng ta có 2 cách tiếp cận khả thi
- Cách tiếp cận đầu tiên là không truyền kiểu cột 1 cách rõ ràng. Khi chúng ta thực hiện điều đó, TypeORM tìm ra cột bằng cách sử dụng các kiểu TS của chúng ta. Điều đó có thể thực hiện được vì NestJs sử dụng `reflect-metadata` ở chế độ nền
- Cách thứ 2 là truyền kiểu cột một cách rõ ràng, ví dụ bằng cách sử dụng `@Column('text')`. Các kiểu cột khả dụng khác nhau giữa các cơ sở dữ liệu như MySql và Postgres. Bạn có thể tra cứu chúng trong tài liệu TypeORM
- Đây là thời điểm thích hợp để thảo luận về các cách khác nhau để lưu trữ chuỗi trong Postgres. Dựa vào TypeORM để tìm ra kiểu của một cột chuỗi sẽ tạo ra kiểu "ký tự thay đổi", còn gọi là varchar
## SQL query
- Trong pgAdmin, chúng ta có thể kiểm tra truy vấn tương đương với những gì TypeORM đã làm cho chúng ta
```ts

CREATE TABLE public.post
(
    id integer NOT NULL DEFAULT nextval('post_id_seq'::regclass),
    title character varying COLLATE pg_catalog."default" NOT NULL,
    content character varying COLLATE pg_catalog."default" NOT NULL,
    CONSTRAINT "PK_be5fda3aac270b134ff9c21cdee" PRIMARY KEY (id)
)
```
- Có 1 vài điều thú vị cần lưu ý ở trên
- Sử dụng `@PrimaryGeneratedColumn()` sẽ có 1 cột int. Mặc định sẽ là giá trị trả về của hàm nextval trả về id duy nhất. Một giải pháp thay thế là sử dụng kiểu tuần tự để làm cho truy vấn ngắn hơn, nhưng vẫn hoạt động tương tự
- Entity có các cột varchar sử dụng COLLATE. Collation được sử dụng để chỉ định thứ tự sắp xếp và phân loại ký tự. Để xem collation mặc định, hãy chạy truy vấn này
```ts
SHOW LC_COLLATE


    - en_US.utf8
```
- Giá trị trên được định nghĩa trong truy vấn được sử dụng để tạo CSDL. Theo mặc định là utf8 và tiếng anh
```ts
CREATE DATABASE nestjs
    WITH 
    OWNER = admin
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.utf8'
    LC_CTYPE = 'en_US.utf8'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1;
```
- Ngoài ra, truy vấn CREATE TABLE của chúng ta đặt ra ràng buộc cho các id để chúng luôn là duy nhất
  - PK_be5fda3aac270b134ff9c21cdee là tên của ràng buộc được tạo ra