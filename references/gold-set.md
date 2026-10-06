# Grill PM gold set

Use this set to calibrate or regression-test the skill. It is not a mandatory response template and should not be loaded for ordinary reviews.

The cases and evaluation criteria are in English so they remain consistent with the skill instructions and can be used in automated evaluations. A response may translate the three canonical outcomes when answering a user in another language, but their meaning must remain the same.

## Evaluation rules

Evaluate only the ticket and context supplied in each case.

- Do not assume that missing evidence, strategy, priority, or success criteria exist elsewhere.
- Do not invent data, targets, customer claims, deadlines, obligations, or decisions.
- Judge the ticket's actual next step, not the eventual rollout.
- A complete implementation specification proves delivery readiness, not product justification.
- A good response need not repeat every fact. It must identify the one missing element that changes the next move.
- Wording does not need to match the expected answer. The outcome, pivotal reasoning, ownership, and next move do.
- Follow the response contract in `SKILL.md`: Verdict first, then Product case or Delivery case, followed by only the applicable gap, next-move, and PM-message sections. Translated headings are equivalent when their meaning and order are preserved.

For every new-feature case, the response should expose:

1. the problem worth solving and affected group,
2. available evidence and baseline,
3. the user or business outcome measure,
4. why the proposed next step is the cheapest credible way to learn or deliver value.

## Coverage map

| Case | Main behavior under test | Expected outcome |
|---|---|---|
| GS-00 | Complete, justified, measured product task | Proceed as scoped |
| GS-01 | Solution and acceptance criteria without a problem | Test or diagnose first |
| GS-02 | Claimed problem without prevalence evidence | Test or diagnose first |
| GS-03 | User friction without business relevance or why now | Test or diagnose first |
| GS-04 | Evidence without a chosen behavior or outcome | Clarify a missing decision |
| GS-05 | Unsupported causal link from solution to outcome | Test or diagnose first |
| GS-06 | Target without a behavioral baseline | Test or diagnose first |
| GS-07 | Feature-usage proxy presented as customer value | Test or diagnose first |
| GS-08 | Broad rollout without a meaningful guardrail | Test or diagnose first |
| GS-09 | Consequential product policy has no owner | Clarify a missing decision |
| GS-10 | Ticket already proposes the missing diagnosis | Proceed as scoped |
| GS-11 | Small measured test despite incomplete causality | Proceed as scoped |
| GS-12 | Urgent regression repair | Proceed as scoped |
| GS-13 | Explicit compliance obligation | Proceed as scoped |
| GS-14 | Material problem but expensive untested solution | Test or diagnose first |

## GS-00 — ideal product task

### Ticket

**FleetFox: reduce the time needed to prepare a list of vehicles due for inspection**

Managers of fleets with more than 200 vehicles prepare a weekly list of vehicles due for inspection within the next 14 days. The current vehicle list supports search only by vehicle name and registration number.

In the last 30 days, 168 of 420 active large-fleet managers exported the vehicle list to CSV within five minutes of opening the view. In a sample of 60 sessions, the median time from opening the list to creating a service order was 4 minutes 20 seconds. In 11 of 15 interviews, managers described manually filtering a spreadsheet by branch, vehicle status, and inspection date. Customer Success estimates that manual list preparation costs customers in this segment about 90 hours per week in total. Reducing service-planning time is one of this quarter's product goals for enterprise customers.

We hypothesize that combinable filters for branch, status, vehicle type, and inspection date will let managers prepare the list without exporting data. We will first release the filters behind a feature flag to 20 large-fleet managers for two weeks. Filter state must be saved in the URL, and an empty result must offer a way to clear all criteria.

Pilot success criteria:

- median time from opening the list to creating a service order falls from 4 minutes 20 seconds to less than 2 minutes,
- the share of sessions containing a CSV export in this flow falls from 40% to less than 25%,
- correctly identified vehicles in the controlled task do not fall below the current 98%,
- list-response p95 does not regress by more than 200 ms.

If both primary criteria are met without violating the guardrails, expand the rollout. If completion time does not improve and users continue to export CSV, return to session evidence and investigate missing data or operations. This task does not change the rules for calculating the next inspection date.

### Expected evaluation

**Outcome:** Proceed as scoped.

The next step is a bounded, reversible, measured pilot. The ticket identifies the affected segment, quantifies the behavior and cost, connects the problem to a current product goal, states a causal hypothesis, defines outcome metrics and guardrails, and includes a decision rule.

**Must recognize:** the pilot, not a full rollout, is being approved. The CSV rate is supporting behavior; time to create a service order and correct vehicle selection are closer to customer value.

**Must not:** demand another generic discovery phase, relabel the existing pilot as a new recommendation, or claim that the supplied data was independently verified.

## Reusable shape of a strong task

This is a shape, not a form that every bug or obligation must fill.

```markdown
# [Problem-oriented title]

## Problem and affected group
Who cannot do what today? What consequence follows?

## Evidence and baseline
Population, denominator, current behavior or performance, affected segments, and qualitative evidence explaining why.

## Business relevance / why now
Revenue, cost, retention, activation, risk, obligation, strategic learning, or another concrete reason to spend capacity now.

## Hypothesis
Why should the proposed change affect the target behavior or outcome?

## Scoped next step
Diagnosis, prototype, pilot, experiment, implementation, or rollout appropriate to current uncertainty.

## Outcome and guardrails
Baseline, target, evaluation window, customer or business outcome, and metrics that must not regress.

## Decision rule
What result causes the team to continue, change direction, stop, or roll back?

## Constraints and owned decisions
Real boundaries, named pre-implementation gates, and the owner of any policy or priority choice.
```

## GS-01 — implementation-ready solution, no problem

### Ticket

**FleetFox: add filters to the vehicle list**

Add filters for branch, status, vehicle type, and inspection date. Filters work together, persist in the URL, and update the list without a page reload. An empty result shows a “Clear filters” button. Release the feature behind a flag to 20 customers, then enable it for everyone after two weeks if there are no errors and list-response p95 has not regressed by more than 200 ms.

### Expected evaluation

**Outcome:** Test or diagnose first.

The ticket is delivery-ready but contains no user problem, affected population, evidence, business relevance, behavioral baseline, or value outcome. Error rate and latency only prove that the feature works technically.

**Cheapest next step:** inspect current list usage, exports, support requests, and a small sample of sessions to identify the job users cannot complete and its scale. That evidence determines whether filters deserve capacity and what should be measured.

**Fail if:** the response says to proceed because the specification is clear, the change is reversible, or the need may have been validated elsewhere.

## GS-02 — problem claim without evidence of prevalence

### Ticket

**FleetFox: large-fleet managers waste time finding vehicles due for inspection**

Managers of fleets with more than 200 vehicles say that manually finding vehicles due for inspection is frustrating and delays service planning. We want to add combinable filters for branch, status, vehicle type, and inspection date. The goal is to reduce list-preparation time by 50% without reducing result correctness or degrading list-response time. We will first release the feature to 20 managers.

### Expected evaluation

**Outcome:** Test or diagnose first.

The group and intended outcome are stated, but the ticket does not show how common or costly the problem is, how long the task takes now, or where users struggle. “Managers say” is a discovery signal, not prevalence evidence, and a 50% reduction cannot be evaluated without a baseline.

**Cheapest next step:** measure the current task time and frequency for the target segment, inspect exports or workarounds, and sample relevant sessions or support cases. Use the result to decide whether to build and to set a target.

**Fail if:** the response treats the qualitative claim as proof that the broad problem is material.

## GS-03 — user friction without business relevance or why now

### Ticket

**FleetFox: reduce the time needed to prepare a list of vehicles due for inspection**

Among 420 active large-fleet managers, 168 export the list to CSV before planning service. In a sample of 60 sessions, median list-preparation time was 4 minutes 20 seconds. In 11 of 15 interviews, managers described manually filtering a spreadsheet. We want to test filters on 20 accounts and bring the median below 2 minutes without reducing result correctness or degrading response time.

The team has not stated what cost, risk, retention impact, or strategic goal justifies addressing this problem now instead of other roadmap items.

### Expected evaluation

**Outcome:** Test or diagnose first.

The user friction and baseline are credible enough for a bounded investigation, but the priority claim is missing. The skill must not invent revenue or retention impact.

**Cheapest next step:** quantify the operational cost or connect the problem to an explicit product goal, renewal risk, or other real priority. The PM owns the priority trade-off after the facts are gathered.

**Fail if:** the response silently equates frequent friction with business priority or manufactures a commercial impact.

## GS-04 — no chosen behavior or outcome

### Ticket

**FleetFox: improve service planning for large fleets**

In the last 30 days, 168 of 420 large-fleet managers exported the list to CSV. Preparing the list takes a median of 4 minutes 20 seconds, and customers spend about 90 hours per week on this process. Reducing service-planning time is an enterprise product goal for this quarter.

We want to add filters for branch, status, vehicle type, and inspection date. After release, we will evaluate whether the solution is successful. We have not decided whether task-completion time, elimination of exports, number of correctly planned inspections, or user satisfaction is the primary outcome.

### Expected evaluation

**Outcome:** Clarify a missing decision.

The problem, evidence, and business relevance exist, but the team has no primary outcome. That choice controls instrumentation, target, test length, and whether the solution is judged successful.

**Owner and recommendation:** the PM or accountable product team should choose time to complete a correct service plan as the primary outcome, with correctness as a guardrail; exports can remain diagnostic.

**Fail if:** the response chooses a product goal silently, proposes implementation without a success definition, or asks engineering to own the priority trade-off.

## GS-05 — solution has no credible causal link

### Ticket

**FleetFox: reduce service-planning time with a new dashboard**

Large-fleet managers need a median of 4 minutes 20 seconds to find vehicles due for inspection and create a service order. Spreadsheet export occurs in 40% of these sessions, and the problem costs customers about 90 hours per week. The goal is to bring the median below 2 minutes without reducing correctness.

Build a dashboard with a pie chart showing the share of vehicles by make and a chart showing the number of vehicles in each branch. Release it to all enterprise customers. The ticket does not explain how aggregates by vehicle make and branch will help identify specific vehicles due for inspection.

### Expected evaluation

**Outcome:** Test or diagnose first.

The problem is material and measured, but the proposed solution does not follow from the job users need to perform. A dashboard may attract views without shortening planning.

**Cheapest next step:** prototype the workflow with target users or test alternative ways of producing the service list. Measure time and correctness, not dashboard views.

**Fail if:** the response approves the dashboard because the problem itself is well evidenced.

## GS-06 — target without baseline

### Ticket

**FleetFox: inspection filters for large fleets**

Of 420 large-fleet managers, 168 export the list to CSV before planning service. Customer Success estimates that the manual work is a material cost for enterprise customers and ties it to this quarter's goal of reducing planning time.

We will test combinable filters on 20 accounts. Success means reducing time to create a service order by 50% without reducing result correctness or degrading response time. We do not currently measure time from opening the list to creating an order and do not know how that time differs between segments.

### Expected evaluation

**Outcome:** Test or diagnose first.

The ticket cannot interpret a 50% target or size the opportunity without the current distribution. The missing baseline can be obtained cheaply before the pilot.

**Cheapest next step:** instrument the flow and collect a baseline for the target segment, including variance and relevant subgroups. Then set a target and start the pilot.

**Fail if:** the response accepts the relative target as measurable without current measurement.

## GS-07 — weak proxy presented as value

### Ticket

**FleetFox: increase use of vehicle-list filters**

Large-fleet managers need a median of 4 minutes 20 seconds to prepare a list of vehicles due for inspection. The manual process costs customers about 90 hours per week. We will add filters for branch, status, vehicle type, and inspection date to 20 accounts.

Success means at least 60% of pilot participants use one or more filters and sessions average three filter clicks. We will not measure task-completion time, list correctness, or service orders created.

### Expected evaluation

**Outcome:** Test or diagnose first.

Filter usage shows discoverability or adoption, not whether planning became faster or more accurate. Three clicks may even signal confusion.

**Required correction:** measure successful completion time and correctness, with filter usage as diagnostic telemetry. Define a keep/change/stop rule using the value outcome.

**Fail if:** the response treats clicks or adoption as sufficient proof of customer value.

## GS-08 — broad rollout without guardrails

### Ticket

**FleetFox: release filters to all enterprise customers**

A pilot on 20 accounts reduced median time to create a service order from 4 minutes 20 seconds to 1 minute 45 seconds and reduced exports from 40% to 22%. Correctness was manually checked on five accounts. Enable the filters for all 3,800 enterprise customers in a single rollout.

Filter queries use a new database path. The ticket does not specify acceptable response time, error rate, result consistency, or a rollback plan.

### Expected evaluation

**Outcome:** Test or diagnose first.

The value hypothesis has support, but a one-step rollout exposes all enterprise customers to correctness and performance risk not covered by the small manual check.

**Cheapest next step:** staged rollout with automated result-consistency checks, latency and error guardrails, and a rollback threshold. This tests scale risk; it does not re-open whether the feature has user value.

**Fail if:** the response asks for generic product discovery or approves the broad rollout solely because the pilot hit its value metrics.

## GS-09 — consequential product policy without an owner

### Ticket

**FleetFox: filters for vehicles due for inspection**

The problem, baseline, business relevance, hypothesis, pilot, outcome metrics, and performance guardrails are the same as in GS-00.

The team has not decided how the “inspection due within 14 days” filter should handle vehicles without a recorded next-inspection date. Excluding them could hide vehicles that require action; including them automatically could flood the result with incomplete records. The ticket does not name an owner for this decision or a step at which it will be made.

### Expected evaluation

**Outcome:** Clarify a missing decision.

The policy affects safety, user trust, result semantics, and measurement. Engineering should not decide it silently.

**Owner and recommendation:** the PM owns the product behavior with input from domain or compliance specialists. Prefer a separate, visible, and measurable “missing date” state rather than silently including or excluding records.

**Fail if:** the response treats this as a routine implementation detail or blocks on unrelated solution questions.

## GS-10 — diagnosis is already the next step

### Ticket

**FleetFox: investigate why managers export the vehicle list**

In the last 30 days, 168 of 420 large-fleet managers exported the vehicle list to CSV within five minutes of opening the view. We do not know whether they are preparing an inspection list, reporting to a supervisor, moving data to another system, or completing another task.

This task does not build filters. Add measurement for the sequence list opened → export → next action, review 30 sessions containing an export, and interview five managers representing different fleet sizes. The deliverable is a breakdown of the main jobs, their frequency in the behavioral data, and a recommendation to improve the workflow in FleetFox, improve export, or not invest. We will decide on a solution after this step.

### Expected evaluation

**Outcome:** Proceed as scoped.

The ticket admits what is unknown and proposes a bounded diagnosis that will decide whether and what to build. Lack of a solution metric does not block this discovery task; the deliverable and decision gate are appropriate to the current uncertainty.

**Fail if:** the response recommends “diagnose first” as though that were not already the scoped next step, or demands a production outcome target before observing the job.

## GS-11 — measured test with incomplete causal diagnosis

### Ticket

**FleetFox: pilot filters for inspection planning**

Large-fleet managers need a median of 4 minutes 20 seconds to create a service order, and 40% of those sessions include a CSV export. We do not know whether the main problem is missing filters, incomplete data, or the need to share the list.

Filters can be released behind a feature flag in three days. We will make them available to 20 managers for two weeks. Hypothesis: if manually narrowing the list is the main obstacle, median completion time will fall below 2 minutes and exports below 25%. Guardrails: correctness of at least 98% and no p95 regression greater than 200 ms. If time does not improve, we will not expand the rollout and will analyze sessions for incomplete data and sharing needs.

### Expected evaluation

**Outcome:** Proceed as scoped.

The causal diagnosis is incomplete, but the change is cheap, reversible, falsifiable, measured against a baseline, and guarded. The result directly informs whether to keep the feature or investigate another cause.

**Fail if:** the response blocks the pilot until the team proves the single root cause, or endorses a later broad rollout in advance.

## GS-12 — urgent regression repair

### Ticket

**FleetFox: the inspection filter hides overdue vehicles after a time-zone change**

Since version 4.18, the “due for inspection” filter has compared the UTC date with the branch's local date. Between local midnight and UTC midnight, some overdue vehicles disappear from the result. We reproduced the bug for UTC+2 and UTC+8 branches; the previous version displays those vehicles correctly.

Restore comparison using the branch's time zone, add tests for day boundaries, and release the fix behind a flag. Roll out to 5% first, then 100% if the error rate does not increase for one hour and result comparison against the stable version shows no differences beyond the repaired case.

### Expected evaluation

**Outcome:** Proceed as scoped.

This restores documented behavior with reproduction evidence and a safe verification path. Do not delay the repair to demand a product hypothesis, revenue metric, or customer interviews.

**May note:** investigate how the regression escaped after the repair, without making that a precondition for restoring correct behavior.

## GS-13 — explicit obligation

### Ticket

**FleetFox: record vehicle-data exports in the audit log**

A signed addendum with a public-sector customer requires every data export from December 1 onward to create an audit-log entry containing the user ID, timestamp, record scope, and file type. Without this capability, the customer cannot launch. Legal and Security have approved the requirement and entry format.

Add an audit entry for CSV and XLSX exports. An entry must also be written when file generation fails, with the appropriate success status. Do not store the export contents. The acceptance test compares the audit log with the set of exports performed in the test environment. Deployment must be complete by November 20.

### Expected evaluation

**Outcome:** Proceed as scoped.

The obligation, owner approvals, deadline, acceptance condition, and data-minimization constraint are explicit. Do not manufacture an experiment or ask for prevalence evidence.

**May check:** implementation security and failure semantics. These are delivery concerns, not reasons to question the product rationale.

## GS-14 — material problem, expensive untested solution

### Ticket

**FleetFox: build an automated service planner**

Large-fleet managers spend about 90 hours per week preparing lists of vehicles due for inspection. The median time for one task is 4 minutes 20 seconds, and 40% of sessions end with a spreadsheet export. Reducing service-planning time is an enterprise product goal.

Build a new planner that automatically selects vehicles, assigns a service shop, books a time slot, and notifies the driver. The solution must replace the current workflow for all enterprise customers. We have not tested whether customers want automatic selection, which exceptions they handle manually, or whether service shops provide reliable availability.

### Expected evaluation

**Outcome:** Test or diagnose first.

The problem is material, but the proposed solution multiplies untested assumptions, integrations, policy choices, and rollout exposure. Strong problem evidence does not validate this solution.

**Cheapest next step:** observe exception handling, prototype recommendations without automatic booking, or run a Wizard of Oz pilot in which a human prepares suggestions. Measure accepted recommendations, corrected fields, task time, and missed constraints. State that this teaches whether assisted planning is useful; it does not yet validate full automation or service-shop integration.

**Fail if:** the response approves the build because the problem is large, or restarts generic problem discovery instead of targeting solution risk.

## Regression scoring

A run passes a case when it:

1. chooses the expected outcome or a genuinely equivalent next move,
2. identifies the isolated missing or satisfied element,
3. proposes a proportionate next step and says what decision it unlocks,
4. does not invent evidence or assume validation elsewhere,
5. does not block an already appropriate diagnosis, measured test, urgent repair, or explicit obligation,
6. follows the response contract without adding empty or generic sections.

A run fails a case when it:

- endorses implementation because acceptance criteria are detailed while product justification is absent,
- treats feature usage as customer or business value without naming the gap,
- asks for discovery that the ticket already scopes,
- demands product experimentation for a repair or obligation,
- lets engineering silently own a product policy or priority decision,
- asks broad generic questions instead of the one answer that changes the next move,
- changes the section order, omits an applicable contract section, or fills an inapplicable section with placeholder text.
