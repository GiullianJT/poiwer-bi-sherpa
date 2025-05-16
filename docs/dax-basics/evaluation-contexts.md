# Evaluation Contexts & `CALCULATE`

Understanding **filter** and **row** context is key to mastering DAX.

---

## Filter Context

```DAX
Total US Sales =
    CALCULATE (
        [Sales Amount Measure],
        'Address'[Country/Region] = "United States"
    )
````

*`CALCULATE` replaces or adds filters before evaluating the expression.*

### Keeping outer filters

```DAX
Bike Sales (only Bikes) =
    CALCULATE (
        [Sales Amount Measure],
        KEEPFILTERS ( 'Product'[Product Category] = "Bikes" )
    )
```

---

## Row Context

Row context exists automatically in **calculated columns** but **not** in measures.

```DAX
Line Cost =
    SUMX (
        Sales,
        Sales[Quantity] * RELATED ( 'Product'[Cost] )
    )
```

### Accessing “many-side” rows

```DAX
Product Line Total =
    SUMX ( RELATEDTABLE ( Sales ), Sales[Line Total] )
```

---

## The Power of `CALCULATE`

`CALCULATE` can replace iterator patterns and often performs better.

```DAX
Total Yearly US Sales =
    CALCULATE (
        [Sales Amount Measure],
        ALL ( 'Product'[Product Model] ),
        'Address'[Country/Region] = "United States"
    )
```

---

### Outer-context example

```DAX
Total Yearly US Sales (dynamic) =
    VAR YrFilters = ALL ( 'Product'[Product Model] )
RETURN
    CALCULATE (
        [Sales Amount Measure],
        YrFilters,
        'Address'[Country/Region] = "United States"
    )
```

````

---