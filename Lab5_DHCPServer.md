# DỰNG DHCP SERVER
## 1, Tải DHCP Server
![image](https://user-images.githubusercontent.com/88284121/207497315-1c836628-27cc-4722-892f-6e763abb203b.png)
## 2, Xử lí file config của DHCP 
### 2.1, Mở file config
![image](https://user-images.githubusercontent.com/88284121/207497552-4f8d2ac6-65d0-43d6-a801-2c04e3192b8f.png)
### 2.2, Chỉnh sửa `default-lease-time` và `max-lease-time` nếu cần
![image](https://user-images.githubusercontent.com/88284121/207498291-f065d25b-4d3e-477b-bcbd-ba0c48464901.png)
### 2.3, Cấu hình dải IP cấp phát
![image](https://user-images.githubusercontent.com/88284121/207499790-76bd81b4-7d5b-4d2f-9534-a619d343bedc.png)
* Điều này sẽ dẫn đến các địa chỉ IP nằm trong khoảng từ 10.0.10.2 đến 10.0.10.254 được gán cho Clients. Thời gian kết nối mặc định được đặt thành 600 giây với giới hạn tối đa là 7200 giây. Client có thể yêu cầu thời gian cụ thể với thời gian kết nối tối đa là 7200 giây. Ngoài ra, máy chủ DHCP sẽ cung cấp cổng mặc định (bộ định tuyến) cũng như máy chủ DNS mặc định.
### 2.4, Cấu hình IP tĩnh cho 1 số thiết bị cần IP cố định
* Dựa vào địa chỉ MAC
* Ví dụ MAC ở máy Client là: `08:00:07:26:c0:a5` 
* Thì ta cấu hình:
![image](https://user-images.githubusercontent.com/88284121/207500505-8080bbd5-d5d5-451e-a3d6-cb3192988521.png)
### 2.5, Lưu file
## 3, Restart dịch vụ DHCP
![image](https://user-images.githubusercontent.com/88284121/207501043-72d6718c-c89e-48ae-bf27-eac17e404849.png)
