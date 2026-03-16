# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A single-page Hebrew (RTL) web app for Shir Hadash synagogue congregants to look up their financial balance and transaction history. No server, no build tools — just `index.html`.

## How It Works

1. Fetches CSV data from a public Google Sheet via the gviz endpoint (`tqx=out:csv`)
2. Parses CSV client-side and groups ~4000 transaction rows by congregant name
3. Computes each person's balance by summing all their `מאזן` (balance) column values
4. Provides search with autocomplete, displays balance + transaction table
5. Saves last searched name to `localStorage` for return visits

## Data Source

- **Sheet ID**: `1124wmlh4n9MaZzZ9zpFz-Oj3q-AwKiNlD0wPOb_aIjI`
- **GID**: `570196390` (ungrouped sheet — has all individual transactions)
- **GID `1354519834`** is the grouped/pivot view (ציר) — only returns summary rows via gviz, not usable for transaction details
- Column layout: `0=מס', 1=מועד, 2=קניה, 3=נדר, 4=שם מתפלל, 5=שולם, 6=מאזן`

## Running Locally

Must be served over HTTP (not `file://`) due to Google Sheets CORS policy:

```
python3 -m http.server 8080
# then open http://localhost:8080/index.html
```

## Deployment

Hosted on GitHub Pages at https://shohamtal.github.io/shir-hadash/. Push to `main` triggers automatic deployment.
