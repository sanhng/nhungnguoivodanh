# 简介
[Fastjson](https://github.com/alibaba/fastjson)是[阿里巴巴开源项目](https://github.com/alibaba/)中的一个JSON库，它能将JavaBean序列化为JSON格式字符串。

# 为什么要用Fastjson
* Fastjson提供简洁易用的API。JSON.toJSONString以及JSON.parseObject两个方法就直接能满足大部分需求。
* 丰富的功能。支持泛型；支持Enum；支持各种日期格式，包括ISO8601、.NET日期格式、sql日期类型、Oracle日期类型；支持循环应用；支持JSONPath。支持多种方式自定义序列化。
* 最好的性能。Fastjson提供在Java SE上以及Android Dalvik上最好的性能。
* 开源。Fastjson采用商业友好的Apache License 2.0。
* 使用广泛。Fastjson不仅在阿里巴巴内部使用，也被业界广泛使用，在2012/2013年被开源中国评选的最受欢迎的TOP 10项目之一。
* 对Android特别优化支持。Fastjson提供针对Android特别优化的版本，jar更小（小于200k），在android性能远超原生json库以及其他库。

# 如何获得Fastjson
首先你可以在fastjson项目的[Release列表](https://github.com/alibaba/fastjson/releases)中获得最新发布的版本信息[![GitHub release](https://img.shields.io/github/release/alibaba/fastjson.svg)](https://github.com/alibaba/fastjson/releases)。
你可以从[maven中央仓库](http://repo1.maven.org/maven2/com/alibaba/fastjson/)直接下载最新版本[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.alibaba/fastjson/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.alibaba/fastjson/)。

### Maven配置
```xml
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
	<version>x.x.x</version>
</dependency>
```
其中x.x.x是你所需要配置的版本，比如1.2.11。

### Android用户
Fastjson提供针对Android特别优化的版本，android版本也发布在[maven中央仓库](http://repo1.maven.org/maven2/com/alibaba/fastjson/)中。比如fastjson-1.1.51.android下载地址是http://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.51.android/ 