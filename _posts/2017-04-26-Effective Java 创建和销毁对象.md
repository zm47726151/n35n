### 本章的主题是创建和销毁对象：如何创建对象、如何避免创建对象、如何确保它们适时的销毁已经如何管理对象销毁之前的必须进行清理的动作

> * 考虑用静态工厂的方法代替构造器。
> * 遇到多个构造器参数(4个以上)时要考虑用构建器。
> * 通过私有构造器强化不可实例的能力。
> * 避免创建不必要的对象。
> * 消除过期的对象引用。
> * 避免使用终结方法。

### 1、考虑用静态工厂的方法代替构造器
优点：

> * 有名字
> * 不必每次创建对象
> * 返回任何子类型对象，简洁的代码。

缺点：

> * 该类将不能被子类化（复合大于继承，也是优点）
> * 不方便doc工具输出文档。

一般约定的命名规则:

> * valueOf  转换类型
> * getInstance 获得对象实例
> * newInstance 创建新的对象实例
> * getType 获得返回对象的类型
> * newType 置入返回对象的类型，在不同类中方便区别工厂方法

###示例代码：

服务提供者

```java
// Service provider framework sketch - Service provider interface - Page 12
public interface Provider {
    Service newService();
}
```

服务

```java
// Service provider framework sketch - Service interface - Page 12

public interface Service {
    // Service-specific methods go here
}
```

服务工厂

```java
import java.util.*;
import java.util.concurrent.*;

public class Services {
	private Services() {
	} // Prevents instantiation (Item 4)

	// Maps service names to services
	private static final Map<String, Provider> providers = new ConcurrentHashMap<String, Provider>();
	public static final String DEFAULT_PROVIDER_NAME = "<def>";

	// Provider registration API
	// 注册默认服务提供者
	public static void registerDefaultProvider(Provider p) {
		registerProvider(DEFAULT_PROVIDER_NAME, p);
	}

	// 根据name注册服务提供者
	public static void registerProvider(String name, Provider p) {
		providers.put(name, p);
	}

	// Service access API
	// 获取默认服务提供者
	public static Service newInstance() {
		return newInstance(DEFAULT_PROVIDER_NAME);
	}

	// 根据name获取服务提供者
	public static Service newInstance(String name) {
		Provider p = providers.get(name);
		if (p == null)
			throw new IllegalArgumentException("No provider registered with name: " + name);
		return p.newService();
	}
}
```

测试代码

```java
public class Test {
	public static void main(String[] args) {
		// Providers would execute these lines
		Services.registerDefaultProvider(DEFAULT_PROVIDER); // 注册默认服务
		Services.registerProvider("comp", COMP_PROVIDER);	// 注册comp服务
		Services.registerProvider("armed", ARMED_PROVIDER); // 注册armed服务

		// Clients would execute these lines
		Service s1 = Services.newInstance();
		Service s2 = Services.newInstance("comp");
		Service s3 = Services.newInstance("armed");
		System.out.printf("%s, %s, %s%n", s1, s2, s3);
	}

	// 默认服务
	private static Provider DEFAULT_PROVIDER = new Provider() {
		public Service newService() {
			return new Service() {
				@Override
				public String toString() {
					return "Default service";
				}
			};
		}
	};

	// como 服务
	private static Provider COMP_PROVIDER = new Provider() {
		public Service newService() {
			return new Service() {
				@Override
				public String toString() {
					return "Complementary service";
				}
			};
		}
	};

	// Armed 服务
	private static Provider ARMED_PROVIDER = new Provider() {
		public Service newService() {
			return new Service() {
				@Override
				public String toString() {
					return "Armed service";
				}
			};
		}
	};
}
```

### 2、遇到多个构造函数参数时要考虑使用构建器
### 3、用私有构造函数强化singleton属性
### 4、通过私有构造函数强化不可实例化的能力
### 5、避免创建不必要的对象
### 6、消除过期的对象引用
### 7、避免使用终结方法