# 简介
[Fastjson](https://github.com/alibaba/fastjson)是[阿里巴巴开源项目](https://github.com/alibaba/)中的一个JSON库，它能将JavaBean序列化为JSON格式字符串，并且能把JSON字符串反序列化为JavaBean。Fastjson支持泛型，支持Enum，支持各种日期格式，(包括ISO8601日期格式、.NET日期格式、sql时间类型、Oracle时间类型），支持循环引用，支持JSONPath，功能丰富而且API简单易用。当然，如其名字所说的那样，它是Java语言中性能最好的JSON库。

# 如何获得Fastjson
首先你可以在fastjson项目的[Release列表](https://github.com/alibaba/fastjson/releases)中获得最新发布的版本信息[![GitHub release](https://img.shields.io/github/release/alibaba/fastjson.svg)](https://github.com/alibaba/fastjson/releases)。
Fastjson发布到maven中央仓库的，你可以从[maven中央仓库](http://repo1.maven.org/maven2/com/alibaba/fastjson/)直接下载最新版本[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.alibaba/fastjson/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.alibaba/fastjson/)。

### Maven配置
```xml
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
	<version>1.2.11</version>
</dependency>
```

### Android用户
Fastjson提供针对Android特别优化的版本，android版本也发布在[maven中央仓库](http://repo1.maven.org/maven2/com/alibaba/fastjson/)中。