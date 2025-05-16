# 🤝 User-Friendly Modeling Lab

> **Goal:** make your data model obvious, tidy, and safe for business users—  
> no cryptic names, no junk columns, no accidental self-joins.

---

## 📋 Prerequisites

* You’ve completed the **Performance Lab** (model is lean and fast).  
* A proper **Calendar** table exists and is marked as the date table.  
* All relationships are **One-to-Many, single-directional** (star schema).

---

## 1 · Rename tables & columns with business language

1. **Fields pane → F2** (or slow double-click) on each table name.  
   *Examples:*  
   * `Sales` ➜ **Sales Fact** (optional)  
   * `SalesPerson` ➜ **Sales People**  
2. Open **Model view**, single-click a column name, press **F2** → change to Title-Case with spaces.  
   *Examples:*  
   * `product_type` ➜ **Product Type**  
   * `order_month_start_date` ➜ **Order Month Start Date**  

Use terms your end users use—rename now to avoid “What’s prod_type again?” questions later. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## 2 · Organise measures and fields

### a) Measure folders  
1. In **Fields pane**, right-click **Profit Margin %** ➜ *Display Folder* → **Financial KPIs**.  
2. Do the same for **Total Sales, Total Cost, Profit**.  

### b) Table ordering  
Drag **MeasureTable** to the top of the table list (just for ergonomics).  
Group dimensions together beneath it (Product, Supplier, etc.). :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## 3 · Hide confusing or useless columns

1. Ctrl-select every **… ID** surrogate key in the dimension tables → **Hide in report view**.  
2. Hide any technical columns in **Sales** you left for compression purposes (e.g., `unit_cost`).  

Hidden fields still power relationships and measures but don’t clutter the field list. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  

---

## 4 · Hide whole tables if necessary

If you created helper queries (e.g., staging tables) that loaded to the model by accident:

1. **Model view → right-click table → Hide in report view**.  
   End users now see only the clean star schema. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

---

## 5 · Star-schema sanity check

* **Model view:** visually confirm *only* Fact-to-Dimension active lines exist.  
* No dotted lines (inactive) unless you added them on purpose.  
* Each arrow points into **Sales**.  

A visible star reassures authors that dragging any slicer will “just work.” :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}  

---

## 6 · (If skipped) expose Calendar columns

Give users rich date slicing:

1. Show `Calendar[Year]`, `Calendar[Month]`, `Calendar[Weekday]`.  
2. Keep the raw `Date` column visible for timeline visuals.  
3. Hide technical columns like `Day Offset`.  

Date tables are user-friendly *and* performant—never rely on the hidden Auto Date/Time tables. :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}  

---

## ✅ Checkpoint

| Area | Expectation |
|------|-------------|
| Names | Spaces + Title-Case, no cryptic abbreviations |
| Measures | Grouped into folders, easy to scan |
| Field list | Only business-relevant columns visible |
| Tables | Clear Fact + Dimensions cluster, helper tables hidden |
| Model | Clean star shape, single-direction arrows |

Open a blank report page → drag **Year**, **Product Type**, and **Profit Margin %** onto a matrix.  
If the matrix builds instantly and field names read naturally, mission accomplished.

---

!!! tip "Remember the mantra"
    *Know your users, speak their language, hide the rest.*  
    User-friendly models drive adoption—and reduce “what does this field mean?” tickets.

You’re done! Your Sherpa model is now **performant *and* pleasant to use.** 🎉
