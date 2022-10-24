# Managing Processes
Khi khởi chạy linux, chạy ứng dụng hay thậm chí là thực thi một câu lệnh bất kỳ trên terminal, hệ thống sẽ tạo tiến trình cho bất cứ hoạt động nào có nêu ở trên. 

Quản lý tiến trình sẽ bao gồm : 
* Identify và monitor tiến trình;
* Phân biệt tiến trình chạy foreground/background;
* Thao tác kill tiến trình.

## CÁC TRƯỜNG QUAN TRỌNG:
| Trường thông tin | Công Dụng 
| ----     | -----
| PID | Process ID - ID của tiến trình 
| PPID | PID của tiến trình cha 
| TTY | Terminal liên quan đến tiến trình
| UID | User ID 
| USER | USER sử dụng
| TIME | thời gian CPU thực hiện
| CMD | Câu lệnh để thực hiện 
| %CPU | lượng CPU sử dụng
| %MEM | lượng Ram sử dụng
| S/STAT | Trạng thái tiến trình
| PRI | độ ưu tiên
| RSS | bộ nhớ thực sử dụng
| VSZ/SZ | bộ nhớ ảo sử dụng

## 1, PS (Process Status)
* Là một trong những lệnh cực kì quan trọng trong quản lý tiến trình, nó show ra các thông tin mà người dùng yêu cầu liên quan đến các thông số, trạng thái của tiến trình trên hệ thống.
* **NOTE**: Chỉ tại thời điểm thực thi câu lệnh ( Không mang tính real-time).
* Cú pháp:
```
ps + [option]
```
Các option phổ biến:
* `ps axu` : show all process on system using BSD syntax.
* `ps -ef`: show all process on system using standard syntax.
* `ps -U root -u root u` : show process running as root.
* `ps -q PID -o comm=` : show only name of PID = ? ( replace PID that you want ).
* `ps -C PROCESS -o pid=` : show only PID of PROCESS ( replace PROCESS that you want ).
* Tham khảo thêm tại: https://www.tecmint.com/ps-command-examples-for-linux-process-monitoring/
## 2, Lệnh `top` và `htop`
* Nếu như `ps` là lệnh kiểm tra tiến trình ở **trạng thái tĩnh trong thời điểm thực thi lệnh** thì `top` và `htop` là 2 lệnh quan trọng để monitoring hệ thống **realtime**. Lệnh này sẽ cho phép hiển thị **thời gian thực trạng thái các tiến trình đang chạy**.
* `top`:

![image](https://user-images.githubusercontent.com/88284121/197449290-a3c470c8-29e8-443e-87b9-20a60a5072ae.png)

* `htop`:

![image](https://user-images.githubusercontent.com/88284121/197449357-0f555d88-2bdb-42b6-ac6c-c33286928f2d.png)

* Để dừng câu lệnh và tiếp tục sử dụng terminal ta sử dụng tổ hợp phím `Ctrl + Z`.
## 3, Foreground và Background Proceses
* Khi bắt đầu một tiến trình, có 2 cách để nó chạy là foreground và background.
* Theo mặc định, mọi tiến trình khởi chạy là foreground, nhận input từ bàn phím và gửi input ra màn hình. Điều này nghĩa là trong khoảng thời gian tiến trình chạy đến lúc đưa ra kết quả, nó sẽ chiếm dụng luôn session đến khi chạy xong. Điều này là ổn với các tiến trình trả kết quả tức thời như ( ls, cd, cat, mv,.... ) nhưng lại là không hợp lý với các tiến trình chạy thời gian dài, liên tục ví dụ như trình duyệt web.
* Thử chạy foreground ứng dụng "Google Chrome" bằng cmd: `google-chrome` trên Terminal:

![image](https://user-images.githubusercontent.com/88284121/197451058-93199126-3c6b-471f-98a4-8b198a8486b1.png)
* Khi sử dụng câu lệnh này, 1 tab Chrome sẽ tự động mở ra và Terminal sẽ sang 1 câu lệnh mới giống như việc nhận input từ bàn phím, thực hiện output ra màn hình ngay lập tức và câu lệnh bị ngắt.

![image](https://user-images.githubusercontent.com/88284121/197451698-831a6e2c-be38-4d09-bca9-36bcc3aa2715.png)
* Ở câu lệnh này, vẫn 1 tab tự động mở ra nhưng thêm vào đó Terminal sẽ để cho chúng ta tiếp tục sử dụng cmd.
## 4, Kill Processes - Ngắt tiến trình
* `kill` : là lệnh sử dụng để ngắt tiến trình đang chạy bằng cơ chế tín hiệu Kill Signal.
* Cú pháp:
```
kill [signal] [pid]
```
* Để hiển thị đấy đủ các Signal: `kill -l`

![image](https://user-images.githubusercontent.com/88284121/197452384-1c79b561-2319-4bab-9407-bf2864dc5fc3.png)
* Hầu như chúng ta chỉ dùng SIGKILL (9) và SIGTERM (15):
  - 15, SIGTERM - đây là default signal, khi `kill [PID]` mà không kèm thêm tham số signal sẽ mặc định dùng signal này. Nó giống như đóng tiến trình thông thường, cho phép dọn dẹp/ đóng các tài nguyên đang sử dụng rồi mới thoát, tránh corrupted.
  - 9, SIGKILL - đây là signal mạnh mẽ hơn, force kill tiến trình một cách ngay lập tức, không cho nó làm các bước dọn dẹp tài nguyên, đang chạy thì ngắt luôn chứ không báo trước. Tín hiệu này hạn chế sử dụng vì dễ gây corrupt dữ liệu.
