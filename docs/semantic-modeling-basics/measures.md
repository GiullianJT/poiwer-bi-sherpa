# 🧮 Measures Lab

> **Goal:** create reusable calculations that live *outside* your tables, keep  
> the model slim, and leverage filter context instead of row context.

---

## 📋 Prerequisites

* You finished the **Relationships Lab** – the star schema is solid.  
* A blank **MeasureTable** exists (one dummy column, load-enabled). :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## 1 · Why measures beat calculated columns

| Aspect | Calculated Column | Measure |
|--------|------------------|---------|
| Storage | Materialised → uses RAM | Virtual → zero RAM |
| Context | Row context | Filter context |
| Refresh cost | High (re-compute per row) | Low (only at query time) |
| Flexibility | Fixed value | Reacts to slicers/filters |

Microsoft’s own guidance: **measures for numbers, columns for categories**. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## 2 · Create your first measure

1. Select **MeasureTable** → **Modeling ▸ New Measure**.  
2. Enter & press **Enter**:

    ```DAX
    Total Sales :=
        SUM ( Sales[amount] )          -- straight aggregate
    ```

3. Format as **Currency ($)** in the ribbon.

!!! tip
    Storing every measure in a *dedicated* table keeps them easy to find and document. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}

---

## 3 · Add a cost measure (iterator pattern)

Because *cost* = `quantity × unit_cost`, we need row-by-row math.

```DAX
Total Cost :=
    SUMX (
        Sales,
        Sales[quantity] * Sales[unit_cost]
    )
````

*`SUMX` creates a **row context**, multiplies each row, then sums the lot.*&#x20;

---

## 4 · Profit & profit margin (measure branching + variables)

### Profit

```DAX
Profit :=
    [Total Sales] - [Total Cost]
```

### Profit Margin

```DAX
Profit Margin % :=
VAR _sales   = [Total Sales]
VAR _profit  = [Profit]
RETURN
    DIVIDE ( _profit, _sales )
```

*Branching* (re-using measures) keeps logic DRY, variables improve readability.&#x20;

Format **Profit Margin %** as *Percentage with 1 decimal*.

---

## 5 · Quick Measure demo (if time permits)

1. **Modeling ▸ Quick Measure**.
2. Choose **Year-to-date (YTD total)**.
3. Base value = **Total Sales**; date = `Date[date]`.
4. Click **Add** → Power BI auto-generates a `TOTALYTD` measure:

   ```DAX
   Total Sales YTD :=
       CALCULATE (
           [Total Sales],
           DATESYTD ( 'Date'[date] )
       )
   ```

Inspect the produced code; notice `CALCULATE` injects a time filter.
Quick Measures are a teaching aid—clean up names & keep only what you understand.&#x20;

---

## 6 · Dynamic KPI titles (bonus)

```DAX
Title – Selected Person :=
"Sales KPIs – " &
IF (
    ISFILTERED ( SalesPerson[Sales Person] ),
    SELECTEDVALUE ( SalesPerson[Sales Person] ),
    "All Sales People"
)
```

Use it in a **card visual** and set the visual’s title field to this measure.

---

## ✅ Checkpoint

| Item          | Expectation                                                               |
| ------------- | ------------------------------------------------------------------------- |
| MeasureTable  | Contains **Total Sales**, **Total Cost**, **Profit**, **Profit Margin %** |
| Formatting    | Currency & percentage applied                                             |
| Quick Measure | `Total Sales YTD` present (optional)                                      |
| Report test   | Drag **Profit Margin %** into a table → slices correctly by any dimension |

If numbers look off, double-check **relationships** and that you used measures, *not* new columns.

---

!!! warning "Common anti-patterns"
\* **SUMX over dimension** – iterate the fact, not a lookup table.
\* **Hard-coding filters in measures** – prefer slicers or `CALCULATE` with parameters.

Your calculations are now centralized, lightweight, and context-aware.
On to the **Performance Lab** to make the model lean & fast! 🚀

```