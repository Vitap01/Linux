# Installing NGINX and NGINX Plus
- [Installing NGINX and NGINX Plus](#installing-nginx-and-nginx-plus)
  - [Overview](#overview)
  - [Installing NGINX Open Source](#installing-nginx-open-source)
    - [Installing a Prebuilt CentOS/RHEL Package from an OS Repository](#installing-a-prebuilt-centosrhel-package-from-an-os-repository)
      - [Cài đặt kho lưu trữ EPEL:](#cài-đặt-kho-lưu-trữ-epel)
      - [Cài đặt Gói `CentOS / RHEL` dựng sẵn từ Kho lưu trữ NGINX Chính thức](#cài-đặt-gói-centos--rhel-dựng-sẵn-từ-kho-lưu-trữ-nginx-chính-thức)
    - [Installing Prebuilt `Debian` Packages](#installing-prebuilt-debian-packages)
    - [Cài đặt gói Ubuntu dựng sẵn từ kho lưu trữ Ubuntu](#cài-đặt-gói-ubuntu-dựng-sẵn-từ-kho-lưu-trữ-ubuntu)
    - [Cài đặt Gói Ubuntu dựng sẵn từ Kho lưu trữ NGINX Chính thức](#cài-đặt-gói-ubuntu-dựng-sẵn-từ-kho-lưu-trữ-nginx-chính-thức)
## Overview
- Nginx Plus là phiên bản trả phí của Nginx sử dụng cùng một mã nguồn mở miễn phí NGINX Plus hỗ trợ một số phần mở rộng khác

![Imgur](https://i.imgur.com/9EAKnBK.png)

## Installing NGINX Open Source
- NGINX Open Source có sẵn trong hai phiên bản:
    - Mainline: Bao gồm các tính năng và bản sửa lỗi mới nhất và luôn được cập nhật. 
    - Stable: Ổn định - Không bao gồm tất cả các tính năng mới nhất, nhưng có các bản sửa lỗi quan trọng luôn được hỗ trợ cho phiên bản chính
### Installing a Prebuilt CentOS/RHEL Package from an OS Repository
 - Cài đặt Nguồn mở NGINX từ một gói dễ dàng và nhanh. Các gói dựng sẵn có sẵn cho hầu hết các bản phân phối Linux phổ biến, bao gồm CentOS, Debian, Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) và Ubuntu. 

#### Cài đặt kho lưu trữ EPEL:
```
$ sudo yum install epel-release
```
Cập nhật kho lưu trữ:
```
$ sudo yum update
```
Cài đặt mã nguồn mở NGINX:
```
$ sudo yum install nginx
```
Xác minh cài đặt:
```
$ sudo nginx -v
nginx version: nginx/1.6.3
```
#### Cài đặt Gói `CentOS / RHEL` dựng sẵn từ Kho lưu trữ NGINX Chính thức

- Thiết lập yumkho lưu trữ cho RHEL hoặc CentOS bằng cách tạo tệp `nginx.repo` trong `/etc/yum.repos.d` , ví dụ bằng cách sử dụng vi:
```
$ sudo vi /etc/yum.repos.d/nginx.repo
```
Thêm các dòng sau vào nginx.repo :
```
[nginx]
name=nginx repo
baseurl=https://nginx.org/packages/mainline/<OS>/<OSRELEASE>/$basearch/
gpgcheck=0
enabled=1
```
Trong đó

Phần `/mainline `tử trong tên đường dẫn trỏ đến phiên bản dòng chính mới nhất của NGINX Open Source; xóa nó để có phiên bản ổn định mới nhất

`OS`là một trong hai rhelhoặccentos

`OSRELEASE`là số phát hành ( ,, 6v.v. )6._x_77._x_

Ví dụ: để tải gói dòng chính mới nhất cho CentOS 7, chèn bằng trình soạn thảo vi
```
[nginx]
name=nginx repo
baseurl=https://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0
enabled=1
```
Lưu các thay đổi và thoát vi(nhấn ESC và nhập wqvào :dấu nhắc).

Cập nhật kho lưu trữ:
```
$ sudo yum update
```
Cài đặt gói Nguồn mở NGINX:
```
$ sudo yum install nginx
```
Khởi động Nguồn mở NGINX:
```
$ sudo nginx
```
Xác minh rằng Nguồn mở NGINX đang hoạt động:
```
$ curl -I 127.0.0.1
HTTP/1.1 200 OK
Server: nginx/1.13.8
```

![Imgur](https://i.imgur.com/f9w03iO.png)

![Imgur](https://i.imgur.com/Mon8iY4.png)

### Installing Prebuilt `Debian` Packages

-  Cập nhật thông tin kho lưu trữ Debian:
```
$ sudo apt-get update
```
- Cài đặt gói Nguồn mở NGINX:
```
$ sudo apt-get install nginx
```
- Xác minh cài đặt:
```
$ sudo nginx -v
nginx version: nginx/1.6.2
```
- Cài đặt Gói Debian dựng sẵn từ Kho lưu trữ NGINX Chính thức
- Tải xuống khóa được sử dụng để ký các gói NGINX và kho lưu trữ, và thêmm khoá
```
$ sudo wget https://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key
```
- chỉnh sử tệp `/etc/apt/sources.list`  với trình soạn thảo Vi
```
$ sudo vi /etc/apt/sources.list
```
- Thêm các dòng này vào `sources.list` để đặt tên cho các kho lưu trữ mà từ đó Nguồn mở NGINX có thể được lấy:
```
deb https://nginx.org/packages/mainline/debian/ <CODENAME> nginx
deb-src https://nginx.org/packages/mainline/debian/ <CODENAME> nginx
```
  - Mô tả
    -   Phần /mainlinetử trong tên đường dẫn trỏ đến phiên bản dòng chính mới nhất của NGINX Open Source; xóa nó để có phiên bản ổn định mới nhất
    -   <CODENAME>là tên mã của bản phát hành Debian
-   Ví dụ: để tải gói dòng chính mới nhất cho Debian 8.2 (“jessie”), sử dụng:
```
deb https://nginx.org/packages/mainline/debian/ jessie nginx
deb-src https://nginx.org/packages/mainline/debian/ jessie nginx
```
-  Lưu các thay đổi và thoát vi
- Cài đặt gói Nginx
```
$ sudo apt-get remove nginx-common
$ sudo apt-get update
$ sudo apt-get install nginx
```
- Khởi động Nguồn mở NGINX:
```
$ sudo nginx
```
- Xác minh rằng Nguồn mở NGINX đang hoạt động:
```
$ curl -I 127.0.0.1
HTTP/1.1 200 OK
Server: nginx/1.13.8
```

### Cài đặt gói Ubuntu dựng sẵn từ kho lưu trữ Ubuntu
-  Cập nhật thông tin kho lưu trữ Ubuntu:
```
$ sudo apt-get update
```
Cài đặt gói:
```
$ sudo apt-get install nginx
```
Xác minh cài đặt:
```
$ sudo nginx -v
nginx version: nginx/1.4.6 (Ubuntu)
```
### Cài đặt Gói Ubuntu dựng sẵn từ Kho lưu trữ NGINX Chính thức
-   Tải xuống khóa được sử dụng để ký các gói NGINX và kho lưu trữ, và thêm nó vào aptvòng khóa của chương trình:
```
$ sudo wget https://nginx.org/keys/nginx_signing.key
$ sudo apt-key add nginx_signing.key
```
Chỉnh sửa tệp /etc/apt/sources.list ,với vi:
```
$ sudo vi /etc/apt/sources.list
```
- Thêm các dòng này `sources.list` để đặt tên cho các kho lưu trữ mà từ đó nguồn Nguồn mở NGINX có thể được lấy:
```
deb https://nginx.org/packages/mainline/ubuntu/ <CODENAME> nginx
deb-src https://nginx.org/packages/mainline/ubuntu/ <CODENAME> nginx
```
 - Với
    -  Phần /mainline : đường dẫn trỏ đến phiên bản dòng chính mới nhất của NGINX Open Source; xóa nó để có phiên bản ổn định mới nhất
    - `<CODENAME>`là tên mã của bản phát hành Ubuntu
Ví dụ: để tải gói dòng mới nhất cho Ubuntu 14.04 , sử dụng:
```
deb https://nginx.org/packages/mainline/ubuntu/ trusty nginx
deb-src https://nginx.org/packages/mainline/ubuntu/ trusty nginx
```
-   Lưu các thay đổi và thoát vi

-   Cài đặt mã nguồn mở NGINX:
```
$ sudo apt-get install nginx
```
- Khởi động Nguồn mở NGINX:
```
$ sudo nginx
```
- Xác minh rằng Nguồn mở NGINX đang hoạt động:
```
$ curl -I 127.0.0.1
HTTP/1.1 200 OK
Server: nginx/1.13.8
```