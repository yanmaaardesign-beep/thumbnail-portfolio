# Supabase Setup

## 1. Create project

Create a new Supabase project from the dashboard.

## 2. Apply schema

Open the SQL Editor in Supabase and run:

- `supabase/schema.sql`

This creates:

- `admin_users`
- `genres`
- `works`
- `work_genres`

It also enables RLS and adds basic policies.

## 3. Create storage buckets

Create these buckets in Storage:

- `work-thumbnails`
- `work-large`

Recommended access policy:

- Public read only if public URLs are used on the site
- Upload/update/delete allowed only for authenticated admins

## 4. Create admin user

1. Create the user in Auth
2. Copy that user's UUID
3. Insert the UUID into `public.admin_users`

Example:

```sql
insert into public.admin_users (id, role)
values ('YOUR_AUTH_USER_UUID', 'admin');
```

## 5. Configure admin app

Edit:

- `admin/config.js`

Replace:

- `supabaseUrl`
- `supabaseAnonKey`

## 6. Open admin UI

Serve the project locally:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/admin/
```

## 7. Current scope

Already prepared:

- login form UI
- work form UI
- image preview UI
- sample work list
- Supabase client bootstrap

Next implementation step:

- actual save/update/delete
- image upload to Storage
- genre relation save
- public site fetch migration from `works.json`
