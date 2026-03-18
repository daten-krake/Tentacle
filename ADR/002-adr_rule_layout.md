# 002 Rule Layout

Author:   daten_krake 
Date:     18.03.2026

## Status
open

## Context
In ADR001 the standard file format was approved for yaml. But there is no standard layout of the rules/documentation. This is needed for consitent deployments and readability of the content. 

## Decision
The Structure is aligned with the [ADS](https://blog.palantir.com/alerting-and-detection-strategy-framework-52dc33722df2) from Palantir and FalconForce [FalconForge](https://github.com/FalconForceTeam/FalconForge/blob/main/usecases/0xFF-0239-Discovery_Commands_Executed_from_Instance_Profile-AWS/usecase.yml) but a bit simplified for the start.
The Goal is to have a consistent, human-readable schema that covers all aspects of the different deployment locations(Sentinel/Defender XDR)



The general structure should look like this:


```yaml
id: ""
name: ""
severity: ""
fp_rate: ""
stage: ""
status: ""
permission_required: ""
mitre:
    - tactics:
        - ""
        - ""
      techniques:
        - ""
        - ""
data_sources: []
tags: []
os_family: []
description: ""
technical_description: ""
considerations: ""
false_positives: ""
blindspots: ""
response_plan: ""
references: []
entity_mapping: []
query_frequency: ""
query_period: ""
query: ""

```

## Consequences
- Due to the simplified Version of this fist draft revision will be required. 
- Schema validation process will be added in the CI pipeline.
- This only works with microsoft Sentinel atm.
- Some fields are not in the yaml structure, but are required for deployments, this needs to be adjusted and further elaborated in another ADR.
