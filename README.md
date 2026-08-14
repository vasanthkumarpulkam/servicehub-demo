# ServiceHub

**A service marketplace front-end prototype - complete UI and state flows running entirely on mock data.**

[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react&logoColor=white)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white)](https://vitejs.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-38B2AC?logo=tailwindcss&logoColor=white)](https://tailwindcss.com)

---

## Overview

ServiceHub is a front-end prototype of a two-sided service marketplace: customers post jobs, providers bid, both sides message each other.

**It runs on mock data by design.** There's no backend - the point was to work out the full interaction model, routing and state architecture before committing to a data layer. Firebase is wired in as a dependency and ready to swap in behind the existing context providers.

If you want the production version of this idea with a real backend, see [Housecal Pro](https://github.com/vasanthkumarpulkam/housecal-pro).

## Screenshots

<!-- Add screenshots here:
![Home](docs/screenshots/home.png)
![Job detail](docs/screenshots/job-detail.png)
-->

## Features

- **Role-based accounts** - separate customer and provider experiences
- **Job management** - post, browse, filter and view jobs
- **Bidding** - providers submit quotes; customers compare them
- **Messaging** - thread list and chat window
- **Dashboards** - distinct customer and provider views
- **Profiles** - ratings and reviews
- **Categories** - organised service taxonomy with a category grid
- **Internationalisation** - translation table in `src/data/translations.ts`
- **Support and legal pages**
- **Responsive** throughout

## Tech stack

| Layer | Technology |
|---|---|
| Framework | React 18 + TypeScript |
| Build | Vite |
| Styling | Tailwind CSS |
| Icons | Lucide React |
| State | React Context API |
| Backend | Firebase (dependency present, not yet wired) |

## Architecture

State is split across three context providers, each with a matching hook - the seam where a real backend would be introduced:

```
App
├── AuthContext   ──► useAuth   ──► user, role, sign in/out
├── JobContext    ──► useJobs   ──► jobs, bids, post/filter
└── ChatContext   ──► useChat   ──► threads, messages

Data source: src/data/mockJobs.ts, categories.ts, translations.ts
             ▲
             └── replace with Firebase calls; component tree is unchanged
```

## Getting started

### Prerequisites

- Node.js 18+

### Install and run

```bash
git clone https://github.com/vasanthkumarpulkam/servicehub-demo.git
cd servicehub-demo
npm install
npm run dev              # http://localhost:5173
```

```bash
npm run build
npm run preview
npm run lint
```

No environment variables are needed - the app is fully self-contained.

## Project structure

```
servicehub-demo/
├── src/
│   ├── components/
│   │   ├── Auth/         SignIn, SignUp
│   │   ├── Chat/         ChatThreadList, ChatWindow
│   │   ├── Dashboard/    CustomerDashboard, ProviderDashboard
│   │   ├── Common/       HeroSection, CategoryGrid, StatsBar, EmptyState
│   │   ├── Header.tsx  Footer.tsx  JobCard.tsx
│   ├── context/          AuthContext, JobContext, ChatContext
│   ├── hooks/            useAuth, useJobs, useChat
│   ├── pages/            Home, Jobs, JobDetail, PostJob, Dashboard,
│   │                     Messages, Profile, Settings, HowItWorks,
│   │                     Support, Legal
│   ├── data/             mockJobs, categories, translations
│   ├── types/            job, bid, message
│   └── styles/
└── vite.config.ts
```

## Connecting a real backend

The mock data layer is isolated to `src/data/` and consumed only through the three hooks. To wire up Firebase:

1. Add your Firebase config and initialise the app
2. Replace the mock reads inside `useJobs`, `useAuth` and `useChat` with Firestore queries
3. Leave every component untouched - they only ever talk to the hooks

## Roadmap

- [ ] Wire up Firebase Auth and Firestore
- [ ] Persist bids and messages
- [ ] File upload for job photos
- [ ] Payment integration

## Author

**Vasanth Kumar Pulkam** - [GitHub](https://github.com/vasanthkumarpulkam)
