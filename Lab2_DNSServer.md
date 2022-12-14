# Dựng DNS Server
## 1, Máy cài DNS Server
### 1.1, Cài đặt
* Cài đặt gói BIND9 (dùng cấu hình dịch vụ DNS trên Linux):
![image](https://user-images.githubusercontent.com/88284121/207530030-a393d1b7-6336-4518-9cb8-1db79545f829.png)
### 1.2, Cấu hình
* Kiểm tra ip của máy:
![image](https://user-images.githubusercontent.com/88284121/207554915-6f48c51b-221b-4f59-91a1-e716c36f7917.png)
* Cấu hình những file sau:
  - `/etc/bind/named.conf.options`
  - `/etc/bind/named.conf.local` 
![image](https://user-images.githubusercontent.com/88284121/207555691-ae85dfdb-ed8e-4470-9c45-7bdd03363a51.png)
![image](https://user-images.githubusercontent.com/88284121/207556291-355a7079-3d9d-4f6d-b681-7a30f26d9e1b.png)
* Tiếp theo, tạo file cơ sở dữ liệu DNS:
  - `/etc/bind/db.toilamlab.com` copy từ file `/etc/bind/db.local`
  - `/etc/bind/db.103` copy từ file `/etc/bind/db.127`
![image](https://user-images.githubusercontent.com/88284121/207557158-ab203f32-4476-4bf3-87db-023d959c0173.png)
* Cấu hình cho 2 file cơ sở dữ liệu vừa tạo:
![image](https://user-images.githubusercontent.com/88284121/207557694-ffe2eb37-d56e-4a92-af28-9f6321b5b226.png)
![image](https://user-images.githubusercontent.com/88284121/207557960-de75e8f9-98c8-427d-bc8a-c714b6122b98.png)
* Sửa file `/etc/resolv.conf` giúp truy vấn để chuyển đổi các hostname đến địa chỉ IP và ngược lại:
![image](https://user-images.githubusercontent.com/88284121/207558578-cad68eba-8e27-4ee1-b6e0-8843bd9081c2.png)
* Khởi động lại dịch vụ BIND9:
![image](https://user-images.githubusercontent.com/88284121/207558827-4c5c021a-ec67-4dad-b645-8fcb378aa699.png)
* Kiểm tra lại `nslookup` của domain `toilamlab.com`:
![image](https://user-images.githubusercontent.com/88284121/207558972-3af678f3-20cd-48d4-9747-17c4ed32a796.png)


## 2, Máy Client
### 2.1, Trước khi trỏ về Server
![image](https://user-images.githubusercontent.com/88284121/207560735-c25c9bbf-f5cb-4adc-b5ef-f5aa44f1cf5a.png)
### 2.2, Sau khi trỏ về Server
* Cấu hình trỏ về:
![image](https://user-images.githubusercontent.com/88284121/207560858-a8f87b26-ca74-4796-aabc-a5a4dbbd0253.png)
![image](https://user-images.githubusercontent.com/88284121/207560996-0abfa4bb-bef4-40ec-952a-0a3198e52830.png)
* Kiểm tra lại `nslookup`:
![image](https://user-images.githubusercontent.com/88284121/207561154-8fa16920-c7ca-437f-9b55-91ebd071f11f.png)
* Ping cũng oke:
![image](https://user-images.githubusercontent.com/88284121/207561591-43897620-9af9-4ef2-94e5-e11d08c1b4b9.png)
