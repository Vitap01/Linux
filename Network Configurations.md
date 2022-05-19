# Network Configurations- [Network Configurations](#network-configurations)
  - [1. Các file cấu hình mạng](#1-các-file-cấu-hình-mạng)
    - [1.1 ``` /etc/sysconfig/network-scripts/ifcfg-[tên_card_mạng] ```](#11-etcsysconfignetwork-scriptsifcfg-tên_card_mạng)
    - [1.2 ``` /etc/hosts```](#12--etchosts)
    - [1.3 ```/etc/resolv.conf```](#13-etcresolvconf)
  - [2. Cấu hình IP](#2-cấu-hình-ip)
    - [2.1 Cấu hình bằng file](#21-cấu-hình-bằng-file)
    - [2.2 Cấu hình bằng giao diện GUIGUI](#22-cấu-hình-bằng-giao-diện-guigui)
  - [3. Cấu hình bằng ``` nmcli```](#3-cấu-hình-bằng--nmcli)
## 1. Các file cấu hình mạng
### 1.1 ``` /etc/sysconfig/network-scripts/ifcfg-[tên_card_mạng] ``` 
- Chưa thông tin cấu hình của từng card mạng mạng
    - ens33: ethernet (có sẵn)
    - wl*: wlan (wifi)
    - lo*: loopback (có sẵn)
    - bridge: (có sẵn)
    - ww* : wwan ( wireless WAN - 3G/4G )

![Imgur](https://i.imgur.com/eQckPqp.png)
### 1.2 ``` /etc/hosts```
- Dùng để phân giải những hostname không thể phân giải được.
- Có thể dùng thay DNS trong hệ thống mạng LAN

    ![Imgur](https://i.imgur.com/FbAGoEb.png)


### 1.3 ```/etc/resolv.conf```
- Dùng để cấu hình DNS
![Imgur](https://i.imgur.com/uwqlQyV.png)
## 2. Cấu hình IP
### 2.1 Cấu hình bằng file
- Thay đổi nội dung trong file cấu hình của card mạng:
  
  ``` #vi etc/sysconfig/network-scripts/ifcfg-[tên_card_mạng]```

![Imgur](https://i.imgur.com/HGgfHLW.png)


- Ý nghĩa các thông số trong file :
    - ```DEVICE``` : tên của card mạng
    - ````ONBOOT```` :
        - ```yes``` : Khởi động khi restart ``` network.service```
        - ```no ```: không khởi động khi restart network service 
    - BOOTPROTO :
        - static : dùng IP tĩnh
        - dhcp : nhận IP từ DHCP Server
    - IPADDR : địa chỉ IP của card mạng ( khi cấu hình IP tĩnh )
    - NETMASK : địa chỉ subnetmask ( khi cấu hình IP tĩnh )
    - GATEWAY : địa chỉ gateway ( khi cấu hình IP tĩnh )
    - DNS[1|2] : địa chỉ DNS Server ( khi cấu hình IP tĩnh )
    - USERCTL :
        - yes : cho phép user thường cấu hình sửa đổi
        - no : không cho phép user thường cấu hình sửa đổi

- VD : Thiết lập IP tĩnh cho Server với IP 192.168.1.3/24 , gateway 192.168.1.1
``` DEVICE=ens33
ONBOOT=yes
BOOTPROTO=static
IPADDR=10.10.10.10
NETMASK=255.255.255.0
GATEWAY=10.10.10.254
DNS1=8.8.8.8
DNS2=8.8.4.4
USERCTL=no
```


![Imgur](https://i.imgur.com/o5FQTl8.png)


        - sau khi restart lại mạng


  ![Imgur](https://i.imgur.com/FVEUid6.png)



- VD : Thiết lập IP động

``` 
DEVICE=ens33
ONBOOT=yes
BOOTPROTO=dhcp
USERCTL=no
```
### 2.2 Cấu hình bằng giao diện GUI
- trong giao diên terminal gõ ``` #nmtui ```
- Cửa sổ NetworkManager TUI hiện ra , chọn Edit a connection => OK


  ![Imgur](https://i.imgur.com/omFsT66.png)


-  Chọn Card mạng cần đặt IP (ens33):


  ![Imgur](https://i.imgur.com/29FZg0v.png)


- Chọn IPV4 CONFIGURATION => Manual => < show >


  ![Imgur](https://i.imgur.com/cGCG3pi.png)
  


- Đặt các thông số IP => OK



  ![Imgur](https://i.imgur.com/dTTnIju.png)

## 3. Cấu hình bằng ``` nmcli```
- Đây là công cụ giúp điều khiển trình quản lý mạng trong Linux bằng dòng lệnh .
- Xem các trạng thái kết nối cơ bản :
``` # nmcli [options] [command] [arguments] ```
  - Options :
      - ```-a```: hiển thị đầy đủ thông tin về phần cứng card mạng gồm MAC , MTU , IP ,...
    - ```-v```: hiển thị version của nmcli
  - Commands + Arguments :
    - ```general```:
      - ```status```:
      - ```hostname```: hiển thị hostname
  - ```network```:
    - ```on```: enable card mạng
    - ```off```: disable card mạng
    - ```connectivity``` : xem trạng thái kết nối:

        - ````full```: đã kết nối mạng và được truy cập Internet
        - ```limited```: đã kết nối mạng nhưng không được phép truy cập Internet
        - ```none```: chưa được kết nối mạng
    - ```device (dev)```: hiển thị các trạng thái interface
    - ```wifi connect```: kết nối tới mạng wifi đã biết
    - ```connection (con)```: ```show --active ```: hiển thị các kết nối đang active.



- Cấu hình IP tĩnh bằng nmcli
    - Hiển thị các thiết bị mạng đang mở:  ```#nmcli dev```



![Imgur](https://i.imgur.com/eQdoKnA.png)


    - kiẻm tra mạng: ``` #ip a ```


![Imgur](https://i.imgur.com/DAmlmQJ.png)


  - Cấu hình mạng ens37 theo thông số:
       
       
         - IP static: 192.168.177.176
         - Gateway: 192.168.177.2
         - Subnet Mask: 255.255.255.0
         - DNS: 8.8.4.4

           


```
nmcli con mod ens37 ipv4.addresses 192.168.177.176/24 
nmcli con mod ens37 ipv4.gateway 192.168.177.2
nmcli con mod ens37 ipv4.method manual 
nmcli con mod ens37 ipv4.dns 8.8.4.4
```
  kết quả: ![Imgur](https://i.imgur.com/vMvogg9.png)