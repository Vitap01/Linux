# Tìm hiểu FTP để đưa file từ client to Server
- [Tìm hiểu FTP để đưa file từ client to Server](#tìm-hiểu-ftp-để-đưa-file-từ-client-to-server)
  - [1.Định nghĩa tổng quan](#1định-nghĩa-tổng-quan)
  - [2. VSFTPD - (Very Secure FTP Daemon Software package)](#2-vsftpd---very-secure-ftp-daemon-software-package)
  - [3. Cấu hình FTP trên CentOS 7 bằng VSFTPD](#3-cấu-hình-ftp-trên-centos-7-bằng-vsftpd)
    - [3.1 Cài VSFTPD bằng dòng lệnh:](#31-cài-vsftpd-bằng-dòng-lệnh)
    - [3.2 Cấu hình dịch vụ VSTFTPD](#32-cấu-hình-dịch-vụ-vstftpd)
    - [3.3 Truy cập dịch vụ ftp từ client](#33-truy-cập-dịch-vụ-ftp-từ-client)

## 1.Định nghĩa tổng quan
FTP - File Transfer Protocol (Giao thức truyền tải tập tin) được dùng trong việc trao đổi dữ liệu trong mạng thông qua giao thức TCP/IP, thường hoạt động trên 2 cổng là 20 và 21. Với giao thức này, các máy client trong mạng có thể truy cập đến máy chủ FTP để gửi hoặc lấy dữ liệu. Điểm nổi bật là người dùng có thể truy cập vào máy chủ FTP để truyền và nhận dữ liệu dù đang ở xa.

![Imgur](https://i.imgur.com/qM3ys4T.png)
## 2. VSFTPD - (Very Secure FTP Daemon Software package)
VSFTPD là một FTP Server Stand Alone được phân phối bởi Red Hat Enterprise Linux. VSFTPD được sử dụng rộng rãi trên Linux Server và sử dụng vsFTPd sẽ đảm bảo cho chúng ta an toàn trước 99% lỗ hổng bảo mật trên FTP Server. Khi muốn cài đặt một server FTP, VSFTPD sẽ là lựa chọn tối ưu nhất

Mô hình của VSFTPD có những đặc điểm chính như sau:

- Giữa tiến trình mang đặc quyền và tiến trình không mang đặc quyền có phân chia rõ ràng.
- Các tiến trình được chạy trong chroot jail nhằm nâng cao bảo mật.
- Chroot trên các hệ điều hành Unix là một công đoạn thay đổi thư mục root cho các tiến trình đang chạy hiện tại và các tiền trình con của nó.

## 3. Cấu hình FTP trên CentOS 7 bằng VSFTPD

### 3.1 Cài VSFTPD bằng dòng lệnh:
- ```sudo yum install vsftpd```

![Imgur](https://i.imgur.com/5TffRTE.png)

- Sau khi nhận thông báo ấn `“Y”` để thoát quá trinh
- Bắt đầu dịch vụ. Sau đó thiết lập cho nó khởi động cùng hệ thống:
- ```sudo systemctl start vsftpd ```
- ```sudo systemctl enable vsftpd```

![Imgur](https://i.imgur.com/Bl0Ostt.png)

- ` `Tiếp theo, tạo một rule cho tường lửa để cho phép truy cập FTP trên cổng 21:
- ```sudo firewall-cmd --zone=public --permanent --add-port=21/tcp ```
- ```sudo firewall-cmd --zone=public --permanent --add-service=ftp ```
- ```sudo firewall-cmd --reload```

![Imgur](https://i.imgur.com/AQKMFO0.png)

### 3.2 Cấu hình dịch vụ VSTFTPD
- Trước khi bắt đầu, hãy tạo một bản sao của file cấu hình mặc định (Việc này đảm bảo bạn có cách để quay trở lại cấu hình mặc định nếu gặp sự cố trong quá trình cài đặt.):
- ```sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.default```
- Sau đó, chỉnh sửa file cấu hình với lệnh:
- ```vi /etc/vsftpd/vsftpd.conf```

![Imgur](https://i.imgur.com/GPXpYOS.png)


![Imgur](https://i.imgur.com/gne2dbP.png)

Nội dung các dòng các dòng này:

- `#listen=YES/NO` : VSFTPD chạy ở chế độ standalone.
- `#session\_support=YES/NO` : VSFTPD quản lý giao dịch login của người dùng.
- `#anonymous\_enable=YES/NO `: người dùng anonymous được phép login vào FTP Server.
- `#cmds\_allowed` : Chỉ ra danh sách các lệnh ftp (cách nhau bởi dấu phẩy) được cho phép bởi FTP Server.
- `#ftpd\_banner` : dòng thông báo sẽ hiển thị khi người dùng kết nối đến FTP Server.
- `#local\_enable==YES/NO` : cho phép người dùng cục bộ login vào FTP Server.
- `#userlist\_deny=YES` và `#userlist\_enable=NO` : thì tất cả những người dùng cục bộ bị cấm truy cập trừ những người dùng được chỉ ra trong userlist\_file.
- `#userlist\_deny=NO `và `#userlist\_enable=YES` : thì tất cả những người dùng được chỉ ra trong `userlist\_file `bị cấm truy cập.
- `#userlist\_file=/etc/vsftpd.user\_list`: chỉ ra tập tin lưu danh sách người dùng.
- `#anon\_mkdir\_write\_enable=YES/NO` : kết hợp với `#write\_enable=YES` thì người dùng anonymous được phép tạo thư mục mới trong thư mục cha có quyền ghi.
- `#anon\_root` : chỉ ra thư mục gốc của user anonymous, mặc định là /var/ftp.
- `#anon\_upload\_enable=YES/NO` : kết hợp với `#write\_enable=YES` thì người dùng anonymous được phép upload tập tin trong thư mục cha có quyền ghi.
- `#anon\_world\_readable\_only=YES` : user anonymous chỉ được phép download những tập tin có quyền đọc.
- `#no\_anon\_password=YES/NO` : yêu cầu user anonymous nhập vào password lúc đăng nhập.
- `#local\_enable=YES/NO `: cho phép người dùng cục bộ truy cập đến Server.
- `#chmod\_enable=YES/NO` : cho phép người dùng thay đổi quyền hạn trên tập tin.
- `#chroot\_local\_user=YES/NO `: người dùng di chuyển đến home directory của mình sau khi login vào.
- `#guest\_enable=YES/NO `: cho phép người dùng anonymous login vào như user guest, mà được chỉ ra trong guest\_username.
- `#guest\_username` : chỉ ra username của người dùng guest (user mặc định ftp).
- `#local\_root`: chỉ ra thư mục khi người dùng cục bộ login vào.
- `#dirlist\_enable=YES/NO` : người dùng được phép xem nội dung của thư mục.
- `#dirmessage\_enable=YES/NO` : hiển thị ra 1 thông điệp khi người dùng di chuyển vào thư mục. Thông điệp này được lưu trong tập tin có tên .message và được chỉ ra trong tùy chọn message\_file.
- `#message\_file `: chỉ ra tên của tập tin lưu thông điệp.
- `#download\_enable=YES/NO` : cho phép download.
- `#chown\_uploads=YES/NO` : tất cả những tập tin được upload bởi user anonymous được sở hữu bởi user được chỉ ra trong chown\_username.
- `#chown\_username` : chỉ ra user sở hữu những tập tin được upload bởi user anonymous (mặc định là user root).
- `write\_enable=YES/NO` : cho phép xoá, thay đổi và lưu trữ tập tin.
- `#accept\_timeout` : chỉ ra thời gian một client sử dụng chế độ passive để thiết lập kết nối đến Server. Tính bằng giây.
- `#anon\_max\_rate` : chỉ ra tốc độ truyền dữ liệu tối đa cho người dùng anonymous. Tính bằng byte/second.
- `#connect\_timeout` : chỉ ra thời gian một client sử dụng chế độ active để trả lời kết nối đến Server. Tính bằng giây.
- `#data\_connect\_timeout` : chỉ ra thời gian truyền dữ liệu tối đa. Khi kết thúc thời gian cho phép kết nối từ client sẽ bị đóng.
- `#max\_clients` : chỉ ra số client tối đa đồng thời truy cập đến Server.




Câu lệnh đề cử

- `anonymous\_enable=NO` → Tắt truy cập ẩn danh
- `local\_enable=YES` → Chỉ cho phép người dùng cục bộ
- `write\_enable=YES` → Cho phép người dùng ghi vào thư mục
- `local\_umask=022` → Người dùng cục bộ kiểm soát quyền mặc định
- `dirmessage\_enable=YES` → hiển thị ra 1 thông điệp khi người dùng di chuyển vào thư mục. Thông điệp này được lưu trong tập tin có tên .message và được chỉ ra trong tùy chọn message\_file.
- `xferlog\_enable=YES` → nhật ký các kết nối  và thông tin  ghi tệp nhật ký theo đường dẫn mặc định /var/log/vsftpd.log
- `connect\_from\_port\_20=YES` → kết nối bằng port 20
- `xferlog\_std\_format=YES`  → kết hợp với xferlog\_enable
- `pam\_service\_name=vsftpd` → Tên dịch vụ
- `userlist\_enable=YES` → ất cả những người dùng được chỉ ra trong userlist\_file bị cấm truy cập.
- `tcp\_wrappers=YES `→ Bật danh sách điều khiển truy cập (ACL – Access Control List) dựa trên máy, và sử dụng để lọc truy cập mạng với các dịch vụ địa phương.
- Tạo user tài khoản local:
- ```#useradd nam```
- ```#passwd nam ```
- Sau khi cấu hình  restart lại dịch vụ ftp
- ```#Systemctl restart vsftpd```


### 3.3 Truy cập dịch vụ ftp từ client
Ở đây, ta sử dụng FileZilla một phần mềm phổ biến nhất  để truy cập tới FTP server. Ta nhập địa chỉ IP của Server, username, password:

![Imgur](https://i.imgur.com/6H9vAal.png)

*Đăng nhập thành công*

- Tạo site kết nối
- File -> Site Manager… để vào phần quản lý Site. (hoặc nhấn tổ hợp phím Ctrl+S)
- Chọn tạo địa chỉ mới và nhập các thông số sau đó kết nối, địa chỉ này sẽ được lưu lại thuận tiền cho lần sử dụng sau

![Imgur](https://i.imgur.com/yzQr9Bf.png)

- Gửi file: 

!<a href="https://imgur.com/ehShg4j"><img src="https://i.imgur.com/ehShg4j.png" title="source: imgur.com" /></a>

*Tải file lên thành công*

![Imgur](https://i.imgur.com/djtINjY.png)

*User local không có quyền truy cập vào thư mục root*
