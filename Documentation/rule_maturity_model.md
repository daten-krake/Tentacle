# Rule Maturity Model

In general a maturity model is something that measures the maturity of an organisation or a process or you name  it.
For our Detection Engineering Framework I wanted to implement something similar, i know there is already work done in that space but
I wanted to provide something that has my own touch to it and at  least what i saw a lot of rules are not tracked for their maturity in Logic
only for their State and i believe we should differ here.

A State is something that tracks the Status of the Rule, like dev,flight,prod this describes where the rule is. Stages on the other hand 
describe the maturity of the logic inside. You can have a lot of production rules that are just checking  for indicators these rules would be low
in maturity or you could have a rule that you revise to a higher maturity  level in Dev-space.


## The Stages

In Detection Engineering there  is a time where you need to act fast and there are time where you can Lab something out to get every little
bit of telemetry and edgecase covered. This is why i want to build this on 3 Stages:

### Indicator
#### Description
This would be a Detection that focuses on an Artifact like a Hash,IP,Domain you name it. This is very useful in situation of emerging new threats,tools or shared TI that you want  to check on. There is nothing wrong with such a rule, but as we all know they are easily bypass-able and in general should not be your long-term solution.

#### Example
This is a super simplified Example of such a rule:

```kql
DeviceFileEvents
| where Filehash == ""

```




### Behavioral
#### Description
A Detection in this Stage does not rely on any Artifact it is build on the Attackers intent -> the Goal of an  Attacker. This Stage is heavily inspired and build on the Capability Abstraction from [SpecterOps](https://specterops.io/blog/2020/02/06/capability-abstraction/). The primary idea is to research the attackers intent(what technical action must occur, regardless of tool or implementation) and find the smallest similarity all the Tools/Methods use. 

In german we would say  "Finde den kleinsten gemeinsamen nenner" -> "Find the lowest common denominator" 
#### Example



### Analytic
#### Description
The most mature detection stage. Where Behavioral detections know what bad looks like, Analytic detections know what normal looks like and flag everything that deviates from it. Rules at this stage incorporate statistical and mathematical methods built on top of your own telemetry. The environment itself becomes part of the detection logic. This makes the detection inherently adaptive to your tenant and significantly harder to evade, since an attacker would need to blend into your normal, not just avoid known-bad patterns. Not always achievable(missing telemetry,baseline-drifts and potential FP), but always worth striving for.

#### Example



