在1.2.25之后的版本，以及所有的.sec01后缀版本中，autotype功能是受限的，这个之前的版本不同，如果在升级的过程中遇到问题，可以通过以下方法配置。

# 添加autotype白名单
添加白名单有三种方式，如下:<br/>
1. ParserConfig.getGlobalInstance().addAccept("com.taobao.pac.client.sdk.dataobject."); 如果有多个包名前缀，分多次addAccept<br/>
2. ParserConfig.getGlobalInstance().addAccept("com.cainiao."); <br/>
3. 加上JVM启动参数 -Dfastjson.parser.autoTypeAccept=com.taobao.pac.client.sdk.dataobject.,com.cainiao. // 如果有多个包名前缀，用逗号隔开<br/>
第3种：在1.2.25/1.2.26版本支持通过类路径的fastjson.properties文件来配置，配置方式如下：
	fastjson.parser.autoTypeAccept=com.taobao.pac.client.sdk.dataobject.,com.cainiao. // 如果有多个包名前缀，用逗号隔开

# 打开autotype功能
1、JVM启动参数 -Dfastjson.parser.autoTypeSupport=true<br/>
2、代码中调用ParserConfig.getGlobalInstance().setAutoTypeSupport(true); 如果有使用非全局ParserConfig则用另外调用setAutoTypeSupport(true)；<br/>

