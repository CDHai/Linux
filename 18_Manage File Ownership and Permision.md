# Manage File Ownership and Permision 
- Trong hệ thống mã nguồn mở linux file/folder luôn bị giới hạn bởi quyền và chủ sở hữu, đó là hai yếu tố không thể tách rời.

## 1. Các quyền ( permission ) và đối tượng sở hữu ( owner ) : 
- Permission : 
	- `r` - read - quy định bằng số `4`
	- `w` - write - quy định bằng số `2`
	- `x` - execute - quy định bằng số `1`
- Owner : một file/folder bất kỳ trên hệ thống sẽ chịu quản lý của 4 đối tượng gọi tắt là `ugoa`
	- `u` - là user tạo ra file/folder đó, đồng thời là chủ sở hữu
	- `g` - group mà user trực thuộc
	- `o` - other , đối tượng ko thuộc u và g
	- `a` - all, toàn bộ user tồn tại trên hệ thống, ít được sử dụng nhất trong cơ chế quản lý này.
- Tiếp theo, hãy tìm hiểu cách tra cứu cụ thể các file, folder trên hệ thống đang được quản lý thế nào
- Cú pháp lệnh kiểm tra : `ls -la` hoặc `ll`- kiểm tra các file/folder ở nơi đang đứng. Kết quả như sau : 

 <img src="https://github.com/tulha161/linux/blob/main/images/14.1.png">

- Ở đây các quyền và owner được thể hiện rõ ràng : 
	- 10 dấu gạch đầu : dấu đầu tiên thể hiện đây là file hay folder ( `d` là folder ), 3 dấu tiếp theo thể hiện các quyền của `u`, 3 dấu tiếp thể hiện các quyền của `g`, 3 dấu cuối thể hiện các quyền của `o` 
	- tiếp theo là tên user và tên group chủ.
- Ngoài ra, còn có có cách đọc theo dạng số gọi là **Octal Mode**, lấy tổng các số theo quy định phần quyền ở trên
	- Ví dụ : quyền lần lượt của u,g,o là như sao : rwxrw-r-x = 765 ; rwxr--r-- = 744

## 2. Lệnh CHOWN 
- cú pháp : `chown <option> [user:group] [file/folder]`
- tác dụng : thay đổi quyền ở hữu, có thể thêm option `-R` để thay luôn cho các tệp con
- Ví dụ, ở đây mình thay đổi chủ sỡ hữu cho folder **test.txt** đang thuộc sở hữu của *root:root* -> *tule:tule* thì thực thi câu lệnh : `sudo chown tule:tule test.txt`
- Kiểm tra lại bằng `ll` xem file đã được thay đổi chủ sở hữu chưa 
- ![image](https://user-images.githubusercontent.com/88284121/198928819-e32a4b30-4f42-469f-b7bc-9a9b0832c82d.png)
## 3. Lệnh CHMOD
- cú pháp : `chmod <option> [permission] file/folder`
- tác dụng: thay đổi permission của file/folder, cũng áp dụng với option `-R` để thay đổi cho cả các tệp con.
- Một số ví vụ vể sử dụng : 

 ![image](https://user-images.githubusercontent.com/88284121/198928946-bb7d6ac1-f87f-47cf-913b-d335c30923de.png)

- Lấy ví dụ về file test.txt này, hiện đang thuộc chủ sở hữu `root`, ugo = rw-r--r-- = 644
	- Nếu muốn gán thêm quyền `x` vào cho tất cả ugo, ta sử dụng : `chmod +x test.txt`
	- Nếu muốn bỏ quyền `x` cho tất cả ugo, ta sử dụng : `chmod -x test.txt`
	- Nếu muốn gán/bỏ quyền `x` cho riêng `o`, ta sử dụng : `chmod o+x/o-x test.txt`
	- Nếu muốn gán, bỏ quyền theo syntax kiểu **octal mode**, ta sử dụng : `chmod [abc] test.txt`  - ví dụ muốn gán full các quyền cho mọi user thì sử dụng : `chmod 777 test.txt`
 
 ![image](https://user-images.githubusercontent.com/88284121/198929169-1d933719-bd89-4c4b-b4f4-5cd9a4ea4cdc.png)
