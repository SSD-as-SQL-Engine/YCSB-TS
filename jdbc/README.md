# YCSB-TS / SQLite

## Prerequisites 
#### 1. maven
```bash
$ sudo apt-get install maven
```

#### 2. sqlite 
[Reference](https://github.com/SWE3003-41/SQLite/tree/master/sqlite-source)

#### 3. sqlite-jdbc
```bash
$ wget https://bitbucket.org/xerial/sqlite-jdbc/downloads/sqlite-jdbc-3.27.2.1.jar
```
From now on, we are going to name sqlite-jdbc library path as `[SQLITE-LIB]`.

#### 4. python
```bash
$ sudo apt-get install python
```

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
$ sqlite3 [DB_PATH] < create.sql
```
We are going to see schema in detail next week!
From now on, we are going to name database path as [DB_PATH].

### Load and Run
#### Setting workload 

You can see sample workloads in workloads directory. Let's use `workloada` for tutorial

As `readproportion = 1` this workload is read 100% workload. 
So if you run `workloada` YCSB will issue 1000 read queries as operationcount is 1000.

Before running `workloada`, we need to load data to use. The amount of data is set by `recordcount` parameter. 

As laptop is slow, let's change the number of records:
```
## file workloads/workloada 
recordcount=1000000 --> 100000
```

1 record size is 50B, so recordcount 100000 means 5MB.




#### Load

```bash
$ ./bin/ycsb load jdbc -P workloads/workloada -p db.driver=org.sqlite.JDBC -p db.url=jdbc:sqlite:[DB_PATH] -cp [SQLITE-LIB]
```
- Enter `DB_PATH` as absolute path (절대경로).

#### Run
```bash
$ ./bin/ycsb run jdbc -P workloads/workloada -p db.driver=org.sqlite.JDBC -p db.url=jdbc:sqlite:[DB_PATH] -cp [SQLITE-LIB]
```
