## CGlib动态代理实战分析

#### 概览

- [官方github](https://github.com/cglib/cglib/wiki)

#### 测试CGLib动态代理

```java
package com.ethen.proxy.dynamic.cglib;

import com.ethen.common.model.Order;
import com.ethen.common.service.OrderService;
import com.ethen.common.service.impl.OrderServiceImpl;
import net.sf.cglib.proxy.Enhancer;
import org.junit.Test;

import java.util.List;

public class CglibTest {

  @Test
  public void testInterceptor() {
    // 设置代理类class文件保存位置
    CgLibUtil.enableSaveProxyFiles("D:/tmp/created/cglib/");

    // 增强器用来创建代理类
    Enhancer enhancer = new Enhancer();
    // 指定被代理的类
    enhancer.setSuperclass(OrderServiceImpl.class);
    CgLibMethodInterceptor cgLibMethodInterceptor = new CgLibMethodInterceptor();
    enhancer.setCallback(cgLibMethodInterceptor);
    OrderService orderService = (OrderServiceImpl) enhancer.create();

    // 调用代理对象的目标方法
    List<Order> orderList = orderService.selectOrderById("cglib-123123123");
    System.err.println(orderList);
  }
}
```

#### 保存CGLib生成的代理类class文件

```java
package com.ethen.proxy.dynamic.cglib;

import net.sf.cglib.core.DebuggingClassWriter;

import java.lang.reflect.Field;
import java.util.Properties;

public class CgLibUtil {
  /**
   * 保存CGLib生成的代理类
   *
   * @param dir 存放目录
   */
  public static void enableSaveProxyFiles(String dir) {
    try {
      Field field = System.class.getDeclaredField("props");
      field.setAccessible(true);
      Properties props = (Properties) field.get(null);
      System.setProperty(DebuggingClassWriter.DEBUG_LOCATION_PROPERTY, dir);
      props.put("net.sf.cglib.core.DebuggingClassWriter.traceEnabled", "true");
    } catch (NoSuchFieldException | IllegalAccessException e) {
      e.printStackTrace();
    }
  }
}
```

#### 代理类实例

![image-20220123215402458](/docs/java-core/imgs/image-20220123215402458.png)

**com.ethen.common.service.impl.OrderServiceImpl$$EnhancerByCGLIB$$b2ed5fca@61d47554**

#### 调用链路分析

持续更新...

#### 参考资料

- [总算有人把动态代理、CGlib、AOP都说清楚了！](https://cloud.tencent.com/developer/article/1461796)
- [通俗的方式分析CGLib动态代理](https://blog.csdn.net/qq_36756682/article/details/108422693)

