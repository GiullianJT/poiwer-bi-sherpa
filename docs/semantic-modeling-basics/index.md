# 🏗️ Semantic Modeling Basics

> **Goal:** Build Power BI data models that are *performant*, *easy to use*, and *future-proof*.  
> You’ll start with a flat sales table and finish with a lean star-schema model that refreshes fast and delights report authors.

---

## 🎯 Learning objectives

By the end you’ll be able to:

1. Explain **why a good model matters** for speed, ease of development, and durability :contentReference[oaicite:15]{index=15}:contentReference[oaicite:16]{index=16}  
2. Identify and create the **four core components** of a model—tables, columns, relationships, measures :contentReference[oaicite:17]{index=17}:contentReference[oaicite:18]{index=18}  
3. Transform a denormalized table into a **fact table plus dimensions** (normalization).  
4. Add **surrogate keys** and calculated columns only when they improve slicing.  
5. Build **one-to-many, single-direction relationships** and know when to avoid bi-directional links.  
6. Use **measures** to keep the model slim and calculations flexible.  
7. Shrink model size with data reduction, compression, and a **proper date table**.  
8. Apply **user-friendly naming & organization** so business users aren’t lost.

---

## 🗺️ Course roadmap

| Module | Link | Hands-on? | Est. time |
|--------|------|-----------|-----------|
| 🟢 Setup & Files | [Getting started](intro-setup.md) | – | 10 min |
| 🟢 Tables & Normalization | [Break up the flat table](tables-normalization.md) | ✅ | 25 min |
| 🟢 Columns & Keys | [Surrogate keys + columns](columns-keys.md) | ✅ | 25 min |
| 🔵 Relationships | [Connect the dots](relationships.md) | ✅ | 30 min |
| 🔵 Measures | [Lightweight calcs](measures.md) | ✅ | 20 min |
| 🟣 Performance | [Shrink & speed up](performance.md) | ✅ | 30 min |
| 🟣 User-friendly Modeling | [Name, hide, organize](user-friendly.md) | ✅ | 20 min |

> **Legend:** 🟢 foundational&nbsp;&nbsp; 🔵 intermediate&nbsp;&nbsp; 🟣 advanced

---

## 🛠️ What you need

* **Power BI Desktop** (latest)  
* Sample file **`Example Tables - v2.xlsx`** ➜ see *Getting started* module for download link.  
* Coffee optional but recommended.

---

## 📂 Assets & downloads

Shared images, icons and supplemental scripts live under  
`/_shared/` → use relative links like:

```markdown
![Star schema](/_shared/images/star-schema.png)
