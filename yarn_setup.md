1. Setting up yarn

`vim yarn-site.xml`
```xml
<?xml version="1.0"?>
<configuration>
	<property>
		<name>yarn.resourcemanager.scheduler.class</name>
		<value>org.apache.hadoop.yarn.server.resourcemanager.scheduler.capacity.CapacityScheduler</value> 
	</property>
	<property>
		<name>yarn.scheduler.capacity.root.queues</name>
		<value>prod,dev</value>
	</property>
	<property>
		<name>yarn.scheduler.capacity.prod.capacity</name>
		<value>0.5</value>
	</property>
	<property>
		<name>yarn.scheduler.capacity.dev.capacity</name> 
		<value>0.5</value>
	</property>
	<property>
		<name>yarn.scheduler.capacity.dev.maximum-capacity</name>
		<value>0.5</value>
	</property>
	<property>
		<name>yarn.scheduler.capacity.prod.maximum-capacity</name>
		<value>0.7</value>
	</property>
		
</configuration>
```
- write the instructions for the capacity scheduler
`vim capacity-scheduler.xml`

