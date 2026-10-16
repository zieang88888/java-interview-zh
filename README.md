# ☕ Java 面试 200 问（中文带答案）

> Java 面试一站通关：200 道高频面试题全中文带答案，基础/进阶/实战三级分级，从 JVM 到并发到 Spring 再到微服务，一册在手，Java 岗面试无忧。

![stars](https://img.shields.io/badge/⭐-给个Star吧-red)
![license](https://img.shields.io/badge/license-MIT-blue)
![status](https://img.shields.io/badge/status-持续更新-green)

## 为什么需要这份题库？

你是不是也有这样的经历：

- 八股文背了一堆，面试时被问**底层原理**直接卡壳？
- 网上搜 Java 面试题，**要么是英文的、要么只有题目没答案**？
- JVM、并发、Spring、MySQL、Redis……**考点太多不知道抓哪头**？

**Java 面试，拼的不是背题数量，而是理解深度。**

一个"HashMap 的原理"就能从散列表问到红黑树问到扩容，问到底层；一个"JVM 内存模型"能问掉半条命。

这份题库把 Java 面试的**高频考点一次性整理全**：

- ✅ **200 道高频题**：覆盖面试 90% 以上的考点
- ✅ **全中文带答案**：每道题都有标准答案+解析
- ✅ **三级分级**：基础（必考）/进阶（拉差距）/实战（拿 offer）
- ✅ **真实代码示例**：不是空谈理论，直接看代码
- ✅ **持续更新**：紧跟 Java 21+ 新特性

## 📚 题库结构

### 第一篇：基础篇（80 题，必考区）

#### 一、Java 基础（20 题）

**1. Java 和 C++ 的区别？**

**答案要点：**
- 内存管理：Java 自动垃圾回收，C++ 手动管理
- 跨平台：Java 靠 JVM 一次编译到处运行，C++ 需平台编译
- 多继承：Java 单继承多接口，C++ 支持多继承
- 指针：Java 无指针（引用代替），C++ 有指针
- 性能：C++ 更快，Java 开发效率更高

**2. 什么是 JDK、JRE、JVM？**

**答案要点：**
- JDK（Java Development Kit）：开发工具包，包含 JRE 和编译器等
- JRE（Java Runtime Environment）：运行环境，包含 JVM 和类库
- JVM（Java Virtual Machine）：Java 虚拟机，负责执行字节码
- 关系：JDK ⊃ JRE ⊃ JVM

**3. `==` 和 `equals()` 的区别？**

**答案要点：**
- `==` 比较引用地址（基本类型比较值）
- `equals()` 默认比较地址，重写后比较内容
- String 的 equals 已重写，比较内容
```java
String a = new String("abc");
String b = new String("abc");
System.out.println(a == b);        // false（地址不同）
System.out.println(a.equals(b));   // true（内容相同）
```

**4. `String`、`StringBuffer`、`StringBuilder` 的区别？**

**答案要点：**
- String：不可变，每次修改创建新对象
- StringBuffer：可变，线程安全（方法加 synchronized），性能较差
- StringBuilder：可变，线程不安全，性能最好
- 单线程用 StringBuilder，多线程共享用 StringBuffer

**5. 重载和重写的区别？**

**答案要点：**
- 重载（Overload）：同一个类中方法名相同、参数不同，编译期决定
- 重写（Override）：子类重写父类方法，方法签名相同，运行期决定（多态）

**6. 什么是反射？有什么优缺点？**

**答案要点：**
- 反射：运行期动态获取类的信息（类名、方法、字段）并操作
- 优点：灵活性高，实现动态代理、Spring IOC
- 缺点：性能开销大、破坏封装、安全风险
```java
Class<?> clazz = Class.forName("com.example.User");
Method method = clazz.getMethod("getName");
```

**7. 什么是注解？常见注解有哪些？**

**答案要点：** 注解是给代码打标签，供编译期或运行期处理。常见：`@Override`（重写校验）、`@Deprecated`（废弃标记）、`@SuppressWarnings`（抑制警告）、`@FunctionalInterface`（函数式接口）。框架层面：`@Component`、`@Autowired`、`@RestController`。

**8. 什么是泛型？为什么要用？**

**答案要点：** 泛型让类型在编译期确定，提高类型安全（避免运行时 ClassCastException）、减少强制类型转换。如 `List<String>`。泛型擦除：编译后类型信息被擦除为 Object。

**9. 自动装箱和拆箱？**

**答案要点：**
- 装箱：基本类型 → 包装类型（`Integer.valueOf()`）
- 拆箱：包装类型 → 基本类型（`intValue()`）
- 陷阱：`Integer` 缓存 -128~127，`==` 比较在此范围返回 true
```java
Integer a = 127, b = 127;
System.out.println(a == b);  // true（缓存）
Integer c = 128, d = 128;
System.out.println(c == d);  // false（超出缓存）
```

**10. `final` 关键字的作用？**

**答案要点：**
- 修饰类：不可继承
- 修饰方法：不可重写
- 修饰变量：不可修改（引用不可变，对象内容可变）
- 注意：`final` 数组/集合对象内容仍可改

（以下 10 题见仓库完整版）

#### 二、集合框架（20 题）

**21. ArrayList 和 LinkedList 的区别？**

**答案要点：**
- 底层：ArrayList 动态数组，LinkedList 双向链表
- 查询：ArrayList O(1) 按索引，LinkedList O(n)
- 插入删除：ArrayList 尾部 O(1)/中间 O(n)，LinkedList O(1)（已定位）
- 内存：ArrayList 连续内存，LinkedList 节点分散（更耗内存）

**22. HashMap 的实现原理？**

**答案要点：**
- 底层：数组 + 链表 + 红黑树（JDK 8+）
- 流程：计算 hash → 定位桶 → 冲突链式存储 → 链表长度 >8 且数组 ≥64 转红黑树
- 扩容：默认负载因子 0.75，容量翻倍，rehash
- 线程不安全：并发 put 可能死循环（JDK 7）/ 丢数据（JDK 8）

**23. HashMap 和 Hashtable 的区别？**

**答案要点：**
- 线程安全：Hashtable 安全（synchronized），HashMap 不安全
- 允许 null：HashMap 允许一个 null key 和多个 null value，Hashtable 不允许
- 初始容量：HashMap 16，Hashtable 11
- Hashtable 已废弃，用 ConcurrentHashMap 代替

**24. ConcurrentHashMap 的实现原理？**

**答案要点：**
- JDK 7：分段锁（Segment 数组，每段一把锁）
- JDK 8：CAS + synchronized 锁单个桶，锁粒度更细
- 读操作无锁（volatile 保证可见性）
- size() 用 baseCount + CounterCell 累加，并发时统计可能不精确

**25. HashSet 的实现原理？**

**答案要点：** HashSet 底层就是 HashMap，value 用固定 Object（PRESENT）。元素不可重复、无序、允许一个 null。去重依赖 hashCode 和 equals。

**26. 什么是 fail-fast 和 fail-safe？**

**答案要点：**
- fail-fast：迭代时修改集合抛 ConcurrentModificationException（ArrayList 等，用 modCount 检测）
- fail-safe：迭代的是副本，不抛异常（CopyOnWriteArrayList、ConcurrentHashMap）

（以下 14 题见仓库完整版）

#### 三、异常与 IO（20 题）

**41. Java 的异常体系？**

**答案要点：**
- Throwable 分 Error（JVM 级，OOM/StackOverflow）和 Exception
- Exception 分受检异常（Checked：IOException、SQLException，必须处理）和运行时异常（RuntimeException：NPE、IndexOutOfBounds，可不处理）

**42. try-catch-finally 和 try-with-resources？**

**答案要点：**
- finally 无论是否异常都执行（return 也会执行，除非 System.exit）
- finally 里 return 会覆盖 try 的 return
- try-with-resources：自动关闭资源，实现 AutoCloseable

**43. 什么是 BIO、NIO、AIO？**

**答案要点：**
- BIO：阻塞 IO，一个连接一个线程
- NIO：非阻塞 IO，Selector 多路复用，少量线程处理大量连接
- AIO：异步 IO，回调通知，目前 Java 中较少用（Netty 用的是 NIO）

（以下 17 题见仓库完整版）

### 第二篇：进阶篇（80 题，拉差距区）

#### 四、JVM（20 题）

**61. JVM 内存模型（运行时数据区）？**

**答案要点：**
- 线程私有：虚拟机栈、本地方法栈、程序计数器
- 线程共享：堆（对象实例）、方法区/元空间（类信息、常量）
- 直接内存（NIO 用）：不属于 JVM 内存

**62. 堆内存如何分区？**

**答案要点：**
- 新生代：Eden + 2 个 Survivor（8:1:1），对象优先在 Eden 分配
- 老年代：大对象、长期存活对象（年龄 ≥15 进入）
- 垃圾回收：Minor GC 回收新生代，Major/Full GC 回收老年代+新生代

**63. 什么是 GC Roots？**

**答案要点：** 可达性分析的根节点：栈帧局部变量、静态变量、常量引用、JNI 引用、活跃线程。从 GC Roots 出发不可达的对象可被回收。

**64. 垃圾回收算法有哪些？**

**答案要点：**
- 标记-清除：有碎片
- 标记-复制：无碎片，浪费一半空间（新生代用）
- 标记-整理：无碎片，效率低（老年代用）
- 分代收集：新生代复制，老年代标记整理

**65. 常见的垃圾收集器？**

**答案要点：**
- Serial/Parallel：老古董
- CMS：并发标记清除，追求低停顿（已废弃）
- G1：分区式，可预测停顿，默认收集器
- ZGC：超低停顿（毫秒级），超大堆

**66. 什么是类加载机制？双亲委派？**

**答案要点：**
- 生命周期：加载 → 验证 → 准备 → 解析 → 初始化
- 双亲委派：类加载请求先给父加载器，父加载不了才自己加载
- 好处：避免核心类被篡改（Object 永远由 Bootstrap 加载）、避免重复加载
- 打破双亲委派：Tomcat、SPI（JDBC）

**67. JVM 调优你会怎么做？**

**答案要点：**
- 先监控：jstat/jmap/jstack/arthas 找问题
- 堆配置：-Xms=-Xmx 避免扩容抖动
- GC 选择：大堆用 G1/ZGC，小堆用 Parallel
- 优化代码：减少大对象、避免内存泄漏（连接未关、静态集合）

（以下 13 题见仓库完整版）

#### 五、并发编程（20 题）

**81. synchronized 的实现原理？**

**答案要点：**
- 基于监视器锁（Monitor），对象头中的 Mark Word 记录锁状态
- 锁升级：无锁 → 偏向锁 → 轻量级锁（CAS 自旋）→ 重量级锁（Monitor）
- 可重入：同一线程可重复获取
- 保证：原子性、可见性（happens-before）、有序性

**82. volatile 的作用？**

**答案要点：**
- 可见性：修改立即可见（写后读，通过缓存一致性/内存屏障）
- 有序性：禁止指令重排序
- 不保证原子性：i++ 仍需 synchronized/AtomicInteger
- 适用：状态标志位、单例双重检查锁

**83. JMM（Java 内存模型）是什么？**

**答案要点：** 定义线程与主内存的交互规则：所有变量存主内存，线程工作内存保存副本。保证三大特性：原子性（锁）、可见性（volatile）、有序性（happens-before 规则）。

**84. 线程池的核心参数？**

**答案要点：**
- corePoolSize：核心线程数
- maximumPoolSize：最大线程数
- keepAliveTime：非核心线程空闲存活时间
- workQueue：任务队列（ArrayBlockingQueue/LinkedBlockingQueue/SynchronousQueue）
- ThreadFactory：线程工厂
- RejectedExecutionHandler：拒绝策略（Abort/CallerRuns/Discard/DiscardOldest）

**85. 线程池执行流程？**

**答案要点：** 提交任务 → 核心线程未满直接创建 → 满了进队列 → 队列满了创建非核心线程 → 达到最大线程数走拒绝策略。

**86. 为什么不建议用 Executors 创建线程池？**

**答案要点：**
- FixedThreadPool/SingleThread：无界队列，OOM 风险
- CachedThreadPool：最大线程数 Integer.MAX_VALUE，OOM 风险
- 推荐：ThreadPoolExecutor 手动创建，明确参数

**87. CountDownLatch 和 CyclicBarrier 的区别？**

**答案要点：**
- CountDownLatch：一个线程等 N 个线程完成，一次性
- CyclicBarrier：N 个线程互相等待到齐，可循环复用
- 语义：Latch 是"放行"，Barrier 是"集合"

（以下 13 题见仓库完整版）

#### 六、Spring 全家桶（20 题）

**101. Spring 和 Spring Boot 的区别？**

**答案要点：**
- Spring：核心是 IOC + AOP，配置复杂（XML/Java Config）
- Spring Boot：自动配置、起步依赖、内嵌服务器，开箱即用
- Spring Boot 简化配置，本质还是 Spring

**102. 什么是 IOC？什么是 AOP？**

**答案要点：**
- IOC（控制反转）：对象创建和依赖管理交给容器，通过依赖注入实现
- AOP（面向切面）：横切关注点（日志、事务、鉴权）分离，动态代理实现

**103. Spring 的 Bean 生命周期？**

**答案要点：** 实例化 → 属性填充 → Aware 接口回调 → BeanPostProcessor（before）→ 初始化（@PostConstruct/InitializingBean）→ BeanPostProcessor（after）→ 使用 → 销毁（@PreDestroy/DisposableBean）。

**104. Spring Bean 的作用域？**

**答案要点：**
- singleton：单例（默认）
- prototype：每次获取新实例
- request/session/application：Web 环境用
- 注意：单例 Bean 注入原型 Bean 要用 @Lookup 或 ObjectProvider

**105. Spring 事务失效的场景？**

**答案要点：**
- 方法不是 public
- 自调用（同类内 this.xxx()）
- 异常被 try-catch 吞掉
- 抛出的是受检异常（默认不回滚，需 rollbackFor）
- 数据库不支持事务（MyISAM）

**106. Spring 的循环依赖怎么解决？**

**答案要点：** 三级缓存：
- 一级：成品 Bean
- 二级：早期暴露的半成品（已实例化未初始化）
- 三级：ObjectFactory（代理工厂）
- 构造器循环依赖无法解决

（以下 14 题见仓库完整版）

### 第三篇：实战篇（40 题，拿 offer 区）

#### 七、MySQL（15 题）

**121. MySQL 索引为什么用 B+ 树？**

**答案要点：**
- 树高矮（3 层可存千万级数据），减少磁盘 IO
- 叶子节点有序 + 链表，范围查询高效
- 非叶子节点只存键，一页能存更多索引
- 相比红黑树：矮胖；相比 B 树：范围查询更快

**122. 什么是聚簇索引和非聚簇索引？**

**答案要点：**
- 聚簇索引：数据行和索引在一起（InnoDB 主键索引），叶子存整行数据
- 非聚簇索引：索引和数据分离（二级索引），叶子存主键，查询需回表
- 覆盖索引：查询列都在索引里，不用回表

**123. 什么是回表？怎么避免？**

**答案要点：** 通过二级索引查到主键，再用主键去聚簇索引查整行 = 回表。避免：用覆盖索引（把查询列加入联合索引）。

**124. 事务的 ACID 特性？**

**答案要点：**
- 原子性（Atomicity）：全做或全不做（undo log）
- 一致性（Consistency）：数据状态一致
- 隔离性（Isolation）：事务间隔离（锁）
- 持久性（Durability）：提交后持久化（redo log）

**125. 事务隔离级别？**

**答案要点：**
- 读未提交：脏读
- 读已提交：不可重复读（Oracle 默认）
- 可重复读：幻读（MySQL 默认，MVCC 解决）
- 串行化：性能最差
- 脏读/不可重复读/幻读对应解决

（以下 10 题见仓库完整版）

#### 八、Redis（15 题）

**136. Redis 的数据结构？**

**答案要点：**
- String：缓存、计数
- Hash：对象存储
- List：消息队列、时间线
- Set：去重、交集并集
- ZSet：排行榜（分数排序）
- 高级：Geo、HyperLogLog、Bitmap

**137. Redis 缓存穿透、击穿、雪崩？**

**答案要点：**
- 穿透：查不存在的 key，打穿到 DB → 布隆过滤器 / 缓存空值
- 击穿：热点 key 过期，大量请求打到 DB → 互斥锁 / 逻辑过期
- 雪崩：大量 key 同时过期 → 随机过期时间 / 集群

**138. Redis 持久化 RDB 和 AOF？**

**答案要点：**
- RDB：快照，快但可能丢数据
- AOF：追加日志，慢但安全（可 everysec）
- 混用：RDB 打底 + AOF 增补

（以下 12 题见仓库完整版）

#### 九、系统设计（10 题）

**151. 设计一个秒杀系统？**

**答案要点：**
- 前端：按钮置灰 + 限流
- 网关：限流（令牌桶）
- Redis：预扣库存（Lua 原子操作）+ 缓存热点数据
- MQ：削峰填谷，异步下单
- 数据库：乐观锁扣库存，最终一致性

**152. 设计一个分布式锁？**

**答案要点：**
- Redis SETNX + 过期时间（防死锁）
- Redisson 看门狗续期（防过期提前释放）
- 高可用：RedLock 多节点
- 防误删：value 用唯一标识，删除时 Lua 校验

（以下 8 题见仓库完整版）

### 附：高频考点速记卡（30 题，面试前 10 分钟）

**161. HashMap 为什么线程不安全？**

**速记：** 并发 put 会覆盖丢数据；JDK 7 扩容时可能死循环（头插法）；JDK 8 尾插法不死循环但仍丢数据。

**162. Spring 中 @Autowired 和 @Resource 区别？**

**速记：** @Autowired 按类型（Spring 注解），@Resource 先按名称再按类型（JSR 250）。

**163. TCP 三次握手？**

**速记：** SYN → SYN+ACK → ACK。客户端发 SYN，服务端回 SYN+ACK，客户端回 ACK 建立连接。

（以下 27 题见仓库完整版）

## 🚀 快速开始

```bash
# 直接浏览
# 打开 README.md 即可查看全部内容

# 或者克隆到本地
git clone https://github.com/zieang88888/java-interview-zh.git
```

## 🤝 贡献

- 有好的面试题？提 PR
- 有想补充的考点？提 Issue
- 觉得有用？点个 ⭐ Star 就是最大的支持！

## 📄 License

MIT

---

**如果这份题库帮到了你，请点个 ⭐ Star，让更多准备 Java 面试的同学看到！** 🙏

**关注我 [@zieang88888](https://github.com/zieang88888)，持续输出中文开源干货！**