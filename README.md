# Haze Watch SG

Live haze and weather for Singapore and ASEAN cities. A static single-page app, no build step.

- Haze (PSI by North, South, East, West, Central; PM2.5 and PM10): NEA via data.gov.sg
- Weather for all cities and the 12-hour Singapore forecast: Open-Meteo

## Deploy on Vercel

1. Push this folder to a GitHub repository.
2. In Vercel choose Add New, then Project, and import the repository.
3. Framework Preset: Other. Leave build command empty. Output directory is already set to `public` in `vercel.json`.
4. Deploy.

Or from a terminal: `npx vercel` in this folder, then `npx vercel --prod`.

## How it works

- `public/index.html` holds the whole app.
- `vercel.json` rewrites `/api/nea/*` to `https://api-open.data.gov.sg/v2/real-time/api/*`, so the browser calls your own domain and avoids CORS problems. Responses are cached at the edge for 5 minutes, which keeps you well inside data.gov.sg rate limits.
- Open-Meteo is called directly from the browser. It needs no key for non-commercial use.

## Notes

- If NEA cannot be reached, the page shows an "unavailable" state. It never shows made-up numbers.
- Opening `public/index.html` directly from disk will not load NEA data, because `/api/nea` only exists on Vercel. Use `npx vercel dev` to test locally.
- Region boundaries on the map are approximate.
