# 1. Repository
* **@Repository** là một trường hợp đặc biệt của @Component, bản thân annotation này đã được đánh dấu với @Component, thế nên một class được đánh dấu với @Repository sẽ được khởi tạo và đăng ký với ApplicationContext.

* Mục đích sử dụng của @Repository là để áp dụng trên các class dùng để thao tác với database.

```
@Repository
public interface UserRepository extends JpaRepository {
    User findByUsername(String username);
}
```
```
@Service
public class UserService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) {
        User user = userRepository.findByUsername(username);
        if (user == null) {
            throw new UsernameNotFoundException(username);
        }
        return new CustomUserDetails(user);
    }
}
```

# 2. Spring JPA

**JPA** viết tắt của từ Java Persitent API . Tầng Persistent có nhiệm vụ thao tác với database như query lấy dữ liệu , lưu dữ liệu xuống database . JPA cung cấp cho mình cơ chế ORM mapping các bảng, column , mối quan hệ trong database thành các lớp java và đồng thời cung cấp cho mình các method cần thiết để thao tác dữ liệu trong database.

Khi khởi tạo Repository, sẽ implement 1 trong 3 interface sau:

* **CrudRepository**: định nghĩa các hàm cơ bản như create, read, update và delete.
* **PagingAndSortingRepository**: thừa kế từ CrudRepository và thêm findAll method cho phép chúng ta sắp xếp và truy xuất kết quả được phân trang.
* **JpaRepository** bổ sung thêm một số method dành riêng cho JPA như flush, findAll.

# 3. Native Query
Native Query là SQL, một ngôn ngữ truy vấn dữ liệu dựa trên các bảng, các cột.

# 4. HQL

* Hibernate Query Language: là một ngôn ngữ truy vấn hướng đối tượng, tương tự như SQL thay vì làm việc trên các bảng và cột, HQL làm việc trên các đối tượng persistent và các thuộc tính của chúng.
* Các truy vấn HQL được dịch vởi hibernate thành các câu truy vấn SQL thông thường, lần lượt thực hiện các công việc trên cơ sở dữ liệu


|Query|Chức năng|
|-----|---------|
| FROM|Tải các đối tượng persistent vào bộ nhớ|
|SELECT|Lấy ra các thuộc tính cần thiết thay vì đối tượng hoàn chỉnh
|AS|Gán bí danh cho các lớp trong các câu truy vấn 
|WHERE|Thu hẹp các đối tượng cụ thể trả về từ cơ sở dữ liệu
|ORDER BY|Sắp xếp theo bất kỳ thuộc tính nào của đối tượng tăng dần (ASC) hoặc giảm dần (DESC)|
|GROUP BY|Lấy thông tin từ csdl và phân nhóm chúng dựa trên giá trị của thuộc tính|
|UPDATE|Cập nhật một hoặc nhiều thuộc tính của một hoặc nhiều đối tượng|
|DELETE|Xoá một hoặc nhiều đối tượng|
|INSERT|Insert từ một đối tượng này sang đối tượng khác (Insert Into)|

```
@Repository
public interface userRepository extends JpaRepository<User, Integer> {
    // find all user and sort by name
  @Query("SELECT e FROM User e ORDER BY e.name DESC")
  List<User> findAllOrderByNameDesc();

    //find all user with native query
  @Query(value = "SELECT * FROM user e ORDER BY e.name DESC", nativeQuery = true)
  List<User> findAllOrderByNameDescNative();

    //find user by username, and username is first param
  @Query("SELECT e FROM User e WHERE e.name = ?1")
  List<User> findByName(String name);

    // find user by username and address with @Param annotation
  @Query("SELECT e FROM User e WHERE e.name = :name AND e.address = :address")
  List<User> findByNameAndAddress(@Param("name") String name, @Param("address") String address);

}
```
