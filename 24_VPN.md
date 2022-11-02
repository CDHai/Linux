# VPN
## 1, VPN là gì?
* **VPN** - *Virtual Private Network*: hay còn gọi là mạng riêng ảo, mạng ảo. Đây là một công nghệ mạng giúp tạo nên những kết nối mạng an toàn khi tham gia mạng riêng của nhà cung cấp dịch vụ hoặc mạng công cộng Internet, Intranet.
* Về căn bản, mỗi VPN là một mạng riêng rẽ sử dụng một mạng chung (thường là Internet) để kết nối cùng với các site (mạng riêng lẻ) hay nhiều người sử dụng từ xa. Thay cho việc sử dụng kết nối thực chuyên dùng như đường leased-line, mỗi VPN sử dụng các kết nối ảo được dẫn qua đường Internet từ mạng riêng của các công ty tới các site các nhân viên từ xa. 
## 2, Các mô hình mạng riêng ảo VPN
Mạng VPN ra đời nhằm đáp ứng các tiêu chí cơ bản như:
  - Nhân viên có thể truy cập vào mạng nội bộ ở mọi lúc, mọi nơi.
  - Giúp nối liền các chi nhánh, văn phòng di động.
  - Điều khiển quyền truy cập của khách hàng, nhà cung cấp dịch vụ hay bất kể đối tượng bên ngoài nào.
Từ đó, mạng riêng ảo VPN được phân chia thành 3 loại chính như sau:
1. Mạng VPN cục bộ (intranet VPN).
2. Mạng VPN mở rộng (extranet VPN).
3. Mạng VPN truy cập từ xa (Remote Access VPN).
### 2.1, Mạng VPN cục bộ (intranet VPN)
* Các VPN cục bộ được sử dụng để bảo mật các kết nối giữa các địa điểm khác nhau của một công ty. Mạng VPN liên kết trụ sở chính, các văn phòng, chi nhánh trên một cơ sở hạ tầng chung sử dụng các kết nối luôn được mã hóa bảo mật. Điều này cho phép tất cả các địa điểm có thể truy nhập an toàn các nguồn dữ liệu được phép trong toàn bộ mạng của công ty.
* Những VPN này vẫn cung cấp những đặc tính của mạng WAN như khả năng mở rộng, tính tin cậy và hỗ trợ cho nhiều kiểu giao thức khác nhau với chi phí thấp nhưng vẫn đảm bảo tính mềm dảo. Kiểu VPN này thường được cấu hình như một VPN site-to-Site.
* ![image](https://user-images.githubusercontent.com/88284121/199391421-8a822eda-17f4-4a32-851e-03d0379ef812.png)
* **Ưu điểm**:
  - Các mạng lưới cục bộ hay toàn bộ có thể được thiết lập (với điều kiện mạng thông qua một hay nhiều nhà cung cấp dịch vụ).
  - Giảm được số nhân viên kỹ thuật hỗ trợ trên mạng đối với những nơi xa.
  - Bởi vì những kết nối trung gian được thực hiện thông qua mạng Internet, nên nó có thể dễ dàng thiết lập thêm một liên kết ngang cấp mới.
  - Tiết kiệm chi phí thu được từ những lợi ích đạt được bằng cách sử dụng đường ngầm VPN thông qua Internet kết hợp với công nghệ chuyển mạch tốc độ cao (Frame Relay, ATM,...)
* **Nhược điểm**:
  - Bởi vì dữ liệu được truyền "ngầm" qua mạng công cộng - mạng Internet - cho nên vẫn còn những mối "đe dọa" về mức độ bảo mật dữ liệu và mức độ chất lượng dịch vụ (QoS).
  - Khả năng các gói dữ liệu bị mất trong khi truyền dẫn vẫn còn khá cao.
  - Trường hợp truyền dẫn khối lượng lớn dữ liệu, như là đa phương tiện, với yêu cầu truyền dẫn tốc độ cao và đảm bảo thời gian thực là thách thức lớn trong môi trường Internet.
### 2.2, Mạng VPN mở rộng (extranet VPN)
* Khác với 2 mô hình còn lại, mạng VPN mở rộng không bị cô lập với "thế giới bên ngoài". Các VPN mở rộng cung cấp một đường hầm bảo mật giữa các khách hàng, các nhà cung cấp và các đối tác qua một cơ sở hạ tầng công cộng. Kiểu VPN này sử dụng các kết nối luôn luôn được bảo mật và được cấu hình như một VPN Site-to-Site. Sự khác nhau giữa một VPN cục bộ và một VPN mở rộng đó là sự truy cập mạng được công nhận ở một trong hai đầu cuối của VPN.
* ![image](https://user-images.githubusercontent.com/88284121/199393107-ca8e3e7a-e048-42dd-b8e7-7d4f5e41f425.png)
* **Ưu điểm**:
  - Chi phí cho mạng VPN mở rộng thấp hơn rất nhiều so với mạng truyền thống.
  - Dễ dàng thiết lập, bảo trì và dễ dàng thay đổi đối với mạng đang hoạt động.
  - Vì mạng VPN mở rộng được xây dựng dựa trên mạng Internet nên có nhiều có hội trong việc cung cấp dịch vụ và chọn lựa giải pháp phù hợp với các nhu cầu của mỗi công ty hơn.
  - Bởi vì các kết nối Internet được nhà cung cấp dịch vụ Internet bảo trì, nên giảm được số lượng nhân viên kĩ thuật hỗ trợ mạng, do vậy giảm được chi phí vận hành của mạng. 
* **Nhược điểm**:
  - Khả năng bảo mật thông tin, mất dữ liệu trong khi truyền qua mạng công cộng vẫn tồn tại.
  - Truyền dẫn khối lượng lớn dữ liệu, như là đa phương tiện, với yêu cầu truyền dẫn tốc độ cao và đảm bảo thời gian thực là thách thức lớn trong môi trường Internet.
  - Làm tăng khả năng rủi ro đối với các mạng cục bộ của công ty.
### 2.3, Mạng VPN truy cập từ xa (Remote Access VPN)
* Đây là kiểu VPN điển hình nhất bởi những VPN này có thể thiết lập bất kì thời điểm nào, từ bất cứ nơi nào có mạng Internet.
* ![image](https://user-images.githubusercontent.com/88284121/199388867-1236afa8-7b06-4ba2-b1c0-32d04e154d46.png)
* **Ưu điểm**:
  - Mạng VPN truy cập từ xa không cần sự hỗ trợ của nhân viên mạng vì quá trình kết nối từ xa đã được các ISP thực hiện.
  - Giảm các chi phí cho kết nối từ khoảng cách xa bởi vì các kết nối khoảng cách xa được thay thế bởi các mạng cục bộ thông qua Internet.
  - Cung cấp dịch vụ kết nối giá rẻ cho những người sử dụng từ xa.
  - Bởi vì các kết nối truy nhập là nội bộ nên các Modem kết nối hoạt động ở tốc độ cao hơn so với các truy nhập từ khoảng cách xa.
  - VPN cung cấp khả năng truy nhập tốt hơn đến các site của công ty bởi vì chúng hỗ trợ mức thấp nhất của dịch vụ kết nối.
* **Nhược điểm**:
  - Mạng VPN truy nhập từ xa không hỗ trợ các dịch vụ đảm bảo QoS.
  - Nguy cơ bị mất dữ liệu cao. Hơn nữa, nguy cơ các gói có thể bị phân tán không đến nơi hoặc mất gói.
  - Bởi vì thuật toán mã hóa phức tạp, nên tiêu đề giao thức tăng một cách đáng kể.

`THAM KHẢO THÊM Ở FILE`: [Chng_1_Tng_Quan_V_VPN.pdf](https://github.com/CDHai/Linux/files/9915897/Chng_1_Tng_Quan_V_VPN.pdf)
