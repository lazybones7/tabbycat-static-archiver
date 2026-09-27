# Tabbycat Static Archiver

Strips everything public on a Tabbycat tournament site into flat static
HTML/CSS/JS and zips it for download. No login, no environment
variables required, since all the data it touches is public.

## Inputs

- **Tournament base URL**, e.g. `https://razm24.calicotab.com`, with or
  without a trailing slash.
- **Slug**, the tournament's slug exactly as in the URL, case
  sensitive.
- **Number of rounds**, defaults to 20. The archiver just tries rounds
  1 through this number and skips any that 404 (most tournaments don't
  have anywhere near 20 rounds, outrounds included). Raise it only if a
  tournament genuinely has more than 20 rounds.

## Running locally

```bash
pip install -r requirements.txt
playwright install chromium
streamlit run app.py
```

## Deploying on Render

1. Push this folder to a GitHub repo.

2. Click **Deploy to Render**

   [![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)
2. Render should detect the `Dockerfile` and offer Docker as the runtime.
3. Known concurrency limit: on Render's Starter plan (512MB RAM), plan
   for one archiving job at a time. Each job launches its own Chromium
   instance, so two people archiving at once risks an out-of-memory
   crash that kills the whole service for everyone using it.
