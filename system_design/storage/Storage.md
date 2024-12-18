# Storage

|   |   |   |   |   |   |
|---|---|---|---|---|---|
| MySQL,PostgreSQL  |  store&select complex relational data | better for schema stable data  |   |   | |
| Memcached  | Key-Value NoSQL  | value **NOT** support SET/LIST  |  Memory-level access speed | **NOT** support persistence  |   |
|  Redis | Key-Value NoSQL  | value support SET/LIST  | can add/append data to values  | Memory-level access speed but lower than Memcached  |  can be Cache / MessageQueue / Database |
| Cassandra,Hbase  | Column Family Key-Value NoSQL  | row-key, column-key (range query)  | better for simple query  |   |   |
| MongoDB  | Document Based NoSQL  | better for write more read less  |   |   |   |
| Rocksdb  | Key-Value NoSQL  | value **NOT** support SET/LIST  | big company use as Key-Value bottom layer  |   |   |
|  Amazon Dynamo DB | Key-Value NoSQL  | better for massive data, limit response time  |   |   |   |
|  AxonEventStore |   |   |   |   |   |
|   |   |   |   |   |   |

# QPS Query Per Second

- 1 K QPS : one web server , one SQL database
- 10 K QPS : one NoSQL, MongoDB, Cassandra
- 1M QPS : Redis, Memcached

# Video
[Youtube](https://www.youtube.com/watch?v=mWW-T2oHN7E)
[bilibili](https://www.bilibili.com/video/BV1sr4y1E7Xt/)
[ixigua](https://www.ixigua.com/i7118758207765512717/)
