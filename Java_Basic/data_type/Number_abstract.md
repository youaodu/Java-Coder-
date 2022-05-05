Number抽象类是所有数字类型都继承的一个抽象类，其中定义了几个抽象方法的API，用于快速拆装箱的方法。

```java
public abstract int intValue();

public abstract long longValue();

public abstract float floatValue();

public abstract double doubleValue();

public byte byteValue() {
    return (byte)intValue();
}

public short shortValue() {
    return (short)intValue();
}
```
