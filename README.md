# MR Reporting Software – Frontend

A React-based web frontend for **MR Reporting Software**. The application provides public-facing pages and role-oriented interfaces for Admin, Manager, and Medical Representative (MR) workflows. It is built with React and Vite, styled with Tailwind CSS, and communicates with a separate backend API.

> **Important:** This repository contains the frontend only. API-driven features require the matching backend service and a correctly configured `VITE_API_BASE_URL`.

## Contents

- [Project Overview](#project-overview)
- [Main Modules](#main-modules)
- [Technology Stack](#technology-stack)
- [Requirements](#requirements)
- [Run the Project Locally](#run-the-project-locally)
- [Environment Configuration](#environment-configuration)
- [Useful Commands](#useful-commands)
- [Project Structure](#project-structure)
- [Authentication and API](#authentication-and-api)
- [Build and Deployment](#build-and-deployment)
- [Troubleshooting](#troubleshooting)
- [GitHub: First Upload](#github-first-upload)
- [Security Notes](#security-notes)

## Project Overview

MR Reporting Software is a web interface intended to support reporting and administrative workflows. The frontend includes public information pages, a login page, dashboards, master-data screens, approval workflows, expense and stock-statement screens, target management, and reporting pages.

### Main Modules

- **Public pages:** Home, About, Services, Contact, and Login.
- **Admin dashboard and profile:** Administrative navigation and dashboard screens.
- **Master data management:** User directory and creation, designations, areas, doctors/chemists, headquarters mapping, hierarchy, products, tour-program-related data, and CRM doctor mapping.
- **Approvals:** Master-data approvals, tour-program approvals, and STP approvals.
- **Expense-related screens:** Fare-rate card and state-wise daily allowance (DA).
- **Stock statement:** Submit/modify and view stock statements, stockist mapping, and mapping-deletion reports.
- **Targets:** Target submission, modification, and view screens.
- **Reports:** Daily Call Report (DCR) views, provider and doctor visits, chemist/stockist visits, missed providers, provider-visit analysis, speciality-doctor reports, and POB reports.
- **Manager and MR interfaces:** Separate layouts and dashboard pages for Manager and MR roles.

The exact data and actions available in each screen depend on the configured backend API and the permissions returned for the signed-in account.

## Technology Stack

| Technology / Package                             | Purpose                                 |
| ------------------------------------------------ | --------------------------------------- |
| React 19                                         | UI components and application interface |
| Vite 8 (beta dependency in the current lockfile) | Development server and production build |
| JavaScript and JSX                               | Frontend application code               |
| Tailwind CSS 3                                   | Utility-first styling                   |
| React Router DOM 7                               | Client-side routing                     |
| Axios                                            | HTTP requests to the backend API        |
| Framer Motion                                    | UI animation and transitions            |
| Recharts                                         | Charts and data visualization           |
| React Select                                     | Select/search dropdown controls         |
| React DatePicker                                 | Date selection controls                 |
| Lucide React and React Icons                     | Icons                                   |
| ESLint                                           | Code-quality checks                     |
| PostCSS and Autoprefixer                         | CSS processing                          |

## Requirements

Install the following on your computer:

- **Node.js 20.19 or later in the 20.x line, or Node.js 22.12 or later.** The current Vite dependency requires one of these supported versions.
- **npm**, which is included with Node.js.
- **Git** for version control and GitHub upload.
- **Visual Studio Code** (recommended).
- Access to the corresponding backend API for login and API-backed features.

Verify the installed versions in the VS Code terminal:

```bash
node -v
npm -v
git --version
```

## Run the Project Locally

### 1. Open the project folder

Extract the project ZIP if needed. In VS Code, select **File → Open Folder** and open the project root—the folder containing `package.json`, `index.html`, and `src/`.

### 2. Install dependencies

Open **Terminal → New Terminal** in VS Code and run:

```bash
npm install
```

Wait for dependency installation to finish.

### 3. Configure the backend API URL

Create or update the `.env` file in the project root. See [Environment Configuration](#environment-configuration) below. Do not upload `.env` to GitHub.

### 4. Start the development server

```bash
npm run dev
```

Vite will print a local URL in the terminal, usually `http://localhost:5173/`. Open the exact URL shown in your terminal in a browser. Leave the terminal running while you use the app.

To stop the development server, press **Ctrl + C** in that terminal.

## Environment Configuration

The frontend reads its backend API base URL from this Vite environment variable:

```env
VITE_API_BASE_URL=YOUR_BACKEND_API_BASE_URL
```

Replace `YOUR_BACKEND_API_BASE_URL` with the actual base URL supplied for your backend environment. This value is a placeholder and will not connect to a real API until replaced.

**Important details:**

- Put `.env` in the project root, next to `package.json`.
- Use the variable name exactly as shown: `VITE_API_BASE_URL`.
- The frontend expects a backend API; starting Vite alone does not start the backend.
- The backend must allow requests from the frontend origin through its CORS configuration where applicable.
- Restart `npm run dev` after changing `.env` so Vite loads the updated value.
- Variables beginning with `VITE_` are included in client-side frontend code when built. Never store passwords, private keys, database credentials, or other server-only secrets in them.

## Useful Commands

Run these commands from the project root (the folder containing `package.json`).

| Command           | Description                                         |
| ----------------- | --------------------------------------------------- |
| `npm install`     | Install project dependencies                        |
| `npm run dev`     | Start the local development server                  |
| `npm run build`   | Create an optimized production build in `dist/`     |
| `npm run preview` | Preview the production build locally after building |
| `npm run lint`    | Run ESLint checks                                   |

To build and preview the production version:

```bash
npm run build
npm run preview
```

Use the local preview URL printed by Vite.

## Project Structure

```text
MR-Reporting-Software-Frontend/
├── public/                 # Public static assets
├── src/
│   ├── assets/             # Images, logos, icons, and other assets
│   ├── components/         # Shared UI components and protected-route logic
│   │   └── admin/          # Admin data-grid components
│   ├── context/            # Authentication context
│   ├── hooks/              # Reusable React hooks
│   ├── layouts/            # Admin, Manager, and MR layouts
│   ├── pages/
│   │   ├── admin/          # Admin dashboard, masters, approvals, expenses, targets, reports
│   │   ├── manager/        # Manager dashboard pages
│   │   └── mr/             # MR dashboard, masters, expenses, and reports
│   ├── routes/             # Application route definitions
│   ├── services/           # API client and admin-user service functions
│   ├── App.jsx             # Root app and router/auth providers
│   ├── App.css             # App-level styles
│   ├── index.css           # Global styles
│   └── main.jsx            # React application entry point
├── .env                    # Local API configuration; do not commit
├── .gitignore              # Files excluded from Git
├── index.html              # Vite HTML entry point
├── package.json            # Dependencies and npm scripts
├── package-lock.json       # Locked dependency versions
├── postcss.config.js       # PostCSS configuration
├── tailwind.config.js      # Tailwind CSS configuration
├── vite.config.js          # Vite configuration
└── README.md               # Project documentation
```

`dist/` is generated by `npm run build`. `node_modules/` is created by `npm install`. Neither directory needs to be committed to GitHub.

## Authentication and API

- HTTP requests are configured through Axios in `src/services/api.js`.
- The API client reads its base URL from `VITE_API_BASE_URL`.
- If a token is present in browser `sessionStorage`, the API client attaches it as a Bearer token to requests.
- A `401 Unauthorized` response clears the saved token and role and redirects the browser to `/login` (unless it is already on that page).
- `src/context/AuthContext.jsx` provides login and logout state to the React app.
- Route definitions are maintained in `src/routes/AppRoutes.jsx`, while layouts and protected-route logic are in `src/layouts/` and `src/components/ProtectedRoute.jsx`.

The frontend's route protection is not a replacement for backend authorization. The backend must validate tokens and enforce user permissions for every protected API operation.

## Build and Deployment

1. Configure `VITE_API_BASE_URL` for the target backend environment.
2. Install dependencies with `npm install`.
3. Run `npm run build`.
4. Deploy the generated `dist/` directory to a static hosting provider.
5. Configure the hosting provider to serve `index.html` as the fallback for client-side routes, because the app uses React Router with browser history.
6. Confirm that the backend allows requests from the deployed frontend domain.

Vite environment variables are resolved during the frontend build. Set the correct API URL before running the production build for each environment.

## Troubleshooting

### `npm` or `node` is not recognized

Install a supported Node.js version, close and reopen VS Code, and re-run `node -v` and `npm -v`.

### Unsupported Node.js version or Vite startup error

The current Vite dependency requires Node.js `^20.19.0` or `>=22.12.0`. Upgrade Node.js to a supported version and reopen the terminal.

### The website opens but login or data does not work

Check that `.env` contains the correct `VITE_API_BASE_URL`, the backend is running and reachable, and the backend permits requests from your frontend origin. Restart the dev server after changing `.env`. Check the browser DevTools **Console** and **Network** tabs for the exact error.

### A page refresh shows 404 after deployment

Configure the host's SPA rewrite/fallback so client-side routes resolve to `index.html`.

### Dependency installation is failing

Verify Node.js and internet connectivity. If needed, close the dev server and run:

```bash
npm install
```

Do not delete `package-lock.json` as a first troubleshooting step; it records the project's dependency versions.

## GitHub: First Upload

These commands assume that you created an **empty** GitHub repository named `Mr-Reporting-Software-Frontend` under `Neerajsingh14` and opened the project root in VS Code. In PowerShell, commands can be pasted one at a time.

### 1. Protect local configuration

Before staging files, make sure `.gitignore` includes at least these entries:

```gitignore
node_modules/
dist/
.env
.env.*
!.env.example
*.local
```

Keep your real `.env` file on your computer, but do not commit it. If this project came from a ZIP containing an old `.git` directory, remove that old Git metadata before connecting it to the new repository. **Run this only from the correct project root:**

```powershell
if (Test-Path .git) { Remove-Item -Recurse -Force .git }
```

This removes Git history and remotes only; it does not delete your source-code files.

### 2. Initialize and upload

```bash
git init
git branch -M main
git add .
git status
```

Before committing, inspect `git status`. Confirm that `.env`, `node_modules/`, and `dist/` are not staged. If `.env` appears, stop and fix `.gitignore` before continuing.

Then commit and push:

```bash
git commit -m "Initial commit: MR Reporting Software Frontend"
git remote add origin https://github.com/Neerajsingh14/Mr-Reporting-Software-Frontend.git
git push -u origin main
```

If Git asks you to configure your commit identity, use the name and email associated with your GitHub account:

```bash
git config --global user.name "Your GitHub Name"
git config --global user.email "your-email@example.com"
```

Replace the example name and email before running the commands. If GitHub authentication is requested, complete it in your browser or through your configured Git credential manager.

### 3. Push later updates

After changing files, use:

```bash
git add .
git status
git commit -m "Describe your update"
git push
```

Review `git status` before every commit, especially when working with environment files.

## Security Notes

- Do not commit `.env`, access tokens, passwords, private keys, or real user/customer data.
- Do not expose a company or client codebase publicly unless you have permission. Choose a private GitHub repository if the code is not approved for public sharing.
- If a secret was committed or pushed previously, deleting the file in a later commit does not remove it from Git history. Revoke or rotate the exposed secret and clean the history as appropriate.
- Treat backend authorization as the security boundary; UI route protection alone is not sufficient.

---

**Project:** MR Reporting Software – Frontend  
**Repository:** [Neerajsingh14/Mr-Reporting-Software-Frontend](https://github.com/Neerajsingh14/Mr-Reporting-Software-Frontend)
