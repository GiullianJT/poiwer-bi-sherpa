# Evaluation Contexts & `CALCULATE`

Understanding **evaluation context** is key to mastering DAX. There are two main types: **filter context** and **row context**. This guide explains both, with practical examples, and shows how `CALCULATE` can be used to manipulate these contexts for powerful analytics.

---

## 1. Filter Context

**Filter context** is created by filters applied in visuals, slicers, or explicitly in DAX formulas. It determines which data is visible to your measure. In this section, we use DAX expressions that do **not** use `CALCULATE` to demonstrate how filter context works naturally.

### Example: Implicit Filter Context

```DAX
Total US Sales :=
    SUMX (
        FILTER (
            Sales,
            RELATED('Address'[Country/Region]) = "United States"
        ),
        Sales[Sales Amount]
    )
```
*This measure only includes sales where the country/region is United States, using FILTER to create a filter context.*

### Using `ALL` to Remove Filters

```DAX
Total Sales (All Products) :=
    SUMX (
        ALL ( Sales ),
        Sales[Sales Amount]
    )
```
*The `ALL` function removes any filters from the Sales table, returning total sales regardless of slicer or visual filters.*

### Using `FILTER` for Custom Logic

```DAX
Total Bike Sales (Expensive Only) :=
    SUMX (
        FILTER (
            Sales,
            RELATED('Product'[Product Category]) = "Bikes" && RELATED('Product'[List Price]) > 1000
        ),
        Sales[Sales Amount]
    )
```
*The `FILTER` function allows you to apply more complex filter logic.*

---

## 2. Row Context

**Row context** exists automatically in calculated columns and iterator functions like `SUMX`. It refers to the current row being evaluated.

### Example: Calculated Column with Row Context

```DAX
Line Cost :=
    SUMX (
        Sales,
        Sales[Quantity] * RELATED ( 'Product'[Cost] )
    )
```
*Here, `SUMX` iterates over each row in Sales, multiplying quantity by the related product cost.*

### Accessing Related Rows

```DAX
Product Line Total :=
    SUMX ( RELATEDTABLE ( Sales ), Sales[Line Total] )
```
*`RELATEDTABLE` brings in all Sales rows related to the current Product row.*

---

## 3. The Power of `CALCULATE`

`CALCULATE` changes the filter context for an expression, allowing you to override, add, or remove filters. Here, we rewrite the Filter Context examples using `CALCULATE` for more flexibility and performance.

### Example: Forcing a Filter with `CALCULATE`

```DAX
Total US Sales =
    CALCULATE (
        [Sales Amount Measure],
        'Address'[Country/Region] = "United States"
    )
```
*This measure applies a filter for United States using CALCULATE.*

### Using `ALL` with `CALCULATE` to Remove Filters

```DAX
Total Sales (All Products) =
    CALCULATE (
        [Sales Amount Measure],
        ALL ( 'Product' )
    )
```
*This measure ignores any product filters, showing total sales.*

### Using `FILTER` with `CALCULATE` for Custom Logic

```DAX
Total Bike Sales (Expensive Only) =
    CALCULATE (
        [Sales Amount Measure],
        FILTER (
            'Product',
            'Product'[Product Category] = "Bikes" && 'Product'[List Price] > 1000
        )
    )
```
*`CALCULATE` applies the custom filter logic defined in the `FILTER` function.*

---

**Summary:**  
- **Filter context** is about which data is visible to your measure, and can be set with iterators and filter functions.
- **Row context** is about the current row being evaluated, usually in iterators or calculated columns.
- **CALCULATE** lets you change the filter context, making your measures more flexible and powerful.

---