# springboot

## 1springboot基础特性

### 1、配置bean

如果你希望将springboot将类作为bean

根据需要可以利用@ComponentScan自动的检测并创建类的实例，该注解与@Autowired和@Value一起使用以获取依赖项或注入属性；或者可以使用注入@Bean，这种方法可以对正在创建的bean的构造过程获取更多的控制

### 2、属性外置

场景：为不同环境配置运行环境。

springboot默认加载application.properties的文件，并使用环境变量和 java System属性，springboot加载资源顺序：

1. 命令行参数
2. 应用程序包之外的application.properties文件
3. 应用程序包之中的application.properties文件

1.使用application.properties中的参数

使用@value("参数名":默认值)

2.使用外部的application.properties文件进行覆盖

首先编译代码并使用命令java-jar recipe_2_2--1.0.0.jar启动应用程序，它将再次运行并加载前面提供的、打包在应用程序内的application.properties。现在，在便以文件位置相同的目录下在添加一个application.properties文件，并将不同属性的值放入其中，再次启动时，它将使用此application.properties文件的属性值

3、使用配置文件覆盖属性

springboot可以使用激活的配置（active profile）加载额外的配置文件，这些配置文件可以完全替换或者部分覆盖常规的配置.在src/main/resources目录中添加一个application-add.properties文件，现在编译代码（生成jar文件）并在命令行通过命令java -jar recipe_2_2-1.0.0.jar--spring.profiles.active=add启动应用程序；应用程序将启动并加载application.properties和application-add.properties中的属性来配置应用程序但application-add.properties优先级高于application.properties

4.使用命令行覆盖属性

使用java -jar recipe_2_2-1.0.0.jar --参数名=参数，命令行中的参数会覆盖所有其他配置

5、从不同的配置文件中加载属性

可以在@springbootApplication注解的类上使用@PropertySource注解来加载指定的附加文件

如：@PropertySource("classpath:you-external.properties")

### 3.测试

1.为springboot部分应用程序编写测试程序

解决方案：

springboot拓展了springTest框架的功能范围，它新增的特性支持对bean进行模拟和监视，并为Web测试提供了自动配置功能，同事，它也引入简单的方法来测试应用程序的片段，只需要启动待测试的程序片段（例如:通过使用WebMvcTest或者@JdbcTest）即能完成测试。

1. 编写测试单元

   使用@test注解进行编写

2. 在单元测试中模拟依赖项

   类有时需要依赖于其他内容，但你希望仅针对一个组件进行测试，springboot会自动引入Mockito框架，该框架对于模拟类并记录其行为非常方便。

3. 使用springboot进行集成测试

   springboot提供了几个注解来帮助测试

   springbootTest：该注解将使测试成为springboot驱动的一个测试、这意味着测试上下文框架将搜索用@SpringbootApplication注解的类（如果没有传递特定的配置），并将实际上使用该类启动应用程序

   ```java
   @RunWith(SpringRunner.class)
   @SpringBootTest(classes=启动类.class)
   public class CalculatorApplicationTests{
       @Autowired
       private Calculator calculator
           
       @Rule
      public OutputCapture capture = new OutputCapture();
           
       @Test(expected = IllegalArgumentException.class)
       public void doingDivisionShouldFail(){
           calculator.calculate(12,13,"/");
           capture.expect(Matchers.containsString("12 * 13 =156"));
       }
   }
   ```

   在进行计算时，输出将打印到控制台，使用JUnit规则中的OutputCapture规则,@Rulle注解将配置指定的JUnit规则，在本例中是OutputCapture规则，它已经集成在spingboot中。该规则截取System.out和System.err输出流，以便在这两个流上生成输出中写入断言。

4. 使用springboot和迷你进行集成测试

   springboot使得在应用程序上下文中用模拟来替换bean变得很容易，为此，springboot引入了@MockBean注解（模拟实例替换普通的bean，如果找不到该名称的bean，模拟bean将注册为该bean的新实例）



















































