# JMS
**Java Message Service (JMS)** API là một phần của kỹ thuật Java Enterprice Edition (JEE). JMS là tất cả những gì thuộc về việc gửi và nhận tin giữa hai hay nhiều client.- Nó là một đặc điểm kỹ thuật mô tả một phương thức tạo bởi trương trình Java cho việc tạo, gửi và nhận tin nhắn.- JMS API cho phép lới lỏng việc liên kết thông tin, và gửi tin một cách bất đồng bộ.

Có hai mô hình nhắn tin là PTP và Pub/Sub
* Ở sơ đồ điểm – điểm (PTP) có ba thành phần chính là ứng dụng gửi, Queue, ứng dụng nhận tin. Mỗi tin nhắn được gửi đến một client cụ thể. Queue giữ lại các tin nhắn cho đến khi client nhận hết hoặc đến thời gian timout thiết lập.
![ptp](https://viblo.asia/uploads/c008fa46-5f21-42fc-9509-57c70889902c.png)
* Ở sơ đồ Pub/Sub trên cũng có ba thành phần chính là phía gửi, Topic, và phía nhận.Mỗi tin nhắn có thể được nhận bởi nhiều client. Topic sẽ lưu lại toàn bộ tin nhắn mà không bị mất đi cho đến khi MOM được reset, hay xóa.
![pub/sub](https://viblo.asia/uploads/a6efb6f4-6f31-4a47-bdef-fc78850066c8.png)
  