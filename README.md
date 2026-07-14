# EDM+ Implementation Training Pack (Notebooks)

## Before You Start

You need:
1. A LUSID domain with JupyterHub access
2. A Personal Access Token (PAT)

### How to get a PAT:
1. Log into your LUSID domain (e.g. https://your-domain.lusid.com/app)
2. Click your profile icon (top right corner)
3. Click **Personal Access Tokens**
4. Click **Create**, give it a name, copy the token

## Setup

### Step 1: Open JupyterHub
In the LUSID sidebar, click **Additional tools → Jupyter Notebooks**.

### Step 2: Upload files
Upload all 7 `.ipynb` notebooks to `/home/jovyan/finbourne-notebooks/`.
The `data/` folder (all CSV and JSON files) is included in this repo — upload it
alongside the notebooks so it sits beside them.

### Step 3: Set up your credentials (once — all notebooks share this)
Copy `secrets.json.example` to `secrets.json` and fill in your domain and PAT:
```json
{
    "api_url": "https://<YOUR_DOMAIN>.lusid.com/api",
    "personal_access_token": "<YOUR_PAT>"
}
```
Replace `<YOUR_DOMAIN>` with your domain name and `<YOUR_PAT>` with your PAT token.
Every notebook reads this one file, so you only edit credentials once.
`secrets.json` is gitignored — never commit your real token.

> Put `secrets.json` beside the notebooks. To keep it elsewhere, set the
> `EDM_SECRETS_PATH` environment variable to its path.

### Step 4: Open NB01
Double click `NB01_Foundation_Setup.ipynb`.

### Step 5: Select the right kernel
In the top right corner, make sure it says **Python (SDK v3)**.
If it says something else, click it and select Python (SDK v3).

### Step 6: Run All
Click **Run → Run All Cells**. Watch the output.

### Step 7: Repeat for NB02 through NB07
Open each notebook in order and Run All. No per-notebook editing needed —
they all read `secrets.json`.

## What Each Notebook Creates

| Notebook | Creates |
|----------|---------|
| NB01 | 6 data types, ~60 properties, 5 derived properties |
| NB02 | 308 instruments (equities, bonds, ETFs, options, FX, private) |
| NB03 | 14 portfolios, 221 transactions |
| NB04 | 226 issuers, 69 instrument links, 314 hierarchy |
| NB05 | ~8,430 quotes |
| NB06 | 4 Luminesce reports |
| NB07 | Derived property proof + 4 DQ workflow tasks |

## Troubleshooting

**ModuleNotFoundError**: The first cell installs packages. Make sure you run it first.

**"You need to edit secrets.json"**: You did not create `secrets.json` (copy it from `secrets.json.example`) or you left the `<YOUR_DOMAIN>`/`<YOUR_PAT>` placeholders in it.

**FileNotFoundError: secrets.json**: The notebook can't find `secrets.json`. Put it beside the notebooks, or set `EDM_SECRETS_PATH` to its full path.

**Kernel says "Python 3 (ipykernel)"**: Click the kernel name (top right) and select **Python (SDK v3)**.

**"AlreadyExists" messages**: Safe to ignore. Notebooks are idempotent.
