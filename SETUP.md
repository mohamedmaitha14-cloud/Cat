# Purrfect Paws — setup

Open `index.html` using VS Code Live Server. All four pages, all 12 cat photos, styles and scripts are included.

## Connect Adoption Inquiry to Supabase (no SQL coding)

1. Create a project at https://supabase.com/dashboard .
2. Open Table Editor and create a table named `adoption_inquiries`. Enable Row Level Security (RLS).
3. Add these columns in Table Editor:
   - `id`: uuid primary key, default `gen_random_uuid()`
   - `created_at`: timestamptz, default `now()`
   - `full_name`, `email`, `phone`, `cat_breed`, `specific_cat`, `home_address`, `comments`, `preferred_contact_method`: text (specific_cat may be nullable)
   - `privacy_consent`: bool
4. In the RLS policy editor, allow only INSERT to the `anon` role with a WITH CHECK condition of `true`. Do not allow public SELECT/UPDATE/DELETE. Keep RLS enabled.
5. In `js/supabase-config.js`, set your project URL and public publishable key. Never use a secret/service_role key in website code.
6. Test an inquiry and check the new row in Table Editor. Until setup is complete, inquiries cannot be submitted.

This public form collects personal information. Before deploying, configure anti-spam/rate limiting, review privacy obligations and retention practices, and verify that anonymous visitors cannot read other submissions.

Image file paths are declared in each page's HTML in the `catPhotoPaths` template; the JavaScript reads them for cards and favorites.
