# Install 
- Cài trên terminal 
    ```js 
    npx create-react-app my-app
    cd my-app
    npm start
    ```

# CDN Link 
- Cả react & reactDOM đều có sẵn CDN 
    - CDN dành cho dev
        ```js
        <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
        ```
    - CDN dành cho production
        ```js 
        <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
        ```
