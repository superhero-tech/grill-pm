# Grill PM

`grill-pm` pressure-tests engineering tasks, bugs, PRDs, and product proposals before a team commits to the wrong next step.

It helps an engineer become a constructive product partner rather than a passive ticket recipient or a judge of the PM. The skill separates two questions that are often conflated:

- **Delivery readiness:** can the team tell what to build?
- **Product justification:** is there a material problem, evidence proportionate to the investment, and a result the team can evaluate?

Detailed acceptance criteria answer only the first question.

## What it does

The skill reviews the task's actual next step: investigation, policy decision, prototype, pilot, implementation, rollout, or repair. It then leads with one of three outcomes:

- **Proceed as scoped** — the next step is justified and proportionate to the evidence.
- **Test or diagnose first** — a cheaper observation or experiment could change the decision.
- **Clarify a missing decision** — a consequential choice has no owner or resolution path.

For new product functionality, the review makes four things explicit:

1. the problem worth solving and the affected group,
2. the available evidence and behavioral baseline,
3. the user or business outcome that should change,
4. why the recommended next step is the cheapest credible way to learn or deliver value.

It does not force product discovery onto an urgent regression, a compliance obligation, or enabling work with an established dependency. It also does not invent missing metrics or assume that a product decision was validated somewhere outside the ticket.

## Response format

Reviews use a stable structure:

```text
Verdict
Product case (or Delivery case for bugs and obligations)
Critical gap, when one exists
Recommended next move
Question or message to PM, when one is needed
```

The message to the PM states what is known, what is assumed, why it matters, and the proposed move. The goal is to unblock a sharper decision, not to manufacture objections.

## Install

Install with [skills.sh](https://skills.sh):

```bash
npx skills@latest add superhero-tech/grill-pm
```

Add `--global` to make the skill available across projects.

For a manual Codex installation:

```bash
git clone https://github.com/superhero-tech/grill-pm.git ~/.codex/skills/grill-pm
```

Start a new agent session after installation so the skill can be discovered.

## Use

Invoke it explicitly when reviewing a task:

```text
$grill-pm Review this task and tell me whether engineering should proceed, test something first, or ask for a product decision.
```

The skill responds in the user's language.

## Evaluation set

[`references/gold-set.md`](references/gold-set.md) contains 15 regression cases. They cover a complete product task, missing problem evidence, missing business relevance, weak proxy metrics, absent guardrails, unowned decisions, an already-correct discovery task, a measured pilot, an urgent bug, a compliance obligation, and an expensive untested solution.

Each case defines the expected verdict, pivotal reasoning, next move, and failure conditions. The set is for calibration and regression testing; it is not loaded during ordinary reviews.

## Repository structure

```text
.
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- references/
|   `-- gold-set.md
`-- README.md
```

## License

MIT. See [LICENSE](LICENSE).

