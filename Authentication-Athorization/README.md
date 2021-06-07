# 1. Authentication 
**Authentication** là về việc xác thực thông tin đăng nhập của người dùng như Tên người dùng / ID người dùng và mật khẩu để xác minh danh tính của người dùng. Trong các public và private network, hệ thống xác thực danh tính người dùng thông qua mật khẩu đăng nhập.
# 2. Authorization
**Authorization** là quá trình để xác định xem người dùng được xác thực có quyền truy cập vào các tài nguyên cụ thể hay không. Nó xác minh quyền của người dùng để cấp cho người dùng quyền truy cập vào các tài nguyên như thông tin, cơ sở dữ liệu, file,... Authorization thường được đưa ra sau khi xác thực xác nhận các đặc quyền của người dùng để thực hiện.
# 3. Authentication vs Athorization
|**Authentication**|**Authorization**|
|------------------|-----------------|
|Authentication xác nhận danh tính của bạn để cấp quyền truy cập vào hệ thống |Authorization xác định xem bạn có được phép truy cập tài nguyên không.
|Đây là quá trình xác nhận thông tin đăng nhập để có quyền truy cập của người dùng.|Đó là quá trình xác minh xem có cho phép truy cập hay không. 
|Nó quyết định liệu người dùng có phải là những gì anh ta tuyên bố hay không.| Nó xác định những gì người dùng có thể và không thể truy cập. 
| Authentication thường yêu cầu tên người dùng và mật khẩu. | Các yếu tố xác thực cần thiết để authorization có thể khác nhau, tùy thuộc vào mức độ bảo mật. 
| Authentication là bước đầu tiên của authorization vì vậy luôn luôn đến trước. | Authorization được thực hiện sau khi authentication thành công.   