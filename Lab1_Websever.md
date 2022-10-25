# Webserver - LAMP/LEMP - Properties
## 1,Web sever
* **Web server** - **Máy chủ web** trong đó được kết nối và liên kết mạng máy tình mở rộng. Máy chủ web được cài đặt các chương trình để phục vụ ứng dụng web,chứ toàn bộ dữ liệu và nắm quyền quản lý.  Web server có thể lấy thông tin requess từ phía trình duyệt web và gửi phần hồi tới máy khách thông qua HTTP hoặc giao thức khác.
* Những web server được sử dụng nhiều nhất hiện nay: Apache, Nginx, IIs...
![image](https://user-images.githubusercontent.com/88284121/197438383-57404700-e76e-462d-8ed9-9a8dbb514cad.png)
* Cách **Web server** hoạt động:
![image](https://user-images.githubusercontent.com/88284121/197438482-5ce53a79-bd11-457d-b1d7-e75fa36a2b28.png)
## 2,Tổng quan về LAMP/LEMP 
### 2.1, LAMP Stack
**LAMP** là viết tắt của: *Linux, Apache, MySQL và PHP* được sắp xếp theo các lớp hỗ trợ nhau, tạo thành các stack phần mềm.
1. Lớp thứ nhất: **LINUX**
``` 
HĐH này là cơ sở nền tảng cho các lớp phần mềm khác.
```
2. Lớp thứ hai: **APACHE**
```
Lớp thứ hai bao gồm phần mềm Web Server.
Lớp này nằm trên lớp Linux.
Web server chịu trách nhiệm chuyển đổi các web browser sang các website chính xác của chúng.
```
3. Lớp thứ ba: **MYSQL**
```
Lớp thứ ba là nơi cơ sở dữ liệu database được lưu trữ.
MySQL lưu trữ các chi tiết có thể được truy vấn bằng script để xây dựng một website.
MySQL có thể được off load xuống 1 máy chủ lưu trữ riêng biệt. (Xây dựng 1 server riêng khác với Web Server).
```
4. Lớp thứ 4: **PHP**
```
Là lớp trên cùng của stack.
Lớp script bao gồm PHP và / hoặc các ngôn ngữ lập trình web tương tự khác. Các website và ứng dụng web chạy trong lớp này.
```
* Ưu điểm lớn nhất của LAMP stack là bảo mật và sự hỗ trợ rộng rãi.
* Cả Apache, PHP và Mysql đều có mã nguồn mở, đó là lý do tại sao Linux là lớp nền tảng cho môi trường này. Đây cũng là môi trường đơn giản nhất để các developer làm web trực tuyến.
### 2.2, LEMP Stack
**LEMP** khác với LAMP **ở 1 thành phần duy nhất** là *Nginx(en-gin-x)* của LEMP thay cho *Apache* của LAMP.
**Nginx**: 
```
Là một ứng dụng HTTP proxy nhưng không có được danh tiếng ấn tượng như Apache.
Nó có ưu điểm là cho phép xử lý tốc độ tải cao hơn đối với các HTTP request.
```
### 2.3,Phân biệt LAMP/LEMP
#### 2.3.1, APACHE
* Apache đã được sử dụng từ lâu (từ những năm 1995), có rất nhiều các module được viết và cả người dùng tham gia vào mở rộng hệ chức năng cho Apache.
* Phương pháp process/thread-oriented – sẽ bắt đầu chậm lại khi xuất hiện tải nặng, cần tạo ra các quy trình mới dẫn đến tiêu thụ nhiều RAM hơn, bên cạnh đó, cũng tạo ra các thread mới cạnh tranh các tài nguyên CPU và RAM;
* Giới hạn phải được thiết lập để đảm bảo rằng tài nguyên không bị quá tải, khi đạt đến giới hạn, các kết nối bổ sung sẽ bị từ chối;
* Yếu tố hạn chế trong điều chỉnh Apache: bộ nhớ và thế vị cho các dead-locked threads cạnh tranh cho cùng một CPU và bộ nhớ.
#### 2.3.2, NGINX
* Ứng dụng web server mã nguồn mở được viết để giải quyết các vấn đề về hiệu suất và khả năng mở rộng có liên quan đến Apache.
* Phương pháp Event-driven, không đồng bộ và không bị chặn, không tạo các process mới cho mỗi request từ web.
* Đặt số lượng cho các worker process và mỗi worker có thể xử lý hàng nghìn kết nối đồng thời.
* Các module sẽ được chèn vào trong thời gian biên dịch, có trình biên dịch mã PHP bên trong (không cần đến module PHP).
## 3, LAB
### 3.1, Check version PHP, MYSQL đã cài đặt
* PHP:

![image](https://user-images.githubusercontent.com/88284121/197443302-ed21c581-5059-48da-93a0-f040d5720523.png)

* MYSQL:

![image](https://user-images.githubusercontent.com/88284121/197443525-376bf7a4-8310-4e68-b82d-2cd942c87acb.png)
### 3.2, Log ứng dụng MySql, Apache, Nginx
* MySQL:

![image](https://user-images.githubusercontent.com/88284121/197443525-376bf7a4-8310-4e68-b82d-2cd942c87acb.png)

* Apache:

![image](https://user-images.githubusercontent.com/88284121/197445805-7ba2f657-90b4-4e60-b1d3-b32310562e9d.png)

* Nginx:

![image](https://user-images.githubusercontent.com/88284121/197446242-495a48aa-56bd-43e1-9d74-b9880a7ef6dd.png)


