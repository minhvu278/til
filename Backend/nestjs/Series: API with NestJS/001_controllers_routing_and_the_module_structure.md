# Introductions
- Nestjs là 1 bộ khung để xây dựng các ứng dụng NodeJs. Nó buộc chúng ta phải tuân theo tầm nhìn của nó về cách 1 ứng dụng nên trông như thế nào ở 1 mức độ nào đó. Điều đó có thể được coi là 1 điều tốt giúp chúng ta duy trì được tính nhất quán của ứng dụng và buộc phải tuân theo các good practices
- Nestjs sử dụng Expressjs theo mặc định. Nếu bạn đã quen thuộc với Typescript Express series và bạn thích nó, có thể bạn cũng sẽ thích nestjs. Ngoài ra, kiến thức về framework Express cũng rất hữu ích
- 1 lưu ý quan trọng là docs của Nestjs rất toàn diện, bạn sẽ được hưởng lợi khi search nó. Ở đây, chúng ta sắp xếp kiến thức theo thứ tự, nhưng đôi khi cũng liên kết đến docs chính thức. Chúng ta cũng tham khảo khuôn khổ của Express để làm nổi bật những lợi thế của việc sử dụng NestJs. Để được hưởng lợi từ bài viết này nhiều hơn, một số kinh nghiệm với Express có thể hữu ích nhưng không bắt buộc
  - Nếu bạn muốn tìm hiểu sâu hơn về Node.js, hãy tham khảo: [Node Ts](https://wanago.io/2019/02/11/node-js-typescript-modules-file-system/). Nó gồm các phần như: Luồng, vòng lặp sự kiện, process đa luồng với worker. Ngoài ra, việc biết cách tạo API mà không cần bất kỳ framework nào như Express và NestJs cũng khiến chúng ta hiểu và trân trọng chúng hơn
# Getting started with NestJS
- Cách đơn giản nhất để bắt đầu là clone repository starter TS chính thức. Nest được build bằng TS và hỗ trợ đầy đủ. Có thể sử dụng Js thay thế nhưng ở đây sẽ sử dụng TS
  ```ts
  git clone git@github.com:nestjs/typescript-starter.git
  ```
- 1 file cần check trong repository trên là file `tsconfig.json`. Khuyên nên thêm các option `alwayStrict` và `noImplicitAny`
- Repository ở trên chứa các packages cơ bản nhất. Chúng ta cũng có các loại file cơ bản để bắt đầu, vì thế hãy cùng xem xét chúng
  - Tất cả code nằm trong repository này [repository](https://github.com/mwanago/nestjs-typescript). Hy vọng sau này có thể đóng góp vai trò là 1 mẫu NestJs với 1 số tính năng tích hợp sẵn. Đây là 1 nhánh của [Typescript Starter](https://github.com/nestjs/typescript-starter)
# Controllers
- Controller xử lý các request đến và trả lại cho client. Repository `Typescript-starter` chứa controller đầu tiên. Hãy tạo ra 1 cái mạnh mẽ hơn
  - posts.controller.ts
  ```ts
  import { Body, Controller, Delete, Get, Param, Post, Put } from '@nestjs/common';
  import PostsService from './posts.service';
  import CreatePostDto from './dto/createPost.dto';
  import UpdatePostDto from './dto/updatePost.dto';
  
  @Controller('posts')
  export default class PostsController {
    constructor(
      private readonly postsService: PostsService
    ) {}
  
    @Get()
    getAllPosts() {
      return this.postsService.getAllPosts();
    }
  
    @Get(':id')
    getPostById(@Param('id') id: string) {
      return this.postsService.getPostById(Number(id));
    }
  
    @Post()
    async createPost(@Body() post: CreatePostDto) {
      return this.postsService.createPost(post);
    }
  
    @Put(':id')
    async replacePost(@Param('id') id: string, @Body() post: UpdatePostDto) {
      return this.postsService.replacePost(Number(id), post);
    }
  
    @Delete(':id')
    async deletePost(@Param('id') id: string) {
      this.postsService.deletePost(Number(id));
    }
  }
  ```
  - post.interface.ts
  ```ts
  export interface Post {
    id: number;
    content: string;
    title: string;
  }
  ```
- Điều đầu tiên chúng ta có thể nhận thấy là NestJs sử dụng nhiều decorators. Để biết 1 class là controller, chúng ta sử dụng `@Controller()` decorator. Chúng ta truyền 1 đối số tuỳ chọn vào cho nó. Nó hoạt động như 1 tiền tố đường dẫn đến tất cả các routes trong controller
# Routing
- Các decorators tiếp theo được connect với routing trong constructor ở trên là `@Get(), @Post(), Delete() và @Put()`. Họ yêu cầu nest tạo handller cho điểm cuối, cụ thể là cho các yêu cầu HTTP. Controller ở trên tạo ra 1 tập hợp các endpoint sau:
  - Trả về tất cả các post: `GET /posts`
  - Trả về 1 post cùng id đã cho: `GET /posts/{id}`
  - Tạo mới 1 post: `POST /posts`
  - Thay thế 1 post bằng id: `PUT /posts/{id}`
  - Xoá 1 post: `DELETE /posts/{id}`
- Theo mặc định, Nest trả về status 200 OK ngoại trừ 201 Created dành cho POST. Chúng ta có thể dễ dàng thay đổi bằng cách sử dụng `@HttpCode()` decorator
- Khi chúng ta triển khai 1 API, chúng ta thường tham chiếu đến 1 phần tử cụ thể. Chúng ta có thể làm như thế với `router parameters`. Chúng là các phân đoạn URL đặc biệt được sử dụng để nắm bắt các giá trị được chỉ định tại vị trí của chúng. Để thêm route parameter, chúng ta cần thêm tiền tố `:` vào tên tham số đó
- Cách trích xuất giá trị của route parameters là sử dụng `@Param()` decorator. Nhờ đó, chúng ta có thể truy cập vào nó thông qua các đối số của route parameters
  - Chúng ta có thể sử dụng đối số tuỳ chọn để tham chiếu đến 1 tham số cụ thể, ví dụ `@Param('id')`. Nếu không, chúng ta sẽ có quyền truy cập vào object params với tất cả các tham số
- Vì các route parameters là chuỗi và id là số nên trước tiên chúng ta cần chuyển đổi các tham số
  - Chúng ta có thể sử dụng `pipes` để chuyển đổi các route parameters. `Pipes` là tính năng tích hợp trong NestJs và chúng ta sẽ đề cập đến sau
# Accessing the body of a request
- Khi chúng ta xử lý POST và PUT trong controller ở trên, chúng ta cần truy cập vào phần body của request. Bằng cách đó, chúng ta có thể sử dụng nó để lưu vào CSDL của mình
- NestJs cung cấp `@Body()` decorator giúp chúng ta dễ dàng truy cập vào phần body. Giống như trong loạt seri TS Express, đã giới thiệu về khái niệm Data Transfer Object (DTO). Nó định nghĩa định dạng data được gửi trong request. Nó có thể là 1 interface hoặc 1 class, nhưng sử dụng cách sau sẽ cho chúng ta nhiều khả năng hơn và chúng ta sẽ tìm hiểu chúng sau
  - createPost.dto.ts
  ```ts
  class CreatePostDto {
    content: string;
    title: string;
  }
  ```
  - updatePost.dto.ts
  ```ts
  class UpdatePostDto {
    id: number;
    content: string;
    title: string;
  }
  ```
# The arguments of a handler function
- Chúng ta hãy xem xét kỹ hơn các đối số của hàm xử lý
  ```ts
  async replacePost(@Body() post: UpdatePostDto, @Param('id') id: string) {
    return this.postsService.replacePost(Number(id), post);
  }
  ```
- Bằng cách sử dụng các method agrument decorators, chúng tôi yêu cầu Nest đưa các đối số cụ thể vào method của chúng tôi. NestJs được xây dựng dựa trên khái niệm Dependency Injection và Inversion of Control
  - Dependency Injection là 1 trong những kỹ thuật thực hiện Inversion of Control. Nếu bạn muốn học thêm về IoC, hãy xem các nguyên tắc SOLID [SOLID](https://wanago.io/2020/02/03/applying-solid-principles-to-your-typescript-code/)
- Một lưu ý quan trọng về việc đảo ngược thứ tự của chúng sẽ mang lại kết quả tương tự, điều này ban đầu có vẻ trái ngược với trực giác
  ```ts
  async replacePost(@Param('id') id: string, @Body() post: UpdatePostDto) {
    return this.postsService.replacePost(Number(id), post);
  }
  ```
# Advantages of NestJS over Express
- NestJs cung cấp cho chúng ta rất nhiều tiện ích ngay khi cài đặt và yêu cầu chúng ta thiết kế API bằng controllers. Mặt khác, ExpressJs cho chúng ta nhiều sự linh hoạt hơn nhưng không trang bị cho chúng ta những công cụ như vậy để duy trì khả năng đọc được code của chúng ta
- Chúng ta có thể tự do triển khai controller bằng ExpressJs. Hãy xem trong Typescript Express series
  ```ts
  import { Request, Response, Router } from 'express';
  import Controller from '../../interfaces/controller.interface';
  import PostsService from './posts.service';
  import CreatePostDto from './dto/createPost.dto';
  import UpdatePostDto from './dto/updatePost.dto';
  
  export default class PostsController implements Controller {
    private path = '/posts';
    public router = Router();
    private postsService = new PostsService();
  
    constructor() {
      this.intializeRoutes();
    }
  
    intializeRoutes() {
      this.router.get(this.path, this.getAllPosts);
      this.router.get(`${this.path}/:id`, this.getPostById);
      this.router.post(this.path, this.createPost);
      this.router.put(`${this.path}/:id`, this.replacePost);
    }
  
    private getAllPosts = (request: Request, response: Response) => {
      const posts = this.postsService.getAllPosts();
      response.send(posts);
    }
  
    private getPostById = (request: Request, response: Response) => {
      const id = request.params.id;
      const post = this.postsService.getPostById(Number(id));
      response.send(post);
    }
  
    private createPost = (request: Request, response: Response) => {
      const post: CreatePostDto = request.body;
      const createdPost = this.postsService.createPost(post);
      response.send(createdPost);
    }
  
    private replacePost = (request: Request, response: Response) => {
      const id = request.params.id;
      const post: UpdatePostDto = request.body;
      const replacedPost = this.postsService.replacePost(Number(id), post);
      response.send(replacedPost);
    }
  
    private deletePost = (request: Request, response: Response) => {
      const id = request.params.id;
      this.postsService.deletePost(Number(id));
      response.sendStatus(200);
    }
  }
  ```
- Ở trên, chúng ta có thể thấy 1 controller tương tự được tạo trong Pure Express. Có khá nhiều điểm khác biệt đáng chú ý
- Đầu tiên, chúng ta cần xử lý việc routing controller. Chúng ta không có công cụ decorators nào có thể giúp chúng ta làm điều đó. Cách Nestjs thực hiện ở đây khá giống với Spring Framework được viết cho Java
- Trong loạt bài TS Express, chúng tôi sử dụng class `Application` để gắn routing vào app
  ```ts
  class Application {
    // ...
    private initializeControllers(controllers: Controller[]) {
      controllers.forEach((controller) => {
        this.app.use('/', controller.router);
      });
    }
    // ...
  }
  ```
- Một lợi thế lớn khác của NextJs là nó cung cấp cho chúng ta một cách thanh lịch để xử lý các Request và Response object. Các decorators như `@Body()` và `@Params()` giúp cải thiện khả năng đọc code của chúng ta
- Một trong những điều hữu ích nhất mà Nest cung cấp là cách nó xử lý response. Trình xử lý response có thể trả về các kiểu nguyên thuỷ, promises hoặc thậm chí là các luồng quan sát được của RxJs. Chúng ta không cần xử lý thủ công mọi lúc và sử dụng hàm `response.send`. NestJs còn giúp xử lý lỗi trong App 1 cách dễ dàng và chúng ta sẽ khám phá trong các phần tiếp theo
  - Khi sử dụng NestJs, chúng ta có thể thao tác trực tiếp trên các object Request và Response. Tuy nhiên, việc tự xử lý response sẽ làm mất đi 1 số lợi thế của Nest
- Ngoài ra còn có sự khác biệt về cách chúng ta xử lý các dependencies trong pure Express và NestJs
- Trong Express controller ở trên, chúng ta tạo 1 `PostsService` mới trực tiếp trong `PostsController`. Thật không may, nó phá vỡ nguyên tắc **Dependency inversion principle** khỏi các nguyên tắc SOLID. Một trong những vấn đề có thể xảy ra là một số rắc rối khi viết test
- Mặt khác, Nest rất quan tâm đến việc tuân thủ các nguyên tắc Dependency inversion principle bằng cách triển khai Dependency Injection
# Services
- Repository `typescript-starter` cũng chứa service đầu tiên. Công việc của 1 service là tách bussiness logic ra khỏi controller, giúp việc test trở nên cleaner hơn. Hãy tạo 1 simple service cho posts
  - posts.service.ts
  ```ts
  import { HttpException, HttpStatus, Injectable } from '@nestjs/common';
  import CreatePostDto from './dto/createPost.dto';
  import Post from './post.interface';
  import UpdatePostDto from './dto/updatePost.dto';
  
  @Injectable()
  export default class PostsService {
    private lastPostId = 0;
    private posts: Post[] = [];
  
    getAllPosts() {
      return this.posts;
    }
  
    getPostById(id: number) {
      const post = this.posts.find(post => post.id === id);
      if (post) {
        return post;
      }
      throw new HttpException('Post not found', HttpStatus.NOT_FOUND);
    }
  
    replacePost(id: number, post: UpdatePostDto) {
      const postIndex = this.posts.findIndex(post => post.id === id);
      if (postIndex > -1) {
        this.posts[postIndex] = post;
        return post;
      }
      throw new HttpException('Post not found', HttpStatus.NOT_FOUND);
    }
  
    createPost(post: CreatePostDto) {
      const newPost = {
        id: ++this.lastPostId,
        ...post
      }
      this.posts.push(newPost);
      return newPost;
    }
  
    deletePost(id: number) {
      const postIndex = this.posts.findIndex(post => post.id === id);
      if (postIndex > -1) {
        this.posts.splice(postIndex, 1);
      } else {
        throw new HttpException('Post not found', HttpStatus.NOT_FOUND);
      }
    }
  }
  ```
- Mặc dù logic khá đơn giản nhưng vẫn có 1 số điểm cần chú ý
- Chúng ta sử dụng class `HttpException` tích hợp để đưa ra lỗi mà Nest có thể hiểu được. Khi chúng ta throw `HttpException('Post not found', HttpStatus.NOT_FOUND)`, nó sẽ được truyền đến **global exception filter** và response thích hợp sẽ được gửi đến client
- Decorator `@Injectable()` cho biết class này là 1 [provider](https://docs.nestjs.com/providers). Nhờ đó, chúng ta có thể thêm nó vào module
# Modules
- Chúng ta có thể sử dụng các module để tổ chức app. `PostsController` và `PostsService` có liên quan chặt chẽ với nhau và thuộc cùng 1 application domain. Do đó đưa chúng vào 1 module là hợp lý
- Bằng cách đó, chúng ta sắp xếp code của mình theo từng tính năng. Điều này đặc biệt hữu ích khi app lớn hơn
  - posts.module.ts
  ```ts
  import { Module } from '@nestjs/common';
  import PostsController from './posts.controller';
  import PostsService from './posts.service';
  
  @Module({
    imports: [],
    controllers: [PostsController],
    providers: [PostsService],
  })
  export class PostsModule {}
  ```
- Ngoài ra, mọi app đều có module gốc. Đây là điểm khởi đầu cho Nest khi xây dựng app.
  - app.module.ts
  ```ts
  import { Module } from '@nestjs/common';
  import { PostsModule } from './posts/posts.module';
  
  @Module({
    imports: [PostsModule],
    controllers: [],
    providers: [],
  })
  export class AppModule {}
  ```
- Module này bao gồm:
  - **import**: import các module - NestJs sử dụng `PostsModule` nhờ việc nhập nó vào `AppModule`
  - **controllers**: cotroller để khởi tạo
  - **providers**: Provider để khởi tạo - chúng có thể được sử dụng ít nhất trong module này
  - **export**: Một tập hợp con các provider có sẵn trong các module khác
# Summary
- Bằng cách thực hiện tất cả các bước trên, folder `src` sẽ trôn như sau
  ```
  ├── src
  │   ├── app.module.ts
  │   ├── main.ts
  │   └── posts
  │       ├── dto
  │       │   ├── createPost.dto.ts
  │       │   └── updatePost.dto.ts
  │       ├── post.interface.ts
  │       ├── posts.controller.ts
  │       ├── posts.module.ts
  │       └── posts.service.ts
  ```
- Trong bài viết này, chúng ta mới bắt đầu với Nest. Chúng ta đã hiểu controller là gì và cách xử lý các routing cơ bản trong app của chúng ta. Chúng ta cũng đã đề cập ngắn gọn đến Services và Modules. Trong các phần sau của loạt bài này, chúng ta sẽ dành khá nhiều thời gian để thảo luận về cấu trúc ứng dụng trong NestJs
- Tất cả những kiến thức trên chỉ là phần nổi của tảng băng chìm NestJs. Có nhiều điều để nói về các tính năng mà Nest cung cấp, chẳng hạn như xử lý lỗi gọn gàng và dependency injection. Chúng ta cũng sẽ tìm hiểu về CSDL PostgreSQL và cách sử dụng nó thông qua câu lệnh ORM và SQL
