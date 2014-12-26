1. 修复parser在处理循环引用在某些特定场景下的bug；
2. 支持在Bean上通过JSONType配置DisableCircularReferenceDetect/BeanToArray特性；
3. 修正在并发序列化时Object类型字段BUG；
4. 新增JSONPObject对jsonp支持；
5. 支持JDK 8日期时间的序列化和反序列化；
6. 增强对ISO-8601日期格式的支持；
7. 序列化新增配置SerializeFeature.NotWriteDefaultValue，不输出缺省值，可以减少序列化后文本的大小；
8. 增强对Calendar类型的支持；
9. @JSONField支持ordinal，用于指定序列化输出的顺序；
10. 提供android专版1.1.42.android；
11. 修复序列化时SerializerFeature.WriteEnumUsingToString不生效的bug；
12. 修复ListSerializer在LinkedList拥有大量item的情况下性能严重下降的问题；
13. 修复spring3代理对象序列化失败的bug。
14. 兼容odps环境JDK
15. 修复SymbolTable>=2048后无法通过@type类型反序列化失败的问题。