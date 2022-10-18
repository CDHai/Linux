# Streams + Redirect + Pipe + Filter
## 1, Stream
* Mọi chương trình trên command line đều bao gồm 3 loại **Data Stream**:

1. `STDIN(0)` - Standard Input (Dữ liệu đầu vào):
 
```
Luồng đầu vào tiêu chuẩn thường mang dữ liệu từ user đến một chương trình. Các chương trình mong đợi đầu vào tiêu chuẩn thường nhận đầu vào từ một thiết bị, chẳng hạn như bàn phím. Đầu vào tiêu chuẩn được kết thúc bằng cách đạt đến EOF (cuối file ). Như được mô tả bởi tên của nó, EOF cho biết không có thêm dữ liệu nào để đọc.
```

2. `STDOUT(1)` - Standard Output (Dữ liệu đầu ra):

```
Đầu ra chuẩn ghi dữ liệu được tạo bởi một chương trình. Khi stream kết quả tiêu chuẩn không được chuyển hướng, nó sẽ xuất văn bản tới terminal.
```

3. `STDERR(2)` - Standard Error (Dữ liệu lỗi đầu ra):

```
Lỗi chuẩn ghi các lỗi được tạo ra bởi một chương trình bị lỗi tại một thời điểm nào đó trong quá trình thực thi. Giống như kết quả tiêu chuẩn, đích mặc định cho stream này là màn hình terminal. Khi stream lỗi tiêu chuẩn của một chương trình được chuyển đến chương trình thứ hai, dữ liệu được tổng hợp (bao gồm các lỗi chương trình) cũng được gửi đồng thời đến terminal.
```

## 2, Redirection
* Redirection dùng để điều hướng luồng dữ liệu (data stream) giữa 1 chương trình và 1 file (khác với pipe là 2 chương trình). Nếu một file không tồn tại được nhắm đến (bằng lệnh ngoặc đơn hoặc ngoặc kép), một file mới có tên đó sẽ được tạo trước khi ghi.
* Cụ thể như sau:
 
`<` : đầu vào chuẩn (ghi đè)

`<<` : đầu vào chuẩn (nối)

`>` : đầu ra chuẩn (ghi đè)

`>>` : đầu ra chuẩn (nối)

`2>` : Lỗi tiêu chuẩn (ghi đè) - **Cần descriptor kèm theo**

`2>>` : Lỗi tiêu chuẩn (nối) - **Cần descriptor kèm theo**

**Ví dụ**:
```
cat <test.txt >testcopy.txt
```
* Lệnh này có tác dụng: đọc file test.txt, nội dung đọc được ghi đè lên file testcopy.txt
* Ta có output như sau:

![image](https://user-images.githubusercontent.com/88284121/196395315-e6e8c2dd-a2b1-4438-925d-a4fedcc493aa.png)


## 3, Pipe
* Pipe thực tế có nghĩa là cái ống, là công cụ để cho dòng chảy đi qua. Trong Linux, Pipe có kí hiệu là dấu "|" và nó có tác chuyện chuyển dòng chảy dữ liệu (data stream) từ output của chương trình này sang input của chương trình ở sau nó.
```
A | B - Output (STDOUT) của chương trình A sẽ thành input (STDIN) của chương trình B
```
**Ví dụ**:
```
cat testcopy.txt | grep 2
```
* Lệnh này có tác dụng: Đọc file testcopy.txt và lọc ra thành phần có kí tự '2'
* Ta có output như sau:

![image](https://user-images.githubusercontent.com/88284121/196396880-03c0f72f-1d8b-4017-8ec1-9ae985dfd7bb.png)
## 4, Filter
* Filter trong giới hạn command line là một chương trình có nhiệm vụ nhận dữ liệu đầu vào (STDIN), xử lý và xuất ra kết quả (STDOUT). Kỹ thuật này được sử dụng nhằm lọc, xử lý dữ liệu đầu vào và ghi ra kết quả.
* Một số loại Filter hay được sử dụng:

`head`: in ra n dòng dữ liệu đầu tiên.

`tail`: in ra n dòng dữ liệu từ dưới lên.

`sort`: sắp xếp dữ liệu.

`nl`: hiển thị dòng dữ liệu kèm số thứ tự dòng.

`wc`: đếm kí tự từ, dòng, byte.

`cut`: cắt dữ liệu.

`sed`: tìm kiếm và thay thế dữ liệu.

`uniq`: bỏ dòng trùng lặp.

`tac`: hiển thị dữ liệu từ dưới lên, ngược lại so với cat.

`awk`: tìm kiếm và xử lí file text.

**Ví dụ**:
```
sort <test.txt >testcopy.txt
```

* Câu lệnh này có tác dụng: đọc dữ liệu trong file test.txt, sắp xếp rồi truyền dữ liệu vào file testcopy.txt.
* Ta có output như sau:

![image](https://user-images.githubusercontent.com/88284121/196401240-da0db9bf-d8b1-43b5-a878-f20c96238deb.png)
