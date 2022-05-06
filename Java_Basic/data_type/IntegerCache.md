IntegerCache是Integer的一个内部类，代码也很少。

```java
private static class IntegerCache {
        static final int low = -128;
        static final int high;
        static final Integer cache[];

        static {
            // high value may be configured by property
            int h = 127;
            String integerCacheHighPropValue =
                sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
            if (integerCacheHighPropValue != null) {
                try {
                    int i = parseInt(integerCacheHighPropValue);
                    i = Math.max(i, 127);
                    // Maximum array size is Integer.MAX_VALUE
                    h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
                } catch( NumberFormatException nfe) {
                    // If the property cannot be parsed into an int, ignore it.
                }
            }
            high = h;

            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);

            // range [-128, 127] must be interned (JLS7 5.1.7)
            assert IntegerCache.high >= 127;
        }

        private IntegerCache() {}
    }
```

从这里可以看出来，只要不是在vm启动时设置的参数，默认缓存存储范围是-128 到 127。



到这里了，看几道关于Integer的面试题。

> 1. 两个new Integer 128相等吗？
> 
> 2. 可以修改Integer缓存池范围吗？如何修改？
> 
> 3. Integer是如何获取你设置的缓存池大小？
> 
> 4. `sun.misc.VM.getSavedProperty`和`System.getProperty`有啥区别？



同样的，除了IntegerCache，还有ShortCache和LongCache，他们的共同点就是都是-128 到 127的范围。不同点是，只有Integer可以修改上限范围，其他都不可以设置。
