# quartz集群配置记录
 配置文件 quatrz.properties
 
 ```

#============================================================================
# Configure JobStore
# Using Spring datasource in quartzJobsConfig.xml
# Spring uses LocalDataSourceJobStore extension of JobStoreCMT
#============================================================================
org.quartz.jobStore.useProperties=true
org.quartz.jobStore.tablePrefix = QRTZ_
org.quartz.jobStore.isClustered = true
org.quartz.jobStore.clusterCheckinInterval = 15000
org.quartz.jobStore.misfireThreshold = 60000
org.quartz.jobStore.txIsolationLevelReadCommitted = true

# Change this to match your DB vendor
org.quartz.jobStore.class = org.quartz.impl.jdbcjobstore.JobStoreTX
org.quartz.jobStore.driverDelegateClass = org.quartz.impl.jdbcjobstore.StdJDBCDelegate


#============================================================================
# Configure Main Scheduler Properties
# Needed to manage cluster instances
#============================================================================
org.quartz.scheduler.instanceId=AUTO
org.quartz.scheduler.instanceName=MY_CLUSTERED_JOB_SCHEDULER
org.quartz.scheduler.rmi.export = false
org.quartz.scheduler.rmi.proxy = false


#============================================================================
# Configure ThreadPool
#============================================================================
org.quartz.threadPool.class = org.quartz.simpl.SimpleThreadPool
org.quartz.threadPool.threadCount = 10
org.quartz.threadPool.threadPriority = 5
org.quartz.threadPool.threadsInheritContextClassLoaderOfInitializingThread = true

 ```

 ##QuartzConfiguration.java

 ```

@Configuration
public class QuartzConfiguration {

    @Value("${mt.quartz.repeatInterval}")
    private int repeatInterval;

    @Autowired
    private DataSource dataSource;


    @Bean
    public JobDetailFactoryBean tradeRollBackjobDetailFactoryBean() {
        JobDetailFactoryBean factory = new JobDetailFactoryBean();
        factory.setJobClass(TradeTimeOutCheck.class);
        factory.setGroup("tradeRollBack");
        factory.setName("tradeRollBack");
        factory.setDurability(true); // 表示任务完成之后是否还保留在数据库
        return factory;
    }

    @Bean
    public SimpleTriggerFactoryBean tradeRollBackTriggerFactoryBean() {
        SimpleTriggerFactoryBean stFactory = new SimpleTriggerFactoryBean();
        stFactory.setJobDetail(tradeRollBackjobDetailFactoryBean().getObject());
        stFactory.setName("rollBackTrigger");
        stFactory.setGroup("tradeRollBack");
        stFactory.setStartDelay(3000);
        stFactory.setRepeatInterval(repeatInterval);
        return stFactory;
    }

    @Bean
    public JobDetailFactoryBean hotTeamJobDetailFactoryBean() {
        JobDetailFactoryBean factory = new JobDetailFactoryBean();
        factory.setJobClass(HotTeamJob.class);
        factory.setGroup("hot");
        factory.setName("hotTeam");
        factory.setDurability(true);
        return factory;
    }

    @Bean
    public CronTriggerFactoryBean hotTeamFactoryBean() {
        CronTriggerFactoryBean stFactory = new CronTriggerFactoryBean();
        stFactory.setJobDetail(hotTeamJobDetailFactoryBean().getObject());
        stFactory.setStartDelay(3000);
        stFactory.setName("hotTeam");
        stFactory.setGroup("hot");
        stFactory.setCronExpression("0 0 3 * * ?");
        return stFactory;
    }

    @Bean
    public ThreadPoolTaskExecutor getTaskExecutor(){
        ThreadPoolTaskExecutor taskExecutor = new ThreadPoolTaskExecutor();
        taskExecutor.setCorePoolSize(5);
        taskExecutor.setMaxPoolSize(10);
        taskExecutor.setQueueCapacity(25);
        return taskExecutor;
    }

    @Bean
    public SchedulerFactoryBean schedulerFactoryBean() {
        SchedulerFactoryBean scheduler = new SchedulerFactoryBean();
        scheduler.setConfigLocation(new ClassPathResource("quatrz.properties"));//配置文件的路径
        scheduler.setTaskExecutor(getTaskExecutor()); //线程池的配置
        scheduler.setDataSource(dataSource);
        scheduler.setOverwriteExistingJobs(true); //每次启动更新job
        scheduler.setAutoStartup(true);
        scheduler.setTriggers(tradeRollBackTriggerFactoryBean().getObject(), 
                hotTeamFactoryBean().getObject(),
             );
        return scheduler;
    }
}

 ```


 参考：[Quartz应用与集群原理分析](http://tech.meituan.com/mt-crm-quartz.html)