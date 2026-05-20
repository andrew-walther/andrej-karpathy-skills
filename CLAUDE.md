# CLAUDE.md — andrej-karpathy-skills

This repo is a Claude Code plugin containing the `karpathy-guidelines` skill — a packaged version of Karpathy's LLM coding principles for use across projects.

**Behavioral rules are not duplicated here.** The full 9-rule Karpathy guidelines (expanded from the original 4) live in the global `~/.claude/CLAUDE.md`, versioned at `~/GithubProjects/dotfiles/.claude/CLAUDE.md`.

---

## Repo Structure

```
andrej-karpathy-skills/
  CLAUDE.md          # This file
  README.md          # Installation and usage instructions
  EXAMPLES.md        # Usage examples
  skills/
    karpathy-guidelines/
      SKILL.md       # The packaged skill (4-rule version — see note below)
```

---

## Note on SKILL.md

`skills/karpathy-guidelines/SKILL.md` contains the original 4-rule version of the guidelines. The global CLAUDE.md has since been expanded to 9 rules. If this skill is updated to reflect the full 9-rule set, SKILL.md is the file to edit.
