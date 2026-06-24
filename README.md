# SR-API-Package — API Documentation

Interactive API documentation for **Super RAG API**, hosted on GitHub Pages via Swagger UI.

- **Live site:** https://cinnamon.github.io/SR-API-Package/
- **Stack:** GitHub Pages + [Swagger UI](https://github.com/swagger-api/swagger-ui) (auto-updated daily via CI)

---

## Repository structure

```
SR-API-Package/
├── apis.json               ← homepage config — add/hide specs here
├── index.html              ← home page (do not edit)
├── swagger.html            ← Swagger UI viewer (do not edit)
├── swagger.yaml            ← active spec (loaded by default)
├── SR-3.4-CwDTCAE.yaml
├── SR-3.3.yaml
├── SR-3.2.yaml
├── SR-3.0.yaml
├── dist/                   ← Swagger UI assets (managed by CI)
└── .github/workflows/
    └── update-swagger.yml  ← daily auto-update workflow
```

---

## How to add a new spec

### Step 1 — Copy the YAML file to the repo root

```bash
cp path/to/SR-3.5.yaml .
git add SR-3.5.yaml
git commit -m "add SR-3.5 spec"
git push
```

### Step 2 — Register it in `apis.json`

Open `apis.json` and add a new entry to the array:

```json
{
  "id": "sr-3.5",
  "title": "Super RAG API — SR 3.5",
  "version": "v3.5.0",
  "badge": "Latest",
  "file": "SR-3.5.yaml",
  "description": "Confluence Page: https://..."
}
```

| Field | Description |
|---|---|
| `id` | Unique identifier (kebab-case) |
| `title` | Display title on the home page card |
| `version` | Version label shown on the card |
| `badge` | `"Latest"` (green) · any string (purple) · `null` (no badge) |
| `file` | Filename of the YAML in the repo root |
| `description` | Short description or Confluence link shown on the card |

> The order of entries in the array determines the display order on the home page.

---

## How to update the active spec (`swagger.yaml`)

`swagger.yaml` is the fallback spec loaded when opening `swagger.html`
without a `?url=` parameter.

```bash
cp SR-3.5.yaml swagger.yaml
git add swagger.yaml
git commit -m "update active spec to SR-3.5"
git push
```

---

## How to hide a spec from the home page

Remove the corresponding object from `apis.json` and push. The YAML
file remains in the repo and is still accessible via a direct URL
(`swagger.html?url=SR-3.x.yaml`), but will no longer appear on the
home page.

---

## Swagger UI auto-update

The CI workflow (`.github/workflows/update-swagger.yml`) runs daily
and opens a pull request when a new Swagger UI release is available.
Merging the PR updates the `dist/` assets and `swagger.html`.

`index.html` and `apis.json` are **never touched** by the CI workflow.
