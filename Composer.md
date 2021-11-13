# Composer

## 介绍

> 官网： https://www.phpcomposer.com/

Composer 是 PHP 的一个依赖管理工具。

我们可以在项目中声明所依赖的外部工具库，Composer 会帮你安装这些依赖的库文件，有了它，我们就可以很轻松的使用一个命令将其他人的优秀代码引用到我们的项目中来。

## 安装

### 条件

- Composer 默认情况下不是全局安装，而是基于指定的项目的某个目录中（例如vendor）进行安装。
- PHP 5.3.2+ 以上版本，且需要开启 openssl。 
- Windows 、 Linux 以及 Mac OS 平台。

### Windows

下载链接： https://getcomposer.org/Composer-Setup.exe

安装成功后，我们可以通过命令窗口(cmd) 输入 composer --version 命令来查看是否安装成功。

```sh
composer --version
```

接下来我们可以更改 Packagist 为国内镜像：

``` sh
composer config -g repo.packagist composer https://packagist.phpcomposer.com 
```

> 需要注意的是你需要开启 openssl 配置，我们打开 php 目录下的 php.ini， 将 extension=php_openssl.dll 前面的分号去掉就可以了。

### Linux

Linux 平台可以使用以下命令来安装：

```shell
php -r "copy('https://install.phpcomposer.com/installer', 'composer- setup.php');"
php composer-setup.php
```

移动 composer.phar，这样 composer 就可以进行全局调用：

```shell
mv composer.phar /usr/local/bin/composer
```

切换为国内镜像：

```shell
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

更新 composer：

```shell
composer selfupdate
```

### Mac OS

Mac OS 系统可以使用以下命令来安装：

```shell
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
composer --version
```

切换为国内镜像：

```shell
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```

更新 composer：

```shell
composer selfupdate
```



