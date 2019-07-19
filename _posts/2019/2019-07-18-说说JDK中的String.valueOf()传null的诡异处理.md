# 说说JDK中的String.valueOf()传null的诡异处理

都说JDK的实现诡异多，今儿也算是被我踩到一个坑了。

就来说说关于String.valueOf的这个坑。

```java

public class TestString {
    public static void main(String[] args) {
        Object obj = null;
        System.out.println(String.valueOf(obj));
        System.out.println(String.valueOf(null));
    }
}

```

这段代码，第一个输出“null”，没错，不是空对象null也不是空串“”,而是一个字符串！！包含四个字母n-u-l-l的字符串...

好吧，我只能说写这个逻辑的人估计是想逗我们玩儿...

第二个输出，咋一看没差别，但是，第二个输出，抛空指针异常了。

下面来分析分析原因。

先说第一个：

看第一个的源码实现：

```java

    /**
     * Returns the string representation of the {@code Object} argument.
     *
     * @param   obj   an {@code Object}.
     * @return  if the argument is {@code null}, then a string equal to
     *          {@code "null"}; otherwise, the value of
     *          {@code obj.toString()} is returned.
     * @see     java.lang.Object#toString()
     */
    public static String valueOf(Object obj) {
        return (obj == null) ? "null" : obj.toString();
    }

```

源码很简单，如果对象为空，就返回字符串的"null"...不为空就调用toString方法。

再来说第二个：

第二个和第一个的不同，是java对重载的不同处理导致的。

基本类型不能接受null入参，所以接受入参的是对象类型，如下两个：

String valueOf(Object obj)

String valueOf(char data[])

这两个都能接受null入参，这种情况下，java的重载会选取其中更精确的一个，所谓精确就是，重载方法A和B，如果方法A的入参是B的入参的子集，则，A比B更精确，重载就会选择A。换成上面这两个就是，char[]入参的比object的更精确，因为object包含char[]，所以String.valueOf(null)是用char[]入参这个重载方法。

看看这个方法的实现：

```java

    /**
     * Returns the string representation of the {@code char} array
     * argument. The contents of the character array are copied; subsequent
     * modification of the character array does not affect the returned
     * string.
     *
     * @param   data     the character array.
     * @return  a {@code String} that contains the characters of the
     *          character array.
     */
    public static String valueOf(char data[]) {
        return new String(data);
    }

```

直接new String的，再看new String的实现：

```java

    /**
     * Allocates a new {@code String} so that it represents the sequence of
     * characters currently contained in the character array argument. The
     * contents of the character array are copied; subsequent modification of
     * the character array does not affect the newly created string.
     *
     * @param  value
     *         The initial value of the string
     */
    public String(char value[]) {
        this.value = Arrays.copyOf(value, value.length);
    }

```

value.length 时出现java.lang.NullPointerException

JDK中的奇葩实现比较多，大家用的时候养成多看源码实现的好习惯，可以避免踩坑...

如果大家还有见到什么奇葩实现，热烈欢迎留言讨论，哈哈。