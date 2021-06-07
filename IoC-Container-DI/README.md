# 1. Inversion of ControlControl
Trong Spring, Spring Container (**IoC Container**) sẽ tạo các đối tượng, lắp rắp chúng lại với nhau, cấu hình các đối tượng và quản lý vòng đời của chúng từ lúc tạo ra cho đến lúc bị hủy.

Để tạo đối tượng, cấu hình, lắp rắp chúng, Spring Container sẽ đọc thông tin từ các file xml và thực thi chúng.

![IoC](https://viblo.asia/uploads/e8537ffa-e5a5-4b78-9aa5-be2ad0ac236e.jpg)

IoC Container trong Spring có 2 kiểu:

* BeanFactory
* ApplicationContext 

# 2. Dependency Injection
**Dependency Injection (DI)** trong Spring là một mẫu thiết kế được sử dụng để loại bỏ sự phụ thuộc giữa các mã chương trình, giúp cho việc quản lý và kiểm thử ứng dụng dễ dàng hơn. Dependency Injection làm cho mã chương trình ít bị phụ thuộc vào nhau hơn.


Các phương pháp cơ bản để Dependency Injection.

* Constructor Injection: Các dependency sẽ được truyền vào (inject vào) 1 class thông qua constructor của class đó. Đây là cách thông dụng nhất. (ví dụ trên mình dùng theo cách này)
* Setter Injection: Các dependency sẽ được truyền vào 1 class thông qua các hàm Setter/Getter

Ưu điểm
* Giảm sự kết dính giữa các module
* Code dễ bảo trì, dễ thay thế module
* Rất dễ test và viết Unit Test
* Dễ dàng thấy quan hệ giữa các module (Vì các dependecy * đều được inject vào constructor)

Nhược điểm
* Khó debug vì không biết implements nào của interface được gọi đến
* Các object được khởi tạo từ đầu làm giảm performance
* Làm tăng độ phức tạp của code
<!-- 
```
public interface AbstractDAO {
  void insert();
  void delete();
  void update();
}
```

```
public class Client {
  AbstractDAO dao;
  public Client() {
    dao = FactoryDAO.getDAO();
  }
  public AbstractDAO getDao() {
    return dao;
  }
  public void setDao(AbstractDAO dao) {
    this.dao = dao;
  }
  
  public void execute() {
    dao.insert();
    dao.update();
    dao.delete();
  }
}
```

```
public class MainApp {
  public static void main(String[] args) {
    Client client = new Client();
    client.execute();
  }
}
```

```
public class FactoryDAO {
  public static AbstractDAO getDAO() {
    Properties prop = new Properties();
    InputStream input = null;
    try {
      input = new FileInputStream("source/config.properties");
      prop.load(input);
      String database = prop.getProperty("database");
      if (database.equals("1")) {
        return new MySQLDAO();
      }
      if (database.equals("2")) {
        return new PostgreDAO();
      }
      if (database.equals("3")) {
        return new MSSQLDAO();
      }
    } catch (IOException ex) {
      ex.printStackTrace();
      return null;
    }
    return null;
  }
}
```

```
public class PostgreDAO implements AbstractDAO {
  @Override
  public void insert() {
    System.out.println("Postgre insert");
  }
  @Override
  public void delete() {
    System.out.println("Postgre delete");
  }
  @Override
  public void update() {
    System.out.println("Postgre update");
  }
}
```

```
Postgre insert
Postgre update
Postgre delete
```
 -->
