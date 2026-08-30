# Search Queries for Job Scraper

<!-- Populated by /setup for Muhammad Irfan. Re-run `/setup --section search` to update. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Currently enabled:

- **linkedin-search** - any country/city or remote (primary)
- **freehire-search** - tech/software/data/DevOps roles across ~50 ATS platforms, many markets + remote (primary for engineering roles)
- **jobindex-search**, **jobbank-search**, **jobdanmark-search**, **jobnet-search** - Denmark only (enabled because Denmark is a target market; ignore their output when not searching Denmark)

You do **not** need a matching `site:` line below for those CLIs to run. The `site:` templates are the **WebSearch fallback** - for portals without a CLI (Reed, Indeed, StepStone, TotalJobs, Otta, Welcome to the Jungle, Greenhouse boards), company career pages, or when a CLI fails. To promote any of those to a real CLI, scaffold one with `/add-portal`.

**Language scope:** all target markets are English-language, so write every query in **English only**. Muhammad also speaks Urdu, Hindi and Punjabi, but these are not job-search languages for the target countries. See `04-job-evaluation.md`'s Language Gate for how language requirements are handled at scoring time.

**Sponsorship scope:** Muhammad holds a UK Graduate Visa (expires 4 Jan 2027) and needs Skilled Worker sponsorship for permanent UK roles, and full sponsorship/relocation for any role outside the UK. Prefer queries and filters that surface sponsor-friendly employers. Add `visa sponsorship` or `sponsorship available` as a query variant where the board supports free-text search. Non-UK results are in scope but should be treated as sponsorship-gated (see `04-job-evaluation.md`).

## Search Sites

Primary (via CLI): LinkedIn, freehire.me aggregator, Danish boards (Denmark only).

Fallback (via WebSearch `site:` filters):
- **reed.co.uk**, **indeed.co.uk**, **stepstone.co.uk** / **stepstone.de**, **totaljobs.com**, **otta.com**, **welcometothejungle.com**, **cv-library.co.uk** - UK/EU general and tech boards
- **boards.greenhouse.io**, **jobs.lever.co**, **ashbyhq.com** - ATS-hosted company career pages (often sponsor-friendly scale-ups)
- Direct Google searches with `site:` filters for company career pages

## Query Categories

Queries are grouped by priority (Muhammad's stated ranking). Combine each with a location term from the Location Filter below where the site supports it. Organised by function; several title variants per category.

### Priority 1: DevOps / Platform Engineer

Strongest and most desired direction.

```
site:linkedin.com/jobs "DevOps Engineer" (remote UK OR London OR Birmingham)
site:linkedin.com/jobs "Platform Engineer" (remote UK OR United Kingdom)
site:linkedin.com/jobs ("DevOps Engineer" OR "Platform Engineer") "visa sponsorship"
site:reed.co.uk "DevOps Engineer" Terraform AWS
site:indeed.co.uk "Platform Engineer" (Kubernetes OR Terraform)
site:boards.greenhouse.io ("DevOps Engineer" OR "Platform Engineer") "sponsorship"
site:linkedin.com/jobs ("Infrastructure Engineer" OR "CI/CD Engineer") Jenkins Terraform
```

### Priority 2: Java Backend / Java Software Engineer

```
site:linkedin.com/jobs ("Java Engineer" OR "Java Backend Engineer" OR "Java Software Engineer") (remote UK OR London)
site:linkedin.com/jobs "Backend Engineer" "Spring Boot" (United Kingdom OR remote)
site:reed.co.uk "Java Developer" "Spring Boot" microservices
site:indeed.co.uk "Java Backend Developer" AWS
site:linkedin.com/jobs ("Java Engineer" OR "Backend Engineer") "visa sponsorship"
site:boards.greenhouse.io "Backend Engineer" Java "sponsorship"
```

### Priority 3: Full Stack Engineer

```
site:linkedin.com/jobs "Full Stack Engineer" (Java OR Node OR React) (remote UK OR London OR Birmingham)
site:linkedin.com/jobs "Full Stack Developer" (Laravel OR PHP OR Node.js)
site:reed.co.uk "Full Stack Developer" React (Java OR Node)
site:otta.com "Full Stack Engineer" (Java OR TypeScript)
site:linkedin.com/jobs "Full Stack Engineer" "visa sponsorship"
```

### Priority 4: Cloud Engineer / SRE

```
site:linkedin.com/jobs ("Cloud Engineer" OR "Site Reliability Engineer" OR "SRE") AWS (remote UK OR United Kingdom)
site:linkedin.com/jobs "AWS Engineer" Terraform
site:reed.co.uk ("Cloud Engineer" OR "SRE") AWS Kubernetes
site:linkedin.com/jobs ("Cloud Engineer" OR "SRE") "visa sponsorship"
```

### Priority 5: PHP / Laravel, and broader Software / Backend / API Engineer

Wider net, including the earlier-career specialism and generic titles.

```
site:linkedin.com/jobs ("PHP Engineer" OR "Laravel Developer" OR "PHP Developer") (remote UK OR United Kingdom)
site:linkedin.com/jobs ("Software Engineer" OR "Backend Engineer" OR "API Engineer") (Java OR Python OR PHP) "visa sponsorship"
site:reed.co.uk "Laravel Developer" REST API
site:indeed.co.uk "Software Engineer" (Java OR PHP) sponsorship
site:welcometothejungle.com ("Backend Engineer" OR "Software Engineer") (Java OR PHP OR Node)
```

### International (all sponsorship-gated - English-language roles only)

Run these against `linkedin-search` and `freehire-search` with the country supplied explicitly.

```
"DevOps Engineer" OR "Platform Engineer" (visa sponsorship OR relocation) [country]
"Java Backend Engineer" OR "Backend Engineer" "relocation" [country]
"Full Stack Engineer" (sponsorship OR relocation assistance) [country]
```

Target countries: USA, Canada, Germany, Netherlands, France, Italy, Denmark, Ireland, rest of EU (English-speaking teams), Australia, New Zealand, UAE / Dubai, Saudi Arabia.

## Location Filter

Tiered by preference. All non-UK tiers require employer sponsorship / relocation.

- **Ideal:** Fully remote (UK-based contract of employment); Birmingham and West Midlands on-site/hybrid.
- **Acceptable:** Hybrid anywhere in the UK with a weekly or occasional commute; London (hybrid); any UK city with relocation.
- **Acceptable (sponsorship-gated):** Remote roles that hire from the UK; USA, Canada, Ireland, Germany, Netherlands, Denmark, rest of Europe (English-language), Australia, New Zealand, UAE/Dubai, Saudi Arabia - with visa sponsorship and relocation support.
- **Borderline:** Non-UK roles that are silent on sponsorship (flag, do not auto-drop - see eligibility gate).
- **Too far / exclude:** Roles explicitly stating "no visa sponsorship" or requiring existing unrestricted/permanent right to work in a country where Muhammad has none; on-site-only roles in a location with no relocation offered and no realistic commute.

## Language Filter

All target markets are English-language. Apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language Muhammad has not declared (English, Urdu, Hindi, Punjabi), as a job condition, is excluded; a posting requiring a higher English level than "professional working proficiency" is flagged, not excluded. Postings merely *written* in another language, for a role that operates in English, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area (e.g. `/scrape kubernetes` or `/scrape london java`), select queries from the matching category and generate 2-3 custom queries for that focus.
