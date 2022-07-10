1. cannot make sure every subscriber received message in the same time.
2. if subscriber blocked, may force disconnected.

```kotlin
import kotlinx.coroutines.coroutineScope
import kotlinx.coroutines.delay
import kotlinx.coroutines.launch
import redis.clients.jedis.Jedis
import java.util.concurrent.TimeUnit

data class Subscriber(val name: String, val topic: String) {
    private val jedis = Jedis("127.0.0.1", 6379)
    fun receive() {
        println("subscriber[$name], Receive: ${jedis.rpop(topic)}")
    }
}

val TOPIC1 = "redis_topic1"
val TOPIC2 = "redis_topic2"
val subscriberMap: MutableMap<String, MutableList<Subscriber>> = HashMap()

suspend fun main(): Unit = coroutineScope {
    launch { publisher1() }
    launch { publisher2() }
    delay(3000)
    launch { subscriber1() }
    launch { subscriber2() }
}

fun register(s: Subscriber, t: String) = subscriberMap.computeIfAbsent(t) { ArrayList() }.add(s)
fun publish(t: String) = subscriberMap[t]?.let { it ->
    it.forEach(Subscriber::receive)
}

fun publisher1() {
    val jedis = Jedis("127.0.0.1", 6379)
    var count = 100
    while (true) {
        jedis.lpush(TOPIC1, "message $count").also { println("publish message $count") }
        count++
        publish(TOPIC1)
        TimeUnit.SECONDS.sleep(2)
    }
}

fun publisher2() {
    val jedis = Jedis("127.0.0.1", 6379)
    var count = 2000
    while (true) {
        jedis.lpush(TOPIC2, "message $count").also { println("publish message $count") }
        count++
        publish(TOPIC2)
        TimeUnit.SECONDS.sleep(2)
    }
}

fun subscriber1() {
    val subscriber = Subscriber("Xiang1", TOPIC1)
    register(subscriber, TOPIC1)
}

fun subscriber2() {
    val subscriber = Subscriber("LI2", TOPIC2)
    register(subscriber, TOPIC2)
}

/*
publish message 100
publish message 2000
publish message 101
publish message 2001
publish message 102
publish message 2002
subscriber[LI2], Receive: message 2007
subscriber[Xiang1], Receive: message 107
publish message 103
publish message 2003
subscriber[Xiang1], Receive: message 108
subscriber[LI2], Receive: message 2008
publish message 104
publish message 2004
subscriber[Xiang1], Receive: message 100
subscriber[LI2], Receive: message 2000
publish message 2005
publish message 105
subscriber[LI2], Receive: message 2001
subscriber[Xiang1], Receive: message 101

Process finished with exit code 130 (interrupted by signal 2: SIGINT)

 */
```