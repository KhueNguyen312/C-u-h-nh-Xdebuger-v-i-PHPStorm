# Cách cài đặt Xdebug và config với PHPStorm trên HDH Linux
## Bước 1: Cài đặt Xdebug
1. Cài đặt Xdebug sử dụng lệnh:
```shell
sudo apt-get install xdebug
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
Cài đặt PHPStorm bằng lệnh
```
sudo snap install phpstorm --classic phpstorm
```
Nếu có rồi thì bỏ qua bước này
Mở phpstorm vừa cài đặt Chọn File -> Settings -> Languages & Frameworks -> PHP -> Debug. Trong mục Xdebug, điền đúng Xdebug port đã cấu hình ở file xdebug.ini và lưu lại.
![image](https://user-images.githubusercontent.com/37147552/177470700-fc2aa885-e63e-45ca-93d6-097d931f3425.png)
