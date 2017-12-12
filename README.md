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

