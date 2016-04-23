JSON使用越来越多，选择一个合适的json库对于框架/应用的长远发展还是比较重要的。

# 性能
fastjson如其名，号称拥有最好的性能，从2012年开始，在pc上从未被超越。在最新的版本中，fastjson针对android退出特别优化的版本，在android上的性能也是最好的。

# Jar大小
                                         | size
-----------------------------------------|-------------------------------------
fastjson-1.2.10                          | 369759
fastjson-1.1.50.android                  | 194419
gson-2.6.2                               | 229650
jackson-2.7.3(core+databind+annotations) | 252518 + 1202276 + 50897 = 1 505 691

fastjson在pc版本上369k，在android版本上194k，都是全功能的实现，支持直接序列化和反序列化JavaBean