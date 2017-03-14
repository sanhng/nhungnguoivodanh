# 安全升级公告
最近发现fastjson在1.2.24以及之前版本存在高危安全漏洞，会对系统造成安全风险。为了保证你的系统安全，请升级到1.2.28或者更新版本。

## 更新方法
### 1. Maven依赖配置更新
通过maven配置更新，使用最新版本，如下：
```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.28</version>
</dependency>
```

### 2. 直接下载
1.2.28版本下载地址
http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.28/

## 常见问题
### 1. 升级遇到不兼容问题怎么办？
1.2.28已经修复了绝大多数兼容问题，但是总会有一些特殊的用法导致不兼容，如果你遇到不兼容问题，通过 https://github.com/alibaba/fastjson/wiki/incompatible_change_list 查看不兼容问题，链接的后面提供了遇到不兼容问题之后的解决版本办法。

### 2. 升级之后报错autotype is not support
安全升级包禁用了部分autotype的功能，也就是"@type"这种指定类型的功能会被限制在一定范围内使用。如果你使用场景中包括了这个功能，https://github.com/alibaba/fastjson/wiki/enable_autotype 这里有一个介绍如何添加白名单或者打开autotype功能。

### 3. 通过配置打开autotype之后是否存在安全漏洞
在1.2.28以及所有的.sec01版本中，有多重保护，但打开autotype之后仍会存在风险，不建议打开，而是使用一个较小范围的白名单。

### 4. Android环境使用是否需要升级
目前未发现漏洞对Android系统产生影响，在Android环境中使用不用升级。

### 5. 升级遇到问题希望提供支持怎么办？
作者愿意帮助大家一起解决问题，如果遇到文档中没说明到的问题，请通过如下方式联系作者：
* 钉钉号 wenshaojin2017
* 微信号 wenshaojin
* 微博 http://weibo.com/wengaotie


