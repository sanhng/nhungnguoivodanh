# 新手指南

## 1. 什么是fastjson?
fastjson是阿里巴巴的开源JSON解析库，它可以解析JSON格式的字符串，支持将Java Bean序列化为JSON字符串，也可以从JSON字符串反序列化到JavaBean。

## 2.fastjson的优点
### 2.1 速度快
fastjson相对其他JSON库的特点是快，从2011年fastjson发布1.1.x版本之后，其性能从未被其他Java实现的JSON库超越。

### 2.2 使用广泛
fastjson在阿里巴巴大规模使用，在数万台服务器上部署，fastjson在业界被广泛接受。在2012年被开源中国评选为最受欢迎的国产开源软件之一。

### 2.3 测试完备
fastjson有非常多的testcase，在1.2.11版本中，testcase超过3321个。每次发布都会进行回归测试，保证质量稳定。

### 2.4 使用简单
fastjson的API十分简洁。

    String text = JSON.toJSONString(obj); //序列化
    VO vo = JSON.parseObject("{...}", VO.class); //反序列化

### 2.5 功能完备
支持泛型，支持流处理超大文本，支持枚举，支持序列化和反序列化扩展。

## 3. 下载和使用
eclipse JavaEE平台下载及使用：

   3.1 下载jar包。[最新版jar包下载](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.53/fastjson-1.2.53.jar)；
   3.2 导入jar包。将jar包复制到需要使用json的工程中；[详细步骤请参考这里](https://blog.csdn.net/baidu_37107022/article/details/70876993)

你可以在maven中央仓库中直接下载：

    http://repo1.maven.org/maven2/com/alibaba/fastjson/

或者配置maven依赖

    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>x.x.x</version>
    </dependency>

其中x.x.x是版本号，根据需要使用特定版本，建议使用最新版本。

## 4. android版本
fastjson会不定期发布针对android版本优化的版本，android优化版本是去掉不必要的代码，减少体积，功能和标准版本基本一样。
已发布的android版本包括：

    http://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.51.android/

