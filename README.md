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
<img width="1471" height="750" alt="image" src="https://github.com/user-attachments/assets/6476cf52-51c4-48e3-b585-dc21bfcff2e6" />
  + Hiện như này là đã thành công

### 3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container
- Tạo thư mục:
  + Ở Ubuntu (WSL2) nhập:
    ```
    cd /mnt/d

    mkdir baitap3_laptrinhweb

    cd baitap3_laptrinhweb
    ```
<img width="664" height="97" alt="image" src="https://github.com/user-attachments/assets/db47e2d5-f225-4662-9301-445ac6cf1584" />

- Tạo 1 file docker-compose.yml
  + Nhập nano docker-compose.yml
<img width="1466" height="759" alt="image" src="https://github.com/user-attachments/assets/23d996e0-d6e4-4c49-820d-f364d9e4cd54" />

- Tạo file nginx.conf:
  + Nhập: /mnt/d/baitap3_laptrinhweb, gõ lệnh: nano nginx.conf
<img width="934" height="333" alt="image" src="https://github.com/user-attachments/assets/5a13a8ae-a137-4a4b-b9ea-10ff5359ddae" />


    




















