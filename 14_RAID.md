# RAID
## 1, RAID là gì?
* **RAID** - *Redundant Arrays of Inexpensive* hoặc *Redundant Arrays of Independent Disk* - là hình thức ghép nhiều ổ đĩa cứng vật lí thành một ổ đĩa cứng có chức năng gia tăng tốc độ đọc/ghi dữ liệu hoặc làm tăng thêm sự an toàn dữ liệu chứa trên hệ thông đĩa hoặc kết hợp cả 2 yếu tố trên.
* **RAID** được chia thành 7 cấp độ, mỗi cấp độ có các tính năng riêng, hầu hết chúng được xây dựng từ 2 cấp độ cơ bản là RAID 0 hoặc RAID 1.
## 2, Các loại RAID phổ biến
### 2.1, RAID 0
```
- RAID 0 cần ít nhất 2 ổ đĩa (vẫn có thể sử dụng 1 ổ đĩa). Tổng quát ta có n đĩa (n >= 2) và các đĩa là cùng loại.
- Dữ liệu sẽ được chia ra nhiều phần bằng nhau. Ví dụ ta dùng 02 ổ cứng 80GB thì hệ thống đĩa của chúng ta là 160GB.
```
* ![image](https://user-images.githubusercontent.com/88284121/198221133-b27bab09-6270-4132-a371-7468bd5facfe.png)
* **Ưu điểm**: Tăng tốc độ đọc/ghi đĩa: mỗi đĩa chỉ cần phải đọc/ghi `1/n` lượng dữ liệu được yêu cầu. Lý thuyết thì tốc độ sẽ tăng n lần.
* **Nhước điểm**: Tính an toàn thấp. Nếu một đĩa bị hư thì tất cả dữ liệu trên các đĩa sẽ còn lại sẽ không sử dụng được nữa. Xác suất để mất dữ liệu sẽ tăng n lần so với dùng ổ đĩa đơn.
### 2.2, RAID 1
```
- Đây là dạng RAID cơ bản nhất có khả năng đảm bảo an toàn dữ liệu. Cũng giống như RAID 0, RAID 1 đòi hỏi ít nhất hai đĩa cứng để làm việc.
- Dữ liệu được ghi vào 2 ổ giống hệt nhau (Mirroring). Trong trường hợp một ổ bị trục trặc, ổ còn lại sẽ tiếp tục hoạt động bình thường.
```
* ![image](https://user-images.githubusercontent.com/88284121/198221252-5e41b9a1-ed2d-4d39-8e6b-1502c2301c2f.png)
* **Ưu điểm**: Tính an toàn dữ liệu cao. Người dùng có thể thay ổ đĩa hỏng mà không cần lo lắng vấn đề thông tin bị thất lạc.
* **Nhược điểm**: Tốc độ chỉ = 1 ổ đĩa, do đó không phù hợp với người dùng có nhu cầu về tốc độ.
### 2.3, RAID 5
```
- Yêu cầu tối thiểu của RAID 5 là có ít nhất 3 ổ đĩa cứng. RAID 5 cũng yêu cầu các ổ cứng tham gia RAID phải có dung lượng bằng nhau.
- RAID 5 là sự cải tiến của RAID 0,có cung cấp cơ chế khôi phục dữ liệu, các Parity dùng để khôi phục dữ liệu được phân bố đồng đều trên tất cả các ổ đĩa cứng.
- Các Parity được lưu trữ tuần tự trên các ổ đĩa cứng. RAID 5 cho phép tối đa có 1 ổ cứng bị chết tại một thời điểm, nếu có nhiều hơn 1 ổ cứng bị chết tại một thời điểm thì toàn bộ dữ liệu coi như mất hết. 
```
* ![image](https://user-images.githubusercontent.com/88284121/198221790-4fa7d07f-3768-4f98-b710-b4867a66a3f8.png)
* Ví dụ:
  - Giả sử dữ liệu A được phân tách thành 3 phần A1, A2, A3 (Xem hình minh hoạ RAID 5), khi đó dữ liệu được chia thành 3 phần chứa trên các ổ đĩa cứng 0, 1, 2 (giống như RAID 0). Phần ổ đĩa cứng thứ 3 chứa Parity (Ap) của A1 A2 A3 để khôi phục dữ liệu có thể sẽ mất ở ổ đĩa cứng 0, 1, 2.
  - Dữ liệu B được chia thành B1 B2 B3 và Parity của nó là Bp, theo thứ tự B1 B2 B3 được lưu trữ tại ổ 0 1 3, và Bp được lưu trữ tại ổ 2.
### 2.4, Tham khảo thêm
* https://hostingviet.vn/cong-nghe-raid-raid-0-raid-1-raid-5-raid-10
## 3, Sử dụng lệnh `mdadm` để quản lí RAID trong Linux

