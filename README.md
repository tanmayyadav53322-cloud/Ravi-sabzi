# Ravi Sabzi Bhandar

Single-shop vegetable store with a private admin panel. Static site (one `index.html`) + Supabase backend.

## Structure
- `index.html` — customer shop + admin panel (`#/admin/login`)
- `supabase/01_schema.sql` — tables, security rules (RLS), order function, storage bucket, seed data
- `supabase/02_restock_and_rate_limit.sql` — stock returns on cancel, order spam limit
- `supabase/03_make_admin.sql` — makes Ravi's login an admin
- `archive/claude-artifact-version.html` — older standalone version (no Supabase)

## Setup
1. Supabase SQL Editor: run `01_schema.sql`, then `02_restock_and_rate_limit.sql` (already applied to project `stlslwkpsaxqroqobsgj`; skip if so).
2. Supabase > Authentication > Users > Add user (Ravi's email + password).
3. Authentication > Sign In / Providers: turn OFF "Allow new users to sign up".
4. Edit the email in `03_make_admin.sql` and run it.
5. Deploy this folder to Netlify / Vercel / GitHub Pages. Admin: `https://your-site/#/admin/login`.

## Security notes
- Only the publishable key is in `index.html`. Never put the `service_role` key in any file.
- Customers can only read products/settings and call `place_order`; all other data and all writes require an admin login (enforced by RLS).
- Orders are priced on the server; the browser cannot set prices.
