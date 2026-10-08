# Full-Stack Patch Exercise

A small, intentionally imperfect task tracker. Your job is to review the codebase, identify the highest-value issues, and submit a focused patch.

---

## Why this exercise

We want to see how you improve an existing codebase under a realistic timebox — not how much boilerplate you can generate. The strongest submissions are small, focused diffs paired with clear reasoning and genuine understanding.

We care about:

- **Judgment** — what you fix first and why
- **Debugging skill** — across frontend, backend, and SQL layers
- **Communication** — can you explain tradeoffs clearly?
- **Understanding** — do you actually understand what you changed and why?

We assume all candidates are using modern AI tools (ChatGPT, Claude, Copilot, etc.) — that is completely fine. What matters is that you understand the bugs you find, the fixes you apply, and can explain them in your own words and handwriting.

---

## Tech stack

| Layer    | Technology                      |
| -------- | ------------------------------- |
| Frontend | React 18 + Vite 5 (JavaScript) |
| Backend  | Spring Boot 3.2 + Java 17      |
| Database | H2 (in-memory, zero setup)     |
| SQL ref  | Oracle PL/SQL artifact in `db/` |

The Oracle PL/SQL file in `db/oracle/` is a reference artifact — it mirrors the app's query logic but does not run locally. You are welcome to review and improve it.

---

## Timebox

- **Spend no more than 90 minutes** (including setup, fixes, and write-up).
- AI tools are expected and completely fine to use.
- Judgment, clarity, and tradeoffs matter more than completeness.
- You are **not** expected to find or fix everything.

---

## What you are expected to do

1. **Run the app locally** (see setup instructions below — install dependencies first).
2. **Explore the codebase** — frontend, backend, SQL, and the Oracle artifact.
3. **Identify and fix** the highest-value issues you can find within the timebox.
4. **Keep changes focused** — a small, high-quality diff beats a large rewrite.
5. **Do not rewrite the app** — this is a patch exercise, not a rebuild.
6. **Add a `NOTES.md` file** at the project root (see below).
7. **Add handwritten explanations** — photographed and included in your repo (see below).

---

## Handwritten explanations (required)

For each bug you found and fixed, write an explanation **by hand on paper** covering:

- Where the bug is (file, line, layer)
- How you discovered it
- What the root cause is
- How you fixed it and why you chose that approach

Photograph or scan your handwritten notes and add the images to a `handwritten/` folder at the project root. Clear, legible handwriting is sufficient — we are not judging penmanship. We are verifying that you genuinely understand what you fixed and can explain it without relying on AI-generated text.

**Submissions without handwritten explanations will be considered incomplete.**

---

## What to include in NOTES.md

Write a short file (under 300 words) covering:

- **Summary of changes** — a brief overview of what you fixed (detailed explanations go in the handwritten notes)
- **What you chose not to change** and why
- **The biggest remaining risk** you see in this codebase
- **What tools/AI you used** and how (e.g., "used Claude to draft the debounce hook, then adjusted the delay")

Be honest and specific. We value self-awareness over perfection.

---

## Local setup

### Prerequisites

- **Java 17+** (run `java --version` to check)
- **Node.js 18+** (run `node --version` to check)
- No Docker required. No external database required.

### Backend

```bash
cd backend
./mvnw spring-boot:run
```

On Windows, use `mvnw.cmd spring-boot:run` instead.

The API starts on **http://localhost:8080**.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

The app starts on **http://localhost:5173**.

The Vite dev server proxies `/api/*` requests to the backend automatically.

---

## Run instructions

1. Start the backend first (port 8080).
2. Start the frontend second (port 5173).
3. Open **http://localhost:5173** in your browser.
4. To stop either service, press `Ctrl+C` in its terminal.

### Useful URLs

| URL                                        | Description           |
| ------------------------------------------ | --------------------- |
| http://localhost:5173                       | App UI                |
| http://localhost:8080/api/tasks             | API — all tasks       |
| http://localhost:8080/api/tasks?q=api       | API — search by term  |
| http://localhost:8080/api/tasks?status=OPEN | API — filter by status|
| http://localhost:8080/h2-console            | H2 database console   |

H2 console connection: JDBC URL `jdbc:h2:mem:taskdb`, username `sa`, no password.

---

## Quick smoke test

1. Open http://localhost:5173 — you should see a table of tasks.
2. Type a search term (e.g., "api") — results should filter.
3. Select a status from the dropdown — results should filter further.
4. Try the API directly:
   ```bash
   curl "http://localhost:8080/api/tasks?q=api&page=1&pageSize=5"
   ```

---

## Submission instructions

1. Click **"Use this template"** on the GitHub repo page to create your own copy (do **not** fork — use the template button).
2. Keep the folder structure and startup commands unchanged.
3. Make your changes and commit them.
4. Add your `NOTES.md` at the project root.
5. Add your handwritten explanation photos in a `handwritten/` folder at the project root.
6. Push to GitHub.
7. **Ensure the app still runs** with the same setup commands before submitting.
8. Share the **repo URL** with us.

---

## Submission timing

- **Earlier complete submissions are prioritized** in our review queue and interview scheduling.
- The ideal latest submission time is **within 48 hours** of receiving the assignment.
- Late submissions may be deprioritized in scheduling.

---

## Submission checklist

Before sharing your repo, verify:

- [ ] App runs with the original setup commands (`./mvnw spring-boot:run` and `npm run dev`)
- [ ] `NOTES.md` exists at the project root
- [ ] `handwritten/` folder exists with photos of your handwritten explanations
- [ ] Handwritten notes cover each bug you fixed (location, discovery, root cause, fix approach)
- [ ] Code changes are committed and pushed
- [ ] You have not accidentally included `node_modules/`, `target/`, or other build artifacts

---

## Interview follow-up

After we review your submission, we will schedule a short call. Be ready to discuss:

- What you fixed first and why you prioritized it
- What you chose not to fix
- Any subtle issues you found or suspected
- Any future risks you noticed in the codebase
- Your handwritten explanations — we may ask you to walk through them
- How you used AI/tools — where you accepted suggestions and where you overrode them
- How you would approach the issues differently with more time

---

## Troubleshooting

**Backend won't start**
- Ensure Java 17+ is installed: `java --version`
- On macOS, if you get `Permission denied`, run: `chmod +x backend/mvnw`
- On Windows, use `mvnw.cmd` instead of `./mvnw`
- Check that port 8080 is free: `lsof -i :8080` (macOS/Linux) or `netstat -ano | findstr :8080` (Windows)

**Frontend won't start**
- Ensure Node 18+ is installed: `node --version`
- Run `npm install` before `npm run dev`
- Check that port 5173 is free

**API returns errors in the browser console**
- Make sure the backend is running before the frontend
- The Vite proxy forwards `/api/*` to `localhost:8080` — if the backend is down, requests will fail

**H2 console won't connect**
- Use JDBC URL: `jdbc:h2:mem:taskdb`
- Username: `sa`, password: (leave blank)
- The console is only available while the backend is running

---

## Scope guidance

This codebase has issues at multiple levels — some obvious, some subtle, some that are really future risks rather than current bugs. **You are not expected to find or fix everything.** Focus on what you believe is highest value, explain your reasoning, and stop when the timebox is up.

Good luck.
#   n e w - p r o j e c t - t e s t i n g 



# Task Tracker Application

A small full-stack Task Tracker application built with **React, Spring Boot, and H2**.

This repository is a focused patch submission for a full-stack debugging exercise. The goal was to identify high-value issues across the SQL, backend, and API layers and make small, safe fixes without rewriting the application.

---

## Overview

The application allows users to:

- Search tasks by title or description
- Filter tasks by status
- View paginated task results
- Access task data through a REST API
- Store task data using an H2 database

### Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, Vite 5, JavaScript |
| Backend | Spring Boot 3.2, Java 17+ |
| Database | H2 |
| Persistence | Spring Data JPA |
| SQL Reference | H2 / Oracle SQL |

---

## Project Structure

```text
task-tracker/
│
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   └── resources/
│   │   ├── pom.xml
│   │   ├── mvnw
│   │   └── mvnw.cmd
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── App.jsx
│   │   └── api.js
│   ├── package.json
│   └── vite.config.js
│
├── db/
│   ├── queries/
│   └── oracle/
│
├── handwritten/
│   └── handwritten bug explanations
│
├── NOTES.md
└── README.md
```

---

# Bugs Identified and Fixed

## 1. SQL Search Precedence Bug

### Problem

The search query used `AND` and `OR` without grouping the title and description conditions.

Because SQL evaluates `AND` before `OR`, the original query could apply the `archived` and `status` conditions incorrectly.

### Fix

Grouped the search conditions using parentheses:

```sql
WHERE archived = FALSE
AND (
    LOWER(title) LIKE :term
    OR LOWER(description) LIKE :term
)
AND (:status IS NULL OR status = :status)
```

The same logical correction was applied to the SQL reference artifacts.

### Result

- Search results are more accurate.
- Archived tasks are correctly excluded.
- Status filtering is applied consistently.

---

## 2. API Input Validation

### Problem

Invalid pagination values such as:

```text
page=0
page=-1
pageSize=0
```

were not rejected properly.

Invalid status values could also cause an API error.

### Fix

Added validation for:

```text
page >= 1
1 <= pageSize <= 100
valid task status
```

Invalid requests now return:

```text
HTTP 400 Bad Request
```

### Result

The API handles invalid client input more safely and predictably.

---

## 3. Artificial API Delay

### Problem

The request path contained an artificial delay using `Thread.sleep()`.

This caused every API request to wait unnecessarily.

### Fix

Removed the artificial delay.

### Result

API requests can now complete without the unnecessary wait.

---

# Existing Frontend Protections Verified

During the review, I also checked the frontend for two potential issues.

### Pagination Reset

The application already resets pagination when search or status filters change:

```javascript
setPage(1);
```

Therefore, no additional change was required.

### Stale Search Requests

The application already uses `AbortController` to cancel previous requests.

This prevents an older search response from incorrectly replacing a newer result.

Therefore, no additional change was required.

---

# Testing

The application was checked using the existing startup process and the main task-search flows.

### Manual checks

- Task list loads successfully
- Search by title/description
- Status filtering
- Search + status filtering
- Pagination
- Invalid pagination parameters
- Invalid status input
- API response behavior

Example API request:

```text
http://localhost:8080/api/tasks?q=api&page=1&pageSize=5
```

---

# Running the Application

## Prerequisites

- Java 17 or higher
- Node.js 18 or higher
- npm

No Docker or external database is required.

---

## Start the Backend

### Windows

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

### macOS / Linux

```bash
cd backend
./mvnw spring-boot:run
```

Backend:

```text
http://localhost:8080
```

---

## Start the Frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend:

```text
http://localhost:5173
```

Open the frontend URL in your browser.

---

# API

### Get tasks

```text
GET /api/tasks
```

### Search tasks

```text
GET /api/tasks?q=api
```

### Filter by status

```text
GET /api/tasks?status=OPEN
```

### Search + pagination

```text
GET /api/tasks?q=api&page=1&pageSize=5
```

---

# H2 Database

The application uses an in-memory H2 database.

H2 Console:

```text
http://localhost:8080/h2-console
```

Connection details:

```text
JDBC URL: jdbc:h2:mem:taskdb
Username: sa
Password: leave blank
```

---

# Scope and Trade-offs

This submission intentionally focuses on high-value correctness and API issues rather than rewriting the application.

I did not make broad architectural changes or redesign the UI because the exercise is time-boxed and the existing structure was sufficient for the required functionality.

One remaining risk is the lack of comprehensive automated tests around search, filtering, pagination, and invalid API input. With more time, I would add unit and integration tests for these cases.

---

# AI Usage

AI tools were used during the code review and debugging process to help identify potential issues, reason about SQL behavior, and review possible fixes.

All implemented changes were reviewed and understood before being applied.

The final changes were kept intentionally small and focused on the highest-value issues.

---

# Author

**Kavi**

Full-Stack Software Engineer Candidate







 
 
