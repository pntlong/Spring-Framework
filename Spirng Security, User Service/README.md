# 1. Spring Security và User Service
**Spring Security** Là một feature quan trọng của Spring Framework, nó giúp phân quyền và xác thực người dùng trước khi cho phép người dùng truy cập vào tài nguyên

**Các thành phần của Spring Security**

* **SecurityContext** là interface cốt lõi của Spring Security, lưu trữ tất cả các chi tiết liên quan đến bảo mật trong ứng dụng. Khi Spring Security được kích hoạt trong ứng dụng thì SecurityContext cũng sẽ được kích hoạt theo.
* **SecurityContextHolder**: Class này lưu trữ Spring context của hiện tại của ứng dụng, bao gồm principal đang tương tác với ứng dụng. Spring security sẽ dùng 1 đối tượng authentication để biểu diễn thông tin này.
* **UserDetails** là một interface cốt lõi của Spring Security. Nó đại diện cho một principal nhưng theo một cách mở rộng và cụ thể hơn. UserDetails bao gồm các method:
  * getAuthorities(): trả về danh sách các quyền của người dùng
  * getPassword(): trả về password đã dùng trong qúa trình xác thực
  * getUsername(): trả về username đã dùng trong qúa trình xác thực
  * isAccountNonExpired(): trả về true nếu tài khoản của người dùng chưa hết hạn
  * isAccountNonLocked(): trả về true nếu người dùng chưa bị khóa
  * isCredentialsNonExpired(): trả về true nếu chứng thực (mật khẩu) của người dùng chưa hết hạn
  * isEnabled(): trả về true nếu người dùng đã được kích hoạt

* **UserDetailsService** Là một interface có duy nhất một phương thức: loadUserByUsername. Phương thức này trả về UserDetails
* **GrantedAuthority** là một quyền được ban cho principal. Các quyền đều có tiền tố là ROLE_, ví dụ: ROLE_ADMIN, ROLE_MEMBER ...

```
@Override
protected void configure(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/","/home").permitAll()
                .antMatchers("/api/student/*").hasRole("ADMIN").anyRequest().authenticated()
                .and()
                .formLogin()
                .and()
                .logout();
    }
```

<!-- ```
@RestController
@RequestMapping("/api/manager")
public class StudentMgmtController {
    @GetMapping("/admin")
    @PreAuthorize("hasAnyRole('ADMIN')")
    public String getAdminPage(){
        return "Welcome ADMIN";
    }

    @GetMapping("/user")
    @PreAuthorize("hasAnyRole('USER')")
    public String getUserPage(){
        return "Welcome USER";
    }
}
``` -->
  
  # 2. JSON Web Tokens (JWT)

  **JWT** gồm 3 phần

**Header**: thường gồm 2 phần là loại token và thuật toán mã hóa. 
**Payload**: chứa các claims (thông tin) như username, issuer… 
**Signature**: chữ ký số. 

  ![JWT](https://viblo.asia/uploads/0cb529a7-8db9-424e-a994-e3ef28b16380.png)

1. User thực hiện login bằng cách gửi id/password hay sử dụng các tài khoản mạng xã hội lên phía Authentication Server.
2. Authentication Server tiếp nhận các dữ liệu mà User gửi lên để phục vụ cho việc xác thực người dùng. Trong trường hợp thành công, Authentication Server sẽ tạo một JWT và trả về cho người dùng thông qua response.
3. Người dùng nhận được JWT do Authentication Server vừa mới trả về làm "chìa khóa" để thực hiện các "lệnh" tiếp theo đối với Application Server.
4. Application Server trước khi thực hiện lệnh được gọi từ phía User, sẽ verify JWT gửi lên. Nếu OK, tiếp tục thực hiện lệnh được gọi.

```
@Override
protected void successfulAuthentication(HttpServletRequest request,
                                            HttpServletResponse response,
                                            FilterChain chain, Authentication authResult) throws IOException, ServletException {
        String key = "securesecuresecuresecuresecure";

        String token = Jwts.builder()
                .setSubject(authResult.getName())
                .claim("authorities", authResult.getAuthorities())
                .setIssuedAt(new Date())
                .setExpiration(java.sql.Date.valueOf(LocalDate.now().plusWeeks(2)))
                .signWith(Keys.hmacShaKeyFor(key.getBytes()))
                .compact();

        response.addHeader("Authorization", "Bearer" + token);
    }
```