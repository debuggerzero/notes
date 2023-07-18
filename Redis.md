# Redis

## 初始 Redis

- 认识 **NoSQL**
  - SQL 
    - 数据结构： 结构化
    - 数据关联：关联化
    - 查询方式：SQL 查询
    - 事务特征：ACID
    - 存储方式：磁盘
    - 扩展性：垂直
  - NoSQL 
    - 数据结构：非结构化
    - 数据关联：无关联化
    - 查询方式：非 SQL
    - 事务特征：BASE
    - 存储方式：内存
    - 扩展性：水平
- 认识 **Redis**
  - 特征
    1. 键值型，value 支持多种不同数据结构，功能丰富；
    2. 单线程，每个命令具备原子性；
    3. 低延迟，速度快（基于内存，IO 多路复用，良好的）；
    4. 支持数据持久化；
    5. 支持主从集群、分片集群；
    6. 支持多语言客户端；

## Redis 命令

### Redis 常用命令

- 通用指令是部分数据类型的，都可以使用指令，常见的有：
  - `KEYS`：查看符合模板的所有 key
  - `DEL`：删除一个指定的 key
  - `EXISTS`：判断 key 是否存在
  - `EXPIRE`：给一个 key 设置有效期，有效期到期时该 key 会被自动删除
  - `TTL`：查看一个 key 的剩余有效期

### String 类型

- String 类型，也就是字符串类型，是 Redis 中最简单的存储类型，其 value 是字符串，不过根据字符串的格式不同，可以分为 3 类

  - string：普通字符串
  - int：整数类型，可以做自增、自减操作
  - float：浮点类型，可以做自增、自减操作

  不管是那种格式，底层都是字节数组形式存储，只不过是编码方式不同。字符串类型的最大控件不能超过512 M.
  
- 常用命令

  - `SET`：添加或者修改已经存在的一个 String 类型的键值对
  - `GET`：根据 key 获取 String 类型的 value
  - `MSET`：批量添加多个 String 类型的键值对
  - `MGET`：更具多个 key 获取多个 String 类型的 value
  - `INCR`：让一个整形的 key 自增 1
  - `INCRBT`：让一个整形的 key 自增并指定步长
  - `INCRBYFLOAT`：让一个浮点类型的数字自增并指定步长
  - `SETNX`：添加一个 String 类型的键值对，前提是这个 key 不存在，否则不执行
  - `SETEX`：添加一个 String 类型的键值对，并且指定有效期 

### Hash 类型

- Hash 类型，也叫散列，其 value 是一个无序字典，类似于 Java 中的 HashMap 结构

- 常用命令：
  - `HSET key field value`：添加或者修改 hash 类型 key 的 field 的值
  - `HGET key field`：获取一个 hash 类型 key 的 field 的值
  - `HMSET`：批量添加多个 hash 类型 key 的 field 的值
  - `HMGET`：批量添加多个 hash 类型 key 的 field 的值
  - `HGETALL`：获取一个 hash 类型的 key 中的所有 field 和 value
  - `HKEYS`：获取一个 hash 类型的 key 中的所有 field
  - `HVALS`：获取一个 hash 类型的 key 中的所有 value
  - `HINCRBY`：让一个 hash 类型 key 的字段值自增并指定步长
  - `HSETNX`：添加一个 hash 类型 key 的 field 值，前提是这个 field 不存在，否则不执行

### List 类型

- List 类型与 Java 中的 LinkedList 类似，可以看做是一个双向链表结构。既可以支持正向检索和反向检索、
  - 有序
  - 元素可以重复
  - 插入和删除快
  - 查询速度一般
- 常用命令：
  - `LPUSH key element ...`：向列表左侧插入一个或多个元素
  - `LPOP key`：移除并返回列表左侧的第一个元素，没有则返回 nil
  - `RPUSH key element ...`：向列表右侧插入一个或多个元素
  - `RPOP key`：移除并返回列表右侧的第一个元素
  - `LRANGE key star end`：返回一段角标范围内的所有元素
  - `BLPOP` 和 `BRPOP`：与 `LPOP` 和 `RPOP` 类似，只不过在没有元素时等待指定时间，而不是直接返回 nil

### Set 类型

- 可以看做是一个 value 为 null 的 HashMap
  - 无序
  - 元素不可重复
  - 查找快
  - 支持交集、并集、差集等功能

- 常用命令：
  - `SADD key member ...`：向 set 中添加一个或者多个元素
  - `SREM key member ...`：移除 set 中的指定元素
  - `SCARD key`：返回 set 中元素的个数
  - `SISMEMBER key member`：判断一个元素是否存在于 set 中
  - `SMEMBERS`：获取 set 中的所有元素
  - `SINTER key1 key2 ...`：求交集
  - `SDIFF key1 key2 ...`：求差集
  - `SUNION key1 key2 ...`：求并集

### SortedSet 类型

- SortedSet 是一个可排序的 set 集合，与 Java中的 TreeSet 有些类似，但底层数据结构却差别很大。SortedSet 中
  的每一个元素都带有一个 score 属性，可以基于 score 属性对元素排序，底层的实现是一个跳表（SkipList）加 hash 表。
  - 可排序
  - 元素不重复
  - 查询速度快
- 常见命令
  - `ZADD key score member`：添加一个或多个元素到 sorted set，如果已经存在则更新其 score 值
  - `ZREM key member`：删除 sorted set 中的一个指定元素
  - `ZSCORE key member`：获取 sorted set 中的指定元素的 score 值
  - `ZRANK key member`：获取 sorted set 中的指定元素的排名
  - `ZCARD key`：获取 sorted set 中的元素个数
  - `ZCOUNT key min max`：统计 score 值在给定范围内的所有元素的个数
  - `ZINCRBY key increment member`：让 sorted set 中的指定元素自增，步长为指定的 increment 值
  - `ZRANGE key min max`：按照 score 排序后，获取指定排名范围内的元素
  - `ZRANGEBYSCORE key min max`：按照 score 排序后，获取指定 score 范围内的元素
  - `ZDIFF、ZINTER、ZUNION`：求差集、交集、并集

## Jedis

网址：https://github.com/redis/jedis

### Jedis 使用的基本步骤

1. 引入依赖

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>4.3.1</version>
</dependency>
```

2. 创建 Jedis 对象，建立连接
3. 使用 Jedis，方法名与 Redis 命令一致

### Jedis 连接池

- Jedis 本身是线程不安全的，并且频繁的创建和销毁连接会有性能损耗，因此我们推荐大家使用 Jedis 连接池代替 Jedis 的直连方式。

```java
package com.zero.util;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig;

public class JedisConnectionFactory {

    private static final JedisPool JEDIS_POOL;

    static {
        // 配置连接池
        JedisPoolConfig poolConfig = new JedisPoolConfig();
        // 最大连接
        poolConfig.setMaxTotal(8);
        // 最大空闲连接
        poolConfig.setMaxIdle(8);
        // 最小空闲连接
        poolConfig.setMinIdle(0);
        // 创建连接池对象
        JEDIS_POOL = new JedisPool(poolConfig, "127.0.0.1", 6379, 1000, "hwc20021123L");
    }

    public static Jedis getJedis() {
        return JEDIS_POOL.getResource();
    }
}

```

## Spring Data Redis

SpringData 是 Spring 中数据操作的模块，包含对各种数据库的集成，其中对 Redis 的集成模块就叫做 Spring DataRedis

网址：https://spring.io/projects/spring-data-redis

- 提供了对不同 Redis 客户端的整合 (Lettuce 和 redis)
- 提供了 RedisTemplate 统一 APl 来操作 Redis
- 支持 Redis 的发布订阅模型
- 支持 Redis 哨兵和 Redis 集群
- 支持基于 Lettuce 的响应式编程
- 支持基于引 JDK、JSON、字符串、Spring 对象的数据序列化及反序列化
- 支持基于 Redis 的 JDKCollection 实现

1. **引入依赖**

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
    </dependency>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-pool2</artifactId>
    </dependency>
</dependencies>
```

2. **配置文件**

```yml
spring:
  redis:
    host:                   # ip
    port:                   # 端口
    password:               # 密码
    lettuce:
      pool:
        max-active:         # 最大连接
        max-idle:           # 最大空闲连接
        min-idle:           # 最小空闲连接
        max-wait:           # 连接等待时间
```

3. **注入 RedisTemplate**

```java
@SpringBootTest
class RedisDemoApplicationTests {
    @Resource
    private RedisTemplate<String, Object> redisTemplate;

    @Test
    void contextLoads() {
        redisTemplate.opsForValue().set("name", "hwc");
        System.out.println(redisTemplate.opsForValue().get("name"));
    }
}
```

