# DNS
## 1, DNS là gì?
* **DNS**: là hệ thống phân giải tên miền viết tắt của từ **Domain Name System**, là một hệ thống cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền trên Internet.
* Mỗi thiết bị điện tử, server, webserver đều có một địa chỉ duy nhất được gọi là địa chỉ IP. Địa chỉ IP có dãy số dài không dễ nhớ. Vì thế, chúng ta đã nghĩ ra một giao thức có thể thay thế dãy số khó nhớ này thành một “cái tên” hay còn gọi là tên miền dễ nhớ hơn và đây chính là lý do DNS ra đời.
## 2, Nguyên tắc làm việc của DNS
* hoạt động của DNS chủ yếu dựa vào DNS Query, các câu hỏi truy vấn. Ở đây mình lấy ví dụ client cần truy cập vào trang web **example.com**
* ![image](https://user-images.githubusercontent.com/88284121/199155573-f19a26ff-ab64-42e5-ae94-2149e3c5d9ab.png)
### 2.1, DNS Resolver -> Root Server
* Nơi đầu tiên nhận DNS Query khi có phát sinh dịch vụ DNS. Nó hoạt động như điểm trung gian nữa Client và DNS Nameserver.
* Khi nhận đc DNS query từ client, nếu CÓ thông tin đã được cached lại từ trước, nó respond về cho Client.
* Nếu KHÔNG, nó sẽ DNS query tới Root Server.
### 2.2, Root Server
* DNS Root Server - là server quan trọng nhất trong hệ thống cấp bậc của DNS. Có tổng cộng 13 Root Server trên thế giới ( 10 cái đặt tại Mỹ ). Nó hoạt động như một thư viện lớn để định hướng query của bạn tới các nơi lưu trữ nhỏ hơn.
* Khi nhận được DNS query từ DNS Resolver với nội dung query IP của tên miền : example.com , nó sẽ respond lại cho DNS Resolver bằng cách hướng nó tới TLD Server dựa trên phần mở rộng của tên miền đó ( .com, .vn, .org, .net ,... etc ...). Ở đây là TLD Server `.com`.
### 2.3, TLD Server
* **TLD - Top Level Domain** Servers: dùng để duy trì thông tin cho tất cả các tên miền có chung một phần mở rộng như chúng ta đã nói bên trên (.com, .vn, .net, .org,...).
* Ở đây query của mình là example.com, vì vậy thôn tin được lưu trong TLD Server .com. Nó nhận query và sẽ phản hồi lại cho DNS Resolver thông tin về Authoritative Server - nơi chính thức chứa nguồn dữ liệu về tên miền này.
### 2.4, Authoritative Server ( SLD nameserver )
* Đây là nơi việc phân giải tên miền diễn ra. Khi nhận query từ DNS Resolver, Authoritative Server chứa các thông về tên miền example.com ứng với IP nào, nó sẽ respond lại IP này cho DNS Resolver.
* DNS Resolver phản hồi lại cho Client IP của hostname example.com
### 2.5, Ex
* Thực hiện DNS Query: `dig +trace [hostname]`

* ![image](https://user-images.githubusercontent.com/88284121/199156998-8e0cd525-39a0-4443-917b-93c16cf1ab36.png)

* B1: Khi truy vấn `facebook.com` trên client thì DNS Resolver làm cầu nối trung gian, DNS Resolver ở đây là 127.0.0.53

* ![image](https://user-images.githubusercontent.com/88284121/199157071-fa73b6eb-fb4f-4862-afb6-1d72aa685b95.png)

* B2: DNS Resolver thực hiện query tới root server

* ![image](https://user-images.githubusercontent.com/88284121/199157129-93e1bc93-4cc9-4523-b671-246d1f87ee52.png)

* B3: Root server chỉ dẫn DNS Resolver tới TLD .com

* ![image](https://user-images.githubusercontent.com/88284121/199157196-8bc87d0a-09d6-4a8b-a4ab-aae2d0c66a1a.png)

* B4: TLD Server giới thiệu đến Authoritative nameserver, ở đây ta truy vấn thành công thông tin IP của facebook.com = 129.134.30.12

* ![image](https://user-images.githubusercontent.com/88284121/199157309-9fbea2fb-7dda-4508-a0bd-9ad85a25c283.png)

