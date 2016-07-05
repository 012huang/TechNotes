
# [Apache Avro](http://avro.apache.org/)

- Avro 是 Hadoop 中的一个子项目，也是Apache中一个独立的项目，Avro是一个基于二进制数据传输高性能的中间件。在Hadoop的其他项目中例如HBase(Ref)和Hive(Ref)的Client端与服务端的数据传输也采用了这个工具，Avro可以做到将数据进行序列化，适用于远程或本地大批量数据交互。

- 在传输的过程中Avro对数据二进制序列化后 ```节约数据存储空间``` 和 ```网络传输带宽```。

- 消息从客户端发送到服务器端需要经过传输层(Transport Layer)，它发送消息并接收服务器端的响应。到达传输层的数据就是二进制数据。通常以HTTP作为传输模型，客户端数据以POST方式发送到服务器端。消息被封装成为一组缓冲区(Buffer)，Avro规定一个标准的序列化的格式，即无论是文件存储还是网络传输，数据的Schema都出现在数据的前面。数据本身并不包含任何Metadata(Tag). 在文件储存的时候，schema出现在文件头中。在网络传输的时候Schema出现在初始的握手阶段，客户端和服务器端需要维护一个可见的协议缓存，因此，简单来说一个握手完成后，在进行网络交 换的时候不需要再传输协议的全部文本。

- Get the latest stable Avro Tools jar (avro-tools-1.7.x.jar) file from the [Avro Release](http://avro.apache.org/releases.html#Download) page.

## example 

- twitter.avsc

```
{
  "type" : "record",
  "name" : "twitter_schema",
  "namespace" : "com.miguno.avro",
  "fields" : [ {
    "name" : "username",
    "type" : "string",
    "doc"  : "Name of the user account on Twitter.com"
  }, {
    "name" : "tweet",
    "type" : "string",
    "doc"  : "The content of the user's Twitter message"
  }, {
    "name" : "timestamp",
    "type" : "long",
    "doc"  : "Unix epoch time in seconds"
  } ],
  "doc:" : "A basic schema for storing Twitter messages"
}
```

- twitter.json

```
{"username":"miguno","tweet":"Rock: Nerf paper, scissors is fine.","timestamp": 1366150681 }
{"username":"BlizzardCS","tweet":"Works as intended.  Terran is IMBA.","timestamp": 1366154481 }
```

### JSON to binary Avro

```shell
$ java -jar ~/avro-tools-1.7.7.jar fromjson --schema-file twitter.avsc twitter.json > twitter.avro
```

### Binary Avro to JSON

```shell
$ java -jar ~/avro-tools-1.7.7.jar tojson twitter.avro > twitter.json
```

### Retrieve Avro schema from binary Avro

```shell
$ java -jar ~/avro-tools-1.7.7.jar getschema twitter.avro > twitter.avsc
```

### Avsc file to Java 

```shell
java -jar /path/to/avro-tools-1.7.7.jar compile schema <schema file> <code destination>  
  
## example
java -jar ~/avro-tools-1.7.7.jar compile schema twitter.avsc ~/
```

### Prints out content for a given parquet file

```
/zion/etl/event.db/event/2016042520 $
java -jar ~/parquet-tools-1.6.0-IBM-7.jar cat part-m-00000.snappy.parquet > abc
java -jar ~/parquet-tools-1.6.0-IBM-7.jar cat --json part-m-00000.snappy.parquet > abc_json
```



## Reference

- [Reading and Writing Avro Files From the Command Line](http://www.michael-noll.com/blog/2013/03/17/reading-and-writing-avro-files-from-the-command-line/)
- [avro 序列化方法](http://blog.jqian.net/post/avro.html)
- [Avro入门1–序列化与远程通信](http://ju.outofmemory.cn/entry/6966)
- [Hadoop Dev | How to use the Avro and Parquet Tools with IOP 4.1 - Hadoop Dev](https://developer.ibm.com/hadoop/blog/2015/11/10/use-parquet-tools-avro-tools-iop-4-1/)




