Fastjson是一个Java语言编写的高性能功能完善的JSON库。它采用一种“假定有序快速匹配”的算法，把JSON Parse的性能提升到极致，是目前Java语言中最快的JSON库。Fastjson接口简单易用，已经被广泛使用在缓存序列化、协议交互、Web输出、Android客户端等多种应用场景。

# Issues
－某些场景下反序列化Set<String>出错
－序列化支持Clob对象
－序列化和反序列化支持Calendar

# 下载
你可以从以下地址中下载fastjson: 

* Maven中央仓库 http://repo1.maven.org/maven2/com/alibaba/fastjson/
* Alibaba OpenSesame开源平台 http://code.alibabatech.com/mvn/releases/com/alibaba/fastjson/

# Maven
配置pom.xml文件，在dependencies中加入：

      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>fastjson</artifactId>
          <version>1.1.22</version>
      </dependency>