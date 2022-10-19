# Processing Text

`cat` : dùng để tạo, chèn, hiển thị và ghép nội dung của file.

* ![image](https://user-images.githubusercontent.com/88284121/196585302-bc90ebfa-a9b1-4f89-a5df-463498fa9471.png)


`join` : dùng để ghép nối từng dòng trong 2 files đầu vào (theo thứ tự nhập) mà có cùng một field giống nhau. Nếu một trong hai files đầu vào (không được cả hai) là dấu ‘–‘, lệnh sẽ đọc thông tin do người dùng nhập vào từ bàn phím (standard input).

* ![image](https://user-images.githubusercontent.com/88284121/196591145-6f2e6d1b-9596-4469-a5cc-000f0ffbd56a.png)
* ![image](https://user-images.githubusercontent.com/88284121/196592856-6eb3fc6e-4f33-4ba9-97d6-5ca79a26beb8.png)
* ![image](https://user-images.githubusercontent.com/88284121/196592878-da2c3d7b-a9d8-476d-8ed8-47b686e9582b.png)
* ![image](https://user-images.githubusercontent.com/88284121/196592903-5ae3a833-ad0b-4044-b7be-6a49deb87883.png)
* ![image](https://user-images.githubusercontent.com/88284121/196592959-39ccd67f-95d6-4ee4-ac68-37735d4ced96.png)

`paste` : dùng để hợp nhất các dòng của nhiều file.

* ![image](https://user-images.githubusercontent.com/88284121/196595415-e67e0eaf-057d-42aa-a0cd-77149fa40dfe.png)

`tac` : giống như `cat` nhưng đọc file từ dưới lên.

`sort` : Dùng để sắp xếp các dòng dữ liệu bản văn trong file.

* ![image](https://user-images.githubusercontent.com/88284121/196593422-2dbeea77-6206-4bcc-baa6-aae675646c74.png)

`split` : dùng để chia (hoặc tách) một tệp thành các phân đoạn có kích thước bằng nhau để xem và thao tác dễ dàng hơn và thường chỉ được sử dụng trên các tệp tương đối lớn.

`uniq` : dùng để gỡ bỏ các dòng trống và kề nhau trong văn bản.

* ![image](https://user-images.githubusercontent.com/88284121/196600356-8f65c055-5c6b-4d53-8336-e8aa66cd935b.png)
* ![image](https://user-images.githubusercontent.com/88284121/196600397-1f907c65-40f8-4f32-88e1-c4884c07ca39.png)
* ![image](https://user-images.githubusercontent.com/88284121/196600450-9eb98e30-57d1-487e-a5b2-e65ca865f6ef.png)

`nl` : dùng để đánh số dòng trong file (= `cat -n`)

* ![image](https://user-images.githubusercontent.com/88284121/196586428-90998c9a-f134-4a5e-84d7-42f99f5184a5.png)

`grep` : dùng để hiện thị những dòng có một phần nội dung nào đó. (giống searching)

* ![image](https://user-images.githubusercontent.com/88284121/196588156-29208b94-45c9-4d3a-a4be-f02060286065.png)

`sed` : read, execute, display.

* ![image](https://user-images.githubusercontent.com/88284121/196597508-fa5cdcdf-65db-44ce-b137-d51d3c3c8725.png)
* ![image](https://user-images.githubusercontent.com/88284121/196598009-5b8e9023-be12-4c66-9d49-0841ed930b5d.png)

`awk` : dùng để xử lí văn bản, tạo báo cáo văn bản được định dạng, thực hiện phép toán số học, tìm kiếm text trong file.

# File-Viewing Commands
`head` : dùng để lấy phần đầu của file văn bản.

* ![image](https://user-images.githubusercontent.com/88284121/196588862-d1fc3ce6-51c9-4a76-a38c-4a73c8ae2725.png)

`tail` : dùng để lấy phần cuối của file văn bản.

* ![image](https://user-images.githubusercontent.com/88284121/196588953-65170f4b-b8e5-454d-afa1-0436be302d8f.png)

`less` : xem file có tương tác ( áp dụng với file lớn ).

`cut` : dùng để cắt các phần của dòng từ các tệp hoặc dữ liệu được chỉ định và in kết quả ra đầu ra tiêu chuẩn.

`wc` : (countword) dùng để đếm số dòng, số từ (cách nhau bằng khoảng trắng) và số kí tự có trong file.

* ![image](https://user-images.githubusercontent.com/88284121/196586873-f090ad4a-c895-408a-a259-dffc2c9d1d91.png)
