# BACKUP

## 1, Vì sao phải backup ? 
- Trong quá trình hoạt động hằng ngày, việc sao lưu lại các dữ liệu quan trọng hay lớn hơn là sao lưu cả hệ thống là việc hết sức quan trọng vì hệ thống nào cũng có rủi ro, nguy cơ mất dữ liệu cho đến lỗi hệ thống. 
- Backup hay sao lưu hiểu đơn giản là lưu dữ liệu quan trọng sang một nơi khác an toàn hơn để sử dụng trong việc rollback ngay lập tức khi cần. 
- Backup truyền thống thì có cáchcopy dữ liệu ( lệnh `cp`), tuy nhiên việc này mang tính local, ví dụ như bạn đã copy đủ dữ liệu sang một folder */backup* nào đó trên hệ thống, thực hiện daily bằng crontab rồi, tuy nhiên khi toàn bộ hệ thống sụp đổ thì dữ liệu của bạn cũng sẽ đi theo. Vì vậy, ta cần có những công cụ mạnh mẽ hơn để lưu data sang một máy khác độc lập, thậm chí đẩy lên cloud để lưu trữ cho an toàn.
- Vì vậy, ta đã có **rsync**

## 2, RSYNC

### 2.1, RSYNC là gì ? 
- **Rsync** (Remote Sync) là một công cụ dùng để sao chép và đồng bộ file/thư mục được dùng rất phổ biến. Với sự trợ giúp của rsync, bạn có thể đồng bộ dữ liệu trên local hoặc giữa các server với nhau một cách dễ dàng.

- Các tính năng nổi bật : 
	- Rsync hỗ trợ copy giữ nguyên thông số của files/folder như Symbolic links, Permissions, TimeStamp, Owner và Group.
	- Rsync nhanh hơn *scp* vì Rsync sử dụng giao thức remote-update, chỉ transfer những dữ liệu thay đổi mà thôi.
	- Rsync tiết kiệm băng thông do sử dụng phương pháp nén và giải nén khi transfer.
	- Rsync không yêu cầu quyền super-user.
	
### 2.2, Sử dụng RSYNC thế nào ?
- Cú pháp: `rsync <option> [source] [dest]`

- một số option phổ biến :

| Option | Usage
| ------ | -----------
| -a | archive mode
| -v | hiển thị trạng thái kết quả.
| -r | copy dữ liệu recursively, nhưng không đảm bảo thông số của file và thư mục.
| -z | nén dữ liệu khi transfer, tiết kiệm băng thông tuy nhiên tốn thêm một chút thời gian.
| -h | human-readable, output kết quả dễ đọc.
| --delete | xóa dữ liệu ở destination nếu source không tồn tại dữ liệu đó.
### Demo thực tế 

- Thực hiện trên local : 
`rsync -vzh abc.yml /home/client1/backup/` - với file abc.yml

 <img src="https://github.com/tulha161/linux/blob/main/images/17.1.png">

`rsync -avzh abc.folder /home/client1/backup` - với folder abc.folder

 <img src="https://github.com/tulha161/linux/blob/main/images/17.2.png">

- Thực hiện rsync folder từ local -> remote server :

`rsync -avzh abc.folder root@192.168.122.3:/root/backup`

 <img src="https://github.com/tulha161/linux/blob/main/images/17.3.png">
 <img src="https://github.com/tulha161/linux/blob/main/images/17.4.png">

- Thực hiện rsync folder từ remote server -> local :
`rsync -avzh root@192.168.122.3:/root/backup/abc.folder /home`

## 3. Nén dữ liệu
- Trong quá trình backup, việc nén file/folder lại là rất quan trọng vì nó sẽ tiết kiệm dung lượng rất hiệu quả, tối ưu quá trình storage và tranfer. 

- tar : công cụ này mang tính chất gom nhiều hơn là nén, dung lượng sẽ vẫn được tối ưu nhưng không nhiều
	- cú pháp : `tar <option> [FILE NÉN] [FILE/FOLDER bị nén]`
	- option : 
	- `-c` : create (nén)
	- `-x` : giải nén 
	- `-z` : kết hợp nén gzip
	- `-f` : nén thành **File**
	- `-p` : bảo toàn quyền
- Ví dụ : `tar -czf /backup/tmp.tar.gz /tmp` <-> `tar -xzf /backup/tmp.tar.gz /backup/tmp`
- Trên đây mình nén folder **/tmp** bằng tar + gzip và đưa vào -> **/backup/tmp.tar.gz** và sau đó giải nén nó ra tại thư mục này luôn. 
- Để tiện so sánh, mình sử dụng cả nén bằng tar và tar + gzip, kết quả như sau : 

 <img src="https://github.com/tulha161/linux/blob/main/images/17.5.png">

- Trong khi đó dung lượng folder gốc lên tới 104K, như vậy hiệu quả nén là rất cao ! 

 <img src="https://github.com/tulha161/linux/blob/main/images/17.6.png">

- Như vậy, ta có thể thấy các công cụ nén giúp ta 2 việc : gom dữ liệu từ folder lại thành một file nén duy nhất và tối ưu về mặt dung lượng. Còn rất nhiều các công cụ nén khác như gunzip, zip, bunzip2,... mà mình không tiện nêu ở đây, tuy nhiên về mặt bản chất các công cụ hoạt động như nhau và đều tương tác được với `tar`. Anh em va đâu search đấy nhé :D

## 4. DD 
- `dd` là công cụ sử dụng khi ta cần sao chép ổ cứng, sao chép phân vùng
- Cú pháp : `dd if=dev/sda of=dev/sdb ` - lệnh này có ý nghĩa là sao chép ổ /dev/sda -> ổ /dev/sdb
- `dd` cũng có thể sao chép partion, tạo image của ổ cứng, tạo cdrom backup.
