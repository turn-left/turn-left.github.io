## Spring Bean的生命周期

#### Bean的创建

扫描 -> .class -> 推断构造方法 -> 普通对象 -> 依赖注入(属性赋值) -> 初始化前(@PostConstruct) -> 初始化(InitializingBean) -> 初始化后(AOP) -> 代理对象 ->
Bean

#### Bean的销毁

#### 循环依赖

#### 三级缓存