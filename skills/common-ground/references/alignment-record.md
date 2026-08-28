# Durable Alignment Record

Use a durable record only when the work crosses sessions or agents, will be handed off, or contains decisions that are expensive to reverse. Prefer updating an existing canonical issue, spec, plan, or decision record. Create a new `alignment.md` only when no suitable artifact exists.

The four unknown categories are a discovery aid, not the permanent shape of the record. Persist outcomes, evidence, decisions, assumptions, open gaps, and change rules.

```markdown
# <Work title>

## Outcome and current purpose

<What is being achieved, for whom, and what this phase must accomplish.>

## Acceptance boundary

### Accepted examples

- <A concrete behavior or outcome that should pass.>

### Rejected examples

- <A plausible but wrong interpretation that should fail.>

## Invariants and non-goals

- <Constraint that must remain true.>
- <Nearby work deliberately excluded.>

## Territory evidence

- <Fact> — <source path, test, command, document, or observation>

## Shared decisions

- <Decision> — <owner and short rationale>

## Assumptions and probes

| Assumption | Why safe enough now | Disconfirming signal | Check |
| --- | --- | --- | --- |
| <assumption> | <reason> | <what would prove it wrong> | <test, observation, or checkpoint> |

## Material gaps

| Gap | Owner | Next cheapest move | Blocks |
| --- | --- | --- | --- |
| <unresolved gap> | user / agent / evidence / third party | <question, inspection, prototype, or probe> | <decision or phase> |

## Deviation policy

- Continue and record when: <bounded conditions>.
- Stop and ask when: <material boundaries>.

## Verification gates

- <Observable check and when it runs.>
```

Keep the record current rather than appending contradictory snapshots. Use version control or the artifact's own history for chronology. Link to detailed evidence instead of copying it.
