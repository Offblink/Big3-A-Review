# Java 框架技术（一）期末：老师原话 → 知识点 → 课程代码逐行对照

> **材料根目录**：`C:\Users\37549\Desktop\JFT1\期末\课程`
> **整理日期**：2026-11-18
> **行号口径**：一律指“该文件自身的物理行”，可直接用编辑器跳转。
>
> **路径口径**：
> - `课程/N/code/文件名`：课程包里真实存在的文件，直接打开。
> - `课程/N/xxx.rar → 内部路径`：先解压该 rar，再按内部路径找。
> - `课程/N/xxx.html → 完整源码 → 项目路径`：源码在 HTML 的“完整源码”章节里，行号指该代码块自身的行号（HTML 没有内嵌行号，用编辑器粘贴后跳转即可）。
>
> **合并口径**：同一个知识点的选择题、填空题、简答题已经合并到同一节，节内用「题型」标注老师原话。
> **重要**：老师的话里有 7 处与课程材料对不上（或材料根本没讲），集中在第 0.1 节列出，避免你把通用答案当成课件原文背。

---

## 0. 老师原话索引（先定位，再背）

| # | 知识点 | 老师原话（题型） | 材料落点 |
|---|---|---|---|
| 1 | IoC 与 DI | 依赖注入 + 控制反转 -> IOC：注解（选择） | 第 8 章 |
| 2 | Bean 构造与属性注入 | Java bean 构造 注解；bean 生命周期：构造器、getter/setter（选择/填空） | 第 8 章 |
| 3 | 自动装配与 Spring 注解 | 自动装配：3 种；spring 注解（all）（多选/填空） | 第 8 章 + 缺口 |
| 4 | Bean 生命周期 | bean 生命周期：构造器、初始化和 getter/setter、xml 与注解的写法（多选/填空） | 第 8 章 |
| 5 | AOP 与通知 | 通知 aop；AOP；aop，四大类（选择/多选/填空） | 第 9 章 |
| 6 | 切点表达式与代理 | AOP 的底层怎么实现（选择） | 第 9 章 |
| 7 | 声明式事务 | 声明式事务；事务：类上、方法上（隔离行为、回滚）（选择/多选） | 第 11 章 + 缺口 |
| 8 | 转账事务案例 | spring 事务：账户转账、accountService（简答） | 第 8 章 dao 模块（等价物） |
| 9 | MyBatis 核心与标签 | mb：标签（填空） | 第 1 章 |
| 10 | Mapper 两种开发 + `#{}` / `${}` | `$ #`（选择） | 第 1、3 章 |
| 11 | resultType 与 resultMap | 自定义返回结果集：resultType 和 map（填空/简答） | 第 4 章 |
| 12 | 动态 SQL | 动态标签 of Mybatis（多选/填空） | 第 4 章 |
| 13 | 关联映射 | 动态 sql：多对一，一对多；mb-empmapper 查询 多对一/一对多（填空/简答） | 第 5 章 |
| 14 | 缓存 | 缓存：分级、和谁绑定（多选） | 第 7 章 |
| 15 | MyBatis-Plus 组件与注解 | mp：四大组件 注解（选择） | 第 6 章 |
| 16 | 逻辑删除 | 逻辑删除（选择） | 第 6 章 |
| 17 | 乐观锁 / 悲观锁 | mp 乐观/悲观锁（填空） | 第 6 章 |
| 18 | 分页与自动填充 | （隐含在“mp 四大组件”） | 第 6 章 |
| 19 | SpringMVC 四大核心 | mvc 四大核心：如何定义（选择） | 第 10 章 |
| 20 | Controller 与返回 JSON | 返回结果为 json，如何实现？（填空） | 第 10 章 |
| 21 | 参数绑定与路径传参 | mvc 参数绑定与数据传递：4 种方式；路径传参（多选/填空） | 第 10 章 |
| 22 | 数据传递与 ModelAndView | modelandview：前后缀（填空） | 第 10 章 |
| 23 | 拦截器 | 拦截器：方法名称；工作顺序，与过滤器的区别（选择/多选） | 第 10 章 |
| 24 | 全局异常 | 全局异常（异常类）（填空） | 第 10 章 |
| 25 | SSM 三层整合 | （简答/综合） | 第 11 章 |
| 26 | 调 bug | 简答题：调 bug（简答） | 全课程“常见坑”汇总 |

---

## 0.1 材料缺口：老师说了、课件里没有（或其口径与课件不同）

这些点**不要硬在课件里找**，下面给出标准答案，并注明最近的可引用代码。考试按标准答案写，不要谎称课件有。

| 老师原话 | 材料情况 | 处理 |
|---|---|---|
| **自动装配：3 种** | 第 8 章只讲 `@Autowired` + `@Qualifier`，**没有** `autowire="byName/byType/constructor"` 的 XML 示例 | 按 Spring 规范答 3 种：`byName`、`byType`、`constructor`；注解等价物见第 3 节 |
| **声明式事务（XML 式）** | 第 11 章只给注解式 `@Transactional`；第 8 章 dao 模块只**提到**“XML 式 `tx:advice`”，源码压缩包里没有该 XML | 定义按标准答，代码只引注解式与配置类，明确标注 XML 式无源码 |
| **spring 事务：账户转账、accountService** | 课件没有 `AccountService`，最接近的是 `UserServiceImpl.transferPoints()`（积分转账） | 答题用“两个账户一扣一加”模板，代码引 `transferPoints`，类名按老师说的 `AccountService` 写 |
| **mp：四大组件** | 课件原话是“实体类**五大**注解”“BaseMapper **四大天王**”，没有“四大组件”这一术语 | 两种可能口径都给出：实体四注解 / BaseMapper 四方法（见第 15 节） |
| **AOP 四大类** | 课件明确是“**五种**通知” | 两种可能口径都给出：四大核心概念 / 四类非环绕通知（见第 5 节） |
| **MVC 参数绑定与数据传递：4 种** | 课件写的是“接收参数 **10** 种、携带数据 **7** 种” | 4 种按考试口径收窄为：`@RequestParam`、`@PathVariable`、实体绑定、`@RequestBody`；完整 10 种见表 |
| **mp 悲观锁** | 只有 `MybatisPlusConfig.java` 的注释讲 `SELECT ... FOR UPDATE`，没有可运行代码 | 定义 + 该注释为证（见第 17 节） |

---

# 一、Spring IoC / Bean

## 1. IoC 与 DI（依赖注入 + 控制反转）

**题型**：选择题“依赖注入 + 控制反转 -> IOC：注解”

**定义（背这段）**

- **IoC（Inversion of Control，控制反转）**：对象的**创建权、依赖装配权**从业务代码转移给 Spring 容器。它是**目标**。
- **DI（Dependency Injection，依赖注入）**：容器把依赖对象“送进”目标对象。它是实现 IoC 的**手段**。
- 一句话：**IoC 是思想，DI 是实现；注解是声明方式。**
- 注解实现三件套：`@Component`（把类注册成 Bean）→ `@Autowired`（按类型注入）→ `@Qualifier`（同类型多个时按名字）。
- 容器接口：`BeanFactory`（顶层、懒加载）→ `ApplicationContext`（子接口、启动即创建单例，实际使用）。实现类 `ClassPathXmlApplicationContext`（XML）/ `AnnotationConfigApplicationContext`（注解配置类）。

**代码落点 1：注解声明 Bean + Setter 注入**

`课程/8/Spring.rar → Spring/Ioc/Annotation/Car.java`　**L8–L9、L26–L46**

```java
@Component("carBySetter")
public class Car {
```

```java
    @Value("比亚迪")
    public void setBrand(String brand) {
        this.brand = brand;
    }

    @Value("秦PLUS")
    public void setModel(String model) {
        this.model = model;
    }

    @Value("128000")
    public void setPrice(int price) {
        this.price = price;
    }

    @Autowired
    @Qualifier("wheelSingleton")
    public void setWheel(Wheel wheel) {
        this.wheel = wheel;
        System.out.println("  [Car] @Autowired + @Qualifier 注入 Wheel -> " + wheel.getType());
    }
```

**代码落点 2：`@Primary`、`@Scope`、`@Value` 字段注入**

`课程/8/Spring.rar → Spring/Ioc/Annotation/Wheel.java`　**L8–L17**

```java
@Component("wheelSingleton")
@Primary
@Scope("singleton")
public class Wheel {

    @Value("米其林")
    private String type;

    @Value("17")
    private int size;
```

**代码落点 3：注解配置类（替代 XML 根标签与 component-scan）**

`课程/8/Spring.rar → Spring/Ioc/Annotation/SpringAnnotationConfig.java`　**L17–L34**

```java
@Configuration
@ComponentScan(basePackages = "com.Spring.Ioc.Annotation")
public class SpringAnnotationConfig {

    public SpringAnnotationConfig() {
        System.out.println("  [SpringAnnotationConfig] 构造器被调用");
    }

    @Bean(name = "wheelPrototype")
    @Scope("prototype")
    public Wheel wheelPrototype() {
        return new Wheel("固特异", 18);
    }

    @Bean(name = "carLifecycle")
    public Car carLifecycle() {
        return new Car("保时捷", "911", 1500000);
    }
```

**易错点**

- `@Autowired` 默认**按类型**；同类型多个会报 `NoUniqueBeanDefinitionException`，必须 `@Qualifier("id")` 或 `@Primary`。
- `@Value` 只能注入**值类型**；集合/对象要靠 `@Bean` 方法或 `@Autowired`。
- 只写 `@Component` 不写扫描（`@ComponentScan` 或 `<context:component-scan>`），Bean 不会进容器。

---

## 2. Bean 的构造与属性注入（XML / 注解两套写法）

**题型**：选择题“Java bean 构造 注解”；填空题“构造器、getter/setter、xml 与注解的写法”

**定义（背这段）**

- Spring 创建 Bean 的两条路：
  1. **无参构造 + Setter 注入**：容器先 `new`（必须有无参构造器），再逐个调 `setXxx()`。XML 用 `<property name value/ref>`；注解用 `@Value` / `@Autowired` 标在 setter 上。
  2. **构造器注入**：容器直接调有参构造。XML 用 `<constructor-arg>`（可加 `index` 指定位置）；注解可把 `@Autowired` 标在构造器上（Spring 4.3 起单构造器可省略）。
- `value` 注入**值类型**；`ref` 注入**另一个 Bean**（按 id）。
- 注解方式下，字段注入、setter 注入、构造器注入都算 DI；**构造器注入最推荐**（字段可 `final`、便于单测）。
- **getter/setter 不是 Spring 必需**：只有当你要用 setter 注入、或要让框架/EL 读属性时才需要。

**代码落点 1：XML 的 setter 注入与构造器注入**

`课程/8/springioc Spring IoC与依赖注入.html → 完整源码 → src/main/resources/springioc/ioc-beans.xml`　**L20–L43**

```xml
    <!-- ============ 1. 无参构造 + Setter 注入值类型 ============ -->

    <bean id="carBySetter" class="com.Spring.Ioc.xml.Car">
        <property name="brand" value="比亚迪"/>
        <property name="model" value="秦PLUS"/>
        <property name="price" value="128000"/>
    </bean>

    <!-- ============ 2. 构造器注入值类型 ============ -->

    <bean id="carByConstructor" class="com.Spring.Ioc.xml.Car">
        <constructor-arg value="特斯拉"/>
        <constructor-arg value="Model 3"/>
        <constructor-arg value="259900"/>
    </bean>

    <!-- ============ 3. Setter + ref 注入引用类型 ============ -->

    <bean id="carWithWheelRef" class="com.Spring.Ioc.xml.Car">
        <property name="brand" value="宝马"/>
        <property name="model" value="3系"/>
        <property name="price" value="320000"/>
        <property name="wheel" ref="wheelSingleton"/>
    </bean>
```

**代码落点 2：Car 的三个构造器与 setter（被上面的 XML 调用）**

`课程/8/Spring.rar → Spring/Ioc/xml/Car.java`　**L10–L27**

```java
    public Car() {
        System.out.println("  [Car] 无参构造器");
    }

    public Car(String brand, String model, int price) {
        this.brand = brand;
        this.model = model;
        this.price = price;
        System.out.println("  [Car] 三参构造器 -> " + brand + " " + model);
    }

    public Car(String brand, String model, int price, Wheel wheel) {
        this.brand = brand;
        this.model = model;
        this.price = price;
        this.wheel = wheel;
        System.out.println("  [Car] 四参构造器 -> " + brand + " " + model);
    }
```

`课程/8/Spring.rar → Spring/Ioc/xml/Car.java`　**L29–L43**

```java
    public void setBrand(String brand) {
        this.brand = brand;
    }

    public void setModel(String model) {
        this.model = model;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public void setWheel(Wheel wheel) {
        this.wheel = wheel;
    }
```

**代码落点 3：注解版对应写法（`@Value` 标 setter）**

见第 1 节 `Car.java` L26–L46。**同一个 `Car` 类，XML 版在 `Ioc.xml` 包（无注解），注解版在 `Ioc.Annotation` 包（有注解）**，两套代码并存、包名不同，是课件刻意做的左右对照。

**易错点**

- 用 `<property>` 做 setter 注入时，类**必须有无参构造器**；否则容器实例化就失败。
- `<constructor-arg>` 不写 `index` 时按**声明顺序**匹配；参数类型有歧义时容易选错构造器。课件用 3 个 `<constructor-arg>` 命中三参构造器、4 个 + `index` 命中四参构造器。
- `resultType` 与本题无关，别混。

---

## 3. 自动装配 3 种 + Spring 注解全集

**题型**：多选题“自动装配：3 种”；填空题“spring 注解（all）”

### 3.1 自动装配 3 种（材料缺口，按标准答案）

| 方式 | XML 写法 | 规则 | 注解等价物 |
|---|---|---|---|
| **byName** | `<bean autowire="byName">` | 按属性名找同 id 的 Bean | `@Autowired` + `@Qualifier("id")` |
| **byType** | `<bean autowire="byType">` | 按属性类型找唯一 Bean；多个则报错 | `@Autowired`（默认按类型） |
| **constructor** | `<bean autowire="constructor">` | 按构造器参数类型装配 | 构造器上的 `@Autowired` |

> 课件第 8 章**没有** XML `autowire` 示例（见 0.2）。考试若问“3 种”，写 `byName / byType / constructor`；若问“注解怎么自动装配”，写 `@Autowired` 按类型 + `@Qualifier` 按名字 + `@Resource` 按名字（JSR-250）。

### 3.2 注解全集（课件第 8 章速查表 + 第 9/10/11 章补充）

| 注解 | 位置 | 作用 | 课件证据 |
|---|---|---|---|
| `@Configuration` | 类 | 声明配置类（本身也是 Bean） | `SpringAnnotationConfig.java` L17 |
| `@ComponentScan(basePackages=…)` | 类 | 扫描 `@Component` 家族 | 同文件 L18 |
| `@Component` / `@Controller` / `@Service` / `@Repository` | 类 | 注册 Bean（后三者是 `@Component` 派生） | `Car.java` L8；`StudentServiceImpl.java` L22 |
| `@Bean(name=…)` | 方法 | 方法返回值注册为 Bean | `SpringAnnotationConfig.java` L25–L29 |
| `@Scope("prototype")` | 类/方法 | 作用域 | `Wheel.java` L10；配置类 L26 |
| `@Value("…")` | 字段/Setter | 注入值、`${}` 占位符、SpEL | `Car.java` L26–L39 |
| `@Autowired(required=false)` | 字段/Setter/构造器 | 按类型注入 | `Car.java` L41 |
| `@Qualifier("id")` | 字段/Setter 参数 | 同类型多个时按名字 | `Car.java` L42；`Person.java` L85 |
| `@Primary` | 类 | 同类型多个时的首选 | `Wheel.java` L9 |
| `@PostConstruct` / `@PreDestroy` | 方法 | 初始化/销毁回调（需 JSR-250 依赖） | `Person.java` L89–L97 |
| `@Lazy` | 类/方法 | 延迟初始化 | 速查表（无示例代码） |
| `@PropertySource` | 类 | 加载 properties | `DaoAnnotationConfig.java` L21 |
| `@EnableTransactionManagement` | 类 | 开启注解事务 | `DaoAnnotationConfig.java` L22 |
| `@Transactional` | 类/方法 | 声明式事务 | `StudentServiceImpl.java` L44 |
| `@Aspect` / `@Pointcut` / `@Before` / `@Around` 等 | 类/方法 | AOP | `LogAspect.java` L16–L52 |
| `@EnableAspectJAutoProxy` | 类 | 开启 AOP 自动代理 | `AopAnnotationConfig.java` L9 |
| `@RestController` | 类 | `@Controller` + `@ResponseBody` | `StudentController.java` L32 |
| `@RequestMapping` / `@GetMapping` / `@PostMapping` | 类/方法 | URL 映射 | 同文件 L33/L39 |
| `@RequestParam` / `@PathVariable` / `@RequestBody` / `@RequestHeader` / `@CookieValue` | 参数 | 参数绑定 | `ParameterController.java` L52–L129 |
| `@ControllerAdvice` / `@ExceptionHandler` | 类/方法 | 全局异常 | `GlobalExceptionHandler.java` L27/L31 |

**代码落点：`@Autowired` + `@Qualifier` 按名字注入**

`课程/8/Spring.rar → Spring/Ioc/Annotation/Person.java`　**L84–L87**

```java
    @Autowired
    public void setHealthInfo(@Qualifier("healthInfo") Properties healthInfo) {
        this.healthInfo = healthInfo;
    }
```

**得分点**

- 多选“自动装配 3 种”只写 3 个英文单词，别写“字段注入/setter 注入/构造器注入”（那是 DI 的 3 种方式，不是 autowire 的 3 种）。
- 问“Spring 常用注解”，按“注册 Bean / 注入 / 配置 / 事务 / AOP / MVC / 异常”分组写，比流水账好得分。

---

## 4. Bean 生命周期

**题型**：多选题“bean 生命周期：构造器、初始化和 getter/setter、xml 与注解的写法”

**定义（老师要的简化版 + 课件完整版）**

老师口径（4 段）：

1. **实例化**：调构造器（反射 `new`）。
2. **属性注入**：调 setter / `@Value` / `@Autowired`（这就是“getter/setter”里的 setter）。
3. **初始化**：`@PostConstruct` → `InitializingBean.afterPropertiesSet()` → `init-method`。
4. **销毁**：`@PreDestroy` → `DisposableBean.destroy()` → `destroy-method`；容器 `close()` 触发。

课件完整 11 步（选择/填空按这个写更稳）：

```text
① 实例化（构造器）
② 属性注入（setter / @Value / @Autowired）
③ BeanNameAware.setBeanName()
④ BeanFactoryAware.setBeanFactory()
⑤ ApplicationContextAware.setApplicationContext()
⑥ BeanPostProcessor.postProcessBeforeInitialization()
⑦ 初始化：@PostConstruct → afterPropertiesSet() → init-method
⑧ BeanPostProcessor.postProcessAfterInitialization()   ← AOP 代理在这里生成
⑨ Bean 就绪，被使用
⑩ 销毁：@PreDestroy → destroy() → destroy-method
⑪ 容器关闭 ctx.close()
```

**代码落点 1：XML 写法（`init-method` / `destroy-method`）**

`课程/8/springioc Spring IoC与依赖注入.html → 完整源码 → src/main/resources/springioc/ioc-beans.xml`　**L105–L113**

```xml
    <!-- ============ 7. Bean 生命周期 ============ -->

    <bean id="carLifecycle" class="com.Spring.Ioc.xml.Car"
          init-method="customInit"
          destroy-method="customDestroy">
        <constructor-arg value="保时捷"/>
        <constructor-arg value="911"/>
        <constructor-arg value="1500000"/>
    </bean>
```

**代码落点 2：XML 里被调用的初始化/销毁方法**

`课程/8/Spring.rar → Spring/Ioc/xml/Car.java`　**L45–L51**

```java
    public void customInit() {
        System.out.println("  [Car] ★ init-method -> " + brand + " " + model);
    }

    public void customDestroy() {
        System.out.println("  [Car] ★ destroy-method -> " + brand + " " + model);
    }
```

**代码落点 3：注解写法（`@PostConstruct` / `@PreDestroy`）**

`课程/8/Spring.rar → Spring/Ioc/Annotation/Person.java`　**L89–L97**

```java
    @PostConstruct
    public void init() {
        System.out.println("  [Person] ★ @PostConstruct 初始化 -> " + name);
    }

    @PreDestroy
    public void destroy() {
        System.out.println("  [Person] ★ @PreDestroy 销毁 -> " + name);
    }
```

**代码落点 4：销毁必须 `close()`**

`课程/8/springioc Spring IoC与依赖注入.html → 完整源码 → src/test/java/com/Spring/Ioc/xml/SpringXmlIoCTest.java`　**L101–L105**

```java
        System.out.println("\n===== 8. Bean 生命周期 (init-method / destroy-method) =====");
        System.out.println("  -> " + ctx.getBean("carLifecycle"));

        ctx.close();
    }
```

**易错点**

- `prototype` 作用域的 Bean，容器**只负责创建，不负责销毁**；`close()` 不会调它的 `destroy-method`。
- `@PostConstruct` / `@PreDestroy` 属 JSR-250，缺 `javax.annotation-api` 时**静默不执行**，不报错。
- 生命周期顺序题：初始化内部是 `@PostConstruct` → `afterPropertiesSet()` → `init-method`，别写反。

---

# 二、AOP

## 5. AOP 核心概念与通知（含“四大类”）

**题型**：选择题“通知 aop”；多选题“AOP”；填空题“aop，四大类”

**定义**

- **AOP（Aspect Oriented Programming，面向切面编程）**：把日志、事务、权限等**横切关注点**从业务方法中抽出来，运行期通过动态代理“织入”到方法调用前后。
- **AOP 的前提是 IoC**：对象必须由 Spring 创建，Spring 才能把它替换成代理。
- 四大核心概念（“四大类”口径一）：
  1. **切面 Aspect**：`LogAspect` 类（`@Aspect`）。
  2. **连接点 JoinPoint**：可被拦截的点；Spring AOP 只支持**方法级**。
  3. **切点 Pointcut**：`execution(...)` 表达式，选中哪些方法。
  4. **通知 Advice**：拦截后做什么（Before/Around/…）。
  - 另有：目标对象 Target、代理对象 Proxy、织入 Weaving。
- 五类通知（“四大类”口径二：除 `@Around` 外的四类；但标准答案是**五种**）：

| 通知 | 注解 | XML 标签 | 时机/特点 |
|---|---|---|---|
| 前置 | `@Before` | `<aop:before>` | 目标方法前；**拦不住**目标方法 |
| 后置返回 | `@AfterReturning` | `<aop:after-returning>` | 正常返回后；`returning="result"` 拿返回值 |
| 后置异常 | `@AfterThrowing` | `<aop:after-throwing>` | 抛异常后；`throwing="ex"` 拿异常 |
| 最终 | `@After` | `<aop:after>` | 无论正常/异常都执行（类似 finally） |
| 环绕 | `@Around` | `<aop:around>` | 最强：可改参数/返回值、捕获异常、控制是否执行目标方法 |

- **执行顺序（单切面、正常返回）**：`@Before → @Around 进入 → 目标方法 → @Around 退出 → @After → @AfterReturning`。
- 异常时：`@Before → @Around 进入 → 目标方法抛异常 → @Around 异常 → @After → @AfterThrowing`（没有 `@AfterReturning`）。

**代码落点 1：注解版五通知（同一类里看全）**

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/java/com/Spring/Aop/Annotation/LogAspect.java`　**L16–L75**

```java
@Aspect
@Component
public class LogAspect {

    @Pointcut("execution(* com.Spring.Aop.Annotation.UserService.*(..))")
    public void servicePointcut() {
    }

    @Before("servicePointcut()")
    public void beforeLog(JoinPoint jp) {
        String method = jp.getSignature().getName();
        Object[] args = jp.getArgs();
        System.out.println("  ⏰ @Before — [" + method + "] 参数: " + Arrays.toString(args));
    }

    @AfterReturning(pointcut = "servicePointcut()", returning = "result")
    public void afterReturningLog(JoinPoint jp, Object result) {
        String method = jp.getSignature().getName();
        Object[] args = jp.getArgs();
        System.out.println("  ✅ @AfterReturning — [" + method + "] 参数: " + Arrays.toString(args) + " → 返回: " + result);
    }

    @AfterThrowing(pointcut = "servicePointcut()", throwing = "ex")
    public void afterThrowingLog(JoinPoint jp, Throwable ex) {
        String method = jp.getSignature().getName();
        Object[] args = jp.getArgs();
        System.out.println("  ❌ @AfterThrowing — [" + method + "] 参数: " + Arrays.toString(args) + " 异常: " + ex.getMessage());
    }

    @After("servicePointcut()")
    public void afterLog(JoinPoint jp) {
        String method = jp.getSignature().getName();
        Object[] args = jp.getArgs();
        System.out.println("  🔔 @After — [" + method + "] 参数: " + Arrays.toString(args));
    }

    @Around("servicePointcut()")
    public Object aroundLog(ProceedingJoinPoint pjp) throws Throwable {
        String method = pjp.getSignature().getName();
        Object[] args = pjp.getArgs();
        System.out.println("  🌯 @Around — 进入 [" + method + "] 参数: " + Arrays.toString(args));

        Object[] newArgs = args.clone();
        if (newArgs.length > 0 && newArgs[0] instanceof String) {
            newArgs[0] = "[已加密]" + newArgs[0];
            System.out.println("  🌯 @Around — 修改参数后: " + Arrays.toString(newArgs));
        }

        long start = System.currentTimeMillis();
        try {
            Object ret = pjp.proceed(newArgs);
            long cost = System.currentTimeMillis() - start;
            System.out.println("  🌯 @Around — 退出 [" + method + "] 耗时: " + cost + "ms 返回: " + ret);
            return ret;
        } catch (Throwable t) {
            long cost = System.currentTimeMillis() - start;
            System.out.println("  🌯 @Around — 异常 [" + method + "] 耗时: " + cost + "ms");
            throw t;
        }
    }
```

**代码落点 2：XML 版五通知（切面类退化成普通 POJO）**

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/resources/springaop/aop-xml.xml`　**L15–L39**

```xml
    <aop:config>
        <aop:aspect ref="logAspect">

            <aop:pointcut id="servicePointcut"
                          expression="execution(* com.Spring.Aop.xml.UserService.*(..))"/>

            <aop:before method="beforeLog"
                        pointcut-ref="servicePointcut"/>

            <aop:after-returning method="afterReturningLog"
                                 pointcut-ref="servicePointcut"
                                 returning="result"/>

            <aop:after-throwing method="afterThrowingLog"
                                pointcut-ref="servicePointcut"
                                throwing="ex"/>

            <aop:after method="afterLog"
                       pointcut-ref="servicePointcut"/>

            <aop:around method="aroundLog"
                        pointcut-ref="servicePointcut"/>

        </aop:aspect>
    </aop:config>
```

**得分点**

- 填空“AOP 四大类”若给的是通知空位，写 **前置、后置返回、后置异常、最终（+环绕）**；若给的是概念空位，写 **切面、连接点、切点、通知**。两种都准备。
- `@Around` 必须 `return pjp.proceed(...)`，否则调用方拿到 `null`；异常必须往外抛，否则事务/上层感知不到。
- 通知顺序不要死背：课件实测 XML 版是 `@Before` 先、注解版是 `@Around` 先进入；不同版本/组合会有差异，答题以“正常返回：Before→目标→After→AfterReturning；异常：Before→目标→After→AfterThrowing”为主。

---

## 6. 切点表达式与代理方式

**题型**：选择题“AOP 底层怎么实现 / JDK 代理与 CGLIB”

**定义**

- **切点表达式**：`execution(修饰符? 返回值 包.类.方法(参数) throws?)`。
  - `*` 任意字符（不跨包）；`..` 任意层包 / 任意个参数；`+` 该类及子类。
  - 例：`execution(* com.Spring.Aop.Annotation.UserService.*(..))`。
- **两种代理**：
  - **JDK 动态代理**：目标类**必须实现接口**；`Proxy.newProxyInstance`；只能按接口类型取 Bean。
  - **CGLIB**：生成子类；无接口也能代理；`final` 类/方法不能代理。
  - 切换：`@EnableAspectJAutoProxy(proxyTargetClass = false)` → 有接口用 JDK；`true` → 一律 CGLIB。
- 结论：**AOP = 动态代理 + 通知链**；Spring 默认有接口走 JDK，无接口走 CGLIB。

**代码落点 1：开启自动代理**

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/java/com/Spring/Aop/Annotation/AopAnnotationConfig.java`　**L7–L10**

```java
@Configuration
@ComponentScan(basePackages = "com.Spring.Aop.Annotation")
@EnableAspectJAutoProxy(proxyTargetClass = false)
public class AopAnnotationConfig {
```

**代码落点 2：命名切点（空方法只作名字用）**

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/java/com/Spring/Aop/Annotation/LogAspect.java`　**L20–L22**

```java
    @Pointcut("execution(* com.Spring.Aop.Annotation.UserService.*(..))")
    public void servicePointcut() {
    }
```

**代码落点 3：目标类实现了接口，所以走 JDK 代理**

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/java/com/Spring/Aop/Annotation/UserServiceImpl.java`　**L5–L11**

```java
@Component("userService")
public class UserServiceImpl implements UserService {

    @Override
    public void saveUser(String name) {
        System.out.println("    [saveUser] 正在保存用户: " + name);
    }
```

`课程/9/springaop Spring AOP面向切面编程.html → 完整源码 → src/main/java/com/Spring/Aop/Annotation/UserService.java`　**L1–L12**

```java
package com.Spring.Aop.Annotation;

public interface UserService {

    void saveUser(String name);

    int deleteUser(String name);

    String findUser(String name);

    void riskyOperation();
}
```

**易错点**

- JDK 代理下 `ctx.getBean(UserServiceImpl.class)` 会失败，必须 `ctx.getBean(UserService.class)`。
- 切点写错包名，通知**一个都不执行**，且不报错——先看 `execution` 全限定名。
- `@Aspect` 不加 `@Component` 是“哑切面”：不报错，也不生效。

---

# 三、事务

## 7. 声明式事务（类上 / 方法上、隔离、回滚）

**题型**：选择题“声明式事务”；多选题“事务：类上、方法上（隔离行为、回滚）”

**定义**

- **声明式事务**：不写 `commit/rollback`，用配置或注解声明事务边界，由 Spring 通过 AOP 代理在方法前后开启/提交/回滚。
  - **注解式**：`@Transactional` + `<tx:annotation-driven/>` 或 `@EnableTransactionManagement`。
  - **XML 式**：`<tx:advice>` + `<aop:config>` 把事务通知织入切点（**课件只提到，未给源码**）。
- **类上 vs 方法上**：
  - 标在**类**上：对该类所有 `public` 方法生效，作为默认值。
  - 标在**方法**上：覆盖类上的设置（方法级优先）。
- **代理机制**：事务代理包住目标对象；方法正常返回 → `commit`；抛异常 → 按规则 `rollback`。
- **回滚规则**：默认只回滚 `RuntimeException` 与 `Error`；**受检异常不回滚**，要 `rollbackFor = Exception.class`。
- **隔离级别**（`isolation`）：`DEFAULT`（跟数据库）、`READ_UNCOMMITTED`、`READ_COMMITTED`、`REPEATABLE_READ`、`SERIALIZABLE`。越高越安全、并发越低。
- **传播行为**（`propagation`）：默认 `REQUIRED`（有事务就加入，没有就新建）；另有 `REQUIRES_NEW`、`NESTED`、`SUPPORTS`、`NOT_SUPPORTED`、`MANDATORY`、`NEVER`。
- `readOnly = true`：只读优化，不能写。

**代码落点 1：事务管理器 + 开启注解事务（XML）**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/resources/ssm/applicationContext.xml`　**L58–L65**

```xml
    <!-- ④ 事务：Spring 事务管理器接管 MyBatis（本质是接管 SqlSession 的提交/回滚） -->
    <bean id="transactionManager"
          class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- 开启 @Transactional 注解事务（对比 Spring/dao 模块的 XML 式 tx:advice） -->
    <tx:annotation-driven transaction-manager="transactionManager"/>
```

**代码落点 2：`@Transactional` 标在方法上（提交与回滚的对照）**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/java/com/ssm/service/StudentServiceImpl.java`　**L22–L55**

```java
@Service
public class StudentServiceImpl implements StudentService {

    private final StudentMapper studentMapper;

    /** 构造器注入（推荐）：字段可 final，依赖一目了然，便于单测 */
    @Autowired
    public StudentServiceImpl(StudentMapper studentMapper) {
        this.studentMapper = studentMapper;
    }

    @Override
    public List<Student> findAll() {
        return studentMapper.selectAll();
    }

    @Override
    public Student findById(Integer id) {
        return studentMapper.selectById(id);
    }

    @Override
    @Transactional
    public void addStudent(Student student) {
        studentMapper.insert(student);
    }

    @Override
    @Transactional
    public void addThenFail(Student student) {
        studentMapper.insert(student);          // ① SQL 已执行（日志可见 INSERT）
        throw new RuntimeException("故意抛出异常 → 事务回滚，上面的 INSERT 不会提交到数据库");
        // ② 异常穿过 @Transactional 代理 → 代理捕获并 rollback
    }
```

**代码落点 3：注解配置类开启事务（`@EnableTransactionManagement`）**

`课程/8/Spring.rar → Spring/dao/annotation/DaoAnnotationConfig.java`　**L19–L23**

```java
@Configuration
@ComponentScan(basePackages = "com.Spring.dao.annotation")
@PropertySource("classpath:common/db.properties")
@EnableTransactionManagement
public class DaoAnnotationConfig {
```

`课程/8/Spring.rar → Spring/dao/annotation/DaoAnnotationConfig.java`　**L61–L64**

```java
    @Bean
    public DataSourceTransactionManager transactionManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
```

**代码落点 4：隔离级别 + 回滚规则 + 传播行为写在注解上**

`课程/8/Spring.rar → Spring/dao/annotation/UserServiceImpl.java`　**L29–L37**

```java
    @Override
    @Transactional(rollbackFor = Exception.class, propagation = Propagation.REQUIRED)
    public void registerUser(User user) {
        userMapper.insertAndGetId(user);
    }

    @Override
    @Transactional(rollbackFor = Exception.class, isolation = Isolation.READ_COMMITTED)
    public void transferPoints(Integer fromUserId, Integer toUserId, int points) {
```

**得分点**

- 多选“事务：类上、方法上”要答出：**类级默认 + 方法级覆盖**；**默认回滚 RuntimeException/Error**；**受检异常需 rollbackFor**；**隔离级别解决脏读/不可重复读/幻读**。
- 事务失效高频原因：**同类内部自调用**（没走代理）、**异常被 catch 没抛**、**方法不是 public**、**子容器重复扫描导致注入的不是事务代理**（见第 25 节）。

---

## 8. 转账事务案例（accountService 的等价代码）

**题型**：简答题“spring 事务：账户转账、accountService”

**答题模板（4 步）**

1. `AccountService` 的 `transfer(fromId, toId, money)` 标 `@Transactional`。
2. 先查两个账户（余额校验），再 `update` 扣款、`update` 入账。
3. 任一步失败/余额不足抛 `RuntimeException` → 代理捕获 → **整个方法回滚**，扣款与入账都不生效。
4. 受检异常要回滚必须写 `rollbackFor = Exception.class`；查询方法可加 `readOnly = true`。

> **材料说明**：课件没有 `AccountService`，最近的是第 8 章 dao 模块的**积分转账** `transferPoints`（转出账户 `_sub`、转入账户 `_add`，金额 >1000 故意抛异常验证回滚）。答题时把“积分”换成“金额”、类名换成 `AccountService` 即可，结构完全一致。

**代码落点 1：注解式转账（带隔离级别与 rollbackFor）**

`课程/8/Spring.rar → Spring/dao/annotation/UserServiceImpl.java`　**L35–L60**

```java
    @Override
    @Transactional(rollbackFor = Exception.class, isolation = Isolation.READ_COMMITTED)
    public void transferPoints(Integer fromUserId, Integer toUserId, int points) {
        User from = userMapper.selectById(fromUserId);
        if (from == null) {
            throw new RuntimeException("转出账户不存在: " + fromUserId);
        }
        User to = userMapper.selectById(toUserId);
        if (to == null) {
            throw new RuntimeException("转入账户不存在: " + toUserId);
        }

        User fromUpdate = new User();
        fromUpdate.setId(fromUserId);
        fromUpdate.setPassword(from.getPassword() + "_sub");
        userMapper.updateById(fromUpdate);

        if (points > 1000) {
            throw new RuntimeException("转账金额过大触发异常 → 事务回滚!");
        }

        User toUpdate = new User();
        toUpdate.setId(toUserId);
        toUpdate.setPassword(to.getPassword() + "_add");
        userMapper.updateById(toUpdate);
    }
```

**代码落点 2：XML 式转账（类上无事务注解，事务应在 XML 中声明；该 XML 未随课件提供）**

`课程/8/Spring.rar → Spring/dao/xml/UserServiceImpl.java`　**L29–L53**

```java
    @Override
    public void transferPoints(Integer fromUserId, Integer toUserId, int points) {
        User from = userMapper.selectById(fromUserId);
        if (from == null) {
            throw new RuntimeException("转出账户不存在: " + fromUserId);
        }
        User to = userMapper.selectById(toUserId);
        if (to == null) {
            throw new RuntimeException("转入账户不存在: " + toUserId);
        }

        User fromUpdate = new User();
        fromUpdate.setId(fromUserId);
        fromUpdate.setPassword(from.getPassword() + "_sub");
        userMapper.updateById(fromUpdate);

        if (points > 1000) {
            throw new RuntimeException("转账金额过大触发异常 → 事务回滚!");
        }

        User toUpdate = new User();
        toUpdate.setId(toUserId);
        toUpdate.setPassword(to.getPassword() + "_add");
        userMapper.updateById(toUpdate);
    }
```

**易错点**

- 转账必须**同一个事务**：两个 `update` 都要在同一 `@Transactional` 方法内；不要在两个 Service 方法里分别提交。
- `try/catch` 吞掉异常 = 不回滚；要么继续抛，要么手动 `TransactionAspectSupport.currentTransactionStatus().setRollbackOnly()`。
- `@Transactional` 默认对 `public` 方法生效；同类自调用不走代理。

---

# 四、MyBatis

## 9. MyBatis 核心对象与全局配置标签

**题型**：填空题“mb：标签”

**定义**

- 四个核心对象：
  1. `SqlSessionFactoryBuilder`：读配置、建工厂，**用完即弃**。
  2. `SqlSessionFactory`：重量级、**单例**，整个应用一个。
  3. `SqlSession`：一次数据库会话，**非线程安全**，用完 `close()`；`openSession(true)` 自动提交。
  4. Mapper 接口代理：`sqlSession.getMapper(XxxMapper.class)`，按“namespace + 方法名”找 SQL。
- 全局配置标签（`mybatis-config.xml`）：`properties` → `settings` → `typeAliases` → `environments`（`transactionManager` + `dataSource`）→ `mappers`。
- 常用 `settings`：`logImpl`、`mapUnderscoreToCamelCase`、`lazyLoadingEnabled`、`aggressiveLazyLoading`、`localCacheScope`、`cacheEnabled`。
- Mapper 文件标签：`<mapper namespace>`、`<select>`、`<insert>`、`<update>`、`<delete>`、`<resultMap>`、`<sql>`/`<include>`、`<cache>`，以及动态标签（第 12 节）。

**代码落点 1：全局配置（顺序不能乱）**

`课程/1/code/mybatis-config.xml`　**L6–L39**

```xml
<configuration>

    <!-- 引入公共properties文件 -->
    <properties resource="common/db.properties"/>

    <!-- 全局设置 -->
    <settings>
        <!-- 开启日志 -->
        <setting name="logImpl" value="LOG4J"/>
        <!-- 开启驼峰命名自动映射 -->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>

    <!-- 环境配置 -->
    <environments default="development">
        <environment id="development">
            <!-- 事务管理器 -->
            <transactionManager type="JDBC"/>
            <!-- 数据源 -->
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.username}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>

    <!-- 注册Mapper -->
    <mappers>
        <mapper resource="chapter01/mapper/UserMapper.xml"/>
    </mappers>

</configuration>
```

**代码落点 2：核心对象的创建与使用**

`课程/1/code/UserMapperTest.java`　**L17–L33**

```java
public class UserMapperTest { //创建一个测试类
    /*
    * mybatis中的核心类
    * SqlSessionFactory：数据库连接工厂
    * SqlSession：数据库连接session 类似connection对象
    * */

    private SqlSessionFactory sqlSessionFactory;  //定义一个Mybatis的连接工厂

    @Before  // 这是一个注解的书写 在测试方法执行前执行
    public void init() throws Exception {
        InputStream is = Resources.getResourceAsStream("chapter01/mybatis-config.xml");
        //读取当前项目的数据库的连接文件mybatis-config.xml
        //该文件中包含数据库的连接和该项目的执行sqlMapper文件
        sqlSessionFactory = new SqlSessionFactoryBuilder().build(is);
        //创建一个Mybatis的连接工厂
    }
```

**代码落点 3：Mapper XML 的 CRUD 标签**

`课程/1/code/UserMapper.xml`　**L20–L44**

```xml
    <!-- 根据ID查询用户 -->
    <select id="findById" parameterType="int" resultType="com.entity.User">
        SELECT * FROM user WHERE id = #{id}
    </select>

    <!-- 添加用户 -->
    <insert id="addUser" parameterType="com.entity.User"
            useGeneratedKeys="true" keyProperty="id">
        INSERT INTO user(username, password, email)
        VALUES(#{username}, #{password}, #{email})
    </insert>

    <!-- 更新用户 -->
    <update id="updateUser" parameterType="com.entity.User">
        UPDATE user
        SET username = #{username},
            password = #{password},
            email = #{email}
        WHERE id = #{id}
    </update>

    <!-- 删除用户 -->
    <delete id="deleteUser" parameterType="int">
        DELETE FROM user WHERE id = #{id}
    </delete>
```

**得分点**

- 填空“MyBatis 标签”按“**配置标签 + 映射标签 + 动态标签**”三层写，别只写 `<select>`。
- `<mappers>` 注册两种方式：`<mapper resource="...xml"/>` 单文件；`<package name="包名"/>` 批量扫接口（XML 必须**同包同名**）。

---

## 10. Mapper 两种开发方式 + `#{}` 与 `${}`

**题型**：选择题“`$ #`”

**定义**

| 方式 | 写法 | 优点 | 缺点 |
|---|---|---|---|
| **XML** | 接口 + `XxxMapper.xml`（namespace = 接口全限定名，id = 方法名） | 复杂 SQL、动态 SQL 可读性好 | 文件多 |
| **注解** | `@Select/@Insert/@Update/@Delete` 直接写在接口方法上 | 简单 SQL 无需 XML | 动态 SQL 难写（要 `<script>` 包） |

- 两种可**混用**：注解写简单 SQL，XML 写复杂 SQL；`@ResultMap("xmlMapId")` 还能跨方式复用映射。
- **`#{}`**：预编译占位符，生成 `?`，用 `PreparedStatement` 设参；**防 SQL 注入**，能做类型处理。
- **`${}`**：字符串**直接拼接**进 SQL；不防注入；只适合表名/列名/`ORDER BY` 等不能用 `?` 的位置。
- 例：`'%${value}%'` 可被 `' OR 1=1 --` 注入；`'%#{value}%'` 才安全（实际写 `LIKE CONCAT('%', #{value}, '%')`）。

**代码落点 1：注解式 CRUD + `${}` 注入风险写法**

`课程/3/code/UserMapperAnnotation.java`　**L24–L62**

```java
    @Select("SELECT * FROM user")
    List<User> findAll();

    /**
     * 根据ID查询用户（注解方式）
     * 日志输出：会显示参数值
     */
    @Select("SELECT * FROM user WHERE id = #{id}")
    User findById(Integer id);

    /**
     * 添加用户（注解方式）
     * 日志输出：会显示插入的参数
     */
    @Insert("INSERT INTO user(username, password, email) VALUES(#{username}, #{password}, #{email})")
    @Options(useGeneratedKeys = true, keyProperty = "id")
    int addUser(User user);

    /**
     * 更新用户（注解方式）
     * 日志输出：会显示更新的参数
     */
    @Update("UPDATE user SET username = #{username}, password = #{password}, email = #{email} WHERE id = #{id}")
    int updateUser(User user);

    /**
     * 删除用户（注解方式）
     * 日志输出：会显示删除的参数
     */
    @Delete("DELETE FROM user WHERE id = #{id}")
    int deleteUser(Integer id);

    /**
     * 根据用户名模糊查询（注解方式）
     * 注意：${value} 是字符串拼接，有 SQL 注入风险
     * 日志输出：会显示完整的 SQL 语句
     */
    @Select("SELECT * FROM user WHERE username = '%${value}%'")
    List<User> findByUsernameLike(String username);
```

**代码落点 2：测试里的结论注释（老师原话）**

`课程/3/code/UserMapperAnnotationTest.java`　**L111–L131**

```java
    //根据用户名模糊查询 #{} 和 ${} 的区别
    //#{value} 是参数绑定，不会被 SQL 注入  使用的是?占位符
    //${value} 是字符串拼接，有 SQL 注入风险  '%${value}%'
    // select * from user where uname='user' and password='123456' or 1=1
    @Test
    public void testFindByUsername() {
        System.out.println("========== 测试注解方式根据用户名模糊查询 ==========");

        SqlSession sqlSession = sqlSessionFactory.openSession();

        UserMapperAnnotation userMapper = sqlSession.getMapper(UserMapperAnnotation.class);

        List<User> users = userMapper.findByUsernameLike("z");
        for (User user : users) {
            System.out.println(user);
        }



        sqlSession.close();
    }
```

**代码落点 3：注解 Mapper 的注册（`class` 单个 / `package` 批量）**

`课程/3/code/mybatis-config-annotation.xml`　**L34–L41**

```xml
    <!-- 注册 Mapper（注解方式） -->
    <mappers>
        <!-- 方式1：单独注册注解 sql操作的接口类-->
        <mapper class="com.chapter01.UserMapperAnnotation"/>

        <!-- 方式2：批量注册（推荐） -->
        <!-- <package name="com.chapter01"/> -->
    </mappers>
```

**易错点**

- `#{}` 里写的是**属性名**，不是列名：`#{username}` 取的是参数对象的 `getUsername()`。
- `${}` 拼接字符串时要自己加引号（`'${name}'`），否则 SQL 语法错。
- 注解方式多参数必须 `@Param("名字")`，否则 XML/注解里只能用 `arg0/param1`。

---

## 11. resultType、resultMap 与 Map 返回（自定义返回结果集）

**题型**：填空题“自定义返回结果集：resultType 和 map”；简答题“usermapper：resultType 和 map”

**定义**

- **`resultType`**：直接指定返回类型，MyBatis 把**列名 → 属性名**自动映射。
  - 要求：列名与属性名一致；不一致时用 **SQL 别名**（`id AS uid`）或开 `mapUnderscoreToCamelCase`（`create_time` → `createTime`）。
  - 返回 `java.util.Map` 时，列名就是 map 的 key（适合聚合/动态列）。
- **`resultMap`**：自定义“列 ↔ 属性”映射，适合：
  - 列名与属性名不一致；主键/普通字段要显式声明；
  - 一对一/一对多/多对多（`association` / `collection`）；
  - 需要复用映射规则。
- **二者互斥**：同一个 `<select>` 不能同时写 `resultType` 和 `resultMap`。
- **`resultType="map"`**：一行 → 一个 `Map<String,Object>`；多行 → `List<Map<...>>`；`selectMaps(wrapper)` 是 MP 的同类能力。

**代码落点 1：`resultType` + SQL 别名（列名不一致的解法一）**

`课程/4/code/4-1/UserMapper (2).xml`　**L64–L71**

```xml
    <!-- 查询所有用户（别名：selectAll） -->
    <select id="selectAll" resultType="com.entity.User">
        select id as uid , username, password ,email from `user`
    </select>

    <select id="selectAllVO" resultType="com.entity.Vo">
        select id as p1 , username AS p2, password as p3 from `user`
    </select>
```

**代码落点 2：`resultMap` + VO（解法二，自由度更高）**

`课程/4/code/4-1/UserMapper (2).xml`　**L73–L92**

```xml
    <!--

    为了替换resultType的使用resultMap 自由度更高 自定义一个返回类型 可以和任何的模型进行映射
    id:自定义的类型的名
    type:自定义的类型的类(有具体的哪个类做模版)
     详细编写 映射规则  id 主键映射 只能出现一次 result 其他字段映射 可以出现多个

     强调: resultMap 不能和 resultType 同时使用 互斥

    -->

    <resultMap id="userResultMap" type="com.entity.Vo">
        <id     property="p1"          column="id"/>
        <result property="p2"    column="username"/>
        <result property="p3"    column="password"/>

    </resultMap>
    <select id="selectAllByVo" resultMap="userResultMap">
        SELECT *  FROM user
    </select>
```

**代码落点 3：VO 类（属性名 P1/P2/P3 与列名完全无关）**

`课程/4/code/4-1/Vo.java`　**L3–L16**

```java
public class Vo { //创建一个VO类 用于封装查询结果

    private Integer P1;
    private String P2;
    private String P3;

    public Vo() {
    }

    public Vo(Integer p1, String p2, String p3) {
        P1 = p1;
        P2 = p2;
        P3 = p3;
    }
```

**代码落点 4：标准 `resultMap`（下划线列 → 驼峰属性）**

`课程/4/code/4-2/UserMapper (3).xml`　**L20–L27**

```xml
    <resultMap id="userResultMap" type="com.entity.User">
        <id     property="id"          column="id"/>
        <result property="username"    column="username"/>
        <result property="password"    column="password"/>
        <result property="email"       column="email"/>
        <result property="createTime"  column="create_time"/>
        <result property="updateTime"  column="update_time"/>
    </resultMap>
```

**代码落点 5：注解版 `@Results` / `@ResultMap`（含跨 XML 引用）**

`课程/4/code/4-2/UserMapper.java`　**L30–L73**

```java
    /**
     * 注解方式 1: 直接在方法上定义匿名 ResultMap
     * 适合只给当前方法用的简单映射
     */
    @Select("SELECT * FROM user WHERE id = #{id}")
    @Results({
            @Result(property = "id",       column = "id",           id = true),
            @Result(property = "username", column = "username"),
            @Result(property = "password", column = "password"),
            @Result(property = "email",    column = "email"),
            @Result(property = "createTime", column = "create_time"),
            @Result(property = "updateTime", column = "update_time")
    })
    User findByIdAnno(Integer id);

    /**
     * 注解方式 2: 在方法上定义【命名 ResultMap】，供 @ResultMap 重复引用
     * 适合多个方法共用同一套映射
     */
    @Select("SELECT * FROM user WHERE id = #{id}")
    @Results(id = "annoUserMap", value = {
            @Result(property = "id",       column = "id",           id = true),
            @Result(property = "username", column = "username"),
            @Result(property = "password", column = "password"),
            @Result(property = "email",    column = "email"),
            @Result(property = "createTime", column = "create_time"),
            @Result(property = "updateTime", column = "update_time")
    })
    User findByIdWithAnnoMap(Integer id);

    /**
     * 注解方式 3: @ResultMap 引用【注解定义的命名 ResultMap】
     */
    @Select("SELECT * FROM user")
    @ResultMap("annoUserMap")
    List<User> findAllByAnnoMap();

    /**
     * 注解方式 4: @ResultMap 引用【XML 中定义的 ResultMap】
     * 跨方式引用 —— 注解写 SQL，但映射规则复用 XML 的 userResultMap
     */
    @Select("SELECT * FROM user WHERE username LIKE CONCAT('%', #{kw}, '%')")
    @ResultMap("userResultMap")
    List<User> findLikeByXmlMap(@Param("kw") String keyword);
```

**得分点（简答）**

1. `resultType`：自动映射，列名必须对得上（或别名/驼峰）；适合单表、DTO 字段与列一致的场景。
2. `resultMap`：手动映射，列名任意；支持主键、关联、集合；适合多表/字段不一致。
3. 二者**互斥**；`resultType="map"` 适合不确定列或聚合查询。
4. 注解版对应 `@Results`（可命名，供 `@ResultMap` 复用）。

---

## 12. 动态 SQL 标签

**题型**：多选题“动态标签 of Mybatis”；填空题“mb：标签”

**定义（6 个核心标签）**

| 标签 | 作用 | 关键点 |
|---|---|---|
| `<if test="…">` | 条件拼接 | `test` 用 OGNL：`username != null and username != ''` |
| `<where>` | 代替 `WHERE` | 有条件才加 `WHERE`；自动去掉**开头**多余的 `AND/OR` |
| `<set>` | 代替 `SET` | 自动加 `SET`；自动去掉**末尾**多余的逗号 |
| `<choose>/<when>/<otherwise>` | 互斥分支 | 只命中第一个 `when`，相当于 if–else if–else |
| `<foreach>` | 遍历集合 | `collection/item/open/separator/close`；批量插入用 `separator=","` |
| `<trim>` | 自定义裁剪 | `prefix/suffix/prefixOverrides/suffixOverrides`；`<where>/<set>` 的本质 |
| `<sql>` + `<include>` | 片段复用 | `refid` 引用；片段内可含动态标签 |

**代码落点 1：`<if>` + `<where>`、`<set>`**

`课程/4/code/4-2/UserMapper (3).xml`　**L46–L85**

```xml
    <!--
        1. <if> + <where>  条件查询
           <where> 的作用：
             · 如果没有任何条件 → 自动去掉 WHERE 关键字（不会语法错误）
             · 如果第一个条件带了 AND → 自动去掉首个 AND
           场景：多条件任意组合，有哪个查哪个
    -->
    <select id="findUsersByCondition" parameterType="com.entity.User"
            resultMap="userResultMap">
        SELECT * FROM user
        <where>
            <if test="username != null and username != ''">
                AND username LIKE CONCAT('%', #{username}, '%')
            </if>
            <if test="email != null and email != ''">
                AND email = #{email}
            </if>
            <if test="id != null">
                AND id = #{id}
            </if>
        </where>
    </select>

    <!--
        2. <set>  动态更新
           <set> 的作用：
             · 自动加上 SET 关键字
             · 自动去掉末尾多余的逗号
           场景：只更新非空字段，避免把 null 写回数据库
    -->
    <update id="updateUserSelective" parameterType="com.entity.User">
        UPDATE user
        <set>
            <if test="username != null">username = #{username},</if>
            <if test="password != null">password = #{password},</if>
            <if test="email != null">email = #{email},</if>
            <if test="updateTime != null">update_time = #{updateTime},</if>
        </set>
        WHERE id = #{id}
    </update>
```

**代码落点 2：`<choose>` 与 `<foreach>`（IN 查询 / 批量插入）**

`课程/4/code/4-2/UserMapper (3).xml`　**L87–L146**

```xml
    <!--
        3. <choose>/<when>/<otherwise>  互斥分支
           相当于 Java 的 if - else if - else
           只命中第一个满足条件的 when，后续全部跳过
           <otherwise> 兜底（相当于最后的 else）
           场景：多个条件有优先级，只取最优先的那一个
    -->
    <select id="findUserPriority" parameterType="com.entity.User"
            resultMap="userResultMap">
        SELECT * FROM user
        <where>
            <choose>
                <when test="id != null">
                    id = #{id}
                </when>
                <when test="username != null and username != ''">
                    username LIKE CONCAT('%', #{username}, '%')
                </when>
                <when test="email != null and email != ''">
                    email = #{email}
                </when>
                <otherwise>
                    1 = 1
                </otherwise>
            </choose>
        </where>
    </select>

    <!--
        4. <foreach>  批量查询（IN 条件）
           属性说明：
             collection="ids"   对应 Java 接口参数 @Param("ids")
             item="id"          遍历中每个元素的变量名
             open="("           开头
             separator=","      分隔符
             close=")"          结尾
           拼接结果：WHERE id IN (1, 2, 3)
    -->
    <select id="findByIds" resultMap="userResultMap">
        SELECT * FROM user
        WHERE id IN
        <foreach collection="ids" item="id"
                 open="(" separator="," close=")">
            #{id}
        </foreach>
    </select>

    <!--
        5. <foreach>  批量插入
           遍历 List<User>，每次迭代生成一条 VALUES 子句
           collection="list"  对应 List<User> 参数（默认名称就是 list）
           拼接结果：VALUES (?, ?, ...), (?, ?, ...), ...
    -->
    <insert id="batchInsert" parameterType="java.util.List">
        INSERT INTO user(username, password, email, create_time, update_time)
        VALUES
        <foreach collection="list" item="u" separator=",">
            (#{u.username}, #{u.password}, #{u.email}, #{u.createTime}, #{u.updateTime})
        </foreach>
    </insert>
```

**代码落点 3：`<trim>` 与 `<sql>/<include>`**

`课程/4/code/4-2/UserMapper (3).xml`　**L148–L199**

```xml
    <!--
        6. <trim>  自定义字符串裁剪
           属性说明：
             prefix="WHERE"          前缀（存在时才加上）
             suffix=""               后缀
             prefixOverrides="AND |OR "   去掉开头的 AND 或 OR
             suffixOverrides=","      去掉末尾的逗号
           <where> / <set> 本质上就是 <trim> 的特殊写法
    -->
    <select id="findUsersByTrim" parameterType="com.entity.User"
            resultMap="userResultMap">
        SELECT * FROM user
        <trim prefix="WHERE" prefixOverrides="AND |OR ">
            <if test="username != null and username != ''">
                AND username LIKE CONCAT('%', #{username}, '%')
            </if>
            <if test="email != null and email != ''">
                AND email = #{email}
            </if>
        </trim>
    </select>

    <!--
        7. <include> 引用 <sql> 片段
           refid 关联上面定义的 <sql> 的 id
           <sql> 片段可以包含动态 SQL，被 <include> 插入后会继续解析
    -->

    <!--
       <sql> 定义可复用的 SQL 片段，<include> 引用该片段
       片段中可以包含动态 SQL 标签（<if>、<foreach> 等）
   -->
    <sql id="userColumns">
        id, username, password, email, create_time, update_time
    </sql>

    <sql id="commonWhereCondition">
        <if test="username != null and username != ''">
            AND username LIKE CONCAT('%', #{username}, '%')
        </if>
        <if test="email != null and email != ''">
            AND email = #{email}
        </if>
    </sql>

    <select id="findUsersWithInclude" parameterType="com.entity.User"
            resultMap="userResultMap">
        SELECT <include refid="userColumns"/> FROM user
        <where>
            <include refid="commonWhereCondition"/>
        </where>
    </select>
```

**易错点**

- `<where>` 只去掉**第一个** `AND/OR`；条件顺序写错仍可能语法错。
- `<set>` 只去掉**最后一个逗号**；每个 `<if>` 里的逗号要写在字段后。
- `<foreach collection="list">` 的默认名是 `list`（List 参数）或 `array`（数组）；用 `@Param("ids")` 后必须写 `ids`。
- 注解方式写动态 SQL 要 `<script>...</script>` 包住，且双引号要转义——复杂 SQL 一律用 XML。

---

## 13. 关联映射：多对一 / 一对多（简答 emp）

**题型**：填空题“动态 sql：多对一，一对多”；简答题“mb-empmapper 查询 多对一/一对多”

**定义**

- **多对一**：多个员工属于一个部门。Java 侧 `Emp` 里有一个 `Dept dept`；XML 用 `<association property="dept" javaType="Dept">`；注解用 `@One`。
- **一对多**：一个部门有多个员工。Java 侧 `Dept` 里有一个 `List<Emp> emps`；XML 用 `<collection property="emps" ofType="Emp">`；注解用 `@Many`。
- **`javaType` vs `ofType`**：`javaType` 是属性本身的类型（单个对象）；`ofType` 是集合里**元素**的类型（`List<Emp>` → `Emp`）。
- 两种实现：
  1. **嵌套结果**：一条 JOIN 查全部列，`resultMap` 内逐列映射；多表同名字段（`deptno`）必须起别名区分。
  2. **嵌套 select**：主查询查主表，`association/collection` 的 `select` 指向另一个查询，`column` 传参；会产生 **N+1** 次查询；`lazyLoadingEnabled=true` 可延迟加载。
- **一对一与多对一在 MyBatis 写法相同**：都是“一个对象”，都用 `association/@One`；区别只在业务语义与从哪侧发起查询。

**代码落点 1：多对一（嵌套结果）**

`课程/5/code/chapter05.rar → chapter05mapper/mapper/Chapter05EmpMapper.xml`　**L8–L28**

```xml
    <!-- ========== ResultMap  Emp的dept对象结构 ========== -->

    <resultMap id="empWithDeptMap" type="com.entity.Emp">
        <id property="empno" column="empno"/>
        <result property="ename" column="ename"/>
        <result property="job" column="job"/>
        <result property="mgr" column="mgr"/>
        <result property="hiredate" column="hiredate"/>
        <result property="sal" column="sal"/>
        <result property="comm" column="comm"/>
        <result property="deptno" column="emp_deptno"/>
        <!--此时的书写为association代表是一个对象    one2Many的many一方
        association: 一个对象  one2one ,  one2Many的many
        collection:一个集合  one2many的one的一方 ,many2many 的书写
        -->
        <association property="dept" javaType="com.entity.Dept">
            <id property="deptno" column="deptno"/>
            <result property="dname" column="dname"/>
            <result property="loc" column="loc"/>
        </association>
    </resultMap>
```

**代码落点 2：一对多（嵌套结果）**

`课程/5/code/chapter05.rar → chapter05mapper/mapper/Chapter05DeptMapper.xml`　**L8–L36**

```xml
    <!-- ========== ResultMap ========== -->

    <resultMap id="deptWithEmpsMap" type="com.entity.Dept">
        <id property="deptno" column="deptno"/>
        <result property="dname" column="dname"/>
        <result property="loc" column="loc"/>
        <!--此时resultMap中使用的是collection ,表示是一个集合 one2Many的on饿的一方设计-->
        <collection property="emps" ofType="com.entity.Emp">
            <id property="empno" column="empno"/>
            <result property="ename" column="ename"/>
            <result property="job" column="job"/>
            <result property="mgr" column="mgr"/>
            <result property="hiredate" column="hiredate"/>
            <result property="sal" column="sal"/>
            <result property="comm" column="comm"/>
            <result property="deptno" column="emp_deptno"/>
        </collection>
    </resultMap>

    <!-- ========== 一对多（XML方式 携带了一个员工的参数)========== -->
    <select id="one2manyByXml" parameterType="int" resultMap="deptWithEmpsMap">
        SELECT d.deptno, d.dname, d.loc,
               e.empno, e.ename, e.job, e.mgr, e.hiredate, e.sal, e.comm,
               e.deptno AS emp_deptno
        FROM dept d
        LEFT JOIN emp e ON d.deptno = e.deptno
        WHERE d.deptno = #{deptno}
        ORDER BY e.empno
    </select>
```

**代码落点 3：一对一 / 多对一的 SQL**

`课程/5/code/chapter05.rar → chapter05mapper/mapper/Chapter05EmpMapper.xml`　**L46–L64**

```xml
    <!-- ========== 一对一（XML方式）========== -->
    <select id="one2oneByXml" parameterType="int" resultMap="empWithDeptMap">
        SELECT e.empno, e.ename, e.job, e.sal, e.mgr, e.hiredate, e.comm,
               e.deptno AS emp_deptno,
               d.deptno, d.dname, d.loc
        FROM emp e
        LEFT JOIN dept d ON e.deptno = d.deptno
        WHERE e.empno = #{empno}
    </select>

    <!-- ========== 多对一（XML方式）========== -->
    <select id="many2oneByXml" resultMap="empWithDeptMap">
        SELECT e.empno, e.ename, e.job, e.sal, e.mgr, e.hiredate, e.comm,
               e.deptno AS emp_deptno,
               d.deptno, d.dname, d.loc
        FROM emp e
        LEFT JOIN dept d ON e.deptno = d.deptno
        ORDER BY e.empno
    </select>
```

**代码落点 4：注解版 `@One`（一对一/多对一，写法相同）**

`课程/5/code/chapter05.rar → chapter05Java/Chapter05EmpMapper.java`　**L13–L28**

```java
    Emp one2oneByXml(Integer empno);

    @Select("SELECT e.empno, e.ename, e.job, e.sal, e.deptno, " +
            "d.deptno AS d_deptno, d.dname, d.loc " +
            "FROM emp e LEFT JOIN dept d ON e.deptno = d.deptno " +
            "WHERE e.empno = #{empno}")
    @Results({
            @Result(property = "empno", column = "empno"),
            @Result(property = "ename", column = "ename"),
            @Result(property = "job", column = "job"),
            @Result(property = "sal", column = "sal"),
            @Result(property = "deptno", column = "deptno"),
            @Result(property = "dept", column = "deptno",
                    one = @One(select = "com.chapter05.Chapter05DeptMapper.findById"))
    })
    Emp one2oneByAnn(Integer empno);
```

**代码落点 5：注解版 `@Many`（一对多）**

`课程/5/code/chapter05.rar → chapter05Java/Chapter05DeptMapper.java`　**L15–L25**

```java
    Dept one2manyByXml(Integer deptno);

    @Select("SELECT * FROM dept WHERE deptno = #{deptno}")
    @Results({
            @Result(property = "deptno", column = "deptno"),
            @Result(property = "dname", column = "dname"),
            @Result(property = "loc", column = "loc"),
            @Result(property = "emps", column = "deptno",
                    many = @Many(select = "com.chapter05.Chapter05EmpMapper.selectListByDeptno"))
    })
    Dept one2manyByAnn(Integer deptno);
```

**代码落点 6：延迟加载开关**

`课程/5/code/chapter05.rar → chapter05mapper/mybatis-config.xml`　**L10–L15**

```xml
    <settings>
        <setting name="logImpl" value="LOG4J"/>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <setting name="lazyLoadingEnabled" value="true"/>
        <setting name="aggressiveLazyLoading" value="false"/>
    </settings>
```

**得分点（简答）**

1. 关系判定：看外键在哪张表。`emp.deptno` 外键 → 员工看部门是**多对一**；部门看员工是**一对多**。
2. 多对一：`<association javaType>` / `@One`；一对多：`<collection ofType>` / `@Many`。
3. 嵌套结果 vs 嵌套 select 的区别：一条 JOIN vs 多次查询；后者有 N+1，可延迟加载。
4. 同名字段必须用别名（`e.deptno AS emp_deptno`），否则映射串列。

---

## 14. 缓存：一级 / 二级（分级与绑定对象）

**题型**：多选题“缓存：分级、和谁绑定”

**定义**

| | 一级缓存 | 二级缓存 |
|---|---|---|
| 名称 | LocalCache | Mapper Cache |
| **和谁绑定** | **SqlSession**（一个数据库会话） | **Mapper 的 namespace**（同一 Mapper 的所有 SqlSession 共享） |
| 默认 | **开启**，不能直接关 | **关闭**，需手动开 |
| 生效条件 | 同一个 SqlSession、同一条 SQL、同一组参数 | ①`cacheEnabled=true` ②`<cache/>` 或 `@CacheNamespace` ③实体 `Serializable` ④`commit()`/`close()` 才提交 |
| 失效 | 增删改 / `commit` / `rollback` / `close` / `clearCache` | 本 Mapper 的增删改（`flushCache=true`）/ 手动清 |
| 返回对象 | 同一个对象引用 | `readOnly=false` 返回拷贝（安全）；`true` 返回本体 |
| 关闭方式 | 只能 `localCacheScope=STATEMENT` 禁用 | 不加 `<cache/>` 即可 |

**查询顺序**：一级缓存 → 二级缓存 → 数据库；查库结果先写一级，`commit/close` 时再写二级。

**代码落点 1：两级缓存的定义与失效（课件注释，直接可背）**

`课程/7/code/CacheTest.java`　**L15–L45**

```java
/**
 * MyBatis 缓存机制完整演示
 *
 * ── 一级缓存（LocalCache）───────────────────────────────────────
 * · 作用域：同一个 SqlSession 内,具体的一个数据库的连接对象
 * · 默认开启，无法关闭（只能通过 localCacheScope=STATEMENT 禁用）
 * · 触发失效：增删改 / commit() / rollback() / close() / clearCache() --会手动的清空一级存存
 *
 * ── 二级缓存（Mapper Cache）─────────────────────────────────────
 * · 作用域：同一个 Mapper 的所有 SqlSession 共享
 * · 默认不开启，需要：
 *     ① 全局 cacheEnabled=true（默认就是 true）
 *     ② Mapper XML 中加 <cache/> 或接口 @CacheNamespace
 *     ③ 实体类 implements Serializable
 *     ④ SqlSession 执行 commit() 或 close()（缓存才提交）
 * · 触发失效：增删改 / 手动 flushCache
 * · 互不影响：不同 Mapper 的二级缓存互相隔离
 *
 * ── 缓存查询流程 ────────────────────────────────────────────────
 *   查询请求
 *     ↓
 *   查一级缓存（当前 SqlSession）── 命中 → 直接返回
 *     ↓ 未命中
 *   查二级缓存（当前 Mapper 所有 SqlSession 共享）── 命中 → 返回并写入一级
 *     ↓ 未命中
 *   查数据库 → 结果写入一级缓存 → （commit/close 时）写入二级缓存
 *
 * ── 日志中的关键字 ──────────────────────────────────────────────
 *   "Preparing: ..."  —— 真的发了 SQL 到数据库
 *   "==>  Preparing"  —— 同上
 *   没有 SQL 日志      —— 走了缓存！
```

**代码落点 2：一级缓存命中（同一 SqlSession，`s1 == s2`）**

`课程/7/code/CacheTest.java`　**L61–L85**

```java
    @Test
    public void testL1Cache_sameSqlSession() {
        System.out.println("╔══════════════════════════════════════════════════════════╗");
        System.out.println("║ 一、一级缓存：同一个 SqlSession 中，相同查询只发 1 次 SQL ║");
        System.out.println("╚══════════════════════════════════════════════════════════╝\n");
        //前提 ：同一个 SqlSession 中 进行sql的查询
        SqlSession sqlSession = sqlSessionFactory.openSession(); // 打开一个数据库连接对象 使用一级缓存
        StudentMapper mapper = sqlSession.getMapper(StudentMapper.class);

        System.out.println(">>> 第 1 次 selectById(1)");
        Student s1 = mapper.selectById(1); //查询后的结果会被缓存到一级缓存中
        System.out.println("    结果: " + s1.getName());

        System.out.println("\n>>> 第 2 次 selectById(1) —— 应该命中一级缓存，不发 SQL！");
        Student s2 = mapper.selectById(1);//执行的sql语句和参数与第1次查询相同，所以命中一级缓存
        System.out.println("    结果: " + s2.getName());

        System.out.println("\n>>> 第 3 次 selectById(2) —— id 不同，缓存 key 不同，要发 SQL");
        Student s3 = mapper.selectById(2);//执行的sql语句和参数与第1次查询不同，所以不命中一级缓存
        System.out.println("    结果: " + s3.getName());

        System.out.println("\n>>> s1 == s2 ? " + (s1 == s2) + "（同一个对象！一级缓存直接返回引用）");

        sqlSession.close();
    }
```

**代码落点 3：二级缓存跨 SqlSession（close 才提交）**

`课程/7/code/CacheTest.java`　**L166–L185**

```java
    @Test
    public void testL2Cache_basic() {
        System.out.println("╔══════════════════════════════════════════════════════════════╗");
        System.out.println("║ 五、二级缓存：跨 SqlSession 共享（关键：close/commit 才提交）║");
        System.out.println("╚══════════════════════════════════════════════════════════════╝\n");

        System.out.println(">>> ===== Session1：查询后关闭（数据提交到二级缓存）=====");
        SqlSession session1 = sqlSessionFactory.openSession();
        StudentMapper m1 = session1.getMapper(StudentMapper.class);
        m1.selectById(1);
        System.out.println("    Session1 关闭，缓存数据提交到二级缓存");
        session1.close();//关闭session1，提交一级缓存数据到二级缓存

        System.out.println("\n>>> ===== Session2：相同 Mapper，应该命中二级缓存！=====");
        SqlSession session2 = sqlSessionFactory.openSession();
        StudentMapper m2 = session2.getMapper(StudentMapper.class);
        m2.selectById(1);
        System.out.println("    如果没看到 SQL 日志 → 命中二级缓存 ✅");
        session2.close();
    }
```

**代码落点 4：`<cache/>` 与语句级开关**

`课程/7/第2节 二级缓存：Mapper 级别_详细版.html → 完整源码 → src/main/resources/chapterCatch/mapper/StudentMapper.xml`　**L1–L25**

```xml
<mapper namespace="com.chapterCatch.mapper.StudentMapper">

    <cache eviction="LRU" size="1024" flushInterval="60000" readOnly="false"/>

    <resultMap id="StudentMap" type="com.chapterCatch.entity.Student">
        <id     column="id"     property="id"/>
        <result column="name"   property="name"/>
        <result column="age"    property="age"/>
        <result column="email"  property="email"/>
        <result column="major"  property="major"/>
        <result column="score"  property="score"/>
    </resultMap>

    <select id="selectById" resultMap="StudentMap" useCache="true">
        SELECT id, name, age, email, major, score FROM student WHERE id = #{id}
    </select>

    <select id="selectByMajor" resultMap="StudentMap" useCache="true">
        SELECT id, name, age, email, major, score FROM student WHERE major = #{major}
    </select>

    <!-- useCache=false：不进二级缓存，每次都查库 -->
    <select id="selectAll" resultMap="StudentMap" useCache="false">
        SELECT id, name, age, email, major, score FROM student
    </select>
```

**易错点**

- 一级缓存“关不掉”，只能 `localCacheScope=STATEMENT` 让它退化成语句级。
- 二级缓存必须 `close()`/`commit()` 才把一级数据提交到二级；只查不关，下一个 Session 命中不了。
- 二级缓存按 **namespace** 隔离，多表查询可能读到旧数据（跨 Mapper 不会互相清空）。

---

# 五、MyBatis-Plus

## 15. MP 核心组件与实体注解

**题型**：选择题“mp：四大组件 注解”

**说明**：课件没有“四大组件”这个术语。它实际讲了两组“四/五”：

- **实体五大注解**：`@TableName`、`@TableId`、`@TableField`、`@TableLogic`、`@Version`。
- **BaseMapper 四大天王（最常用四方法）**：`insert`、`selectById`、`updateById`、`deleteById`。

**考试怎么选**：如果选项是**注解**，选 `@TableName` / `@TableId` / `@TableField` / `@TableLogic`（第五个是 `@Version`）；如果选项是**方法**，选 `insert` / `selectById` / `updateById` / `deleteById`。课件没有把 Wrapper、分页插件、GlobalConfig 统称为“四大组件”，不要硬凑这四个词。

**定义**

- `BaseMapper<T>`：只要 `interface XxxMapper extends BaseMapper<T>`，不写 SQL、不写 XML，就获得单表 17 个方法（增删改查、批量、分页）。
- `@TableName("表名")`：类名与表名不一致时指定。
- `@TableId(type = IdType.AUTO)`：主键字段与策略（`AUTO` 自增、`ASSIGN_ID` 雪花、`ASSIGN_UUID`、`INPUT`）。
- `@TableField`：列名映射、`updateStrategy`（null 不更新）、`fill`（自动填充）。
- `@TableLogic`：逻辑删除（第 16 节）。
- `@Version`：乐观锁（第 17 节）。
- MP 必须走自己的构建链：`MybatisXMLConfigBuilder` → `MybatisConfiguration` → `MybatisSqlSessionFactoryBuilder`；用原生 `SqlSessionFactoryBuilder` 会 `Invalid bound statement`。

**代码落点 1：实体上的五个注解**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/entity/Student.java`　**L30–L93**

```java
@TableName("mp_student")  //指定表名 标准的映射关系
@Data //自动添加getter和setter方法
@AllArgsConstructor
@NoArgsConstructor
public class Student implements Serializable { //创建一个模型类

    private static final long serialVersionUID = 1L;

    /**
     * 主键 —— 数据库自增
     * IdType.AUTO：数据库自增（最常用）
     * 其他策略：ASSIGN_ID(雪花算法)、ASSIGN_UUID、INPUT(手动赋值) 等
     */
    @TableId( value = "id", type = IdType.AUTO)
    private Long id;

    /**
     * 姓名 —— 普通字段
     * 表字段名默认为 name（驼峰转下划线），若不一致可用 value 属性指定
     */
    @TableField("name")
    private String name;

    private Integer age;

    private String email;

    private String major;

    /**
     * 分数 —— 演示 updateStrategy = NOT_NULL
     * 当 score 为 null 时，UPDATE 语句不会包含该字段（避免把原值覆盖为 null）
     */
    @TableField(updateStrategy = FieldStrategy.NOT_NULL) //字段取值上的约束，当值为null时，不更新该字段
    private Double score;

    /**
     * 乐观锁版本号
     * 更新时 MP 自动追加 WHERE version = 旧值，并 SET version = 旧值+1
     * 配合 MybatisPlusConfig 中的 OptimisticLockerInnerInterceptor 插件生效
     */
    @Version
    private Integer version;

    /**
     * 逻辑删除标记
     * 0 = 未删除，1 = 已删除
     * 删除时执行 UPDATE SET deleted = 1，查询时自动追加 WHERE deleted = 0
     */
    @TableLogic
    private Integer deleted;

    /**
     * 创建时间 —— 自动填充（INSERT 时填充）
     * 填充逻辑在 MyMetaObjectHandler 中实现
     */
    @TableField(fill = FieldFill.INSERT)
    private LocalDateTime createTime;

    /**
     * 更新时间 —— 自动填充（INSERT 和 UPDATE 时都填充）
     */
    @TableField(fill = FieldFill.INSERT_UPDATE)
    private LocalDateTime updateTime;
```

**代码落点 2：BaseMapper 零 SQL**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/mapper/StudentMapper.java`　**L40–L42**

```java
public interface StudentMapper extends BaseMapper<Student> {
 //创建一个对应Student表的Mapper接口
}
```

**代码落点 3：插件链（分页/防全表/乐观锁）**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/config/MybatisPlusConfig.java`　**L23–L30**

```java
    public static MybatisPlusInterceptor buildInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        //分页插件：必加，否则 selectPage 不生效
        PaginationInnerInterceptor pagination = new PaginationInnerInterceptor(DbType.MYSQL);
        pagination.setMaxLimit(500L);
        interceptor.addInnerInterceptor(pagination);
//乐观锁插件
        interceptor.addInnerInterceptor(new BlockAttackInnerInterceptor()); // 防止全表更新删除
```

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/config/MybatisPlusConfig.java`　**L91–L93**

```java
        interceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());

        return interceptor;
```

**易错点**

- 包名是 `chaperMybatisPlus`（少一个 `t`），照抄项目拼写，别自动“纠正”。
- `@TableLogic` 与 `@Version` 都需要**插件/配置**配合；只加注解不生效。
- `BaseMapper` 只能做**单表**；多表要自己写 XML/注解 SQL。

---

## 16. 逻辑删除

**题型**：选择题“逻辑删除”

**定义**

- **物理删除**：`DELETE FROM 表 WHERE id=?`，数据真的没了。
- **逻辑删除**：表加标记列（如 `deleted`，0 未删 / 1 已删）；删除时执行 `UPDATE 表 SET deleted=1 WHERE id=?`；查询自动追加 `WHERE deleted=0`。
- MP 做法：实体字段加 `@TableLogic`；`deleteById` 自动改写成 UPDATE，`selectById/selectList/selectCount` 自动过滤已删除数据。
- 好处：可恢复、可审计、不破坏外键；坏处：表会变大、唯一索引要带删除标记、必须记得过滤。

**代码落点：`@TableLogic` 字段与注释**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/entity/Student.java`　**L74–L80**

```java
    /**
     * 逻辑删除标记
     * 0 = 未删除，1 = 已删除
     * 删除时执行 UPDATE SET deleted = 1，查询时自动追加 WHERE deleted = 0
     */
    @TableLogic
    private Integer deleted;
```

**得分点**

- 写清“**删改写、查加条件**”：`deleteById` → `UPDATE ... SET deleted=1`；`select` → 自动加 `WHERE deleted=0`。
- 需要真删时：自定义 SQL 或去掉 `@TableLogic`。

---

## 17. 乐观锁 / 悲观锁

**题型**：填空题“mp 乐观/悲观锁”

**定义**

| | 悲观锁 | 乐观锁 |
|---|---|---|
| 思想 | 先锁住再操作，认为冲突**一定**发生 | 先操作再校验，认为冲突**很少** |
| 数据库实现 | `SELECT ... FOR UPDATE` | `version` 字段 + `WHERE version=旧值` |
| MP 对应 | 手动写 `FOR UPDATE`（**无插件**） | `@Version` + `OptimisticLockerInnerInterceptor` |
| 并发 | 低（锁等待） | 高（无锁） |
| 场景 | 写多、冲突频繁、资金 | 读多写少、偶尔冲突 |

**乐观锁流程**：查数据拿到 `version=1` → 改内存对象 → 更新时插件改写成 `SET ..., version=version+1 WHERE id=? AND version=1` → 匹配到则成功；匹配不到 `rows=0`，业务重试或报错。

**代码落点 1：`@Version` 字段**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/entity/Student.java`　**L66–L72**

```java
    /**
     * 乐观锁版本号
     * 更新时 MP 自动追加 WHERE version = 旧值，并 SET version = 旧值+1
     * 配合 MybatisPlusConfig 中的 OptimisticLockerInnerInterceptor 插件生效
     */
    @Version
    private Integer version;
```

**代码落点 2：插件注册 + 两种锁的对照注释（课件原话）**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/config/MybatisPlusConfig.java`　**L40–L91**

```java
        // 【锁的两大流派对比】
        //
        //   ┌──────────────┬───────────────────────────┬──────────────────────┐
        //   │              │  悲观锁 Pessimistic Lock   │ 乐观锁 Optimistic Lock│
        //   ├──────────────┼───────────────────────────┼──────────────────────┤
        //   │ 核心思想     │ 先锁住再操作，冲突必发生   │ 先操作再校验，冲突少 │
        //   │ 数据库实现   │ SELECT ... FOR UPDATE     │ version 字段 + WHERE │
        //   │ MP 中对应    │ 手动加 FOR UPDATE        │ @Version + 本插件     │
        //   │ 并发吞吐     │ 低（锁等待）               │ 高（无锁）           │
        //   │ 适用场景     │ 写多、冲突频繁、资金操作   │ 读多写少、偶尔冲突   │
        //   └──────────────┴───────────────────────────┴──────────────────────┘
        //
        // 【乐观锁工作流程（本项目实际使用的方式）】
        //
        //   ① SELECT 读取数据时，拿到 version = 1
        //   ② 业务层修改对象（内存中）
        //   ③ UPDATE 时，OptimisticLockerInnerInterceptor 自动改写 SQL：
        //
        //        你写的：UPDATE student SET score=66 WHERE id=3
        //        插件改：UPDATE student SET score=66, version=version+1
        //                               WHERE id=3 AND version=1
        //
        //   ④ WHERE version=1 匹配到 → 更新成功，version 自动 +1
        //      匹配不到（被别人抢先改过了） → rows=0，业务层自行重试/报错
        //
        // 【本项目中的完整配置链】
        //
        //   DB 表： student 表必须有 version 列（INT，默认值 0）
        //   实体类：@Version  private Integer version;        ← 见 Student.java:70
        //   插件：  下一行 ↓
        //   业务层：updateById(student) 即可，无需手动管理 version
        //
        // 【冲突时怎么办？】rows=0 说明乐观锁冲突，典型处理方式：
        //
        //   // 方案一：简单重试（适合冲突极少的场景）
        //   for (int i = 0; i < 3; i++) {
        //       Student s = studentMapper.selectById(id);
        //       s.setScore(newScore);
        //       if (studentMapper.updateById(s) > 0) break;
        //   }
        //
        //   // 方案二：抛异常让上层决定（推荐）
        //   if (studentMapper.updateById(s) == 0) {
        //       throw new RuntimeException("数据已被他人修改，请刷新后重试");
        //   }
        //
        // 【悲观锁简单对比（本项目未启用，了解即可）】
        //   // 写法：加 FOR UPDATE 锁住行直到事务结束
        //   SELECT * FROM student WHERE id = 3 FOR UPDATE
        //   // 其他线程必须等你 COMMIT/ROLLBACK 后才能读这行
        //   // 代价：长事务 + 锁等待，吞吐量下降
        interceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
```

**易错点**

- 乐观锁必须**先查后改**（要带旧 `version`）；直接 `new Student()` 只设 id 和 version 会更新 0 行。
- 悲观锁 `FOR UPDATE` 必须在**事务内**，否则锁立刻释放；长事务会拖垮吞吐。
- `@Version` 只对 `updateById` / `update(entity, wrapper)` 生效，自己写的 SQL 不管。

---

## 18. 分页与自动填充（MP 的另两个“组件”）

**题型**：选择题/填空题中与“mp 四大组件”同题出现

**定义**

- **分页**：`Page<T> page = new Page<>(页码, 每页条数)` → `mapper.selectPage(page, wrapper)` → `IPage` 回填 `total/pages/current/size/records`。必须注册 `PaginationInnerInterceptor`，否则不分页（内存分页/全量）。
- **自动填充**：实体字段标 `@TableField(fill = FieldFill.INSERT / INSERT_UPDATE)`；处理器实现 `MetaObjectHandler`，在 `insertFill/updateFill` 里 `strictInsertFill`（null 才填）或 `setFieldValByName`（强制覆盖）。处理器挂在 `GlobalConfig` 上，**不是** `InnerInterceptor`。

**代码落点 1：分页插件**

见第 15 节 `MybatisPlusConfig.java` L23–L30（`PaginationInnerInterceptor(DbType.MYSQL)` + `setMaxLimit(500)`）。

**代码落点 2：自动填充处理器**

`课程/6/code/chaperMybatisPlus.rar → chaperMybatisPlus/config/MyMetaObjectHandler.java`　**L21–L46**

```java
public class MyMetaObjectHandler implements MetaObjectHandler {

    @Override
    public void insertFill(MetaObject metaObject) {
        LocalDateTime now = LocalDateTime.now();

        /**
         * strictInsertFill —— 严格填充
         *   只有当字段为 null 时才填充（不会覆盖手动设置的值）
         *
         * setFieldValByName —— 强制填充
         *   不管字段是否已有值，都会覆盖
         *
         * 推荐用 strictInsertFill，更安全
         */
        this.strictInsertFill(metaObject, "createTime", LocalDateTime.class, now);
        this.strictInsertFill(metaObject, "updateTime", LocalDateTime.class, now);
    }

    @Override
    public void updateFill(MetaObject metaObject) {
        /**
         * INSERT_UPDATE 类型的字段，在 UPDATE 时也会走这里
         */
        this.strictUpdateFill(metaObject, "updateTime", LocalDateTime.class, LocalDateTime.now());
    }
```

**代码落点 3：填充注解字段**

见第 15 节 `Student.java` L82–L93（`@TableField(fill=...)`，不重复贴）。

**得分点**

- 分页三件套：`Page` 对象 + `selectPage` + `PaginationInnerInterceptor`。
- 自动填充四件套：`@TableField(fill)` + `MetaObjectHandler` + `GlobalConfig` 注册 + `strictInsertFill`。

---

# 六、SpringMVC

## 19. MVC 四大核心组件与执行流程

**题型**：选择题“mvc 四大核心：如何定义”

**定义（背这段）**

| 组件 | 作用 | 注解方式怎么来 | XML 方式怎么定义 |
|---|---|---|---|
| **DispatcherServlet** | 前端控制器，所有请求的统一入口 | `web.xml` 注册 Servlet | 同左 |
| **HandlerMapping** | 按 URL 找 Handler（Controller 方法） | `<mvc:annotation-driven>` 自动注册 `RequestMappingHandlerMapping` | `<bean class="...BeanNameUrlHandlerMapping"/>`（bean 名即 URL） |
| **HandlerAdapter** | 调用 Handler，完成参数绑定/返回值处理 | 同上自动注册 `RequestMappingHandlerAdapter` | `DispatcherServlet` 默认注册 `SimpleControllerHandlerAdapter`（实现 `Controller` 接口时） |
| **ViewResolver** | 逻辑视图名 → 物理 JSP 路径 | `<bean class="InternalResourceViewResolver">` + prefix/suffix | 同左 |

**执行流程**：

```text
浏览器 → DispatcherServlet
      → HandlerMapping（找 Handler）
      → HandlerAdapter（调 Handler，做参数绑定）
      → Controller / 拦截器链
      → ModelAndView 或 @ResponseBody
      → ViewResolver（逻辑视图名 → JSP）
      → View 渲染 → 响应
```

**代码落点 1：DispatcherServlet 注册**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/webapp/WEB-INF/web.xml`　**L65–L77**

```xml
    <servlet>
        <servlet-name>springmvc-annotation</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc/annotation/springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc-annotation</servlet-name>
        <url-pattern>/annotation/*</url-pattern>
    </servlet-mapping>
```

**代码落点 2：XML 方式的三要素（HandlerMapping + Controller + ViewResolver）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/resources/springmvc/xml/springmvc-servlet.xml`　**L18–L29**

```xml
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>

    <!-- ② 控制器：XML 方式的控制器不写任何注解，
            URL 完全由这里的 name 决定 → /xml/student/list -->
    <bean name="/student/list" class="com.springmvc.xml.StudentXmlController"/>

    <!-- ③ 视图解析器：把 ModelAndView 里的逻辑视图名拼成 JSP 路径
            studentList → prefix + "studentList" + suffix → /WEB-INF/views/studentList.jsp -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
```

**代码落点 3：注解方式由 `annotation-driven` 自动注册前两个组件**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/resources/springmvc/annotation/springmvc-servlet.xml`　**L14–L21**

```xml
    <!--
      SpringMVC 注解方式配置
      =====================================================
      ① <mvc:annotation-driven>：开启注解驱动
         - 注册 RequestMappingHandlerMapping（处理 @RequestMapping）
         - 注册 RequestMappingHandlerAdapter（参数绑定、@ResponseBody 转 JSON 等）
      ② <context:component-scan>：扫描 @RestController 所在包
    -->
```

**得分点**

- 四大核心按顺序写：`DispatcherServlet → HandlerMapping → HandlerAdapter → ViewResolver`。
- “如何定义”：`DispatcherServlet` 在 `web.xml` 注册；注解方式由 `<mvc:annotation-driven>` 自动注册 `RequestMappingHandlerMapping`/`RequestMappingHandlerAdapter`，XML 方式显式配 `BeanNameUrlHandlerMapping`，`HandlerAdapter` 由 `DispatcherServlet` 默认注册；`ViewResolver` 显式配 `prefix/suffix`。

---

## 20. Controller 两种写法与返回 JSON

**题型**：填空题“返回结果为 json，如何实现？”

**定义**

- 两种 Controller：
  1. **注解方式**：普通类 + `@Controller` / `@RestController` + `@RequestMapping`。
  2. **XML 方式**：类实现 `org.springframework.web.servlet.mvc.Controller`，返回 `ModelAndView`；`<bean name="/url">` 注册，`BeanNameUrlHandlerMapping` 把 bean 名当 URL。
- **返回 JSON 的 3 个条件**：
  1. 方法/类上有 `@ResponseBody`（或直接用 `@RestController` = `@Controller` + `@ResponseBody`）。
  2. `<mvc:annotation-driven>` 注册了 `MappingJackson2HttpMessageConverter`（需要 Jackson 依赖）。
  3. 对象由 Jackson 序列化；通常配合 `Accept: application/json` 或 `produces = "application/json"` 明确内容类型。
- `@RestController` 的方法返回值**直接写响应体**，不走 ViewResolver；返回 `String` 时也不是视图名。
- 中文乱码：`StringHttpMessageConverter` 默认 ISO-8859-1，需在 `annotation-driven` 里注册 UTF-8 的转换器（课件已配）。

**代码落点 1：`@RestController` + `@RequestMapping` + 返回 List/String**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/StudentController.java`　**L32–L72**

```java
@RestController
@RequestMapping("/student")
public class StudentController {

    /**
     * GET /student/hello —— 最简单的入门接口
     */
    @GetMapping("/hello")
    public String hello() {
        return "SpringMVC Controller is running";
    }

    /**
     * GET /student/list?major=CS —— @RequestParam 查询参数绑定
     * major 可不传（required=false，默认 null 返回全部）
     */
    @GetMapping("/list")
    public List<String> list(@RequestParam(required = false) String major) {
        List<String> all = new ArrayList<>();
        all.add("zhangsan / CS / 90.0");
        all.add("lisi / Math / 85.5");
        all.add("wangwu / CS / 78.0");
        if (major == null || major.isEmpty()) {
            return all;
        }
        List<String> filtered = new ArrayList<>();
        for (String s : all) {
            if (s.contains(major)) {
                filtered.add(s);
            }
        }
        return filtered;
    }

    /**
     * GET /student/detail/{id} —— @PathVariable 路径变量绑定
     */
    @GetMapping("/detail/{id}")
    public String detail(@PathVariable Integer id) {
        return "student id = " + id + "（Service 层重建后返回完整学生信息）";
    }
```

**代码落点 2：JSON 消息转换器（含 UTF-8）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/resources/springmvc/annotation/springmvc-servlet.xml`　**L22–L40**

```xml
    <!--
      【@ResponseBody/@RestController 中文乱码】
      StringHttpMessageConverter 默认 charset=ISO-8859-1，
      CharacterEncodingFilter 管不到它（转换器自己编码写出字节）→ 中文变 ?
      解决：在 annotation-driven 里注册 UTF-8 的 StringHttpMessageConverter
    -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/plain;charset=UTF-8</value>
                        <value>text/html;charset=UTF-8</value>
                        <value>application/json;charset=UTF-8</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
```

**得分点**

- 填空写：`@ResponseBody`（或 `@RestController`）+ `<mvc:annotation-driven>` + Jackson。
- 追问“为什么返回字符串不是跳页面”：因为 `@ResponseBody` 把返回值交给 `HttpMessageConverter` 写响应体，不经过 `ViewResolver`。

---

## 21. 参数绑定与路径传参（4 种核心 + 10 种全表）

**题型**：多选题“mvc 参数绑定与数据传递：4 种方式”；填空题“路径传参”

**4 种核心（考试口径）**

| 方式 | 典型 URL/请求 | 代码 |
|---|---|---|
| `@RequestParam` | `?name=x&age=18` | `query(@RequestParam String name, ...)` |
| `@PathVariable` | `/path/1/zhangsan` | `path(@PathVariable Integer id, ...)` |
| 实体自动绑定 | POST 表单，字段名 = 属性名 | `form(Student student)` |
| `@RequestBody` | POST JSON | `json(@RequestBody Student student)` |

**课件完整 10 种**：`@RequestParam`、`@PathVariable`、数组、List、实体绑定、`@RequestBody`、`@RequestHeader`、`@CookieValue`、原生 `HttpServletRequest/HttpSession`、`@RequestParam Map`。

**绑定总规则**：参数名 == 属性名 → 自动注入；String → Integer/Double/Date 自动转换；日期要 `@DateTimeFormat`。

**代码落点 1：`@RequestParam` 与 `@PathVariable`（路径传参）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/ParameterController.java`　**L51–L65**

```java
    @GetMapping("/query")
    public String query(@RequestParam String name,
                        @RequestParam(defaultValue = "18") Integer age,
                        @RequestParam(required = false) String major) {
        return "1) @RequestParam -> name=" + name + ", age=" + age + ", major=" + major;
    }

    /**
     * 2. @PathVariable —— 路径变量（REST 风格 URL）
     * {} 占位符名字必须和方法参数名一致
     */
    @GetMapping("/path/{id}/{name}")
    public String path(@PathVariable Integer id, @PathVariable String name) {
        return "2) @PathVariable -> id=" + id + ", name=" + name;
    }
```

**代码落点 2：实体绑定与 `@RequestBody`（JSON）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/ParameterController.java`　**L83–L100**

```java
    /**
     * 5. 实体自动绑定 —— 不写任何注解
     * POST 表单（application/x-www-form-urlencoded）字段名与属性同名 → setter 注入
     */
    @PostMapping("/form")
    public String form(Student student) {
        return "5) 实体绑定 -> " + student;
    }

    /**
     * 6. @RequestBody —— 请求体 JSON → 实体
     * 需要 Jackson 依赖（mvc:annotation-driven 自动注册 MappingJackson2HttpMessageConverter）
     * Content-Type 必须是 application/json
     */
    @PostMapping("/json")
    public String json(@RequestBody Student student) {
        return "6) @RequestBody -> " + student;
    }
```

**代码落点 3：原生 API 与 Map 接收**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/ParameterController.java`　**L116–L131**

```java
    @GetMapping("/servlet")
    public String servlet(HttpServletRequest request, HttpSession session) {
        String name = request.getParameter("name");
        session.setAttribute("lastUser", name);
        return "9) 原生 API -> name=" + name
                + ", session.lastUser=" + session.getAttribute("lastUser");
    }

    /**
     * 10. Map 接收 —— 一次性拿到所有请求参数（适合参数不确定的场景）
     * 注意：Map 前必须加 @RequestParam，否则会被当作 Model（数据模型）
     */
    @PostMapping("/map")
    public String map(@RequestParam Map<String, String> params) {
        return "10) Map 参数 -> " + params;
    }
```

**易错点**

- `@PathVariable` 的 `{}` 名字必须与方法参数名一致；不一致要 `@PathVariable("id")`。
- `@RequestParam` 默认必传，缺了报 400；可空要 `required = false` 或 `defaultValue`。
- `Map` 参数前**必须**加 `@RequestParam`，否则被当成 Model。
- `@RequestBody` 只适用于 `application/json`，表单用实体绑定。

---

## 22. 数据传递与 ModelAndView 前后缀

**题型**：填空题“modelandview：前后缀”

**定义**

- **ModelAndView**：`new ModelAndView("逻辑视图名")` + `addObject(key, value)`；返回值同时带“视图 + 数据”。
- **ViewResolver 前后缀**：`InternalResourceViewResolver` 的 `prefix` + 逻辑视图名 + `suffix` = 物理路径。
  - 例：`prefix=/WEB-INF/views/`、`suffix=.jsp`，视图名 `page/show` → `/WEB-INF/views/page/show.jsp`。
- **7 种携带数据**：`ModelAndView`、`Model`、`ModelMap`、`Map`、`@ModelAttribute`（方法级公共参数）、`HttpSession`、`RedirectAttributes`（`addAttribute` 拼 URL / `addFlashAttribute` 跨重定向）。
- **跳转 3 种**：返回逻辑视图名（转发，1 次请求）、`forward:/path`（转发）、`redirect:/path`（重定向，2 次请求，request 数据丢失）。

**代码落点 1：ModelAndView 与 Model**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/PageController.java`　**L56–L77**

```java
    @GetMapping("/modelAndView")
    public ModelAndView modelAndView() {
        ModelAndView mv = new ModelAndView("page/show");
        mv.addObject("message", "方式① ModelAndView");
        mv.addObject("name", "zhangsan");
        mv.addObject("age", 20);
        return mv;
    }

    /**
     * ② Model —— 方法参数方式（最常用），返回逻辑视图名
     * via/nm 可选参数：用于演示 forward/redirect 后 URL 参数的存活情况
     */
    @GetMapping("/model")
    public String model(Model model,
                        @RequestParam(required = false) String nm,
                        @RequestParam(required = false) String via) {
        model.addAttribute("message", "方式② Model（跳转来源: " + via + "）");
        model.addAttribute("name", nm);
        model.addAttribute("age", 22);
        return "page/show";
    }
```

**代码落点 2：Flash 属性跨重定向**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/PageController.java`　**L144–L151**

```java
    @GetMapping("/flash")
    public String flash(RedirectAttributes redirectAttributes) {
        redirectAttributes.addFlashAttribute("message", "方式⑦ Flash 属性：跨重定向存活");
        redirectAttributes.addFlashAttribute("student",
                new Student(1, "flashStu", 20, "CS", 95.0));
        redirectAttributes.addAttribute("nm", "urlParam");
        return "redirect:/annotation/page/show";
    }
```

**代码落点 3：前后缀配置**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/resources/springmvc/annotation/springmvc-servlet.xml`　**L95–L100**

```xml
    <!-- 视图解析器：@Controller 返回的逻辑视图名 → JSP 路径
         page/show → /WEB-INF/views/page/show.jsp（与 XML 方式配置原理相同） -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
```

**得分点**

- 填空：`InternalResourceViewResolver`，`prefix` + 视图名 + `suffix`；例子写 `page/show → /WEB-INF/views/page/show.jsp`。
- 重定向带数据：URL 参数（`addAttribute`）或 Flash 属性（`addFlashAttribute`，存 session，到达后取出即删）。

---

## 23. 拦截器：三个方法、工作顺序、与过滤器的区别

**题型**：选择题“拦截器：方法名称”；多选题“工作顺序，与过滤器的区别”

**定义**

- 实现 `HandlerInterceptor`（Spring 5 起三方法都有默认实现，按需覆盖）：
  1. `preHandle(request, response, handler)`：Handler 执行**前**；返回 `true` 放行，`false` 中断（后续拦截器与 Handler 都不执行）。
  2. `postHandle(request, response, handler, modelAndView)`：Handler 执行**后**、视图渲染**前**；可修改 `ModelAndView`。
  3. `afterCompletion(request, response, handler, ex)`：渲染**完成后**；无论是否异常都执行（类似 finally），适合清理/记日志。
- **多拦截器顺序（洋葱模型）**：`pre1 → pre2 → Handler → post2 → post1 → 渲染 → after2 → after1`。
- **注册**：`<mvc:interceptors>` + `<mvc:mapping path>` + `<mvc:exclude-mapping path>`；按声明顺序执行。
- **拦截器 vs 过滤器**：

| | 拦截器 | 过滤器 |
|---|---|---|
| 规范 | SpringMVC 机制 | Servlet 规范 |
| 位置 | `DispatcherServlet` **之后** | 最外层，`DispatcherServlet` **之前** |
| 能拿到 | Handler 信息、Spring Bean | 只有 `ServletRequest/Response` |
| 范围 | 只拦 Controller 请求 | 所有请求（含静态资源） |

**代码落点 1：三个方法的完整实现**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/interceptor/TimeInterceptor.java`　**L34–L64**

```java
public class TimeInterceptor implements HandlerInterceptor {

    private static final String START_TIME = "TimeInterceptor.startTime";

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response,
                             Object handler) {
        long start = System.currentTimeMillis();
        request.setAttribute(START_TIME, start);
        System.out.println("[TimeInterceptor] 1.preHandle  → Handler 执行前: "
                + request.getRequestURI());
        // 返回 false 的效果见 LoginInterceptor；这里返回 true 放行
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response,
                           Object handler, ModelAndView modelAndView) {
        System.out.println("[TimeInterceptor] 2.postHandle → Handler 后、渲染前，"
                + "逻辑视图名=" + (modelAndView != null ? modelAndView.getViewName() : "无(REST)"));
        // 此处可以修改/补充模型数据，页面渲染前最后一次机会
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response,
                                Object handler, Exception ex) {
        long cost = System.currentTimeMillis() - (Long) request.getAttribute(START_TIME);
        System.out.println("[TimeInterceptor] 3.afterCompletion → 渲染完成，本次请求耗时 "
                + cost + " ms" + (ex != null ? "，发生异常: " + ex.getMessage() : "，无异常"));
        // ex 非空时可记录日志；本方法无论如何都会执行（类似 finally）
    }
```

**代码落点 2：`preHandle` 返回 false 中断**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/interceptor/LoginInterceptor.java`　**L24–L42**

```java
public class LoginInterceptor extends HandlerInterceptorAdapter {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response,
                             Object handler) throws Exception {
        HttpSession session = request.getSession();
        Object loginUser = session.getAttribute("loginUser");

        if (loginUser != null) {
            System.out.println("[LoginInterceptor] 已登录(user=" + loginUser + ")，放行");
            return true;
        }

        System.out.println("[LoginInterceptor] 未登录，拦截请求: "
                + request.getRequestURI() + " → 重定向到登录演示页");
        // contextPath = 部署上下文（如 /spring_springmvc_mybatis）
        response.sendRedirect(request.getContextPath() + "/annotation/page/session");
        return false; // 中断：Handler 不会执行
    }
```

**代码落点 3：注册（mapping / exclude-mapping / 顺序）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/resources/springmvc/annotation/springmvc-servlet.xml`　**L63–L78**

```xml
    <mvc:interceptors>

        <!-- 拦截器①：耗时统计 —— 拦截 /page/** 下所有页面跳转（放行演示） -->
        <mvc:interceptor>
            <mvc:mapping path="/page/**"/>
            <bean class="com.springmvc.interceptor.TimeInterceptor"/>
        </mvc:interceptor>

        <!-- 拦截器②：登录检查 —— 只拦 /student/**，
             preHandle 返回 false 中断请求（未登录重定向到 /annotation/page/session） -->
        <mvc:interceptor>
            <mvc:mapping path="/student/**"/>
            <bean class="com.springmvc.interceptor.LoginInterceptor"/>
        </mvc:interceptor>

    </mvc:interceptors>
```

**代码落点 4：过滤器的对照写法（`CharacterEncodingFilter`）**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/webapp/WEB-INF/web.xml`　**L35–L54**

```xml
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/annotation/*</url-pattern>
    </filter-mapping>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/ssm/*</url-pattern>
    </filter-mapping>
```

**易错点**

- `postHandle` 在异常时**不执行**；`afterCompletion` 一定执行。
- `preHandle` 返回 `false` 后，已经执行过 `preHandle` 的拦截器的 `afterCompletion` **仍会**执行。
- 拦截器拿不到静态资源请求（取决于 mapping）；过滤器能。

---

## 24. 全局异常处理

**题型**：填空题“全局异常（异常类）”

**定义**

- `@ControllerAdvice`：全局增强，对所有 Controller 生效；**必须被组件扫描到**。
- `@ExceptionHandler(XxxException.class)`：按异常类型精确匹配；**越具体越优先**（`ArithmeticException` 先于 `Exception`）。
- 可以返回 `ModelAndView`（错误页）或 `@ResponseBody` 的 JSON；Controller 内也能写 `@ExceptionHandler`，但只对本类生效。
- 好处：业务代码只管抛，不用每个方法 `try-catch`；统一友好提示，不再 500 白页。

**代码落点 1：全局异常处理器**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/exception/GlobalExceptionHandler.java`　**L26–L63**

```java
@Controller
@ControllerAdvice
public class GlobalExceptionHandler {

    /** 算术异常演示：/extra/arith/10/0（见 AdvanceController 统一演示类） */
    @ExceptionHandler(ArithmeticException.class)
    public ModelAndView arithmeticException(ArithmeticException ex) {
        return errorPage("算术异常", ex);
    }

    /** 空指针异常演示：/extra/null */
    @ExceptionHandler(NullPointerException.class)
    public ModelAndView nullPointerException(NullPointerException ex) {
        return errorPage("空指针异常", ex);
    }

    /** 上传文件超限（见 multipartResolver.maxUploadSize=10MB）→ 友好提示而不是报错页 */
    @ExceptionHandler(MaxUploadSizeExceededException.class)
    public ModelAndView maxUploadException(MaxUploadSizeExceededException ex) {
        ModelAndView mv = new ModelAndView("error/error");
        mv.addObject("exClass", "上传文件过大");
        mv.addObject("exMessage", "单个文件不能超过 10MB（multipartResolver.maxUploadSize）");
        return mv;
    }

    /** 兜底：其余所有异常 */
    @ExceptionHandler(Exception.class)
    public ModelAndView allException(Exception ex) {
        return errorPage("其他异常", ex);
    }

    /** 统一的错误页视图 */
    private ModelAndView errorPage(String title, Exception ex) {
        ModelAndView mv = new ModelAndView("error/error");
        mv.addObject("exClass", title);
        mv.addObject("exMessage", ex.getMessage());
        return mv;
    }
```

**代码落点 2：被捕获的异常从哪来（除零 / 空指针）**

`课程/10/springmvc SpringMVC.html → 完整源码 → src/main/java/com/springmvc/controller/AdvanceController.java`　**L56–L66**

```java
    @GetMapping("/arith/{a}/{b}")
    public String arith(@PathVariable Integer a, @PathVariable Integer b) {
        return "二) " + a + " / " + b + " = " + (a / b);
    }

    /** 空指针异常 → 被 @ExceptionHandler(NullPointerException.class) 精确捕获 */
    @GetMapping("/null")
    public String nullPointer() {
        String s = null;
        return "二) " + s.length();
    }
```

**得分点**

- 两个注解：`@ControllerAdvice` + `@ExceptionHandler`。
- 异常类举例：`ArithmeticException`、`NullPointerException`、`MaxUploadSizeExceededException`、`Exception`（兜底）。
- 匹配规则：**具体优先**，兜底最后。

---

# 七、SSM 与调试

## 25. SSM 三层整合（父子容器 + 四件套）

**题型**：综合/简答；也是“调 bug”题的背景

**定义**

- 三层：表现层 Controller → 业务层 Service（`@Transactional`）→ 持久层 Mapper（接口 + XML）→ 数据库。
- **整合四件套**（父容器 `applicationContext.xml`）：
  1. `DataSource`（HikariCP 连接池）。
  2. `SqlSessionFactoryBean`（把 MyBatis 工厂交给 Spring；替代 `mybatis-config.xml`）。
  3. `MapperScannerConfigurer`（扫 Mapper 接口，生成 JDK 动态代理 Bean，无需实现类）。
  4. `DataSourceTransactionManager` + `<tx:annotation-driven/>`（支撑 `@Transactional`）。
- **父子容器**：
  - 父容器：`ContextLoaderListener` 加载 `applicationContext.xml`，管 Service/Mapper/事务/数据源，全局唯一。
  - 子容器：每个 `DispatcherServlet` 加载自己的 `spring-mvc.xml`，管 Controller/视图解析器/拦截器。
  - **可见性单向**：子能看到父（Controller 注入 Service）；父看不到子。
  - **两个坑**：父子都扫同一个包 → Service 两份，事务可能失效；Service 注入 Controller → 启动报 `NoSuchBeanDefinitionException`。

**代码落点 1：父容器四件套**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/resources/ssm/applicationContext.xml`　**L28–L65**

```xml
    <!-- 数据库连接参数（与 Spring/dao 模块共用同一份 db.properties） -->
    <context:property-placeholder location="classpath:common/db.properties"/>

    <!-- Service 层扫描：Controller 留给子容器（ssm/spring-mvc.xml）扫 -->
    <context:component-scan base-package="com.ssm.service"/>

    <!-- ① 连接池 -->
    <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="maximumPoolSize" value="10"/>
        <property name="minimumIdle" value="5"/>
    </bean>

    <!-- ② MyBatis 核心工厂：不再手写 SqlSessionFactoryBuilder.build()，
            Spring 启动时自动构建；mapperLocations 指向本模块的 SQL 文件 -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="mapperLocations" value="classpath:ssm/mapper/*.xml"/>
        <property name="typeAliasesPackage" value="com.ssm.entity"/>
    </bean>

    <!-- ③ Mapper 扫描：com.ssm.mapper 下每个接口 → 一个代理 Bean（无需实现类） -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.ssm.mapper"/>
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
    </bean>

    <!-- ④ 事务：Spring 事务管理器接管 MyBatis（本质是接管 SqlSession 的提交/回滚） -->
    <bean id="transactionManager"
          class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- 开启 @Transactional 注解事务（对比 Spring/dao 模块的 XML 式 tx:advice） -->
    <tx:annotation-driven transaction-manager="transactionManager"/>
```

**代码落点 2：子容器只扫 Controller + 视图解析器**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/resources/ssm/spring-mvc.xml`　**L28–L35**

```xml
    <mvc:annotation-driven/>

    <context:component-scan base-package="com.ssm.controller"/>

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
```

**代码落点 3：父容器由监听器启动**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/webapp/WEB-INF/web.xml`　**L19–L25**

```xml
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:ssm/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
```

**代码落点 4：持久层 namespace = 接口全限定名（铁律）**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/resources/ssm/mapper/StudentMapper.xml`　**L15–L41**

```xml
<mapper namespace="com.ssm.mapper.StudentMapper">

    <!-- 驼峰映射：数据库下划线列 ↔ 实体驼峰属性 -->
    <resultMap id="StudentMap" type="com.ssm.entity.Student">
        <id     property="id"    column="id"/>
        <result property="name"  column="name"/>
        <result property="age"   column="age"/>
        <result property="email" column="email"/>
        <result property="major" column="major"/>
        <result property="score" column="score"/>
    </resultMap>

    <select id="selectAll" resultMap="StudentMap">
        SELECT id, name, age, email, major, score FROM student ORDER BY id
    </select>

    <select id="selectById" parameterType="int" resultMap="StudentMap">
        SELECT id, name, age, email, major, score FROM student WHERE id = #{id}
    </select>

    <!-- useGeneratedKeys：自增主键回填到实体的 id 属性（keyProperty） -->
    <insert id="insert" parameterType="com.ssm.entity.Student"
            useGeneratedKeys="true" keyProperty="id">
        INSERT INTO student(name, age, email, major, score)
        VALUES(#{name}, #{age}, #{email}, #{major}, #{score})
    </insert>

```

**代码落点 5：Controller 构造器注入 Service（子取父）**

`课程/11/ssm SSM三层整合.html → 完整源码 → src/main/java/com/ssm/controller/StudentController.java`　**L26–L35**

```java
@Controller
@RequestMapping("/student")
public class StudentController {

    private final StudentService studentService;

    @Autowired
    public StudentController(StudentService studentService) {
        this.studentService = studentService;
    }
```

**得分点**

- 背“四件套 + 父子容器 + 单向可见”。
- 事务生效链：`@Transactional` → 事务代理 → `DataSourceTransactionManager` → 同一个 `Connection` 绑到 ThreadLocal。
- XML 的 `namespace` 必须等于接口全限定名，`id` 必须等于方法名，否则 `Invalid bound statement (not found)`。

---

## 26. 简答“调 bug”：方法 + 高频错误对照

**题型**：简答题“调 bug”

**答题框架（4 步，老师要的是过程不是背答案）**

1. **看现象/日志**：先定位第一处异常（`Caused by`），不要从最后一屏开始猜。
2. **缩范围**：二分注释/最小复现；确认是配置、映射、参数还是事务问题。
3. **验证假设**：改一个变量、跑一次；用日志（`Preparing/Parameters`）证明 SQL 是否发出、参数是什么。
4. **回归**：修复后重跑同类用例，确认没有把别的功能带崩。

**高频 bug 对照表（都来自课件“常见坑”）**

| 现象 | 根因 | 修复 | 课程证据 |
|---|---|---|---|
| `Invalid bound statement (not found)` | XML `namespace` ≠ 接口全限定名，或 `id` ≠ 方法名；Mapper 没注册 | 对齐 namespace/id；`<mapper resource>` 或 `<package>` 注册 | 第 25 节 L15；第 9 节 `<mappers>` |
| 查询结果字段全是 `null` | 列名与属性名不一致，没开驼峰/没起别名 | `mapUnderscoreToCamelCase=true` 或 SQL 别名或 `resultMap` | 第 11 节 |
| 参数绑定报错/取不到 | 多参数没 `@Param`；`${}` 没加引号；`@RequestParam` 必传缺参 | 加 `@Param`、改 `#{}`、`required=false` | 第 10、21 节 |
| 事务不回滚 | 异常被 catch；受检异常；同类自调用；父子容器重复扫描 | 继续抛/`rollbackFor`/走代理/只扫 controller | 第 7、25 节 |
| 拦截器不生效 | 没注册；mapping 写错；类没被扫描 | `<mvc:interceptors>` + 正确 path | 第 23 节 |
| 全局异常不生效 | `@ControllerAdvice` 类没被组件扫描 | 加 `<context:component-scan>` | 第 24 节；`springmvc-servlet.xml` L44 |
| 返回 JSON 500/乱码 | 缺 Jackson；没 `@ResponseBody`；转换器 ISO-8859-1 | 加依赖/注解/UTF-8 转换器 | 第 20 节 |
| 逻辑删除“删了还能查到” | 只加字段没加 `@TableLogic`；自定义 SQL 没过 MP | 加注解；自定义 SQL 手动过滤 | 第 16 节 |
| 乐观锁更新 0 行 | 没带旧 `version`；没注册插件 | 先查后改；注册 `OptimisticLockerInnerInterceptor` | 第 17 节 |
| 二级缓存不命中 | 没 `<cache/>`；实体没序列化；没 `close/commit` | 四个前提逐条查 | 第 14 节 |

**得分点**

- 简答不要只写“加日志”。按“**现象 → 定位 → 假设 → 验证 → 回归**”写，并给一个具体例子（如 `Invalid bound statement` 查 namespace）。
- 能说出“用日志看 `Preparing/Parameters` 判断 SQL 是否发出”，比空谈“调试”高分。

---

## 附：考前 10 分钟只看这些

| 主题 | 一句话 |
|---|---|
| IoC/DI | IoC 是目标（控制权给容器），DI 是手段（注入依赖） |
| 自动装配 3 种 | `byName` / `byType` / `constructor` |
| Bean 生命周期 | 构造 → setter 注入 → 初始化（`@PostConstruct`→`afterPropertiesSet`→`init-method`）→ 使用 → 销毁 |
| AOP 五通知 | Before / AfterReturning / AfterThrowing / After / Around |
| 事务 | 类上默认、方法上覆盖；默认回滚 `RuntimeException/Error`；受检异常 `rollbackFor` |
| `#{}` vs `${}` | 预编译防注入 vs 字符串拼接有注入风险 |
| resultType vs resultMap | 自动映射（列名要对）vs 手动映射（任意列/关联）；互斥 |
| 动态 SQL | `if/where/set/choose/foreach/trim/sql+include` |
| 多对一 / 一对多 | `association javaType/@One` vs `collection ofType/@Many` |
| 缓存 | 一级绑 SqlSession；二级绑 Mapper namespace；二级要 `close/commit` 才提交 |
| MP 注解 | `@TableName/@TableId/@TableField/@TableLogic/@Version` |
| 逻辑删除 | 删改写 UPDATE，查自动加 `deleted=0` |
| 乐观锁 | `@Version` + `WHERE version=旧值`；悲观锁 `FOR UPDATE` |
| MVC 四核心 | `DispatcherServlet → HandlerMapping → HandlerAdapter → ViewResolver` |
| JSON | `@ResponseBody`/`@RestController` + `annotation-driven` + Jackson |
| 路径传参 | `@PathVariable`，`{}` 名 = 参数名 |
| ModelAndView | `prefix + 视图名 + suffix` |
| 拦截器 | `preHandle/postHandle/afterCompletion`；pre 正序、post/after 逆序 |
| 全局异常 | `@ControllerAdvice` + `@ExceptionHandler`，具体优先 |
| SSM | 四件套 + 父子容器单向可见 |
