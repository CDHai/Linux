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
* printevn HOME
* echo $HOME 

