# Report Reconciliation Playbook

## Objective
This repository documents common reconciliation issues in Microsoft Business Central and structured troubleshooting approaches.

---

## Case Study 1: Customer Detail Trial Balance vs Aged A/R

### Problem
Customer Detail Trial Balance total does not match Aged Accounts Receivable report.

### Common Root Causes

1. Adjust Exchange Rates not posted
2. Different Posting Date filters
3. Document Date vs Posting Date mismatch
4. Closed entries excluded
5. Currency revaluation timing differences

---

## Investigation Checklist

- [ ] Verify Posting Date filter
- [ ] Verify Document Date filter
- [ ] Run Adjust Exchange Rates batch job
- [ ] Check Detailed Customer Ledger Entries
- [ ] Confirm Open/Closed entry filter
- [ ] Compare LCY vs FCY values

---

## Technical Insight

Customer – Detail Trial Balance aggregates from:
- Detailed Customer Ledger Entries

Aged A/R is based on:
- Customer Ledger Entries (Open entries only)

Understanding data source differences is critical in reconciliation.

---

## Lessons Learned

- Always run currency revaluation before period-end reporting.
- Ensure filters are aligned across reports.
- Never assume reports use the same data structure.

---

## Future Enhancements

- Add Vendor reconciliation scenario
- Add GL vs Subledger reconciliation guide
- Add Exchange Rate revaluation flow diagram

---

## Case Study 2: Foreign Currency Difference  
### Scenario: Detail Trial Balance vs Aged A/R Mismatch

### Incident Summary
While reconciling customer balances, the **Customer – Detail Trial Balance** did not match the **Aged Accounts Receivable** totals for foreign currency customers.

### Observed Behaviour

- Aged A/R showed correct outstanding balance
- Detail Trial Balance displayed different total
- Difference amount matched historical exchange rate adjustment
- No visible "Adjustment of Opening Balance" line in report

---

### Initial Assumption
Report calculation error or missing ledger entries.

---

### Root Cause Analysis

Investigation revealed:

1. **Adjust Exchange Rates** batch job had not been run for prior period
2. Exchange rate revaluation entries existed but:
   - Reflected in Detailed Customer Ledger Entries
   - Not displayed as "Adjustment of Opening Balance"
3. Reports were using different logic:

| Report                          | Data Source                      |
|---------------------------------|----------------------------------|
| Customer – Detail Trial Balance | Detailed Customer Ledger Entries |
| Aged Accounts Receivable        | Customer Ledger Entries (Open)   |

---

### Why the Difference Occurred

- Exchange rate adjustments modify LCY values
- Adjustments impact detailed entries
- Opening balance does not automatically reclassify adjustments
- Reports respect date filters differently

---

### Resolution Steps

- Run **Adjust Exchange Rates**
- Post revaluation entries
- Re-run reports with identical filters:
  - Posting Date
  - Document Date
  - Currency
  - Customer No.
  - Open/Closed status

---

### Key Learning

✔ Exchange rate adjustments may not appear as explicit "Opening Balance Adjustment"  
✔ Report totals can differ due to data source design  
✔ Always validate batch jobs before reconciliation  

---

### Preventive Action

- Schedule monthly Adjust Exchange Rates job
- Add reconciliation checklist before reporting
