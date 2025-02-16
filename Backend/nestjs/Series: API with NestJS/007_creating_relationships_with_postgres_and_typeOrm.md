> https://wanago.io/2020/06/22/api-nestjs-relationships-postgres-typeorm/
# Creating relationships with Postgres and TypeORM
- Khi xây dựng 1 ứng dụng, chúng ta tạo ra nhiều entities. Chúng thường liên quan đến nhau theo 1 cách nào đó và việc xác định các mối quan hệ như vậy là 1 phần thiết yếu của việc thiết kế CSDL. Bài này chúng ta sẽ tìm hiểu relationship trong Postgres là gì và cách chúng ta làm việc với chúng bằng TypeORM và NestJs
- Relational databases đã tồn tại 1 thời gian khá dài và hoạt động tốt với data có cấu trúc. Họ thực hiện điều đó bằng cách sắp xếp data thành các table và liên kết chúng với nhau. Khi chạy nhiều query SQL khác nhau, chúng ta có thể nối các bảng trích xuất thông tin có ý nghĩa.

# One-to-one
- Với relation 1-1, bảng đầu tiên chỉ có 1 hàng khớp với bảng thứ 2 và ngược lại
- Ví dụ trực tiếp nhất là thêm 1 `address` entity
```ts
users/address.entity.ts
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
 
@Entity()
class Address {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public street: string;
 
  @Column()
  public city: string;
 
  @Column()
  public country: string;
}
 
export default Address;
```
- Giả sử 1 address chỉ có thể được liên kết với 1 người dùng. Ngoài ra 1 người dùng không thể có nhiều hơn 1 adress
- Để thực hiện những điều trên, chúng ta cần mối quan hệ 1-1. Khi sử dụng TypeORM, chúng ta có thể tạo mối quan hệ này 1 cách rõ ràng bằng cách sử dụng decorator
```ts
users/user.entity.ts
import { Column, Entity, JoinColumn, OneToOne, PrimaryGeneratedColumn } from 'typeorm';
import { Exclude } from 'class-transformer';
import Address from './address.entity';
 
@Entity()
class User {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column({ unique: true })
  public email: string;
 
  @Column()
  public name: string;
 
  @Column()
  @Exclude()
  public password: string;
 
  @OneToOne(() => Address)
  @JoinColumn()
  public address: Address;
}
 
export default User;
```
- Chúng ta sử dụng `@OneToOne()`, đối số của nó là 1 hàm trả về class của entity mà chúng ta muốn tạo relationship
- `@JoinColumn()` chỉ ra rằng entity User sở hữu mối quan hệ. Điều này có nghĩa là các hàng của bảng User chứa cột `addressId` có thể lưu trữ id của 1 address. Chúng ta chỉ sử dụng nó ở 1 phía của relationship

## Inverse relationship
- Hiện tại, relationship của chúng ta là 1 chiều. Điều đó có nghĩa là chỉ có 1 bên của relation có thông tin về bên kia. Chúng ta có thể thay đổi điều đó bằng cách tạo ra 1 `inverse relationship`. Bằng cách đó, chúng ta tạo ra mối quan hệ 2 chiều giữa User và Address
- Để tạo inverse relationship, chúng ta cần sử dụng `@OneToOne()` và cung cấp property chứa phía bên kia của relationship
```ts
users/address.entity.ts
import { Column, Entity, OneToOne, PrimaryGeneratedColumn } from 'typeorm';
import User from './user.entity';
 
@Entity()
class Address {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public street: string;
 
  @Column()
  public city: string;
 
  @Column()
  public country: string;
 
  @OneToOne(() => User, (user: User) => user.address)
  public user: User;
}
 
export default Address;
```
- Inverse relationship là 1 khái niệm khá trừu tượng và nó không tạo ra bất kỳ cột bổ sung nào trong CSDL
- Việc lưu trữ thông tin về cả 2 bên của relationship có thể hữu ích. Chúng ta có thể dễ dàng liên hệ với cả 2 bên, ví dụ để lấy address với user
```ts

getAllAddressesWithUsers() {
  return this.addressRepository.find({ relations: ['user'] });
}
```
- Nếu chúng ta muốn các thực thể liên quan luôn được bao gồm, chúng ta có thể làm cho relationship của chúng ta trở nên `eager`
```ts
@OneToOne(() => Address, {
  eager: true
})
@JoinColumn()
public address: Address;
```
- Bây giờ, mỗi lần lấy thông tin người dùng, chúng tôi cũng có thể lấy được address của họ. Chỉ 1 bên của relationship có thể `eager`

## Saving the related entities
- Hiện tại chúng ta cần lưu user và address riêng biệt và đây có thể không phải là cách thuận tiện nhất. Thay vào đó, chúng ta có thể bật option `cascade`. Nhờ đó chúng ta có thể lưu 1 address trong khi lưu 1 user
```ts
@OneToOne(() => Address, {
  eager: true,
  cascade: true
})
@JoinColumn()
public address: Address;
```
# One-to-many and many-to-one
- Relationship `one-to-many` và `many-to-one` là mối quan hệ trong đó 1 hàng từ bảng đầu tiên có thể liên kết với nhiều hàng của bảng thứ 2. Các hàng từ bảng thứ 2 chỉ có thể liên kết với 1 hàng của bảng thứ 1
- Trên đây là mối quan hệ rất phù hợp để triển khai cho các bài post và user mà chúng tôi đã xác định trong các phần trước. Giả sử người dùng có thể tạo nhiều bài post nhưng mỗi bài post chỉ có 1 author
```ts
users/user.entity.ts
import { Column, Entity, JoinColumn, OneToMany, OneToOne, PrimaryGeneratedColumn } from 'typeorm';
import { Exclude } from 'class-transformer';
import Address from './address.entity';
import Post from '../posts/post.entity';
 
@Entity()
class User {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column({ unique: true })
  public email: string;
 
  @Column()
  public name: string;
 
  @Column()
  @Exclude()
  public password: string;
 
  @OneToOne(() => Address, {
    eager: true,
    cascade: true
  })
  @JoinColumn()
  public address: Address;
 
  @OneToMany(() => Post, (post: Post) => post.author)
  public posts: Post[];
}
 
export default User;
```
- Nhờ sử dụng `@OneToMany()`, 1 user có thể được liên kết với nhiều post. Chúng ta cũng cần xác định phía bên kia của relation này
```ts
import { Column, Entity, ManyToOne, PrimaryGeneratedColumn } from 'typeorm';
import User from '../users/user.entity';
 
@Entity()
class Post {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public title: string;
 
  @Column()
  public content: string;
 
  @Column({ nullable: true })
  public category?: string;
 
  @ManyToOne(() => User, (author: User) => author.posts)
  public author: User;
}
 
export default Post;
```
- Nhờ có `@ManyToOne()` nhiều bài post có thể related đến 1 user
- Chúng ta dã triển khai authentication trong phần 3. Khi 1 bài post được tạo trong API của chúng ta, chúng ta có quyền truy cập vào dữ liệu của user đã xác thực. Chúng ta cần sử dụng nó để xác định tác giả của bài post
```ts
@Post()
@UseGuards(JwtAuthenticationGuard)
async createPost(@Body() post: CreatePostDto, @Req() req: RequestWithUser) {
  return this.postsService.createPost(post, req.user);
}
```
```ts
async createPost(post: CreatePostDto, user: User) {
  const newPost = await this.postsRepository.create({
    ...post,
    author: user
  });
  await this.postsRepository.save(newPost);
  return newPost;
}
```
- Nếu chúng ta muốn trả về danh sách các bài post có tên author, giờ đây chúng ta có thể dễ dàng thực hiện 1 cách dễ dàng
```ts
getAllPosts() {
  return this.postsRepository.find({ relations: ['author'] });
}
 
async getPostById(id: number) {
  const post = await this.postsRepository.findOne(id, { relations: ['author'] });
  if (post) {
    return post;
  }
  throw new PostNotFoundException(id);
}
 
async updatePost(id: number, post: UpdatePostDto) {
  await this.postsRepository.update(id, post);
  const updatedPost = await this.postsRepository.findOne(id, { relations: ['author'] });
  if (updatedPost) {
    return updatedPost
  }
  throw new PostNotFoundException(id);
}
```
- Nếu check ở CSDL sẽ thấy phía relationship `ManyToOne()` sẽ lưu trữ foreign key
- Điều này có nghĩa là bài post sẽ lưu id của author chứ không phải ngược lại

# Many-to-many
- Trước đây, chúng ta đã thêm 1 property được gọi là `category` vào posts. Hãy cùng tìm hiểu điều đó
- Chúng tôi muốn có thể định nghĩa các category có thể sử dụng lại trên nhiều bài posts. Chúng tôi cũng muốn 1 bài post có thể thuộc nhiều category
- Phía trên là relationship many-to-many. Nó xảy ra khi 1 hàng từ bảng đầu tiên có thể liên kết đến nhiều hàng từ bảng thứ 2 và ngược lại
```ts
// categories/category.entity.ts
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';
 
@Entity()
class Category {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public name: string;
}
 
export default Category;
```
```ts
// posts/post.entity.ts
import { Column, Entity, JoinTable, ManyToMany, ManyToOne, PrimaryGeneratedColumn } from 'typeorm';
import User from '../users/user.entity';
import Category from '../categories/category.entity';
 
@Entity()
class Post {
  @PrimaryGeneratedColumn()
  public id: number;
 
  @Column()
  public title: string;
 
  @Column()
  public content: string;
 
  @Column({ nullable: true })
  public category?: string;
 
  @ManyToOne(() => User, (author: User) => author.posts)
  public author: User;
 
  @ManyToMany(() => Category)
  @JoinTable()
  public categories: Category[];
}
 
export default Post;
```
- Khi chúng ta sử dụng `@ManyToMany()` và `@JoinTable()`, TypeORM thiết lập 1 bảng bổ sung. Theo cách này, cả bảng Post và Category đều không lưu trữ dữ liệu về relationship
```ts
CREATE TABLE public.post_categories_category
(
    "postId" integer NOT NULL,
    "categoryId" integer NOT NULL,
    CONSTRAINT "PK_91306c0021c4901c1825ef097ce" PRIMARY KEY ("postId", "categoryId"),
    CONSTRAINT "FK_93b566d522b73cb8bc46f7405bd" FOREIGN KEY ("postId")
        REFERENCES public.post (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE CASCADE,
    CONSTRAINT "FK_a5e63f80ca58e7296d5864bd2d3" FOREIGN KEY ("categoryId")
        REFERENCES public.category (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE CASCADE
)
```
- Chúng ta có thể thấy rằng bảng `post_categories_category` mới của chúng ta sử dụng khoá chính gôm `postId` và `categoryId` kết hợp
- Chúng ta cũng có thể tạo mối quan hệ nhiều nhiều theo 2 chiều. Tuy nhiên hãy nhớ chỉ sử dụng `@JoinTable()` ở 1 bên của relationship
```ts
@ManyToMany(() => Category, (category: Category) => category.posts)
@JoinTable()
public categories: Category[];
```
```ts
@ManyToMany(() => Post, (post: Post) => post.categories)
public posts: Post[];
```
- Nhờ thực hiện các bước trên, giờ đây chúng ta có thể dễ dàng lấy các category cùng với các post của chúng
```ts
getAllCategories() {
  return this.categoriesRepository.find({ relations: ['posts'] });
}
 
async getCategoryById(id: number) {
  const category = await this.categoriesRepository.findOne(id, { relations: ['posts'] });
  if (category) {
    return category;
  }
  throw new CategoryNotFoundException(id);
}
 
async updateCategory(id: number, category: UpdateCategoryDto) {
  await this.categoriesRepository.update(id, category);
  const updatedCategory = await this.categoriesRepository.findOne(id, { relations: ['posts'] });
  if (updatedCategory) {
    return updatedCategory
  }
  throw new CategoryNotFoundException(id);
}
```

# Summary
- Chúng ta đã đề cập đến việc tạo relationship trong khi sử dụng NestJs với Postgres và TypeORM. Nó bao gồm 1-1 và 1-n và n-n. Cung cấp các option khác nhau như `cascade` và `eager`. Chúng tôi cũng đã xem xét các truy vấn SQL mà TypeORM tạo ra để hiểu rõ hơn về cách thức hoạt động của nó

