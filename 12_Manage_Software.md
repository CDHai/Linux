# Quản Lí Phần Mềm & Dịch Vụ
## Nguyên tắc quản lí phần mềm
* Các thành phần của một phần mềm:
  - File thực hiện.
  - Các thư viện phần mềm.
  - Các file cấu hình.
  - Dữ liệu tạm thời.
* Các thao tác quản lí phần mềm.
  - Cài đặt.
  - Gỡ bỏ.
  - Cấu hình lại.
  - Lấy thông tin.
* Cách thức quản lí:
  - Độc lập.
  - Script cho từng phần mềm.
  - Quản lí bằng CSDL chung.
  - Công cụ quản lí chung.
## 1, Cài đặt phần mềm
* Phần mềm linux được phân phối dưới dạng gói cài (package) , có 2 dạng chính có đuôi là `.rpm` và `.deb` đại diện cho 2 nhánh phát triển là Redhat và Debian. Các gói cài này được định dạng như là những file nén, trong đó chứa thông tin phần mềm, các file chạy phần mềm, các thư viện đi kèm , ... etc ... Khi nhận lệnh cài đặt hệ thống sẽ bung gói và tiến hành cài đặt.
### 1.1, Binary và Source Package
* Các gói cài đến từ repository (kho) - là nơi lưu trữ các gói cài phần mềm tập trung cho 1 hệ điều hành nào đó (Ví dụ repo của Ubuntu sẽ khác với repo của CentOS)
* Ta có 2 cách cài đặt phần mềm:
  - Cài từ **Binary Package**: Đây là cách cài phổ biến hơn, download gói từ repo về, sử dụng trình xử lý package để cài đặt phần mềm vào hệ thống.
  - Cài từ **Source Package**: Đây là cách cài khó hơn, bạn vẫn sẽ lấy package từ repo hay source gốc về, nhưng không phải dùng trình xử lí package để cài đặt mà tự biên dịch phần mềm để tối ưu nhu cầu của chính bạn, nâng cao tính bảo mật,...sau đó mới đặt vào hệ thống.
### 1.2, Ví dụ cài từ Binary Package
- Đây là ví dụ 2 gói cài phần mềm "skype" theo định dạng .rpm và .deb mà mình vừa download từ skype với wget :
 
 ```` wget https://go.skype.com/skypeforlinux-64.deb ```` và
 
 ```` wget https://go.skype.com/skypeforlinux-64.rpm ````
 
  <img src="https://github.com/tulha161/linux/blob/main/images/09.03.png">
 
 - Tiếp theo mình sẽ tiến hành cài đặt thử cả 2 gói trên bằng lệnh ````rpm```` - lệnh cài đặt mặc định trên Redhat - CentOS.
 - Tất nhiên là trên CentOS thì không thể cài gói deb.
 <img src="https://github.com/tulha161/linux/blob/main/images/09.04.png">
 
 - Ở đây mình đã chạy đúng lệnh, gọi đúng package đuôi .rpm, vậy mà vẫn không được.
 
 <img src="https://github.com/tulha161/linux/blob/main/images/09.05.png">
 
 - Hệ thống trả về lỗi : ````failed dependencies```` với một list rất nhiều thứ loằng ngoằng ở dưới, như vậy là gói cài này bị lỗi chăng ??? Câu trả lời là không hề, gói cài này được download trực tiếp từ Skype website nên không lỗi, chỉ là đúng nhưng chưa đủ.
 - Như vậy, ở đây ta có một khái niệm mới là ***Dependency***. Một package thì rất ít khi mang tính **standalone** mà nó thường được xây dựng dựa trên các package khác, cũng giống như khi các bạn lập trình, khi cài đặt sử dụng một thư viện thì thư viện đó đều xây dựng dựa trên một thư viện khác, **các thư viện khác đó gọi là *dependencies***. Vì vậy, để cài đặt được package "skype" ở trên, ta buộc phải cài đặt đầy đủ các dependencies của nó, chưa kể trong số đó có thể có các dependencies của dependencies đó nữa, một cấu trúc hình cây khá là dài. 
 - Để giải quyết điều rắc rối này, thường thì người ta không hay dùng trực tiếp các tools truyền thống trên linux là ````rpm```` (Redhat) hay ````dpkg```` (Debian) mà sẽ dùng các **high-level tools** có khả năng tự động cài đặt các dependencies luôn. Ví dụ như: 
 	- Redhat : yum, dnf
 	- Debian : apt, apt-get
## 2, High-level Package Tools
### CÀI ĐẶT
* Đầu tiên, ta thử cài đặt "nginx" bằng apt-get :
 ```` sudo apt-get install nginx ```` - ở đây ta chỉ cần type đúng tên phần mềm, `apt-get` sẽ tự tìm source download về, tìm các dependencies cần thiết và tiến hành cài đặt.
* `apt-get` tự động tìm về các gói cần cài, ở đây tổng cộng có 7 gói sẽ được cài mới, sau đó nó cần người dùng confirm để tiến hành quá trình cài đặt. Quá trình diễn ra nhanh chóng, tự động và thu được kết quả đã cài thành công "nginx" 
 <img src="https://github.com/tulha161/linux/blob/main/images/09.06.png">
 <img src="https://github.com/tulha161/linux/blob/main/images/9.7.png">


### GỠ CÀI ĐẶT
- **Cú pháp lệnh gỡ cài đặt** : ```` apt-get remove PACKAGE ````
- Áp dụng vào trường hợp cụ thể là gỡ gói nginx vừa cài trước đó : 
 ```` sudo apt-get remove nginx ````
- sử dụng thêm lệnh autoremove để xóa các dependencies cho triệt để :
 ```` sudo apt-get autoremove ````
- kết quả cho thấy :
 <img src="https://github.com/tulha161/linux/blob/main/images/9.8.png">

### UPDATE & UPGRADE	
- Lệnh : ````apt-get update && apt-get upgrade```` - sử dụng cùng lúc 2 lệnh này để apt-get tự động download version mới nhất của các phần mềm trên hệ thống và upgrade chúng lên. 
- Sử dụng lệnh low-level để upgrade đối với các package được down sẵn trước đó : 
 ```` dpkg -i PACKAGE_FILE ````
 
### TRA CỨU - LIỆT KÊ 
- Liệt kê các package đã được cài (có thể dùng pipe với grep cho tiện lọc)  : 
 ```` dpkg --list ```` for Debian or
 ```` rpm -qa ```` for RedHat
- Xác định xem package được cài chưa, nếu rồi thì hiện thị các thông tin chi tiết : 
 ```` dpkg -s PACKAGE_NAME ```` or 
 ```` rpm -q PACKAGE_NAME ````
 * với high-lv tool :
 ```` apt-cache show package_name ```` or
 ```` yum info package_name ````
### More Info 
* https://viblo.asia/p/linux-cai-phan-mem-tu-source-tren-linux-YWOZr34wlQ0
