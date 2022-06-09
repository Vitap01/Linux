# Log file
- là một bản ghi văn bản đơn giản của các sự kiện nhất định với thời gian.
- File log của apache server nằm ở thư mục /var/log/apache2 (đối với ubuntu) và ở /var/log/httpd (đối với centOs).
- Bao gồm 2 file chính đó là access log và error log.
- 
![Imgur](https://i.imgur.com/JPCk54q.png)

## Access log

![Imgur](https://i.imgur.com/wPFBzh5.png)

- Ghi lại những lần sử dụng, truy cập, yên cầu đến apache server
- Định dạng log (LogFormat) cơ bản như sau :` %h %l %u %t %r %>s %b Refer User_agent `
- Trong đó:
    - %h: địa chỉ của máy client
    - %l: nhận dạng người dùng được xác định bởi identd (thường không SD vì không tin cậy)
    - %u: tên người dung được xác định bằng xác thức HTTP
    - %t: thời gian yêu cầu được nhận
    - %r: là yêu cầu từ người sử dụng (client)
    - %>s: mã trạng thái được gửi từ máy chủ đến máy khách
    - %b: kích cỡ phản hồi đối với client
    - Refer: tiêu đề Refeer của yêu cầu HTTP (chứa URL của trang mà yêu cầu này được khởi tạo)
    - User_agent: chuỗi xác định trình duyệt

- Ví dụ
![Imgur](https://i.imgur.com/wPFBzh5.png)

    - 172:16.206.1: là địa chỉ IP của máy client truy cập tới apache server
    - 2 trường %l %u không có giá trị sẽ hiển thị “-“
    - 07/Jun/2022…. Là thời gian nhận được yêu cầu từ client
    - GET/HTTP/1.1: là yêu cầu từ client
    - 304: mã trạng thái gửi từ server đến client
    - `-`: kich thước phản hồi lại client
    - “http:/172.16.206.152”: url mà client yêu cầu tới server
    - Moliza …. Chrome, Safari: là chuỗi định danh trình duyệt

## Error log

- Chứa thông tin về lỗi mà máy chủ web gặp phải khi xử lý các yêu cầu, chẳng hạn như khi tệp bị thiếu.

- Là nơi đầu tiên để xem xét khi xảy ra sự cố khi khởi động máy chủ hoặc với hoạt động của máy chủ vì nó thường chứa thông tin chi tiết về những gì xảy ra và cách khắc phục 

- Định danh của error log tương đối tự do về mặt hình thức nhưng 1 số thông tin quan trọng có trong hầu hết các mục log như sau:

     - Trường thứ nhất: Trường thời gian - lưu thời gian nhận được message từ apache server
     - Trường thứ 2: liệt kê mức độ nghiêm trọng của lỗi được báo cáo
     - Trường thứ 3: Địa chỉ IP của client tạo ra lỗi
- Ví dụ: 

![Imgur](https://i.imgur.com/XiZcysY.png)

`
[Mon Jun 06 20:14:54.263599 2022] [core:notice] [pid 2978] SELinux policy enabled; httpd running as context system_u:system_r:httpd_t:s0 
`

`[Mon Jun 06 20:14:54.263599 2022]` : Trường thời gian - lưu thời gian nhận được message từ apache server

`[core:notice]` : Module tạo ra thông điệp

` [pid 2978]` : Process ID 

`SELinux policy enabled; httpd running as context system_u:system_r:httpd_t:s0` : thông báo kết nối