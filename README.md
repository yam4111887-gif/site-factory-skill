# Site Factory — Agent Skill

**From idea to a deployed static product site — in one conversation.**

An [agent skill](https://www.anthropic.com/news/skills) that turns "I want to build a website" into a launched, legally-clean, SEO-ready static site on free hosting. Zero backend, zero cost, honest content.

```yaml
name: site-factory
```

## What it does

Runs a 7-step launch pipeline:

1. **Name & collision check** — exact-match search + domain availability
2. **Site skeleton** — product pages + legal pages (about/privacy/disclaimer) + SEO baseline, privacy-by-default
3. **Content red lines** — data licensing, official-source-only rules, non-advice disclaimers per site type
4. **Deploy** — GitHub Pages via git + API
5. **Verify** — URL status checks, DOM assertions
6. **Record** — site registry conventions, dated content
7. **Post-launch** — Search Console, distribution, custom-domain timing

## Why it exists

Most "build me a website" attempts skip the boring parts that decide whether a site can **monetize and survive**: legal pages (ad networks reject sites without them), data licensing (which APIs are actually allowed in products), honest limitation copy, and per-page SEO. This skill bakes those into the pipeline so they can't be skipped.

Distilled from 8+ production launches.

## Install

Drop this repo into your agent's skills directory:

```bash
# Claude Code / ZCode
git clone https://github.com/yam4111887-gif/site-factory-skill.git ~/.agents/skills/site-factory
```

Or copy `SKILL.md` wherever your agent loads skills from.

## 中文說明

**Site Factory（新站工廠）** 是一個 agent skill：讓 AI 助手把「我想做一個網站」變成上線的靜態產品站。管線包含命名查重、法務頁面、資料授權紅線（哪種開放資料可以商用）、SEO 基本款、GitHub Pages 部署與驗證。零後端、零成本、可放廣告。提煉自 8+ 個實際上線的網站。

## License

MIT — use it, ship things.
