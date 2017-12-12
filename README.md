# JavaSkillLearning
## BoneCP连接池学习
1.在spring-bean配置文件中配置
 <bean id="sessionFactory" class="org.springframework.orm.hibernate.LocalSessionFactoryBean" autowire="autodetect">
	<property name="hibernateProperties">
		<props>
			<prop key="hibernate.connection.provider_class">com.jolbox.bonecp.provider.BoneCPConnectionProvider</prop>
			<prop key="hibernate.connection.driver_class">com.mysql.jdbc.Driver</prop>
			<prop key="hibernate.connection.url">jdbc:mysql://127.0.0.1/yourdb</prop>
			<prop key="hibernate.connection.username">root</prop>
			<prop key="hibernate.connection.password">abcdefgh</prop>
			<prop key="bonecp.idleMaxAge">240</prop>
			<prop key="bonecp.idleConnectionTestPeriod">60</prop>
			<prop key="bonecp.partitionCount">3</prop>
			<prop key="bonecp.acquireIncrement">10</prop>
			<prop key="bonecp.maxConnectionsPerPartition">60</prop>
 			<prop key="bonecp.minConnectionsPerPartition">20</prop>
 			<prop key="bonecp.statementsCacheSize">50</prop>
 			<prop key="bonecp.releaseHelperThreads">3</prop>
		</props>
	</property>
</bean>

2.导入bonecp的包，可在官方下载

## 在jsp中设置路径
1.绝对路径：/项目名/类名

2.相对路径

3.添加语句

<%@ taglib uri="http://java.sun.com/jsp/jstl/core " prefix="c"%>

<c:set var="ctx" value="${pageContext.request.contextPath}" />

使用${ctx}/文件夹/文件
 
## Hibernate不允许int和float性的数据为空
 
## hibernate中的注解设置方式
集装映射方式：
使用注解映射主键关联的一对一：数据库表中正常，类中各自包含对方对象

在 User 一端的 getPerson()上配置。
@OneToOne(cascade=CascadeType.ALL) ：指定一对一关联关系，并设置级联属性。
@PrimaryKeyJoinColumn(name="ID") ：指定 PERSON 表主键列名。

在 Person 一端的 getId()上配置主键生成策略为 foreign。
@GeneratedValue(generator="foreign")    
@GenericGenerator(name="foreign",
       strategy="foreign",     
       parameters={@Parameter(
       name="property",value="user")})
在 Person 一端的 getUser()上配置一对一关联关系。
@OneToOne(mappedBy="person")

使用注解映射唯一外键关联的一对一：user表中设置personid，各类中包含对方对象
在User一端的person属性上配置。
@OneToOne(cascade=CascadeType.ALL)
@JoinColumn(name="PERSONID")：指明USER表中的外键列名。
在Person一端的user属性上配置。
@OneToOne(mappedBy="person")


使用注解映射组合关系
@Embedded
@AttributeOverrides(value={
    @AttributeOverride(
        name = "province", 
        column = @Column(name="WORKPROVINCE")),
    @AttributeOverride(
        name = "city",
        column = @Column(name="WORKCITY")),
    ......
})


使用注解映射一对多关联（双向：数据库中多方含外键字段，类中多方含对方对象，一方含对方集）

在 many 方 Order类 的 getUser() 方法上配置。
@ManyToOne
@JoinColumn(name="USERID")
public User getUser() {
    return user;
}

如果使用Set集合，在 one 方 User类 的 getOrderSet() 方法上配置。
@OneToMany(mappedBy="user", targetEntity=Order.class, 
        cascade=CascadeType.ALL)
public Set getOrderSet() {
    return orderSet;
}
如果使用List集合，在one方User类的getOrderList()上
{注：@OrderColumn(name=“ORDERINDEX”)：指定ORDER表中记录顺序的列名}

@OneToMany(mappedBy="user", targetEntity=Order.class, 
        cascade=CascadeType.ALL)
@OrderColumn(name="ORDERINDEX") 
public Set getOrderList() {
    return orderList;
}

如果使用Map集合，在one方User类的getOrderMap()上
注：@MapKey(name=“ORDERKEY” )：指定ORDER表中记录Map中key值的列名
@OneToMany(mappedBy="user", targetEntity=Order.class, 
        cascade=CascadeType.ALL)
@MapKey(name="orderKey")
public Set getOrderMap() {
    return orderMap;
}
若为单向一对多将mappedBy属性删掉 添加对方外键属性
例：@OneToMany(targetEntity=Cake.class, 
    cascade=CascadeType.ALL)
    @JoinColumn(name="sizeid") 
若为多对一单向则不变


使用注解映射多对多关系（设置第三张表，上方含对方集）
在 Student 类的 courseSet 属性上配置。
@ManyToMany
@JoinTable(name="STUDENTCOURSE", 
    joinColumns=@JoinColumn(name="STUDENTID"),
    inverseJoinColumns=@JoinColumn(name="COURSEID"))
在 Course 类的 studentSet 属性上配置。
@ManyToMany(mappedBy="course")
