---
parent: policies
layout: ops
layout: docs
sidenav: true
title: Security Incident Response checklist
linktitle: Security IR checklist
---

*This is a short, actionable checklist for the Incident Commander (IC) to follow during incident response. It's a companion to the [IR guide]({{ site.baseurl }}{% link _docs/ops/security-ir.md %}), where you can find the full details of each step.*

You're the first cloud.gov team member to notice a non-team-member's report of a possible security incident regarding cloud.gov, or you've noticed an unreported possible security incident yourself. Congratulations, you're now the Incident Commander (IC)! Follow these steps:

## Initiate

- **follow the the [18F security incident response process](https://handbook.18f.gov/security-incidents/)**.
  - At step 6 ("If the incident involves cloud.gov"), notify the rest of the cloud.gov team in [`#cloud-gov`](https://gsa-tts.slack.com/messages/cloud-gov/) using `@cg-team`.

## Assess

- Confirm the incident — was it a real incident?
    - If it's expected behavior, go to [False Alarm](#false-alarm).
    - If it's unexpected behavior, it is a real incident even if it may not be cloud.gov's responsibility.
- Assess the severity, using [the rubric in the IR guide]({{ site.baseurl }}{% link _docs/ops/security-ir.md %}#incident-severities).
- Update the GitHub issue:
    - Status → "confirmed"
    - Severity → high/medium/low
    - List of responders
- Assess whether to also activate the [contingency plan]({{ site.baseurl }}{% link _docs/ops/contingency-plan.md %}).
- Send an initial situation report (“sitrep”) ([example sitrep]({{ site.baseurl }}{% link _docs/ops/security-ir.md %}#assess)) to:
    - Post in [`#incident-response`](https://gsa-tts.slack.com/messages/incident-response/)
    - Email to `gsa-ir@gsa.gov` and `devops@gsa.gov`
    - Email/Slack other stakeholders, if applicable

## Remediate

- You may not be able to "walk backwards" from the observed behavior to the root cause.
  - Consider the things that must be true for the behavior to occur, and test those hypotheses against the information that
  is available to you.
- Keep the ticket/docs updated as people work, tracking:
    - Leads, and who's following them
    - Remediation items, and who's working on them, including customer notification (if appropriate to the situation)
- Send out sitreps on a regular cadence (high: hourly; medium: 2x daily; low: daily).
- Go into work shifts if the incident lasts longer then 3 hours.
- [Hand off IC](#handing-off-ic) if the incident lasts longer than 3 hours.

Once the incident is resolved:

- Update the ticket, set status → "resolved".
- Send a final sitrep to stakeholders.
- Schedule a retrospective.
- Thank everyone involved for their service!

## Special Situations

Extra checklists for special situations that don't always occur during incidents:

### False Alarm

Follow this checklist if an event turns out not to be a security incident:

- Update the GitHub issue, setting status to `false alarm`.
- Close the GitHub issue.
- Notify `gsa-ir@gsa.gov` of the false alarm.
- If any sitreps have been sent out, send a final sitrep to all previous recipients, noting the false alarm.

### Handing off IC

Follow this checklist if you need to hand over IC duties:

- Old IC: brief New IC on the situation.
- New IC: confirm that you're taking over.
- New IC: update GitHub issue, noting that you're now the IC.
- New IC: send out a sitrep, noting that you're taking over IC.
- Old IC: stick around for 15-20 minutes to ensure a smooth handoff, then log off!

### Network Interconnect

If a cloud.gov team member or automated scanning system detects unauthorized access or traffic across a secure VPN / interconnection with a customer:

- Invite customer team contacts (such as Org Managers and System Owner) to the call
- Confirm whether traffic should be terminated or captured
- If traffic should be terminated: from the Amazon AWS console select `Services -> VPC -> Virtual Private Gateways -> VPN ID -> Detach from VPC`
- If traffic should be captured:
  - VPC Flow Logs: from the Amazon AWS console select `Services -> VPC -> VPC ID -> Flow Logs`
  - Live capture: from the Isolation Segment Diego Cell run `tcpdump -i $INTERFACE -s 65535 -w /tmp/incident-$(date +%s).pcap`
  - Customer: the customer has control of all systems on the customer side of the VPN, so the customer needs to capture that traffic

### Github Secret Leak

If we've leaked secrets in Github, _once the Incident Response team has told us to remove the data from Github_, follow [these instructions to remove the secret from Git history](https://help.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository), and then file a [support ticket to have the files removed from their cache](https://support.github.com/contact).

---

### Page information

* Last modified on: {% last_modified_at %}
* [Recent document history](https://github.com/cloud-gov/cg-site/commits/main/{{ page.path }}) (since 2022-11-08)
* [Older document history](https://github.com/cloud-gov/cg-site/commits/master/{{ page.path }}) (from 2020-02-05 to 2022-11-08)
* [Much older document history](https://github.com/cloud-gov/cg-site/commits/master/content/docs/ops/{{ page.slug }}.md) (before 2020-02-05)
