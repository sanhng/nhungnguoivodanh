Fastjson提供Android版本，和标准版本相比，Android版本去掉一些Android虚拟机dalvik不支持的功能，使得jar更小。

# Android版本中去掉的功能
### 1. ASM
Dalvik虚拟机的字节码格式和Java SE不一样，目前的ASM动态优化无法在Android上实现。

### 2. AWT
Android上的Dalvik虚拟机不支持awt，所以去掉标准版本的awt相关类序列化和反序列化的支持。

### 3. AtomicXXX
AtomicXXX不应该作为POJO的属性，不常用，所以在Android版本中去掉了。

### 4. 不支持Clob对象序列化。

### 5. 不支持Reference字段类型序列化和反序列化，比如WeakReference/SoftReference/AtomicReference，这些类型不常用用作POJO的属性，所以去掉了。

### 6. 以下方法不常用，不支持

    public abstract class JSON {
        public static parseObject(byte[] input, int off, int len, CharsetDecoder charsetDecoder, Type clazz,
                                          Feature... features) { ... }
    
        public static Object parse(byte[] input, int off, int len, CharsetDecoder charsetDecoder, 
                                          int features) {}

        public static Object parse(byte[] input, int off, int len, CharsetDecoder charsetDecoder, 
                                          Feature...features) {}
    
        public static Object parse(byte[] input, int off, int len, CharsetDecoder charsetDecoder, 
                                          int features) {}
    }

    // JSONSerializerMap已废弃，不支持
    com.alibaba.fastjson.serializer.JSONSerializer.JSONSerializer(JSONSerializerMap)

### 7. 一些废弃的类不支持

    com.alibaba.fastjson.parser.JavaBeanMapping 使用com.alibaba.fastjson.parser.ParserConfig代替
    com.alibaba.fastjson.serializer.JSONSerializerMap  使用com.alibaba.fastjson.serializer.SerializeConfig代替
    com.alibaba.fastjson.parser.DefaultExtJSONParser 使用com.alibaba.fastjson.parser.DefaultJSONParser代替

### 8. 一些废弃方法不支持
    
    class com.alibaba.fastjson.JSONWriter {
        @Deprecated
        public void writeStartObject();
        
        @Deprecated
        public void writeEndObject();
    
        @Deprecated
        public void writeStartArray();
        
        @Deprecated
        public void writeEndArray();
    }

# 下载
目前只有快照版本：
http://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.33.android/
http://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.34.android/