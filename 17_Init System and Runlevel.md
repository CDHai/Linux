# Initialization and Runlevels
## 1, Một số Init System phổ biến
* Trên các hệ điều hành Linux, tùy thuộc vào phiên bản, distro mà sử dụng các init system khác nhau.
### 1.1, System V
* **System V** (đọc là System Five) được phát triển bởi AT&T và được ra mắt lần đầu tiên vào năm 1983, do khá cổ và còn nhiều điểm không hoàn thiện nên SysV đang dần được thay thế bởi các Init System khác.
* Một số Linux OS sử dụng System V:
  - Debian 6 và trước nữa.
  - Ubuntu 9.04 và trước đó nữa.
  - CentOS 5 trở về trước.
### 1.2, Upstart
* **Upstart** là một init system được phát triển bởi những người đã tạo nên Ubuntu nhằm thay thế cho **SysV** trên các distro Ubuntu.
* **Upstart** có nhiệm vụ khởi chạy các tiến trình và tác vụ khác nhau, kiểm tra các process đang hoạt động và stop những process này khi shutdown hệ thống.
* Một số distro hỗ trợ Upstart (đa phần là Ubuntu vì Upstart vốn được phát triển cho riêng Ubuntu):
  - Từ Ubuntu 9.10 tới Ubuntu 14.04, 14.10.
  - CentOS 6.
### 1.3, Systemd
* **Systemd** là init system tiêu chuẩn (de facto) cho các distro được release gần đây như CentOS 7, Ubuntu 16, 18…
* **Systemd** là một init system quản lý các tiến trình trên Linux, chữ ‘d’ ở cuối có nghĩa là trình daemon. Tương tự như init, systemd là process của tất cả các process khác trong một hệ thống Linux, systemd là process đầu tiên được start lên khi boot và có PID là 1.
* Systemd được thiết kế khắc phục những khuyết điểm của init. Ví dụ như một tiến trình của init sẽ khởi động tuần tự, từng tiến trình một sẽ được start lên và đưa vô bộ nhớ. Do hoạt động theo cơ chế này nên thời gian boot hệ thống sẽ rất lâu. Trái ngược với init, systemd được thiết kế để khởi động tác tác vụ song song, vì vậy giảm thiểu được boot time và tài nguyên tính toán. Ngoài ra, systemd còn có nhiều tính năng hơn so với init, cụ thể như:
  - Khả năng xử lý các tiến trình song song.
  - Dùng socker và D-Bus để khởi chạy các dịch vụ.
  - Khởi tạo các trình daemon theo nhu cầu, quản lý các process sử dụng Linux cgroups.
  - Hỗ trợ snapshot và restore trạng thái của hệ thống.
  - Có khả năng giữ các mount point và auto mount point.
  - Có cơ chế kiểm soát dependency của service chặt chẽ.
* Lệnh `systemctl` là công cụ chính dùng để quản lý systemd. Lệnh này kết hợp cả 2 lệnh `service` và `chkconfig` thành 1 tool duy nhất để có thể quản lý hiệu quả các dịch vụ trên hệ thống.
### 1.4, Kiểm tra Init System của hệ thống
#### 1.4.1, Cách 1:
* Kiểm tra xem các folder này có tồn tại hay không:
  - Nếu có /usr/lib/systemd thì hệ thống có hỗ trợ Systemd.
  * ![image](https://user-images.githubusercontent.com/88284121/198922925-d1d8f71c-46c0-4359-837e-0fa74e2cb71b.png)
  - Nếu có /usr/share/upstart thì hệ thống có hỗ trợ Upstart.
  * ![image](https://user-images.githubusercontent.com/88284121/198923019-a70d29e0-b29c-4767-bbd6-c9739079e952.png)
  - Nếu có /etc/init.d thì hệ thống có hỗ trợ System V.
  * ![image](https://user-images.githubusercontent.com/88284121/198923069-1e123df3-3814-4fd8-99a0-a67178fa39fe.png)
#### 1.4.2, Cách 2:
* Vì init process luôn có PID là 1, ta có thể dùng lệnh sau để kiểm tra hệ thống của mình đang dùng init system nào chính:
* `ps -p 1`
* ![image](https://user-images.githubusercontent.com/88284121/198923423-434d18e9-7082-41c3-832a-8156c7e2dfbf.png)
## 2, Runlevels
* **Runlevel** là biểu thị một trạng thái trong Linux, mỗi runlevel sẽ biểu thị cho một trạng thái riêng của Linux server như shutdown, single-user mode, restart mode, mỗi một con số sẽ biểu thị một runlevel riêng.
* Các số runlevel này chạy từ 0 tới 6 và có ý nghĩa như sau:
  - **Runlevel 0**: Shutdown hệ thống.
  - **Runlevel 1**: Chế độ rescue mode, 1 user.
  - **Runlevels 2, 3, 4**: Chế độ nhiều user, có kết nối mạng, giao diện CLI.
  - **Runlevel 5**: Chế độ nhiều user, có kết nối mạng, giao diện đồ họa GUI.
  - **Runlevel 6**: Reboot hệ thống.
### Cách kiểm tra Runlevel đang chạy 
#### Cách 1:
* Ta dùng lệnh `runlevel` hoặc `who -r`
* ![image](https://user-images.githubusercontent.com/88284121/198924236-9f92ca19-2e18-4ced-b169-cf329b261d62.png)
* ![image](https://user-images.githubusercontent.com/88284121/198924321-5b94a125-b6ec-40c9-95b4-de170663c04c.png)
#### Cách 2:
* Đối với những hệ thống có hỗ trợ *systemd* thì ta có thể dùng lệnh `systemctl get-default`
* ![image](https://user-images.githubusercontent.com/88284121/198924538-73648cac-951a-4d80-894f-bc3fe0ab4f51.png)


