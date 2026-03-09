# 001 Standard Rule File Type

Author: daten_krake
Date:   09.03.2026

## Status
approved

## Context
The framework is in need of a standardize file format for Rule/Analytics. This is required to be consistent in potential multi tenant deployments of the content. At the moment no standard format is existing. 

## Decision

YAML will be the standard file  format,even though this project is focusing on the microsoft security stack, due to the following reasons:

- YAML seems to be the de facto standard in Analytic/Signature sharing
- it is easier to read than JSON
- it has the capability for comments unlike JSON
- the build in feature of [Sentinel Repo](https://learn.microsoft.com/en-us/azure/sentinel/ci-cd-custom-content) is using YAML aswell


The Alternatives not chosen:
- JSON, has no ability to be commented and is harder to read in general
- terraform/opentofu, would be a great alternative but, a. not sure about terraform licensing and b. Microsoft is transitioning into the defender portal. There are no modules  yet to deploy content into Defender directly.
- TOML, no  experience using it and from what i know  there  is no established tooling in the Detection Engineering Community.
## Consequences

As i will not use the standard integration for content population(not stateful and  very  much manual work), i will be in need for custom tooling that is converting, the yet to come, standard layout of the rules into a deployable JSON.

The tool needs to convert the standard layout into deployable JSON that utilizes the Security Graph API/Azure Resource Manager(Sentinel). It needs to function with Sentinel and Defender.

Dependency: ADR 00x
