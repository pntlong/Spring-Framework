# 1. Entity
Một **Entity** tương ứng với một table dưới database vì thế nó phải chứa đầy đủ các thông tin như tên bảng, khoá chính, khoá ngoại, các cột trong bảng,...

**@Entity** được sử dụng để chú thích một class là một Entity.

**@Table** cho phép chú thích tên bảng thông qua thuộc tính name (thuộc tính này không bắt buộc).

**@Column** được sử dụng để chỉ định thông tin chi tiết của cột mà một field của entity sẽ được ánh xạ với một column trong database.

**@Id** được sử dụng để mô tả đây là Id (Identity) của Entity, nó tương đương với cột đó là khóa chính (Primary Key) của table trong database.

**@JoinColumn**: Chỉ rõ thực hiện Mapping field nào 

```
@Entity
@Table(name = "user")
public class User {
    @Id
    private Long id;

    private Role role;

    @Column(nullable = false, unique = true)
    private String username;
}
```

# 2. ORM
**ORM**: Object Relational Mapping Là một  kỹ thuật lập  trình  thực  hiện ánh xạ CSDL sang các Object trong ngôn ngữ lập trình

# 3. Relationship
**@OneToOne**: Biểu thị quan hệ 1-1 

**@OneToMany**: Thực hiện mapping 1-n. (VD  ! đối  tượng  Company có  			                thể chứa nhiều dối tượng Employee)  

**@ManyToOne**: Thực hiện mapping n-1 (VD Nhiều đối tượng Employee thuộc 1 		      đối tượng Company) 

**@ManyToMany**: Biểu thị quan hệ n-n 

# 4. Fetch Type (Lazy vs Eager)
**FetchType**: là một thuộc tính trong các annotation Relationship ở trên được dùng để định nghĩa phương thức lấy các đối tượng liên quan 

* ``fetch = FetchType.LAZY`` tức là khi bạn find, select đối tượng Company từ database thì nó sẽ không lấy các đối tượng Employee liên quan 

* ``fetch = FetchType.EAGER`` tức là khi bạn find, select đối tượng Company từ database thì tất cả các đối tượng Employee liên quan sẽ được lấy ra và lưu vào listEmployee 

Với ``@ManyToOne`` và ``@OneToOne`` thì FetchTyoe mặc định là EAGER 

Với ``@MnayToMany`` và ``@OneToMany`` thì FetchType mặc định là LAZY 

```
@Entity
@Table(name = "role")
public class Role {
    private Long id;

    @Column(name = "name")
    private String name;
    @OneToMany(mappedBy = "role", fetch = FetchType.LAZY)
    private Set<User> list = new HashSet<>();

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setId(Long id) {
        this.id = id;
    }

    @Id
    @GeneratedValue
    public Long getId() {
        return id;
    }
}
```
Với FetchType = LAZY(Lazy Loading):

* Ưu điểm: tiết kiệm thời gian và bộ nhớ khi select
* Nhược điểm: gây ra lỗi LazyInitializationException, khi muốn lấy các đối tượng liên quan phải mở transaction 1 lần nữa để query

Với FetchType = EAGER(Eager Loading):

* Ưu điểm: có thể lấy luôn các đối tượng liên quan, xử lý đơn giản, tiện lợi
* Nhược điểm: tốn nhiều thời gian và bộ nhớ khi select, dữ liệu lấy ra bị thừa, không cần thiết.