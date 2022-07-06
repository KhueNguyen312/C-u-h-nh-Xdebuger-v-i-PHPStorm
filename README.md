# Cách cài đặt Xdebug và config với PHPStorm trên HDH Linux
## Bước 1: Cài đặt Xdebug
1. Cài đặt Xdebug sử dụng lệnh:
```shell
sudo apt-get install php-xdebug
```
Nếu gặp lỗi ERROR: `phpize' failed thì sử dụng lệnh
```shell
apt search xdebug
```
để tìm kiếm available package cho xdebug. 
```shell
Sorting... Done
Full Text Search... Done
php-xdebug/bionic,now 2.6.0-0ubuntu1 amd64 [installed]
  Xdebug Module for PHP
```
Từ kết quả tìm kiếm trên sử dụng lệnh sau để install xdebug. 
```shell
sudo apt-get install php-xdebug
```
Kết quả sau khi install thành công 
```shell
Build process completed successfully
Installing '/usr/lib/php/20190902/xdebug.so
You should add "zend_extension=/usr/lib/php/20190902/xdebug.so" to php.ini
```
Tiếp theo ta tìm kiếm file php.ini sử dụng lệnh
```shell
sudo find / -name php.ini
```
và edit file trên với lệnh
```shell
sudo nano /etc/php/7.2/apache2/php.ini
```
và thêm 
```shell
zend_extension=/usr/lib/php/20190902/xdebug.so
xdebug.remote_enable=1
xdebug.remote_host=localhost
xdebug.remote_port=9000
xdebug.remote_handler="dbgp"
```
vào sau
```shell
; If you use constants in your value,  and these constants belong to a
; dynamically loaded extension (either a PHP extension or a Zend extension),
; you may only use these constants *after* the line that loads the extension.
```
sau đó restart lại web server
```shell 
sudo service apache2 restart
```
## Bước 2: Config trên PHPStorm
Cài đặt PHPStorm bằng lệnh
```
sudo snap install phpstorm --classic phpstorm
```

Mở phpstorm vừa cài đặt Chọn File -> Settings -> Languages & Frameworks -> PHP -> Debug. Trong mục Xdebug, điền đúng Xdebug port đã cấu hình ở file xdebug.ini và lưu lại.
![Screenshot from 2022-07-06 13-57-31](https://user-images.githubusercontent.com/37147552/177488526-1cec0d1f-8bc0-474f-a253-2f5941337f6a.png)

Trong File -> Settings -> Languages & Frameworks -> PHP. Chọn phiên bản PHP phù hợp.
![Screenshot from 2022-07-06 13-56-20](https://user-images.githubusercontent.com/37147552/177488428-55498f7b-07c1-48fe-81b1-998a51a68c4a.png)
Chọn button ... trong dòng CLI Interpreter
![Screenshot from 2022-07-06 13-58-01](https://user-images.githubusercontent.com/37147552/177488661-4119d052-62fa-4c0a-8208-d0dead193178.png)
Chọn button + góc trên bên trái và chọn /usr/bin/php sau đó bấm button refesh ở dòng php executable. Sau khi cài đặt thành công ta sẽ thấy hiển thị phiên bản Xdebug đã cài như hình dưới đây
![Screenshot from 2022-07-06 14-04-01](https://user-images.githubusercontent.com/37147552/177489812-2a2b11d1-d284-4413-bcc2-20fda6c01897.png)

## Bước 3: Cài đặt Chrome Xdebug và config
Cài đặt Xdebug helper tại đây:
https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=en
![image](https://user-images.githubusercontent.com/37147552/177491280-75e398f4-67d0-4237-abc9-a87848a9adbd.png)
Chọn IDE KEY là PHPStorm sau đó enable extension này lên trang web cần debug.

## Bước 4: Debug
Quay lại PHPStorm bấm vào button ![Screenshot from 2022-07-06 14-15-07](https://user-images.githubusercontent.com/37147552/177491811-40c453c4-7fe3-465f-a3bf-f4d63d9546e2.png)

![Screenshot from 2022-07-06 14-14-08](https://user-images.githubusercontent.com/37147552/177491641-fecaa3ae-dca6-42c5-9bef-bc58fe815cfb.png)

Tạo 1 breakpoint tại vị trí code cần debug. Khi chạy đến đoạn code đó. PHPStorm sẽ dừng tại điểm breakpoint. 
![Screenshot from 2022-07-06 14-17-40](https://user-images.githubusercontent.com/37147552/177492293-65b03910-961b-4aee-9b00-b0145cba7a36.png)
 
