# Example

Conversation: the user listed 10 tasks (3 easy, 4 medium, 3 hard) and ran `/SessionHandoff` with 3 sessions.

| Session | Difficulty | Tasks | Suggested model |
|---------|-----------|-------|-----------------|
| 1 | easy   | 3 | fast, cheap model |
| 2 | medium | 4 | mid-tier model |
| 3 | hard   | 3 | strongest model |

1st prompt (easy), saved to /home/jason/project/handoffs/session-1-easy.md

```
# Session 1/3 (easy): Docs and config cleanup

## Summary
...

## Tasks
1. ...

## Files
...

## Constraints
...

## Acceptance criteria
- ...

## Branch
handoff/session-1-easy, branched from main.

## Report back
...
```

2nd prompt (medium), saved to ...

3rd prompt (hard), saved to ...

Run order: sessions 1 and 2 can run in parallel; session 3 depends on session 2's branch.
