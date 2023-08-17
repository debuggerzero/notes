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

SpringData 是 Spring 中数据操作的模块，包含对各种数据库的集成，其中对 Redis 的集成模块就叫做 Spring Data Redis

网址：https://spring.io/projects/spring-data-redis

- 提供了对不同 Redis 客户端的整合 (Lettuce 和 redis)
- 提供了 RedisTemplate 统一 APl 来操作 Redis
- 支持 Redis 的发布订阅模型
- 支持 Redis 哨兵和 Redis 集群
- 支持基于 Lettuce 的响应式编程
- 支持基于引 JDK、JSON、字符串、Spring 对象的数据序列化及反序列化
- 支持基于 Redis 的 JDKCollection 实现

### Spring Data Redis 使用步骤

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

### Spring Data Redis 的序列化方式

#### **方法一**：

1. 自定义 RedisTemplate
2. 修改 RedisTemplate 的序列化器

```java
@Configuration
@RequiredArgsConstructor
public class RedisConfig {
    @Bean
    public RedisTemplate<Object, Object> redisTemplate(RedisConnectionFactory factory) {
        // 创建 RedisTemplate 对象
        RedisTemplate<Object, Object> template = new RedisTemplate<>();
		// 设置连接工厂
        template.setConnectionFactory(factory);
        // 配置 序列化方式
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
		// 设置序列化
        template.setKeySerializer(stringRedisSerializer);
        template.setValueSerializer(stringRedisSerializer);
        template.setHashKeySerializer(stringRedisSerializer);
        template.setHashValueSerializer(stringRedisSerializer);
        // 返回
        return template;
    }
}
```

#### 方法二：

1. 使用 StringRedisTemplate
2. 写入 Redis 时，手动把对象序列化为 JSON
3. 读取 Redis 时，手动把读取到的 JSON 反序列化为对象

## Redis 常用场景

### 集群的 session 共享问题

**Session 共享问题**：多台 Tomcat 并不共享 Session 存储空间，当请求切换到不同 Tomcat 服务时导致数据丢失的问题。

Session 的替代方案应该满足：

- 数据共享
- 内存存储
- key-value 结构

### 什么是缓存

**缓存**就是数据交换的缓冲区（ 称作 Cache )，是存贮数据的临时地方，一般读写性能较高。

**缓存的作用：**

- 降低后端负载
- 提高读写效率，降低响应时间

**缓存的成本：**

- 数据的一致性成本
- 代码维护成本
- 运维成本

### 缓存更新策略

|          | 内存淘汰                                                     | 超时剔除                                                     | 主动更新                                   |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ |
| 说明     | 不用自己维护，利用 Redis 的内存淘汰机制，当内存不足时自动淘汰部分数据。下次查询时更新缓存。 | 给缓存数据添加 TTL 时间，到期后自动删除缓存。下次查询时更新缓存 | 编写业务逻辑，在修改数据库的同时，更新缓存 |
| 一致性   | 差                                                           | 一般                                                         | 好                                         |
| 维护成本 | 无                                                           | 低                                                           | 高                                         |

#### 主动更新策略

1. 由缓存的调用者，在更新数据库的同时更新缓存。
   1. 删除缓存还是更新缓存？
      1. 更新缓存：每次更新数据库都更新缓存，无效写操作较多
      2. 删除缓存：更新数据库时让缓存失效，查询时再更新缓存
   2. 如何保证缓存与数据库的操作的同时成功或失败？
      1. 单体系统，将缓存与数据库操作放在一个事物
      2. 分布式系统，利用 TCC 等分布式事务方案
   3. 先操作缓存还是先操作数据库？
      1. 先删除缓存，再操作数据库
      2. 先操作数据库，在删除缓存  √
2. 缓存和数据库整合为一个服务，由服务来维护一致性，调用者调用该服务，无需关心缓存一致性问题。
3. 调用者只操作缓存，由其他线程异步的将缓存数据持久化到数据库，保证最终一致。

**业务场景：**

- 低一致性需求：使用内存淘汰机制。
- 高一致性需求：主动更新，并以超时剔除作为兜底方案。
  - 读操作：
    - 缓存命中则直接返回
    - 缓存未命中则查询数据库，并写入缓存，设定超时时间
  - 写操作：
    - 先写数据库，然后再删除缓存
    - 要确保数据库与缓存操作的原子性

### 缓存穿透

**缓存穿透**是指客户端请求的数据在缓存中和数据库中都不存在，这样缓存永远不会生效，这些请求都会达打到数据库。

**解决方法**：

- 缓存空对象
  - 优点：实现简单，维护方便
  - 缺点：
    - 额外的内存小号
    - 可能造成短期的不一致

![image-20230816140858987](Redis.assets\image-20230816140858987.png)

- 布隆过滤
  - 优点：内存占用比较少，没有多余 key
  - 缺点：
    - 实现复杂
    - 存在误判可能

![image-20230816141016882](Redis.assets\image-20230816141016882.png)

- 增强 id 的复杂度，避免被猜测 id 规律
- 做好数据的基础格式校验
- 加强用户权限校验

- 做好热点参数的限流

### 缓存雪崩

**缓存雪崩**是指在同一时段大量的缓存 key 同时失效或者 Redis 服务宕机，导致大量请求到达数据库，带来巨大压力。

![image-20230816144843223](Redis.assets\image-20230816144843223.png)

**解决方案**：

- 给不同的 key 的 TTL 添加随机值
- 利用 Redis 集群提高服务的可用性
- 给缓存业务添加降级限流决策
- 给业务添加多级缓存

### 缓存击穿

**缓存击穿问题**也叫热点 key 问题，就是一个被**高并发访问**并且缓存重建业务比较重复的 key 突然失效了，无数的请求访问会在瞬间给数据库带来巨大的冲击。

**解决方案**：

- 互斥锁

![image-20230816150353223](Redis.assets\image-20230816150353223.png)

- 逻辑过期

![image-20230816150753259](E:\Notes\Redis.assets\image-20230816150753259.png)

| 解决方法 | 优点                                           | 缺点                                         |
| -------- | ---------------------------------------------- | -------------------------------------------- |
| 互斥锁   | 没有额外的内存消耗<br/>保证一致性<br/>实现简单 | 线程需要等待，性能受影响<br/>可能有死锁风险  |
| 逻辑过期 | 线程无需等待                                   | 不保证一致性<br/>有额外内存消耗<br/>实现复杂 |

