# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Two connected projects that together form the digital business card system for Satyajit v Dutta, Founder & CEO of Pithonix AI:

- **`digital_visiting_card/`** — Static GitHub Pages site at `card.pithonix.ai`. Single `index.html` file. No build step.
- **`card-api/`** — Vercel serverless API at `card-api-lemon.vercel.app`. Receives form submissions from the card and forwards to Formspree for email notification.

## Deployment

**Card (GitHub Pages):**
```
git add index.html
git commit -m "..."
git push origin main
```
GitHub Pages auto-deploys from `main`. Live within ~2 minutes. Always `git pull origin main --no-rebase -X ours` before pushing — the repo is sometimes edited directly on GitHub.

**API (Vercel):**
```
cd card-api
npx vercel deploy --prod --yes --scope satyajit-duttas-projects
```
Vercel CLI is authenticated as `satyajitdutta-4426`. No login needed.

## Lead capture pipeline

When a visitor submits the gate form on the card:

1. **Browser** POSTs to `https://card-api-lemon.vercel.app/api/lead` (primary)
2. **Browser** also POSTs directly to Web3Forms (`access_key` in `index.html`) as backup email notification
3. **Vercel API** (`card-api/api/lead.js`) forwards server-side to Formspree `mvzwkqyl`

All three deliver to `satyajitv.d@pithonix.ai`. Web3Forms only works browser-side (free plan blocks server-side calls).

## Environment variables

`WEB3FORMS_KEY` is stored as a Vercel environment variable on the `card-api` project. It is also hardcoded in `index.html` as the Web3Forms access key — this is intentional and safe (Web3Forms public keys are designed to be client-side).

## Key facts

- Owner: **Satyajit v Dutta** — always use this exact name everywhere (title, vCard, payloads, copy). Never "Satyajit Dutta", never "Jeet".
- Business mobile: +91 96526 40505 (calls). WhatsApp only: +91 99030 89000.
- Official email: satyajitv.d@pithonix.ai
- The vCard downloaded via "Save to Contacts" is generated entirely client-side in `index.html` — no server involved.
- `arun.html` is a separate card for Arun Kumar Sahu (advisor). Same structure as `index.html`.
