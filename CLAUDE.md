# AK_AddPaymentMethodName_onTenderTrans

## Project Purpose
Add a "Payment method name" display column to the D365 F&O Retail **Shift Tender Transactions** screen (form: `RetailPosBatchTable`, inner datasource: `RetailPosBatchTenderTrans`).

## Conventions

- **Extensions only** — no base object modifications under any circumstance.
- **AK_ prefix** — all custom AOT objects, methods, controls, and labels must carry the `AK_` prefix.
- **Chain of Command / Augmentation** — use `[ExtensionOf(...)]` patterns only.
- **Reuse existing EDTs** — do not create new EDTs if a standard one already exists (e.g. `RetailTenderTypeName`).
- **No hardcoded values** — never hardcode store IDs, tender type IDs, or other business data.
- **Display methods on table extension classes** — not inline on forms.

## Key Objects

| Object | Type | Purpose |
|---|---|---|
| `RetailPosBatchTenderTrans` | Table (base) | Source table for the tender transactions grid |
| `RetailTenderTypeTable` | Table (base) | Lookup table for tender type names |
| `RetailPosBatchTable` | Form (base) | Shift Tender Transactions screen |
| `AK_RetailPosBatchTenderTrans_Extension` | Class (extension) | Adds `AK_paymentMethodName()` display method |
| `AK_RetailPosBatchTable.Extension` | Form extension | Adds `AK_PaymentMethodName` column to the grid |

## Join Logic
```
RetailPosBatchTenderTrans.storeId      → RetailTenderTypeTable.storeId
RetailPosBatchTenderTrans.tenderTypeId → RetailTenderTypeTable.tenderTypeId
```

## Verification
1. Open **Shift Tender Transactions** (form `RetailPosBatchTable`).
2. Confirm "Payment method name" column appears after "Payment method" in the inner grid.
3. Verify correct names display; empty cell if no matching tender type record.
