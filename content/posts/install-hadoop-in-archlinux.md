+++
title = "Install Apache Hadoop in Archlinux"
date = 2026-02-28
+++
# Download Java Version
For the hadoop version we are going to install, that will need java11 so first we need to install and set that to default.

```
sudo pacman -S jdk11-opnjdk
sudo archlinux-java set jdk11-opnjdk
```

# Download the Hadoop Binary
First download the latest hadoop binary. I am using `curl` but you can use browser to download from this url [Index of /hadoop/common](https://downloads.apache.org/hadoop/common/)

```
curl -O https://downloads.apache.org/hadoop/common/hadoop-3.4.3/hadoop-3.4.3.tar.gz
```
After downloading the compressed binary we have to extract it

```
tar -xf hadoop-3.4.3.tar.gz
```

Now we will move the hadoop directory to the `/opt` directory

```
sudo mv hadoop-3.4.3 /opt/hadoop
```

# Set Ownership
```
sudo chown -R $USER:$(id -gn) /opt/hadoop
```
# Set Environment Variables
Let's set some environment variables.
In your dafault shell's configuration file `.bashrc` or `.zshrc` set these environment variables.

```
export HADOOP_HOME=/opt/hadoop
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export JAVA_HOME=/usr/lib/jvm/default
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```

To apply these changes open new terminal or run

```
source ~/.bashrc
```

# Verify Installation
```
hadoop version
```
This will return the hadoop version and other information.

# Configuring Hadoop(Pseudo-Distributed Mode)
First change directory to

```
cd /opt/hadoop/etc/hadoop
```
Edit the `core-site.xml` file. Inside `<configuration>` tag add:

```
<property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9000</value>
</property>
```

Now edit the `hdfs-site.xml`. Inside `<configuration>` tag add:

```
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>

<property>
  <name>dfs.namenode.name.dir</name>
  <value>file:///opt/hadoop/hdfs/namenode</value>
</property>

<property>
  <name>dfs.datanode.data.dir</name>
  <value>file:///opt/hadoop/hdfs/datanode</value>
</property>
```

Similarily in `mapred-site.xml`, inside `<configuration>` tag add:

```
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>

<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>

<property>
  <name>mapreduce.map.env</name>
  <value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>

<property>
  <name>mapreduce.reduce.env</name>
  <value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>

<property>
  <name>mapreduce.application.classpath</name>
  <value>
    $HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*,
    $HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*,
    $HADOOP_MAPRED_HOME/share/hadoop/common/*,
    $HADOOP_MAPRED_HOME/share/hadoop/common/lib/*,
    $HADOOP_MAPRED_HOME/share/hadoop/yarn/*,
    $HADOOP_MAPRED_HOME/share/hadoop/yarn/lib/*
  </value>
</property>
```

And now in `yarn-site.xml` add:

```
<property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
<property>
  <name>yarn.nodemanager.env-whitelist</name>
  <value>JAVA_HOME,HADOOP_HOME,HADOOP_MAPRED_HOME</value>
</property>
<property>
  <name>yarn.application.classpath</name>
  <value>
    /opt/hadoop/share/hadoop/common/*,
    /opt/hadoop/share/hadoop/common/lib/*,
    /opt/hadoop/share/hadoop/hdfs/*,
    /opt/hadoop/share/hadoop/hdfs/lib/*,
    /opt/hadoop/share/hadoop/mapreduce/*,
    /opt/hadoop/share/hadoop/mapreduce/lib/*,
    /opt/hadoop/share/hadoop/yarn/*,
    /opt/hadoop/share/hadoop/yarn/lib/*
  </value>
</property>
```

# Configuring SSH
To acces the hadoop we need to configue the SSH. First install the SSH if not installed already:

```
sudo pacman -S openssh
```

Enable and start the SSH service:

```
sudo systemctl enable sshd
sudo systemctl start sshd
```
Generate SSH Keys:

```
ssh-keygen -t rsa -P ""
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

# Install `inetutils`
`hostname` is a dependency and is provided by this utility:

```
sudo pacman -S inetutils
```

# Set JAVA_HOME
Edit `/opt/hadoop/etc/hadoop/hadoop-env.sh` file. Find the line:

```
# export JAVA_HOME=
```

Uncomment the line and set:

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk
```



# Test the SSH Setup
```
ssh localhost
```
You will be connected to the new shell. Run the below command in that shell.

# Format the HDFS
```
hdfs namenode -format
```
# Start Hadoop Services
```
start-dfs.sh
start-yarn.sh
```

Check the running daemons:

```
jps
```
You should see something like:
```
481619 NodeManager
480751 NameNode
480942 DataNode
573619 Jps
481497 ResourceManager
481193 SecondaryNameNode
```

# Access Web Interfaces
| Service         | URL                                            |
| --------------- | ---------------------------------------------- |
| NameNode        | [http://localhost:9870](http://localhost:9870) |
| ResourceManager | [http://localhost:8088](http://localhost:8088) |
