# Time Intelligence

These patterns require a **marked date table** with contiguous dates.

---

## Built-in Period-to-Date

```DAX
MTD Sales Amount =
    CALCULATE ( [Sales Amount Measure], DATESMTD ( 'Date'[Date] ) )

QTD Sales Amount =
    TOTALQTD ( [Sales Amount Measure], 'Date'[Date] )

YTD Sales Amount =
    TOTALYTD ( [Sales Amount Measure], 'Date'[Date] )
````

---

## Rolling Three-Month Total

```DAX
3-Month Sales =
VAR LastMonth      = EOMONTH ( MAX ( 'Date'[Date] ), -1 )
VAR ThreeMonthsAgo = EOMONTH ( MAX ( 'Date'[Date] ), -4 ) + 1
RETURN
    CALCULATE (
        [Sales Amount Measure],
        DATESBETWEEN ( 'Date'[Date], ThreeMonthsAgo, LastMonth )
    )
```

---

### Checklist for reliable time intelligence

1. **Date table marked as Date** (`Table Tools ▸ Mark as date table`).
2. One row per calendar date, no gaps.
3. Relationships from the Date table to fact tables set on the date key.

If those rules aren’t met, period functions will return unexpected blanks or totals.

```

---

**Next step:**  
Commit these files to your `docs/dax-basics/` folder, update `mkdocs.yml` nav, and
preview with `mkdocs serve`. Ping me once they’re in—happy to tweak wording or
convert more content!
```