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