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
### 1. Cài đặt môi trường linux
- Cài đặt Ubuntu:
  + Mở CMD (chạy bằng quyền Admin) -> chạy lệnh `wsl --install`
<img width="1223" height="641" alt="image" src="https://github.com/user-attachments/assets/60101852-9ff7-4d5e-952f-57fb743fe1b1" />
- Dùng VirtualBox để cài Ubuntu:
  + Truy cập: https://www.virtualbox.org/wiki/Downloads và ở mục: VirtualBox Platform Packages chọn bản Windows hosts để cài đặt:
<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/4b868ec8-5e20-4fc2-a630-a16246d6e975" />
  + Tiếp tục truy cập vào: https://ubuntu.com/download/server để tải bản Ubuntu 24.04.3 LTS:
<img width="1919" height="867" alt="image" src="https://github.com/user-attachments/assets/8b8b1224-ffa7-4a99-85f1-f5d64331b216" />

<img width="1919" height="865" alt="image" src="https://github.com/user-attachments/assets/183386b1-5b90-4f68-8cc5-c76a9b816f71" />

- Mở VirtualBox để tạo máy ảo Ubuntu:
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/293ef8f1-17e4-43b2-984c-7c693a336601" />
  + Chọn New -> có thể đặt tên VM Name tuỳ chọn. VD: Ubuntu
  + Ở VM Forder có thể tuỳ chọn nơi để đặt máy ảo
  + OS: Linux
  + OS Version: Ubuntu (64-bit)
  -> Chọn Next
<img width="1892" height="1079" alt="image" src="https://github.com/user-attachments/assets/6a3936c7-9438-4e48-9740-b391741ba9bf" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/aeefe132-e712-409c-b08a-3140fc5b716d" />

<img width="1899" height="1075" alt="image" src="https://github.com/user-attachments/assets/3b5ef6bb-cfc4-46b6-90e9-338ed854d805" />

- Cài đặt Ubuntu:
  + Chuột phải vào máy ảo tên: Ubuntu -> chọn Settings -> Storage
  + Ở mục "Controller: IDE" -> chọn Choose a disk file
  + Chọn file .iso ubuntun đã tải về -> OK
<img width="1285" height="374" alt="image" src="https://github.com/user-attachments/assets/47e28ce8-1ccb-4dac-b24e-de42971d959d" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/28d004ca-0038-4748-ad1e-a7cea15875f1" />

- Tiếp tục chuột phải vào máy ảo tên: Ubuntu -> chọn Start -> Start with GUI:
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/022c67b1-7afc-4bb4-8f71-033bade0c682" />












