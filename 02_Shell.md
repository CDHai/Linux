# SHELL
## 1, Shell là gì?
* **Shell** là một chương trình cung cấp giao diện giao tiếp giữa người dùng và hệ điều hành (OS). Hệ điều hành khởi động một shell cho mỗi người dùng khi người dùng đăng nhập hoặc mở một cửa sổ terminal hoặc console.
## 2, Các loại Shell trong Linux
Trên Linux, shell mặc định được cài sẵn là Bash Shell, nhưng không chỉ có duy nhất một loại shell mà có thể lựa chọn đa dạng các loại shells khác nhau, tùy theo nhu cầu, thói quen sử dụng.
* Câu lệnh kiểm tra shell đang dùng:
> echo $0
* Câu lệnh kiểm tra các shell đang có trên hệ thống: 
> cat /etc/shells

> eg ![image](https://user-images.githubusercontent.com/88284121/196130637-5a58aa67-691f-4462-bd33-e0a1716d1c55.png)
### 2.1, Bournce Shell (sh)
* Đây là 1 Shell được viết nên bởi Steve Bourne ở AT&T Bell Labs và cũng là UNIX shell đầu tiên, hiện tại là shell thích hợp nhất dùng cho lập trình Shell. Bourne Shell đang là một shell mặc định thuộc Solaris OS và đồng thời cũng là shell tiêu chuẩn cho những script về quản trị hệ thống Solaris.
* Ưu điểm: tốc độ, tính nhỏ gọn.
* Nhược điểm: thiếu những tính năng tương tác.
* Các lệnh trong Bournce Shell:
> "$" là lời nhắc mặc định dành cho non-root user

> "#" là lời nhắc mặc định dành cho root user

> /sbin/sh và /bin/sh là lệnh gọi tên của đường dẫn đầy đủ
### 2.2, C-Shell (csh)
* Đây là 1 phần cải tiến UNIX đã được viết nên bởi Bill Joy của Đại học California Berkeley.
* Giúp hỗ trợ những tính năng lập trình vô cùng tiện lợi, ví dụ như số học tích hợp cũng như cú pháp về biểu thức C-like. Có những tính năng kết hợp để có thể sử dụng tương tác, ví dụ như lịch sử lệnh và bí danh.
* Những lệnh trong C-Shell:
> /bin/csh chính là lệnh tên của đường dẫn đầy đủ

> Tên máy chủ "%" là dấu nhắc mặc định dành cho non-root user

> Tên máy chủ "#" là dấu nhắc mặc định dành cho root user
### 2.3, Korn Shell (ksh)
* Korn Shell là 1 superset của Bourne Shell.
* Korn Shell có những tính năng tương tác và tương đương với những tính năng có trong C shell. Nhanh hơn C-Shell.
* Hiện tại nó gồm có những tính năng lập trình vô cùng tiện lợi như những hàm C-like và những hàm số học, cùng những phương thức thao tác chuỗi. Chạy những script và được viết cho Bourne shell.
* Những lệnh có trong Korn Shell:
> /bin/ksh là lệnh đầy đủ của tên đường dẫn

> "$" là dấu mặc định dành cho non-root user

> "#" là dấu nhắc mặc định cho root user
### 2.4, GNU Bourne-Again Shell (bash)
* Tương thích với Bourne shell.
* Có những phím mũi tên và cho phép map tự động để chỉnh sửa và recall lệnh.
* Kết hợp những tính năng hữu ích từ C Shell và Korn.
* Cách lệnh của GNU Bourne-Again Shell:
> Dấu nhắc mặc định dành cho non-root user hiện tại là: bash-x.xx$. (x.xx sẽ cho biết được số phiên bản của shell là gì)

> Dấu nhắc mặc định dành cho root user hiện tại là: bash-x.xx #. (x.xx sẽ cho biết được số phiên bản của shell là gì)

> Lệnh của tên đường dẫn đầy đủ gồm có /bin/bash
## 3, Shell Script
* Thay vì phải thực thi nhiều câu lệnh phức tạp, mất thời gian, chúng ta có thể viết vào một file để thực thi nó, chúng ta gọi đó là **Shell Script****.
## Ví dụ với Bash Script:

* file: nano example.sh
* Code :
>#!/bin/bash

> echo "Printing text with newline"

> echo -n "Printing text without newline"

> echo -e "\nRemoving \t backslash \t characters\n"
* Thực thi: bash example.sh
> ![image](https://user-images.githubusercontent.com/88284121/196148828-f42bc7b8-ec00-40e1-bcec-2049f1c14e2f.png)
