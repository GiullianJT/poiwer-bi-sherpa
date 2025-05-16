# Measures

Measures are the preferred way to perform calculations in Power BI because they’re
*evaluated on demand* rather than stored in the data model. Smaller models usually mean
better performance.

!!! note "Measures need context"
    Unlike Excel formulas, every DAX measure is evaluated **in a filter context**.  
    That’s why you’ll often see aggregators (e.g. `SUMX`) wrapped around row-level math.

---

## Creating Your First Measure

1. In **Modeling ▸ New Measure**, type:

    ```DAX
    Sales Amount Measure =
        SUMX (
            Sales,
            Sales[Quantity] * Sales[Unit Price]
        )
    ```

2. `SUMX` iterates each row of **Sales**, multiplies *Quantity* × *Unit Price*, and then
   sums the results.

---

## When *not* to use a measure

* Categorising rows (use a **calculated column** instead).  
* Filtering data (model relationships & filters do that).  
* Fixing a bad model (clean the model first!).

---

## Organising Measures

### Measure table

1. **Home ▸ Enter data** → name it `Measures` → leave it empty → **Load**.  
2. Add at least one measure, then hide the lone column.  
   The table icon changes to the “calculator” glyph.

### Display folders  
Right-click any measure ➜ *Display Folder* to group logically (e.g. “Financial KPIs”).

---

## Best-practice checklist

| ✅ Do | ❌ Don’t |
|------|--------|
| Use measures for numbers & equations | Materialise numbers in columns unless required |
| Keep names unique & descriptive | Mix camelCase and spaces arbitrarily |
| Store measures in a dedicated table | Scatter them across many tables |
