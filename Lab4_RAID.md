# RAID
* Sử dụng `mdadm` 
## 1, Thêm 2 ổ cứng cùng dung lượng để chuẩn bị
![image](https://user-images.githubusercontent.com/88284121/204695558-3601a843-8887-48a2-8a13-95494d839d0e.png)
* 2 ổ mới là sdb và sdc có cùng dung lượng.
## 2, Kiểm tra xem RAID đã được sử dụng trên bất kì ổ nào hay chưa?
![image](https://user-images.githubusercontent.com/88284121/204696015-5277a3fb-3a83-4de0-b13b-6d7b2801abee.png)
## 3, Cấu hình
### 3,1. Sử dụng `fdisk` để tạo phân vùng cho 2 ổ
* Trước hết làm với ổ `sdc`:
![image](https://user-images.githubusercontent.com/88284121/204697060-11c294dd-eacb-415f-8bab-e3b958d1931c.png)
  - Ấn `n` để tạo partition mới:
![image](https://user-images.githubusercontent.com/88284121/204697170-e00d665d-cb66-4a66-8c4d-eac4c5cd59f8.png)
  - Chọn primary và cấu hình dung lượng:
![image](https://user-images.githubusercontent.com/88284121/204697307-3a3cd152-0861-4e4b-b764-cc4d82bdedde.png)
  - Chọn `p` để xem các partition đã được tạo:
![image](https://user-images.githubusercontent.com/88284121/204697496-2387690c-71c9-4d56-aaca-609f952ad547.png)
  - Chọn `l` để liệt kê các loại Type có sẵn:
![image](https://user-images.githubusercontent.com/88284121/204697692-73dc51cf-fadb-4a65-8a51-1fc2787733b0.png)
  - Chọn `t` để chọn partition, ở đây chỉ có 1 partition vừa tạo nên nó auto chọn:
![image](https://user-images.githubusercontent.com/88284121/204697862-19b2b8f4-9a8a-4a07-8386-6af1873995d4.png)
  - Chọn `fd` để chọn Type: Linux raid auto
![image](https://user-images.githubusercontent.com/88284121/204697949-e7403ca8-5cb3-4ea8-9d29-a75d2de7f378.png)
  - Chọn `p` lại để kiểm tra kết quả
![image](https://user-images.githubusercontent.com/88284121/204698034-7ed6edaf-7e14-4d91-a606-3cbc7a525dc1.png)
* Làm tương tự vơi ổ: `sdb`:
![image](https://user-images.githubusercontent.com/88284121/204699107-207c25d6-9b4f-4203-bd90-39a49d411154.png)
### 3.2, Sử dụng `mdadm` tạo RAID
#### 3.2.1, Tạo `RAID0`
![image](https://user-images.githubusercontent.com/88284121/204700660-f0e1ed83-5e8f-46be-a28a-02d8555d67a4.png)
```
-C : mode Create
-l : loại raid 
-n : chỉ định số lượng và device tham gia Raid
```
* Kiểm tra lại thông tin RAID0 vừa tạo
![image](https://user-images.githubusercontent.com/88284121/204700876-acaf3be1-3866-4be0-a32c-ea2a3b03f4fc.png)
* Tạo FileSystem cho RAID
![image](https://user-images.githubusercontent.com/88284121/204701296-d1ecf4ad-befd-445e-8802-99f2c4086a14.png)
* Tạo thư mục raid0 và mount vào 
![image](https://user-images.githubusercontent.com/88284121/204701563-ea5365a0-936b-48c7-b252-b9f6f8c2aa6b.png)
#### 3.2.2, Tạo `RAID1`
* Làm tương tự đối với `RAID0`
# 4, Sử dụng `Sysbench` để so sánh tốc độ Disk
# 5, Giả lập trường hợp chết 1 Disk
* Tạo 1 file `raid.txt` dùng để test dữ liệu sau khi nhổ Disk ra.
![image](https://user-images.githubusercontent.com/88284121/204711317-f5160279-ab4b-4499-bd49-f5ecc9f11e4c.png)
## 5.1, RAID0
* Đây là lượng dữ liệu đã được sử dụng sau khi thêm file `raid.txt`
![image](https://user-images.githubusercontent.com/88284121/205215281-d694c5a5-674a-4617-a0a7-18ab1dd8eb02.png)
* Sau khi nhổ 1 disk ra
![image](https://user-images.githubusercontent.com/88284121/204716601-2e92ef7f-1ee3-473e-8db3-46b73cc142f0.png)
* Kết quả sau khi kiểm tra lại RAID vừa tạo:
![image](https://user-images.githubusercontent.com/88284121/205216426-88b0f858-6a62-40ea-9492-a50895687956.png)
* Sau khi vào lại file `/raid0/` để kiểm tra file `raid.txt` vừa tạo thì không còn thấy nữa:
![image](https://user-images.githubusercontent.com/88284121/204717128-36d4a4d8-1eeb-4577-a90f-399aae18f246.png)
* Vì vậy, RAID0 tính bảo mật không cao.
## 5.2, RAID1
* Thông tin của RAID ban đầu:
![image](https://user-images.githubusercontent.com/88284121/205221274-51372eaa-3060-4af4-bf22-9140706284a9.png)
* Đây là lượng dữ liệu đã được sử dụng sau khi thêm file `raid.txt`
![image](https://user-images.githubusercontent.com/88284121/205204794-4290f8e6-bfbf-457a-a8ab-0d5e45269373.png)
* Có thể thấy dung lượng sử dụng của RAID1 (/dev/md127) chỉ là 9.8GB (tương đương với 1 disk tham gia) so với 20GB của RAID0 là cả 2 disk cùng tham gia.
* Sau khi nhổ 1 disk ra
![image](https://user-images.githubusercontent.com/88284121/205542964-b5656924-7ab4-4417-aae0-cb70f5667876.png)
* Kết quả sau khi kiểm tra lại RAID vừa tạo:
![image](https://user-images.githubusercontent.com/88284121/205543034-74236a33-40c5-4895-b681-ccdc9957e2e6.png)
* Sau khi vào lại file `/raid0/` để kiểm tra file `raid.txt` vừa tạo thì **vẫn còn nguyên**:
![image](https://user-images.githubusercontent.com/88284121/205543100-8464a7ed-c2b4-44e1-b0fa-10cf4ed688d5.png)
