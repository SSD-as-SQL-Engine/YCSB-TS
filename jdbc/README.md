# YCSB-TS / SQLite

## Prerequisites 
#### 1. java
```bash
$ sudo apt-get install sodftware-properties-common
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```
Check `echo $JAVA_HOME`. 

#### 2. maven
```bash
$ sudo apt-get install maven3
```

#### 3. sqlite 
[Reference](https://github.com/SWE3003-41/SQLite/tree/master/sqlite-source)

#### 4. sqlite-jdbc
```bash
$ wget https://bitbucket.org/xerial/sqlite-jdbc/downloads/sqlite-jdbc-3.27.2.1.jar
```
From now on, we are going to name sqlite-jdbc library path as `[SQLITE-LIB]`.



## Build

### Clone YCSB-TS repository
``` bash
$ git clone https://github.com/SWE3003-41/YCSB
$ cd YCSB-TS
```
From now on, all the command will be issued on `YCSB-TS` directory. 

### Build YCSB-TS jdbc
``` bash
$ mvn -pl com.yahoo.ycsb:jdbc-binding -am clean package
```

## Load and Run

### Create Table 
```bash
$ sqlite [DB_PATH] < create.sql
```
We are going to see schema in detail next week!
From now on, we are going to name database path as [DB_PATH]`.

### Load and Run
#### Load
```bash
$ ./bin/ycsb load jdbc -P workloads/workloada -p db.driver=org.sqlite.JDBC -p db.url=jdbc:sqlite://[DB_PATH] -cp [SQLITE-LIB]
```

#### Run
```bash
$ ./bin/ycsb run jdbc -P workloads/workloada -p db.driver=org.sqlite.JDBC -p db.url=jdbc:sqlite://[DB_PATH] -cp [SQLITE-LIB]
```
