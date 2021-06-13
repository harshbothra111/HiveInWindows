## Instructions
Keep all folders in E or D drive and update the below commands according to your installed path
### Java Setup
- Install JDK **jdk-8u291-windows-x64.exe**
- Setup Environment variables
- - ** Add C:\Program Files\Java\jdk1.8.0_291\bin** to **Path** variable
- - Create new variable **JAVA_HOME **with value **C:\Program Files\Java\jdk1.8.0_291**

### Hadoop Setup
- Extract contents of **hadoop-3.3.0.zip**
- Move the extracted contents to folder **hadoop-3.3.0**
- Setup Environment variables
- - ** Add YourPath\hadoop-3.3.01\bin** to **Path** variable
- - Create new variable **HADOOP_HOME **with value **YourPath\hadoop-3.3.01**
- Verify **JAVA_HOME** in **YourPath\hadoop-3.3.0\etc\hadoop\hadoop-env.cmd** as **C:\PROGRA~1\Java\JDK18~1.0_2** (JDK path with ProgramFiles trimmed)
- Create two folders **datannode** and **nodename** inside data folder(create data folder also) inside **YourPath\hadoop-3.3.0**
- Update **YourPath\hadoop-3.3.0\etc\hadoop\hdfs-site.xml** with your correct data path inside hadoop folder with following values
&lt;property>
&lt;name>dfs.replication&lt;/name>
&lt;value>1&lt;/value>
&lt;/property>
&lt;property>
&lt;name>dfs.namenode.name.dir&lt;/name>
&lt;value>file:///YourPath/hadoop-3.3.0/data/dfs/namenode&lt;/value>
&lt;/property>
&lt;property>
&lt;name>dfs.datanode.data.dir</name>
&lt;value>file:///YourPath/hadoop-3.3.0/data/dfs/datanode&lt;/value>
&lt;/property>
- Execute **hdfs namenode -format** command in cmd to format namenode
- Open cmd and navigate to %HADOOP_HOME%\sbin and execute **start-dfs.cmd** to start the hadoop nodes
- Open cmd and navigate to %HADOOP_HOME%\sbin and execute **start-yarn.cmd** to start the hadoop yarn service
- Execute **jps** command to verify services as followed
14560 DataNode
4960 ResourceManager
5936 NameNode
768 NodeManager
14636 Jps
- Verify following Hadoop UI with following URLs
http://localhost:9870/dfshealth.html
http://localhost:9864/datanode.html
http://localhost:8088/cluster

### Derby Setup
- Setup Environment variables
- - ** Add YourPath\db-derby-10.14.2.0-bin\bin** to **Path** variable
- - Create new variable **DERBY_HOME **with value **YourPath\db-derby-10.14.2.0-bin**
- Execute **StartNetworkServer -h 0.0.0.0** command in cmd to start Derby

### Hive Setup
- Setup Environment variables
- - ** Add YourPath\apache-hive-3.1.2\bin** to **Path** variable
- - Create new variable **HIVE_HOME **with value **YourPath\apache-hive-3.1.2**
- Install **Cygwin** with all packages
- Create two folders as
E:\cygdrive
C:\cygdrive
- Open cmd as admin and execute follwing commands
mklink /J  E:\cygdrive\e\ E:\
mklink /J  C:\cygdrive\c\ C:\
- Update **C:\cygwin64\home\YourUserName\bashrc** file by  adding  following lines
export HADOOP_HOME='/cygdrive/e/YourPath/hadoop-3.3.0'
export PATH=$PATH:$HADOOP_HOME/bin
export HIVE_HOME='/cygdrive/e/YourPath/apache-hive-3.1.2'
export PATH=$PATH:$HIVE_HOME/bin
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$HIVE_HOME/lib/*.jar
- Open cygwin terminal and execute following command to initialize  Hive metastore
**$HIVE_HOME/bin/schematool -dbType derby -initSchema**
- Open cmd in new terminal as admin and execute following command to start hive2 service **hive --service hiveserver2 start**
- open cmd in new terminal and execute command to enter into **Hive CLI**
**hive**

**Alternate for Cygwin**
- hive --service schematool -dbType derby -initSchema

### HIVE GUI
Install dbeaver community edition for accessing Hive GUI (dbeaver-ce-7.3.5-x86_64-setup.exe) 
