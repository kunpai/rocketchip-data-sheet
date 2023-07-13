# Rocket Core

## Rocket Branch Predictor

Here are the details for the [branch predictor](https://github.com/chipsalliance/rocket-chip/blob/master/src/main/scala/rocket/BTB.scala):

``` scala
case class BHTParams(
  nEntries: Int = 512,
  counterLength: Int = 1,
  historyLength: Int = 8,
  historyBits: Int = 3)

case class BTBParams(
  nEntries: Int = 28,
  nMatchBits: Int = 14,
  nPages: Int = 6,
  nRAS: Int = 6,
  bhtParams: Option[BHTParams] = Some(BHTParams()),
  updatesOutOfOrder: Boolean = false)
```

A gem5 equivalent would be:

``` python
class RocketBP(TournamentBP):
    BTBEntries = 28
    RASSize = 6
    localHistoryTableSize = 256
    localPredictorSize = 1024
    globalPredictorSize = 1024
    choicePredictorSize = 1024
    localCtrBits = 1
    globalCtrBits = 1
    choiceCtrBits = 2
    indirectBranchPred = SimpleIndirectPredictor()
    indirectBranchPred.indirectSets = 6
```

I picked the tournament BP because of the existence of the history table.
