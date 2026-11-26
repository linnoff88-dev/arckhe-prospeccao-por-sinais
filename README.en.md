# 📡 Signal-Based Prospecting

[![Signal-Based Prospecting](guia/assets/banner-en.jpg)](https://linnoff88-dev.github.io/arckhe-/guia/en/)

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

## What it is

This is a free kit for people who sell to businesses and want to prospect without blasting cold email lists. The idea is to look for **signals**—public events that show a company may need you now, such as an open job, a product launch, or a new executive—and only then find the decision-maker and write a message that mentions that signal. Claude Code does the heavy lifting using Clay, a company and contact data platform, and delivers a spreadsheet for you to review. You need Claude Code, a Clay account (there's a free plan and a trial), and an afternoon to fill in the context for your business.

## 📖 User guide

Full guide (landing page + step-by-step instructions): **https://linnoff88-dev.github.io/arckhe-/guia/en/**

## Before you start

- **Claude Code** ≥ 2.1.91 (requires a paid Claude subscription): `curl -fsSL https://claude.ai/install.sh | bash` (Mac/Linux), `irm https://claude.ai/install.ps1 | iex` (Windows) or `npm install -g @anthropic-ai/claude-code` — docs: https://docs.claude.com/en/docs/claude-code/overview
- **A Clay account** (free plan or 14-day trial).
- **git** (or download the [.zip](https://github.com/linnoff88-dev/prospeccao-por-sinais/archive/refs/heads/main.zip)) and, only for the optional signals skill, **Node.js** (`npx`).

## The process, from start to finish

Who does what: 🧠 you in Claude Code · ⚙️ Clay/script · 🤖 agent (Claude Code working on its own)

| # | Step | Command | Who |
|---|-------|---------|------|
| 1 | Download the kit and open Claude Code in the folder | `git clone https://github.com/linnoff88-dev/prospeccao-por-sinais.git` · `cp -r prospeccao-por-sinais/kit ~/minha-prospeccao` · `cd ~/minha-prospeccao` · `claude` | 🧠 |
| 2 | Install the Clay plugin (Claude Code ≥ 2.1.91) | `/plugin marketplace add clay-run/agent-plugins` · `/plugin install clay@clay-plugins` · "Run the clay:setup skill" | 🧠 |
| 3 | Fill in your business context | Edit `contexto/*.md` (template in `contexto/exemplo/`) | 🧠 |
| 4 | Define the signals | Edit `sinais.yaml` · optional: `npx skills add clay-run/clay-skill-creator --skill customer-signal-generator` | 🧠 + 🤖 |
| 5 | ICP: company list (start with 10 rows) | Step 1 of `prompts/passo-a-passo.md` | 🤖 + ⚙️ |
| 6 | Monitor hiring signals | Step 2 | 🤖 + ⚙️ |
| 7 | Research agent (product launch) | Step 3 | 🤖 + ⚙️ |
| 8 | Find decision-makers only when there is a signal (run condition: active signal weights add up to 30 or more) | Step 4 | 🤖 + ⚙️ |
| 9 | Email waterfall + verification | Step 5 | ⚙️ |
| 10 | Contextual message (subject + body mentioning the signal) | Step 6 — or do it all at once with `/goal` (`prompts/goal-prospeccao.md`) | 🤖 |
| 11 | Final CSV for review | `saida/leads-AAAA-MM-DD.csv` (columns in `colunas-csv.md`) | 🤖 |
| 12 | Human review | Read the rows with `revisar = sim` and make corrections | 🧠 |
| 13 | Import into your sequencer and send slowly | Import CSV → campaign; warmed secondary domain, few sends per day, spam complaints < 0.3% | 🧠 + ⚙️ |
| 14 | Suppression | Anyone who asks to opt out goes into `supressao.csv` the same day | 🧠 |

Golden rule (in `kit/CLAUDE.md`): the agent **never spends credits without asking**, **runs 10 rows first**, and **never sends anything**.

## The kit

The kit files are in Portuguese (Claude Code reads them in any language; translate the templates if you prefer).

```
kit/
├── CLAUDE.md                 agent rules (credits, 10 rows, review, opt-out, LGPD)
├── contexto/                 6 templates: perfil-do-negocio, oferta, casos, provas, faq, tom-de-voz
│   └── exemplo/              the same 6, filled in for a FICTIONAL company
├── prompts/
│   ├── goal-prospeccao.md    prompt for /goal with a verifiable finish line
│   └── passo-a-passo.md      one prompt per workflow step
├── sinais.yaml               sample signals with validity window and weight
├── colunas-csv.md            output spreadsheet columns
├── checklist-lgpd.md         practical checklist (not legal advice)
└── supressao.csv             people who asked to opt out
```

## Costs (Clay public documentation, checked on Nov 1, 2026)

- Free: 100 credits/month. 14-day trial: 1,000 credits. Launch plan: from US$ 185/month (2,500 credits + 15,000 actions).
- In the waterfall, the default email and mobile providers return the credit when they don't find a match; mobile is not available on the free plan or trial.
- Source: https://github.com/clay-run/public-docs

## References

- Clay plugin for agents: https://github.com/clay-run/agent-plugins
- Gmail — sender guidelines: https://support.google.com/a/answer/81126?hl=en
- LGPD (Brazil's General Data Protection Law, Law 13.709/2018): https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm · ANPD (Brazil's National Data Protection Authority): https://www.gov.br/anpd

---

Open and free content from [ARCKHÉ AI](https://ARCKHÉ AI).