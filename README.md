# Flexi Technical Code Reviewer — Gold Standard Web App

A modern, high-performance web application designed for technical code review of **Intellinum Flexi Mobility** screen definitions (`.json` files) against the **8 Gold Technical Review Parameters**.

Preloaded with the full review of **`FUSION_PO_RECEIPT.json`** (73 findings) and equipped with a real-time browser engine to upload and analyze any Flexi screen JSON on the fly.

---

## 🚀 Features

- **Interactive Findings Dashboard**:
  - Filter across all 8 parameters with live metric counters.
  - Search by Component, Field, Event, Location, Issue, or Suggested Fix.
  - One-click **Copy Fix** button to easily transfer solutions into your codebase.
  - Export full reports in **CSV (Excel-ready)**, **Markdown**, or **JSON**.
- **Live Client-Side Analyzer**:
  - Drag and drop or browse any `.json` Flexi screen file.
  - Evaluates all components, WebServices, LOVs, scripts, and event handlers in real time.
- **Applied Review Exceptions & Clarifications**:
  - Dynamic runtime variables (`${VARIABLE_NAME}`) are recognized and not flagged as hardcoding.
  - Display durations in `flexi.setStatusMessage("...", <duration>)` are exempt.
  - Business logic filter literals (`contextCode`, `DefaultType=2`) are exempt.
  - Server-side LOV limit/pagination is handled by the platform and exempt from `limit` checks.

---

## 📦 Deploying to Vercel

This repository is pre-configured with `vercel.json` and static routing for **instant, zero-configuration deployment** to Vercel.

### Option 1: Deploy with Vercel CLI

```bash
# Navigate to the app directory
cd "d:/Intellinum Flexi Projects/AntiGravity Projects/flexi-code-reviewer"

# Deploy to Vercel
npx vercel
```

### Option 2: Deploy via GitHub / GitLab / Bitbucket

1. Push this directory (`flexi-code-reviewer`) to your Git repository.
2. Go to [vercel.com/new](https://vercel.com/new).
3. Import your repository and click **Deploy**.
4. Vercel will automatically detect the static project and deploy it within seconds with a live global URL (e.g. `https://flexi-code-reviewer.vercel.app`).

### Option 3: Drag & Drop via Vercel Dashboard

1. Log into your [Vercel Dashboard](https://vercel.com/dashboard).
2. Drag and drop the `flexi-code-reviewer` folder directly into the deployment area.

---

## 💻 Running Locally

### Method A: Direct Browser Preview
Double-click `index.html` or open it in any web browser (Chrome, Edge, Firefox, Safari).

### Method B: Local Static Server
```bash
cd "d:/Intellinum Flexi Projects/AntiGravity Projects/flexi-code-reviewer"
npx serve .
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 📋 The 8 Review Parameters

1. **Hardcoding and Latest Library Version Check**: Flags hardcoded URLs, outdated HCM versions (`11.13.18.05`), deprecated REST Framework versions (`REST-Framework-Version: 2`).
2. **API Structure**: Enforces `limit`, `onlyData=true`, and `fields` projection on standalone script-called WebServices. Checks HTTP operations (`POST` for transaction/print APIs).
3. **LOV Field Smart Search Enablement**: Checks all LOV components for `_smartSearch` configuration.
4. **Object Reference Check**: Flags calls to non-existent components (`PROJECT_LOV`, `TASK_LOV`), unsafe chained `.getValue().replace()`, `.parseDouble()`, and `.getString()` calls without `.has()`.
5. **Missing Exception Handling**: Ensures API calls, JSON parsing, and numeric conversions are enclosed in `try-catch` blocks and prevents swallowed errors.
6. **Field Dependency Check**: Verifies parent-to-child cascading field resets (`PO_NUM`, `PROJECT_NUMBER`, `SUBINVENTORY`, `SERIAL_TYPE`).
7. **Memory Leak / Garbage Collector (Objects)**: Verifies cleanup of session/flexi objects upon CANCEL, page entry, and transaction submission.
8. **Logging**: Prevents sensitive employee/payload data leakage in `logger.info`, corrects log levels (`warn` vs `debug`), and checks for documentation comments.
