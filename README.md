# River Bank CRM

A full-stack real-estate CRM built with Next.js App Router, TypeScript, Tailwind CSS, shadcn/ui, Prisma and SQLite.

## Stack

- Next.js 15 (App Router) + React 19 + TypeScript
- Tailwind CSS 4 (CSS-first) + shadcn/ui
- Prisma 6 + SQLite (swap to PostgreSQL via `prisma/schema.prisma`)
- Auth.js (NextAuth) credentials + bcrypt + sessions
- Zod validation, recharts, jsPDF, xlsx

## Getting started (Supabase / Postgres)

```bash
cd river-bank
npm install
cp .env.example .env
# edit .env: set AUTH_SECRET, DATABASE_URL, DIRECT_URL, and Supabase storage keys
npx prisma db push
npm run db:seed
npm run dev
```

For production on Vercel, set the same env vars in the project settings and run `prisma db push` (or `prisma migrate deploy` after creating migrations) against your Supabase database.

Open http://localhost:3000.

## Scripts

- `npm run dev` – development server
- `npm run build` – production build
- `npm run start` – production server
- `npm run typecheck` – TypeScript
- `npm run db:migrate` – create/apply migrations (dev)
- `npm run db:push` – push schema without migration
- `npm run db:seed` – seed demo data
- `npm run db:reset` – drop, migrate and seed (destructive)

## Demo credentials

| Role          | Email                  | Password      |
| ------------- | ---------------------- | ------------- |
| Admin         | admin@riverbank.com    | Admin@12345   |
| Sales Manager | manager@riverbank.com  | Manager@12345 |
| Sales Agent   | agent@riverbank.com    | Agent@12345   |

The admin account is flagged `mustChangePassword` and will be prompted to change its password on first login.

## Roles & scope

- **Admin** – full access, including user management, settings, soft-delete/restore, audit log.
- **Sales Manager** – sees own records plus direct reports and unassigned records.
- **Sales Agent** – sees only own records.

Protection is enforced in middleware, API routes and query-level scopes.

## Notable features

- Customers with 7-stage pipeline, search/filter/sort/pagination, timeline, CSV import/export.
- Properties with images, statuses and customer links.
- Deals (kanban + table), stage history, tasks/reminders, calendar.
- Feedback: internal logging, tokenized public form (`/f/<token>`), replies, resolve/reopen, negative-feedback alerts.
- Dashboard with cards, charts and alerts; Reports with PDF/Excel export.
- Arabic (RTL) + English toggle, dark mode, responsive layout.

## Environment

See `.env.example`. Key variables: `DATABASE_URL`, `AUTH_SECRET`, `AUTH_TRUST_HOST`, `NEXTAUTH_URL`, `NEXT_PUBLIC_APP_URL`.
