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
