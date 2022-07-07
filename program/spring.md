### spring

 ##### BeanFactory

Spring的底层bean容器，每个bean拥有唯一的字符串标识



##### ApplicationContext 对 BeanFactory做了哪些增强

>1.支持国际化
>
>2.根据路径（包含classpath）获取资源的能力
>
>3.获取环境变量
>
>4.spring事件的发布订阅 



##### Spring Bean 生命周期

周期及相关注解：

>实例化
>
>依赖注入 @Autowired @Resourse @ConfigurationProperties
>
>初始化 @PostConstruct
>
>销毁 @PreDestroy

Bean的后处理器

```java
public interface BeanPostProcessor {
	default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

	default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
		return bean;
	}

}
public interface InstantiationAwareBeanPostProcessor extends BeanPostProcessor {
    Object postProcessBeforeInstantiation(Class<?> var1, String var2) throws BeansException;

    boolean postProcessAfterInstantiation(Object var1, String var2) throws BeansException;

    PropertyValues postProcessPropertyValues(PropertyValues var1, PropertyDescriptor[] var2, Object var3, String var4) throws BeansException;
}
public interface DestructionAwareBeanPostProcessor extends BeanPostProcessor {
    void postProcessBeforeDestruction(Object var1, String var2) throws BeansException;

    boolean requiresDestruction(Object var1);
}
```



##### 各处理器操作对应数据

AutowiredAnnotationBeanPostProcessor——@Autowired && @Value

CommonAnnotationBeanPostProcessor——@Resource && @PostConstruct && @PreDestory

ConfigurationPropertiesBindingPostProcessor—— @ConfigurationProperties

ConfigurationClassPostProcessor——@ConponentScan && @Bean && @Import && @ImportResource



##### AutowiredAnnotationBeanPostProcessor 做了些什么

>1.首先拿到哪些方法或变量加了@Autowired注解
>
>2.
>
>



##### 依赖的来源

自建的bean，容器自动创建的bean（比如Envorinment）,内键的依赖|非bean对象（比如自动注入BeanFactory，不是main方法中的BeanFactory，新新建的BeanFactory）



##### 配置元信息

Bean定义配置、IOC容器配置、外部属性配置（@Value）



##### BeanFactory 和FactoryBean的区别



##### IOC 容器启动做了啥

ioc配置源信息读取和解析，ioc生命周期管理，事件发布，国际化



##### BeanDefinition

>bean类的全限定名字
>
>bean的配置元信息，作用域、自动绑定模式、生命周期回调
>
>其他bean的引用，合作者（Collaborators） 依赖（Dependency)
>
>配置设置，bean的属性（properties）





