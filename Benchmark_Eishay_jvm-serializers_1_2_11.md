<h3>Test Platform</h3>
OS:Linux
JVM:Oracle Corporation 1.8.0_91
CPU:null os-arch:null
Cores (incl HT):1

<h3>Disclaimer</h3>

This test focusses on en/decoding of a cyclefree data structure, but the featureset of the libraries compared differs a lot:
<ul><li>some serializers support cycle detection/object sharing others just write non-cyclic tree structures</li>
<li>some include full metadata in serialized output, some don't</li>
<li>some are cross platform, some are language specific</li>
<li>some are text based, some are binary,</li>
<li>some support versioning forward/backward, both, some don't</li></ul>

(See "ToolBehavior":wiki/ToolBehavior)
Other test data will yield different results (e.g. adding a non ascii char to every string :-) ). However the results give a raw estimation of library performance.


<h3>Serializers (no shared refs)</h3>
Benchmarks serializers
<ul><li>Only cycle free tree structures. An object referenced twice will be serialized twice.</li>
<li>no manual optimizations.</li>
<li>schema is known in advance (pre registration or even class generation). (Not all might make use of that)</li>
</ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:452,786,826,918,885,968,1267,2191,1399,2288,2488,1447,1467,1728,1823,2841,2105,2574|722,1204,1240,1374,1417,1474,1466,1298,2156,1520,1370,2525,2519,2348,2282,1382,2476,2109&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,4683&chxr=1,0,4683&chxt=y,x&chxl=0:|scala%2Fsbinary|json%2Ffastjson%2Fdatabind|thrift|smile%2Fjackson%2Bafterburner%2Fdatabind|cbor%2Fjackson%2Bafterburner%2Fdatabind|smile-col%2Fjackson%2Fdatabind|cbor-col%2Fjackson%2Fdatabind|flatbuffers|thrift-compact|msgpack%2Fdatabind|protobuf|json-array%2Ffastjson%2Fdatabind|json%2Fdsl-platform|fst-flat-pre|kryo-flat-pre|minified-json%2Fdsl-platform|protostuff|colfer'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:132,146,148,150,149,148,165,165,165,147,163,178,327,241,197,252,197,246|80,87,90,89,90,92,86,86,87,108,118,115,10,97,152,100,156,151&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,397&chxr=1,0,397&chxt=y,x&chxl=0:|cbor%2Fjackson%2Bafterburner%2Fdatabind|minified-json%2Fdsl-platform|smile%2Fjackson%2Bafterburner%2Fdatabind|thrift|smile%2Fjackson%2Fdatabind|xml%2Fexi-manual|json-col%2Fjackson%2Fdatabind|json-array%2Ffastjson%2Fdatabind|scala%2Fsbinary|smile-col%2Fjackson%2Fdatabind|cbor-col%2Fjackson%2Fdatabind|fst-flat-pre|thrift-compact|protobuf|protostuff|colfer|msgpack%2Fdatabind|kryo-flat-pre'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
colfer                                 80     452     722    1174    238   148
protostuff                            144     786    1203    1990    239   150
minified-json/dsl-platform             88     826    1240    2066    353   197
kryo-flat-pre                         112     918    1374    2292    212   132
fst-flat-pre                          113     885    1418    2302    251   165
json/dsl-platform                      88     968    1474    2442    485   261
json-array/fastjson/databind          122    1267    1466    2733    281   163
protobuf                              235    2191    1298    3489    239   149
msgpack/databind                      108    1399    2156    3555    233   146
thrift-compact                        203    2288    1520    3808    240   148
flatbuffers                           115    2488    1370    3858    432   226
cbor-col/jackson/databind             114    1447    2524    3972    251   165
smile-col/jackson/databind            113    1467    2519    3986    252   165
cbor/jackson+afterburner/databind     109    1728    2347    4076    397   246
smile/jackson+afterburner/databind    109    1823    2283    4105    352   252
thrift                                203    2841    1382    4223    349   197
json/fastjson/databind                114    2105    2476    4581    486   262
scala/sbinary                         860    2574    2109    4683    255   147
json-col/jackson/databind             108    2002    2917    4919    293   178
json/jackson+afterburner/databind     116    2168    3009    5177    485   261
smile/jackson/databind                114    2532    2936    5468    338   241
json/protostuff-runtime               108    2487    3237    5724    469   243
cbor/jackson/databind                 113    2334    3574    5909    397   246
json/jackson/databind                 108    2831    3943    6774    485   261
capnproto                             116    3375    4192    7566    400   204
json/jackson-jr/databind              111    3132    4492    7624    468   255
xml/jackson/databind                   99    4957    9814   14771    683   286
json/gson/databind                    109    8355    8912   17267    486   259
bson/jackson/databind                 110    7746   10222   17969    506   286
xml/xstream+c                         117   10095   30655   40750    487   244
json/javax-tree/glassfish            2134   18218   24011   42229    485   263
xml/exi-manual                        107   23180   24148   47328    337   327
java-built-in                         108    9260   75735   84995    889   514
json/protobuf                         223   13368   99349  112718    488   253
scala/java-built-in                   830   17564  100649  118213   1293   698
json/json-lib/databind                109   50870  366619  417489    485   263
</pre>



<h3>Full Object Graph Serializers</h3>
Contains serializer(-configurations)
<ul><li>supporting full object graph write/read. Object graph may contain cycles. If an Object is referenced twice, it will be so after deserialization.</li>
<li>nothing is known in advance, no class generation, no preregistering of classes. Everything is captured at runtime using e.g. reflection.</li>
<li>note this usually cannot be used cross language, however JSON/XML formats may enable cross language deserialization.</li>
</ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x314&chd=t:1081,1708,2404,2404,4568,6102,10261,9032,6190,9271,22442,10837,17049,27288,9235|1226,1634,2474,2843,4598,9457,10850,22537,51898,73117,63278,77372,82006,93111,604441&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,613676&chxr=1,0,613676&chxt=y,x&chxl=0:|xml%2FJAXB|yaml%2Fjackson%2Fdatabind|jboss-marshalling-serial|stephenerialization|json%2Fflexjson%2Fdatabind|java-built-in-serializer|jboss-marshalling-river|xml%2FJAXB%2Faalto|jboss-serialization|hessian|jboss-marshalling-river-ct|fst|kryo-serializer|protostuff-graph-runtime|protostuff-graph'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x314&chd=t:150,151,188,199,203,313,273,260,400,318,329,498,514,582,515|89,90,98,99,113,188,230,245,294,384,390,358,375,350,578&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,1093&chxr=1,0,1093&chxt=y,x&chxl=0:|stephenerialization|jboss-serialization|java-built-in-serializer|jboss-marshalling-serial|xml%2FJAXB|xml%2FJAXB%2Faalto|jboss-marshalling-river|yaml%2Fjackson%2Fdatabind|json%2Fflexjson%2Fdatabind|hessian|fst|jboss-marshalling-river-ct|kryo-serializer|protostuff-graph-runtime|protostuff-graph'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
protostuff-graph                      140    1081    1225    2307    239   150
protostuff-graph-runtime              110    1708    1633    3342    241   151
kryo-serializer                       116    2404    2474    4878    286   188
fst                                   109    2404    2843    5247    316   203
jboss-marshalling-river-ct            112    4568    4598    9166    298   199
hessian                               111    6102    9457   15559    501   313
jboss-serialization                   112   10261   10849   21111    932   582
xml/JAXB/aalto                        193    9032   22537   31569    702   318
jboss-marshalling-river               107    6190   51898   58088    694   400
java-built-in-serializer              114    9271   73118   82388    889   514
json/flexjson/databind                112   22442   63278   85720    503   273
stephenerialization                   112   10837   77372   88209   1093   515
jboss-marshalling-serial              109   17049   82006   99055    856   498
yaml/jackson/databind                 111   27288   93112  120399    505   260
xml/JAXB                              113    9235  604441  613676    719   329
</pre>



<h3>Cross Lang Binary Serializers</h3>
Contains serializer(-configurations)
<ul><li>Only cycle free tree structures. An object referenced twice will be serialized twice.</li>
<li>schema is known in advance (pre registration, intermediate message description languages, class generation).</li>
</ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x254&chd=t:452,831,1222,2191,1399,2288,2488,2841,2334,3375,6102,7746|722,1115,1524,1298,2156,1520,1370,1382,3575,4191,9457,10223&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,17969&chxr=1,0,17969&chxt=y,x&chxl=0:|bson%2Fjackson%2Fdatabind|hessian|capnproto|cbor%2Fjackson%2Fdatabind|thrift|flatbuffers|thrift-compact|msgpack%2Fdatabind|protobuf|protobuf%2Fprotostuff-runtime|protobuf%2Fprotostuff|colfer'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x254&chd=t:146,148,149,149,148,150,197,246,204,226,313,286|87,90,90,90,92,91,152,151,196,206,188,220&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,506&chxr=1,0,506&chxt=y,x&chxl=0:|bson%2Fjackson%2Fdatabind|hessian|flatbuffers|capnproto|cbor%2Fjackson%2Fdatabind|thrift|protobuf%2Fprotostuff-runtime|thrift-compact|protobuf|protobuf%2Fprotostuff|colfer|msgpack%2Fdatabind'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
colfer                                 80     452     722    1174    238   148
protobuf/protostuff                   146     831    1114    1946    239   149
protobuf/protostuff-runtime           101    1222    1524    2746    241   150
protobuf                              235    2191    1298    3489    239   149
msgpack/databind                      108    1399    2156    3555    233   146
thrift-compact                        203    2288    1520    3808    240   148
flatbuffers                           115    2488    1370    3858    432   226
thrift                                203    2841    1382    4223    349   197
cbor/jackson/databind                 113    2334    3574    5909    397   246
capnproto                             116    3375    4192    7566    400   204
hessian                               111    6102    9457   15559    501   313
bson/jackson/databind                 110    7746   10222   17969    506   286
</pre>



<h3>XML/JSon Serializers</h3>
<ul><li>text format based. Usually can be read by anybody. Frequently inline schema inside data.</li>
<li>Mixed regarding required preparation, object graph awareness (references).</li>
</ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:826,968,1267,1447,1467,2105,2002,2487,2831,3132,4957,8355,9032,10095,18218,23180,22442,13368|1240,1474,1466,2525,2519,2476,2917,3237,3943,4492,9814,8912,22537,30655,24011,24148,63278,99350&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,112718&chxr=1,0,112718&chxt=y,x&chxl=0:|json%2Fprotobuf|json%2Fflexjson%2Fdatabind|xml%2Fexi-manual|json%2Fjavax-tree%2Fglassfish|xml%2Fxstream%2Bc|xml%2FJAXB%2Faalto|json%2Fgson%2Fdatabind|xml%2Fjackson%2Fdatabind|json%2Fjackson-jr%2Fdatabind|json%2Fjackson%2Fdatabind|json%2Fprotostuff-runtime|json-col%2Fjackson%2Fdatabind|json%2Ffastjson%2Fdatabind|smile-col%2Fjackson%2Fdatabind|cbor-col%2Fjackson%2Fdatabind|json-array%2Ffastjson%2Fdatabind|json%2Fdsl-platform|minified-json%2Fdsl-platform'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:165,165,163,178,327,197,255,243,261,261,263,263,262,259,244,253,273,260|86,87,118,115,10,156,213,226,224,224,222,222,224,227,243,235,230,245&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,505&chxr=1,0,505&chxt=y,x&chxl=0:|yaml%2Fjackson%2Fdatabind|json%2Fflexjson%2Fdatabind|json%2Fprotobuf|xml%2Fxstream%2Bc|json%2Fgson%2Fdatabind|json%2Ffastjson%2Fdatabind|json%2Fjson-lib%2Fdatabind|json%2Fjavax-tree%2Fglassfish|json%2Fjackson%2Fdatabind|json%2Fdsl-platform|json%2Fprotostuff-runtime|json%2Fjackson-jr%2Fdatabind|minified-json%2Fdsl-platform|xml%2Fexi-manual|json-col%2Fjackson%2Fdatabind|json-array%2Ffastjson%2Fdatabind|smile-col%2Fjackson%2Fdatabind|cbor-col%2Fjackson%2Fdatabind'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
minified-json/dsl-platform             88     826    1240    2066    353   197
json/dsl-platform                      88     968    1474    2442    485   261
json-array/fastjson/databind          122    1267    1466    2733    281   163
cbor-col/jackson/databind             114    1447    2524    3972    251   165
smile-col/jackson/databind            113    1467    2519    3986    252   165
json/fastjson/databind                114    2105    2476    4581    486   262
json-col/jackson/databind             108    2002    2917    4919    293   178
json/protostuff-runtime               108    2487    3237    5724    469   243
json/jackson/databind                 108    2831    3943    6774    485   261
json/jackson-jr/databind              111    3132    4492    7624    468   255
xml/jackson/databind                   99    4957    9814   14771    683   286
json/gson/databind                    109    8355    8912   17267    486   259
xml/JAXB/aalto                        193    9032   22537   31569    702   318
xml/xstream+c                         117   10095   30655   40750    487   244
json/javax-tree/glassfish            2134   18218   24011   42229    485   263
xml/exi-manual                        107   23180   24148   47328    337   327
json/flexjson/databind                112   22442   63278   85720    503   273
json/protobuf                         223   13368   99349  112718    488   253
yaml/jackson/databind                 111   27288   93112  120399    505   260
json/json-lib/databind                109   50870  366619  417489    485   263
xml/JAXB                              113    9235  604441  613676    719   329
</pre>



<h3>Manually optimized Serializers</h3>
all flavours of manually optimized serializers. Handcoded and hardwired to exactly the benchmark's message structures.
<ul><li>illustrates what's possible, at what level generic approaches can be optimized in case
</li></ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:799,748,1064,880,1253,1321,1512,1543,1484,1510,1968,2419,2296,3375,2960,3412,2761,4424|935,1113,901,1159,921,973,1125,1725,2068,2097,2445,2681,2839,2429,3547,5238,8961,7671&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,12095&chxr=1,0,12095&chxt=y,x&chxl=0:|xml%2Fwoodstox-manual|jboss-marshalling-river-manual|xml%2Faalto-manual|avro-specific|avro-generic|json%2Fprotostuff-manual|jboss-marshalling-river-ct-manual|json%2Fjackson%2Fmanual|cbor%2Fjackson%2Fmanual|msgpack%2Fmanual|smile%2Fjackson%2Fmanual|java-manual|wobly-compact|wobly|kryo-opt|datakernel|protostuff-manual|kryo-manual'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x374&chd=t:129,131,133,133,133,139,146,150,151,147,167,244,264,284,238,233,253,253|80,80,88,88,92,86,87,89,100,108,122,97,81,93,148,216,215,215&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,468&chxr=1,0,468&chxt=y,x&chxl=0:|json%2Fgson%2Fmanual|json%2Fjackson%2Fmanual|json%2Fprotostuff-manual|cbor%2Fjackson%2Fmanual|xml%2Ffastinfo-manual|xml%2Fxstream%2Bc-fastinfo|smile%2Fjackson%2Fmanual|jboss-marshalling-river-ct-manual|java-manual|wobly|protostuff-manual|msgpack%2Fmanual|wobly-compact|datakernel|avro-specific|avro-generic|kryo-manual|kryo-opt'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
kryo-manual                           114     799     936    1734    211   131
protostuff-manual                     113     748    1113    1861    239   150
datakernel                            118    1064     900    1965    225   133
kryo-opt                              115     880    1159    2039    209   129
wobly                                  77    1253     922    2174    251   151
wobly-compact                          76    1321     973    2294    225   139
java-manual                           114    1512    1125    2637    255   147
smile/jackson/manual                  115    1543    1725    3268    341   244
msgpack/manual                        109    1484    2067    3552    233   146
cbor/jackson/manual                   114    1510    2097    3607    386   238
json/jackson/manual                   109    1968    2445    4413    468   253
jboss-marshalling-river-ct-manual     111    2419    2682    5100    289   167
json/protostuff-manual                110    2296    2838    5135    449   233
avro-generic                          564    3375    2430    5804    221   133
avro-specific                         152    2960    3547    6507    221   133
xml/aalto-manual                      115    3412    5238    8650    653   304
jboss-marshalling-river-manual        108    2761    8961   11722    483   240
xml/woodstox-manual                   103    4424    7671   12095    653   304
json/gson/manual                      116    5451    7514   12965    468   253
json/json-smart/manual-tree           115    8331    6913   15244    495   265
bson/mongodb/manual                   110    4027   15672   19700    495   278
json/gson/manual-tree                 107    8389   11555   19944    485   259
xml/fastinfo-manual                   114   10409   10741   21150    377   284
xml/javolution/manual                 112    7351   14557   21908    504   263
json/json.simple/manual               108   10713   14786   25499    495   265
json/org.json/manual-tree             111   11209   14337   25546    485   259
xml/xstream+c-aalto                   118    7497   21283   28779    525   273
json/javax-stream/glassfish           111   12667   18595   31261    468   253
xml/xstream+c-woodstox                110    8119   23530   31649    525   273
xml/xstream+c-fastinfo                122   13722   18806   32528    345   264
json/svenson/databind                 115    7390   28402   35792    495   268
json/jsonij/manual-jpath              114   40004   21898   61902    478   258
json/argo/manual-tree                 108  113479   31243  144722    485   263
</pre>



<h3>Cost of features</h3>
shows performance vs convenience of manually-selected libs.
<ul><li>cycle free, schema known at compile time, manual optimization: kryo-manual, msgpack/manual</li>
<li>cycle free, schema known at compile time: protostuff, fst-flat-pre, kryo-flat-pre. (note: protostuff uses class generation while the other two just require a list of classes to be written)</li>
<li>cycle free, schema UNKNOWN at compile time: fst-flat, kryo-flat, protostuff-runtime, msgpack/databind</li>
<li>full object graph awareness, schema UNKNOWN at compile time: fst, kryo.</li>
</ul>
<b>Ser Time+Deser Time (ns)</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x234&chd=t:799,786,918,885,1088,1185,1484,1399,1344,2404,2404|935,1204,1374,1417,1480,1883,2068,2156,2332,2474,2843&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,5247&chxr=1,0,5247&chxt=y,x&chxl=0:|fst|kryo-serializer|fst-flat|msgpack%2Fdatabind|msgpack%2Fmanual|kryo-flat|protostuff-runtime|fst-flat-pre|kryo-flat-pre|protostuff|kryo-manual'/>
<br clear='all' /><b>Size, Compressed size [light] in bytes</b><br><img src='https://chart.googleapis.com/chart?cht=bhs&chs=600x234&chd=t:131,132,146,146,150,151,165,177,188,204,203|80,80,87,87,89,90,86,91,98,110,113&chco=5d99f9,4d89f9&chdlp=t&chbh=15&chds=0,316&chxr=1,0,316&chxt=y,x&chxl=0:|fst|fst-flat|kryo-serializer|kryo-flat|fst-flat-pre|protostuff-runtime|protostuff|msgpack%2Fdatabind|msgpack%2Fmanual|kryo-flat-pre|kryo-manual'/>
<br clear='all' />
<pre>                                   create     ser   deser   total   size  +dfl
kryo-manual                           114     799     936    1734    211   131
protostuff                            144     786    1203    1990    239   150
kryo-flat-pre                         112     918    1374    2292    212   132
fst-flat-pre                          113     885    1418    2302    251   165
protostuff-runtime                    109    1088    1480    2568    241   151
kryo-flat                             113    1185    1882    3068    268   177
msgpack/manual                        109    1484    2067    3552    233   146
msgpack/databind                      108    1399    2156    3555    233   146
fst-flat                              116    1344    2332    3676    314   204
kryo-serializer                       116    2404    2474    4878    286   188
fst                                   109    2404    2843    5247    316   203
</pre>

<h3>Full data</h3>


<pre>                                   create     ser   deser   total   size  +dfl
colfer                                 80     452     722    1174    238   148
kryo-manual                           114     799     936    1734    211   131
protostuff-manual                     113     748    1113    1861    239   150
protobuf/protostuff                   146     831    1114    1946    239   149
datakernel                            118    1064     900    1965    225   133
protostuff                            144     786    1203    1990    239   150
kryo-opt                              115     880    1159    2039    209   129
minified-json/dsl-platform             88     826    1240    2066    353   197
wobly                                  77    1253     922    2174    251   151
kryo-flat-pre                         112     918    1374    2292    212   132
wobly-compact                          76    1321     973    2294    225   139
fst-flat-pre                          113     885    1418    2302    251   165
protostuff-graph                      140    1081    1225    2307    239   150
json/dsl-platform                      88     968    1474    2442    485   261
protostuff-runtime                    109    1088    1480    2568    241   151
java-manual                           114    1512    1125    2637    255   147
json-array/fastjson/databind          122    1267    1466    2733    281   163
protobuf/protostuff-runtime           101    1222    1524    2746    241   150
kryo-flat                             113    1185    1882    3068    268   177
smile/jackson/manual                  115    1543    1725    3268    341   244
protostuff-graph-runtime              110    1708    1633    3342    241   151
protobuf                              235    2191    1298    3489    239   149
msgpack/manual                        109    1484    2067    3552    233   146
msgpack/databind                      108    1399    2156    3555    233   146
cbor/jackson/manual                   114    1510    2097    3607    386   238
fst-flat                              116    1344    2332    3676    314   204
thrift-compact                        203    2288    1520    3808    240   148
flatbuffers                           115    2488    1370    3858    432   226
cbor-col/jackson/databind             114    1447    2524    3972    251   165
smile-col/jackson/databind            113    1467    2519    3986    252   165
cbor/jackson+afterburner/databind     109    1728    2347    4076    397   246
smile/jackson+afterburner/databind    109    1823    2283    4105    352   252
thrift                                203    2841    1382    4223    349   197
json/jackson/manual                   109    1968    2445    4413    468   253
json/fastjson/databind                114    2105    2476    4581    486   262
scala/sbinary                         860    2574    2109    4683    255   147
kryo-serializer                       116    2404    2474    4878    286   188
json-col/jackson/databind             108    2002    2917    4919    293   178
jboss-marshalling-river-ct-manual     111    2419    2682    5100    289   167
json/protostuff-manual                110    2296    2838    5135    449   233
json/jackson+afterburner/databind     116    2168    3009    5177    485   261
fst                                   109    2404    2843    5247    316   203
smile/jackson/databind                114    2532    2936    5468    338   241
json/protostuff-runtime               108    2487    3237    5724    469   243
avro-generic                          564    3375    2430    5804    221   133
cbor/jackson/databind                 113    2334    3574    5909    397   246
avro-specific                         152    2960    3547    6507    221   133
json/jackson/databind                 108    2831    3943    6774    485   261
capnproto                             116    3375    4192    7566    400   204
json/jackson-jr/databind              111    3132    4492    7624    468   255
xml/aalto-manual                      115    3412    5238    8650    653   304
jboss-marshalling-river-ct            112    4568    4598    9166    298   199
jboss-marshalling-river-manual        108    2761    8961   11722    483   240
xml/woodstox-manual                   103    4424    7671   12095    653   304
json/gson/manual                      116    5451    7514   12965    468   253
xml/jackson/databind                   99    4957    9814   14771    683   286
json/json-smart/manual-tree           115    8331    6913   15244    495   265
hessian                               111    6102    9457   15559    501   313
json/gson/databind                    109    8355    8912   17267    486   259
bson/jackson/databind                 110    7746   10222   17969    506   286
bson/mongodb/manual                   110    4027   15672   19700    495   278
json/gson/manual-tree                 107    8389   11555   19944    485   259
jboss-serialization                   112   10261   10849   21111    932   582
xml/fastinfo-manual                   114   10409   10741   21150    377   284
xml/javolution/manual                 112    7351   14557   21908    504   263
json/json.simple/manual               108   10713   14786   25499    495   265
json/org.json/manual-tree             111   11209   14337   25546    485   259
xml/xstream+c-aalto                   118    7497   21283   28779    525   273
json/javax-stream/glassfish           111   12667   18595   31261    468   253
xml/JAXB/aalto                        193    9032   22537   31569    702   318
xml/xstream+c-woodstox                110    8119   23530   31649    525   273
xml/xstream+c-fastinfo                122   13722   18806   32528    345   264
json/svenson/databind                 115    7390   28402   35792    495   268
xml/xstream+c                         117   10095   30655   40750    487   244
json/javax-tree/glassfish            2134   18218   24011   42229    485   263
xml/exi-manual                        107   23180   24148   47328    337   327
jboss-marshalling-river               107    6190   51898   58088    694   400
json/jsonij/manual-jpath              114   40004   21898   61902    478   258
java-built-in-serializer              114    9271   73118   82388    889   514
java-built-in                         108    9260   75735   84995    889   514
json/flexjson/databind                112   22442   63278   85720    503   273
stephenerialization                   112   10837   77372   88209   1093   515
jboss-marshalling-serial              109   17049   82006   99055    856   498
json/protobuf                         223   13368   99349  112718    488   253
scala/java-built-in                   830   17564  100649  118213   1293   698
yaml/jackson/databind                 111   27288   93112  120399    505   260
json/argo/manual-tree                 108  113479   31243  144722    485   263
json/json-lib/databind                109   50870  366619  417489    485   263
xml/JAXB                              113    9235  604441  613676    719   329
</pre>



<pre>                                   Effort          Format         Structure  Misc
colfer                             CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  [] generated code                                           
kryo-manual                        MANUAL_OPT      BINARY         FLAT_TREE  [] manually optimized                                       
protostuff-manual                  MANUAL_OPT      BINARY         FLAT_TREE  [] manual                                                   
protobuf/protostuff                CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  [] protobuf + generated code                                
datakernel                         MANUAL_OPT      BINARY         FLAT_TREE  [] manually optimized                                       
protostuff                         CLASSES_KNOWN   BINARY         FLAT_TREE  [] generated code                                           
kryo-opt                           MANUAL_OPT      BINARY         FLAT_TREE  [] manually optimized                                       
minified-json/dsl-platform         CLASSES_KNOWN   JSON           FLAT_TREE  [] JSON with minified property names and without default values.
wobly                              MANUAL_OPT      BINARY         FLAT_TREE  []                                                          
kryo-flat-pre                      CLASSES_KNOWN   BINARY         FLAT_TREE  [] no shared refs, preregistered classes                    
wobly-compact                      MANUAL_OPT      BINARY         FLAT_TREE  []                                                          
fst-flat-pre                       CLASSES_KNOWN   BINARY         FLAT_TREE  [] fst in unshared mode with preregistered classes          
protostuff-graph                   CLASSES_KNOWN   BINARY         FULL_GRAPH [] graph + generated code                                   
json/dsl-platform                  CLASSES_KNOWN   JSON           FLAT_TREE  [] Serializes all properties with exact names.              
protostuff-runtime                 ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] reflection                                               
java-manual                        MANUAL_OPT      BINARY         FLAT_TREE  []                                                          
json-array/fastjson/databind       ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
protobuf/protostuff-runtime        ZERO_KNOWLEDGE  BIN_CROSSLANG  FLAT_TREE  [] protobuf + reflection                                    
kryo-flat                          ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] default, no shared refs                                  
smile/jackson/manual               MANUAL_OPT      BINARY         FLAT_TREE  []                                                          
protostuff-graph-runtime           ZERO_KNOWLEDGE  BINARY         FULL_GRAPH [] graph + reflection                                       
protobuf                           CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
msgpack/manual                     MANUAL_OPT      BIN_CROSSLANG  FLAT_TREE  [] uses positional (column) layout (instead of Maps std impl uses) to eliminate use of names
msgpack/databind                   CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  [] uses positional (column) layout (instead of Maps std impl uses) to eliminate use of names
cbor/jackson/manual                MANUAL_OPT      BIN_CROSSLANG  FLAT_TREE  []                                                          
fst-flat                           ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] fst default, but unshared mode                           
thrift-compact                     CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
flatbuffers                        CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
cbor-col/jackson/databind          ZERO_KNOWLEDGE  JSON           FLAT_TREE  [] uses positional (column) layout to eliminate use of names
smile-col/jackson/databind         ZERO_KNOWLEDGE  JSON           FLAT_TREE  [] uses positional (column) layout to eliminate use of names
cbor/jackson+afterburner/databind  ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] uses bytecode generation to reduce overhead              
smile/jackson+afterburner/databind ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] uses bytecode generation to reduce overhead              
thrift                             CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
json/jackson/manual                MANUAL_OPT      JSON           FLAT_TREE  []                                                          
json/fastjson/databind             ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
scala/sbinary                      MISC            MISC           UNKNOWN    [] null                                                     
kryo-serializer                    ZERO_KNOWLEDGE  BINARY         FULL_GRAPH [] default                                                  
json-col/jackson/databind          ZERO_KNOWLEDGE  JSON           FLAT_TREE  [] uses positional (column) layout to eliminate use of names
jboss-marshalling-river-ct-manual  MANUAL_OPT      BINARY         FULL_GRAPH [] full graph preregistered classes, manual optimization    
json/protostuff-manual             MANUAL_OPT      JSON           FLAT_TREE  [] json + manual                                            
json/jackson+afterburner/databind  ZERO_KNOWLEDGE  BINARY         FLAT_TREE  [] uses bytecode generation to reduce overhead              
fst                                ZERO_KNOWLEDGE  BINARY         FULL_GRAPH [] default: JDK serialization drop-in-replacement mode      
smile/jackson/databind             ZERO_KNOWLEDGE  BINARY         FLAT_TREE  []                                                          
json/protostuff-runtime            ZERO_KNOWLEDGE  JSON           FLAT_TREE  [] json + reflection                                        
avro-generic                       MANUAL_OPT      BIN_CROSSLANG  FLAT_TREE  []                                                          
cbor/jackson/databind              ZERO_KNOWLEDGE  BIN_CROSSLANG  FLAT_TREE  []                                                          
avro-specific                      MANUAL_OPT      BIN_CROSSLANG  UNKNOWN    []                                                          
json/jackson/databind              ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
capnproto                          CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
json/jackson-jr/databind           ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
xml/aalto-manual                   MANUAL_OPT      XML            UNKNOWN    []                                                          
jboss-marshalling-river-ct         CLASSES_KNOWN   BINARY         FULL_GRAPH [] full graph with preregistered classes                    
jboss-marshalling-river-manual     MANUAL_OPT      BINARY         FULL_GRAPH [] full graph with manual optimizations                     
xml/woodstox-manual                MANUAL_OPT      XML            UNKNOWN    []                                                          
json/gson/manual                   MANUAL_OPT      JSON           FLAT_TREE  []                                                          
xml/jackson/databind               ZERO_KNOWLEDGE  XML            FLAT_TREE  []                                                          
json/json-smart/manual-tree        MANUAL_OPT      JSON           FLAT_TREE  []                                                          
hessian                            ZERO_KNOWLEDGE  BIN_CROSSLANG  FULL_GRAPH []                                                          
json/gson/databind                 ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
bson/jackson/databind              CLASSES_KNOWN   BIN_CROSSLANG  FLAT_TREE  []                                                          
bson/mongodb/manual                MANUAL_OPT      BIN_CROSSLANG  FLAT_TREE  []                                                          
json/gson/manual-tree              MANUAL_OPT      JSON           FLAT_TREE  []                                                          
jboss-serialization                ZERO_KNOWLEDGE  BINARY         FULL_GRAPH []                                                          
xml/fastinfo-manual                MANUAL_OPT      XML            UNKNOWN    []                                                          
xml/javolution/manual              MANUAL_OPT      XML            FLAT_TREE  []                                                          
json/json.simple/manual            MANUAL_OPT      JSON           FLAT_TREE  []                                                          
json/org.json/manual-tree          MANUAL_OPT      JSON           FLAT_TREE  []                                                          
xml/xstream+c-aalto                MANUAL_OPT      XML            FLAT_TREE  []                                                          
json/javax-stream/glassfish        MANUAL_OPT      JSON           FLAT_TREE  []                                                          
xml/JAXB/aalto                     CLASSES_KNOWN   XML            FULL_GRAPH []                                                          
xml/xstream+c-woodstox             MANUAL_OPT      XML            FLAT_TREE  []                                                          
xml/xstream+c-fastinfo             MANUAL_OPT      XML            FLAT_TREE  []                                                          
json/svenson/databind              MANUAL_OPT      JSON           FLAT_TREE  []                                                          
xml/xstream+c                      ZERO_KNOWLEDGE  XML            FLAT_TREE  []                                                          
json/javax-tree/glassfish          ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
xml/exi-manual                     ZERO_KNOWLEDGE  XML            UNKNOWN    []                                                          
jboss-marshalling-river            ZERO_KNOWLEDGE  BINARY         FULL_GRAPH [] full graph zero knowledge                                
json/jsonij/manual-jpath           MANUAL_OPT      JSON           FLAT_TREE  []                                                          
java-built-in-serializer           ZERO_KNOWLEDGE  BINARY         FULL_GRAPH []                                                          
java-built-in                      ZERO_KNOWLEDGE  BINARY         FLAT_TREE  []                                                          
json/flexjson/databind             ZERO_KNOWLEDGE  JSON           FULL_GRAPH []                                                          
stephenerialization                ZERO_KNOWLEDGE  BINARY         FULL_GRAPH [] null                                                     
jboss-marshalling-serial           ZERO_KNOWLEDGE  BINARY         FULL_GRAPH []                                                          
json/protobuf                      CLASSES_KNOWN   JSON           FLAT_TREE  []                                                          
scala/java-built-in                MISC            MISC           UNKNOWN    [] null                                                     
yaml/jackson/databind              ZERO_KNOWLEDGE  JSON           FULL_GRAPH []                                                          
json/argo/manual-tree              MANUAL_OPT      JSON           FLAT_TREE  []                                                          
json/json-lib/databind             ZERO_KNOWLEDGE  JSON           FLAT_TREE  []                                                          
xml/JAXB                           CLASSES_KNOWN   XML            FULL_GRAPH []                                                          
</pre>

