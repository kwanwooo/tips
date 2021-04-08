# JUnit 是什么？

1. JUnit 是一个Java语言的单元测试框架。它由Kent Beck和Erich Gamma建立，逐渐成为源于Kent Beck的sUnit的xUnit家族中最为成功的一个。

2. JUnit 测试是程序员测试，即所谓的白盒测试，它需要程序员知道被测试的代码如何完成功能，以及完成什么样的功能。

3. JUnit是一套框架，继承TestCase类，就可以用Junit进行自动测试。

4. 断言机制：将程序预期的结果与程序运行的最终结果进行比对，确保对结果的可预知性。

5. hamcrest-core设置匹配集规则的框架，可用来增强junit的功能。

6. JUnit3：必须继承junit.framework.TestCase这个类，在方法前面必须加上test最为前缀。

7. JUnit4：只要加上@Test注解即可，不需要继承任何类，命名没有限制。JDK 5及以上可以使用。

8. JUnit5：JDK 8及以上可以使用。

# JUnit 能做什么？

1. 通常我们写完代码想要测试一段代码的正确性，那么必须创建一个 main() 方法，然后编写测试代码。测试的代码越多，main() 方法越多，或者将其全部写在一个 main() 方法里面。这也会大大的增加测试的复杂度，降低程序员的测试积极性。
2. JUnit 能很好的解决这个问题，简化单元测试，写一点测一点，在编写以后的代码中如果发现问题可以较快的追踪到问题的原因，减小回归错误的纠错难度。

# JUnit 的用法

1. 测试方法上必须使用@Test进行修饰
2. 测试方法必须使用public void 进行修饰，不能带任何的参数
3. 新建一个源代码目录来存放我们的测试代码
4. 测试类的包应该和被测试类保持一致
5. 测试单元中的每个方法必须可以独立测试，测试方法间不能有任何的依赖
6. 测试类使用Test作为类名后缀（不是必须）
7. 测试方法用test作为方法的前缀（不是必须）

# spring下使用JUnit，需要读取spring的配置文件

1. @RunWith(SpringJUnit4ClassRunner.class)//表示继承了SpringJunit4ClassRunner类
2. @ContextConfiguration("classpath:applictionContext.xml")//告诉junit spring配置文件

# JUnit 4 特点

1. 使用JUnit4.x版本进行单元测试时，不用测试类继承TestCase父类，因为，JUnit4.x全面引入了Annotation来执行我们编写的测试。
2. JUnit4.x版本，引用了注解的方式，进行单元测试；
3. JUnit4.x版本我们常用的注解：
    - @Before 注解：与junit3.x中的setUp()方法功能一样，在每个测试方法之前执行。
    - @After 注解：与junit3.x中的tearDown()方法功能一样，在每个测试方法之后执行。
    - @BeforeClass 注解：在所有方法执行之前执行。方法是静态的，只运行一次，所以比较适合加载配置文件。
    - @AfterClass 注解：在所有方法执行之后执行。方法是静态的，只运行一次，比较适合资源的回收，比如关闭数据库连接。
    - @Test(timeout = xxx) 注解：设置当前测试方法在一定时间内运行完，否则返回错误；
    - @Test(expected = Exception.class) 注解：设置被测试的方法是否有异常抛出。抛出异常类型为：Exception.class；
    - @Ignore 注解：注释掉一个测试方法或一个类，被注释的方法或类，不会被执行。
4. JUnit5.x版本我们常用的注解：略

# 测试失败

1. Failure一般由单元测试使用的断言方法判断失败所引起的，这表示 测试点发现了问题，就是说程序输出的结果和我们预期的不一样
2. error是由代码异常引起的，他可以产生于测试代码本身的错误，也可以是被测试代码中的一个隐藏的bug
3. 测试用例不是用来证明你是对的，而是用来证明你没有错

# 测试套件 测试套件就是组织测试类一起运行的

1. 写一个作为测试套件的入口类，这个类里不包含其他的方法
2. 更改测试运行器Suite.class.
    - ```@RunWith(Suite.class)```
3. *JUnit 4* 将要测试的类作为数组传入到Suite.SuiteClasses({}) 
    - ```@Suite.SuiteClasses({Task1Test.class, Task2Test.class, Task3Test.class})```
4. *JUnit 5* @SelectPackages和@SelectClasses
    - ```@SelectPackages("com.demo")```

# 参数化测试

1. 更改默认的测试运行器为RunWith(Parameterized.class)
2. 声明变量存放预期值和结果值
3. 声明一个返回值为Collection的公共静态方法，并使用@Parameters进行修饰
4. 为测试类声明一个带有参数的公共构造函数，并在其中为之声明变量赋值（预期值、输入参数值等）

# JUnit 4 和 JUnit 5 对比

特征|JUnit 4|JUnit 5
---|:--:|:---:
声明一种测试方法|@Test|@Test
在当前类中的所有测试方法之前执行|@BeforeClass|@BeforeAll
在当前类中的所有测试方法之后执行|@AfterClass|@AfterAll
在每个测试方法之前执行|@Before|@BeforeEach
每种测试方法后执行|@After|@AfterEach
禁用测试方法/类|@Ignore|@Disabled
测试工厂进行动态测试|NA|@TestFactory
嵌套测试|NA|@Nested
标记和过滤|@Category|@Tag
注册自定义扩展|NA|@ExtendWith
