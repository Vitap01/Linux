# Cấu hình Web cơ bản trên Apache
## Mô hình lab

![Imgur](https://i.imgur.com/MGNAw6b.png)

- Giao diện khi chưa cấu hình

![Imgur](https://i.imgur.com/XPtwtfF.png)

## Các bươc triển khai
### Bước 1: chỉnh sửa file `http.config`
```
vi /etc/httpd/conf/httpd.conf
:set nu
```

![Imgur](https://i.imgur.com/mL1Tyrb.png)

- Ở dòng 86 , sửa localhost thành tên domain :

![Imgur](https://i.imgur.com/z2whDTN.png)

- Ở dòng 95 , sửa www.example.com thành tên domain , đồng thời bỏ dấu # ở đầu dòng :

![Imgur](https://i.imgur.com/NCrfzMC.png)

- Ở dòng 119 , chỉ định thư mục chính lưu nội dung trang web (mặc định) :

![Imgur](https://i.imgur.com/9Bl8mHv.png)

- Ở dòng 151 , sửa none thành All :

![Imgur](https://i.imgur.com/Z2ygR4P.png)

- Ở dòng 164 , chỉ định file index.html là nội dung chính của website :

![Imgur](https://i.imgur.com/T5dgub5.png)

- Lưu lại và thoát `:wq`

### Bước 2: Chỉnh sửa nội dung trang web ( file index.html ):
``` 
vi /var/www/html/index.html
<h1>Gan nhau chi trong anh mat ma xa sam tua nhu nui doi</h1>
```
### Bước 3: khởi động lại dịch vụ `httpd`
```
systemctl restart httpd
```
### Bước 4:  Truy cập trang web trên máy client trên trình duyệt web và gõ : http:172.16.206.152

![Imgur](https://i.imgur.com/h45jhDk.png)
