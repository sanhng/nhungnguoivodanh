```
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