# Driver Receivables & Payment Activity — Executive Summary

**Prepared for funder review**  
**Reporting period:** 2026-01-01 to 2026-04-30 (inclusive, by SOA path date)  
**Locations:** Boracay, Coron  
**Report cutoff (SOA/payment path dates):** 2026-04-30  
**Exported from RTDB at:** 2026-06-04T09:10:26.070Z  
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
| Drivers discovered in scope | 347 |
| Payment events (SOA path dates in range) | 16,866 |
| **Amount collected on charges** (matches Fleet Operations) | PHP 22,681,035.00 |
| Net payment tenders (cash movement view) | PHP 22,730,110.00 |
| Gross payment tenders (incl. voided) | PHP 22,980,329.93 |
| Voided payments | 201 (PHP 250,219.93) |
| SOA ledger lines | 95,024 |
| Gross charge amount (positive, non-voided charges) | PHP 22,862,485.00 |
| Outstanding unpaid balance (ledger snapshot in range) | PHP 181,450.00 |
| Collection rate (fleet-aligned / gross charges) | 99.21% |
| Data reconciliation | Allocation diff PHP 0.00; SOA PAYMENT mirror diff PHP 0.00 |
| Review exceptions | 449 (1 WARN) |

*Fleet Operations uses **paidAmount on SOA charge lines** by line `locationId` — same as `collections_on_charges_*.csv`. Payment tenders can differ slightly (timing/allocation). Boracay+Coron only; global dashboard includes other locations (e.g. PAMBOTODA).*

### Dashboard alignment (material diffs)

- **2026-01 Boracay**: fleet PHP 4,239,845.00 vs export charges PHP 4,242,845.00 (Δ PHP -3,000.00)
- **2026-02 Boracay**: fleet PHP 4,191,225.00 vs export charges PHP 4,194,150.00 (Δ PHP -2,925.00)
- **2026-02 Coron**: fleet PHP 924,400.00 vs export charges PHP 926,400.00 (Δ PHP -2,000.00)
- **2026-04 Coron**: fleet PHP 928,080.00 vs export charges PHP 941,080.00 (Δ PHP -13,000.00)


---

## Location overview

- **Boracay**: PHP 18,930,855.00 on charges (fleet-aligned); PHP 18,979,430.00 payment tenders; PHP 145,800.00 unpaid across 174 drivers
- **Coron**: PHP 3,750,180.00 on charges (fleet-aligned); PHP 3,750,680.00 payment tenders; PHP 35,650.00 unpaid across 20 drivers

---

## Revenue composition (top charge types)

- **VEHICLE_LEASE**: PHP 13,631,270.00 gross, PHP 129,725.00 unpaid (17,323 lines)
- **UNLIMITED_BATTERY_FEE**: PHP 7,277,350.00 gross, PHP 43,575.00 unpaid (14,170 lines)
- **AMORTIZATION**: PHP 1,003,100.00 gross, PHP 0.00 unpaid (128 lines)

Charges are primarily **vehicle lease**, **unlimited battery fees**, and **battery swap** activity. Discount lines (hourly wait, custom discount) reduce gross billings.

---

## Receivables aging (unpaid balances)

- **1-7 DPD**: PHP 4,700.00 (19 items, 12 drivers)
- **8-30 DPD**: PHP 25,425.00 (175 items, 71 drivers)
- **31-60 DPD**: PHP 60,850.00 (145 items, 82 drivers)
- **61-90 DPD**: PHP 72,485.00 (559 items, 128 drivers)
- **90+ DPD**: PHP 17,840.00 (97 items, 67 drivers)

Largest single-driver unpaid balance in export: **PHP 9,450.00** (Boracay, oldest unpaid date 2026-03-07, 54 days).

---

## Collection trends

- **Average net daily collections (days with non-voided payments):** PHP 189,417.58
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
| `dashboard_reconciliation.csv` | Month/location: fleetMetrics vs export (in parent export folder) |
