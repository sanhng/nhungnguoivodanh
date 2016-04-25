# Primitive Types and Array
type                 | standard_version | android_version | 
---------------------|------------------|-----------------|---------
byte                 | Y                | Y               |
short                | Y                | Y               |
int                  | Y                | Y               |
long                 | Y                | Y               |
float                | Y                | Y               |
double               | Y                | Y               |
char                 | Y                | Y               |
boolean              | Y                | Y               |
byte[]               | Y                | Y               | base64 string encode
short[]              | Y                | Y               |
int[]                | Y                | Y               |
long[]               | Y                | Y               |
float[]              | Y                | Y               |
double[]             | Y                | Y               |
char[]               | Y                | Y               |
boolean[]            | Y                | Y               |

# Basic Types
type                           | standard_version | android_version |              |
-------------------------------|------------------|-----------------|--------------
java.lang.Number               | Y                | Y               |
java.lang.Byte                 | Y                | Y               |
java.lang.Short                | Y                | Y               |
java.lang.Integer              | Y                | Y               |
java.lang.Long                 | Y                | Y               |
java.lang.Float                | Y                | Y               |
java.lang.Double               | Y                | Y               |
java.lang.String               | Y                | Y               |
java.lang.Enum                 | Y                | Y               | 
java.lang.Class                | Y                | Y               | 
java.math.BigInteger           | Y                | Y               |
java.math.BigDecimal           | Y                | Y               |
java.lang.Object[]             | Y                | Y               |
java.util.UUID                 | Y                | Y               |
java.net.URI                   | Y                | Y               |
java.net.URL                   | Y                | Y               |
java.net.SocketAddress         | Y                | Y               |
java.net.InetAddress           | Y                | Y               |
java.net.Inet4Address          | Y                | Y               |
java.net.Inet6Address          | Y                | Y               |
java.lang.Throwable            | Y                | Y               |
java.lang.StackTraceElement    | Y                | Y               |
java.util.TimeZone             | Y                | Y               |
java.util.Currency             | Y                | Y               |
java.util.Locale               | Y                | Y               |
java.io.File                   | Y                | Y               | 
java.nio.file.Path             | Y                | N               |
java.util.regex.Pattern        | Y                | Y               |
java.nio.charset.Charset       | Y                | Y               |
java.text.SimpleDateFormat     | Y                | Y               |
java.util.Date                 | Y                | Y               |
java.util.Calendar             | Y                | Y               |

# Map Types
type                                      | standard_version | android_version |
------------------------------------------|------------------|-----------------|--------------
java.util.Map                             | Y                | Y               |
java.util.HashMap                         | Y                | Y               |
java.util.HashTable                       | Y                | Y               |
java.util.LinkedHashMap                   | Y                | Y               |
java.util.TreeMap                         | Y                | Y               |
java.util.concurrent.ConcurrentHashMap    | Y                | Y               |
java.util.concurrent.ConcurrentSkipListMap| Y                | Y               |
java.util.Collections.EmptyMap            | Y                | Y               |

# Collection Types
type                                       | standard_version | android_version |
-------------------------------------------|------------------|-----------------|--------------
java.util.Iterator                         | Y                | Y               |
java.util.Iterable                         | Y                | Y               |
java.util.Collection                       | Y                | Y               |
java.util.Queue                            | Y                | Y               |
java.util.List                             | Y                | Y               |
java.util.ArrayList                        | Y                | Y               |
java.util.LinkedList                       | Y                | Y               |
java.util.Vector                           | Y                | Y               |
java.util.Set                              | Y                | Y               |
java.util.EnumSet                          | Y                | Y               |
java.util.HashSet                          | Y                | Y               |
java.util.LinkedHashSet                    | Y                | Y               |
java.util.Collections.EmptySet             | Y                | Y               |
java.util.Collections.EmptyList            | Y                | Y               |
java.util.concurrent.ConcurrentLinkedDeque | Y                | Y               |
java.util.concurrent.ConcurrentLinkedQueue | Y                | Y               |
java.util.concurrent.ConcurrentSkipListSet | Y                | Y               |
java.util.concurrent.ConcurrentSkipListSet | Y                | Y               |
java.util.concurrent.CopyOnWriteArrayList  | Y                | Y               |
java.util.concurrent.CopyOnWriteArraySet   | Y                | Y               |

# Extend Types
type                                           | standard_version | android_version |
-----------------------------------------------|------------------|-----------------|--------------
java.util.concurrent.atomic.AtomicBoolean      | Y                | N               | 
java.util.concurrent.atomic.AtomicInteger      | Y                | N               | 
java.util.concurrent.atomic.AtomicIntegerArray | Y                | N               | 
java.util.concurrent.atomic.AtomicLong         | Y                | N               | 
java.util.concurrent.atomic.AtomicLongArray    | Y                | N               | 
java.util.concurrent.atomic.AtomicReference    | Y                | N               | 
java.lang.ref.Reference                        | Y                | N               | 
java.lang.ref.FinalReference                   | Y                | N               | 
java.lang.ref.SoftReference                    | Y                | N               | 
java.lang.ref.WeakReference                    | Y                | N               | 

# AWT Types
type                     | standard_version | android_version |
-------------------------|------------------|-----------------|--------------
java.awt.Point           | Y                | N               | 
java.awt.Font            | Y                | N               | 
java.awt.Rectangle       | Y                | N               | 
java.awt.Color           | Y                | N               | 

# SQL Types
type                     | standard_version | android_version |
-------------------------|------------------|-----------------|--------------
java.sql.Date            | Y                | N               | 
java.sql.Time            | Y                | N               | 
java.sql.Timestamp       | Y                | N               | 
java.sql.Clob            | Y                | N               | 
oracle.sql.DATE          | Y                | N               | 
oracle.sql.TIMESTAMP     | Y                | N               | 

# Java 8 Time & Optional Types
type                       | standard_version | android_version |
---------------------------|------------------|-----------------|--------------
java.time.LocalDateTime    | Y                | N               | 
java.time.LocalDate        | Y                | N               | 
java.time.LocalTime        | Y                | N               | 
java.time.ZonedDateTime    | Y                | N               | 
java.time.OffsetDateTime   | Y                | N               | 
java.time.OffsetTime       | Y                | N               | 
java.time.ZoneOffset       | Y                | N               | 
java.time.ZoneRegion       | Y                | N               | 
java.time.ZoneId           | Y                | N               | 
java.time.Period           | Y                | N               | 
java.time.Duration         | Y                | N               | 
java.time.Instant          | Y                | N               | 
java.util.Optional         | Y                | N               | 
java.util.OptionalDouble   | Y                | N               | 
java.util.OptionalInt      | Y                | N               | 
java.util.OptionalLong     | Y                | N               | 

# JavaBean & Proxy
type                                               | standard_version | android_version |
---------------------------------------------------|------------------|-----------------|--------------
net.sf.cglib.proxy.Factory                         | Y                | N               | 
org.springframework.cglib.proxy.Factory            | Y                | N               | 
javassist.util.proxy.ProxyObject                   | Y                | N               | 
org.apache.ibatis.javassist.util.proxy.ProxyObject | Y                | N               | 