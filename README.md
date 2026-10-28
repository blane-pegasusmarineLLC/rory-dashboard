# RORY dashboard v2 (Pegasus vessel page)

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

## v2 changes
- Layout follows the fleet mock-up: map with geofence on top, Charter Readiness Score, check-before-handover list, system tiles (Safety critical, Propulsion, Fuel, Fresh water, Electrical, Security, Environment, Position, Gateway), maintenance list, recent events.
- Edit three blocks at the top of the script: `RULES` (score and readiness thresholds), `BASE` (geofence centre and radius in metres), `MAINT` (maintenance entries; entries with `sample: true` show a "sample" tag).
- The score uses live data only. Unverified sensors (second tanks, frozen battery current and charge) never lower it.
- Water maker rows show "Not monitored yet" until paths `electrical.watermaker.current` and `electrical.watermaker.filterHours` appear in the data.
- Same files to deploy: `index.html` replaces the old one. The publishable key and Supabase URL are unchanged.
