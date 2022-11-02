# Cassandra Monitoring



                                                                                              
## Prerequisites

- Download and install the latest version of the [Site24x7 Linux agent] (https://www.site24x7.com/app/client#/admin/inventory/add-monitor) in the server where you plan to run the plugin. 

- Install jmxquery module for python
```
  pip install jmxquery
```
- Setting the jmx port for cassandra
	- Open the cassandra-env.sh file from the location "/etc/cassandra"
	- Add the following line to the cassandra-env.sh file
	
		```JVM_OPTS="$JVM_OPTS -Dcom.sun.management.jmxremote.authenticate=true"
		   JVM_OPTS="$JVM_OPTS -Dcassandra.jmx.remote.login.config=CassandraLogin"'
		   JVM_OPTS="$JVM_OPTS -Djava.security.auth.login.config=$CASSANDRA_HOME/conf/cassandra-jaas.config"
		   JVM_OPTS="$JVM_OPTS -Dcassandra.jmx.authorizer=org.apache.cassandra.auth.jmx.AuthorizationProxy"
		```
	- And comment out the following lines in the cassandra-env.sh file:
	
		```
		JVM_OPTS="$JVM_OPTS -Dcom.sun.management.jmxremote.password.file=/etc/cassandra/jmxremote.password"
		JVM_OPTS="$JVM_OPTS -Dcom.sun.management.jmxremote.access.file=/etc/cassandra/jmxremote.access"
		```
	- Change authentication in the cassandra.yaml file to PasswordAuthenticator
	
		```
		authenticator: PasswordAuthenticator
	
		```
   	- Change authorization in the cassandra.yaml file to CassandraAuthorizer

		```
		authorizer: CassandraAuthorizer
		
		```
	- Finally restart the cassandra
  
---



### Plugin Installation  

- Create a directory named "cassandra_monitoring" under the Site24x7 Linux Agent plugin directory: 

		Linux             ->   /opt/site24x7/monagent/plugins/cassandra_monitoring
      
- Download all the files in the "cassandra_monitoring" folder and place it under the "cassandra_monitoring" directory.
-
		```
		wget https://raw.githubusercontent.com/site24x7/plugins/master/cassandra_monitoring/cassandramonitoring.py
		wget https://raw.githubusercontent.com/site24x7/plugins/master/cassandra_monitoring/cassandra_monitoring.cfg
		```
- Execute the following command in your server to install jmxquery: 

		```
		pip install jmxquery
		```
- Execute the below command with appropriate arguments to check for the valid json output:

	```
	 python3 cassandra_monitoring.py --hostname localhost --port 7199 --logs_enabled False
	 ```



---

### Configurations

- Provide your cassandra configurations in cassandra_monitoring.cfg file.
```
[cassandra_1]
hostname=<HOSTNAME>
port=<PORT NUMBER>
logs_enabled=False
log_type_name=None
log_file_path=None
```	
		
The agent will automatically execute the plugin within five minutes and send performance data to the Site24x7 data center.

## Supported Metrics
The following metrics are captured in the IBM MQ monitoring plugin
 
 
- #### Total Latency (Read)
    Read response time, in microseconds.	


- #### Total Latency (Write)
     Write response time, in microseconds.


- #### Cross Node Latency
     The time period starts when a node sends a message and ends when the current node receives it.


- #### Total Hints
     Number of hint messages written to this node since [re]start. Includes one entry for each host to be hinted per hint.
  

- #### Throughtput (Writes)
     Write requests per second

- #### Throughtput (Read)
     Read requests per second.
 

- #### Key cache hit rate
     Fraction of read requests for which the key’s location on disk was found in the cache
  

- #### Load
     Disk space used on a node, in bytes
  

- #### Completed compaction tasks
     Total compaction tasks completed
  

- #### Pending campaction tasks 
     Total compaction tasks in queue.
  

- #### ParNew garbage collections (count) 
     Number of young-generation collections
 

- #### ParNew garbage collections (time) 
     Elapsed time of young-generation collections, in milliseconds
  

- #### CMS garbage collections (count)
     Number of old-generation collections
  

- #### CMS garbage collections (time)
     Elapsed time of old-generation collections, in milliseconds
  

- #### Exceptions
     Requests for which Cassandra encountered an error
 
 
- #### Timeout exceptions (write)
     Requests not acknowledged within configurable timeout window during write
 
 
- #### Timeout exception (read)
     Requests not acknowledged within configurable timeout window during read
 
 
- #### Unavailable exceptions (write)
     Requests for which the required number of nodes was unavailable during writing
 
 
- #### Unavailable exceptions (read)
     Requests for which the required number of nodes was unavailable during reading

 
- #### Pending tasks
     Tasks in a queue awaiting a thread for processing

 
- #### Dropped Mutations
     Number of dropped mutations on this table.

 
- #### Pending Flushes
     Estimated number of flush tasks pending for this table.


- #### Blocked On Allocation
     Number threads are blocked by memtable allocation
 
 
- #### Currently Blocked Tasks
     Number of tasks that are currently blocked due to queue saturation but on retry will become unblocked




