# scala-agent
Scala Akka Agents

...


```scala
object Wat extends App {


}
```

Used for [collecting some metrics in paypal/squbs](https://github.com/paypal/squbs/blob/master/squbs-pattern/src/main/scala/org/squbs/pattern/timeoutpolicy/TimeoutPolicy.scala#L35)
and [maintaining state in paypal/squbs unicomplex](https://github.com/paypal/squbs/blob/master/squbs-unicomplex/src/main/scala/org/squbs/unicomplex/Unicomplex.scala).

Used in gearpump, although usage seems inappropriate and better [for an actor](https://github.com/gearpump/gearpump/blob/master/core/src/main/scala/io/gearpump/transport/Express.scala#L92).
