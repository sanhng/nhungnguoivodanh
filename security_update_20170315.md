# 安全升级公告
最近发现fastjson在1.2.24以及之前版本存在远程代码执行高危安全漏洞，为了保证系统安全，请升级到1.2.28/1.2.29/1.2.30/1.2.31或者更新版本。

1.2.29//1.2.30/1.2.31是在1.2.28版本上修复了一些大家升级过程中遇到的问题的版本，非安全问题，如果升级到1.2.25~1.2.28以及各种sec01版本的，也是没有安全问题的。

1.2.25/1.2.26/1.2.27/1.2.28/1.2.29/1.2.30都是在升级的过程中修复不兼容问题发布的过度版本，如果你是在此之前升级到这些版本，不用因为这次的安全问题再次升级。

## 更新方法
### 1. Maven依赖配置更新
通过maven配置更新，使用最新版本，如下：
```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.31</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.39</version>
</dependency>
```

注意，版本号1.2.3~1.2.9版本都比1.2.31小，都是需要升级的。

### 2. 直接下载
* 1.2.31版本下载地址
http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.31/
* 1.2.39版本下载地址
http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.39/

## 常见问题
### 1. 升级遇到不兼容问题怎么办？
1.2.28/1.2.29/1.2.30/1.2.31已经修复了绝大多数兼容问题，但是总会有一些特殊的用法导致不兼容，如果你遇到不兼容问题，通过 https://github.com/alibaba/fastjson/wiki/incompatible_change_list 查看不兼容问题，链接的后面提供了遇到不兼容问题之后的使用相应的sec01版本解决办法。

### 2. 升级之后报错autotype is not support
安全升级包禁用了部分autotype的功能，也就是"@type"这种指定类型的功能会被限制在一定范围内使用。如果你使用场景中包括了这个功能，https://github.com/alibaba/fastjson/wiki/enable_autotype 这里有一个介绍如何添加白名单或者打开autotype功能。

### 3. 通过配置打开autotype之后是否存在安全漏洞
在1.2.28/1.2.29以及所有的.sec01版本中，有多重保护，但打开autotype之后仍会存在风险，不建议打开，而是使用一个较小范围的白名单。打开autoType建议升级到最新版本1.2.37以上

### 4. Android环境使用是否需要升级
目前未发现漏洞对Android系统产生影响，在Android环境中使用不用升级。

### 5. 升级遇到问题希望提供支持怎么办？
作者愿意帮助大家一起解决问题，如果遇到文档中没说明到的问题，请通过如下方式联系作者：
* 钉钉号 wenshaojin2017
* 微信号 wenshaojin
* 微博 http://weibo.com/wengaotie

### 6. 有没有漏洞利用详情可以提供
为了保证更多用户的安全，目前不适合扩散漏洞利用的细节

### 7. 是否有在WAF上检测的办法
检测post内容中是否包含如下字符
```
"@type"
```
注意，为了减少误报，包括双引号

### 8. 检测当前使用版本的是否有问题
1. 通过maven dependency检测
如果是maven工程，在代码根目录下执行如下命令，如果有返回，就是需要升级
```
mvn dependency:tree | grep "com.alibaba.fastjson:"
 | grep -v sec01 | grep -v 1.2.25 | grep -v 1.2.26 | grep -v 1.2.27 | grep -v 1.2.28 | grep -v 1.2.29 | grep -v 1.2.30 | grep -v 1.2.31
```

2. 在lib目录下执行如下脚本命令，可以判断版本是否有问题
```
ls | grep fastjson | grep jar
 | grep -v sec01 | grep -v 1.2.25 | grep -v 1.2.26 | grep -v 1.2.27
 | grep -v 1.2.28 | grep -v 1.2.29 | grep -v 1.2.30 | grep -v 1.2.31
```
请注意，为了方便阅读，加上了换行符，请使用时把上面的三行合并成一行。

3. 看打开的文件中是否包含fastjson
```
sudo -u admin lsof -X | grep -v 1.2.25 | grep -v 1.2.26 | grep -v 1.2.27
 | grep -v 1.2.28 | grep -v 1.2.29 | grep -v 1.2.30 | grep -v 1.2.31
```
请注意，为了方便阅读，加上了换行符，请使用时把上面的两行合并成一行。另外通过lsof检测，在tomcat某些场景是检测不出来的，最好在lib目录下用ls检测（第2中方法）。
