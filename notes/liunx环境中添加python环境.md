# python下载
```shell
cd /home

wget http://cdn.npm.taobao.org/dist/python/3.6.5/Python-3.6.5.tgz
```

# 解压Python3安装文件
```shell
tar -zxvf Python-3.6.5.tgz
```

# 安装编译Python3源文件所需的编译环境
```shell
yum install -y gcc

yum install -y zlib*

yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

```

# 进入Python3 源文件文件夹
```shell
cd Python-3.6.5/
```

# 指定安装目录
```shell
./configure --prefix=/usr/local/python3 --with-ssl
```

# 编译源文件
```shell
make

make install
```

# 建立软连接
```shell
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
```
