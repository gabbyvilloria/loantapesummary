# Driver Receivables & Payment Activity — Executive Summary

**Prepared for funder review**  
**Reporting period:** 2026-01-01 to 2026-06-04 (inclusive, by SOA path date)  
**Locations:** Boracay, Coron  
**Report cutoff (SOA/payment path dates):** 2026-06-04  
**Exported from RTDB at:** 2026-06-04T08:42:45.012Z  
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
| Drivers in scope | 386 |
| Payment events (SOA path dates in range) | 21,475 |
| **Gross payment amount** (includes voided) | PHP 30,073,569.93 |
| **Net cash collected** (voided excluded) | PHP 29,769,075.00 |
| Voided payments | 240 (PHP 304,494.93) |
| SOA ledger lines | 125,318 |
| Gross charge amount (positive, non-voided charges) | PHP 30,155,005.00 |
| Outstanding unpaid balance (ledger snapshot in range) | PHP 462,420.00 |
| Collection rate (net cash / gross charges) | 98.72% |
| Data reconciliation | Allocation diff PHP 0.00; SOA PAYMENT mirror diff PHP 0.00 |
| Review exceptions | 541 (1 WARN) |

*Collections are keyed by **SOA path date** (`payments/{driver}/{yyyy}/{MM}/{dd}`), not payment clock time. Late postings appear on the SOA date bucket. Dashboard daily collection logs may differ slightly.*

---

## Location overview

- **Boracay**: PHP 25,166,395.00 collected; PHP 388,060.00 unpaid across 204 drivers
- **Coron**: PHP 4,602,680.00 collected; PHP 74,360.00 unpaid across 52 drivers

---

## Revenue composition (top charge types)

- **VEHICLE_LEASE**: PHP 17,887,870.00 gross, PHP 294,985.00 unpaid (22,504 lines)
- **UNLIMITED_BATTERY_FEE**: PHP 9,761,000.00 gross, PHP 120,700.00 unpaid (18,661 lines)
- **AMORTIZATION**: PHP 1,276,710.00 gross, PHP 1,230.00 unpaid (169 lines)

Charges are primarily **vehicle lease**, **unlimited battery fees**, and **battery swap** activity. Discount lines (hourly wait, custom discount) reduce gross billings.

---

## Receivables aging (unpaid balances)

- **1-7 DPD**: PHP 46,265.00 (143 items, 66 drivers)
- **8-30 DPD**: PHP 96,795.00 (283 items, 100 drivers)
- **31-60 DPD**: PHP 22,220.00 (126 items, 58 drivers)
- **61-90 DPD**: PHP 69,200.00 (254 items, 104 drivers)
- **90+ DPD**: PHP 93,000.00 (666 items, 147 drivers)

Largest single-driver unpaid balance in export: **PHP 9,450.00** (Boracay, oldest unpaid date 2026-03-07, 89 days).

---

## Collection trends

- **Average net daily collections (days with non-voided payments):** PHP 192,058.55
- **Voided payments retained for transparency:** 240 events (PHP 304,494.93)

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
