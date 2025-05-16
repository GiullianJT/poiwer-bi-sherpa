# 🚀 Getting Started & Setup

> Follow these steps **before** you open the first lab.  
> They give you the sample data and a blank Power BI file to work in.  
> Skipping them will break every lab that follows. 🙃

---

## 1 . Download the sample data

Grab **`Example Tables – v2.xlsx`** from JourneyTEAM’s public repo: https://github.com/JourneyTEAM-Public/BusinessIntelligence/raw/master/Example%20Tables%20-%20v2.xlsx


Save the file somewhere easy to find (e.g. `C:\PBI-Sherpa\example-tables.xlsx`). :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}

---

## 2 . Create a new Power BI Desktop file

1. Launch **Power BI Desktop** (latest version recommended).  
2. **File ▸ New** – a blank report opens.

---

## 3 . Connect to the Excel workbook

1. On the ribbon, choose **Get data ▸ Excel workbook**.  
2. Browse to `example-tables.xlsx` and **Open**.  
3. In the Navigator, tick the table **FlatTable** – you should see a ✓.  
4. Click **Load** (or **Transform Data** if you want to peek first). :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}  
5. Wait for the load spinner to finish.

---

## 4 . Save your PBIX

Save the file as **`semantic-modeling-labs.pbix`** in the same folder as the Excel workbook.  
You’ll reopen this one PBIX for every lab.

---

## 5 . Lab order matters

!!! warning
    The labs are **sequential**.  
    Skipping ahead will make later steps impossible because tables, columns, or relationships won’t exist yet. :contentReference[oaicite:4]{index=4}:contentReference[oaicite:5]{index=5}

Recommended flow:

| Step | Module (Markdown file) |
|------|------------------------|
| 1 | `tables-normalization.md` |
| 2 | `columns-keys.md` |
| 3 | `relationships.md` |
| 4 | `measures.md` |
| 5 | `performance.md` |
| 6 | `user-friendly.md` |

---

### Need help?

* Retrace your steps first—most issues come from a missed click.  
* Still stuck? Open a GitHub issue or ping the #powerbi-sherpa channel.

Good to go? Head over to **Tables & Normalization** and start breaking up that flat file! 🏗️
