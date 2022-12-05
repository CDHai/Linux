# Disk - Ổ đĩa - Partirtion - Filesystem 
## 1, Tạo máy ảo
![image](https://user-images.githubusercontent.com/88284121/204226522-f296b444-8a17-4023-a352-f5786e38c1af.png)
## 2, Kiểm tra ổ cứng
![image](https://user-images.githubusercontent.com/88284121/204226621-ae8ec191-9328-48f7-b7b8-8bc26a32c2cb.png)
## 3, Gán thêm 1 ổ 60GB
![image](https://user-images.githubusercontent.com/88284121/204227034-4d80b2a7-c46c-401f-9d3b-67404ca3bec3.png)
![image](https://user-images.githubusercontent.com/88284121/204227750-0764bb60-b26f-4634-af9e-9dcb25881a64.png)
* Giờ đã có thêm 1 ổ sdb với dung lượng 60GB
## 4, Thực hiện chia Partition
### 4.1, Sử dụng lệnh `fdisk`
![image](https://user-images.githubusercontent.com/88284121/204228742-73c0c0ca-e9fe-49f9-b8ab-0b4fcd218fb2.png)
### 4.2, Sử dụng toàn bộ ổ cứng vừa thêm làm Extended Partition
![image](https://user-images.githubusercontent.com/88284121/204230672-a59dafd2-4e93-46b4-a0e3-163e22cba7ab.png)
### 4.3, Tạo các Logical Partition dựa vào Extended Partition ở trên
* ![image](https://user-images.githubusercontent.com/88284121/204230863-eb161c63-d42d-4db2-a205-5c8538ca9de0.png)
* ![image](https://user-images.githubusercontent.com/88284121/204230938-1e302909-5c1c-4c1d-a286-37bca19bc928.png)
* ![image](https://user-images.githubusercontent.com/88284121/204231075-a684450c-a297-4e6e-b00d-e1d52eb30b41.png)
* Sử dụng command: `w` để lưu những thay đổi trên ổ cứng
* ![image](https://user-images.githubusercontent.com/88284121/204232651-9f6e2ff9-edb0-4167-ad03-53c99fcf1bca.png)
### 4.4, Tạo FileSystem và Mount
#### 4.4.1, Tạo Mount Point
* Trước hết, để thực hiện `mount` thì cần phải có Mount Point
* Thêm Mount Point:
* ![image](https://user-images.githubusercontent.com/88284121/204236278-7ec34635-dab9-45b1-acc9-1759dc1cdb13.png)
#### 4.4.2, Tạo FileSystem và Mount
![image](https://user-images.githubusercontent.com/88284121/204237291-929184e8-b528-4ed5-90f1-f001ef0dd5c9.png)
![image](https://user-images.githubusercontent.com/88284121/204237532-2e64fe8b-6edd-48d9-a55f-de5afcff00d3.png)
## 5, Kiểm tra lại cấu hình
![image](https://user-images.githubusercontent.com/88284121/204237685-8756ab3b-7398-47e7-848b-bef2faadab9c.png)
## 6, Tự động `mount` lại khi REBOOT
### 6.1, Thực hiện cấu hình
* Phần mount tự động đượng cấu hình ở file /etc/fstab. Nó chứa nội dung tùy chọn cho mỗi phân vùng và những setting cho việc mount khi khởi động.
* ![image](https://user-images.githubusercontent.com/88284121/204238523-1a60925a-9b54-4241-85cb-868e5f9c0916.png)
* Chỉnh sửa lại cấu hình:
* ![image](https://user-images.githubusercontent.com/88284121/204245000-1dcf6605-6a2a-4dc2-a246-3b73eac0a736.png)
### 6.2, Kiểm tra lại kết quả
* Reboot trước khi lưu cấu hình file fstab:
![image](https://user-images.githubusercontent.com/88284121/204232651-9f6e2ff9-edb0-4167-ad03-53c99fcf1bca.png)
* Sau khi lưu cấu hình file `fstab` và Reboot:
![image](https://user-images.githubusercontent.com/88284121/204248308-076f6035-f9f0-4c66-8c8a-78d0f0b7bc57.png)

