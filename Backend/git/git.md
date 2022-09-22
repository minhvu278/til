## Rebase
- Rebase
    ```
    git rebase --continue
    ```
## Config git 
- Config email password 
    ```
    git config --global user.name "YOUR NAME"
    git config --global user.email "YOUR@EMAIL.com"
    ```
- Generate ssh key 
    ```
    ssh-keygen -t rsa -b 4096 -C "your_mail@example.com" 
    ```
- Add ssh key 
    ```
    cat ~/.ssh/id_rsa.pub
    ```
- Kiểm tra kết nối 
    ```
    ssh -T git@github.com
    ```