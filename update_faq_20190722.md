# FASTJSON升级常见问题解答

在2018年2月5日和2018年10月1日，FASTJSON分别发布了1.2.46和1.2.51版本做了安全更新。

- 2018年2月5日发布FASTJSON 1.2.46 [https://github.com/alibaba/fastjson/releases/tag/1.2.46](https://github.com/alibaba/fastjson/releases/tag/1.2.46)
- 2018年10月1日发布FASTJSON 1.2.51 [https://github.com/alibaba/fastjson/releases/tag/1.2.51](https://github.com/alibaba/fastjson/releases/tag/1.2.51)

在2018年10月1日发布的1.2.51版本中，修复了所有已知安全漏洞。在1.2.51之后陆续修复了一些兼容性问题和bug，最新版本是1.2.58。最近咨询升级兼容的同学较多，将更新常见问题整理如下：

<a name="47bb9a7b"></a>
## 更新方法

<a name="0288f5bf"></a>
## #1. Maven依赖配置更新

通过maven配置更新，使用最新版本，如下：

```xml
<!-- 1.2.51包括所有的安全更新 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.51</version>
</dependency>

<!-- 1.2.58是最新的版本 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.58</version>
</dependency>
```

<a name="618ab5e4"></a>
### 2. 直接下载

- 1.2.51版本下载地址 [http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.51/](http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.51/)
- 1.2.58版本下载地址 [http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.58/](http://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.58/)

<a name="50d52dd9"></a>
## 常见问题

<a name="4daeaf62"></a>
### 1. 升级遇到不兼容问题怎么办？

1.2.58已经修复了绝大多数兼容问题，但是总会有一些特殊的用法导致不兼容，如果你遇到不兼容问题，通过 [https://github.com/alibaba/fastjson/wiki/incompatible_change_list](https://github.com/alibaba/fastjson/wiki/incompatible_change_list) 查看不兼容问题，链接的后面提供了遇到不兼容问题之后的使用相应的sec04版本解决办法。所有的sec04版本都可以在maven中央仓库中下载。

- Maven中央仓库 [http://repo.maven.apache.org/maven2/com/alibaba/fastjson/](http://repo.maven.apache.org/maven2/com/alibaba/fastjson/)

<a name="89c7d396"></a>
### 2. 升级之后报错autotype is not support

安全升级包禁用了部分autotype的功能，也就是"@type"这种指定类型的功能会被限制在一定范围内使用。如果你使用场景中包括了这个功能，[https://github.com/alibaba/fastjson/wiki/enable_autotype](https://github.com/alibaba/fastjson/wiki/enable_autotype) 这里有一个介绍如何添加白名单或者打开autotype功能。

<a name="af0a88cf"></a>
### 3. 通过配置打开autotype之后是否存在安全漏洞

在1.2.51以及所有的.sec04版本中，有多重保护，但打开autotype之后仍会存在风险，不建议打开，而是使用一个较小范围的白名单。打开autoType建议升级到最新版本1.2.51以上

<a name="3e2636c8"></a>
### 4. Android环境使用是否需要升级

目前未发现漏洞对Android系统产生影响，在Android环境中使用不用升级。但Android升级到最新版1.1.71.android版本能提升性能。

<a name="a3b7cbe5"></a>
### 5. 升级遇到问题希望提供支持怎么办？

作者愿意帮助大家一起解决问题，如果遇到文档中没说明到的问题，请通过如下方式联系作者：

钉钉号 wenshaojin2017<br />微信号 wenshaojin<br />微博 [http://weibo.com/wengaotie](http://weibo.com/wengaotie)
