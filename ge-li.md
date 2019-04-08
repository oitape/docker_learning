#### 内存限制
  在docker run命令上使用`-m`或`--memory`选项来设置内存限制，这个选项会接受一个值和一个基础单元作为参数。格式`where unit = b,k,m or g`在这个命令中:
b-字节、k-千字节、m-兆字节、g-千兆字节。
  ```
  docker run -d --name ch6_mariadb --memory 256m --cpu-shares 1024 --user nobody --cap-drop all dockerfile/mariadb
  ```
     