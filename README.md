# Docshare

A small Next.js document sharing app. Document records, admins, and submissions are stored in PostgreSQL through Prisma. PDFs are stored privately in Cloudflare R2 and sent as email attachments after a visitor submits their email.

## Setup

1. Copy `.env.example` to `.env.local` and fill in `DATABASE_URL`, a random `AUTH_SECRET` of at least 32 characters, admin credentials, Gmail SMTP settings, and the R2 settings.
2. Create an R2 bucket and an API token with object read/write access to that bucket. Set `R2_ENDPOINT` to `https://<account-id>.r2.cloudflarestorage.com`.
3. Install dependencies with `npm install`.
4. Run `npm run db:generate`, then `npm run db:migrate -- --name init` to create the PostgreSQL schema.
5. Run `npm run seed` to create or update the admin account, then `npm run dev`.

The seed command reads `ADMIN_EMAIL` and `ADMIN_PASSWORD` from the environment. Running it updates the password for that admin account.

Email delivery uses Gmail SMTP with `GMAIL_USER` and a Google App Password in `GMAIL_APP_PASSWORD`. `NEXT_PUBLIC_APP_URL` is used to build links shown in the admin dashboard.

## Routes

- `/admin/login` signs in the administrator.
- `/admin` manages documents and submission counts.
- `/d/[slug]` displays a document title and email delivery form.

PDF bytes are only sent as email attachments. No public PDF download route is provided.
# DocShare
