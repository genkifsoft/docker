#### Hướng dẫn học docker
### Thư viện docker
```bash
    https://hub.docker.com/_/ubuntu?tab=tags
```
#### Tải image docker
```bash
    docker pull tên
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