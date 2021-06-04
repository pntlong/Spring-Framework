# 1. Service Scheduler/Cronjob
**Cron** expression là một đoạn text với định dạng gồm 6-7 trường để xsac định lịch chạy một phương thức, hàm, ứng dụng 

![cron](https://stackjava.com/wp-content/uploads/2018/10/cron-expression-1.png)


|TÊN TRƯỜNG|BẮT BUỘC|GIÁ TRỊ CHO PHÉP|CÁC KÝ TỰ ĐẶC BIỆT CHO PHÉP|
|----------|--------|----------------|------------------|
|Seconds|Có|0-59|,-*/|
|Minutes|Có|0-59|,-*/|
|Hours|Có|0-23|,-*/|
|Day of month|Có|1-31|,-*/?LW|
|Month|Có|1-12 or JAN-DEC|,-*/|
|Day of week|Có|1-7 or SUN-SAT|,-*/L#|
|Year|Không||,-*/ |

**@Schedule**: Thực hiện task theo thời gian đặt trước 

* fixedDelay: Cứ sau khoảng thời gian thì chạy lại 1 lần (VD: fixedDelay = 1000 cứ sau 1000ms(1s) chạy 1 lần 

* Với fixedDelay chỉ khi nào task trước đó thực hiện xong thì nó mới thực hiện task đó 1 lần nữa 

* fixedRate thì giống với fixedDelay, tuy nhiên sau khoảng thời gian fixedRate thì nó chạy tiếp 1 lần nữua mà không quan tâm task trước đó hoàn thành chưa 

* Sử dụng cron "5-10/1 * 12-14 * * MON-FRI " Thực hiện chạy trong thời gian nhất định 

```
@Scheduled(fixedDelay = 1000)
    public void schefuleFixedDelayTask(){
        System.out.println(java.time.LocalTime.now());
    }
```
# 2. Transactional

**@Transactional**: Dùng để đảm bảo tính toàn vẹn dữ liệu khi có sự thay đổi trong Database trong trường hợp xảy ra lỗi sẽ rollback lại trạng thái trước khi thay đổi 
```
@Repository(value = "customerDAO")
@Transactional(rollbackFor = Exception.class)
public class CustomerDAO {
	
	@Autowired
	private SessionFactory sessionFactory;

	public void test(Customer customer) throws Exception {
		this.save(customer);
		this.demoException();
	}
	public void save(Customer customer) {
		Session session = this.sessionFactory.getCurrentSession();
		session.save(customer);
		System.out.println("save done!");
	}
	public void demoException() throws Exception {
		// do something
		throw new Exception("demo throw exception");
	}
}
```


