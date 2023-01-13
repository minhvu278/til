# 1 số thứ cần cài 
- Đầu tiên thì chúng ta cùng đi qua 1 số thứ cần cài để chuẩn bị cho việc deploy 
    - PM2: Là một daemon process manager, nó giúp bạn quản lý các tiến trình trong ứng dụng của bạn, giúp cho application của bạn luôn chạy, mình thì hay gọi là luôn ở trạng trái "sống".
        ```
        npm i pm2 -g
        ```
    - NVM: Node Version Manager là một công cụ, phần mềm dùng để quản lý các version Node.js cài đặt trên máy.
    - Nginx: Phát âm là "engine-ex" là một phần mềm mã nguồn mở dùng để phục vụ web, reverse proxy, caching, cân bằng tải, và nhiều hơn nữa
        ```
        sudo apt-get install -y nginx
        ```

# Setup
- Đầu tiên thì ta cần tạo mới 1 ứng dụng Nextjs và đẩy code lên Github repo
    ```js 
    npx create-next-app
    cd my-app
    ```
- Tiếp theo thì ta cần generate pm2 ecosystem file
    ```
    pm2 ecosystem
    ```
- Sau khi generate thì ta sẽ thay thế các giá trị tương ứng của mình vào nhé và sau khi xong thì đẩy nó lên github
    ```js
    module.exports = {
    apps: [{
        script: 'npm start'
    }],

    deploy: {
        production: {
        key: 'key.pem',
        user: 'ubuntu',
        host: 'SSH_HOSTMACHINE',
        ref: 'origin/main',
        repo: 'GIT_REPOSITORY',
        path: '/home/ubuntu',
        'pre-deploy-local': '',
        'post-deploy': 'source ~/.nvm/nvm.sh && npm install && npm run build && pm2 reload ecosystem.config.js --env production',
        'pre-setup': '',
        'ssh_options': 'ForwardAgent=yes'
        }
    }
    };
    ```
# SSH to server
- Đầu tiên thì ta cần thay đổi quyền pem rồi coppy tệp pem vào thư mục gốc của dự án.
    ```
    chmod 400 key.pem
    ```
- SSH to server
    ```
    ssh -i key.pem ubuntu@[IP_ADDRESS]
    ```
- Trên server 
    - Cài Node, PM2, Nginx 
        ```
        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
        source .bashrc
        nvm install --lts
        npm i -g pm2
        sudo apt-get update
        sudo apt-get install -y nginx
        sudo service nginx restart
        ```
    - Cấu hình Nginx
        ```
        sudo vim /etc/nginx/conf.d/my-app.conf
        ```
    - Chèn cấu hình 
        ```js
        server {  
            listen 80;  
            server_name IP_ADDRESS;
            
            location / {  
                proxy_pass http://127.0.0.1:3000/;
            }  
        }
        ```
    - Restart Nginx
        ```
        sudo service nginx restart
        ```
# Deployment Options
- SSH Agent Forwarding
    - Trên local: 
        - Chỉnh sửa cấu hình SSH 
            ```
            vim ~/.ssh/config
            ```
        - Chèn IP_ADDRESS vào 
            ```
            Host [IP_ADDRESS]
                ForwardAgent yes
            ```
        - Chạy ssh-add 
            ```
            ssh-add
            ```
        - SSH to server
            ```
            ssh -i key.pem ubuntu@[IP_ADDRESS]
            ```
    - Trên server 
        - Xác thực kết nối với github 
            ```
            ssh -T git@github.com
            ```
# Deployment
- Trên local: 
    - Chạy pm2 setup 
    ```
    pm2 deploy production setup
    ```
    - Chạy deployment
    ```
    pm2 deploy production
    ```
# Kết luận 
Hy vọng, nó sẽ là 1 thông tin bổ ích giúp mọi người trong quá trình làm việc.

Cảm ơn mọi người đã đọc bài viết, hẹn gặp lại !

# Tài liệu tham khảo 
- https://www.fullstackbook.com/guides/how-to-deploy-nextjs-with-pm2