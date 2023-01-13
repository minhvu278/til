# Install
- NestJs CLI 
    ```js
    yarn global add @nestjs/cli
    //or
    npm install -g @nestjs/cli
    ```
- Create project
    ```js
    nest new my-nest-project
    ```
- Run project
    ```js
    npm run start:dev
    //or 
    yarn start:dev
    ```
- Generate module 
    - Generate module task
    ```js
    nest g module tasks
    ```
- Create controller 
    ```js
    nest g controller tasks --no-spec
    ```
- Create service 
    ```js
    nest g service tasks --no-spec
    ```
# Validate
- Install 
    ```js
    npm i --save class-validator class-transformer
    // or
    yarn add class-validator class-transformer
    ```

# Run docker 
- Running PG via docker
    ```
    docker run --name postgres-nest -p 5432:5432 -e POSTGRES_PASSWORD=postgres -d postgres
    ```
- Stop 
    ```
    docker container stop postgres-nest
    ```
- Remove 
    ```
    docker container rm postgres-nest
