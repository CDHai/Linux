# IPTABLES LABS
## NOTE:
* Ở đây mình sử dụng LAN `192.168.181.0/24` thay vì `172.16.69.0/24` như ở đề bài
* 2 Ubuntu Server Client và Server có IP lần lượt là:
  - **Client**: `192.168.181.138`
  - **Server**: `192.168.181.139`
## 1, LAB 1
### 1.1, Mô hình:
![image](https://user-images.githubusercontent.com/88284121/209078380-b579e10b-d8e8-4f44-b7a3-00febaf18a33.png)
* Client, Server cài hệ điều hành Ubuntu Server.
* Cấu hình iptables tại Server.
### 1.2, Mục đích:
1. Mặc định, DROP INPUT.
2. Mặc định, ACCEPT OUTPUT.
3. Mặc định, DROP FORWARD.
4. ACCEPT Established Connection.
5. ACCEPT kết nối từ loopback.
6. ACCEPT kết nối Ping với 5 lần mỗi phút từ mạng LAN.
7. ACCEPT kết nối SSH từ trong mạng LAN. 
### 1.3, Thực hành:
#### Kiểm tra các filter hiện đang có
![image](https://user-images.githubusercontent.com/88284121/209080214-fa00efff-7ece-4ed4-9eaf-fb2c8a3257c8.png)
#### M1: Mặc định, DROP INPUT
![image](https://user-images.githubusercontent.com/88284121/209080687-d22e2c16-9e37-4e7d-b58f-19ba2d338e7e.png)
* Ping thử từ **Client** đến **Server**: Đã xịt do gói tin đi vào **Server** bị DROP.
![image](https://user-images.githubusercontent.com/88284121/209084223-ac0e46a7-db46-49de-a3c5-59eb202cfbac.png)
#### M2: Mặc định, ACCEPT OUTPUT
![image](https://user-images.githubusercontent.com/88284121/209080881-54dd1f56-daed-497d-b50f-6a023e1d9b33.png)
#### M3: Mặc định, DROP FORWARD
![image](https://user-images.githubusercontent.com/88284121/209080989-210c3417-f1ef-45ec-b7fd-c32f1fce9858.png)
#### M4: ACCEPT Establishes Connection
![image](https://user-images.githubusercontent.com/88284121/209084950-a582decf-d3ea-422b-bd2d-895c6c1fe909.png)
#### M5: ACCEPT kết nối từ Loopback
* Ping thử về `localhost` khi vẫn đang mặc định INPUT là DROP (Chưa cấu hình ACCEPT kết nối từ Loopback): xịt.
![image](https://user-images.githubusercontent.com/88284121/209087112-ca787ff3-6168-4163-85a5-b2e4514c1147.png)
* Sau khi cấu hình: Ping ngon nghẻ.
![image](https://user-images.githubusercontent.com/88284121/209087290-23ddc18b-299d-40f8-8b30-2041167bf8c5.png)
#### M6: ACCEPT kết nối Ping với 5 lần mỗi phút từ mạng LAN
* **Server**:
![image](https://user-images.githubusercontent.com/88284121/209104857-3d781217-1a7c-47ee-8508-a61b5e625310.png)
* **Client**: 
![image](https://user-images.githubusercontent.com/88284121/209099490-8df1144c-3111-442c-bc09-42881984b705.png)
* Nhìn vào `icmp_seq` có thể thấy là ping không đến liên tục
#### M7: ACCEPT kết nối  từ SSH trong mạng LAN
* Nếu tổng hợp tất cả các rule ở trên mà chưa cần cấu hình ACCEP SSH thì sau khi yêu cầu kết nối ssh vẫn có thể ssh thành công, tuy nhiên sau khi xóa hết các rules đi và thử ta có:
![image](https://user-images.githubusercontent.com/88284121/209098458-27aeab37-0af4-4909-a4f9-885141b0f6dc.png)
* Sau khi cấu hình rule ACCEPT SSH:
![image](https://user-images.githubusercontent.com/88284121/209104335-3ca8bcc1-c116-4395-883a-d176b2010c4d.png)
* SSH ngon nghẻ:
![image](https://user-images.githubusercontent.com/88284121/209098777-135b14b0-56d3-41b9-889e-a46f3312ea16.png)

## 2, LAB 2
### 2.1, Mô hình:
![image](https://user-images.githubusercontent.com/88284121/209100866-194efaa3-b5d8-4ed1-adb1-799ae32bfce5.png)
* Client, Server cài hệ điều hành Ubuntu Server.
* Cấu hình iptables tại Server.
### 2.2, Mục đích:
1. Mặc định, DROP INPUT.
2. Mặc định, ACCEPT OUTPUT.
3. Mặc định, DROP FORWARD.
4. ACCEPT Established Connection.
5. ACCEPT kết nối từ loopback.
6. ACCEPT kết nối Ping với 5 lần mỗi phút từ mạng LAN.
7. ACCEPT kết nối SSH từ trong mạng LAN.
8. ACCEPT Outgoing gói tin thông qua Server từ mạng LAN (10.10.10.0/24) và nat địa chỉ nguồn của gói tin.
### 2.3, Thực hành:
#### Kiểm tra các filter hiện đang có
![image](https://user-images.githubusercontent.com/88284121/209080214-fa00efff-7ece-4ed4-9eaf-fb2c8a3257c8.png)
#### M1: Mặc định, DROP INPUT
![image](https://user-images.githubusercontent.com/88284121/209080687-d22e2c16-9e37-4e7d-b58f-19ba2d338e7e.png)
* Ping thử từ **Client** đến **Server**: Đã xịt do gói tin đi vào **Server** bị DROP.
![image](https://user-images.githubusercontent.com/88284121/209084223-ac0e46a7-db46-49de-a3c5-59eb202cfbac.png)
#### M2: Mặc định, ACCEPT OUTPUT
![image](https://user-images.githubusercontent.com/88284121/209080881-54dd1f56-daed-497d-b50f-6a023e1d9b33.png)
#### M3: Mặc định, DROP FORWARD
![image](https://user-images.githubusercontent.com/88284121/209080989-210c3417-f1ef-45ec-b7fd-c32f1fce9858.png)
#### M4: ACCEPT Establishes Connection
![image](https://user-images.githubusercontent.com/88284121/209084950-a582decf-d3ea-422b-bd2d-895c6c1fe909.png)
#### M5: ACCEPT kết nối từ Loopback
* Ping thử về `localhost` khi vẫn đang mặc định INPUT là DROP (Chưa cấu hình ACCEPT kết nối từ Loopback): xịt.
![image](https://user-images.githubusercontent.com/88284121/209087112-ca787ff3-6168-4163-85a5-b2e4514c1147.png)
* Sau khi cấu hình: Ping ngon nghẻ.
![image](https://user-images.githubusercontent.com/88284121/209087290-23ddc18b-299d-40f8-8b30-2041167bf8c5.png)
#### M6: ACCEPT kết nối Ping với 5 lần mỗi phút từ mạng LAN
* **Server**:
![image](https://user-images.githubusercontent.com/88284121/209104857-3d781217-1a7c-47ee-8508-a61b5e625310.png)
* **Client**: 
![image](https://user-images.githubusercontent.com/88284121/209099490-8df1144c-3111-442c-bc09-42881984b705.png)
* Nhìn vào `icmp_seq` có thể thấy là ping không đến liên tục
#### M7: ACCEPT kết nối  từ SSH trong mạng LAN
* Nếu tổng hợp tất cả các rule ở trên mà chưa cần cấu hình ACCEP SSH thì sau khi yêu cầu kết nối ssh vẫn có thể ssh thành công, tuy nhiên sau khi xóa hết các rules đi và thử ta có:
![image](https://user-images.githubusercontent.com/88284121/209098458-27aeab37-0af4-4909-a4f9-885141b0f6dc.png)
* Sau khi cấu hình rule ACCEPT SSH:
![image](https://user-images.githubusercontent.com/88284121/209104335-3ca8bcc1-c116-4395-883a-d176b2010c4d.png)
* SSH ngon nghẻ:
![image](https://user-images.githubusercontent.com/88284121/209098777-135b14b0-56d3-41b9-889e-a46f3312ea16.png)
#### M8: ACCEPT Outgoing gói tin thông qua Server từ mạng LAN (10.10.10.0/24) và NAT địa chỉ nguồn của gói tin.
