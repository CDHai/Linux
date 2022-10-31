# Linux Logging Basic
# LOG 
## 1, Log là gì ? 
- Khi hệ thống hoạt động, nó luôn ghi lại **log**. Log bao gồm chi tiết các sự kiện xảy ra với hệ thống của bạn, bao gồm các thành phần như : thời gian, user, service, ...etc...
- Các file log hệ thống thường được ghi liên tục bất khi có event xảy ra, vị trí storing log : `/var/log`

<img src="https://github.com/tulha161/linux/blob/main/images/15.1.png">

- Đi tới folder này, có thể thấy rất nhiều log các loại được lưu trên hệ thống, trong đó có 1 số file quan trọng như sau : 
	- syslog(Debian) or messages(RetHat) : system log, lưu toàn bộ hoạt động chung của hệ thống.
	- auth.log or secure  : lưu các thông tin về các event đăng nhập/đăng xuất hệ thống trực tiếp/ từ xa.
	- kern.log : kernel log - nơi đây lưu các thông tin về hoạt động của nhân kernel.
	- cron : lưu thông tin về cron jobs.
	- Các log của ứng dụng, service hay được lưu trong các folder riêng của chúng, ví dụ như log về hoạt động của *apache* lưu ở */var/log/apache*.
- ![image](https://user-images.githubusercontent.com/88284121/198930600-7345f343-93c1-4122-8c73-22ce743261b9.png)
- ![image](https://user-images.githubusercontent.com/88284121/198930659-8cf7da28-93fd-467e-b47b-a0792f84577a.png)
## 2, Log Rotation
- File log rất quan trọng, nó là nhật ký hoạt động của hệ thống nói chung hay của từng ứng dụng dịch vụ nói riêng. Với một hệ thống việc chạy và ghi log liên tục là điều hết sức bình thường, nhưng mặc định nó lưu tất cả các log vào chung 1 file lại gây ra đôi chút phiền toái khi ta cần phải tra soát, troubleshoot lỗi hay cả việc lưu trữ một lượng lớn log cũng sẽ tiêu tốn tài nguyên. Vì vậy, người quản trị cần phải thực hiện chính sách **chia để trị**.
- `logrotate` là công cụ sinh ra để làm công việc như vậy, nó hỗ trợ việc tách các file log ra theo tháng, theo tuần, theo ngày thậm chí là theo giờ. Nó có thể nén các file log cũ lại, xóa các file cũ đi theo lịch để giải phóng dung lượng. 
- `logrotate` hầu hết được cài mặt định trên các bản phân phối linux, file cấu hình mặc định đặt trong `etc/logrotate.conf` còn khi muốn lập lịch cho các ứng dụng cụ thể, ta sẽ tạo từng file riêng biệt trong `/etc/logrotate.d`
- Giờ hãy lập thử một file demo để chỉ định quá trình log rotation cho `/var/log/auth.log`.
- Tạo và chỉnh sửa file auth trong `/etc/logrotate.d` : `nano /etc/logrotate.d/auth`.

<img src="https://github.com/tulha161/linux/blob/main/images/15.2.png">

- `/var/log/auth.log` : thành phần chỉ định file log được rotate.
- `hourly` : chỉ định chu kỳ xoay vòng, có thể để `daily/weekly/monthly/yealy`.
- `dateext` : thêm hậu tố thời gian vào cuối tên các file log cũ, mặc định là `YYYYMMDD`. Nếu không thêm dòng này thì mặc định hệ thống sẽ đánh số tăng dần.
- `dateformat` : tùy chỉnh định dạng thời gian.
- `notifempty`: không thực hiện rotate nếu file rỗng.
- `missingok` : không báo lỗi nếu file gốc mất ( ngược lại có `nomissingok`).
- `compress` : nén log cũ, mặc định là nén `gzip`. Ngoài ra có thể chỉ định chương trình nén `compresscmd [prog]`.
- `rotate` : số lượng file log cũ được giữ lại.
- `create` : tạo file log mới sau khi rotate file cũ .

- Trên đây là một số trường thông tin có thể cấu hình, ngoài ra có thể xem thêm tại https://linuxconfig.org/logrotate-8-manual-page nếu muốn mở rộng thêm kỹ năng.

- Như vậy ta đã hoàn thành soạn xong một kịch bản log rotation.
- Lệnh kiểm tra ( debug) : `logrotate -d [file]`.
- Chạy ngay rotate mà không cần đợi chu kỳ : `logrotate -vf [file]`.
