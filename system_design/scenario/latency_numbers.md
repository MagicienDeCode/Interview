# Latency numbers every programmer should know

- 1 s = 1 000 ms 
- 1 m = 1 000 µs = 1 000 000 ns

| **Operation Name**  | **Time**  |   | 
|---|---|---|
| L1 cache reference  | 0.5 ns  | ▢ |
|  Branch mispredict | 5 ns  | ▣ ▣ ▣ ▣ ▣  |
|  L2 cache reference | 7 ns | ▣ ▣ ▣ ▣ ▣ ▣ ▣  |
|  Mutex lock/unlock | 100 ns  | ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ x 10 |
| Main memory reference  | 100 ns  |  ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ ▣ x 10 |
|   |   | ✪ = 1 µs = 1 000 ns =  ▣ x 1 000 |
| Compress 1K bytes with Zippy  | 10 000 ns = 10 µs  |  ✪✪✪✪✪✪✪✪✪✪  |
|  Send 2K bytes over 1 Gbps network | 20 000 ns = 20 µs  | ✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪✪  |
| Read 1MB sequentially from memory  | 250 000 ns = 250 µs  |  ✪✪✪✪✪✪✪✪✪✪ x 25 |
|  Round trip within the same datacenter | 500 000 ns = 500 µs  | ✪✪✪✪✪✪✪✪✪✪ x 50  |
|   |   | █  = 1 ms = 1 000 µs = ✪ x 1 000 = 1 000 000 ns = ▣ x 1 000 000  |
| Disk seek  |  10 000 000 ns = 10 ms | █ █ █ █ █ █ █ █ █ █   |
|  Read 1MB sequentially from network  |  10 000 000 ns = 10 ms | █ █ █ █ █ █ █ █ █ █   |
| Read 1MB sequentially from disk  | 30 000 000 ns = 30 ms  | █ █ █ █ █ █ █ █ █ █ x 3   |
| Round packet CA->Netherlands->CA  | 150 000 000 ns = 150 ms  | █ █ █ █ █ █ █ █ █ █  x 15  |
