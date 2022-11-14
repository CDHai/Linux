#SSH 
## 1, SSH là gì?
* **Secure Shell - ( SSH )** là một giao thức mạng dùng để thiết lập kết nối mạng một cách bảo mật. SSH tạo ra một kênh kết nối được mã hóa an toàn từ một mạng không an toàn, dựa trên kiến trúc client-server, kết nối 1 SSH-client tới một SSH-server. 
* Port mặc định đuợc sử dụng bởi SSH là **22**.
* SSH có nhiều cách để xác thực một người dùng, nhưng 2 cách thông dụng nhất vẫn là xác thực dựa trên **mật khẩu** và **public-key**.
  - Xác thực bằng **mật khẩu**: Xác thực dựa trên mật khẩu đơn giản là bạn chỉ việc sử dụng mật khẩu của user bạn tạo để truy cập, server sẽ lưu chúng, và đối chiếu với mật khẩu của bạn khi đăng nhập. Cách này thì không đủ an toàn do bạn có khả năng bị đánh cắp mật khẩu.
  - Xác thực bằng **public-key**: Cách này sử dụng một cặp khóa – public-key và private-key – được tạo ra dựa trên thuật toán mã hóa public-key. Cặp khóa sau khi được tạo ra từ một máy tính, ta sẽ lấy public-key lưu vào server, khi truy cập ta sẽ dựa vào private-key lưu trên máy local và đặc tính liên quan mật thiết tới nhau của chúng để thiết lập kết nối. Kiểu xác thực này còn cho cho phép chúng ta thiết lập một kết nối an toàn một cách tự động hóa (automation).
  - ![image](https://user-images.githubusercontent.com/88284121/201571558-dfbc6fe9-69d2-4790-ba73-d7d2bf058d76.png)
## 2, Các câu lệnh cơ bản
### 2.1, Sử dụng SSH để login với password
