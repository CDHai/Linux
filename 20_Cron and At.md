# Cron và `at`

## 1, Cron
- Cron là một tiện ích giúp lập lịch chạy những dòng lệnh bên phía server để thực thi một hoặc nhiều công việc nào đó theo thời gian được lập sẵn. Một số người gọi những công việc đó là Cron job hoặc Cron task.
- Cron là một chương trình deamon, tức là nó được chạy ngầm mãi mãi một khi nó được khởi động lên. Như các deamon khác thì bạn cần khởi động lại nó nếu như có thay đổi thiết lập gì đó. Chương trình này nhìn vào file thiết lập có tên là *crontab* để thực thi những task được mô tả ở bên trong.
- Có tệp crontab trên toàn hệ thống và crontab cho mỗi người dùng
- Mỗi dòng của tệp crontab đại diện cho một công việc và bao gồm một biểu thức được gọi là `cron`, theo sau là một lệnh shell để thực thi.
- Để mở trình soạn thảo crontab xem các công việc đang được cấu hình + tạo/ chỉnh sửa công việc mới : `crontab -e`
- Mỗi dòng của tệp crontab chứa 6 trường `min hour dom mon dow cmd` được mô tả như sau:

| Định dạng | Mô tả | Giá trị cho phép
| --------- | ----- | ---------------------
| min | Phút | 0-59
| hour | Giờ | 0-23
| dom | Ngày | 0-31
| mon | Tháng | 1-12
| dow | Ngày trong tuần | 0-6
| cmd | command | Lệnh thực cần thi

 <img src="https://github.com/tulha161/linux/blob/main/images/16.1.png">
 
- Mình demo bằng cách lập lịch tự động nén folder `/etc` và để vào `/backup/etc.tar.gz` vào **10h 10 phút tất cả các ngày trong tuần**
- Hãy cùng xem kết quả : 

 <img src="https://github.com/tulha161/linux/blob/main/images/16.2.png">

- Đây là một ví dụ đơn giản giúp các bạn hiểu về cách lập lịch qua `crontab -e`, ta hoàn toàn có thể lập lịch chạy tự động các file scripts liên quan đến việc backup, đẩy dữ liệu phức tạp hơn. Ứng dụng của `crontab` là khá lớn, giúp bạn tối ưu hóa các công việc lập đi lập lại của mình hay đặt lịch cho các công việc trong tương lai ! 

- Lệnh xóa : `crontab -r` để xóa các cronjob đang được cài

## 2, `at` 
- lệnh `at` cũng có vai trò lập lịch cho câu lệnh.
- Cú pháp 
 	- `at now + [n minute/hour/day/week]` - lập lịch cho thời gian now + thời gian tương ứng ( Ví dụ : `at now + 10 minute` = 10 phút nữa lệnh sẽ chạy ) 
 	- `at [time]` - chỉ định thời gian cụ thể ( VD : `at 23:00` - chỉ định thời gian vào 23h00 )
 	- `atq` - kiểm tra các lệnh đã được đặt lịch
 	- `atrm [jobid]` - xóa lệnh đã được đặt lịch 
 - Ví dụ về sử dụng `at` dạng thường và pipeline : 

 <img src="https://github.com/tulha161/linux/blob/main/images/16.3.png">

- Ở đây mình lập lịch để đẩy nội dung dạng text vào `test.txt`, 2 lệnh với 2 dạng dùng khác nhau.

 <img src="https://github.com/tulha161/linux/blob/main/images/16.4.png">
