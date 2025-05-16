# Functions in DAX — A Unified Reference

This file collects every function group used in **DAX Basics**.

---

## Aggregators

`SUM`, `AVERAGE`, `MIN`, `MAX`, `COUNT`, `DISTINCTCOUNT`, …

```DAX
Sum of Line Total = SUM ( Sales[Line Total] )
Min Start Date    = MIN ( 'Product'[Start Date] )
Average Line Total = AVERAGE ( Sales[Line Total] )
````

---

## Iterators

Aggregator “X” variants that accept **expressions**.

```DAX
Product Total Sales =
    SUMX (
        Sales,
        Sales[Line Total]
    )

First Sale Date =
    MINX (
        Sales,
        Sales[Order Date]
    )
```

---

## Counters

| Function          | Typical use      |
| ----------------- | ---------------- |
| `COUNT`, `COUNTA` | Non-blank rows   |
| `COUNTBLANK`      | Blanks only      |
| `COUNTROWS`       | Whole-table rows |
| `DISTINCTCOUNT`   | Unique values    |

```DAX
# Distinct Product Models =
    DISTINCTCOUNT ( 'Product'[Product Model] )
```

---

## Error Management

```DAX
Cost per oz =
    DIVIDE ( 'Product'[Cost], 'Product'[Weight] )          -- safest

Error? = ISERROR ( 'Product'[Cost per oz] )

Cost per oz (fallback) =
    IFERROR ( 'Product'[Cost] / 'Product'[Weight], BLANK () )
```

---

## Conditional Logic

```DAX
Large Sales (AND) =
    SUMX (
        FILTER (
            Sales,
            Sales[Quantity] > 2
                && Sales[Line Total] > 1000
        ),
        Sales[Line Total]
    )

Large Sales (IN) =
    SUMX (
        FILTER ( Sales, Sales[Quantity] IN { 1, 2 } ),
        Sales[Line Total]
    )
```

---

## Date Functions

```DAX
Year    = YEAR    ( Sales[Order Date] )
Month # = MONTH   ( Sales[Order Date] )
Weekday = WEEKDAY ( Sales[Order Date] )

First Day of Month =
    DATE ( YEAR ( Sales[Order Date] ), MONTH ( Sales[Order Date] ), 1 )
```

---

## Table Functions

```DAX
US & Canada Sales =
    SUMX (
        FILTER (
            Sales,
            RELATED ( 'Address'[Country/Region] ) IN { "United States", "Canada" }
        ),
        Sales[Line Total]
    )

All Sales =
    CALCULATE ( [Sales Amount Measure], ALL ( Sales ) )
```

---

## Statements & Variables

```DAX
Discounted Sales =
VAR DiscountPerc =
        1 - SELECTEDVALUE ( Discount[Value] )
RETURN
    [Sales Amount Measure] * DiscountPerc
```