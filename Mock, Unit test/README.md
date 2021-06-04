# 1. Mock
**Mock Object** (MO) là một đối tượng ảo, mô phỏng các tính chất và hành vi giống hệt như đối tượng thực. Được truyền vào bên trong khối, mã để kiểm tra tính đúng đắn của các hoạt động bên trong.
* Đơn giản hơn đối tượng thực nhưng vẫn giữ được sự tương tác với các đối tượng khác.
* Không lặp lại nội dung đối tượng thực.
* Cho phép thiết lập các trạng thái riêng trợ giúp cho việc thực hiện unit test.

**Các trường hợp sử dụng**
* Đối tượng thật có những hành vi không đoán trước được.
* Đối tượng thật khó cài đặt.
* Đối tượng thật chậm.
* Đối tượng thật có / là giao diện người dùng.
* Đối tượng thật không tồn tại.

# 2. Unit Test
**Unit test** là một loại kiểm thử phần mềm trong đó các đơn vị hay thành phần riêng lẻ của phần mềm được kiểm thử

* Được thực hiện trong quá trình phát triển ứng dụng.

* Cô lập một phần code và xác minh tính chính xác của đơn vị đó

* Một unit bao gồm: function, procedure, class, method

**Các trường hợp sử dụng**
* Tạo môi trường để kiểm tra bất kỳ đoạn code nào.
* Phát hiện thuật toán thực thi không hiệu quả
* Phát hiện vấn đề thiết kế, xử lý hệ thống..
* Phát hiện các lỗi nghiêm trọng có thể xảy ra trong những tình huống hẹp

# 3. JUnit
**Unit** là một framework đơn giản dùng cho việc tạo unit test tự động, và chạy cấc test có thể lặp đi lặp lại.

Junit là một chuẩn trên thực tế cho unit test trong Java.

**Đặc điểm**
* Xác nhận(assert) việc kiểm tra kết quả được mong đợi.
* Các Test Suite cho phép chúng ta dễ dàng tổ chức và chạy các test.


