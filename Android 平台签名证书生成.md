# Android 平台签名证书(.keystore)生成

Android 平台打包发布apk应用，需要使用数字证书（.keystore文件）进行签名，用于表明开发者身份

Android 证书的生成是自助和免费的，不需要审批或付费。

## Keytool 命令生成证书

### 安装 JRE（如已有可跳过）

Oracle 官方下载地址：https://www.oracle.com/technetwork/java/javase/downloads/index.html

Windows 为例，jre 安装目录为 "C:\Program Files\Java\jre1.8.0_201" 为例

打开命令行（cmd），输入以下命令：

```
d:  
set PATH=%PATH%;"C:\Program Files\Java\jre1.8.0_201\bin"
```

- 第一行：切换工作目录到D:路径
- 第二行：将jre命令添加到临时环境变量中

> 安装了 JDK 一般都会包含 JRE，可以检查 JDK 或者 JRE 目录下的 bin 文件夹内是否有 keytool.exe
>
> 详细的安装 JDK 可以参考 [Java 环境安装](www.pengjunfu.com)
>
> 如果环境变量配置不成功或者因为不常用懒得配置可以 cd 到 jdk/jre 的 bin 目录操作

### 生成签名证书

使用 keytool -genkey 命令生成证书：

```
keytool -genkey -alias testalias -keyalg RSA -keysize 2048 -validity 36500 -keystore test.keystore
```

- testalias 是证书别名，可修改为自己想设置的字符，建议使用英文字母和数字
- test.keystore 是证书文件名称，可修改为自己想设置的文件名称，也可以指定完整文件路径
- 36500 是证书的有效期，表示 100 年有效期，单位天，建议时间设置长一点，避免证书过期

回车后会提示：

```
Enter keystore password:  //输入证书文件密码，输入完成回车  
Re-enter new password:   //再次输入证书文件密码，输入完成回车  
What is your first and last name?  
  [Unknown]:  //输入名字和姓氏，输入完成回车  
What is the name of your organizational unit?  
  [Unknown]:  //输入组织单位名称，输入完成回车  
What is the name of your organization?  
  [Unknown]:  //输入组织名称，输入完成回车  
What is the name of your City or Locality?  
  [Unknown]:  //输入城市或区域名称，输入完成回车  
What is the name of your State or Province?  
  [Unknown]:  //输入省/市/自治区名称，输入完成回车  
What is the two-letter country code for this unit?  
  [Unknown]:  //输入国家/地区代号（两个字母），中国为CN，输入完成回车  
Is CN=XX, OU=XX, O=XX, L=XX, ST=XX, C=XX correct?  
  [no]:  //确认上面输入的内容是否正确，输入y，回车  

Enter key password for <testalias>  
        (RETURN if same as keystore password):  //确认证书密码与证书文件密码一样（HBuilder|HBuilderX要求这两个密码一致），直接回车就可以
```

> 注意：上述信息填写要规范，乱填有可能会影响应用上架应用市场。

#### Google 开发者证书信息有误，请正确填写相关信息

在HBuilder | HBuilderX 中出现这个提示是因为密钥库类型和官方的不一样。

更改密钥库类型：

```
keytool -importkeystore -srckeystore ./test.keystore -destkeystore ./test.keystore -deststoretype JKS
```

### 查看证书信息

可以使用以下命令查看：

```
keytool -list -v -keystore test.keystore
Enter keystore password: //输入密码，回车
```

会输出以下格式信息：

```
Keystore type: PKCS12    
Keystore provider: SUN    

Your keystore contains 1 entry    

Alias name: test    
Creation date: 2019-10-28    
Entry type: PrivateKeyEntry    
Certificate chain length: 1    
Certificate[1]:    
Owner: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
Issuer: CN=Tester, OU=Test, O=Test, L=HD, ST=BJ, C=CN    
Serial number: 7dd12840    
Valid from: Fri Jul 26 20:52:56 CST 2019 until: Sun Jul 02 20:52:56 CST 2119    
Certificate fingerprints:    
         MD5:  F9:F6:C8:1F:DB:AB:50:14:7D:6F:2C:4F:CE:E6:0A:A5    
         SHA1: BB:AC:E2:2F:97:3B:18:02:E7:D6:69:A3:7A:28:EF:D2:3F:A3:68:E7    
         SHA256: 24:11:7D:E7:36:12:BC:FE:AF:2A:6A:24:BD:04:4F:2E:33:E5:2D:41:96:5F:50:4D:74:17:7F:4F:E2:55:EB:26    
Signature algorithm name: SHA256withRSA    
Subject Public Key Algorithm: 2048-bit RSA key    
Version: 3
```

其中证书指纹信息（Certificate fingerprints）：

- MD5
  证书的MD5指纹信息（安全码MD5）
- SHA1
  证书的SHA1指纹信息（安全码SHA1）
- SHA256
  证书的SHA256指纹信息（安全码SHA245）

> MD5 的签名目前不知到什么原因在比较高版本的 Java 中获取不到，可以用下面的方法获取

#### 安卓签名获取工具

直接通过一个apk，获取安装到手机的第三方应用签名的apk包。 

详情：https://developers.weixin.qq.com/doc/oplatform/Downloads/Android_Resource.html

