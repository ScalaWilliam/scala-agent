# scala-agent
Scala Akka Agents

...


```scala
object Wat extends App {


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

