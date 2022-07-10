1. difficult to confirm ACK
2. cannot consume twice
3. doesn't support group

```kotlin
import kotlinx.coroutines.coroutineScope
import kotlinx.coroutines.delay
import kotlinx.coroutines.launch
import redis.clients.jedis.Jedis

val REDIS_P_TO_C = "redis_point_to_point"

suspend fun main(): Unit = coroutineScope {
    launch { producer() }
    launch { consumer() }
    delay(2000)
    launch { producer2() }
    launch { consumer2() }
}

fun producer() {
    val jedis = Jedis("127.0.0.1", 6379)
    println("launch producer")
    jedis.lpush(REDIS_P_TO_C, "message 1").also { println("push message 1") }
    jedis.lpush(REDIS_P_TO_C, "message 2").also { println("push message 2") }
}

fun consumer() {
    val jedis = Jedis("127.0.0.1", 6379)
    println("launch consumer")
    while (true) {
        val message = jedis.rpop(REDIS_P_TO_C)
        if (message != null) {
            println("Received: $message")
        }
    }
}

fun producer2() {
    val jedis = Jedis("127.0.0.1", 6379)
    println("launch producer")
    jedis.lpush(REDIS_P_TO_C, "message 1").also { println("push message 1") }
    jedis.lpush(REDIS_P_TO_C, "message 2").also { println("push message 2") }
    jedis.lpush(REDIS_P_TO_C, "message 3").also { println("push message 3") }
}

fun consumer2() {
    val jedis = Jedis("127.0.0.1", 6379)
    println("launch consumer")
    while (true) {
        jedis.brpop(2, REDIS_P_TO_C)?.let { println("Received: $it") }
    }
}
/*
launch producer
launch consumer
Received: message 1
push message 1
push message 2
Received: message 2
launch producer
launch consumer
push message 1
Received: message 1
push message 2
Received: message 2
Received: message 3
push message 3
 */

```