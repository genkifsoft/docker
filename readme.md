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