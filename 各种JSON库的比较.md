<table>
<tr><td></td><td>序列化性能</td><td>反序列化性能</td><td>jar大小</td></tr>
<tr><td>fastjson</td><td> 1201 </td><td> 1216 </td>
<td>fastjson-1.1.26.jar(356k)<br/>fastjson-1.1.25-android.jar(226k)</td></tr>
<tr><td>jackson</td><td>1408</td><td>1915</td><td>jackson-annotations-2.1.1.jar(34k)<br/>jackson-core-2.1.1.jar(206k)<br/>jackson-databind-2.1.1.jar(922k)<br/>总共1162k</td></tr>
<tr><td>gson</td><td>7421</td><td>5065</td><td>gson-2.2.2.jar(189k)</td></tr>
<tr><td>json-lib</td><td> 27555 </td><td> 87292 </td><td>json-lib-2.4-jdk15.jar(159k)</td></tr>
</table>

        | fastjson      |fastjson.android | gson      | jackson-core
--------|---------------|-----------------|-----------|----------------
最新版本 | 1.2.24         |1.1.56.android   | 2.8.0    | 
更新时间 | 2017-01-19     |2017-01-15      | 2016-10-27|        
大小     | 427k          |209k             | 261k     |
性能数据有第三方独立提供：https://github.com/eishay/jvm-serializers/wiki/Staging-Results