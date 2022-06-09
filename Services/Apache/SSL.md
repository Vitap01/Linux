# SSL
## Tổng quan

![Imgur](https://i.imgur.com/DX0wxsm.png)

- SSL là viết tắt của từ Secure Sockets Layer, llà một tiêu chuẩn an ninh công nghệ toàn cầu tạo ra một liên kết được mã hóa giữa máy chủ website và trình duyệt.
-  Hiện tại TLS (Transport Layer Security: "Bảo mật tầng giao vận") đã thay thế cho SSL (Secure Sockets Layer: "Tầng socket bảo mật")
-  Về cơ bản chứng chỉ SSL có 1 cặp key-pair : 1 public key và 1 private key . Chúng hoạt động cùng nhau để tạo ra kết nối mã hóa và cũng bao gồm 1 phần gọi là "subject" , dùng để nhận biết chủ sở hữu của webste/certificate .
-  HTTPS là phần mở rộng bảo mật của HTTP . Website được cài đặt chứng chỉ SSL/TLS có thể dùng giao thức HTTPS để thiết lập kênh kết nối an toàn tới server . HTTPS sử dụng port 443/tcp .
-  Let's Enscrypt là một tổ chức xác thực SSL phi lợi nhuận và cung cấp chứng chỉ miễn phí cho toàn thế giới.

## Cấu hình SSL - Https
- Bước 1 : Cài đặt module `mod_ssl` và các gói `openssl` :
    ```
    yum install -y mod_ssl openssl
    ```
    => Lệnh sẽ thực hiện tạo ra file cấu hình chính : `/etc/httpd/conf.d/ssl.conf`
- Bước 2 : Tạo thư mục chứa `server key` và `certificate` :
    ```
    mkdir /etc/httpd/ssl
    ```
- Bước 3 : Tạo ***SSL key*** và ***certificate*** :
    ```
    # openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/httpd/ssl/apache.key -out /etc/httpd/ssl/apache.crt
    ```
    - Trong đó :
        - `openssl` : là công cụ cơ bản để quản lý ***OpenSSL certificates*** , ***keys*** , và các file khác .
        - `req -x509` : tùy chọn sử dụng chuẩn `x509` . `x509` là chuẩn kiến trúc ***public key*** mà **SSL** và **TLS** sử dụng cho việc quản lý ***key*** và ***certificates*** .
        - `-nodes` : tùy chọn bỏ qua bảo mật bằng cách nhập ***passphrase*** ( nếu không có tùy chọn này sẽ phải nhập lại 1 đoạn ***passphrase*** mỗi lần khởi động lại Server )
        - `-days 365` : tùy chọn thời gian hết hạn cho ***key*** và ***certificate***
        - `-newkey rsa:2048` : tùy chọn tạo ***key*** và ***certificate*** cùng 1 lúc . `rsa:2048` cho biết ***key*** dài `2048 bit`
        - `keyout` : khai báo nơi lưu ***private key***
        - `out` : khai báo nơi lưu ***certificate***
    - Sau khi thực hiện lệnh , 1 bảng prompt hiện ra yêu cầu nhập thông tin của Website :

        ![Imgur](https://i.imgur.com/63J7ScT.png)

        > `Common Name` là dòng quan trọng nhất , nếu có domain name thì ghi domain name , nếu không thì thay thế bằng IP Public
- Bước 4 : Thêm virtual host cho website HTTPS :
    ```
    # vi /etc/httpd/conf.d/ssl.conf
    ```
    - Tại dòng `59` , bỏ dấu `#` ở đầu dòng :

        ![Imgur](https://i.imgur.com/iqROGHZ.png)
    
    - Tại dòng `100` , khai báo nơi lưu ***certificate*** :

        ![Imgur](https://i.imgur.com/CBAdEKN.png)

    - Tại dòng `107` , khai báo nơi lưu ***private key*** :

        ![Imgur](https://i.imgur.com/XE0ATx4.png)

- Bước 5 : Cho phép dịch vụ **HTTPS** trên **firewalld** :
    ```
    # firewall-cmd --zone=public --permanent --add-service=https
    # firewall-cmd --reload
    ```
- B6 : Khởi động lại dịch vụ `httpd` :
    ```
    systemctl restart httpd
    ```
- Bước 7 : Truy cập trang web từ Client :
    ```
    https://<ip_web_server>
    ```
    - Do trình duyệt không trust ***certificate*** vừa tạo nên sẽ xuất hiện cảnh báo . Chọn ***Advanced*** : 

        ![Imgur](https://i.imgur.com/5olvzH7.png)

    - Chọn ***Accept the Risk and Continue*** :
    - Truy cập trang web thành công :

        ![Imgur](https://i.imgur.com/qhXa9je.jpg)


 
Tham khảo : Github/Quoccuong97