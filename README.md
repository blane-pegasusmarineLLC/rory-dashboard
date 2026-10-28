# RORY dashboard v0 (Pegasus detail page)

Single static page: `index.html`. No build step.

1. Edit `SUPABASE_KEY` near the top of the script: paste the **publishable** key
   (`sb_publishable_...`). Never put the secret key here.
2. `?demo` at the end of the address shows fake data (banner says so) without signing in.
3. Users: Supabase > Authentication > Users (email + password), then add a membership row:
   ```sql
   insert into memberships(user_id, operator_id, role)
   select u.id, o.id, 'staff' from auth.users u, operators o
   where u.email = 'person@example.com' and o.name = 'Pegasus Marine';
   ```
4. GitHub Pages: push `index.html` to a public repo, Settings > Pages > Deploy from branch (main, /root).
