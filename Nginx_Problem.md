[toc]

## 安装Nginx在 阿里云服务器 Cenos8

1. 更新 yum

    ```shell
    sudo yum update
    ```

2. 安装nginx

   ```shell
   sudo yum install nginx
   ```

3. enable nginx服务

   ```shell
   sudo systemctl enable nginx.service
   ```

4. start nginx

   ```shell
   sudo systemctl start nginx.service
   ```

   这一步可能会失败，通过查看：

   /var/log/nginx/error.log

   ![](/Users/zhangyuyang/Desktop/Screenshot/Screenshot 2022-01-13 at 15.58.30.png)

   发现端口被占用

   查看端口并且关闭被占用的端口

   ```shell
   netstat -tulnp | grep :80 # 查看被占用端口
   sudo kill -2 PID # 关闭端口
   ```

   通过 public network 访问 nginx， 

   ```shell
   curl ipinfo.io # 获取 public IP address
   ```

   如果不能访问，有以下几种可能：

   1. 防火墙：

      ```shell
      sudo firewall-cmd --permanent --zone=public --add-service={http, https} # 将 http, https 加入
      sudo firewall-cmd --reload # 重新加载
      sudo firewall-cmd --list-services --zone=public # 查看
      ```

   2. 阿里云的安全组： 需要将 http:80 加入 阿里云的安全组

5. 其他：
   1. nginx 配置文件： /etc/nginx/nginx.conf
   2. 默认 web document 根文件： /usr/share/nginx/html
6. [参考网址](https://www.cyberciti.biz/faq/how-to-install-and-use-nginx-on-centos-8/)

