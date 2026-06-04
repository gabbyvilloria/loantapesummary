# Driver Receivables & Payment Activity — Executive Summary

**Prepared for funder review**  
**Reporting period:** 2026-01-01 to 2026-04-30  
**Locations:** Boracay, Coron  
**As of:** 2026-04-30  
**Data basis:** Firebase RTDB payment and SOA records (masked driver references)

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
| Drivers in scope | 344 |
| Payment events | 16,765 |
| Total cash collected | PHP 22,587,310.00 |
| SOA ledger lines | 94,844 |
| Gross charge amount (positive charges) | PHP 22,854,185.00 |
| Outstanding unpaid balance (as of 2026-04-30) | PHP 316,000.00 |
| Collection rate on charges | 98.83% (cash vs gross charges; see note below) |
| Data reconciliation | Payment ↔ allocation ↔ SOA PAYMENT mirrors aligned (PHP 0.00) |
| Review exceptions | 449 (1 WARN) |

*Note: Cash collected can exceed same-day charge recognition timing; use **collection_rate_on_charges_pct** in the monthly summary for charge-level collection performance.*

---

## Location overview

- **Boracay**: PHP 18,856,630.00 collected; PHP 263,300.00 unpaid across 178 drivers
- **Coron**: PHP 3,730,680.00 collected; PHP 52,700.00 unpaid across 36 drivers

---

## Revenue composition (top charge types)

- **VEHICLE_LEASE**: PHP 13,625,370.00 gross, PHP 210,925.00 unpaid (17,302 lines)
- **UNLIMITED_BATTERY_FEE**: PHP 7,274,750.00 gross, PHP 93,075.00 unpaid (14,154 lines)
- **AMORTIZATION**: PHP 1,002,450.00 gross, PHP 0.00 unpaid (127 lines)

Charges are primarily **vehicle lease**, **unlimited battery fees**, and **battery swap** activity. Discount lines (hourly wait, custom discount) reduce gross billings.

---

## Receivables aging (unpaid balances)

- **1-7 DPD**: PHP 12,950.00 (30 items, 19 drivers)
- **8-30 DPD**: PHP 25,950.00 (176 items, 71 drivers)
- **31-60 DPD**: PHP 61,850.00 (146 items, 83 drivers)
- **61-90 DPD**: PHP 72,410.00 (558 items, 127 drivers)
- **90+ DPD**: PHP 16,390.00 (95 items, 66 drivers)

Largest single-driver unpaid balance in export: **PHP 9,450.00** (Boracay, oldest unpaid date 2026-03-07, 54 days).

---

## Collection trends

- **Average daily collections (days with payments):** PHP 188,227.58
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
