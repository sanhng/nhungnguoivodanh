### write10AsString
```
java -Xmx256m -jar target/microbenchmarks.jar -wi 4 -i 5 -f 9 ".*DZoneWrite.*write10AsString"

Benchmark                             Mode  Cnt       Score       Error  Units
DZoneWriteFastjson.write10AsString   thrpt   45  476436.182 ± 10123.057  ops/s
DZoneWriteDslJson.write10AsString    thrpt   45  416872.751 ±  3599.205  ops/s
DZoneWriteJacksonAB.write10AsString  thrpt   45  306310.217 ±  3948.435  ops/s
DZoneWriteJackson.write10AsString    thrpt   45  234603.755 ±  3788.233  ops/s
DZoneWriteJacksonJr.write10AsString  thrpt   45  224772.236 ±  1875.920  ops/s
DZoneWriteMoshi.write10AsString      thrpt   45  124215.907 ±   664.051  ops/s
DZoneWriteBoon.write10AsString       thrpt   45  106093.314 ±  1732.035  ops/s
DZoneWriteJohnzon.write10AsString    thrpt   45   30630.930 ±   233.012  ops/s
DZoneWriteJsonIO.write10AsString     thrpt   45   16018.749 ±  3711.678  ops/s
DZoneWriteGSON.write10AsString       thrpt   45   83956.443 ±  1456.487  ops/s
```

### Reading 1000 item (POJO) list from String

```
java -Xmx256m -jar target/microbenchmarks.jar ".*DZoneReadPojo.*read10FromString.*" -wi 4 -i 5 -f 9

Benchmark                                 Mode  Cnt       Score      Error  Units
DZoneReadPojoDslJson.read10FromString    thrpt   45  199728.153 ± 1231.002  ops/s
DZoneReadPojoFastjson.read10FromString   thrpt   45  151060.526 ± 2700.248  ops/s
DZoneReadPojoJacksonAB.read10FromString  thrpt   45  150816.951 ± 1607.385  ops/s
DZoneReadPojoJacksonJr.read10FromString  thrpt   45  145262.943 ± 2509.262  ops/s
DZoneReadPojoJackson.read10FromString    thrpt   45  140813.727 ± 3671.932  ops/s
DZoneReadPojoGSON.read10FromString       thrpt   45  104762.208 ± 1285.506  ops/s
DZoneReadPojoBoon.read10FromString       thrpt   45   72738.583 ± 1112.040  ops/s
DZoneReadPojoMoshi.read10FromString      thrpt   45   61181.062 ± 1524.961  ops/s
DZoneReadPojoJohnzon.read10FromString    thrpt   45   57053.948 ± 2576.479  ops/s
```