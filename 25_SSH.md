# SSH 
## 1, SSH là gì?
* **Secure Shell - ( SSH )** là một giao thức mạng dùng để thiết lập kết nối mạng một cách bảo mật. SSH tạo ra một kênh kết nối được mã hóa an toàn từ một mạng không an toàn, dựa trên kiến trúc client-server, kết nối 1 SSH-client tới một SSH-server. 
* Port mặc định đuợc sử dụng bởi SSH là **22**.
* SSH có nhiều cách để xác thực một người dùng, nhưng 2 cách thông dụng nhất vẫn là xác thực dựa trên **mật khẩu** và **public-key**.
  - Xác thực bằng **mật khẩu**: Xác thực dựa trên mật khẩu đơn giản là bạn chỉ việc sử dụng mật khẩu của user bạn tạo để truy cập, server sẽ lưu chúng, và đối chiếu với mật khẩu của bạn khi đăng nhập. Cách này thì không đủ an toàn do bạn có khả năng bị đánh cắp mật khẩu.
  - Xác thực bằng **public-key**: Cách này sử dụng một cặp khóa – public-key và private-key – được tạo ra dựa trên thuật toán mã hóa public-key. Cặp khóa sau khi được tạo ra từ một máy tính, ta sẽ lấy public-key lưu vào server, khi truy cập ta sẽ dựa vào private-key lưu trên máy local và đặc tính liên quan mật thiết tới nhau của chúng để thiết lập kết nối. Kiểu xác thực này còn cho cho phép chúng ta thiết lập một kết nối an toàn một cách tự động hóa (automation).
  - ![image](https://user-images.githubusercontent.com/88284121/201571558-dfbc6fe9-69d2-4790-ba73-d7d2bf058d76.png)
## 2, SSH hoạt động như thế nào?
* SSH chia dữ liệu thành một loạt các packets. Giống như bất kỳ packet nào, có một vài trường như sau:
![image](https://user-images.githubusercontent.com/88284121/205547065-cc1aa82b-5940-492a-8ba6-36f82452d38e.png)
* Cụ thể:
  - `Packet Length`: cho bạn biết gói có dung lượng như thế nào.
  - `Padding Amount`: cho bạn biết có bao nhiêu phần đệm.
  - `Payload`: dữ liệu.
  - `Padding`: là các byte ngẫu nhiên không có nghĩa gì cả nhưng được mã hóa cùng với payload để khiến việc phát hiện dữ liệu trở nên khó khăn hơn vì bạn đã ném vào dữ liệu bổ sung ngẫu nhiên này.
  - `Message Authentication Code`: để bạn có thể chắc chắn dữ liệu chưa bị giả mạo.
* `Payload` cũng có thể được **nén** bằng các **thuật toán nén tiêu chuẩn**. **Toàn bộ packet**, không bao gồm độ dài và mã xác thực, sau đó được mã hóa.

![image](https://user-images.githubusercontent.com/88284121/205547565-7fe8bfc3-6e5c-4459-99cf-fb13954cb48c.png)
* Packet sau đó được gửi đến Server. Server giải mã gói tin và giải nén Payload để trích xuất dữ liệu. Quá trình tương tự được thực hiện cho mọi gói được gửi qua connection.
* Để giữ an toàn cho SSH, SSH sử dụng **3** loại **kỹ thuật thao tác dữ liệu khác nhau tại các điểm khác nhau** trong quá trình truyền. Ba kỹ thuật được sử dụng trong SSH là:
  - Symmetrical Encryption.
  - Asymmetrical Encryption.
  - Hashing.
* Tham khảo thêm về các **kỹ thuật thao tác dữ liệu**: https://viblo.asia/p/tong-quan-ve-ssh-va-cach-connect-ssh-den-server-L4x5x34OlBM
## 3, Các câu lệnh cơ bản
### 3.1, Sử dụng SSH để login với password
