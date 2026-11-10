# codelaw-pre-commit

[codelaw](https://github.com/arpitarya/codelaw)'s hooks for the
[pre-commit](https://pre-commit.com) framework. The framework installs codelaw
from PyPI at the tag's version into a virtualenv of its own — no Rust build,
nothing on `PATH`.

```yaml
repos:
  - repo: https://github.com/arpitarya/codelaw-pre-commit
    rev: v0.5.1
    hooks:
      - id: codelaw-fix
      - id: codelaw-format
      - id: codelaw-check
```

| hook | runs | blocks the commit when |
|---|---|---|
| `codelaw-check` | `codelaw check --staged` on the staged files | a finding is an error |
| `codelaw-fix` | `codelaw fix --staged` — the safe (auto) fixes | it changed a file (re-stage, commit again) |
| `codelaw-format` | `codelaw format` on the staged files | it changed a file (re-stage, commit again) |

**The tag is the version:** `rev: v0.5.1` installs `codelaw==0.4.3`. A new
codelaw release reaches this repository within a day: `.github/workflows/bump.yml`
reads PyPI's latest version, rewrites the pin, commits and pushes the matching
tag. `pre-commit autoupdate` then moves your `rev`.

Rule packs come from your project's own dependencies (`codelaw.toml`'s
`extends`), as with any codelaw run. If codelaw is already installed — npm or
pip — the `language: system` hooks in the main repository run that copy
instead: `repo: https://github.com/arpitarya/codelaw`. See codelaw's
[USAGE](https://github.com/arpitarya/codelaw/blob/main/USAGE.md#without-ai-editor-pre-commit-ci).

MIT licensed, like codelaw.
