# ⚡ Performance Lab

> **Goal:** shrink the model, speed up refresh & queries, and build the right
> infrastructure for long-term scale—without losing the business story.

---

## 0 · Prerequisites

* Star-schema model finished; measures exist in **MeasureTable**.
* You’re in **Power BI Desktop** with **Power Query Editor** open.  
  The **Sales** fact still contains many raw columns.

---

## 1 · Remove unnecessary columns & rows  *(Performant Lab A)*

1. **Queries pane → Sales**.  
2. Ctrl-select only the columns you still need:  
   `Product ID`, `Account ID`, `Sales Person ID`, `Supplier ID`,  
   `value`, `ship_date`, `order_date`.  
3. **Right-click header → Remove Other Columns**.  
   You just stripped all dead weight—one of the three big levers for speed. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  
4. **Group By** monthly granularity (assume reports only need month-level):  
   *Home ▸ Group By ▸ Advanced* →  
   *Group by* `order_month_start_date` →  
   *New column* **Sales Amount** = **Sum** of *value*.  
   Row count drops by ~50 %. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## 2 · Sort for maximum compression  *(still Lab A)*

Dictionary encoding loves long runs of repeated values.  
Sort low-cardinality columns first, then high. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}

Example:

1. **Queries pane → Sales**.  
2. Select `order_month_start_date` → **Sort Ascending**.  
3. Optional: sort `Product ID`, then `Supplier ID`.  

Power BI now packs identical values together → smaller column segments and faster scans. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

---

## 3 · Add a proper Date table  *(Performant Lab C)*

1. **Home ▸ Transform Data** to stay in Power Query.  
2. **Right-click Queries pane → New Query → Blank Query**.  
3. **Advanced Editor** → paste your favorite M calendar script (or Power BI’s `Calendar` function) → **Done**.  
4. Rename query **Calendar**.  
5. **Close & Apply**; in Model view drag **Calendar[Date]** onto **Sales[order_month_start_date]** to create the relationship.  
6. **Fields pane → Calendar (right-click) → Mark as date table → Date**. :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}  

Using a single date table lets you kill the invisible auto-generated ones and keeps slicing consistent. :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}  

---

## 4 · Disable Auto Date/Time  *(also Lab C)*

1. **File ▸ Options and settings ▸ Options → Current File ▸ Data Load**.  
2. Uncheck **Auto date/time for new files** → **OK**. :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13}  

Auto date/time spawns hidden tables for every date column—dead weight you don’t need once a real Calendar table exists.

---

## 5 · Re-measure model size (optional)

*Model view ▸ Table tools ▸ Properties* shows size per table.  
You should see noticeable drops after each step.

---

## ✅ Checkpoint

| Area | What to verify |
|------|----------------|
| **Sales** fact | Only IDs + value + dates; ~40 rows (monthly) |
| Sort order | Calendar date ascending; low-cardinality columns first |
| Calendar table | Related to Sales; marked as Date |
| Auto Date/Time | Disabled (Options) |

---

!!! tip "Three levers of performance"
    1. **Minimize data** – remove columns/rows, aggregate at needed grain.  
    2. **Compress smart** – sort columns so repeats cluster.  
    3. **Build the right infra** – date table, star schema, one-directional relationships.

Your model is now leaner, meaner, and ready for the **User-Friendly Lab** where we polish names, folders, and hiding rules. 🚀
