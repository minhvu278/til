# Authentication
- Cài đặt REST
```ts
nest g res auth --no-spec
```
```ts
npm install --save @nestjs/passport passport passport-local

npm install --save-dev @types/passport-local
```
- Cài đặt guards
```ts
nest g gu auth/guards/local-auth
```

```ts
npm i @nestjs/jwt passport-jwt

npm i -D @types/passport-jwt

openssl rand -hex 32
```