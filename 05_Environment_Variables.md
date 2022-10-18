# Environment Variables
## 1, Biến môi trường là gì?
* Biến môi trường là **giá trị động** ảnh hưởng trực tiếp đến phần mềm và tiến trình hoạt động trên server.
* Biến môi trường – environment variable có trên mọi hệ điều hành và có nhiều loại khác nhau, có thể được tạo, chỉnh sửa, lưu hay xóa.
* Biến môi trường của linux chứa thông tin hệ thống, mà sẽ chuyển dữ liệu đó đi cho phần mềm trong shells hoặc sub-shells.
## 2, Xem toàn bộ biến môi trường đang có
Có **2 cách** để xem Linux Environtment Variable:
* Cách 1: Sử dụng lệnh 
> printevn

```
Nhưng nếu chỉ dùng lệnh này không sẽ hiển thị rất nhiều biến trên Ubuntu nên bạn cần thêm option less để chỉ hiển thị các output quản lý được
```

* Cách 2: Sử dụng lệnh 
> printenv | less
```
Biến môi trường thường được viết in hoa, nhưng bạn cũng có thể in thường. Kết quả của printenv hiển thị tất cả các biến môi trường in hoa.
Nếu bạn muốn xem giá trị của một biến nhất định, bạn cần gõ tên biến như là đối số trong lệnh printenv và cần gõ chính xác nó in hoa hay thường.
```

**Ví dụ:**
* Có: HOME = home/cdhai

Có **2 cách** để hiển thị biến HOME:
* printenv HOME
* echo $HOME 

![image](https://user-images.githubusercontent.com/88284121/196361913-1c2507fc-bd6c-4c0a-a55d-4d0ecc0d6a65.png)
## 3, Tạo biến môi trường
Cú pháp cơ bản để tạo 1 biến:
```
export VAR="value"
```

Nó có nghĩa:
* **export** : lệnh được dùng để tạo biến
* **VAR** : tên biến
* **value** : giá trị của biến
## 4, Gỡ giá trị ra khỏi biến môi trường Linux
Cú pháp cơ bản để gỡ 1 biến:
``` 
unset VAR 
```
Nó có nghĩa:
* **unset** : lệnh
* **VAR** : biến bạn muốn gỡ

```
Đặt và gỡ đặt (Setting / unsetting)  Linux environmental variable sẽ ảnh hưởng đến các tiến trình đang chạy. Nếu bạn muốn đặt cấu hình cố định cho biến môi trường, bạn cần định nghĩa trong file cấu hình cá nhân – i.e. .bash_profile.
```
## 4, Biến môi trường Local và Global trong Linux
* Trong lập trình máy tính, **global variable** là biến được dùng khắp mọi nơi trong ứng dụng. Biến global có thể lấy trong shell session và bất kỳ child process nào.
* **Local environment** thì là biến được định nghĩa 1 lần trong hàm đó. Local variable chỉ có trong shell mà nó được tạo.
```
System environment variables dùng tất cả các ký tự được in hoa để phân biệt với biến người dùng thông thường.
```
**Ví dụ**:
* **local_var** chỉ hiện trong shell hiện hành:

![image](https://user-images.githubusercontent.com/88284121/196369668-399736ad-c306-4018-ad34-9a8ff230403b.png)

* Chúng ta có thể tạo biến **global** bằng lệnh **export**:

![image](https://user-images.githubusercontent.com/88284121/196369875-b745f91f-4aae-4f2c-ba18-1e32481b5ab7.png)

![image](https://user-images.githubusercontent.com/88284121/196370002-74f7e1b6-c4b9-471d-9c50-10716f04254f.png)
