# 1. Bean life cycle
Spring boot từ khi chạy đến khi shutdown thì các **bean** nó quản lý sẽ có một vòng đời

![bean life cycle](https://loda.me/assets/static/2.2b6d00f.f8f825a.jpg)

1. Khi ``IoC Container`` (ApplicationContext) tìm thấy một Bean cần quản lý, nó sẽ khởi tạo bằng ``Constructor``
2. Inject dependencies vào Bean bằng Setter, và thực hiện các quá trình cài đặt khác vào Bean như setBeanName, setBeanClassLoader, v.v..
3. Hàm đánh dấu ``@PostConstruct`` được gọi
4. Tiền xử lý sau khi @PostConstruct được gọi.
5. Bean sẵn sàng để hoạt động
6. Nếu IoC Container không quản lý bean nữa hoặc bị shutdown nó sẽ gọi hàm ``@PreDestroy`` trong Bean
7. Xóa Bean.

**@PostConstruct** được đánh dấu trên một method duy nhất bên trong Bean. IoC Container hoặc ApplicationContext sẽ gọi hàm này sau khi một Bean được tạo ra và quản lý.

**@PreDestroy** được đánh dấu trên một method duy nhất bên trong Bean. IoC Container hoặc ApplicationContext sẽ gọi hàm này trước khi một Bean bị xóa hoặc không được quản lý nữa.

```
@Component
public class Car {
    @PostConstruct
    public void postContructCar(){
        System.out.println("Đối tượng Car sau khi đã được khởi tạo");
    }
    @PreDestroy
    public void preDestroyCar(){
        System.out.println("Đối tượng Car trước khi bị destroy");
    }
}
```

```
@SpringBootApplication
public class TestForReportApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(TestForReportApplication.class, args);
        Car car = context.getBean(Car.class);
        context.getBeanFactory().destroyBean(car);
    }
}
```
>Kết quả
```
Đối tượng Car sau khi đã được khởi tạo
Đối tượng Car trước khi bị destroy
```
# 2. Bean scopes
Scope của một bean định nghĩa life cycle và tính visibility của bean đó tỏng context

Có 5 scope trong bean
* **Singleton**: Chỉ duy nhất một thể hiện của bean sẽ được tạo cho mỗi container. Đây là scope mặc định cho spring bean. Khi sử dụng scope này cần chắc chắn rằng các bean không có các biến/thuộc tính được share. Khi được đánh dấu @Autowired thì sẽ gọi lại object trong ApplicationContext  

* **Prototype**: Một thể hiện của bean sẽ được tạo cho mỗi lần được yêu cầu(request) 

* **Request**: giống với prototype scope, tuy nhiên nó dùng cho ứng dụng web, một thể hiện của bean sẽ được tạo cho mỗi HTTP request. 

* **Session**: Mỗi thể hiện của bean sẽ được tạo cho mỗi HTTP Session 

* **Global-Session**: Được sử dụng để tạo global session bean cho các ứng dụng Portlet. 
  
```
public class Student {
    private String name;
    private int age;
    @Bean
    @Scope("singleton")
    public Student studentSingleton(){
        return new Student();
    }
}
```
