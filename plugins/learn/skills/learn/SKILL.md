---
name: learn
description: Review this session and save corrections, preferences, decisions and references to auto-memory.
disable-model-invocation: true
argument-hint: "[optional note about what to focus on]"
---

# Learn

Review the current session and write anything worth keeping to the auto-memory system. Run this at the end of a session or at any point when the conversation has surfaced something worth remembering.

You may also write a single `feedback` memory immediately, without waiting to be invoked, the moment the user corrects your approach. Corrections given early in a long session are lost to compaction before anyone runs this skill.

## What to look for

Go through the conversation from the beginning. For each exchange, ask whether it produced one of these:

**Feedback (corrections and confirmations)**
- The user corrected your approach: "no", "don't do that", "stop doing X", "use Y instead"
- The user confirmed a non-obvious approach worked: "yes exactly", "perfect", accepted an unusual choice without pushback
- Save both. Corrections are easy to spot; confirmations are quieter but equally useful.

**User context**
- The user's role, expertise level, team, or domain knowledge
- Stated preferences about how to collaborate ("keep it terse", "always ask before pushing")
- Things to avoid that aren't already obvious from the code
- Constraints of the form "X is not possible here" — always with the date and the evidence, worded so a future session re-tests instead of assuming. Left undated, these are the memories most likely to be wrong and least likely to be questioned.

**Project context**
- Decisions and the reason behind them (not just what was decided, but why)
- Deadlines or constraints that affect future suggestions
- Architectural choices that would otherwise need re-explaining
- Ongoing work or initiatives the user mentioned — keep the mechanism and the reason as prose, and confine anything that can change (ticket, PR, deploy state) to a single trailing block: `**Status (as of YYYY-MM-DD, re-verify before quoting):** …`. Never let a status snapshot be the whole memory.

**References**
- External systems and where to find things in them (Linear project names, Grafana dashboards, Slack channels, Confluence spaces)

## What NOT to save

Skip anything that can be derived by reading the current files or running a git command:
- Code patterns, file paths, function names (check the code instead)
- Who changed what (git log or git blame)
- Fix recipes (the fix is already in the code)
- Anything already in a CLAUDE.md file
- Ephemeral details only relevant to this session's task

## Steps

1. **Read the index.** Open `MEMORY.md` in the auto-memory directory. If it does not exist, you will create it.

2. **List candidates.** Go through the session and write one bullet per candidate with its type and a one-line summary. Do not write any file yet.

   If the user passed a note in `$ARGUMENTS`, use it to narrow the sweep. For example "focus on the Terraform discussion" or "only save corrections".

3. **Deduplicate.** For each candidate, check the index. If an existing memory covers the topic, read it and decide whether to update it or skip the candidate. Never create a second file for a topic that already has one. Updating means *reconciling*: delete the lines this session superseded, so a file never holds two generations of the same claim.

4. **Write.** Create or update the memory files and the index entries.

   Name each file `<type>_<snake_case_slug>.md`, so the type is visible without opening it. Do not mix the three forms: the filename is `snake_case`, while the `name:` slug and every `[[link]]` are `hyphen-case`. `feedback_close_idle_agents.md` carries `name: feedback-close-idle-agents` and is linked as `[[feedback-close-idle-agents]]` — a hyphen/underscore mismatch breaks recall silently.

   Keep each file under 4 KB. If one goes over, split out the distinct fact or re-summarise the file back down in this same pass — never append and move on.

5. **Report.** One line per saved or updated item, with its type and summary.

   "Nothing worth keeping this session" is a valid outcome — say so plainly and write nothing.

6. **Prune, then check the budget.** Delete the memories this session proved wrong, and the ones describing completed work with no forward value — the file *and* its index line. Then, if `MEMORY.md` is over ~120 entries or ~15 KB, say so and recommend a consolidation pass. Do not start one inside a capture pass.
