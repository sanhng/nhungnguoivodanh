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
type                           | standard_version | android_version |
-------------------------------|------------------|-----------------|--------------
java.lang.Byte                 | Y                | Y               |
java.lang.Short                | Y                | Y               |
java.lang.Integer              | Y                | Y               |
java.lang.Long                 | Y                | Y               |
java.lang.Float                | Y                | Y               |
java.lang.Double               | Y                | Y               |
java.lang.String               | Y                | Y               |
java.lang.Enum                 | Y                | Y               | 
java.lang.Class                | Y                | Y               | encode/decode to stirng using ClassName
java.math.BigInteger           | Y                | Y               |
java.math.BigDecimal           | Y                | Y               |
java.lang.Object[]             | Y                | Y               |

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