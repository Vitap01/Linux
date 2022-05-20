# Text Editors Vi(Vim)- [Text Editors Vi(Vim)](#text-editors-vivim)
  - [1. Vi (vim)](#1-vi-vim)
  - [2. Chế độ hoạt động](#2-chế-độ-hoạt-động)
  - [3. Các lệnh trong chế độ Command mode](#3-các-lệnh-trong-chế-độ-command-mode)
    - [3.1 Lệnh di chuyển, điều hướng](#31-lệnh-di-chuyển-điều-hướng)
    - [3.2 nhóm lệnh xoá](#32-nhóm-lệnh-xoá)
    - [3.3  nhóm lệnh sửa file](#33--nhóm-lệnh-sửa-file)
    - [3.4 nhóm lệnh thay đổi](#34-nhóm-lệnh-thay-đổi)
    - [3.5 Các câu lệnh dán và chèn](#35-các-câu-lệnh-dán-và-chèn)
    - [3.6 Nhóm lệnh tìm kiếm và thay thế](#36-nhóm-lệnh-tìm-kiếm-và-thay-thế)
    - [3.7 Lệnh tuỳ chỉnh](#37-lệnh-tuỳ-chỉnh)
## 1. Vi (vim)
- Vi là trình soạn thảo thường có sẵn trong Unix/Linux
- Vi được sử dụng nhiều nhất trong chỉnh sửa file cấu hình


![Imgur](https://i.imgur.com/FwwEi3I.png)


## 2. Chế độ hoạt động
- Cấu trúc 
    - ``` #vi [file] ```:   Tạo một file mới nếu nó đã không tồn tại, nếu không thì mở một file đang tồn tại để xem hoặc chỉnh sửa.
 
  - ``` #vi - R [file] ```: Mở một file đang tồn tại trong chế độ chỉ đọc.
  - ``` #view [file] ```: Mở một file đang tồn tại trong chế độ chỉ đọc.
- Chế độ hoạt động: 
    - Khi khởi tại vi bằng các cấu trúc trên, vi mặc định ở chế độ *Command Mode* để vào chế độ *Insert mode* bấm phím ``i`` hoặc ``a``.
    -  Thoát khỏi chế độ *Insert mode* về *Command mode* nhấn phím ``ESC`` 
    - Để thoát khỏi vi, phải ở chế độ *Command mode* để sử dụng lệnh để thoát:
        -   Thoát và lưu: ```:x``` hoặc ```:wq!``` hoặc ```ZZ``` (nhanh nhất)  
        -   Thoát và không lưu thay đổi: ```:q!```

![Imgur](https://i.imgur.com/J2M8mDi.png)

- Lưu ý :
  - Bộ soạn thảo vi là phân biệt chữ hoa và thường, vì thế bạn cần chú ý khi viết chữ hoa trong khi sử dụng lệnh
  - Có nhiều cách khác để di chuyển trong một file trong vi. Nhớ rằng bạn phải trong chế độ lệnh (nhấn Esc hai lần)

## 3. Các lệnh trong chế độ Command mode
### 3.1 Lệnh di chuyển, điều hướng
- ```k```:	Di chuyển con trỏ lên trên một dòng.
- ```j```:	Di chuyển con trỏ xuống một dòng.
- ```h```:	Di chuyển con trỏ sang trái một ký tự.
- ```l```:	Di chuyển con trỏ sang phải một ký tự.
- ```{```:	Di chuyển tới đoạn văn sau.
- ```}```:	Di chuyển về đoạn văn trước.
- ```1G```: Di chuyển tới dòng đầu tiên của file.
- ```G```:	Di chuyển tới dòng cuối cùng của file.
- ```nG```: Di chuyển tới dòng thứ n của file.
- ```M```:	Di chuyển tới giữa màn hình.
- ```$```:	Đặt vị trí con trở ở cuối dòng.
- ```0```: Đặt vị trí con trỏ tại đầu dòng
- ```(```:	Đặt vị trí con trỏ ở đầu câu văn hiện tại.
- ```)```:	Đặt vị trí con trỏ ở đầu câu văn kế tiếp.
### 3.2 nhóm lệnh xoá
- ```x```:	Xóa một ký tự dưới vị trí con trỏ hiện tại.
- ```X```:	Xóa một ký tự trước vị trí con trỏ hiện tại.
- ```dw```: Xóa từ vị trí con trỏ hiện tại tới từ kế tiếp.
- ```d^```: Xóa từ vị trí con trỏ hiện tại tới phần bắt đầu của dòng.
- ```d$```: Xóa từ vị trí con trỏ hiện tại tới phần cuối của dòng.
- ```D```:	Xóa từ vị trí con trỏ hiện tại tới phần cuối của dòng hiện tại.
- ```dd```: Xóa dòng mà con trỏ hiện tại đang ở trên.
- ```5dd```: xoá 5 dòng hiện hành
### 3.3  nhóm lệnh sửa file
- ```i```:	Chèn văn bản trước vị trí con trỏ hiện tại.
- ```I```:	Chèn văn bản ở phần đầu dòng hiện tại.
- ```a```:	Chèn văn bản sau vị trí con trỏ hiện tại.
- ```A```:	Chèn văn bản tại phần cuối của dòng hiện tại.
- ```o```:	Tạo một dòng mới để nhập văn bản dưới vị trí con trỏ hiện tại.
- ```O```:	Tạo một dòng mới để nhập văn bản trên vị trí con trỏ hiện tại.
### 3.4 nhóm lệnh thay đổi
- ```cc```:	Gỡ bỏ nội dung của dòng, làm cho bạn rời khỏi chế độ chèn.
- ```cw```:	Thay đổi từ mà con trỏ đang ở tại đó, từ vị trí con trỏ tới vị trí chữ w thường cuối cùng của từ.
- ```r```:	Đổi vị trí của ký tự dưới vị trí con trỏ. Vi trở lại chế độ lệnh sau khi sự đổi vị trí này được thực hiện xong.
- ```R```:	Ghi đè nhiều ký tự bắt đầu với ký tự hiện tại ở dưới con trỏ. Bạn phải sử dụng phím Esc để dừng việc ghi đè này.
- ```s```:	Đổi vị trí của ký tự hiện tại với ký tự mà bạn gõ vào. Sau đó, bạn bị rời khỏi chế độ chèn.
- ```S```:	Xóa dòng mà con trỏ đang ở trên và thay đổi bằng một đoạn văn bản mới. Sau khi văn bản mới được nhập, vi vẫn giữ nguyên chế độ chèn.
### 3.5 Các câu lệnh dán và chèn
- ```yy```:	Sao chép dòng hiện tại.
- ```yw```:	Sao chép từ hiện tại từ ký tự chữ thường w con trỏ ở trên tới phần cuối của từ.
- ```p```:	Dán bản sao sau vị trí con trỏ.
- ```P```:	Dán bản sao trước vị trí con trỏ. 
- ```u```: undo quay lại bước trước
### 3.6 Nhóm lệnh tìm kiếm và thay thế
- ```?text```: tìm trở lên
- ```/text```: tìm trở xuống
- ```*/and```: tìm từ kế tiếp của and
- ```*/?and```: tìm từ kế thúc là and
- ```*/nThe```: tìm dòng kế tiếp bắt đầu bằng The
    - ```n```: tìm hướng xuống
    - ```N```: tìm hướng lên
- ```:%s/text1/text2/g ```: thay thế text1 bằng text2
- ```:1.$s/tập_tin/thư_mục```: thay tập tin bằng thư mục này từ hàng 1
- ```:g/one/s/1/g ```: thay thế one bằng 1
### 3.7 Lệnh tuỳ chỉnh
- ```:set nu```: hiển thị số thứ tự dòng trong file
- ```:set nonu```:không hiển thị số dòng của file
- ```:<number>```: di chuyển con trỏ đến dòng thứ mấy

