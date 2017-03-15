#打开AutoType功能
在1.2.25之后的版本，以及所有的.sec01后缀版本中，autotype功能是受限的，和之前的版本不同，如果在升级的过程中遇到问题，可以通过以下方法配置。

## 一、添加autotype白名单
添加白名单有三种方式，三选一，如下:<br/>
### 1. 在代码中配置
```java
ParserConfig.getGlobalInstance().addAccept("com.taobao.pac.client.sdk.dataobject."); 
```
如果有多个包名前缀，分多次addAccept

### 2. 加上JVM启动参数
```script
    -Dfastjson.parser.autoTypeAccept=com.taobao.pac.client.sdk.dataobject.,com.cainiao. 
```
如果有多个包名前缀，用逗号隔开

### 3. 通过fastjson.properties文件配置。
在1.2.25/1.2.26版本支持通过类路径的fastjson.properties文件来配置，配置方式如下：
```
fastjson.parser.autoTypeAccept=com.taobao.pac.client.sdk.dataobject.,com.cainiao. // 如果有多个包名前缀，用逗号隔开
```

## 二、打开autotype功能
如果通过配置白名单解决不了问题，可以选择继续打开autotype功能，fastjson在新版本中内置了多重防护，但是还是可能会存在一定风险。两种方法打开autotype，二选一，如下：
### 1、JVM启动参数 
```
-Dfastjson.parser.autoTypeSupport=true
```
### 2、代码中设置
```java
ParserConfig.getGlobalInstance().setAutoTypeSupport(true); 
```
如果有使用非全局ParserConfig则用另外调用setAutoTypeSupport(true)；

