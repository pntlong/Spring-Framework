# DTO

**Data Transfer Object Pattern** là một mẫu thiết kế được sử dụng để truyền dữ liệu với nhiều thuộc tính giữa client và server. Transfer Object cũng được biết như là một value object.

**DTO (Data Transfer Object)** chỉ chứa các thuộc tính để truyền dữ liệu giữa client-server, thông thường thì DTO được ánh xạ từ Data Model trước khi truyền dữ liệu (ví dụ: MemberDTO được ánh xạ từ MemberModel, với MemberModel là chứa những thuộc tính có trong bảng Member của DB, còn MemberDTO chứa ít thuộc tính hơn so với MemberModel).

 **Lợi ích**

* Cải thiện hiệu suất ứng dụng: chi phí của mỗi request/ response là lớn, vì vậy chúng ta cố gắng gửi DTO để có thể nhận hoặc gửi yêu cầu một cách nhanh nhất, tiết kiệm băng thông đường truyền.
* Thiết kế phần mềm rõ ràng: DTO chỉ chứa data các thuộc tính, được sử dụng để truyền giữa client-server.
* Giảm kết dính giữa các tầng trong ứng dụng: Client chỉ thao tác với Transfer Object, nên nó không bị ảnh hưởng khi Domain Model thay đổi.
* Tăng bảo mật ứng dụng: Thay vì gửi toàn bộ dữ liệu data model, chúng ta chỉ cần gửi DTO (chứa một số thông tin cần thiết từ data model thôi), do đó tránh làm lộ 1 số thông tin nhạy cảm từ data model.

```
public class UserDto {
    String name;
    String age;

    public UserDto() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAge() {
        return age;
    }

    public void setAge(String age) {
        this.age = age;
    }


    public void loadFromEntity(User entity) {
        this.name = entity.getName();
        this.age = entity.getAge();
    }
}
```
```
public class UserDto {
    String name;
    String age;

    public UserDto() {
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAge() {
        return age;
    }

    public void setAge(String age) {
        this.age = age;
    }

    public void loadFromEntity(User entity) {
        this.name = entity.getName();
        this.age = entity.getAge();
    }
}
```

Ở controller thực hiện 
```
//DTO > entity
User user = new User();
user.loadFromDto(userDto);

//Entity > DTO
User user = userService.getUser(username);
userDto userDto = new UserDto();
userDto.loadFromEntity(user);
return userDto;
```