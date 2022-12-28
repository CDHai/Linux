# IPTABLES LABS
## NOTE:
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
* Ở đây mình sử dụng LAN `192.168.181.0/24` thay vì `172.16.69.0/24` như ở đề bài
* 2 Ubuntu Server Client và Server có IP lần lượt là:
  - **Client**: `192.168.181.138`
  - **Server**: `192.168.181.139`
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
* Nếu tổng hợp tất cả các rule ở trên mà chưa cần cấu hình ACCEPT SSH thì sau khi yêu cầu kết nối ssh vẫn có thể ssh thành công, tuy nhiên sau khi xóa hết các rules đi và thử ta có:
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
* Điều chỉnh bảng route của Client:
![image](https://user-images.githubusercontent.com/88284121/209757788-c93efc94-3f86-4852-8ffa-663f6785b5c3.png)
* Cấu hình RULE NAT:
```
iptables -A FORWARD -i ens37 -o ens33 -j ACCEPT
iptables -t nat -A POSTROUTING -o ens33 -s 10.10.10.0/24 -j MASQUERADE
```
* Ping oke ngay: *hình ảnh minh hoạ ping từ Client đến `172.16.69.11` của Server thành công thôi nhưng ảnh lỡ bị xóa mất hihi*

## 3, LAB 
### 3.1, Mô hình:
![image](https://user-images.githubusercontent.com/88284121/209758286-16320fda-aa94-498d-8568-bdc50de12c8a.png)
* Client, Server cài hệ điều hành Ubuntu Server 16.04.
* Cấu hình iptables tại Server.
* Trên Backend1, cài Web server (apache2) lắng nghê trên port 80.
* Trên Backend2, cài Web server (apache2) lắng nghê trên port 443.
### 3.2, Mục đích:
1. Mặc định, DROP INPUT.
2. Mặc định, ACCEPT OUTPUT.
3. Mặc định, DROP FORWARD.
4. ACCEPT Established Connection.
5. ACCEPT kết nối từ loopback.
6. FORWARD gói tin đến port 80 trên ens33 đến port tương tự trên Backend1.
   FORWARD gói tin đến port 443 trên ens33 đến port tương tự trên Backend2. 
   Nhưng DROP gói tin từ 172.16.69.2.
7. ACCEPT kết nối Ping với 5 lần mỗi phút từ mạng LAN.
8. ACCEPT kết nối SSH từ trong mạng LAN. Nhưng DROP gói tin từ 10.10.10.101.
9. ACCEPT Outgoing Packets thông qua Server từ mạng LAN (10.10.10.0/24) và nat địa chỉ nguồn của packet.
### 3.3, Thực hành:
#### Cài Apache2 trên Backend1 và Backend2 và cấu hình IP
![image](https://user-images.githubusercontent.com/88284121/209780966-fa8ac001-a19b-4b4c-96da-9ef46a10b1fd.png)
![image](https://user-images.githubusercontent.com/88284121/209780995-14438c8f-0153-4f2b-98df-61bdce8a0af8.png)
* Active SSL trên con Backend2:
![image](https://user-images.githubusercontent.com/88284121/209782167-5fb16834-6ccb-48b9-9d13-9cc0e8586595.png)
#### Kích hoạt các cấu hình cần thiết cho Server
![image](https://user-images.githubusercontent.com/88284121/209782624-c26bbb1c-7c12-41ec-aaf1-9636390b1bf0.png)
#### M1: Mặc định, DROP INPUT
![image](https://user-images.githubusercontent.com/88284121/209782756-9012abe8-4927-4645-acb7-c21aefec7f8b.png)
#### M2: Mặc định, ACCEPT OUTPUT
![image](https://user-images.githubusercontent.com/88284121/209080881-54dd1f56-daed-497d-b50f-6a023e1d9b33.png)
#### M3: Mặc định, DROP FORWARD
![image](https://user-images.githubusercontent.com/88284121/209080989-210c3417-f1ef-45ec-b7fd-c32f1fce9858.png)
#### M4: ACCEPT Establishes Connection
![image](https://user-images.githubusercontent.com/88284121/209783638-043b7ae0-eaed-46bb-bd76-658467c5453c.png)
#### M5: ACCEPT kết nối từ Loopback
![image](https://user-images.githubusercontent.com/88284121/209783901-96ad14b9-ced9-4c81-948b-dc35175dafca.png)
#### M6: FORWARD gói tin
![image](https://user-images.githubusercontent.com/88284121/209786866-3df0745a-87b7-4f00-b101-17e014d7471a.png)
* **Test**:
  - http://
![image](https://user-images.githubusercontent.com/88284121/209789011-b3522e33-e3f9-4e02-b368-16837bdf1dab.png)
  - https://
![image](https://user-images.githubusercontent.com/88284121/209792017-023cb50f-f81e-4ce2-b168-0935b106fbd7.png)
#### M7: ACCEPT gói tin 5 lần mỗi phút từ mạng LAN
![image](https://user-images.githubusercontent.com/88284121/209785106-44a69e0e-6a0a-41d2-9d7d-1a6c3e68fd1d.png)
#### M8: ACCEPT kết nối SSH từ trong mạng LAN. Nhưng DROP gói tin từ 10.10.10.101
![image](https://user-images.githubusercontent.com/88284121/209788794-f880faf6-bbfa-4b50-aa13-985847ff6042.png)
* Filter INPUT số 1 và số 5
#### M9: ACCEPT Outgoing gói tin thông qua Server từ mạng LAN (10.10.10.0/24) và NAT địa chỉ nguồn của gói tin.
* Cấu hình RULE NAT:
```
iptables -A FORWARD -i ens37 -o ens33 -j ACCEPT
iptables -t nat -A POSTROUTING -o ens33 -s 10.10.10.0/24 -j MASQUERADE
```
