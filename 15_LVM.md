# LVM
## 1, LVM là gì?
* **LVM** - *Logical Volume Manager* - là kỹ thuật quản lý việc thay đổi kích thước lưu trữ của ổ cứng. Là một phương pháp ấn định không gian ổ đĩa thành những logical volumn khiến cho việc thay đổi kích thước phân vùng trở nên dễ dàng.
* Một số khái niệm liên quan:
  - Physical volume: là một đĩa cứng vật lý hoặc là Partition.
  - Volume group: là một nhóm các physical volume ( ổ đĩa ảo ).
  - Logical volume: là các phân vùng ảo của ổ đĩa ảo.
## 2, Những thành phần trong LVM
* **HDD**: Là một thiết bị lưu trữ máy tính. Nó là loại bộ nhớ không thay đổi và không bị mất dữ liệu kia khi ta ngừng cung cấp nguồn điện cho chúng.
* **Partition**: là các phân vùng của ổ cứng. Mỗi một ổ cứng có 4 partition. Trong đó bao gồm 2 loại là primary partition và extended partition.
### Cách thức hoạt động của các tầng trong LVM
```
1. Tầng đầu tiên: Hard drives là các tầng disk ban đầu khi chưa chia vùng
2. Partition: Sau đó ta chia các disk ra thành các phân vùng nhỏ hơn
3. Physical Volume: Từ 1 Partition ta sẽ tạo được 1 Physical
4. Group Volume: Ta sẽ ghép các Physical Volume thành 1 Group Volume
5. Logical Volume: Ta có thể sẽ tạo ra được Logical Volume.
```
* Mô hình:
* ![image](https://user-images.githubusercontent.com/88284121/198233636-6fb898a1-8023-4a7c-b30a-9eeeb397c7fa.png)
## 3, Ưu nhược điểm của LVM
### 3.1, Ưu điểm
* Không để hệ thông bị gián đoạn.
* Không làm hỏng dịch vụ.
* Có thể kế hợp swap.
* Có thể tạo ra các vùng dung lượng lớn nhỏ tuỳ ý.
### 3.2, Nhược điểm
* Các bước thiết lập phức tạp và khó khăn hơn.
* Càng gắn nhiều đĩa cứng và thiết lập càng nhiều LVM thì hệ thống khởi động càng lâu.
* Khả năng mất dữ liệu cao khi một trong số các đĩa cứng bị hỏng.
* Windows không thể nhận ra vùng dữ liệu của LVM. Nếu Dual-boot ,Windows sẽ không thể truy cập dữ liệu trong LVM.
## 4, Cấu hình LVM
- Demo được thực hiện trên CentOS7, đã được cài lvm
- Cấu hình demo : 
 	- PV : 2 ổ /dev/sdc và /dev/sdd ( mỗi ổ 1GB)
 	- VG : gom 2 ổ này thành 1 VG, đặt tên là DemoVG ( tổng dung lượng = 2GB )
 	- LV : từ VG chia thành 2 LV khác nhau dung lượng 1.5 GB và 200 MB 
### TẠO và MOUNT 
 - Đầu tiên, hãy add thêm ổ cứng vật lý vào trong VM của bạn, ở đây mình đã thêm 2 ổ như sau : 
 
 <img src="https://github.com/tulha161/linux/blob/main/images/12.2.png">
 
 - Tạo PV cho các ổ vật lý : `pvcreate [dev]`
 - kiểm tra các PV trên hệ thống : `pvs` or `pvdisplay`
  
  <img src="https://github.com/tulha161/linux/blob/main/images/12.3.png">
 
 - Tạo VG gồm 2 PV đã tạo ở trên : `vgcreate [nameVG] [dev]` 
 - kiểm tra VG đã tạo : `vgs` or `vgdisplay`
 
  <img src="https://github.com/tulha161/linux/blob/main/images/12.4.png">
 
 - Tạo LV : `lvcreate -L [dung lượng cấp] -n [nameLV] [nameVG]`
 - Câu lệnh thực tế : `lvcreate -L 1.5G -n lv1 DemoVG` và  `lvcreate -L 200M -n lv2 DemoVG`
 - Kiểm tra LV : `lvs` or `lvdisplay`
 
  <img src="https://github.com/tulha161/linux/blob/main/images/12.5.png">
 
 - Tạo FS cho các LV : `mkfs -t ext4 /dev/DemoVG/lv1` và `mkfs -t ext2 /dev/DemoVG/lv2`
 - tạo thư mục và mount các lv vào hệ thống 
 	`mkdir /demo1`
 	`mount /dev/DemoVG/demo1`
 	`mkdir /demo2`
 	`mount /dev/DemoVG/demo2`
 - Do ở đây mình chỉ demo nên bỏ qua bước mount cố định, giờ cùng kiểm tra kết quả bằng `lsblk`
 
  <img src="https://github.com/tulha161/linux/blob/main/images/12.6.png">
 
### Thay đổi dung lượng LV
 - Điểm quan tọng ở phương thức chia ổ này là khả năng tăng/giảm dung lượng rất flexible mà không ảnh hưởng đến dữ liệu bên trong.
 - Cú pháp : 
 	- Thay đổi dung lượng lv :
 	`lvextend -L +[Dung lượng cấp thêm] [dev]` 
 	`lvreduce -L -[Dung lượng giảm đi] [dev`
 	- Thay đổi FS cho nó : `resize2fs [dev]`
 - Demo thay đổi -400M ở lv1 và +500M ở lv2 : 
 
  <img src="https://github.com/tulha161/linux/blob/main/images/12.7.png">
 
### Thay đổi dung lượng VG
- Khi muốn tăng/giảm dung lượng của VG thì ta sẽ tăng/giảm các PV được gán cho nó
- Cú pháp : 
	- Tăng : `vgextend [dev VG] [dev PV]`
	- Giảm : `vgreduce [dev VG] [dev PV]`
- Ví dụ, muốn gán cho DemoVG thêm parition /dev/sde1 và bỏ ổ /dev/sdd ta làm như sau : 
 	- `vgextend /dev/DemoVG /dev/sde1`
 	- `vgreduce /dev/DemoVG /dev/sdd`
 - Đổi tên VG : `vgrename [namecũ] [namemới]`
 
### Thao tác xóa 

- Umount thiết bị
- Xóa LV : `lvremove [dev]`
- Xóa hết các LV rồi hẵng xóa VG nhé
- Xóa VG : `vgremove [dev]`
- Xóa PV : `pvremove [dev]`

- kiểm tra lại : `lvmdiskscan`
