#  Redis

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

![image-20230816140858987.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230816140858987.png)

- 布隆过滤
  - 优点：内存占用比较少，没有多余 key
  - 缺点：
    - 实现复杂
    - 存在误判可能

![image-20230816141016882.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230816141016882.png)

- 增强 id 的复杂度，避免被猜测 id 规律
- 做好数据的基础格式校验
- 加强用户权限校验

- 做好热点参数的限流

### 缓存雪崩

**缓存雪崩**是指在同一时段大量的缓存 key 同时失效或者 Redis 服务宕机，导致大量请求到达数据库，带来巨大压力。

![image-20230816144909103.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230816144909103.png)

**解决方案**：

- 给不同的 key 的 TTL 添加随机值
- 利用 Redis 集群提高服务的可用性
- 给缓存业务添加降级限流决策
- 给业务添加多级缓存

### 缓存击穿

**缓存击穿问题**也叫热点 key 问题，就是一个被**高并发访问**并且缓存重建业务比较重复的 key 突然失效了，无数的请求访问会在瞬间给数据库带来巨大的冲击。

**解决方案**：

- 互斥锁

![image-20230816150353223.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230816150353223.png)

- 逻辑过期

![image-20230816150753259.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230816150753259.png)

| 解决方法 | 优点                                           | 缺点                                         |
| -------- | ---------------------------------------------- | -------------------------------------------- |
| 互斥锁   | 没有额外的内存消耗<br/>保证一致性<br/>实现简单 | 线程需要等待，性能受影响<br/>可能有死锁风险  |
| 逻辑过期 | 线程无需等待                                   | 不保证一致性<br/>有额外内存消耗<br/>实现复杂 |

### 封装 Redis 工具类

```java
@Slf4j
@Component
public class CacheClient {

    private final StringRedisTemplate stringRedisTemplate;

    private static final ExecutorService CACHE_REBUILD_EXECUTOR = Executors.newFixedThreadPool(10);

    public CacheClient(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }

    public void set(String key, Object value, Long time, TimeUnit unit) {
        stringRedisTemplate.opsForValue().set(key, JSONUtil.toJsonStr(value), time, unit);
    }

    public void setWithLogicalExpire(String key, Object value, Long time, TimeUnit unit) {
        // 设置逻辑过期
        RedisData redisData = new RedisData();
        redisData.setData(value);
        redisData.setExpireTime(LocalDateTime.now().plusSeconds(unit.toSeconds(time)));
        // 写入 Redis
        stringRedisTemplate.opsForValue().set(key, JSONUtil.toJsonStr(redisData));
    }

    public <R,ID> R queryWithPassThrough(
            String keyPrefix, ID id, Class<R> type, Function<ID, R> dbFallback, Long time, TimeUnit unit){
        String key = keyPrefix + id;
        // 1.从 redis 查询缓存
        String json = stringRedisTemplate.opsForValue().get(key);
        // 2.判断是否存在
        if (StrUtil.isNotBlank(json)) {
            // 3.存在，直接返回
            return JSONUtil.toBean(json, type);
        }
        // 判断命中的是否是空值
        if (json != null) {
            // 返回一个错误信息
            return null;
        }

        // 4.不存在，根据 id 查询数据库
        R r = dbFallback.apply(id);
        // 5.不存在，返回错误
        if (r == null) {
            // 将空值写入 redis
            stringRedisTemplate.opsForValue().set(key, "", CACHE_NULL_TTL, TimeUnit.MINUTES);
            // 返回错误信息
            return null;
        }
        // 6.存在，写入 redis
        this.set(key, r, time, unit);
        return r;
    }

    public <R, ID> R queryWithLogicalExpire(
            String keyPrefix, ID id, Class<R> type, Function<ID, R> dbFallback, Long time, TimeUnit unit) {
        String key = keyPrefix + id;
        // 1.从 redis 查询缓存
        String json = stringRedisTemplate.opsForValue().get(key);
        // 2.判断是否存在
        if (StrUtil.isBlank(json)) {
            // 3.存在，直接返回
            return null;
        }
        // 4.命中，需要先把 json 反序列化为对象
        RedisData redisData = JSONUtil.toBean(json, RedisData.class);
        R r = JSONUtil.toBean((JSONObject) redisData.getData(), type);
        LocalDateTime expireTime = redisData.getExpireTime();
        // 5.判断是否过期
        if(expireTime.isAfter(LocalDateTime.now())) {
            // 5.1.未过期，直接返回信息
            return r;
        }
        // 5.2.已过期，需要缓存重建
        // 6.缓存重建
        // 6.1.获取互斥锁
        String lockKey = LOCK_SHOP_KEY + id;
        boolean isLock = tryLock(lockKey);
        // 6.2.判断是否获取锁成功
        if (isLock){
            // 6.3.成功，开启独立线程，实现缓存重建
            CACHE_REBUILD_EXECUTOR.submit(() -> {
                try {
                    // 查询数据库
                    R newR = dbFallback.apply(id);
                    // 重建缓存
                    this.setWithLogicalExpire(key, newR, time, unit);
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }finally {
                    // 释放锁
                    unlock(lockKey);
                }
            });
        }
        // 6.4.返回过期的商铺信息
        return r;
    }

    public <R, ID> R queryWithMutex(
            String keyPrefix, ID id, Class<R> type, Function<ID, R> dbFallback, Long time, TimeUnit unit) {
        String key = keyPrefix + id;
        // 1.从 redis 查询缓存
        String shopJson = stringRedisTemplate.opsForValue().get(key);
        // 2.判断是否存在
        if (StrUtil.isNotBlank(shopJson)) {
            // 3.存在，直接返回
            return JSONUtil.toBean(shopJson, type);
        }
        // 判断命中的是否是空值
        if (shopJson != null) {
            // 返回一个错误信息
            return null;
        }

        // 4.实现缓存重建
        // 4.1.获取互斥锁
        String lockKey = LOCK_SHOP_KEY + id;
        R r = null;
        try {
            boolean isLock = tryLock(lockKey);
            // 4.2.判断是否获取成功
            if (!isLock) {
                // 4.3.获取锁失败，休眠并重试
                Thread.sleep(50);
                return queryWithMutex(keyPrefix, id, type, dbFallback, time, unit);
            }
            // 4.4.获取锁成功，根据 id 查询数据库
            r = dbFallback.apply(id);
            // 5.不存在，返回错误
            if (r == null) {
                // 将空值写入 redis
                stringRedisTemplate.opsForValue().set(key, "", CACHE_NULL_TTL, TimeUnit.MINUTES);
                // 返回错误信息
                return null;
            }
            // 6.存在，写入 redis
            this.set(key, r, time, unit);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }finally {
            // 7.释放锁
            unlock(lockKey);
        }
        // 8.返回
        return r;
    }

    private boolean tryLock(String key) {
        Boolean flag = stringRedisTemplate.opsForValue().setIfAbsent(key, "1", 10, TimeUnit.SECONDS);
        return BooleanUtil.isTrue(flag);
    }

    private void unlock(String key) {
        stringRedisTemplate.delete(key);
    }
}
```

### 全局 ID 生成器

为了增加 ID 的安全性，我们可以不直接使用 Redis 自增的数值，而是拼接一些其他的信息。

- UUID
- Redis 自增
- snowflake 算法
- 数据库自增

```java
@Component
public class RedisIdWorker {
    
    /**
     * 开始时间戳
     */
    private static final long BEGIN_TIMESTAMP = 1640995200L;
    
    /**
     * 序列号的位数
     */
    private static final int COUNT_BITS = 32;

    private StringRedisTemplate stringRedisTemplate;

    public RedisIdWorker(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }

    public long nextId(String keyPrefix) {
        // 1.生成时间戳
        LocalDateTime now = LocalDateTime.now();
        long nowSecond = now.toEpochSecond(ZoneOffset.UTC);
        long timestamp = nowSecond - BEGIN_TIMESTAMP;

        // 2.生成序列号
        // 2.1.获取当前日期，精确到天
        String date = now.format(DateTimeFormatter.ofPattern("yyyy:MM:dd"));
        // 2.2.自增长
        long count = stringRedisTemplate.opsForValue().increment("icr:" + keyPrefix + ":" + date);

        // 3.拼接并返回
        return timestamp << COUNT_BITS | count;
    }
}
```

### 悲观锁

认为线程安全问题一定会发生，因此在操作数据之前先获取锁，确保线程串行执行。

- 例如 Synchronized，Lock 都属于悲观锁

优点：简单粗暴

缺点：性能一般

### 乐观锁

认为线程安全不一定发生，因此不加锁，只是在更新数据时去判断有没有其他线程对数据做了修改。

- 如果没有修改则认为是安全的，自己才更新数据。
- 如果已经被其他线程修改说明发生了安全问题，此时可以重试或异常。

#### 常见方式

乐观锁的关键是判断之前查询得到的数据是否有被修改过

- 版本号法
- CAS 法

优点：性能好

缺点：存在成功率低的问题

## 分布式锁

**分布式锁**：满足分布式系统或集群模式下多进程可见并且互斥的锁

- 多进程可见
- 互斥
- 高可用
- 高性能
- 安全性

### 分布式锁的实现

分布式锁的核心是实现多进程之间互斥，而满足这一点的方式有很多，常见的有：

|        | MySQL                       | Redis                     | Zookeeper                        |
| ------ | --------------------------- | ------------------------- | -------------------------------- |
| 互斥   | 利用 mysql 本身的互斥锁机制 | 利用 setnx 这样的互斥命令 | 利用结点的唯一性和有序性实现互斥 |
| 高可用 | 好                          | 好                        | 好                               |
| 高性能 | 一般                        | 好                        | 一般                             |
| 安全性 | 断开连接，自动释放锁        | 利用锁超时时间，到期释放  | 临时结点，断开连接自动释放       |

### 基于 Redis 的分布式锁

实现分布式锁时需要实验的两个基本方法：

- 获取锁：

  - 互斥：确保只能有一个线程获取锁
  - 非阻塞：尝试一次，成功返回 true，失败返回 false

```shell
# 添加锁，NX 互斥，EX 是设置超时时间
SET lock thread1 NX EX 10
```

- 释放锁：

  - 手动释放
  - 超时释放

```shell
# 释放锁，删除即可
DEL key
```

#### 分布式锁误删情况解决方法

1. 在获取锁时存入线程标识（可以用 UUID 表示）
2. 在释放锁时现获取锁中的线程标识，判断是否与当前线程标识一致
   1. 如果一致则释放锁
   2. 如果不一致则不释放锁

##### Redis 的 Lua 脚本

Redis  提供了 Lua 脚本功能，在一个脚本中编写多条 Redis 命令，确保多条命令执行时的原子性。

```shell
# 执行 redis 命令
redis.call('命令名称', 'key', '其他参数', ....)

# 调用 例：
eval "return redis.call(('set', KEYS[1], ARGV[1], ....)" 1 name hwc
```

释放锁的业务流程：

1. 获取锁种的线程标识
2. 判断是否与指定的标识（当前线程标识）一致
3. 如果一直则释放锁（删除）
4. 如果不一致则什么都不做

```lua
-- 获取锁中的线程标识 get key
local id = redis.call('get', KEYS[1])
-- 比较线程标识与锁中的标识是否一致
if (id == ARGV[1]) then 
    -- 释放锁 del key
    return redis.call('del', KEYS[1])
end
return 
```

### 基于 Redis 的分布式锁优化

1. 不可重入：同一个线程无法多次获取同一把锁
2. 不可重试：获取锁只尝试一次就返回 false，没有重试机制
3. 超时释放：锁超时释放虽然可以避免死锁，但如果是业务执行耗时较长，也会导致锁释放，存在安全隐患
4. 主从一致性：如果 Redis 提供了主从集群，主从同步存在延迟，当主宕机时，如果从并同步主中锁数据，则会出现锁实现

### Redisson

Redisson 是一个在 Redis 的基础上实现的 Java 驻内存数据网络。他不仅提供了一系列的分布式的 Java 常用对象，还提供了许多分布式服务，其中就包含了各种分布式锁的实现。

#### Redisson 入门

1. 引入依赖

```xml
<dependency>
    <groupId>org.redisson</groupId>
    <artifactId>redisson</artifactId>
    <version>3.13.6</version>
</dependency>
```

2. 配置 Redisson 客户端

```java
@Configuration
public class RedisConfig {
    @Bean
    public RedissonClient redissonClient() {
        // 配置类
        Config config = new Config();
        // 添加 redis 地址，这里添加了单点的地址，也可以使用 config.useClusterServers() 添加集群地址
        config.useSingleServer().setAddress("redis://ip:port").setPassword(password);
        // 创建客户端
        return Redisson.create(config);
    }
}
```

3. 使用 Redisson 的分布式锁

#### Redisson 可重入锁原理

![image-20230924214632899.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230924214632899.png)****

- 注意：
  1. 所有的判断和操作都需要使用 Lua 脚本来保证原子性
  2. 每次获取和释放锁时要重置锁的有效期，就像新抢到锁一样，给业务充分的执行时间

- 获取锁的 Lua 脚本：

```lua
local key = KEYS[1];			-- 锁的 key
local threadId = ARGV[1];		-- 线程唯一标识
local releaseTime = ARGV[2];	-- 锁的自动释放时间
-- 判断是否存在
if (redis.call('exists', key) == 0) the
    -- 不存在，获取锁
    redis.call('hset', key, threadId, '1');
    -- 设置有效期
    redis.call('expire', key, releaseTime);
    return 1;	-- 返回结果
end;
-- 锁已经存在，判断 threadId 是否是自己
if (redis.call('hexists', key, threadId) == 1) then 
    -- 不存在，获取锁，重入次数 + 1
    redis.call('hincrby', key, threadId, '1');
    -- 设置有效期
    redis.call('expire', key, releaseTime);
    return 1;
end;
return 0; -- 代码走到这里，说明获取锁不是自己，获取锁失败
```

- 释放锁的 Lua 脚本

```lua
local key = KEYS[1];			-- 锁的 key
local threadId = ARGV[1];		-- 线程唯一标识
local releaseTime = ARGV[2];	-- 锁的自动释放时间
-- 判断当前锁是否还是被自己持有
if (redis.call('hexists', key, threadId) == 0) then
    return nil;		-- 如果已经不是自己，则直接返回
end;
-- 是自己的锁，则重入次数 -1
local count = redis.call('hincrby', key, threadId, -1);
-- 判断是否重入次数是否已经为 0
if (count > 0) then
    -- 大于 0 说明不能释放锁，重置有效期然后返回
    redis.call('expire', key, releaseTime);
    return nil;
else 
    redis.call('del', key);
    return nil;
end;
```

#### **如何重试获取锁？**

**基于 redis Pub / Sub 发布订阅机制。**如果获取锁失败，则阻塞订阅释放锁的消息；当锁被释放时，会触发推送（告诉其他线程我释放锁了），然后其他线程在重试获取；如此往复，直到超时。

#### **如何防止锁提前超时释放？**

**基于看门狗机制**。如果不手动设置锁释放时间（leaseTime)，默认设置 30 秒过期，并且给当前锁注册一个定时任务，该定时任务每隔 1 / 3 的锁释放时间（一般是 10 秒）会重置锁的过期时间（递归调用，一次续期完了再）。

1. 如何保证同一个锁只注册一个定时任务？
2. 如何防止无限续期？

要解决这些问题，使用全局 ConcurrentHashMap 来管理所 => 任务消息，key 为锁的 id，从而保证唯一。当某个锁释放时，从全局 ConcurrentHashMap 中取出定时任务并取消掉，然后把锁的信息从 Map 中删除即可。

**Redisson 分布式锁原理**

![image-20230925201106673.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230925201106673.png)

#### Redisson 分布式锁主从一致性问题

![image-20230925201915720.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230925201915720.png)

如果使用主从复制的 Redis 集群，可能出现主从结点设置的锁状态不一致的问题。

可以使用 Redisson 的 MultiLock （联锁）来解决，核心思想是开启多个独立的 Redis 主节点，设置锁是必须在所有主节点都写入成功，才算设置成功。

这样做之后，哪怕有部分结点挂掉，其他线程也无法 setnx 全部成功，就不会出现重复执行业务的情况。

如下图：

![image-20230925203258255.png](https://zero-img-1314223587.cos.ap-shanghai.myqcloud.com/zero/image-20230925203258255.png)

实现 MultiLock 的几个关键：

1. 遍历所有节点，依次设置锁，并使用列表来记录所有主节点的锁是否设置成功。
2. 只要有一个节点设置不成功，就要释放所有的锁，从头来过。
3. 因为不同节点设置锁成功的时间不同，所以在所有锁设置成功后，要统一设置过期时间（但如果 leaseTime = -1 就不用了，因为开启了看门狗机制会自动续期)。
4. 锁释放时间（leaseTime）必须要大于抢锁最大等待时间（waitTime），否则可能出现第一个节点抢到锁，最后一个节点还没抢到锁，之前的锁就已经超时释放了。所以如果指定了 waitTime 和 leaseTime，默认 leaseTime = waitTime * 2。

MulitLock 最安全，但同样会带来很大的运维成本。

### 小结

1. **不可重入 Redis 分布式锁：**
   - 原理：利用 setnx 的互斥性；利用 ex 避免死锁；释放锁时判断线程标识
   - 缺陷：不可重入、无法重试、锁超时失效
2. **可重入的 Redis 分布式锁：**
   - 原理：利用 hash 结构，记录线程标识和重入次数；利用 watchDog 延续所时间；利用信号量控制锁重试等待
   - 缺陷：redis 宕机引起锁失效问题
3. **Redisson 的 multiLock：**
   - 原理：多个独立的 Redis 结点，必须在所有结点都获取重入锁，才算获取锁成功
   - 缺陷：运维成本高、实现复杂
