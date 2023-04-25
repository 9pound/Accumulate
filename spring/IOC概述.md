# IOC容器



IOC 容器的本质？



BeanFactory



XmlWebApplicationContext

ClassPathApplicationContext







## BeanFactory

也叫IOC容器，是spring框架的基础设施面向Spring本身,它用来创建并管理各种类的对象（Bean）

**实现**

XmlBeanDefinitionReader

DefaultListableBeanFactory

## ApplicationContext

也被称为“应用上下文”或者是“Spring容器”、面向Spring框架的开发者，

**ApplicationContext初始化与BeanFactory初始化得区别？**

- BeanFactory在初始化容器时，并未实例化Bean，直到第一次访问某个Bean时才实例化目标Bean
- ApplicationContext则在初始化应用上下文时就实例化所有单实例Bean

**实现**

ClassPathXmlApplicationContext

FileSystemXmlApplicationContext

AnnotationConfigApplicationContext

## WebApplicationContext

扩展了ApplicationContext，是专门为Web应用准备的，它可以从相对于Web根目录的路径中装载配置文件。例如：可以从它当中获取ServletContext对象

**启动器**

前提：WebApplicationContext必须在有Web容器的情况下才能完成启动工作、有两类

- ContextLoadServlet
- ContextLoadListener
