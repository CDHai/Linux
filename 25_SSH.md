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
* Tham khảo thêm về các **kỹ thuật thao tác dữ liệu**: https://www.hostinger.vn/huong-dan/ssh-la-gi-va-cach-su-dung-ssh-cho-nguoi-moi-bat-dau
## 3, Các câu lệnh cơ bản
* Trên Ubuntu Desktop sẽ có mặc định OpenSSH:
![image](https://user-images.githubusercontent.com/88284121/206083475-f47d9a7b-5a63-46c2-92a7-0856cdf77b6b.png)
* Nếu không có thì dùng lệnh để cài đặt: `sudo apt install openssh-client`
* Ở trong bài này có Ubuntu Desktop **`haicd@cowhai` - Client**, Ubuntu Server **`hello@test` - Server** 
* **Server** sẽ có IP là: ![image](https://user-images.githubusercontent.com/88284121/206085884-c6019cad-a798-4d6b-886a-73429256d00b.png)
### 3.1, Sử dụng SSH để login với password
* Thực hiện SSH ở máy **Client** như sau:
![image](https://user-images.githubusercontent.com/88284121/206086082-a55cb560-8717-45b9-879a-bb1093adc5fe.png)
* Trong đó:
  - **hello**: là tên user bạn muốn sử dụng khi ssh vào Server
  - **IP**: là IP của Server (Nếu dùng **test** như theo tên của máy chủ sẽ không thành công vì sẽ không thể phân giải được)
 * Sau khi nhập lệnh, do lần đầu kết nối SSH đến IP này, nên ssh có hỏi về ECDSA key fingerprint- gõ *yes*, rồi nhập password theo yêu cầu, ta có kết quả như sau: 
 ![image](https://user-images.githubusercontent.com/88284121/206086563-49dd23a1-b106-498d-9947-a201bd5da56d.png)
* Host ở Ubuntu Desktop đã thay = Host của Ubuntu Server -> **SSH thành công bằng password**.
#### Lưu ý
* Mặc định dùng lệnh trên Client sẽ SSH vào Server bằng cổng 22.
* Nếu công kết nối khác mình sử dụng option `-p`, Ví dụ cổng 2222 ta sử dụng lệnh:
`ssh -p 2222 hello@192.168.181.132`
### 3.2, File cấu hình SSH Client
* ssh (ssh client) khi chạy, thực hiện các kết nối - nó sẽ tìm file cấu hình tại đường dẫn `~/.ssh/config`, nếu có file này nó dùng file đó thiết lập các thông tin bổ sung kết nối.
* Trong đường dẫn file trên, `~` cho biết đó là thư mục của User hiện tại, như vậy mỗi user của máy có thể có file config riêng.
* **NOTE**: Có thư mục `.ssh` rồi mới tạo file `config` trong đó.
![image](https://user-images.githubusercontent.com/88284121/206091513-e2e0e4b5-e4f3-4486-af57-ef2bfb7da18d.png)
* Ngoài `Port User HostName` tham khảo một số cấu hình nữa như:
  - `PreferredAuthentications publickey` : bật chế độ xác thực bằng SSH Key trước.
  - `IdentityFile "path/../file_private_key` : vị trí file Private key.
### 3.3, Tạo SSH Key và xác thực kết nối SSH bằng Public/Private key
* Ngoài cơ chế xác thức bằng cách nhập mật khẩu như trên còn có cơ chế sử dụng SSH Key để xác thực. Để tạo nên xác thực này cần có hai file, 1 file lưu **Private Key** và 1 lưu **Public key**:
  - **Public Key** khóa chung, là một file **text** - nó lại lưu ở phía **Server SSH**, nó dùng để khi **Client** gửi **Private Key** (file lưu ở Client) lên để xác thực thì **kiểm tra phù hợp** giữa **Private Key** và **Public Key** này. Nếu phù hợp thì cho kết nối.
  - **Private Key** khóa riêng, là một file **text** bên trong nó chứa **mã riêng** để xác thực (xác thực là kiểm tra sự phù hợp của Private Key và Public Key). Client kết nối với Server phải **chỉ ra** file này khi kết nối SSH **thay vì** nhập mật khẩu. **Hãy lưu file Private key cận thận**, bất kỳ ai có file này có thể thực hiện kết nối đến máy chủ của bạn.
