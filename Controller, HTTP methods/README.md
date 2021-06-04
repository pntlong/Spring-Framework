# 1. Controller
Các Controller thường được đánh dấy với annotation @Controller. @Controller sẽ được sử dụng với @RequestMapping trên các phương thức để xử lý các request
```
@Controller
public class WebController {
    @GetMapping(value={"/","/home"})
    public String homePage(){
        return "home";
    }
    @GetMapping("/welcome")
    public String welcomePage(){
        return "welcome";
    }
}
```
![homePage](Screen%20Shot%202021-06-03%20at%2010.14.26.png)

# 2. HTTP methods
**HTTP** viết tắt của từ Hypertext Transfer Protocol được thiết kế để cho phép giao tiếp giữa client và server. Là công nghệ được sử dụng để truyền gửi files, đồ họa hoặc văn bản trên internet và về cơ bản là nền tảng của trao đổi dữ liệu cho World Wide Web.HTTP hoạt động như là một giao thức request-response giữa client và server
* **GET** được sử dụng để lấy lại thông tin từ Server đã cung cấp bởi sử dụng một URI đã cung cấp. Các yêu cầu sử dụng GET nên chỉ nhận dữ liệu và nên không có ảnh hưởng gì tới dữ liệu.
* **POST** được sử dụng để gửi dữ liệu tới Server, ví dụ, thông tin khách hàng, file tải lên, …, bởi sử dụng các mẫu HTML.
* **PUT** Thay đổi tất cả các đại diện hiện tại của nguồn mục tiêu với nội dung được tải lên.
* **DELETE** Gỡ bỏ tất cả các đại diện hiện tại của nguồn mục tiêu bởi URI.