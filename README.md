# Scala Agent

Akka's Agents are wonderful. 

They effectively are concurrent `var`'s with asynchronous capabilities.

But when do you use them? Great question! Consider using an Agent instead of an Actor:

## Agent vs Actor

A crucial difference between an Agent and an Actor is that an Actor receives data, whereas an Agent receives functions.

An actor will change its own state based on the data that it receives.

Whereas an Agent will change its data based on the function it receives.

Both Actors and Agents have internal message queues.

An Agent however is not capable of side effects unlike an Actor.

An Agent provides you with synchronous access to its data, whereas an Actor does not.

By passing functions you don't need to create unnecessary case classes and type hierarchies, you just deal with it as 
if were any simple synchronous code.


Agents are somewhat a dual to an actor - to Agents you pass functions and the state is public, to Actors you pass data and they have their own private state. Here's [an interesting read](http://michaelneale.blogspot.sg/2012/06/agents-and-actors-oh-my.html).


Also [a couple of clojure agent examples](https://lethain.com/a-couple-of-clojure-agent-examples/).

And a question [agents vs actors in clojure?](https://groups.google.com/d/msg/clojure/VuV_mi9m510/py7JSDoAP6IJ)

Someone even [came up](https://www.chrisstucchio.com/blog/2014/agents.html) with [scalaz_agent](https://github.com/stucchio/scalaz_agent), though I'm not sure if it's definitely the same thing.

Interesting read: is [Clojure better at concurrency than Scala?](https://www.quora.com/Is-Clojure-better-at-concurrency-than-Scala/answer/Gary-Verhaegen?srid=DB6V).

Another one: [Making Sense of Clojure's Overlooked Agents](http://www.shayne.me/blog/2015/2015-09-14-clojure-agents/).. "our functions can operate ignorant of concurrency issues" sounds nice!

Another way to think about it: your agent functions act directly on the state. This means that you have an unlimited interface to that state. Actors on the other hand limit the interface tightly - which is exactly why it's better for distribution than an agent is - since functions are much tougher to pass about than data. It's almost like an Agent could be better for a prototype.

["actors in clojure - why not?" comment](http://www.dalnefre.com/wp/2010/06/actors-in-clojure-why-not/#comment-23).




```scala
import akka.agent.Agent
import scala.concurrent.ExecutionContext.Implicits.global

object ExampleAgent extends App {
  sealed trait SomeState {
    def include(input: Input): SomeState
    def someValue: Value
  }
  object SomeState {
  
  }
  val stateAgent = Agent(SomeState.initial)
  
  inParallel { input =>
    stateAgent
      .alter(_.include(input))
      .map(_.someValue)
      .foreach(println)
  }
  
  every(2.seconds) {
    println(stateAgent().someValue)
  }

}
```

- Used for [collecting some metrics in paypal/squbs](https://github.com/paypal/squbs/blob/master/squbs-pattern/src/main/scala/org/squbs/pattern/timeoutpolicy/TimeoutPolicy.scala#L35)
- and [maintaining state in paypal/squbs unicomplex](https://github.com/paypal/squbs/blob/master/squbs-unicomplex/src/main/scala/org/squbs/unicomplex/Unicomplex.scala).
- Used in gearpump, although usage seems inappropriate and better [for an actor](https://github.com/gearpump/gearpump/blob/master/core/src/main/scala/io/gearpump/transport/Express.scala#L92).
- Some sort of [game related indexing service](https://github.com/shioriotome/anzuchang/blob/dbd2348d025314497d127b1ed59441a16595f3ed/stream/src/main/scala/walfie/gbf/raidfinder/KnownBossesMap.scala)
- [Wellcome Collection OaiHarvestActor](https://github.com/wellcometrust/platform-api/blob/91698b5177f220d49ef946d53e42ccf2a828a862/calm_adapter/src/main/scala/uk/ac/wellcome/calm_adapter/actors/OaiHarvestActor.scala) - for some London Museum website
- Guardian editorial [permissions store](https://github.com/guardian/editorial-permissions-client/blob/bbae1d8b743ab5bdf64fed1a8ce58421efe11e49/src/main/scala/com/gu/editorial/permissions/client/PermissionsStore.scala#L45)
- Guardian's image management system: [not clear how though](https://github.com/guardian/grid/blob/13c841ab315857bf6db0bd00aa53ac9afc45009c/common-lib/src/main/scala/com/gu/mediaservice/lib/BaseStore.scala)
- Demo from Akka in Action [for recording books sold](https://github.com/gilbutITbook/006877/blob/699a04504088b731ccce84a136af07b2cfb9f633/chapter-state/src/main/scala/aia/state/Agent.scala#L16)
- Ovo tech but [not sure how](https://github.com/ovotech/comms-profiles/blob/ff8308f7b4c5dbcc422fd0a4737bf476f47150ae/src/main/scala/com/ovoenergy/comms/profiles/Main.scala#L40) (code by ex-guardian person... they love agents; that's where I learned them too)
- For something in [an ethereum client](https://github.com/input-output-hk/etc-client/blob/2b9fec28ed83daab8ec46d45a2b70af55d34e222/src/main/scala/io/iohk/ethereum/network/ServerActor.scala)
- Some state storage/event cache [for an analytics app](https://github.com/lancewf/narrative-analytics/blob/55cffc7a98db388694604b7a9031b02b5af57fdd/src/main/scala/com/finfrock/narrative_analytics/model/EventCache.scala)
- Guardian using it [for some salesforce code](https://github.com/guardian/support-workers/blob/8d74dfaee2fb04e94a3f1a749d7a53dbaecb4930/common/src/main/scala/com/gu/salesforce/SalesforceService.scala)

