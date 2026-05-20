# ZenseAI.QI Cookbook

The release hub and capability guide for the **ZenseAI.QI** AI-powered Quality Engineering workflow.

🌐 **Live site:** <https://qe-coe.github.io/zenseaiqicookbook/>

## Local preview

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Open <http://localhost:8000>.

## Adding screenshots

Drop PNGs in `docs/assets/img/` and reference them as:

```markdown
![Alt text](../assets/img/<filename>.png)
*Caption text.*
```

Search the docs for `<!-- SCREENSHOT:` to find every placeholder waiting for a capture.

## Publishing

Push to `main` → the `Deploy docs` GitHub Action builds with `mkdocs build --strict` and publishes to GitHub Pages.

---

© 2026 Zensar QE CoE
