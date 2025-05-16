# 🛠️ Tables & Normalization Lab

> **Goal:** turn the single **FlatTable** you imported into  
> *one* **Fact** table, *four* **Dimension** tables, and a tidy **Measures** table—  
> the core of a Power BI star-schema model.

---

## 🔎 Why Normalize?

Microsoft’s own guidance: star-schema models compress better, refresh faster, and simplify DAX— even though Power BI will denormalize “on the fly” during query time :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}.  
The memory you save by splitting text columns into small dimension tables vastly outweighs the CPU cost of re-joining them in the background.

---

## 0 · Prereqs

* You already loaded **FlatTable** from `example-tables.xlsx` (see *Getting Started*).  
* **Power Query Editor** is open (`Home ▸ Transform Data`).

---

## 1 · Create a Measures Table

1. **Home ▸ Enter Data**  
2. Rename the lone column to `Hide Me`.  
3. Rename the table (bottom-left) to `MeasureTable`.  
4. Click **OK**.  

You now have a blank table that will eventually hold measures only :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}.

---

## 2 · Disable Load on `FlatTable`

* In the Queries pane, **right-click FlatTable ▸ Enable Load** (it becomes unchecked & italic).  
  *This keeps the query available for references while stopping it bloating the model* :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}.

---

## 3 · Product Dimension

1. **Right-click FlatTable ▸ Reference** → new copy appears (named *FlatTable (2)*).  
2. Select columns `product` & `product_type` → **Remove Other Columns**.  
3. Select `product` header → **Remove Duplicates**.  
4. In **Query Settings** rename the query to `Product`.  

Granularity check: *one row per product*; `product_type` merely categorises the product and stays for convenience :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}.

---

## 4 · Supplier Dimension

1. Repeat steps 1-3 above.  
2. **Home ▸ Choose Columns** → select `supplier`, `country`.  
3. While both selected: **Remove Duplicates**.  
4. Rename query to `Supplier`.  

Keep both columns—some suppliers operate in multiple countries, so the grain is the *supplier + country* pair :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}.

---

## 5 · SalesPerson Dimension

* Reference **FlatTable** again, keep only `sales_person`, remove duplicates, rename to `SalesPerson` :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}.

---

## 6 · Account Dimension

* Reference **FlatTable**, keep `contact`, `store`, `account`, remove duplicates, rename to `Account` :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13}.

---

## 7 · Sales Fact

1. Reference **FlatTable** one last time.  
2. Rename query to `Sales`.  
3. No column removals yet—surrogate keys will be added in the next lab.  
   Fact grain already = one sales line, which we keep :contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15}.

---

## 8 · Apply & Close

* **Home ▸ Close & Apply** to push the new tables into the model (FlatTable remains query-only).  

You should now see **Product, Supplier, SalesPerson, Account, Sales, MeasureTable** in the *Fields* pane—ready for keys and relationships in the following labs.

---

## ✅ Checkpoint

| Item | Should look like… |
|------|------------------|
| *FlatTable* | *Italic* (load disabled) |
| Dimension tables | ≤ ~100 rows each, no duplicates |
| `Sales` fact | 80+ rows, all original columns |
| MeasureTable | One dummy column `Hide Me` (we’ll hide it later) |

If anything is off, retrace the specific step; 95 % of issues stem from missed “Remove Other Columns” or duplicate removal.

---

!!! tip "The shortcut you’ll use daily"
    **Right-click column header ▸ Remove Other Columns** is the fastest way  
    to isolate what you need in Power Query—burn it into muscle memory.

Next stop → **Columns & Keys** where we build surrogate keys and slim the fact.
