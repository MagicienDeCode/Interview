# Storage

|   |   |   |   |   |   |
|---|---|---|---|---|---|
| MySQL,PostgreSQL  |  store&select complex relational data | better for schema stable data  |   |   | |
| Memcached  | Key-Value NoSQL  | value **NOT** support SET/LIST  |  Memory-level access speed | **NOT** support persistence  |   |
|  Redis | Key-Value NoSQL  | value support SET/LIST  | can add/append data to values  | Memory-level access speed but lower than Memcached  |  can be Cache / MessageQueue / Database |
| Cassandra,Hbase  | Column Family Key-Value NoSQL  | row-key, column-key (range query)  | better for simple query  |   |   |
| MongoDB  | Document Based NoSQL  | better for write more read less  |   |   |   |
| Rocksdb  | Key-Value NoSQL  | value **NOT** support SET/LIST  | big company use as Key-Value bottom layer  |   |   |
|  AmazonDB | Key-Value NoSQL  | better for massive data, limit response time  |   |   |   |
|  AxonEventStore |   |   |   |   |   |
|   |   |   |   |   |   |