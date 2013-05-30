ASMDeserializerFactory是用来动态使用ASM生成JavaBean的Deserializer，针对每个类的特点进行特别优化，以获得最快的性能。
# 兼容性
目前ASMDeserializerFactory不能在android的dalvik虚拟机以及阿里云OS的lemur虚拟机上运行。
<table>
<tr><td>虚拟机</td><td>是否支持</td></tr>
<tr><td>Oracle Hotspot</td><td>支持</td></tr>
<tr><td>dalvik</td><td>不支持</td></tr>
<tr><td>lemur</td><td>不支持</td></tr>
</table>

