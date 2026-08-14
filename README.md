# QuoteGuard 🛡️
### A SaaS Deal Desk & Pricing Governance Simulator

QuoteGuard simulates the full commercial lifecycle of an enterprise SaaS deal — new-business quoting, renewals, deployment migrations, multi-currency pricing, competitive benchmarking, and approval governance — modeled on the pricing mechanics of a modular, unified data security platform (Varonis-style: per-user licensing, layered add-ons and standalone modules, enterprise/regulated buyers).

## Why This Project Exists

Most pricing portfolio projects stop at "here's a pricing calculator." Real Pricing & Deal Desk roles live one step further: they price a platform built from a dozen individually-licensable capabilities (not flat SKUs), separate one-time implementation from recurring subscription down to the line item, handle the *existing customer* lifecycle (renewals, migrations, shrinkage risk) as much as new deals, work across currencies, keep internal pricing mechanics hidden from the sales-facing team, and report all of it upward for governance. QuoteGuard is built to demonstrate that full picture in a single working Excel model.

## What's Inside

### Excel Workbook (`QuoteGuard_Model.xlsx`)

| Sheet | Visible to AMs? | Purpose |
|---|---|---|
| `Deal_Input` | ✅ | New-business deal parameters |
| `Deal_Overview` | ✅ | New-business quote — full line-item breakdown, live discount & currency, approval status |
| `Renewal_Input` | ✅ | Existing-customer renewal parameters |
| `Renewal_Overview` | ✅ | Renewal quote — same breakdown depth as Deal_Overview, plus growth/shrinkage & migration flags |
| `Competitive_Benchmark` | ✅ | Scope-aware competitor comparison, isolated from the pricing engine |
| `Deal_Log` | ✅ | Historical deal records — structured for downstream reporting (see Roadmap) |
| `Lookup_Tables` | 🔒 Hidden + protected | Single source of truth for all pricing, FX, and reference data |
| `Pricing_Calculation` | 🔒 Hidden + protected | New-business pricing engine, FX control, approval workflow |
| `Renewal_Calculation` | 🔒 Hidden + protected | Renewal pricing engine, migration logic, FX control, approval workflow |

**Pricing structure:** 1 Core Platform (2 tiers) + 4 Add-Ons (% uplift) + 7 standalone Additional Modules (flat price) = 12 licensable capabilities, each with its own recurring price and implementation fee, fully itemized on every customer-facing view — never shown only as a lump sum.

**Multi-currency:** USD/GBP/EUR selectable per deal, with pricing-team-controlled manual FX override cells separate from the reference rate table.

**Governance:** A 3-stage approval workflow (Pricing Analyst → Manager Approved → Final Quote Sent) with live green/red conditional formatting, visible read-only to account managers, editable only behind a password on the hidden calculation sheets.

**Renewal intelligence:** Two independent escalation flags — Renewal Shrinkage and Deployment Migration — that can fire simultaneously, since they represent different governance risks.

![Deal Input](https://github.com/Sundhar-CMA/Quote-guard-Pricing-Model/blob/main/Screenshots/Deal%20Input.png)
![Deal Overview](https://github.com/Sundhar-CMA/Quote-guard-Pricing-Model/blob/main/Screenshots/Deal%20Overview.png)

## Roadmap — Not Yet Built

**Power BI dashboard.** `Deal_Log` was purpose-built as a flat, row-per-deal reporting table specifically so it can be dropped straight into Power BI (or Excel PivotTables/PivotCharts) without restructuring — every pricing figure on it is formula-driven off the same `Lookup_Tables` engine as the rest of the workbook, so it stays consistent with the quoting logic rather than being a static export. The intended design (4 pages — Deal Desk Command Center, Pricing Governance, Pipeline & Mix, Renewal Health — with weighted-average DAX measures rather than naive averages) is documented in `02_StepByStep_Build_Guide.md`, ready to build out when there's a reason to pick it back up.

## Repository Structure

```
QuoteGuard/
├── README.md
├──Project_Overview.pdf
├──Step_ByStep_Build_Guide.pdf
├── QuoteGuard_Model.xlsx
└── screenshots
```

## Tools Used
- Excel (pricing engine, deal/renewal overviews, approval governance, conditional formatting)

## Key Design Principles
- **One source of truth**: every price, rate, and assumption lives in `Lookup_Tables` exactly once.
- **Recurring and one-time never mix**: implementation fees are structurally separate from ACV throughout the formula chain, only combining once, in the final TCV calculation.
- **Governance is never averaged away**: discount and shrinkage metrics are always size-weighted.
- **Internal mechanics stay internal**: uplift %s, T-shirt tables, and FX overrides live only on hidden, password-protected sheets — account managers see clean outputs only.
- **Assumptions are always labeled**: every figure not publicly disclosed by the real vendor is marked `[ASSUMPTION]` and anchored to a public reference point wherever one exists.

## Status
✅ Excel workbook complete — 9 sheets, full new-business + renewal lifecycle, multi-currency, approval governance
📋 Power BI dashboard scoped and documented, not yet built

---
*This is an independent portfolio project built to demonstrate Pricing & Deal Desk Analyst competencies. It is not affiliated with or endorsed by Varonis Systems, Inc.*
