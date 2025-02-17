> https://wanago.io/2020/07/06/api-nestjs-unit-tests/
# Writing unit tests
- Việc viết test có thể giúp chúng ta tự tin hơn tạo ra 1 API có đầy đủ chức năng. Trong bài viết này, chúng ta sẽ xem xét cách chúng ta có thể test ứng dụng của mfinh bằng cách viết unit tests. Chúng ta thực hiện điều này bằng cách sử dụng 1 số tiện ích được tích hợp sẵn trong NestJs cũng như Jest library

# Testing NestJS with unit tests
- Nhiệm vụ của 1 unit test là xác minh 1 đoạn code riêng lẻ. Một unit test có thể là 1 module, 1 class hoặc 1 function. Mỗi unit test phải được tách biệt và độc lập với nhau. Bằng cách viết các unit test, chúng ta có thể đảm bảo rằng từng phần riêng lẻ của ứng dụng hoạt động như mong đợi
- Hãy viết test cho `AuthenticationService`
```ts
src/authentication/tests/authentication.service.spec.ts
import { AuthenticationService } from '../authentication.service';
import { UsersService } from '../../users/users.service';
import { Repository } from 'typeorm';
import User from '../../users/user.entity';
import { JwtService } from '@nestjs/jwt';
import { ConfigService } from '@nestjs/config';
 
describe('The AuthenticationService', () => {
  const authenticationService = new AuthenticationService(
    new UsersService(
      new Repository<User>()
    ),
    new JwtService({
      secretOrPrivateKey: 'Secret key'
    }),
    new ConfigService()
  );
  describe('when creating a cookie', () => {
    it('should return a string', () => {
      const userId = 1;
      expect(
        typeof authenticationService.getCookieWithJwtToken(userId)
      ).toEqual('string')
    })
  })
});
```
```
PASS src/authentication/tests/authentication.service.spec.ts
The AuthenticationService
when creating a cookie
✓ should return a string (12ms)
```
- Chúng ta thực hiện `npm run test`, Jest sẽ tìm kiếm các file có đuôi là `.spec.ts` và thực thi chúng
- Có thể cải thiện đoạn code trên. Mỗi unit test của chúng ta cần phải độc lập và cần đảm bảo rằng nếu thêm nhiều tests hơn vào file trên, tất cả chúng sẽ sử dụng cùng 1 phiên bản của `AuthenticationService`. Điều này phá vỡ quy tắc tất cả các bài test đều độc lập
- Để giải quyết vấn đề này, chúng ta có thể sử dụng `beforeEach` chạy trước mỗi test
```ts
src/authentication/tests/authentication.service.spec.ts
import { AuthenticationService } from '../authentication.service';
import { UsersService } from '../../users/users.service';
import { Repository } from 'typeorm';
import User from '../../users/user.entity';
import { JwtService } from '@nestjs/jwt';
import { ConfigService } from '@nestjs/config';
 
describe('The AuthenticationService', () => {
  let authenticationService: AuthenticationService;
  beforeEach(() => {
    authenticationService = new AuthenticationService(
      new UsersService(
        new Repository<User>()
      ),
      new JwtService({
        secretOrPrivateKey: 'Secret key'
      }),
      new ConfigService()
    );
  })
  describe('when creating a cookie', () => {
    it('should return a string', () => {
      const userId = 1;
      expect(
        typeof authenticationService.getCookieWithJwtToken(userId)
      ).toEqual('string')
    })
  })
});
```
- Bây giờ, chắc chắn mọi tests trong file authentication.service.spec.ts đều nhận được 1 phiên bản hoàn toàn mới của `AuthenticationService`
- Đoạn code trên không được đẹp cho lắm. Vì constructor của `AuthenticationService` mong đợi 1 số dependency nên chúng ta đã cung cấp cho chúng theo cách thủ công cho đến nay

# Creating testing modules
- NestJs cung cấp cho chúng ta các utilties để giải quyết vấn đề trên
```ts
npm install @nestjs/testing
```
- Bằng cách sử dụng `Test.createTestingModule().compile()`, chúng ta có thể tạo 1 module với các dependency đã được giải quyết
```ts
src/authentication/tests/authentication.service.spec.ts
import { AuthenticationService } from '../authentication.service';
import { Test } from '@nestjs/testing';
import { UsersModule } from '../../users/users.module';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { JwtModule } from '@nestjs/jwt';
import { DatabaseModule } from '../../database/database.module';
import * as Joi from '@hapi/joi';
 
describe('The AuthenticationService', () => {
  let authenticationService: AuthenticationService;
  beforeEach(async () => {
    const module = await Test.createTestingModule({
      imports: [
        UsersModule,
        ConfigModule.forRoot({
          validationSchema: Joi.object({
            POSTGRES_HOST: Joi.string().required(),
            POSTGRES_PORT: Joi.number().required(),
            POSTGRES_USER: Joi.string().required(),
            POSTGRES_PASSWORD: Joi.string().required(),
            POSTGRES_DB: Joi.string().required(),
            JWT_SECRET: Joi.string().required(),
            JWT_EXPIRATION_TIME: Joi.string().required(),
            PORT: Joi.number(),
          })
        }),
        DatabaseModule,
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
      providers: [
        AuthenticationService
      ],
    }).compile();
    authenticationService = await module.get<AuthenticationService>(AuthenticationService);
  })
  describe('when creating a cookie', () => {
    it('should return a string', () => {
      const userId = 1;
      expect(
        typeof authenticationService.getCookieWithJwtToken(userId)
      ).toEqual('string')
    })
  })
});
```
- Vẫn còn nhiều vấn đề với đoạn code trên. Chúng ta sẽ giải quyết từng vấn đề 1

## Mocking the database connection
- Vấn đề lớn nhất ở trên là chúng ta sử dụng DatabaseModule có nghĩa là kết nối với DB thực. Khi chạy unit tests, chúng ta muốn tránh nó
- Sau khi xoá `DatabaseModule` khỏi imports, chúng ta có thể thấy lỗi
```
Error: Nest can’t resolve dependencies of the UserRepository (?). Please make sure that the argument Connection at index [0] is available in the TypeOrmModule context.
```
- Để giải quyết vấn đề này, chúng ta cần mock 1 User repository . Để làm vậy chúng ta cần sử dụng `getRepositoryToken` từ `@nestjs/typeorm`
```ts
import User from '../../users/user.entity';
```
```ts
providers: [
  AuthenticationService,
  {
    provide: getRepositoryToken(User),
    useValue: {},
  }
],
```
- Thật không may, lỗi trên vẫn tiếp diễn. Điều này là do chúng tôi import `UserModule` có chứa `TypeOrmModule.forFeature([User])`. Chúng ta có thể tránh import các module khi viết test vì chúng ta chưa muốn test tính tích hợp giữa các class ngay lúc này. Thay vào đó, chúng ta cần thêm `UsersService` vào providers
```ts
src/authentication/tests/authentication.service.spec.ts
import { AuthenticationService } from '../authentication.service';
import { Test } from '@nestjs/testing';
import { ConfigModule } from '@nestjs/config';
import { JwtModule } from '@nestjs/jwt';
import { getRepositoryToken } from '@nestjs/typeorm';
import User from '../../users/user.entity';
import { UsersService } from '../../users/users.service';
 
describe('The AuthenticationService', () => {
  let authenticationService: AuthenticationService;
  beforeEach(async () => {
    const module = await Test.createTestingModule({
      imports: [
        ConfigModule.forRoot({
          // ...
        }),
        JwtModule.registerAsync({
          // ...
        }),
      ],
      providers: [
        UsersService,
        AuthenticationService,
        {
          provide: getRepositoryToken(User),
          useValue: {},
        }
      ],
    }).compile();
    authenticationService = await module.get<AuthenticationService>(AuthenticationService);
  })
  describe('when creating a cookie', () => {
    it('should return a string', () => {
      const userId = 1;
      expect(
        typeof authenticationService.getCookieWithJwtToken(userId)
      ).toEqual('string')
    })
  })
});
```
- Object chúng ta đưa vào `useValue` ở trên là mocked repository. Chúng ta sẽ thêm 1 số method vào nó ở bên dưới

## Mocking ConfigService and JwtService
- Vì chúng ta muốn tránh sử dụng các module, chúng ta có thể thay thế `ConfigModule` và `JwtModule` bằng các mock. Chính xác hơn, chúng ta cần cung cấp `ConfigService` và `JwtService` đã mock
- Một cách tiếp cận rõ ràng cho vấn đề đó là tạo các file riêng biệt
```ts
// src/utils/mocks/config.service.ts
const mockedConfigService = {
  get(key: string) {
    switch (key) {
      case 'JWT_EXPIRATION_TIME':
        return '3600'
    }
  }
}
```
```ts
// src/utils/mocks/jwt.service.ts
const mockedJwtService = {
  sign: () => ''
}
```
- Khi chúng ta sử dụng phần trên, test của chúng ta sẽ trông như thế này
```ts
src/utils/mocks/config.service.ts
import { AuthenticationService } from '../authentication.service';
import { Test } from '@nestjs/testing';
import { ConfigService } from '@nestjs/config';
import { JwtService } from '@nestjs/jwt';
import { getRepositoryToken } from '@nestjs/typeorm';
import User from '../../users/user.entity';
import { UsersService } from '../../users/users.service';
import mockedJwtService from '../../utils/mocks/jwt.service';
import mockedConfigService from '../../utils/mocks/config.service';
 
describe('The AuthenticationService', () => {
  let authenticationService: AuthenticationService;
  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [
        UsersService,
        AuthenticationService,
        {
          provide: ConfigService,
          useValue: mockedConfigService
        },
        {
          provide: JwtService,
          useValue: mockedJwtService
        },
        {
          provide: getRepositoryToken(User),
          useValue: {}
        }
      ],
    })
      .compile();
    authenticationService = await module.get(AuthenticationService);
  })
  describe('when creating a cookie', () => {
    it('should return a string', () => {
      const userId = 1;
      expect(
        typeof authenticationService.getCookieWithJwtToken(userId)
      ).toEqual('string')
    })
  })
});
```
## Changing the mock per test
- Chúng ta không phải lúc nào cũng muốn mock theo cùng 1 cách trong mỗi test. Để thay đổi cách triển khai giữa các bài test, chúng ta có thể sử dụng `jest.Mock`
```ts
src/users/tests/users.service.spec.ts
import { Test } from '@nestjs/testing';
import { getRepositoryToken } from '@nestjs/typeorm';
import User from '../../users/user.entity';
import { UsersService } from '../../users/users.service';
 
describe('The UsersService', () => {
  let usersService: UsersService;
  let findOne: jest.Mock;
  beforeEach(async () => {
    findOne = jest.fn();
    const module = await Test.createTestingModule({
      providers: [
        UsersService,
        {
          provide: getRepositoryToken(User),
          useValue: {
            findOne
          }
        }
      ],
    })
      .compile();
    usersService = await module.get(UsersService);
  })
  describe('when getting a user by email', () => {
    describe('and the user is matched', () => {
      let user: User;
      beforeEach(() => {
        user = new User();
        findOne.mockReturnValue(Promise.resolve(user));
      })
      it('should return the user', async () => {
        const fetchedUser = await usersService.getByEmail('test@test.com');
        expect(fetchedUser).toEqual(user);
      })
    })
    describe('and the user is not matched', () => {
      beforeEach(() => {
        findOne.mockReturnValue(undefined);
      })
      it('should throw an error', async () => {
        await expect(usersService.getByEmail('test@test.com')).rejects.toThrow();
      })
    })
  })
});
```
# Summary
- Trong bài này, chúng ta đã tìm hiểu cách viết các unit test trong NestJs. Để thực hiện, chúng ta cần sử dụng library Jest đi kèm với Nest. Chúng ta cũng đã sử dụng 1 số utilities tích hợp để mock các service và module khác nhau 1 cách chính xác. Một trong những điều quan trọng nhất là mô phỏng kết nối CSDL để tách biệt test
