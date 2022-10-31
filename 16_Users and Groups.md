# Users and Groups
## 1, Users and Groups là gì?
- **User** là một thuật ngữ chuyên dụng được sử dụng trong ngành công nghệ thông tin. User được dùng để thể hiện tài khoản của người dùng trong máy tính. User giúp bạn bảo mật thông tin máy tính của bạn. User được sử dụng để login, gán quyền, v.v.. Mặc định khi bạn thêm một User mới vào thì User này sẽ sở nằm trong một group với tên trùng với tên user
- Có 2 loại user trên linux : user **root** là user toàn quyền và mặc định trên các hệ thống linux, ngoài ra là các user khác được phân quyền thấp hơn.

- Dưới đây là cách dùng lệnh `su` và `exit` để chuyển qua lại giữa phiên làm việc với user *root* và user thường:
 
 <img src="https://github.com/tulha161/linux/blob/main/images/13.1.png">

- **Group** là thuật ngữ chỉ 1 nhóm tập hợp của nhiều user lại với nhau. Mỗi user trên linux bắt buộc phải thuộc một group chính (gọi là Primary Group), ngoài ra còn có thể lựa chọn tham gia vào các group khác (gọi là Secondary Group).
### Lệnh kiểm tra : 

- `id [user]` - kiểm tra cụ thể theo tên user 
- `groups [user]`- kiểm tra các groups của user
 
 <img src="https://github.com/tulha161/linux/blob/main/images/13.2.png">
## 2, Tạo và quản lý user
### Tạo user
- ` useradd <option> [username]`
- Với các option phổ biến : 
	- `-c` : thêm mô tả cho user
	- `-d` : chỉ định thư mục home cho user
	- `-m` : tạo thư mục home cho user
	- `-s` : chỉ định shell mặc định cho user

### Đặt password 
- `passwd [username]`

### Xóa user 
- `usermod --lock/--unlock [username]` - lock/unlock user
- `userdel [username]` - xóa user

- *LƯU Ý : các thao tác trên cần thực hiện dưới quyền sudo nhé !*

### Chuyển đổi giữa các user
- `su` : chuyển đổi sang user *root*
- `su - [username]` : chuyển đổi sang *[username]*
- `sudo [cmd] ` : thực thi lệnh dưới quyền sudo (cần pass sudo nhé)

## 3, Quản lý group 
### Tạo group
- `groupadd [groupname]` 

### Thêm và xóa user 
- `usermod -a -G [groupname] [username]` - thêm user vào group
- `gpasswd -M [user1,user2,user3] [groupname]` - thêm nhiều user vào gr
- `gpasswd -d [username] [groupname]` - xóa user khỏi group

### Xóa group 
- `groupdel [groupname]`

 <img src="https://github.com/tulha161/linux/blob/main/images/13.4.png">

## 4, Các file quan trọng
- `/etc/passwd` : nơi lưu thông tin chi tiết về user 
- `/etc/group` : nơi lưu thông tin về group
- `/etc/sudoers` : lệnh `sudo` được cấu hình thông qua đây, cấu hình chi tiết đặt ở đây 

