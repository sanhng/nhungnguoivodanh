# License & Project URL

         | License    | URL
---------|------------|------------------------------------------
Fastjson | Apaceh 2.0 | https://github.com/alibaba/fastjson 
Gson     | Apaceh 2.0 | https://github.com/google/gson 
Jackson  | Apaceh 2.0 | https://github.com/FasterXML/jackson-core

# Maven
### fastjson
```xml
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
	<version>1.2.11</version>
</dependency>
```

### fastjson-android
```xml
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
	<version>1.1.51.android</version>
</dependency>
```

### jackson
```xml
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
	<version>2.7.3</version>
</dependency>
```

### gson
```xml
<dependency>
	<groupId>com.google.code.gson</groupId>
	<artifactId>gson</artifactId>
	<version>2.6.2</version>
</dependency>
```

# API
### Fastjson parse Tree
```java
import com.alibaba.fastjson.*;

JSONObject jsonObj = JSON.parseObject(jsonStr);
```

### Fastjson parse POJO
```java
import com.alibaba.fastjson.JSON;

Model model = JSON.parseObject(jsonStr, Model.class);
```

### Fastjson parse POJO Generic
```java
import com.alibaba.fastjson.JSON;

Type type = new TypeReference<List<Model>>() {}.getType(); 
List<Model> list = JSON.parseObject(jsonStr, type);
```

### Fastjson convert POJO to json string
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
String jsonStr = JSON.toJSONString(model);
```

### Fastjson convert POJO to json bytes
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
byte[] jsonBytes = JSON.toJSONBytes(model);
```

### Fastjson write POJO as json string to OutputStream
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
OutputStream os;
JSON.writeJSONString(os, model);
```

### Fastjson write POJO as json string to Writer
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
Writer writer = ...;
JSON.writeJSONString(writer, model);
```

