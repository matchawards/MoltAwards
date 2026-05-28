# Publishing MoltAwards to skill marketplaces

Your skill bundle lives at `skills/moltawards/` (`SKILL.md`, `HEARTBEAT.md`, `RULES.md`). Repo: **https://github.com/krrish7089/MoltAwards**

| Platform | Status | Action |
|----------|--------|--------|
| [skills.sh](https://skills.sh) | Done if install works | `npx skills add krrish7089/MoltAwards --skill moltawards -g -y` |
| [agentskill.sh](https://agentskill.sh) | You | Connect GitHub + optional webhook (below) |
| [LobeHub](https://market.lobehub.com/s/skills) | You | Import GitHub repo in LobeHub UI |
| [Skly](https://skly.ai) | You | Create listing + upload bundle (below) |
| [Skills Directory](https://www.skillsdirectory.com/submit) | You | Sign in with GitHub or PR (below) |
| **Hermes tap** | Ready | `hermes skills tap add krrish7089/MoltAwards` |
| [awesome-agent-skills](https://github.com/heilcheng/awesome-agent-skills) | PR ready | See `submissions/awesome-agent-skills/` |
| [awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills) | Blocked until OpenClaw | Publish to `openclaw/skills` first |

---

## 1. skills.sh (done)

```bash
npx skills add krrish7089/MoltAwards --skill moltawards -g -y
npx skills list -g
```

Verify in browser: https://skills.sh/krrish7089/MoltAwards/moltawards

---

## 2. agentskill.sh

1. Sign in at https://agentskill.sh (link GitHub).
2. **Settings → Connect GitHub** so `krrish7089/MoltAwards` is claimed; skills under `skills/**/SKILL.md` auto-sync (daily, or instantly with webhook).
3. **Optional instant sync** — repo → Settings → Webhooks → Add:
   - URL: `https://agentskill.sh/api/webhooks/github`
   - Content type: `application/json`
   - Events: **Push** only
4. Users install via: `npx @agentskill.sh/cli@latest` then `ags search moltawards` / `ags install @krrish7089/moltawards` (exact slug appears after claim).

Docs: https://agentskill.sh/creators

---

## 3. LobeHub Skills Marketplace

LobeHub indexes skills via marketplace import (not a separate `publish` CLI in this repo).

**Option A — Web import (recommended)**

1. Open https://lobehub.com or https://market.lobehub.com/s/skills
2. Use **Create / Import skill** → **From GitHub repository**
3. URL: `https://github.com/krrish7089/MoltAwards/tree/main/skills/moltawards`

**Option B — Users install directly from your repo**

```bash
npx -y @lobehub/market-cli register --name "YourAgent" --description "..." --source cursor
npx -y @lobehub/market-cli skills install krrish7089-moltawards-moltawards --agent cursor
```

(Search first: `npx -y @lobehub/market-cli skills search --q moltawards` — identifier appears after LobeHub indexes the repo.)

Requires **Node 22+** for `@lobehub/market-cli`.

---

## 4. Skly

1. Create account at https://skly.ai
2. **Dashboard → Create skill / listing**
3. Upload a ZIP of `skills/moltawards/` (or paste `SKILL.md` + companions).
4. Listing fields (suggested):
   - **Title:** MoltAwards — Government Contract Opportunity Engine
   - **Category:** Business / Productivity
   - **Price:** $0 (free) or your choice
   - **AI tools:** Claude, Cursor, ChatGPT, Codex, OpenClaw
5. Submit for review.

Docs: https://skly.ai/docs/skills

---

## 5. Skills Directory (skillsdirectory.com)

**Option A — Web (fastest)**

1. https://www.skillsdirectory.com/submit
2. Sign in with GitHub
3. Submit repo URL or paste skill content from `submissions/skillsdirectory/SKILL.md`

**Option B — GitHub PR to community repo**

1. Fork https://github.com/theskillsdirectory/skills
2. Copy `submissions/skillsdirectory/SKILL.md` → `skills/moltawards/SKILL.md` in your fork
3. Open PR

Template follows their required frontmatter (single-line `description`, `compatible_agents`, etc.).

---

## 6. Hermes (tap + Skills Hub)

Your repo is already a valid **tap** (`skills/moltawards/SKILL.md`).

```bash
# Any Hermes user can subscribe
hermes skills tap add krrish7089/MoltAwards
hermes skills search moltawards
hermes skills install krrish7089/MoltAwards/moltawards

# Publish to Hermes Skills Hub (requires Hermes CLI + GitHub)
hermes skills publish skills/moltawards --to github --repo krrish7089/MoltAwards
```

Docs: https://hermes-agent.nousresearch.com/docs/user-guide/features/skills

---

## 7. awesome-agent-skills (PR)

1. Fork https://github.com/heilcheng/awesome-agent-skills
2. Add the line from `submissions/awesome-agent-skills/README-patch.md` under **Business, Productivity & Marketing**
3. PR title: `Add skill: krrish7089/moltawards`

---

## 8. awesome-openclaw-skills (two-step)

**This list only links skills already in the official OpenClaw registry.**

1. Publish to https://github.com/openclaw/skills (ClawHub + their CONTRIBUTING flow).
2. After merged, PR to https://github.com/VoltAgent/awesome-openclaw-skills using `submissions/awesome-openclaw-skills/README-patch.md`.

Suggested category: **Finance** (see `govpredict` / business skills) or **Clawdbot Tools**.

---

## agentskill.sh vs agentskillhub.dev

| Site | URL | Action |
|------|-----|--------|
| agentskill.sh | https://agentskill.sh | GitHub connect + webhook (section 2) |
| Agent Skill Hub | https://agentskillhub.dev | Import repo via “Add Skills” UI (similar to skills.sh) |

---

## After any update

```bash
git push   # triggers agentskill.sh webhook if configured
npx skills update moltawards -g -y
```

Re-import on LobeHub / Skly / Skills Directory when you bump `metadata.version` in `SKILL.md`.
