# Rakamin Workforce Intelligence Platform
### PM Case Study — Medika Nusantara Engagement

**Built by C.M. Fajar** · [@fajaruuxyz](https://instagram.com/fajaruuxyz)

---

## What This Is

A working prototype of an AI-powered workforce decision platform, built as part of Rakamin's Product Manager (AI-Native) case study.

The scenario: Medika Nusantara, a healthcare distribution company with 15,000 employees across 90 branches, has asked Rakamin to deliver AI-driven workforce decisions in 90 days. The CHRO wants to know which employees need reskilling — starting from an HR data stack that is fragmented, inconsistent, and partially inaccessible.

This prototype makes one argument: **the data layer is the product.** Before any AI insight is possible, someone has to fix what's broken underneath.

---

## Live Demo

→ **[rakamin-workforce-intelligence.vercel.app](https://rakamin-workforce-intelligence.vercel.app)**

---

## What the Prototype Does

Four pages, one toggle. Switch between **Dataset A (raw)** and **Dataset B (processed)** at any point to see how data quality directly changes what the AI layer can and can't see.

**Overview** shows the full employee table. In raw mode you see name mismatches between HRIS and ATS, inconsistent job titles across branches, missing skill fields, and incompatible performance scales. In processed mode the same employees appear with unified identities, normalized roles, and reskilling priority scores.

**Reskilling Priorities** is locked on Dataset A — intentionally. With 42% of skill records missing, the model can't generate reliable gap scores. Switch to Dataset B to unlock employee cards sorted by skill gap score, with missing skills, inferred skills, confidence pips, and recommended training courses.

**Identity Resolution** shows how each employee was matched across SAP SuccessFactors, Workable, and Moodle (Oracle Payroll is off-limits). Four tiers from high-confidence email matches down to fuzzy name matching that requires human sign-off.

**Data Quality Gap** puts both datasets side by side. Seven metrics. Four implication cards. One core argument.

---

## Project Structure

```
rakamin-workforce-intelligence/
├── index.html              # Full prototype — self-contained, no build step
├── data/
│   ├── dataset_A_messy.csv     # 200 records — raw enterprise reality
│   └── dataset_B_clean.csv     # 195 records — post-processing output
├── vercel.json             # Routing config for Vercel deployment
├── package.json            # Optional: local dev server
├── .gitignore
└── README.md
```

---

## The Data

Two synthetic CSV datasets representing Medika Nusantara employee records, generated to reflect realistic enterprise HR conditions.

| File | Records | Description |
|---|---|---|
| `data/dataset_A_messy.csv` | 200 | Raw enterprise reality |
| `data/dataset_B_clean.csv` | 195 | Post-processing output |

### What makes Dataset A messy

- 42% of employees have no skill fields populated
- The same role has different names by branch ("Senior Sales" in Surabaya, "Sales 2" in Makassar, "Penjualan Senior" elsewhere)
- Performance ratings use three incompatible scales: 1–5, 1–4, and letter grades A–D
- 30 email mismatches between HRIS and ATS (personal Gmail vs. work email)
- 67 hire date conflicts across systems
- 5 near-duplicate records from different systems

### What Dataset B adds

- A unified `rakamin_id` linking each employee across all accessible systems
- Identity confidence scores by match tier (email, name+date, name+dept, fuzzy)
- Skills resolved from three sources: self-reported, LMS-inferred, or title-inferred — each tagged with its own confidence level
- Performance normalized to a single 1–5 scale with branch-specific conversion logic
- A `skill_gap_score` (0–100), `reskill_priority` (HIGH/MEDIUM/LOW), and `recommended_courses` per employee
- A `needs_human_review` flag with a plain-language reason

---

## Running Locally

No build step needed. Open `index.html` directly in your browser, or run a local server:

```bash
npm install
npm run dev
```

Then visit `http://localhost:3000`.

---

## Design Notes

**The toggle is the thesis.** Every page responds to the dataset switch. The Reskilling page locks on Dataset A not as a bug, but as a statement — you can't generate reliable AI output from broken data.

**Confidence is always visible, never alarming.** Low-confidence records get a pip bar, a plain-language review flag, and a "Review Profile" button instead of a destructive action. The model doesn't pretend certainty when it doesn't have it.

**Cards use flex column layout.** All reskilling cards share the same height within each row, with the action button pinned to the bottom — so the "View Recommendations" button always sits at the same vertical position regardless of content length.

**Shadow system for depth.** Cards, sidebar, topbar, and modal each sit at a different elevation. The layering creates visual hierarchy without relying on background color alone.

**Plus Jakarta Sans** is Rakamin's brand font — a geometric sans-serif designed for Jakarta's city branding program, now widely adopted across Indonesian tech products.

---

## Tech Stack

- Pure HTML, CSS, and vanilla JavaScript — no framework, no build step
- Plus Jakarta Sans + JetBrains Mono via Google Fonts
- Synthetic data embedded directly in the HTML
- Vercel for hosting (zero config for static files)

---

## Case Study Context

This is Deliverable 2 of a three-part PM case study submission for Rakamin's AI-Native Product Manager role.

- **Deliverable 1** — Written strategy document (problem framing, data architecture, AI system design, 90-day roadmap, platform strategy)
- **Deliverable 2** — This prototype
- **Deliverable 3** — Synthetic datasets in `/data`

The least confident decision in the submission: prioritizing Skill Gap Analysis over Attrition Prediction as the 90-day PoC. The reasoning is in the strategy document. Short version: attrition modeling without payroll data has a systematic blind spot — it misses the most expensive flight risk. Skill gap analysis works with the data we actually have.

---

## Credit

Built by **M. Fajar** ([@fajaruuxyz](https://instagram.com/fajaruuxyz)) as a PM case study for Rakamin.

AI tools used: Claude Sonnet 4 for strategy, document writing, data generation, and code. All product decisions, prioritization calls, and design choices are the author's own.

© @fajaruuxyz · 2026

---

*This prototype uses synthetic data. No real employee information is represented.*
