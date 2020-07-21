#### Hướng dẫn học docker
### Thư viện docker
```bash
    https://hub.docker.com/_/ubuntu?tab=tags
```
#### Tải image docker
```bash
    docker pull tên_ubutu
```
#### Xem cái images đã được cài đặt
```bash
    docker images
```
#### Remove một image
```bash
    docker image rm ubuntu:16.04
    or
    docker image rm ID_IMAGE
```
#### Nếu muốn xóa một image đang chạy
```bash
    docker image rm -f ID_IMAGE
```
#### Tương tác docker với teminal
```bash
     docker run -it ID_IMAGE
```

#### Xem tất cả các docker đang chạy
```bash
    docker ps
```
#### Xem docker đang dừng
```bash
    docker ps -a
```
#### Start lại container đang tắt
```bash
    docker start CONTAINER_ID
```
#### Đi vào teminal container
```bash
    docker attach CONTAINER_ID
```
#### Từ những image này tạo ra container
```bash
    docker run -it --name NAME -h HOST image
    NAME: là đặt tên cho container
    HOST: là host của container
```
#### Đang ở teminal của container. Muốn thoát teminal container nó không bị tắt
```bash
    CTRL + P, CTRL + Q
```
### Dừng 1 container đang chạy
```bash
    docker stop CONTAINER_ID
```
#### Đang đứng ở ngoài container mà muốn thi hành 1 container đang chạy
```bash
    docker exec CONTAINER_ID ls-- xem tất cả các file
```
#### Kết nối vô teminal root
```bash
    docker exec -it U1 bash
```

#### Update apt htop
```bash
    apt update -y
```
#### Install htop
```bash
    apt install htop
```
#### Cài đặt vim
```bash
    apt install vim
```
#### Cài đặt ping
```bash
    apt install iputils-ping
```

### Quan trọng
#### Tạo 1 image từ 1 container. Nhớ là có stast là Exited mới build ra được image
```bash
    docker commit CONTAINER image:tag
    docker commit U1 ubutun:version-1
```
#### Save image ra file
```bash
    docker save --ouput myimage.tar CONTAINER_ID
```
#### Muốn phục hồi file image
```bash
    docker load -i myimage.tar
```
### Đặt tên cho image
```bash
    docker tag IMAGE_ID newimage:version2
```
#### Để chia sẻ dữ liệu giữa máy host và container
```bash
    docker run -it -v Thư mục máy tính:/home/dulieu IMAGE_ID
```
#### Để chia sẻ dữ liệu giữa máy host và container và đặt tên 
```bash
    docker run -it -v Thư mục máy tính:/home/dulieu --name NAME IMAGE_ID
```
#### Chia sẻ các file giữa container với nhau
```bash
    docker run -it --name C2 --volumes-from C1:unbuntu:latest
    C2: Đặt tên mới và con container C1 được sinh ra từ unbuntu:latest
```
#### Tạo ổ đĩa với docker
```bash
    docker volume create D1
```
#### Xem tất cả các ổ đĩa
```bash
    docker volume ls
```
#### Xem chi tiết thông tin ổ đĩa
```bash
    docker volume inspect Ổ đĩa
```
#### Xoá ổ đĩa
```bash
    docker volume rm Ổ đĩa
```

#### Move container vào ổ đĩa
```bash
    docker run -it --name C1 --mount source=D2,target=/home/dist2 ubuntu
```
#### Chỉ cho phép chạy 1 lần và xoá nó đi
```bash
    docker run -it -v rm Container
```
#### Xem danh sách network. Mặt định rạo ra 3 mạng và nó tự kết nối mạng bridge
```bash
    docker network ls
```

#### tạo container từ images
```bash
    docker run -it --name B1 busybox
```
#### Xem thông tin chi tiết mạng
```bash
    docker network inspect Tên network
```
#### Cấp phép mạng docker container và mạng local
```bash
    docker run -it --name B3 -p 8888:80 busybox
```
#### Tạo httpd cho container
```bash
    cs var/www
    httpd
```
#### Tạo một mạng riêng
```bash
    docker network create Name
```
#### Tạo 1 container trong 1 netwrok
```bash
    docker run -it --name B3 --network Name_Network
```
#### Để gán 1 network container đang chạy
```bash
    docker network connect NAME_NETWORK _Container_name
```

### Ánh xạ thư mục local vào docker
```bash
    docker run -d --name c-php -h php -v Ổ địa local/:/home/mycode/ --network www-net php:7.3
```
### Chạy vào container
```bash
    docker exec -it c-php bash
```
### Setting Htttpd
```bash
    docker run --rm -v /Volumes/Programmer/docker/mycode/:/home/mycode/  httpd cp /usr/local/apache2/conf/httpd.conf /home/mycode
```
### Uncomment
```bash
    LoadModule proxy_module modules/mod_proxy.so
    LoadModule proxy_fcgi_module modules/mod_proxy_fcgi.so
```
### Add Hadler
```bash
    AddHandler "proxy:fcgi://c-php:9000" .php
```
### Cấu hình host và port cho httpd
```bash
    docker run --network www-net --name c-httpd -h httpd -p 9999:80 -p 443:443 -v /Volumes/Programmer/docker/mycode/:/home/mycode/ -v /Volumes/Programmer/docker/mycode/httpd.conf:/usr/local/apache2/conf/httpd.conf httpd
```
### Tạo httpd và chưa có và chạy nó, ánh xạ và chia sẽ dữ liệu
```bash
    docker run --name c-http -p 9999:80 -p 443:443 -v /Volumes/Programmer/docker/mycode/:/home/mycode/ -v /Volumes/Programmer/docker/mycode/httpd.conf:/usr/local/apache2/conf/httpd.conf --network www-net httpd
```

### Thiết lập biến môi trường
```bash
    docker run -it --rm -e BIEN1=value1 -e BIEN2=value2 busybox
```

### Cài đặt mysql. Tạo file my.cnf
```bash
    docker run --rm -v /Volumes/Programmer/docker/mycode/:/home/mycode mysql cp /etc/mysql/my.cnf /home/mycode/
```
### Cài đặt mật khẩu và ánh xạ db
```bash
    docker run -e MYSQL_ROOT_PASSWORD=abc123 -v /Volumes/Programmer/docker/mycode/my.cnf:/etc/mysql/my.cnf -v /Volumes/Programmer/docker/mycode/db:/var/lib/mysql --name c-mysql mysql
```
### Truy cập mysql
```bash
    docker exec -it c-mysql bash
```
### Truy cập root mysql
```bash
    mysql -u root -pabc123  
```
### Các lệnh cơ bản tương tác với db
```bash
    USE database;
    show databases;
    CREATE USER 'testuser'@'%' IDENTIFIED BY 'testpass';
```
### Cấp quyền cho use
```bash
    GRANT ALL PRIVILEGES ON db_wordpress.* TO 'testuser'@'%';
    flush privileges;
```
### Xem lịch sử của image
```bash
    docker image history ID
```
### Xem trang thái chi tiết Image, Container
```bash
    docker inspectID
```
### Xem các file folder đã xoá
```bash
    docker diff ID
```
### Xem log container dừng số dòng muốn kiểm tra
```bash
    docker logs --tail 10 c-php
```
### Xem log container đang chạy số dòng muốn kiểm tra
```bash
    docker logs -f c-php
```
### Start nhiều container
```bash
    docker start ID1, ID2, ID3...
```
### Xem trạng thái mạng và dung lượng docker đang chạy
```bash
    docker stats c-php c-mysql
```
### XXem trạng thái mạng và dung lượng docker đang chạy tất cả container
```bash
    docker stats
```
### Cài đặt các gói trên Centos
```bash
    yum update -y
    yum install httpd httpd-tools -y
    yum install vim -y
    yum install epel-release -y
    yum update -y
    yum install htop -y
```
### Sao chép file từ local đến trong centos
```bash
    docker cp path_local Ten_container:/path centos =>var/www/html
```
### Lưu container thành image
```bash
    docker commit c-cent myimage:v1
```
### Chạy container từ image
```bash
    docker run --rm -p 9876:80 reposity:tag/container id httpd -D FOREGROUND
```
### Chạy lệnh trong file dockerfile
```bash
    docker build -t name_image -f Dockerfile .(thư mục chứa dockerfile)"." là folder hiện tại
```