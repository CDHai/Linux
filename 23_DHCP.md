# DHCP
## 1, DHCP là gì?
* **DHCP** - *Dynamic Host Configuration Protocol*: là giao thực cấu hình host động. Nó cung cấp cho máy tính địa chỉ ip; subnet mask; default gateway. Nó thường được cấp phát bởi DHPC server được tích hợp sẵn trên router.
* DHCP giao tiếp bằng UDP và sử dụng port 67 và 68. DHCP server sử dụng port 67 để nghe thông tin từ các client và sử dụng port 68 để reply thông tin.
### 1.1, Mô hình và Thành phần
* DHCP làm việc theo mô hình client server và thành phần chính của DHCP là:
  - DHCP client: Là thiết bị dùng để kết nối vào mạng.
  - DHCP server: Là thiết bị dùng để cấp phát địa chỉ cho client.
### 1.2, Ưu điểm
* Tập trung quản trị thông tin cấu hình host.
* Cấu hình động các máy.
* Cấu hình IP cho các máy một cách liền mạch.
* Sự linh hoạt.
* Đơn giản hóa vài trò quản trị của việc cấu hình địa chỉ IP của client.
* Sự linh hoạt.
### 1.3, Nhược điểm
* Không nên sử dụng địa chỉ IP động, địa chỉ IP thay đổi đối với các thiết bị cố định và cần truy cập liên tục như máy in và file server.
* Không nên sử dụng IP động cho các thiết bị cố định như máy in văn phòng. Dù các thiết bị này chỉ sử dụng chủ yếu trong môi trường văn phòng, nhưng việc gán chúng với các địa chỉ IP thay đổi không mang tính thực tiễn.
* Cách thiết lập này cực kỳ không cần thiết và có thể dễ dàng tránh được bằng cách không sử dụng DHCP cho các loại thiết bị trên, thay vào đó hãy gán một địa chỉ IP tĩnh cho chúng.
* Điều tương tự cũng xảy ra nếu bạn cần có quyền truy cập từ xa vào máy tính trong một mạng nội bộ trong lâu dài. Nếu DHCP được bật, máy tính đó sẽ nhận được một địa chỉ IP mới tại một thời điểm nào đó, có nghĩa là những gì máy tính đã ghi lại sẽ không chính xác được lâu. Nếu bạn đang sử dụng phần mềm truy cập từ xa, bạn sẽ cần phải sử dụng địa chỉ IP tĩnh cho thiết bị đó.
## 2, Nguyên lí hoạt động của DHCP
* Thành phần chính của DHCP bao gồm 4 bản tin:
  - DISCOVERY
  - OFFER
  - REQUEST
  - ACK
* Quá trình cấp phát địa chỉ IP trong giao thức DHCP bao gồm các bước sau:
* ![image](https://user-images.githubusercontent.com/88284121/199383738-7d0775e7-621b-4d14-9322-62bfacd53bfa.png)
* Kịch bản Client xin cấp DHCP từ Modem:
  - Bước 1: Khi muốn có địa chỉ IP để truy cập vào internet thì client sẽ tạo ra bản tin DISCOVERY để yêu cầu cấp phát địa chỉ IP.
  - Bước 2: Client chưa biết địa chỉ chính xác của Server cấp phát địa chỉ cho mình do đó nó sẽ gửi bản tin này dưới dạng broadcast.
  - Bước 3: Server sẽ nhận bản tin DISCOVERY của client. Sau khi biết client muốn được cấp địa chỉ IP nó sẽ kiểm tra xem địa chỉ IP nào phù hợp để cấp cho Client sử dụng.
  - Bước 4: Server tạo bản tin OFFER. Gói tin này sẽ lưu trữ thông tin về IP và các thông số cấu hình khác mà client yêu cầu để có thể sử dụng để truy cập internet.
  - Bước 5: Tất cả các server sẽ gửi bản OFFER dưới dạng broadcast.
  - Bước 6: Client nhận gói OFFER và nó sẽ chọn ra bản OFFER đầu tiên mà nó nhận được. Nếu không nhận được OFFER nào trong một khoảng thời gian nào đó thì nó sẽ gửi lại DISCOVERY một lần nữa.
  - Bước 7: Client tạo ra gói REQUEST. Và gửi dưới dạng broadcast tới tất cả các server. Server nào được nhận OFFER sẽ mang ý nghĩa là nó đồng ý nhận IP. Server nào không được nhận OFFER thì thông báo là không nhận OFFER đó.
  - Bước 8: Server nhận bản tin REQEST. Các server không được nhận OFFER sẽ bỏ qua gói tin này. Gói tin nào được nhận OFFER sẽ nhận và xử lý nó. Nó sẽ kiểm tra sem IP này còn sử dụng được hay không. Nếu còn sử dụng được thì nó sẽ ghi lại thông tin và gửi lại gói tin ACK cho client. Còn nếu không thì nó sẽ gửi lại ACK để quay lại bước 1.



