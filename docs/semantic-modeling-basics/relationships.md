# 🔗 Relationships Lab

> **Goal:** wire your star-schema together with **One-to-Many, one-directional, active** relationships—  
> then explore what happens when you bend (or break) those rules.

---

## 📋 Prerequisites

* Dimension tables now contain surrogate keys (`… ID`).  
* The **Sales** fact inherits those keys.  
* You’ve clicked **Close & Apply** and loaded the model into Power BI Desktop. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}  

---

## 1 · Inspect the AI-generated relationships

1. Switch to **Model view** (left rail).  
2. Hover each line: the paired key columns are highlighted.  
   You’ll notice the AI chose some *non-ID* columns—let’s fix that. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  

---

## 2 · Replace weak keys with surrogate keys

1. **Manage relationships** (Home ▸ Manage).  
2. Select a relationship that isn’t using an `… ID` column → **Edit**.  
3. In the pop-up, change both sides to the corresponding `… ID`.  
4. **OK** → repeat until every dimension-fact relationship uses an ID. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}  

> **Why?** Text keys work, but numeric surrogate keys compress better and query faster on big models.

---

## 3 · Review key cardinality

With all IDs in place you should see **1⟶*** arrows (One on the dimension, Many on the fact).  
Cardinality is driven by uniqueness of the key column values. :contentReference[oaicite:6]{index=6}:contentReference[oaicite:7]{index=7}  

!!! tip
    A single duplicate in the “One” side flips the symbol to * – instantly turning the join into Many-to-Many.

---

### Quick experiment – break & fix a key

1. **Right-click** the line between **Product** and **Sales** → **Properties**.  
2. Switch the key on **Product** from `Product ID` to `product_type` → **OK**.  
   *Cardinality flips to Many; arrow disappears.*  
3. Head to **Report view**, open the *Relational Model Test* page—see the visual fail. :contentReference[oaicite:8]{index=8}:contentReference[oaicite:9]{index=9}  
4. Fix it: revert the key to `Product ID` and refresh the page.

---

## 4 · Explore filter direction

By default arrows point from the **1** (dimension) to the **\*** (fact).  
Let’s see why bi-directional is dangerous.

1. In **Model view**, **right-click** the line **Supplier → Sales** → **Properties**.  
2. Change **Cross filter direction** to **Both** → **OK**. :contentReference[oaicite:10]{index=10}:contentReference[oaicite:11]{index=11}  
3. Back in the test report, slicers now behave unpredictably (Sales filters Supplier, etc.).  
4. Revert direction to **Single**.

> Bi-directional joins add CPU cost and can multiply ambiguity—stick with one-directional unless you *really* need the other way. :contentReference[oaicite:12]{index=12}:contentReference[oaicite:13]{index=13}

---

## 5 · Active vs. inactive relationships

1. **Right-click** the **Account → Sales** line → **Properties** → uncheck **Make this relationship active** → **OK**. :contentReference[oaicite:14]{index=14}:contentReference[oaicite:15]{index=15}  
2. Visuals that used Account fields now break—inactive lines (dotted) do *nothing* unless activated in DAX (`USERELATIONSHIP`).  
3. Reactivate it to restore the report.

---

## 6 · Validate the finished star schema

* One active, one-directional line from every **dimension** to **Sales**.  
* No fact-to-fact or dimension-to-dimension active joins.  
* Every arrow points *into* the fact.  

This structure is what Microsoft calls the **most performant** setup. :contentReference[oaicite:16]{index=16}:contentReference[oaicite:17]{index=17}  

---

## ✅ Checkpoint

| Check | Expectation |
|-------|-------------|
| Keys  | `Product ID`, `Supplier ID`, `Sales Person ID`, `Account ID` used on every join |
| Cardinality | `1` on dimensions, `*` on **Sales** |
| Direction | Single (dimension ⟶ fact) |
| State | Solid lines (active) |

If any line shows **Both**, dotted, or `*⟶*`, revisit steps above.

---

!!! warning "Bad joins ≠ small mistakes"
    Wrong cardinality or direction can silently inflate result sets, wreck totals,  
    and slow queries. Treat relationship edits as **model-breaking** changes—validate visuals afterwards.

Great—your model now filters correctly and performs well. Next: dive into the **Measures Lab** to calculate real insight without ballooning model size. 🚀
