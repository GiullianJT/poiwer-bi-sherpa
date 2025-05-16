# 🔑 Columns & Surrogate Keys Lab

> **Goal:** add surrogate keys to every dimension, push them onto the fact,  
> build a couple of slicer columns, and lock down correct data types.

---

## 📋 Prerequisites

* You completed **Tables & Normalization**—so you have six tables:  
  `Product`, `Supplier`, `SalesPerson`, `Account`, `Sales`, `MeasureTable`.  
* Power Query Editor is still open (`Home ▸ Transform Data`).

---

## 1 · Create surrogate keys on dimension tables

Surrogate keys improve performance, manage granularity, and shrink model size—exactly the three reasons Microsoft favors them:contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}.

1. **Product**  
   * Queries pane → **Product** → **Add Column ▸ Index Column**  
   * Rename `Index` → **Product ID**
2. **Supplier**, **SalesPerson**, **Account**  
   * Repeat the same four clicks; rename to **Supplier ID**, **Sales Person ID**, **Account ID** respectively:contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}.

!!! tip
    Surrogate keys always start life in the **dimension** table; the fact just borrows them.

---

## 2 · Push keys onto the fact table

Dim keys must live on the **Sales** fact before we can build relationships.

1. Queries pane → **Sales**  
2. **Home ▸ Merge Queries**  
3. In the dialog pick **Supplier**; Ctrl-click `supplier` + `country` in *both* tables (multi-column join):contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}.  
4. **OK** → new column `Supplier.1` appears.  
5. Click the **expand** icon → deselect *Select All* → tick **Supplier ID** → **OK**.  
6. Repeat the merge / expand routine for **Product**, **SalesPerson**, **Account** so Sales ends with four ID columns:contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}.

---

## 3 · Add calculated slicer columns (optional but handy)

Columns drive slicers; create two quick categorisers.

### Sales Team (on SalesPerson)

1. **SalesPerson** → **Add Column ▸ Conditional Column**.  
2. Build logic:  
   * *If* `sales_person` = **Jessica** → “Jessica Team”  
   * *Else* “Jaina Team” (feel free to adjust).  
3. **OK**. Column `Sales Team` appears.

### Sales Region (also on SalesPerson)

1. **Add Column ▸ Conditional Column** again.  
2. E.g. Pacific vs. Mountain vs. Central, etc.—choose your mapping.  
3. **OK**. Column `Sales Region` appears:contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}.

!!! note
    Only create calculated columns when you *need* new filter fields.  
    Numeric calcs belong in **measures**, not columns—measures add almost zero memory footprint:contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}.

---

## 4 · Fix data types

Power BI stores every character—pick slim types to save RAM.

| Table / Column | From ➜ To | Why |
|----------------|-----------|-----|
| `Sales[value]` | *Decimal* ➜ **Fixed Decimal Number** | rounds excess precision, fewer characters:contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13} |
| `Sales[order_date]` | *Date/Time* ➜ **Date** | drop useless “12:00:00 AM” noise:contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15} |

Steps: click the type icon on the header → choose the new type.

---

## ✅ Checkpoint

* **Product/Supplier/SalesPerson/Account** each have an `… ID` key.  
* **Sales** now holds the four ID columns.  
* **SalesPerson** contains `Sales Team` + `Sales Region`.  
* `value` shows 2 decimal places; `order_date` has no timestamp.

If your table list doesn’t match, retrace the step where it diverged.

---

!!! tip "Why bother with keys?"
    Relationships on short numeric IDs out-perform text joins, compress better,  
    and cut memory by orders of magnitude on large models:contentReference[oaicite:16]{index=16}:contentReference[oaicite:17]{index=17}.

Next up → **Relationships Lab** where we wire the tables together and let the star shine. 🌟
