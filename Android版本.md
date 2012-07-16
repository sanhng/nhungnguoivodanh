Fastjson提供Android版本，和标准版本相比，Android版本去掉一些Android虚拟机dalvik不支持的功能，使得jar更小。

# Android版本中去掉的功能
### 1. ASM
Dalvik虚拟机的字节码格式和Java SE不一样，目前的ASM动态优化无法在Android上实现。

### 2. AWT
Android上的Dalvik虚拟机不支持awt，所以去掉标准版本的awt相关类序列化和反序列化的支持。

### 3. AtomicXXX
AtomicXXX不应该作为POJO的属性，不常用，所以在Android版本中去掉了。

### 4. 不支持Clob对象序列化。

# 下载
目前只有快照版本：
http://code.alibabatech.com/mvn/snapshots/com/alibaba/fastjson/1.1.22-android-SNAPSHOT/