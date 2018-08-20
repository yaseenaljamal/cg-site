---
menu:
  docs:
    parent: policies
layout: ops

title: Component Health Scorecard
---

# Engineering Health Scorecard
The Engineering Health Scorecard is used to assess component health, quality and team delivery.

## Under what circumstances should a assessment be performed?
1. Customers consider it a outage if this software fails
1. Operators are unable to perform their duties if this software fails
1. Software is > 500 lines of code
1. Product team requires functionality to generate sales / maintain renewals

## Scorecard

|Factor|Description|
|------|-----------|
|**Continuously Deployed**|Deployed through a CI pipeline, and the libraries required to build the component are specified as inputs.  Once build the artifact is tested through **smoke** and **acceptance** tests prior to production rollout|
|**Source Control**|Stored in a source control repository with master branch protection and required peer reviews|
|**Error Checking**|Handles errors such as lack of network connection, missing dependencies, dependent software errors|
|**Testing**|Test suite provides **smoke** and **acceptance** tests and exercises critical functionality|
|**Upstream**|Code is part of a active upstream project and modifications which are submitted are likely to be accepted|
|**Monitoring**|Once deployed there are Key Performance Indicators to understand if the service is functioning as expected and alerts for critical functionality|

## Scores
|Score|Description|
|-----|-----------|
|**None**|Not implemented|
|**Low**|Initial idea is present but does not meet criteria|
|**Medium**|Some portions are working|
|**High**|Majority of functionality implemented|
|**Exception**|This functionality is not valuable or not feasible|

## Shell Script Example
|Factor|Score|Exception|Notes|
|------|-----|---------|-----|
|**Continuously Deployed**|Medium|No|Dependencies are not specified|
|**Source Control**|High|No||
|**Error Checking**|Low|No|Returns success when networking not present|
|**Testing**|None|No|No tests provided|
|**Upstream**|None|Yes|Integration code, no open source alternative available|
|**Monitoring**|None|Yes|Script does not run continuously|

## Analyzing the Results
|Risk|Description|
|-|-|
|**Low**|Software has no scores of `None` or `Low` without **Exception**|
|**Medium**|Software has one component with `None` or `Low` but has planned work to remediate|
|**High**|Software has two or more components with `None` or `Low`, or no planned work to remediate|

## Corrective Actions
When a software project is found to be at **medium** or **high** risk the following actions should be taken:
1. **Analyze:**  Why were these not implemented originally?  Time? Scope? Knowledge? Feasibility?  Does it qualify for a exception?
1. **Plan:** Create a card to remediate missing functionality
1. **Implement:** Develop and commit functionality, perform reasonable effort to merge changes upstream
