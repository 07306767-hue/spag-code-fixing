# Messy Catalog Activity

Starter code for the CC105 Atomic Design refactor activity.

## Run it

```
flutter pub get
```

## Supabase setup

Products are stored in Supabase PostgreSQL. Product photos are stored in the
private `product-images` Supabase Storage bucket; the database stores each
photo's storage path. The app signs users in before allowing catalog access.

1. Create a Supabase project.
2. In the Supabase SQL Editor, run [`supabase/schema.sql`](./supabase/schema.sql).
   This creates the products table, case-insensitive unique item-code index,
   row-level security policies, private image bucket, and the catalog's sample
   products (without adding duplicates if you run it again).
3. In **Authentication → Providers**, enable Email. Create an account in the
   app. If email confirmation is enabled, confirm the address before signing in.
   For a private deployment, disable public sign-ups after creating authorized
   accounts.
4. Copy the project's **Project URL** and **publishable key**. Do not use
   or ship the `service_role` key in the Flutter app.
5. Run with your project values:

   ```
   flutter run --dart-define=SUPABASE_URL=https://your-project.supabase.co --dart-define=SUPABASE_PUBLISHABLE_KEY=your-publishable-key
   ```

Only authenticated users can read, add, update, or delete products and images.
All authenticated accounts share the catalog. The item code is optional, but
when provided it must be unique (case-insensitively).
