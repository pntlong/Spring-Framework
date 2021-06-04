# 1. Email Service
Spring Framework cung cấp cho bạn một API để gửi email, nó bao gồm một vài interface và một vài lớp, tất cả nằm trong 2 package org.springframework.mail & org.springframework.mail.javamail.

|Class/Interface|Mô tả|
|-----|-----------|
|MailSender|Là một interface ở mức cao nhất (top-level), nó cung cấp các chức năng để gửi một email đơn giản.|
|JavaMailSender|	Là interface con (subinterface) của MailSender, nó hỗ trợ các tin nhắn kiểu MIME, nó thường đươc sử dụng với lớp MimeMessageHelper để tạo ra MimeMessage. Một lời khuyên là nên sử dụng interface MimeMessagePreparator cùng với interface này.|
|JavaMailSenderImpl|	Là một lớp thực hiện interface JavaMailSender. Nó hỗ trợ gửi các tin nhắn MimeMessage và SimpleMailMessage.|
|MailMessage|Là một interface đại diện cho một tin nhắn (message) đơn giản. Nó bao gồm các thông tin cơ bản của một email như người gửi, người nhận, tiêu đề (subject) và nội tin nhắn.|
|SimpleMailMessage|Là một lớp thực hiện (implements) interface MailMessage, được sử dụng để tạo một tin nhắn (message) đơn giản.|
|MimeMailMessage|Là một lớp thực hiện interface MailMessage, được sử dụng để tạo ra một tin nhắn hỗ trợ MIME.|
|MimeMessagePreparator|	Interface này cung cấp phương thức callback được gọi khi chuẩn bị một tin nhắn MIME.|
|MimeMessageHelper|Là một lớp trợ giúp để tạo ra một tin nhắn MIME, nó hỗ trợ image, và các tập tin đính kèm, và tạo ra các tin nhắn kiểu HTML.|
|MimeMessageHelper|	Là một lớp trợ giúp để tạo ra một tin nhắn MIME, nó hỗ trợ image, và các tập tin đính kèm, và tạo ra các tin nhắn kiểu HTML.|

```
@Bean
    public JavaMailSender getJavaMailSender() {
        JavaMailSenderImpl mailSender = new JavaMailSenderImpl();
        mailSender.setHost("smtp.gmail.com");
        mailSender.setPort(587);

        mailSender.setUsername(MyConstants.MY_EMAIL);
        mailSender.setPassword(MyConstants.MY_PASSWORD);

        Properties props = mailSender.getJavaMailProperties();
        props.put("mail.transport.protocol", "smtp");
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.debug", "true");

        return mailSender;
    }
```

```
@GetMapping("/sendEmail")
    public String sendSimpleEmail() {

        SimpleMailMessage message = new SimpleMailMessage();

        message.setTo(MyConstants.FRIEND_EMAIL);
        message.setSubject("Test Email service");
        message.setText("Hello Long");
        this.emailSender.send(message);

        return "Email Sent!";
    }
```

![email](Screen%20Shot%202021-06-04%20at%2016.50.36.png)

# 2. Thymleaf

**Thymeleaf** là một Java Template Engine. Có nhiệm vụ xử lý và generate ra các file HTML, XML, v.v..

Các file HMTL do Thymeleaf tạo ra là nhờ kết hợp dữ liệu và template + quy tắc để sinh ra một file HTML chứa đầy đủ thông tin.

Trong Thymeleaf, để lấy giá trị của Model, chúng ta sẽ sử dụng Thymeleaf Standard Expression
* ${...}: giá trị của một biến
* *{...}: giá trị của một biến được chỉ định
* #{...}: giá trị của một message
* @{...}: đường dẫn URL theo context của server

![thymleaf](https://s3-ap-southeast-1.amazonaws.com/kipalog.com/ct1pe51ln3_2.png)

# 3. Multilanguage

Internationalization đa ngôn ngữ hoặc trong lập trình mình còn gọi là i18n. Bởi vì mình có 18 ký tự ở giữa ký tự I và ký tự N. Internationalization (quốc tế hoá) là một kỹ thuật cho phép chúng ta tạo ra các ứng dụng mà có thể thích ứng với nhiều ngôn ngữ và nhiều khu vực khác nhau.

```
@Bean
    public LocaleResolver localeResolver()  {
        CookieLocaleResolver resolver= new CookieLocaleResolver();
        return resolver;
    }

    @Bean
    public MessageSource messageSource()  {
        ReloadableResourceBundleMessageSource messageResource= new ReloadableResourceBundleMessageSource();
        messageResource.setBasename("classpath:i18n/lang");
        messageResource.setDefaultEncoding("UTF-8");
        return messageResource;
    }

    public void addInterceptors(InterceptorRegistry registry) {
        LocaleChangeInterceptor localeInterceptor = new LocaleChangeInterceptor();
        localeInterceptor.setParamName("lang");
        registry.addInterceptor(localeInterceptor).addPathPatterns("/*");
    }
 ```

 ```
 hello = Hello
name = Long
language = English
```
```
hello = Xin Chào
name = Long
language = Tiếng Việt
```
