ASMDeserializerFactory是用来动态使用ASM生成JavaBean的Deserializer，针对每个类的特点进行特别优化，以获得最快的性能。
# 1. 局限性
## 1.1 虚拟机兼容
目前ASMDeserializerFactory不能在android的dalvik虚拟机以及阿里云OS的lemur虚拟机上运行。
<table>
<tr><td>虚拟机</td><td>是否支持</td></tr>
<tr><td>Oracle Hotspot</td><td>支持</td></tr>
<tr><td>dalvik</td><td>不支持</td></tr>
<tr><td>lemur</td><td>不支持</td></tr>
</table>

```java
public class ASMUtils {
     public static boolean isAndroid(String vmName) {
     	String lowerVMName = vmName.toLowerCase();
        return lowerVMName.contains("dalvik") 
                 || lowerVMName.contains("lemur") // aliyun-vm name
                 ;
     }
}
```
## 1.2 超多字段类
目前ASMDeserializerFactory不支持超过200个字段JavaBean。做反序列化的时候，需要定义局部变量保存parse的结果，目前的asm框架不能定义超过256个变量，目前保守的做法是，如果字段数量超过200个，则不使用ASMDeserializerFactory。

            DeserializeBeanInfo beanInfo = DeserializeBeanInfo.computeSetters(clazz, type);
            if (beanInfo.getFieldList().size() > 200) {
                asmEnable = false;
            }   


# 2 实现
## 2.1 创建实例
如果类有缺省public的构造函数，直接使用new来创建实例；否则使用JavaBeanDeserializer.createInstance(DefaultJSONParser, Type)来创建实例。

## 2.2 定义字段是否已经被parse的标识变量
每32个变量的flag保存在一个int类型的变量中，_setFlag和_isFlag分别用于设置和读取其是否被parse。