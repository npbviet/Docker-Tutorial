# Docker

- [Docker](#docker)
  - [1. Docker là gì?](#1-docker-là-gì)
  - [2. Kiến trúc Docker](#2-kiến-trúc-docker)
  - [3. Các khái niệm chính](#3-các-khái-niệm-chính)
  - [4. Sơ đồ \& mô tả quy trình CI/CD với Docker và AWS](#4-sơ-đồ--mô-tả-quy-trình-cicd-với-docker-và-aws)
    - [Mô tả quy trình](#mô-tả-quy-trình)
    - [Sơ đồ quy trình CI/CD với Docker và AWS](#sơ-đồ-quy-trình-cicd-với-docker-và-aws)
    - [Diễn giải sơ đồ:](#diễn-giải-sơ-đồ)
    - [Các thành phần chính:](#các-thành-phần-chính)
  - [5. Các lệnh Docker cơ bản](#5-các-lệnh-docker-cơ-bản)
    - [Quản lý Image](#quản-lý-image)
    - [Quản lý Container](#quản-lý-container)
  - [6. Ví dụ Dockerfile cho ứng dụng Node.js](#6-ví-dụ-dockerfile-cho-ứng-dụng-nodejs)
  - [7. Docker Compose](#7-docker-compose)
    - [Ví dụ `docker-compose.yml`](#ví-dụ-docker-composeyml)
    - [Lệnh Docker Compose](#lệnh-docker-compose)
  - [8. Bài tập thực hành cho Fresher](#8-bài-tập-thực-hành-cho-fresher)
    - [Bài tập 1: Hello World](#bài-tập-1-hello-world)
    - [Bài tập 2: Chạy Web Server Nginx](#bài-tập-2-chạy-web-server-nginx)
    - [Bài tập 3: Build Image cho ứng dụng Node.js](#bài-tập-3-build-image-cho-ứng-dụng-nodejs)
    - [Bài tập 4: Sử dụng Volume để lưu dữ liệu](#bài-tập-4-sử-dụng-volume-để-lưu-dữ-liệu)
    - [Bài tập 5: Chạy ứng dụng đa container với Docker Compose](#bài-tập-5-chạy-ứng-dụng-đa-container-với-docker-compose)
  - [9. Bài tập về nhà: Xây dựng ứng dụng Full-Stack](#9-bài-tập-về-nhà-xây-dựng-ứng-dụng-full-stack)
    - [Các bước thực hiện:](#các-bước-thực-hiện)
      - [Bước 1: Cấu trúc dự án](#bước-1-cấu-trúc-dự-án)
      - [Bước 2: Xây dựng Backend API (Node.js)](#bước-2-xây-dựng-backend-api-nodejs)
      - [Bước 3: Xây dựng Frontend (Next.js)](#bước-3-xây-dựng-frontend-nextjs)
      - [Bước 4: Viết file Docker Compose](#bước-4-viết-file-docker-compose)
      - [Bước 5: Chạy và kiểm tra](#bước-5-chạy-và-kiểm-tra)
  - [10. Build \& Push image lên Docker Hub](#10-build--push-image-lên-docker-hub)
      - [Bước 1: Build image](#bước-1-build-image)
      - [Bước 2: Tag lại image (nếu cần)](#bước-2-tag-lại-image-nếu-cần)
      - [Bước 3: Đăng nhập Docker Hub](#bước-3-đăng-nhập-docker-hub)
      - [Bước 4: Push image lên Docker Hub](#bước-4-push-image-lên-docker-hub)
      - [Bước 5: Kiểm tra trên Docker Hub](#bước-5-kiểm-tra-trên-docker-hub)
      - [Bước 6: Pull image về máy khác (hoặc xóa local rồi pull lại)](#bước-6-pull-image-về-máy-khác-hoặc-xóa-local-rồi-pull-lại)
  - [11. Bài tập nâng cao: CI/CD với Docker Hub và Self-hosted Runner](#11-bài-tập-nâng-cao-cicd-với-docker-hub-và-self-hosted-runner)
    - [Các bước thực hiện chi tiết:](#các-bước-thực-hiện-chi-tiết)
      - [**Bước 1: Build image trên self-hosted runner**](#bước-1-build-image-trên-self-hosted-runner)
      - [**Bước 2: Đăng nhập Docker Hub trên self-hosted runner**](#bước-2-đăng-nhập-docker-hub-trên-self-hosted-runner)
      - [**Bước 3: Push image lên Docker Hub**](#bước-3-push-image-lên-docker-hub)
      - [**Bước 4: Pull image về lại máy (self-hosted runner)**](#bước-4-pull-image-về-lại-máy-self-hosted-runner)
      - [**Bước 5: Run bằng docker-compose**](#bước-5-run-bằng-docker-compose)
      - [**Bước 6: Clean up (tùy chọn)**](#bước-6-clean-up-tùy-chọn)
    - [**Tích hợp vào GitHub Actions Workflow (ví dụ)**](#tích-hợp-vào-github-actions-workflow-ví-dụ)
  - [12. Tài nguyên học tập](#12-tài-nguyên-học-tập)


## 1. Docker là gì?
- **Docker** là một nền tảng container hóa (containerization) giúp đóng gói ứng dụng và các dependencies của nó vào một container.
- **Container** là một môi trường độc lập, nhẹ và có thể chạy nhất quán trên mọi môi trường (development, staging, production).
- **Lợi ích:**
  - **Nhất quán**: "It works on my machine" không còn là vấn đề.
  - **Nhanh chóng**: Khởi động container gần như tức thì.
  - **Linh hoạt**: Chạy được trên mọi hệ điều hành (Linux, Windows, macOS).
  - **Tối ưu tài nguyên**: Hiệu quả hơn máy ảo (VM) vì chia sẻ kernel với host.

## 2. Kiến trúc Docker
- **Docker Client**: Giao diện dòng lệnh (`docker`) để tương tác với Docker Daemon.
- **Docker Daemon (dockerd)**: Chạy trên host, quản lý các đối tượng Docker (images, containers, networks, volumes).
- **Docker Registry**: Nơi lưu trữ Docker images (Docker Hub, ECR, GCR, ...).

## 3. Các khái niệm chính
- **Image**: Template chỉ đọc (read-only) chứa các chỉ dẫn để tạo container.
- **Container**: Một instance của image, là môi trường chạy ứng dụng.
- **Dockerfile**: File văn bản chứa các lệnh để build một Docker image.
- **Volume**: Cơ chế lưu trữ dữ liệu bền vững (persistent) cho container.
- **Network**: Kết nối các container với nhau và với host.

## 4. Sơ đồ & mô tả quy trình CI/CD với Docker và AWS

### Mô tả quy trình
1. **Developer** push code lên GitHub (hoặc GitLab, Bitbucket...).
2. **GitHub Actions** (hoặc một CI server khác) sẽ tự động:
   - **Build Docker image** từ source code.
   - **Push image** lên một Docker Registry (thường là Docker Hub hoặc Amazon ECR).
3. **AWS (EC2, ECS, EKS, hoặc Lightsail)** sẽ:
   - **Pull image** mới nhất từ Registry.
   - **Restart service/container** để chạy phiên bản mới.
4. **Ứng dụng** được cập nhật và phục vụ người dùng cuối.

### Sơ đồ quy trình CI/CD với Docker và AWS

```
+-------------------+         +---------------------+         +---------------------+         +---------------------+
|                   |         |                     |         |                     |         |                     |
|   Developer       +-------->+   GitHub Repository +-------->+   CI/CD Pipeline    +-------->+   AWS (ECS/EC2/...) |
|   (Push code)     |         |   (Source code)     |         |   (GitHub Actions)  |         |   (Pull & Deploy)   |
|                   |         |                     |         |                     |         |                     |
+-------------------+         +---------------------+         +---------------------+         +---------------------+
                                                                  |         |
                                                                  |         |
                                                                  v         v
                                                          +---------------------+
                                                          |   Docker Registry   |
                                                          | (Docker Hub/ECR)    |
                                                          +---------------------+
```

### Diễn giải sơ đồ:
1. **Developer** push code lên GitHub.
2. **GitHub Actions** (CI/CD) tự động build Docker image và push lên Docker Registry (Docker Hub hoặc AWS ECR).
3. **AWS** (ECS, EC2, EKS, Lightsail, ...) sẽ pull image mới nhất từ Registry về và deploy (restart container/service).
4. Ứng dụng được cập nhật và phục vụ người dùng.

**Kết:**
> Từ AWS, hệ thống sẽ pull image mới nhất từ registry và tự động cập nhật ứng dụng phục vụ người dùng cuối.

### Các thành phần chính:
- **Source code repository:** GitHub, GitLab, Bitbucket...
- **CI/CD pipeline:** GitHub Actions, GitLab CI, Jenkins, CircleCI...
- **Docker Registry:** Docker Hub, Amazon ECR, GitHub Container Registry...
- **AWS Service:** ECS (Fargate/EC2), EKS (Kubernetes), EC2 (tự quản lý), Lightsail...

## 5. Các lệnh Docker cơ bản

### Quản lý Image
- `docker build -t <image_name> .`: Build image từ Dockerfile
- `docker images`: Liệt kê các images
- `docker rmi <image_id>`: Xóa một image
- `docker pull <image_name>`: Tải image từ registry
- `docker push <username>/<image_name>`: Đẩy image lên registry

### Quản lý Container
- `docker run <image_name>`: Chạy container từ image
- `docker run -d -p <host_port>:<container_port> <image_name>`: Chạy container ở chế độ detached và map port
- `docker ps`: Liệt kê các container đang chạy
- `docker ps -a`: Liệt kê tất cả container
- `docker stop <container_id>`: Dừng container
- `docker rm <container_id>`: Xóa container
- `docker logs <container_id>`: Xem log của container
- `docker exec -it <container_id> bash`: Truy cập vào container

## 6. Ví dụ Dockerfile cho ứng dụng Node.js

```Dockerfile
# Sử dụng base image Node.js
FROM node:18-alpine

# Thiết lập thư mục làm việc trong container
WORKDIR /app

# Copy package.json và package-lock.json
COPY package*.json ./

# Cài đặt dependencies
RUN npm install

# Copy source code vào container
COPY . .

# Mở port 3000
EXPOSE 3000

# Lệnh chạy ứng dụng
CMD ["node", "server.js"]
```

## 7. Docker Compose
- Công cụ để định nghĩa và chạy các ứng dụng đa container.
- Sử dụng file `docker-compose.yml` để cấu hình các services, networks, volumes.

### Ví dụ `docker-compose.yml`

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
  db:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

### Lệnh Docker Compose
- `docker-compose up`: Build và chạy các services
- `docker-compose down`: Dừng và xóa các containers, networks
- `docker-compose build`: Build lại các services
- `docker-compose ps`: Liệt kê các containers

## 8. Bài tập thực hành cho Fresher

### Bài tập 1: Hello World
- **Mục tiêu**: Làm quen với việc chạy một container.
- **Yêu cầu**: Chạy container `hello-world` và xem output.
- **Lệnh**: `docker run hello-world`
- **Kiểm tra**: Bạn sẽ thấy một message chào mừng từ Docker.

### Bài tập 2: Chạy Web Server Nginx
- **Mục tiêu**: Chạy một service và truy cập từ bên ngoài.
- **Yêu cầu**:
  1. Chạy container Nginx.
  2. Map port `8080` của máy bạn vào port `80` của container.
  3. Chạy ở chế độ detached (`-d`).
- **Lệnh**: `docker run -d -p 8080:80 nginx`
- **Kiểm tra**: Mở trình duyệt và truy cập `http://localhost:8080`. Bạn sẽ thấy trang chào mừng của Nginx.
- **Dọn dẹp**:
  1. `docker ps` để lấy container ID.
  2. `docker stop <container_id>`
  3. `docker rm <container_id>`

### Bài tập 3: Build Image cho ứng dụng Node.js
- **Mục tiêu**: Học cách tạo image riêng với Dockerfile.
- **Yêu cầu**:
  1. Tạo thư mục `node-app`.
  2. Bên trong, tạo file `server.js`:
     ```javascript
     const http = require('http');
     const server = http.createServer((req, res) => {
       res.writeHead(200, { 'Content-Type': 'text/plain' });
       res.end('Hello from Docker!\n');
     });
     server.listen(3000, '0.0.0.0', () => {
       console.log('Server running at http://0.0.0.0:3000/');
     });
     ```
  3. Tạo file `Dockerfile` (không có đuôi file) trong cùng thư mục:
     ```Dockerfile
     FROM node:18-alpine
     WORKDIR /app
     COPY server.js .
     EXPOSE 3000
     CMD ["node", "server.js"]
     ```
  4. Build image và đặt tên là `my-node-app`.
- **Lệnh**:
  1. `cd node-app`
  2. `docker build -t my-node-app .`
- **Kiểm tra**:
  1. `docker images` để xem image của bạn.
  2. `docker run -d -p 3001:3000 my-node-app`
  3. Truy cập `http://localhost:3001` trên trình duyệt.

### Bài tập 4: Sử dụng Volume để lưu dữ liệu
- **Mục tiêu**: Hiểu cách dữ liệu được lưu trữ bền vững.
- **Yêu cầu**:
  1. Tạo một volume tên là `my-data`.
  2. Chạy container `ubuntu`.
  3. Mount volume `my-data` vào thư mục `/data` trong container.
  4. Tạo một file `test.txt` trong `/data`.
  5. Dừng container.
  6. Chạy container mới, cũng mount volume `my-data` và kiểm tra file `test.txt` còn tồn tại không.
- **Lệnh**:
  1. `docker volume create my-data`
  2. `docker run -it -v my-data:/data ubuntu bash`
     - Bên trong container: `echo "Persistent Data" > /data/test.txt` và `exit`
  3. `docker run -it -v my-data:/data ubuntu bash`
     - Bên trong container: `cat /data/test.txt`
- **Kiểm tra**: Lệnh `cat` sẽ hiển thị "Persistent Data".

### Bài tập 5: Chạy ứng dụng đa container với Docker Compose
- **Mục tiêu**: Làm quen với việc quản lý nhiều services.
- **Yêu cầu**:
  1. Tạo thư mục `compose-app`.
  2. Tạo file `docker-compose.yml` với nội dung:
      ```yaml
      version: '3.8'
      services:
        web:
          image: nginx:latest
          ports:
            - "8081:80"
        database:
          image: redis:latest
      ```
  3. Chạy ứng dụng.
- **Lệnh**:
  1. `cd compose-app`
  2. `docker-compose up -d`
- **Kiểm tra**:
  1. `docker-compose ps` để xem 2 services `web` và `database` đang chạy.
  2. Truy cập `http://localhost:8081` để thấy trang Nginx.
- **Dọn dẹp**: `docker-compose down`

## 9. Bài tập về nhà: Xây dựng ứng dụng Full-Stack

**Mục tiêu:**
Xây dựng và chạy một ứng dụng web hoàn chỉnh bao gồm Frontend, Backend, Database, và Cache, tất cả được quản lý bởi Docker Compose. Đây là bài tập không có code giải pháp chi tiết để bạn có thể tự mình thực hành và giải quyết vấn đề.

**Stack công nghệ:**
- **Frontend**: Next.js
- **Backend**: Node.js (sử dụng Express.js)
- **Database**: MySQL
- **Cache**: Redis
- **Orchestration**: Docker Compose

**Yêu cầu ứng dụng:**
Xây dựng một ứng dụng quản lý đơn giản với các tính năng sau:
1.  **Trang chủ (Visitor Counter)**:
    -   Hiển thị số lượt truy cập.
    -   Mỗi lần tải lại, số lượt truy cập tăng lên.
    -   Dữ liệu được lưu trong MySQL và cache bằng Redis.
2.  **Trang quản lý Ghi chú (CRUD với Database)**:
    -   Tạo, đọc, cập nhật, xóa các ghi chú.
    -   Dữ liệu được lưu trực tiếp vào MySQL.
3.  **Trang quản lý Cache (CRUD với Redis)**:
    -   Giao diện để xem, thêm, sửa, xóa các key-value trong Redis.
    -   Giúp trực quan hóa dữ liệu cache.

---

### Các bước thực hiện:

#### Bước 1: Cấu trúc dự án
Tạo cấu trúc thư mục cho dự án của bạn như sau:

```
fullstack-docker-app/
├── backend/
│   ├── src/
│   ├── package.json
│   └── Dockerfile
├── frontend/
│   ├── app/
│   ├── package.json
│   └── Dockerfile
└── docker-compose.yml
```

#### Bước 2: Xây dựng Backend API (Node.js)
1.  **Khởi tạo dự án Node.js** trong thư mục `backend`. Sử dụng Express.js.
2.  **Viết API**:
    -   Tạo một endpoint `GET /api/counter`.
        -   Logic: Lấy giá trị từ Redis, nếu không có thì lấy từ MySQL, lưu vào Redis, tăng giá trị, cập nhật lại DB và Redis, trả về giá trị mới.
    -   Tạo các endpoint CRUD cho Ghi chú (ví dụ: `Notes`):
        -   `GET /api/notes`: Lấy danh sách tất cả ghi chú.
        -   `POST /api/notes`: Tạo một ghi chú mới.
        -   `PUT /api/notes/:id`: Cập nhật một ghi chú.
        -   `DELETE /api/notes/:id`: Xóa một ghi chú.
    -   Tạo các endpoint CRUD cho Redis:
        -   `GET /api/redis/keys`: Lấy tất cả các keys.
        -   `GET /api/redis/keys/:key`: Lấy giá trị của một key.
        -   `POST /api/redis`: Tạo một cặp key-value mới.
        -   `DELETE /api/redis/keys/:key`: Xóa một key.
3.  **Kết nối Database & Cache**: Viết code để kết nối tới MySQL và Redis. Thông tin kết nối (host, user, password) nên được đọc từ biến môi trường.
4.  **Tạo `Dockerfile` cho Backend**:
    -   Sử dụng base image `node:18-alpine`.
    -   **Quan trọng**: Đảm bảo cài đặt `mysql2` và `redis` clients.
    -   Copy `package.json` và cài đặt dependencies.
    -   Copy toàn bộ source code.
    -   Expose port mà API của bạn đang chạy (ví dụ: `3001`).
    -   Dùng `CMD` để khởi động server.

#### Bước 3: Xây dựng Frontend (Next.js)
1.  **Khởi tạo dự án Next.js** trong thư mục `frontend`.
2.  **Thiết kế giao diện**:
    -   Tạo một trang đơn giản hiển thị: "Số lượt truy cập: [số]".
    -   Tạo một trang `/notes` để quản lý ghi chú với các chức năng thêm, sửa, xóa.
    -   Tạo một trang `/redis-admin` để thao tác với Redis cache.
3.  **Gọi API**:
    -   Sử dụng `useEffect` và `fetch` (hoặc `axios`) để gọi đến endpoint `/api/counter` của backend khi component được mount.
    -   Trên các trang tương ứng, gọi các API CRUD cho Notes và Redis.
    -   Hiển thị giá trị nhận được lên giao diện.
4.  **Tạo `Dockerfile` cho Frontend**:
    -   Sử dụng base image `node:18-alpine`.
    -   Tận dụng multi-stage builds để tối ưu kích thước image.
    -   **Stage 1 (Build)**: Cài dependencies và build ứng dụng (`npm run build`).
    -   **Stage 2 (Production)**: Copy kết quả build từ stage 1 và chỉ cài đặt production dependencies (`npm install --production`).
    -   Expose port `3000`.
    -   Dùng `CMD` để chạy ứng dụng Next.js (`npm start`).

#### Bước 4: Viết file Docker Compose
Tạo file `docker-compose.yml` ở thư mục gốc.
1.  **Định nghĩa 4 services**: `frontend`, `backend`, `db`, `cache`.
2.  **Cấu hình `frontend` service**:
    -   Sử dụng `build: ./frontend` để Docker Compose tự build image.
    -   Map port `3000:3000`.
    -   Thiết lập `depends_on: - backend` để frontend khởi động sau backend.
3.  **Cấu hình `backend` service**:
    -   Sử dụng `build: ./backend`.
    -   Map port, ví dụ `3001:3001`.
    -   Sử dụng `depends_on` để đảm bảo `db` và `cache` khởi động trước.
    -   Truyền các biến môi trường cần thiết cho việc kết nối database và cache.
4.  **Cấu hình `db` service (MySQL)**:
    -   Sử dụng image chính thức `mysql:8.0`.
    -   Thiết lập các biến môi trường bắt buộc của MySQL: `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`.
    -   **Quan trọng**: Cần có một cơ chế để khởi tạo bảng (table) cho `Notes` khi database khởi động lần đầu. Bạn có thể dùng một init script.
    -   Tạo một `volume` để dữ liệu của MySQL không bị mất khi container khởi động lại.
5.  **Cấu hình `cache` service (Redis)**:
    -   Sử dụng image chính thức `redis:alpine`.

#### Bước 5: Chạy và kiểm tra
1.  Từ thư mục gốc của dự án, chạy lệnh: `docker-compose up --build`.
2.  Mở trình duyệt và truy cập `http://localhost:3000`. Bạn sẽ thấy giao diện frontend.
3.  Kiểm tra xem số lượt truy cập có hiển thị và tăng lên sau mỗi lần refresh không.
4.  Truy cập trang `/notes` và `/redis-admin` để kiểm tra các chức năng CRUD.
5.  Sử dụng `docker-compose logs -f <service_name>` để xem log của từng service và debug nếu có lỗi.
6.  Khi hoàn thành, dùng `docker-compose down` để dừng và xóa toàn bộ tài nguyên.

## 10. Build & Push image lên Docker Hub

**Mục tiêu:**
- Thành thạo quy trình build image từ source code và đẩy lên Docker Hub để chia sẻ hoặc deploy ở bất kỳ đâu.

**Yêu cầu:**
1. Tạo tài khoản Docker Hub (nếu chưa có): https://hub.docker.com/
2. Build một Docker image cho ứng dụng Node.js hoặc bất kỳ app nào bạn có.
3. Tag image đúng chuẩn Docker Hub.
4. Đăng nhập Docker Hub từ terminal.
5. Push image lên Docker Hub.
6. Kiểm tra lại trên Docker Hub và thử pull image về máy khác (hoặc xóa local rồi pull lại).

**Các bước thực hiện:**

#### Bước 1: Build image
```bash
docker build -t <your-dockerhub-username>/my-demo-app:latest .
```

#### Bước 2: Tag lại image (nếu cần)
```bash
docker tag my-demo-app <your-dockerhub-username>/my-demo-app:latest
```

#### Bước 3: Đăng nhập Docker Hub
```bash
docker login
```
> Nhập username và password Docker Hub.

#### Bước 4: Push image lên Docker Hub
```bash
docker push <your-dockerhub-username>/my-demo-app:latest
```

#### Bước 5: Kiểm tra trên Docker Hub
- Truy cập https://hub.docker.com/repositories và kiểm tra repo `my-demo-app` đã xuất hiện.

  #### Bước 6: Pull image về máy khác (hoặc xóa local rồi pull lại)
  ```bash
  docker rmi <your-dockerhub-username>/my-demo-app:latest
  docker pull <your-dockerhub-username>/my-demo-app:latest
  ```

  **Gợi ý mở rộng:**
  - Thử push image của backend, frontend, hoặc bất kỳ microservice nào bạn có.
  - Thử sử dụng image này trong một file `docker-compose.yml` để chạy ứng dụng.

## 11. Bài tập nâng cao: CI/CD với Docker Hub và Self-hosted Runner

**Mục tiêu:**
Thiết lập một pipeline CI/CD hoàn chỉnh trên self-hosted runner. Toàn bộ quy trình sẽ được thực hiện trên máy cá nhân của bạn, bao gồm các bước rõ ràng:
1. **Build image**
2. **Push image lên Docker Hub**
3. **Pull image về lại máy**
4. **Run bằng docker-compose**

---

### Các bước thực hiện chi tiết:

#### **Bước 1: Build image trên self-hosted runner**
- **Mục tiêu:** Tạo image mới nhất cho backend và frontend từ source code.
- **Lệnh thực hiện:**
  ```bash
  docker build -t <your-dockerhub-username>/my-fullstack-backend:latest ./backend
  docker build -t <your-dockerhub-username>/my-fullstack-frontend:latest ./frontend
  ```

#### **Bước 2: Đăng nhập Docker Hub trên self-hosted runner**
- **Mục tiêu:** Đảm bảo runner có quyền push image lên Docker Hub.
- **Lệnh thực hiện:**
  ```bash
  docker login -u <your-dockerhub-username> -p <your-dockerhub-token>
  ```

#### **Bước 3: Push image lên Docker Hub**
- **Mục tiêu:** Đưa image vừa build lên Docker Hub để có thể pull ở bất kỳ đâu.
- **Lệnh thực hiện:**
  ```bash
  docker push <your-dockerhub-username>/my-fullstack-backend:latest
  docker push <your-dockerhub-username>/my-fullstack-frontend:latest
  ```

#### **Bước 4: Pull image về lại máy (self-hosted runner)**
- **Mục tiêu:** Đảm bảo luôn sử dụng image mới nhất từ Docker Hub (giả lập môi trường production).
- **Lệnh thực hiện:**
  ```bash
  docker pull <your-dockerhub-username>/my-fullstack-backend:latest
  docker pull <your-dockerhub-username>/my-fullstack-frontend:latest
  ```

#### **Bước 5: Run bằng docker-compose**
- **Mục tiêu:** Khởi động lại toàn bộ hệ thống với image mới nhất.
- **Lệnh thực hiện:**
  ```bash
  docker-compose down || true
  docker-compose up -d
  ```

#### **Bước 6: Clean up (tùy chọn)**
- **Mục tiêu:** Dọn dẹp các image cũ không còn sử dụng để tiết kiệm dung lượng.
- **Lệnh thực hiện:**
  ```bash
  docker image prune -f
  ```

---

### **Tích hợp vào GitHub Actions Workflow (ví dụ)**

```yaml
name: Build, Push, Pull & Deploy (Self-hosted)

on:
  push:
    branches: [ main ]

jobs:
  build_push_pull_run:
    runs-on: self-hosted
    steps:
      - name: Checkout code

      - name: Build backend image

      - name: Build frontend image

      - name: Login to Docker Hub

      - name: Push backend image

      - name: Push frontend image

      - name: Pull backend image

      - name: Pull frontend image

      - name: Stop and remove old containers

      - name: Start new containers

      - name: Clean up old images
```

---

**Lưu ý:**
- Đảm bảo file `docker-compose.yml` sử dụng image từ Docker Hub, không dùng build local.
- Secrets `DOCKERHUB_USERNAME` và `DOCKERHUB_TOKEN` phải được cấu hình trong repo.
- Có thể chia nhỏ các step này thành script riêng để dễ debug và bảo trì.

## 12. Tài nguyên học tập
- [Docker Documentation](https://docs.docker.com/)
- [Play with Docker](https://labs.play-with-docker.com/)
- [Awesome Docker (GitHub)](https://github.com/veggiemonk/awesome-docker)
- [Docker Curriculum](https://docker-curriculum.com/)
- [Viblo Docker Series](https://viblo.asia/tags/docker)

---
**Ghi chú:** Docker là một công cụ mạnh mẽ trong DevOps. Hãy bắt đầu với các lệnh cơ bản và dần dần tìm hiểu các khái niệm nâng cao như Docker Swarm, Kubernetes. 