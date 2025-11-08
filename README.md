# BÀI TẬP 3     : MÔN PHÁT TRIỂN ỨNG DỤNG TRÊN NỀN WEB
## Họ tên       : Vũ Việt Anh
## Lớp học phần : K58KTP.K01
## MSSV: K225480106082

# LẬP TRÌNH ỨNG DỤNG WEB TRÊN NỀN LINUX.</P>
## 1. Cài đặt môi trường linux
## 2. Cài đặt Docker
## 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container
## 4. Lập trình web frontend+backend
## 5. Nginx làm web-server

## Bài làm
### 1. Chọn Docker và WSL2
- enable wsl: cài đặt docker desktop
- enable wsl: cài đặt ubuntu
<img width="1471" height="539" alt="image" src="https://github.com/user-attachments/assets/3caf688c-5b29-4507-a246-3c2056a2c4c4" />

<img width="1111" height="426" alt="image" src="https://github.com/user-attachments/assets/9d72cbb4-76a0-40a5-a7fe-89b0ef6179aa" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6f977cd6-c0f7-4767-89da-efc066f25630" />

- Tạo username: vietanh
- Password: 123 và nhập lại lần 2
<img width="1253" height="370" alt="image" src="https://github.com/user-attachments/assets/be980d71-25c2-4127-9e30-9d23908d28b6" />

### 2. Cài đặt Docker Desktop
- Truy cập trang: https://www.docker.com/
  + Chọn bản: Windows - AMD64
<img width="1919" height="866" alt="image" src="https://github.com/user-attachments/assets/2f0f2f0a-4347-4455-b16a-9e78b85cec4a" />

- Bật WSL:
  + Vào Docker Desktop -> Settings -> Resources -> WSL Integration -> Kích hoạt Ubuntu
  + Ấn Apply & restart
<img width="1919" height="1018" alt="image" src="https://github.com/user-attachments/assets/c8608fb8-9694-417c-9ddc-31ff32b8953f" />

- Mở Ubuntu (WSL2) rồi nhập: docker version
<img width="1473" height="752" alt="image" src="https://github.com/user-attachments/assets/a226b79f-f9c7-4a28-98b1-73769b867cc3" />
  -> Hiện như này là đã thành công

### 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container
- Tạo thư mục:
  + Ở Ubuntu nhập:
    ```
    cd /mnt/d

    mkdir baitap3_laptrinhweb

    cd baitap3_laptrinhweb
    ```
<img width="664" height="97" alt="image" src="https://github.com/user-attachments/assets/db47e2d5-f225-4662-9301-445ac6cf1584" />

- Tạo 1 file docker-compose.yml
  + Nhập nano docker-compose.yml
<img width="1466" height="759" alt="image" src="https://github.com/user-attachments/assets/23d996e0-d6e4-4c49-820d-f364d9e4cd54" />

```
version: "3.8"

services:
  mariadb:
    image: mariadb:10.6
    container_name: mariadb
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: webdb
    ports:
      - "3306:3306"
    volumes:
      - mariadb_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin
    restart: always
    environment:
      PMA_HOST: mariadb
      PMA_USER: root
      PMA_PASSWORD: root
    ports:
      - "8080:80"
    depends_on:
      - mariadb

  nodered:
    image: nodered/node-red
    container_name: nodered
    restart: always
    ports:
      - "1880:1880"
    volumes:
      - nodered_data:/data

influxdb:
    image: influxdb:1.8
    container_name: influxdb
    restart: always
    ports:
      - "8086:8086"
    volumes:
      - influxdb_data:/var/lib/influxdb

  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - influxdb
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin

  nginx:
    image: nginx:latest
    container_name: nginx
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./frontend:/usr/share/nginx/html

volumes:
  mariadb_data:
  influxdb_data:
  nodered_data:
```
- Tạo file nginx.conf:
  + Ở /mnt/d/baitap3_laptrinhweb, gõ lệnh: nano nginx.conf

```
events {}

http {
  server {
    listen 80;
    server_name vietanh.com;

    # Trang web chính (Frontend)
    location / {
      root /usr/share/nginx/html;
      index index.html;
    }

    # Truy cập Node-RED qua http://vietanh.com/nodered
    location /nodered/ {
      proxy_pass http://nodered:1880/;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
    }

    # Truy cập Grafana qua http://vietanh.com/grafana
    location /grafana/ {
      proxy_pass http://grafana:3000/;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
    }
  }
}
```

- Tạo thư mục giao diện web:
  + Ở Ubuntu ( thư mục /mnt/d/baitap3_laptrinhweb), nhập: mkdir frontend
  + Tạo file index.html để kiểm tra: nano frontend/index.html
```
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Website Vũ Việt Anh</title>
  <style>
    /* Toàn trang */
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: #f2f2f2;
      text-align: center;
      padding: 100px 20px;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      animation: fadeIn 1.5s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Tiêu đề chính */
    h1 {
      font-size: 52px;
      margin-bottom: 25px;
      background: linear-gradient(90deg, #00c6ff, #0072ff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      letter-spacing: 1px;
    }
    /* Dòng mô tả */
    p {
      font-size: 20px;
      max-width: 600px;
      line-height: 1.6;
      margin-bottom: 40px;
      color: #d8e1e9;
    }

    /* Nút bấm */
    .btn {
      display: inline-block;
      background: linear-gradient(90deg, #00c6ff, #0072ff);
      color: white;
      padding: 14px 30px;
      text-decoration: none;
      border-radius: 50px;
      font-weight: 600;
      font-size: 16px;
      margin: 10px;
      transition: all 0.3s ease;
      box-shadow: 0 4px 12px rgba(0, 114, 255, 0.3);
    }

    .btn:hover {
      transform: scale(1.08);
      box-shadow: 0 6px 16px rgba(0, 114, 255, 0.5);
    }

    /* Footer */
    footer {
      margin-top: 50px;
      font-size: 14px;
      opacity: 0.8;
    }
  </style>
</head>
<body>
  <h1>🌐 Website Vũ Việt Anh</h1>
  <p>Chào mừng bạn đến với hệ thống web cá nhân của <strong>Vũ Việt Anh</strong> —
     được triển khai trên nền tảng <strong>Docker + Nginx + Node-RED + Grafana</strong>.</p>

  <a href="/nodered/" class="btn">🚀 Truy cập Node-RED</a>
  <a href="/grafana/" class="btn">📊 Xem biểu đồ Grafana</a>

  <footer>© 2025 - Thiết kế bởi Vũ Việt Anh | Web phát triển ứng dụng trên nền Linux</footer>
</body>
</html>
```
-> Ctrl + O rồi Enter 
-> Ctrl + X để thoát

- Chạy hệ thống:
  + Nhập: docker compose up -d
<img width="975" height="314" alt="image" src="https://github.com/user-attachments/assets/6c970a34-013e-494f-97fe-ea257f3e2b64" />

  + Sau đó kiểm tra container bằng cách nhập: docker ps
<img width="1919" height="1015" alt="image" src="https://github.com/user-attachments/assets/b81c3b96-2984-459b-a982-c6e3fee0e8f9" />

- Chạy thử trên trình duyệt:
  + Trang web chính: http://localhost/
<img width="1919" height="964" alt="image" src="https://github.com/user-attachments/assets/5eabeb3b-7cf1-42f1-a7cf-b9f3823f819f" />

  + Node-RED: http://localhost:1880/
<img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/7d1a4a5e-fe9f-4677-9091-04097f89a6b4" />

  + Grafana: http://localhost:3000/
<img width="1919" height="965" alt="image" src="https://github.com/user-attachments/assets/c9b909fa-7975-47a7-9bc0-e793c017f52e" />

  + phpMyAdmin: http://localhost:8081/
<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/a29a9ec1-9d17-4392-a24b-4b707de01c50" />

### 4. Lập trình web frontend+backend
- Truy cập: http://localhost:8081/ -> đăng nhập:
<img width="1919" height="966" alt="image" src="https://github.com/user-attachments/assets/3db6445e-0059-4602-8960-257b37505272" />

<img width="1919" height="967" alt="image" src="https://github.com/user-attachments/assets/af660f9f-0b2e-48e6-8fba-eb5c66183f69" />

- Kết nối MariaDB & InfluxDB:
<img width="1919" height="969" alt="image" src="https://github.com/user-attachments/assets/f08c34dd-b6e3-48ec-b5b1-6e632d8888ec" />
- MySQLdatabase:
  + Host: mariadb
  + Port: 3306
  + User: iotuser
  + Password: iotuser
  + Database: iotdb
<img width="1919" height="966" alt="image" src="https://github.com/user-attachments/assets/eefab5f5-9feb-485e-9209-5b1d9325371c" />
- Function:
<img width="1919" height="965" alt="Ảnh chụp màn hình 2025-11-08 141411" src="https://github.com/user-attachments/assets/dbcba96d-fada-4749-ad6e-25148410f6b5" />
- Inject:
<img width="1919" height="964" alt="image" src="https://github.com/user-attachments/assets/208196ac-6ac0-454d-b973-d78af32898b0" />
- InfluxDB:
<img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/5a181503-bfc3-4137-a6f0-1203de718250" />

- Cấu hình Node-RED: vào Node-RED cài các node sau:
  + node-red-contrib-influxdb
  + node-red-node-random
  + node-red-dashboard
  + node-red-node-mysql
<img width="908" height="441" alt="image" src="https://github.com/user-attachments/assets/41da4401-4433-470b-931c-df2d9201e746" />

<img width="890" height="444" alt="image" src="https://github.com/user-attachments/assets/ef89d6f6-415d-4a02-8eed-48f2ec30c4f8" />

<img width="893" height="448" alt="image" src="https://github.com/user-attachments/assets/d0418579-4d71-4248-b81e-884affeb6834" />

<img width="888" height="412" alt="image" src="https://github.com/user-attachments/assets/492066a1-89c6-4e7f-8985-6c5aa91734d7" />

- Kết nối Grafana và hiển thị biểu đồ:
  + Truy cập vào: http://localhost:3000 sẽ vào trang đăng nhập
  + Username: admin
  + Password: admin
-> Sau đó sẽ vào bước nhập mật khẩu mới và xác nhận mật khẩu.
- Chọn Connections -> Data sources
  + Query language: InfluxQL
  + User: iotuser
  + Password: 123456
-> Save & test
<img width="975" height="522" alt="image" src="https://github.com/user-attachments/assets/6dff074a-3ea6-4aea-a3af-d88c0dd7c11a" />

<img width="975" height="517" alt="image" src="https://github.com/user-attachments/assets/a3949e31-7fbd-4d71-8eb6-d2c2be7947da" />

<img width="975" height="514" alt="image" src="https://github.com/user-attachments/assets/72f6a8ba-c6f4-4a1a-8590-82cf514a99e6" />

- Tạo Frontend (index.html):
<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/bc6f6693-f853-4384-813f-58ab2d946582" />

<img width="1476" height="759" alt="image" src="https://github.com/user-attachments/assets/e319ead8-1bc2-4afa-8cb0-77f3e573ac9b" />

- Mở Web Frontend
  + Truy cập vào trình duyệt: http://localhost
<img width="1651" height="838" alt="image" src="https://github.com/user-attachments/assets/1bae6580-2bfe-48f1-a116-f388fe8bab9e" />

<img width="1763" height="818" alt="image" src="https://github.com/user-attachments/assets/7b3608b1-2b8a-4ca7-8647-e9dc2555e0db" />




























   










    




















