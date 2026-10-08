# Ravi Sabzi Bhandar

Single-shop vegetable store with a private admin panel. Static site (one `index.html`) + Supabase backend.

## Structure
- `index.html` — customer shop + admin panel (`#/admin/login`)
- `supabase/01_schema.sql` — tables, security rules (RLS), order function, storage bucket, seed data
- `supabase/02_restock_and_rate_limit.sql` — stock returns on cancel, order spam limit
- `supabase/03_make_admin.sql` — makes Ravi's login an admin
- `archive/claude-artifact-version.html` — older standalone version (no Supabase)

## Setup
1. Supabase SQL Editor: run `01_schema.sql`, `02_restock_and_rate_limit.sql`, then `04_ravi_self_setup.sql`.
2. Run the last (commented) line of `04_ravi_self_setup.sql` with a setup code of your own choice. Keep the code private.
3. Authentication > Sign In / Providers: keep "Allow new users to sign up" ON only until Ravi finishes step 5. Optionally turn OFF "Confirm email" for the first setup.
4. Deploy this folder to Netlify / Vercel / GitHub Pages.
5. Ravi opens `https://your-site/#/admin/login`, taps "Pehli baar? Ravi ka profile banayein", enters name, mobile, email, password and the setup code. The code is deleted automatically after use.
6. Turn "Allow new users to sign up" OFF again. From now on only Ravi's email + password opens the admin panel.

(`03_make_admin.sql` is an alternative: promote an existing user by email, without the setup form.)

## Security notes
- Only the publishable key is in `index.html`. Never put the `service_role` key in any file.
- Customers can only read products/settings and call `place_order`; all other data and all writes require an admin login (enforced by RLS).
- Orders are priced on the server; the browser cannot set prices.
