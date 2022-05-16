# Ubuntu内安装使用mysql

* 安装mysql

  sudo apt-get install mysql-server

* mysql 8.0 以上修改密码

`alter user 'root'@'localhost' identified with caching_sha2_password BY 'yourPassword';`

