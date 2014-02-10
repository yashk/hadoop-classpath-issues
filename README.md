Hadoop Classpath issues - starting with some links collected while solving hadoop classpath issues.

1. http://www.kiji.org/2013/10/08/fixing-classpath-ordering-issues-in-hadoop/
2. http://blog.cloudera.com/blog/2011/01/how-to-include-third-party-libraries-in-your-map-reduce-job/
3. https://issues.apache.org/jira/browse/MAPREDUCE-1938
4. https://issues.cloudera.org/browse/DISTRO-468


Resolution
modify following hadoop config files


1. hadoop-env.sh

``` bash
# for client side classpath
export HADOOP_USER_CLASSPATH_FIRST=true 

# include all libs which should take precedence over hadoop platform libs.
export HADOOP_CLASSPATH=$(find ../lib/user.preced.lib/ -name *.jar | tr "\n" ":")
```

2. mapred-site.xml - add following properties at the End of file

``` xml
<!-- for client side jvm-->
<property>
<name>mapreduce.job.user.classpath.first</name>
<value>true</value>
</property>

<!-- for task tracker jvm-->
<property>
<name>mapreduce.task.classpath.user.precedence</name>
<value>true</value>
</property>
</code>
```
