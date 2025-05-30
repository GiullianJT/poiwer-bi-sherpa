Below is a practical “ **Quick-Start Guide** ” you can paste into any new repository’s `README.md`.
It captures **everything you need** to spin up a fresh MkDocs-Material site—with image zoom—on any machine in under five minutes.

---

# 🚀 Quick-Start Guide — Fabric Copilot Docs

> **Prerequisites**
>
> * Python 3.9 + installed and on PATH
> * Git (CLI)
> * (Optional) VS Code with the Python extension

---

## 1.  Clone (or init) the repo

```bash
# Clone an empty GitHub repo you just created
git clone https://github.com/<org>/fabric-copilot-docs.git
cd fabric-copilot-docs
```

> **Already in a folder?**
> `git init && git remote add origin <url>` works the same.

---

## 2.  Create & activate a virtual environment

```bash
python -m venv .venv          # create
# Windows PowerShell
.venv\Scripts\Activate.ps1
# macOS / Linux
# source .venv/bin/activate
```

> **First time PowerShell users**
> If you see *“running scripts is disabled”*, run an **Admin** shell once:
>
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```

---

## 3.  Install required packages

```bash
pip install mkdocs mkdocs-material mkdocs-glightbox
```

Freeze the exact versions:

```bash
pip freeze > requirements.txt
```

Commit:

```bash
git add requirements.txt
git commit -m "Pin Python dependencies"
```

---

## 4.  Add a .gitignore

```gitignore
# Python
.venv/
__pycache__/
*.py[cod]

# MkDocs build output
site/

# VS Code
.vscode/
```

```bash
git add .gitignore
git commit -m "Add standard Python/MkDocs .gitignore"
```

---

## 5.  Drop in minimal content

```
docs/
└─ index.md
```

`docs/index.md`

```md
# Fabric Copilot Lab
Welcome!  Click any screenshot to zoom.
```

---

## 6.  Create `mkdocs.yml`

```yaml
site_name: Fabric Copilot Lab
theme:
  name: material

plugins:
  - search
  - glightbox      # image light-box (auto-applies to all images)

markdown_extensions:
  - toc
  - tables
  - fenced_code
```

Commit:

```bash
git add docs mkdocs.yml
git commit -m "Initial site skeleton with glightbox plugin"
```

---

## 7.  Preview locally

```bash
mkdocs serve
```

Visit **[http://127.0.0.1:8000](http://127.0.0.1:8000)**.
Add an image in `docs/index.md` and verify it zooms on click.

---

## 8.  Push to GitHub

```bash
git push -u origin main   # or 'master'
```

*(Later, add a GitHub Actions workflow or manual `mkdocs gh-deploy` to publish to `gh-pages`.)*

---

### 🔁 Re-creating the environment on any computer

```bash
git clone https://github.com/<org>/fabric-copilot-docs.git
cd fabric-copilot-docs
python -m venv .venv
.venv\Scripts\activate         # or source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Enjoy a conflict-free, reproducible MkDocs setup with clickable screenshots!
