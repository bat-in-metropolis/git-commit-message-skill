# git-commit-message

A Claude Code skill that generates [Conventional Commits](https://www.conventionalcommits.org/) from your staged changes. Works across React, Node, Go, Python, Terraform, Docker, Kubernetes, and more.

Type `/git-commit-message` after staging files and get back a properly-formatted commit message with two alternates.

---

## Install (manual)

```bash
# Clone this repo anywhere
git clone git@github.com:bat-in-metropolis/git-commit-message-skill.git

# Copy the skill into your Claude Code skills directory
mkdir -p ~/.claude/skills
cp -r git-commit-message-skill/skills/git-commit-message ~/.claude/skills/
```

Restart your Claude Code session. The skill is now available globally.

> **Per-project install:** copy into `<your-project>/.claude/skills/` instead — the skill will only load when working inside that project.

---

## Usage

```bash
git add src/auth.ts
```

In your Claude Code session:

```
/git-commit-message
```

You can also trigger it naturally — phrases like `"commit message"`, `"suggest commit"`, or `"what should I commit"` work too.

### Example

Staged diff: a new password reset endpoint in `src/auth/controllers.ts`.

Output:
```
feat(auth): add password reset endpoint

- add POST /auth/reset-password route
- send reset link via email service
- expire token after 15 minutes

Alternates:
1. feat(api): add password reset flow for forgotten credentials
2. feat(auth): support self-service password reset via email
```

### Short mode

Ask for `"short"` or `"one line"` and get just the subject:
```
feat(auth): add password reset endpoint
```

---

## What it does well

- **Picks the right type** — distinguishes `fix` vs `refactor` vs `feat` using diff intent, not filenames
- **Infers scope from file paths** — `src/components/` → `ui`, `.github/workflows/` → `ci`, `*.tf` → `infra`, etc.
- **Flags breaking changes** — detects renamed exports, changed routes, removed env vars
- **Splits mixed commits** — suggests separating truly unrelated changes
- **Offers alternates** — always returns 2 alternate phrasings

See [skills/git-commit-message/SKILL.md](skills/git-commit-message/SKILL.md) for the full rules and [skills/git-commit-message/examples.md](skills/git-commit-message/examples.md) for per-stack examples.

---

## Token-efficient by design

Detailed per-stack examples live in `examples.md`, separate from the core rules in `SKILL.md`. Claude loads examples only when a diff is unusual enough that the rules alone don't disambiguate — most invocations stay lean (~4k tokens vs ~7k for a monolithic skill).

---

## License

MIT — see [LICENSE](LICENSE).
