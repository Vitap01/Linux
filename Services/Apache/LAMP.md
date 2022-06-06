# LAMP
  - [1. Định nghĩa](#1-định-nghĩa)
  - [2. Tiến hành cài đặt](#2-tiến-hành-cài-đặt)
    - [2.1 Cài đặt linux](#21-cài-đặt-linux)
    - [2.2 Cài đặt Apache](#22-cài-đặt-apache)
    - [2.3 Cài đặt hệ quản trị cơ sở dữ liệu MariaDB](#23-cài-đặt-hệ-quản-trị-cơ-sở-dữ-liệu-mariadb)
    - [2.4 Cài đặt PHP](#24-cài-đặt-php)
## 1. Định nghĩa
- LAMP là chữ viết tắt thường được dùng để chỉ sự sử dụng các phần mềm Linux, Apache, MySQL và ngôn ngữ văn lệnh PHP hay Perl hay Python để tạo nên một môi trường máy chủ Web có khả năng chứa và phân phối các trang Web động.

![imgur](https://linuxteamvietnam.us/wp-content/uploads/2020/07/lamp.png)

## 2. Tiến hành cài đặt
### 2.1 Cài đặt linux
- là môt hệ điều hành mã nguồn mở tạo môi trường cho các phần mềm hoạt động. Có nhiều phiên bản Distro phổ biến như CentOS,Ubuntu, Debian, Redhat Enterpise Linux,... hôm nay chúng ta sẽ sử dụng Centos-7
### 2.2 Cài đặt Apache
- Cài đặt và khởi động dịch vụ
```
yum install -y httpd
systemctl start httpd
systemctl enable httpd 
```
- Kiểm tra trạng thái hoạt động
```
systemctl status httpd
```

![Imgur](https://i.imgur.com/fncptZR.png)

- Kiểm tra trên máy ClinetClinet

![Imgur](https://i.imgur.com/FXQ4pKX.png)

- Lưu ý nếu các bạn sử dụng Firewall để có thể truy cập được website các bạn sẽ cần mở port:
```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```
- Kiểm tra phiên bản của Apache
```
httpd -v
```

![Imgur](https://i.imgur.com/xnezLNa.png)

### 2.3 Cài đặt hệ quản trị cơ sở dữ liệu MariaDB
- Tiến hành cài đặt và khởi động MariaDB
```
yum -y install mariadb mariadb-server
systemctl start mariadb
systemctl enable mariadb
```
- Kiểm tra trạng thái của cơ sở dữu liệuliệu
```
systeamctl status mariadb
```

![Imgur](https://i.imgur.com/QQ2O2wB.png)

- Cài mật khẩu root cho cơ sở dữ liệu
```
mysql_secure_installation
```
### 2.4 Cài đặt PHP
- Cài đặt phiên bản mới nhất.Tiến hành thêm kho Remi CentOS:
```
yum install epel-release
yum update epel-release
rpm -Uvh https://rpms.remirepo.net/enterprise/remi-release-7.rpm
```
- Cài Yum-utils vì cần tiện ích yum-config-manager để cài đặt:
```
yum -y install yum-utils
```
Tiến hành cài đặt PHP. Ở đây ta cần lưu ý về phiên bản cài đặt như sau:

- Ver 7.0:
`yum-config-manager --enable remi-php70`
- Ver 7.1:
`yum-config-manager --enable remi-php71`
- Ver 7.2:
`yum-config-manager --enable remi-php72`
- Ver 7.3:
`yum-config-manager --enable remi-php73`

- Cài đặt các Option php:
`yum -y install php php-opcache php-mysql`

- Tiến hành kiểm tra kết quả. Ta thêm file sau:
```
echo "<?php phpinfo(); ?>" > /var/www/html/info.php
```
- Sau khi cài đặt , thực hiện restart lại Apache:
```
systemctl restart httpd
```
- Vào trình duyệt, gỗ trên thanh URL địa chỉ như sau:
```
[Địa chỉ IP]/info.php
```
- Sau khi màn hình xuất hiện, đã thực hiện thành công!

![Imgur](https://i.imgur.com/Ou4aj8D.png)


Tham khảo : github/Huydv398