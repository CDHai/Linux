# File System
## 1, File System là gì ?
* **File System** (Hệ thống tập tin) là các phương pháp và cấu trúc dữ liệu mà một hệ điều hành sử dụng để theo dõi các tập tin trên ổ đĩa hoặc phân vùng. Hay nói các khác là cách tổ chức và quản lí dữ liệu được đọc và lưu trên thiết bị. File system cho phép người dùng truy cập nhanh chóng và an toàn khi vào các tệp tin thư mục khi cần thiết.

![image](https://user-images.githubusercontent.com/88284121/197670970-9d6be3c7-f84c-4756-afb2-0c8e67d232cb.png)

* Những loại File System được Linux hỗ trợ: 
  - Filesystem cơ bản: EXT2, EXT3, EXT4, XFS, Btrfs, JFS, NTFS,...
  - Filesystem dành cho dạng lưu trữ Flash (thẻ nhớ,…): ubifs, JFFS2, YAFFS,...
  - Filesystem dành cho hệ cơ sở dữ liệu.
  - Filesystem mục đích đặc biệt: procfs, sysfs, tmpfs, squashfs, debugfs,...

Để tra cứu cụ thể cách hoạt động của từng file: https://manpages.ubuntu.com/manpages/kinetic/en/man5/filesystems.5.html
### Phân vùng và File System
- Một phân vùng là một vùng chứa trong đó có một filesystem được lưu trữ , trong một số trường hợp thì filesystem có thể mở rộng hơn một phân vùng nếu filesystem sử dụng các liên kết.
- File system là một phương pháp lưu trữ hoặc tìm kiếm các tập tin trên một đĩa cứng ( trong một phân vùng ).
- So sánh giữa filesystem trên hệ điều hành Windows và hệ điều hành Linux:

![image](https://user-images.githubusercontent.com/88284121/197672366-954edf6c-50f7-4ee4-bc20-9e26556fdb3a.png)
### Tiêu chuẩn cấp bậc của hệ thống tập tin - Filesystem Hierarchy Standard (FHS)

![image](https://user-images.githubusercontent.com/88284121/197672904-68b1f526-7680-4e41-a193-174408797a34.png)

* Các thư mục được mô tả như sau:
* ![image](https://user-images.githubusercontent.com/88284121/197673371-a7ce8d95-ad2c-40ec-aa66-9f71d72f3f78.png)

## 2, `mount` và `umount`
Không giống như trong Windows, để có thể truy cập dữ liệu được lưu trữ trong USB, đĩa CD/DVD, file ISO, phân vùng ổ cứng, các tài nguyên được chia sẻ qua mạng (gọi chung là thiết bị)… trong Linux thì trước hết các thiết bị này các được gắn kết (mount) vào 1 thư mục trống (gọi là mount point) đã tồn tại sẵn trong cây thư mục. Và khi muốn tháo gỡ thiết bị đang hoạt động khỏi hệ thống thì bạn phải ngắt kết nối (unmount) giữa thiết bị với mount point trước.
* Linux có khả năng tự nhận biết được các filesystem đang được kết nối với hệ thống. Tuy nhiên, để có thể sử dụng được các filesystem này, bắt buộc bạn phải làm một công việc gọi là **mount**.
  - Khi mount, bạn cần chỉ định thiết bị cần mount và vị trí của mount point.
  - Ví dụ để mount ổ CD bạn sử dụng lệnh: `$ mount /dev/cdrom /media/cdrom`
    - Trong đó, /dev/cdrom là đường dẫn tới ổ CD-ROM cần mount và /media/cdrom là mount point.
    - Bây giờ, khi bạn truy cập tới thư mục /media/cdrom thì bạn mới thực sự truy cập được nội dung trong đĩa CD.
* Bạn sử dụng lệnh **umount** (chú ý: không phải unmount) để ngắt kết nối thiết bị khỏi hệ thống.
  - Ví dụ để gỡ bỏ ổ CD-ROM bạn gõ lệnh: `$ umount /mnt/cdrom` hoặc `$ unmount /dev/cdrom`
  - Nếu bạn rút trực tiếp thiết bị khỏi máy tính mà không unmount trước thì **có thể dữ liệu trên thiết bị sẽ bị lỗi hoặc tệ hơn làm hỏng luôn thiết bị!**

## 3, Partition Disks
* **Partition** là một phân vùng nhỏ (phân vùng logic) được chia ra từ 1 ổ cứng vật lí.
* Một ổ cứng có thể có 1 hoặc nhiều partion. Partion là cách phân chia và quản lí ổ cứng một cách đơn giản và hiệu quả (chẳng hạn như phân ra 1 vùng quan trọng để chứa dữ liệu của hệ điều hành và 1 phân vùng để chứa phim, nhạc).
* Hiện có 3 loại partition chính là: **primary**, **extended** và **logical**:
  - **primary partition**: Đây là những phân vùng có thể được dùng để boot HĐH.
  - **logical partition**: Đây là một phân vùng nhỏ nằm trong extended partition, thường dùng để chứa dữ liệu.
  - **extended partition**: Là vùng dữ liệu còn lại khi ta phân chia ra các primary partition, extended partition chứa các logical partition trong đó. Mỗi 1 ổ đĩa chỉ có thể chưa được 1 extended partition.

![image](https://user-images.githubusercontent.com/88284121/197706515-43e97cd1-b255-4c82-85bf-28cd7674fd2e.png)
### 3.1, Tạo/Quản lý Partition đĩa bằng `fdisk`. 

- kiểm tra ổ đĩa cứng : ````lsblk````
 
  <img src="https://github.com/tulha161/linux/blob/main/images/10.2.png">
  
 - ở đây mình mới thêm một ổ "sda" 2GB vào VM để demo, ở nay do thêm sau khi tạo VM nên ta cần phải tạo các phân vùng cho ổ.
 - nếu ổ không tự nhân, có thể rescan lại để nhận ổ mới add : 
 `echo "- - -" > /sys/class/scsi_host/host0/scan` ( thay host0-2 để scan lần lượt)
 - `fdisk -l` - show các ổ đĩa cứng
 
 <img src="https://github.com/tulha161/linux/blob/main/images/10.3.png">
 
 - `fdisk /dev/sda` - tool chia ổ -> partition ( sửa lại sda -> tên ổ mà bạn muốn thao tác ), tool này sẽ chạy lần lượt như một dạng script có tương tác với người dùng, nếu mới sử dụng hãy `commann =m ` để đọc manual trước.
 - 2 loại phân vùng ( max =4 ) : 
	- primary  : phân vùng chính, có thể chứa phần boot
	- extended : quản lý phần còn lại, chia cho các logical partition
 - Vì vậy, để tạo phân vùng boot để OS thì tạo phân vùng primary, còn nếu muốn tạo phân vùng chứa dữ liệu thì tạo phân vùng extended rồi chia cho các ra các phân vùng logical nhỏ hơn. Ở đây mình sẽ tạo cả 2 loại trên.
 - Step-by-step thì như sau
 	- B1 : tạo phần vùng primary trước `( cmd = n )`, chọn loại primary, đánh số nó theo số 1 và gán cho nó 1G dung lượng ổ.
 	- B2 : tạo phân vùng extended `( cmd =n )`, chọn loại extended, đánh số cho nó theo số 2 và gán cho nó phần dung lượng còn lại của ổ ( cứ để default ) 
 	- B3 : tạo phần vùng logical `(cmd =n)` phân vùng này nằm dưới quản lý của phân vùng extended `( cmd = l )`, gán cho nó phần dung lượng còn lại và đánh số phân vùng ( phân vùng logical thì bắt đầu từ số 5 )
 	- B4 : verify và write xuống ổ `( cmd = w )`
 - Sau đó, có thể kiểm tra lại bằng `lsblk` or `fdisk -l` để coi kết quả : 
 
 <img src="https://github.com/tulha161/linux/blob/main/images/10.5.png">
 <img src="https://github.com/tulha161/linux/blob/main/images/10.6.png">

### 3.2, Lệnh `df` và `du` kiểm tra dung lượng Disk
#### 3.2.1, `df`
* `df`: **Disk Filesystem** : được dùng để lấy toàn bộ thông tin về lượng ổ cứng khả dụng và lượng ổ cứng đã sử dụng của các FS.
* Các option thường dùng:
  - `df -h`: hiển thị theo fomat dung lượng K,M,G;
  - `df -i`: hiển thị theo fomat inodes.
#### 3.2.2, `du`
* `du`: **Disk Usage** : báo cáo dung lượng ổ đĩa được sử dụng bởi các thư mục và File. Đây là công cụ chính để phân tích không gian ổ đĩa trong dòng lệnh.
* Các option thường dùng:
  - `du -h`: hiển thị theo fomat dung lượng K,M,G;
  - `df -shc`: hiển thị dung lượng.
## 4, Dùng lệnh `fsck` để kiểm tra và sửa lỗi Filesystem
* Hệ thống file chịu trách nhiệm về cách dữ liệu của người dùng được lưu trữ và tổ chức. Nếu hệ thống file bị hỏng và một số phần nhất định không hoạt động thì chúng sẽ dẫn đến sự không nhất quán trong hệ thống file. Vấn đề này có thể được giải quyết bằng cách sử dụng lệnh `fsck` - ( **file system consistency check** ). 
* **Fsck này hoạt động tại thời điểm BOOT**.
* Cú pháp: `fsck [-option]`
* ![image](https://user-images.githubusercontent.com/88284121/197677440-2f0e65d3-04a8-43f2-b0c8-71639aefe86b.png)
* Ngoài ra, tính năng fsck này còn được tích hợp trong recovery mode của linux, trường hợp này ta áp dụng khi cần check `FS` của của `/`.
* **Sửa** Filesystem:
  - Cú pháp: `# fsck -y /dev/sdb`
## 5, Dùng lệnh `mkfs` để tạo Filesystem (Makes File Systems)
* `mkfs` - **Makes File Systems*
* Để xem các loại FS mà mkfs có thể tạo, ta dùng cú pháp: `mkfs [tab]x2`
  
  ![image](https://user-images.githubusercontent.com/88284121/197709317-18c06752-e697-4c0c-ac14-40420fc1daae.png)
* Một số option thường dùng:
  - `-t`: Chỉ định loại FS (mặc định là ext2).
  - `-c`: Check bad block trước khi tạo file.

![image](https://user-images.githubusercontent.com/88284121/197710688-676f84b7-382e-4c82-ad24-0994973606a2.png)

* Các thuộc tính quan trọng:
  - **inode** : thuộc meta - phần ilist, chứa thông tin liên quan thuộc tính. Là 1 con số, đơn vị đo cho phần meta.
  - **superblock** : phần các vị trí backup của meta.
