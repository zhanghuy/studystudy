# redis

## 简介

1.基于内存的key-value数据库
2.基于c语言编写的，可以支持多语言的api
3.支持数据持久化
4.value可以是string，hash，list，set， sorted set

## 使用场景

string: 缓存，限流，计数器， 分布式锁，分布式session
hash: 存储用户信息，用户主页访问量，组合查询
list：微博关注人时间轴，简单队列
set：赞，踩，标签，好友关系
zset: 排行榜

## 常用命令

key
    keys * 获取所有的key
    select 0 选择第一个库
    move myString 1 将当前的数据库key移动到某个数据库,目标库有，则不能移动
    flush db      清除指定库
    randomkey     随机key
    type key      类型

    set key1 value1 设置key
    get key1    获取key
    mset key1 value1 key2 value2 key3 value3
    mget key1 key2 key3
    del key1   删除key
    exists key      判断是否存在key
    expire key 10   10过期
    pexpire key 1000 毫秒
    persist key     删除过期时间

string
    set name cxx
    get name
    getrange name 0 -1        字符串分段
    getset name new_cxx       设置值，返回旧值
    mset key1 key2            批量设置
    mget key1 key2            批量获取
    setnx key value           不存在就插入（not exists）
    setex key time value      过期时间（expire）
    setrange key index value  从index开始替换value
    incr age        递增
    incrby age 10   递增
    decr age        递减
    decrby age 10   递减
    incrbyfloat     增减浮点数
    append          追加
    strlen          长度
    getbit/setbit/bitcount/bitop    位操作

hash
    hset myhash name cxx
    hget myhash name
    hmset myhash name cxx age 25 note "i am notes"
    hmget myhash name age note
    hgetall myhash               获取所有的
    hexists myhash name          是否存在
    hsetnx myhash score 100      设置不存在的
    hincrby myhash id 1          递增
    hdel myhash name             删除
    hkeys myhash                 只取key
    hvals myhash                 只取value
    hlen myhash                  长度

list
    lpush mylist a b c  左插入
    rpush mylist x y z  右插入
    lrange mylist 0 -1  数据集合
    lpop mylist  弹出元素
    rpop mylist  弹出元素
    llen mylist  长度
    lrem mylist count value  删除
    lindex mylist 2          指定索引的值
    lset mylist 2 n          索引设值
    ltrim mylist 0 4         删除key
    linsert mylist before a  插入
    linsert mylist after a   插入
    rpoplpush list list2     转移列表的数据

set
    sadd myset redis
    smembers myset       数据集合
    srem myset set1         删除
    sismember myset set1 判断元素是否在集合中
    scard key_name       个数
    sdiff | sinter | sunion 操作：集合间运算：差集 | 交集 | 并集
    srandmember          随机获取集合中的元素
    spop                 从集合中弹出一个元素

zset
    zadd zset 1 one
    zadd zset 2 two
    zadd zset 3 three
    zincrby zset 1 one              增长分数
    zscore zset two                 获取分数
    zrange zset 0 -1 withscores     范围值
    zrangebyscore zset 10 25 withscores 指定范围的值
    zrangebyscore zset 10 25 withscores limit 1 2 分页
    Zrevrangebyscore zset 10 25 withscores  指定范围的值
    zcard zset  元素数量
    Zcount zset 获得指定分数范围内的元素个数
    Zrem zset one two        删除一个或多个元素
    Zremrangebyrank zset 0 1  按照排名范围删除元素
    Zremrangebyscore zset 0 1 按照分数范围删除元素
    Zrank zset 0 -1    分数最小的元素排名为0
    Zrevrank zset 0 -1  分数最大的元素排名为0
    Zinterstore
    zunionstore rank:last_week 7 rank:20150323 rank:20150324 rank:20150325  weights 1 1 1 1 1 1 1
