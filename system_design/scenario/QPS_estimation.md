# QPS estimation (Query Per Second)

- DAU (Daily Active Users) 日活跃用户
- MAU (Monthly Active Users)

# Example 1

- Twitter : DAU x number_of_requests / one_day_seconds = 150M x 60 / 86400 ~= 150K
- Peek : Average Concurrent Users x (2->9) = 300K
- Fast Growing : Peek Users x 2
- Read QPS 300K, Write QPS 5K

# Example 2

- Twitter: 300 million MAU, 300 000 000
- 50% of users use Twitter daily
- Users post 2 tweets per day on average
- 10% of tweets contain media
- Data is stored for 5 years

######

- DAU = 300M / 2 = 150M
- Tweets QPS = 150M x 2 / 86400 ~= 3.5K ~= 3K
- Peek = QPS x 2 ~= 6K or 7K
- Tweet media 1M, Media storage 150M x 2 x 0.1 x 1M ~= 30TB per day (30 000 000 000 000 )
- 5 years media storage = 30 TB * 365 * 5 ~= 55PT

# QPS Query Per Second

- 1 K QPS : one web server , one SQL database
- 10 K QPS : one NoSQL, MongoDB, Cassandra
- 1M QPS : Redis, Memcached

# Utils

| **Number**  | **Approximate value**  | **Full Name**  | **Short name** |
|---|---|---|---|
| 2**10 ~= 1 000 | 1 Thousand | 1 Kilobyte | 1 KB |
|  2**20 ~= 1 000 000 |  1 Million  | 1 Megabyte  | 1 MB  |
| 2**30 ~= 1 000 000 000  |  1 Billion  | 1 Gigabyte  | 1 GB  |
|  2**40 ~= 10**12 |  1 Trillion  |  1 Terabyte | 1 TB  |
|  2**50 ~= 10**15 |  1 Quadrillion  | 1 Petabyte  | 1 PB  |