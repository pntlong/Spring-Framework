# Spring property vs Spring config
Là một tiện ích cho phép cấu hình ứng dụng từ bên ngoài và lấy các thông tin đó ra một cách dễ dàng

``@PropertySource`` Để định nghĩa tên của file config. Nếu không có annotation này Spring sẽ sử dụng file mặc định *(classpath:application.yml trong thư mục resources)*

``@ConfigurationProperties`` Đánh dấu class bên dưới nó là properties, các thuộc tính sẽ được tự động nạp vào khi Spring khởi tạo.

``@Configuration``: Là 1 Annotation đánh dấu trên 1 class cho phép Spring Boot biết được dây là nơi định nghĩa ra các Bean 

``@Value`` Để inject giá trị của property vào giá trị của thuộng tính

> file properties
```
server.port=8080

spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.initialization-mode=always
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgresql
spring.datasource.password=1234
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
```

>Class properties
```
@Component
@PropertySource("classpath: test.properties")
public class TestConfig{
    @Value(${name})
    priate String name;
    ...
}
```



