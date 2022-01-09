## Mockito与PowerMock的使用基础教程

【转载于https://juejin.cn/post/6844903711483887623】

### 一、Mockito与PowerMock简述

    Mockito与PowerMock都是Java流行的一种Mock框架，使用Mock技术能让我们隔离外部依赖以便对我们自己的业务逻辑代码进行单元测试，在编写单元测试时，不需要再进行繁琐的初始化工作，在需要调用某一个接口时，直接模拟一个假方法，并任意指定方法的返回值。     Mockito的工作原理是通过创建依赖对象的proxy，所有的调用先经过proxy对象，proxy对象拦截了所有的请求再根据预设的返回值进行处理。PowerMock则在Mockito原有的基础上做了扩展，通过修改类字节码并使用自定义ClassLoader加载运行的方式来实现mock静态方法、final方法、private方法、系统类的功能。   从两者的项目结构中就可以看出，PowerMock直接依赖于Mockito，所以如果项目中已经导入了PowerMock包就不需要再单独导入Mockito包，如果两者同时导入还要小心PowerMock和Mockito不同版本之间的兼容问题：

1. Mockito包依赖：

```xml
<dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>2.23.0</version>
        <scope>test</scope>
</dependency>
```

2. PowerMock包依赖：

```xml
<dependency>
        <groupId>org.powermock</groupId>
        <artifactId>powermock-module-junit4</artifactId>
        <version>2.0.0-RC.3</version>
        <scope>test</scope>
</dependency>
<dependency>
        <groupId>org.powermock</groupId>
        <artifactId>powermock-api-mockito2</artifactId>
        <version>2.0.0-RC.3</version>
        <scope>test</scope>
</dependency>
```

3. 官方文档
   - [mockito官方github](https://github.com/mockito/mockito)
   - [powermock官方github](https://github.com/powermock/powermock)

### 二、Mockito的使用

    Mockito一般通过创建mock或spy对象，并制定具体返回规则来实现模拟的功能，在调用完成后还可以进行方法调用验证以检验程序逻辑是否正确。mock和spy对象的区别是mock对象对于未指定处理规则的调用会按方法返回值类型返回该类型的默认值（如int、long则返回0，boolean则返回false，对象则返回null，void则什么都不做），而spy对象在未指定处理规则时则会直接调用真实方法。

以下3个类是我们的项目中需要用到的一些业务类：

```java
//实体类
public class Node {
    private int num;
    private String name;

    //以下忽略所有构造方法和get、set方法
}

//本地负责实现具体业务的业务类
public class LocalServiceImpl implements ILocalService {

    //外部依赖
    @Autowired
    private IRemoteService remoteService;

    //具体业务处理方法
    @Override
    public Node getRemoteNode(int num) {
        return remoteService.getRemoteNode(num);
    }
    //以下忽略其他业务调用方法，在后面例子中补充
}

//外部依赖业务类，由其他人实现，可能我们的业务类写好了别人还没写好
public class RemoteServiceImpl implements IRemoteService {
    //外部类提供的一些业务方法
    @Override
    public Node getRemoteNode(int num) {
        return new Node(num, "Node from remote service");
    }
    //其他业务方法在后面例子中补充
}
```

下面是Mockito具体使用的一些示例：

1. cmock外部依赖对象，并注入到我们的业务类中，以便在单元测试中进行模拟调用：

```java
@RunWith(MockitoJUnitRunner.class) //让测试运行于Mockito环境
public class LocalServiceImplMockTest {

    @InjectMocks    //此注解表示这个对象需要被注入mock对象
    private LocalServiceImpl localService;
    @Mock   //此注解会自动创建1个mock对象并注入到@InjectMocks对象中
    private RemoteServiceImpl remoteService;

    //如果不使用上述注解，可以使用@Before方法来手动进行mock对象的创建和注入，但会几行很多代码
    /*
    private LocalServiceImpl localService;
    private RemoteServiceImpl remoteService;

    @Before
    public void setUp() throws Exception {
        localService = new LocalServiceImpl();
        remoteService = Mockito.mock(RemoteServiceImpl.class);  //创建Mock对象
        Whitebox.setInternalState(localService, "remoteService", remoteService); //注入依赖对象
    }
    */

    @Test
    public void testMock() {
        Node target = new Node(1, "target");    //创建一个Node对象作为返回值
        Mockito.when(remoteService.getRemoteNode(1)).thenReturn(target); //指定当remoteService.getRemoteNode(int)方法传入参数为1时返回target对象
        Node result = localService.getRemoteNode(1);    //调用我们的业务方法，业务方法内部调用依赖对象方法
        assertEquals(target, result);   //可以断言我们得到的返回值其实就是target对象
        assertEquals(1, result.getNum());   //具体属性和我们指定的返回值相同
        assertEquals("target", result.getName());   //具体属性和我们指定的返回值相同

        Node result2 = localService.getRemoteNode(2);   //未指定参数为2时对应的返回规则
        assertNull(result2);    //未指定时返回为null
    }
}
```

2. spy外部依赖对象，并注入到我们的业务类中：

```java
@RunWith(MockitoJUnitRunner.class)
public class LocalServiceImplSpyTest {

    @InjectMocks
    private LocalServiceImpl localService;
    @Spy    //注意这里使用的是@Spy注解
    private RemoteServiceImpl remoteService;
    //注意如果自己创建spy对象的话要这么写：
    /*
        remoteService = new RemoteServiceImpl();    //先创建一个具体实例
        remoteService = Mockito.spy(remoteService);   //再调用Mockito.spy(T)方法创建spy对象
    */

    @Test
    public void testSpy() {
        Node target = new Node(1, "target");    //创建一个Node对象作为返回值
        Mockito.when(remoteService.getRemoteNode(1)).thenReturn(target); //指定当remoteService.getRemoteNode(int)方法传入参数为1时返回target对象
        Node result = localService.getRemoteNode(1);    //调用我们的业务方法，业务方法内部调用依赖对象方法
        assertEquals(target, result);   //可以断言我们得到的返回值其实就是target对象
        assertEquals(1, result.getNum());   //具体属性和我们指定的返回值相同
        assertEquals("target", result.getName());   //具体属性和我们指定的返回值相同

        Node result2 = localService.getRemoteNode(2);   //未指定参数为2时的调用规则，所以会直接调用真实对象，返回remote创建的节点
        assertEquals(2, result2.getNum());
        assertEquals("Node from remote service", result2.getName());    //remoteService创建Node对象时设置name属性为"Node from remote service"
    }
}
```

3. 使用ArgumentMatchers的any系列方法指定多种返回值，有any()、anyInt()、anyString()、anyByte()、anyLong()等等，可以看下ArgumentMatchers类源码中定义的所有方法：

```java
    @Test
    public void testAny() {
        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(anyInt())).thenReturn(target); //静态导入Mockito.when和ArgumentMatchers.anyInt后可以简化代码提升可读性

        Node result = localService.getRemoteNode(20); //上面指定了调用remoteService.getRemoteNode(int)时，不管传入什么参数都会返回target对象
        assertEquals(target, result);   //可以断言我们得到的返回值其实就是target对象
        assertEquals(1, result.getNum());   //具体属性和我们指定的返回值相同
        assertEquals("target", result.getName());   //具体属性和我们指定的返回值相同
    }
```

4. 指定mock对象多次调用的返回值：

```java
    /**
     * 指定mock多次调用返回值
     */
    @Test
    public void testMultipleReturn() {
        Node target1 = new Node(1, "target");
        Node target2 = new Node(1, "target");
        Node target3 = new Node(1, "target");
        when(remoteService.getRemoteNode(anyInt())).thenReturn(target1).thenReturn(target2).thenReturn(target3);
        //第一次调用返回target1、第二次返回target2、第三次返回target3

        Node result1 = localService.getRemoteNode(1); //第1次调用
        assertEquals(target1, result1);
        Node result2 = localService.getRemoteNode(2); //第2次调用
        assertEquals(target2, result2);
        Node result3 = localService.getRemoteNode(3); //第3次调用
        assertEquals(target3, result3);
    }
```

5. 指定mock对象抛出异常（注意如果方法中未声明会抛出异常，只能指定抛出运行时异常，如果仍指定为抛出受检查异常，运行时会报错误org.mockito.exceptions.base.MockitoException: Checked exception is invalid for this method!）：

```jade
    //RemoteServiceImpl方法：
    @Override
    public Node getRemoteNode(String name) throws MockException {
        if (StringUtils.isEmpty(name)) {
            throw new MockException("name不能为空", name);
        }
        return new Node(name);
    }

    //LocalServiceImpl方法
    @Override
    public Node getRemoteNode(String name) throws MockException {
        try {
            return remoteService.getRemoteNode(name);
        } catch (IllegalArgumentException e) {
            throw e;
        }
    }

    /**
     * 指定mock对象已声明异常抛出的方法抛出受检查异常
     */
    @Test
    public void testExceptionDeclare() {
        try {
            Node target = new Node(1, "target");
            when(remoteService.getRemoteNode("name")).thenReturn(target).thenThrow(new MockException(
                    "message", "exception")); //第一次调用正常返回，第二次则抛出一个Exception

            Node result1 = localService.getRemoteNode("name");
            assertEquals(target, result1); //第一次调用正常返回

            Node result2 = localService.getRemoteNode("name"); //第二次调用不会正常返回，会抛出异常
            assertEquals(target, result2);
        } catch (MockException e) {
            assertEquals("exception", e.getName()); //验证是否返回指定异常内容
            assertEquals("message", e.getMessage()); //验证是否返回指定异常内容
        }
    }

    /**
     * 指定mock对象为声明异常抛出的方法抛出运行时异常
     */
    @Test
    public void testRuntimeException() {
        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(1)).thenThrow(new RuntimeException("exception")); //指定调用时抛出一个运行时异常

        try {
            Node result = localService.getRemoteNode(1);
            assertEquals(target, result);
        } catch (RuntimeException e) {
            assertEquals("exception", e.getMessage());
        }
    }

    /**
     * 指定mock对象未声明异常抛出的方法抛出受检查异常，以下方法执行会报错
     */
    @Test
    public void testNotDefineCheckedException() {
        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(1)).thenThrow(new IOException("io exception"));

        try {
            Node result = localService.getRemoteNode(1);
            assertEquals(target, result);
        } catch (Exception e) {
            assertEquals("io exception", e.getMessage());
        }
    }
```

6. mock void方法抛异常、什么都不做：

```
    //RemoteServiceImpl方法：
    @Override
    public void doSometing() {
        System.out.println("remote service do something!");
    }

    //LocalServiceImpl方法
    @Override
    public void remoteDoSomething() {
        remoteService.doSometing();
    }

    //注意void方法没有返回值，所以mock规则写法顺序不一样
    doNothing().when(remoteService).doSometing();
    doThrow(new RuntimeException("exception")).when(remoteService).doSometing();
复制代码
```

7. 校验mock对象的调用情况（除Mockito中的never()、times(int)方法外，还有atLeast(int)、atLeastOne()、atMost(int)等方法）：

```
   /**
     * 校验mock对象和方法的调用情况
     *
     */
    public void testVerify() {
        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(anyInt())).thenReturn(target);

        verify(remoteService, never()).getRemoteNode(1); //mock方法未调用过

        localService.getRemoteNode(1);
        Mockito.verify(remoteService, times(1)).getRemoteNode(anyInt()); //目前mock方法调用过1次

        localService.getRemoteNode(2);
        verify(remoteService, times(2)).getRemoteNode(anyInt()); //目前mock方法调用过2次
        verify(remoteService, times(1)).getRemoteNode(2); //目前mock方法参数为2只调用过1次
    }
复制代码
```

8. 利用ArgumentCaptor捕获方法参数进行mock方法参数校验

```
    /**
     * 利用ArgumentCaptor捕获方法参数进行mock方法参数校验
     */
    @Test
    public void testCaptor() throws Exception {
        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(anyString())).thenReturn(target);

        localService.getRemoteNode("name1");
        localService.getRemoteNode("name2");
        verify(remoteService, atLeastOnce()).getRemoteNode(localCaptor.capture()); //设置captor

        assertEquals("name2", localCaptor.getValue()); //获取最后一次调用的参数
        List<String> list = localCaptor.getAllValues(); //按顺序获取所有传入的参数
        assertEquals("name1", list.get(0));
        assertEquals("name2", list.get(1));
    }
复制代码
```

9. mock对象调用真实方法：

```
    /**
     * mock对象调用真实方法
     */
    @Test
    public void testCallRealMethod() {
        when(remoteService.getRemoteNode(anyInt())).thenCallRealMethod(); //设置调用真实方法
        Node result = localService.getRemoteNode(1);

        assertEquals(1, result.getNum());
        assertEquals("Node from remote service", result.getName());
    }
复制代码
```

10. 重置mock对象：

```
    //重置mock，清除所有的调用记录和返回规则
    Mockito.reset(remoteService);
复制代码
```

11. 校验mock对象0调用和未被验证的调用

```java
    /**
     * 校验mock对象0调用和未被验证的调用
     */
    @Test(expected = NoInteractionsWanted.class)
    public void testInteraction() {
        verifyZeroInteractions(remoteService); //目前还未被调用过，执行不报错

        Node target = new Node(1, "target");
        when(remoteService.getRemoteNode(anyInt())).thenReturn(target);

        localService.getRemoteNode(1);
        localService.getRemoteNode(2);
        verify(remoteService, times(2)).getRemoteNode(anyInt());
        // 参数1和2的两次调用都会被上面的anyInt()校验到，所以没有未被校验的调用了
        verifyNoMoreInteractions(remoteService);

        reset(remoteService);
        localService.getRemoteNode(1);
        localService.getRemoteNode(2);
        verify(remoteService, times(1)).getRemoteNode(1);
        // 参数2的调用不会被上面的校验到，所以执行会抛异常
        verifyNoMoreInteractions(remoteService);
    }
```

### 三、PowerMock的使用

PowerMock的使用与Mockito有一些不同，首先是测试类上的@RunWith注解需要修改为：

```
@RunWith(PowerMockRunner.class)
复制代码
```

第二是需要使用到@PrepareForTest注解（PrepareFotTest注解会修改传入参数类的字节码，通过修改字节码达到模拟final、static、私有方法、系统类等的功能），此注解可写在类上也可写在方法上：

```
@PrepareForTest(RemoteServiceImpl.class)
复制代码
```

1. mock new关键字

```java
    //LocalServiceImpl
    @Override
    public Node getLocalNode(int num, String name) {
        return new Node(num, name);
    }

    /**
     * mock new关键字
     */
    @Test
    @PrepareForTest(LocalServiceImpl.class) //PrepareForTest修改local类的字节码以覆盖new的功能
    public void testNew() throws Exception {
        Node target = new Node(1, "target");
        //当传入任意int且name属性为"name"时，new对象返回为target
        //当参数条件使用了any系列方法时，剩余的参数都得使用相应的模糊匹配规则，如eq("name")代表参数等于"name"
        //剩余还有isNull(), isNotNull(), isA()等方法
        PowerMockito.whenNew(Node.class).withArguments(anyInt(), eq("name")).thenReturn(target);
        Node result = localService.getLocalNode(2, "name");
        assertEquals(target, result); //返回值为target
        assertEquals(1, result.getNum());
        assertEquals("target", result.getName());

        //未指定name为"test"的返回值，默认返回null
        Node result2 = localService.getLocalNode(1, "test");
        assertNull(result2);
    }
```

2. mock final方法

```jade
    //RemoteServiceImpl
    @Override
    public final Node getFinalNode() {
        return new Node(1, "final node");
    }

    /**
     * mock final方法
     */
    @Test
    @PrepareForTest(RemoteServiceImpl.class) //final方法在RemoteServiceImpl类中
    public void testFinal() {
        Node target = new Node(2, "mock");
        PowerMockito.when(remoteService.getFinalNode()).thenReturn(target); //指定返回值

        Node result = remoteService.getFinalNode(); //直接调用final方法，返回mock后的值
        assertEquals(target, result); //验证返回值
        assertEquals(2, result.getNum());
        assertEquals("mock", result.getName());
    }
```

3. mock static方法

```
    //Node
    public static Node getStaticNode() {
        return new Node(1, "static node");
    }

    /**
     * mock static方法
     */
    @Test
    @PrepareForTest(Node.class) //static方法定义在Node类中
    public void testStatic() {
        Node target = new Node(2, "mock");
        PowerMockito.mockStatic(Node.class); //mock static方法前需要加这一句
        PowerMockito.when(Node.getStaticNode()).thenReturn(target); //指定返回值

        Node result = Node.getStaticNode(); //直接调用static方法，返回mock后的值
        assertEquals(target, result); //验证返回值
        assertEquals(2, result.getNum());
        assertEquals("mock", result.getName());
    }
```

4. mock private方法

```
    //RemoteServiceImpl
    @Override
    public Node getPrivateNode() {
        return privateMethod();
    }

    //RemoteServiceImpl
    private Node privateMethod() {
        return new Node(1, "private node");
    }

    /**
     * mock 私有方法
     */
    @Test
    @PrepareForTest(RemoteServiceImpl.class) //private方法定义在RemoteServiceImpl类中
    public void testPrivate() throws Exception {
        Node target = new Node(2, "mock");
        //按照真实代码调用privateMethod方法
        PowerMockito.when(remoteService.getPrivateNode()).thenCallRealMethod();
        //私有方法无法访问，类似反射传递方法名和参数，此处无参数故未传
        PowerMockito.when(remoteService, "privateMethod").thenReturn(target);

        Node result = remoteService.getPrivateNode();
        assertEquals(target, result); //验证返回值
        assertEquals(2, result.getNum());
        assertEquals("mock", result.getName());
    }
```

5. mock 系统类方法

```java
    //RemoteServiceImpl
    @Override
    public Node getSystemPropertyNode() {
        return new Node(System.getProperty("abc"));
    }

    /**
     * mock 系统类方法
     */
    @Test
    @PrepareForTest(RemoteServiceImpl.class) //类似new关键字，系统类方法的调用在类RemoteServiceImpl中，所以这里填的是RemoteServiceImpl
    public void testSystem() {
        PowerMockito.mockStatic(System.class); //调用的是系统类的静态方法，所以要加这一句
        PowerMockito.when(System.getProperty("abc")).thenReturn("mock"); //设置System.getProperty("abc")返回"mock"
        PowerMockito.when(remoteService.getSystemPropertyNode()).thenCallRealMethod(); //设置mock对象调用实际方法

        Node result = remoteService.getSystemPropertyNode(); //按代码会返回一个name属性为"mock"的对象
        assertEquals(0, result.getNum()); //int默认值为0
        assertEquals("mock", result.getName()); //remoteService对象中调用System.getProperty("abc")返回的是上面设置的"mock"
    }
```