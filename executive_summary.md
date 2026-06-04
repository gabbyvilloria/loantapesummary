# Driver Receivables & Payment Activity — Executive Summary

**Prepared for funder review**  
**Reporting period:** 2026-01-01 to 2026-04-30 (inclusive, by SOA path date)  
**Locations:** Boracay, Coron  
**Report cutoff (SOA/payment path dates):** 2026-04-30  
**Exported from RTDB at:** 2026-06-04T08:44:22.775Z  
**Data basis:** Firebase RTDB `payments/` and `SOA/` records (masked driver references)

---

## What this is

This summary describes **operating receivables and payment activity** for drivers at Boracay and Coron. It is **not** a formal loan tape: there are no loan contracts, principal balances, interest rates, or amortization schedules in this dataset.

The funder receives:
- **This memo** — portfolio-level narrative and KPIs
- **Summary tables** (CSV) — rollups by month, location, transaction type, aging, and exceptions
- **Detail files** (separate folder) — payment movements, allocations, and full SOA ledger for audit

---

## Portfolio snapshot

| Metric | Value |
|--------|------:|
| Drivers in scope | 339 |
| Payment events (SOA path dates in range) | 16,849 |
| **Gross payment amount** (includes voided) | PHP 22,959,404.93 |
| **Net cash collected** (voided excluded) | PHP 22,709,185.00 |
| Voided payments | 201 (PHP 250,219.93) |
| SOA ledger lines | 94,890 |
| Gross charge amount (positive, non-voided charges) | PHP 22,840,035.00 |
| Outstanding unpaid balance (ledger snapshot in range) | PHP 179,925.00 |
| Collection rate (net cash / gross charges) | 99.43% |
| Data reconciliation | Allocation diff PHP 0.00; SOA PAYMENT mirror diff PHP 0.00 |
| Review exceptions | 449 (1 WARN) |

*Collections are keyed by **SOA path date** (`payments/{driver}/{yyyy}/{MM}/{dd}`), not payment clock time. Late postings appear on the SOA date bucket. Dashboard daily collection logs may differ slightly.*

---

## Location overview

- **Boracay**: PHP 18,973,505.00 collected; PHP 145,725.00 unpaid across 173 drivers
- **Coron**: PHP 3,735,680.00 collected; PHP 34,200.00 unpaid across 19 drivers

---

## Revenue composition (top charge types)

- **VEHICLE_LEASE**: PHP 13,611,870.00 gross, PHP 128,725.00 unpaid (17,284 lines)
- **UNLIMITED_BATTERY_FEE**: PHP 7,274,750.00 gross, PHP 43,500.00 unpaid (14,140 lines)
- **AMORTIZATION**: PHP 1,003,100.00 gross, PHP 0.00 unpaid (128 lines)

Charges are primarily **vehicle lease**, **unlimited battery fees**, and **battery swap** activity. Discount lines (hourly wait, custom discount) reduce gross billings.

---

## Receivables aging (unpaid balances)

- **1-7 DPD**: PHP 4,700.00 (19 items, 12 drivers)
- **8-30 DPD**: PHP 25,425.00 (175 items, 71 drivers)
- **31-60 DPD**: PHP 60,850.00 (145 items, 82 drivers)
- **61-90 DPD**: PHP 72,410.00 (558 items, 127 drivers)
- **90+ DPD**: PHP 16,390.00 (95 items, 66 drivers)

Largest single-driver unpaid balance in export: **PHP 9,450.00** (Boracay, oldest unpaid date 2026-03-07, 54 days).

---

## Collection trends

- **Average net daily collections (days with non-voided payments):** PHP 189,243.21
- **Voided payments retained for transparency:** 201 events (PHP 250,219.93)

---

## Data quality & limitations

- Driver and staff identities are **masked** in all funder-facing files; no names, phone numbers, or government IDs are included.
- **449** exception rows are documented in `exceptions_summary.csv`; most are informational (voided payments, allocations to voided charges).
- Operator **amortization** charges on operator SOA paths are excluded from this driver-scoped export.
- This package reflects **billing and collection behavior**, suitable for receivables analysis, not secured lending analysis without a loan contract layer.

---

## Recommended next step for funder

1. Review **summary/** tables first (5–10 minutes).
2. Use **transaction_type_summary.csv** and **aging_summary.csv** for risk questions.
3. Drill into **detail/** CSVs only where validation is needed.

---

## Summary file index

| File | Description |
|------|-------------|
| `monthly_by_location.csv` | Collections by month and location |
| `location_rollup.csv` | One row per location |
| `transaction_type_summary.csv` | Gross, collected, unpaid by SOA type |
| `collection_rate_by_month.csv` | Monthly gross charges vs collections |
| `aging_summary.csv` | Unpaid balances by aging bucket |
| `top_exposures.csv` | Top drivers by outstanding balance |
| `payment_method_mix.csv` | Cash vs other payment methods |
| `exceptions_summary.csv` | Exception counts by type |
