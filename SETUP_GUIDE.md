# HomeCard Supabase Setup Guide

This guide provides step-by-step instructions for setting up Supabase for the HomeCard application.

## 1. Create a Supabase Project

1. Go to [Supabase](https://supabase.com/) and sign in or create an account
2. Create a new project
3. Choose a name for your project (e.g., "HomeCard")
4. Set a secure database password
5. Choose a region close to your users
6. Wait for your project to be created

## 2. Apply Database Migrations

### Option 1: Using the Supabase Dashboard

1. In your Supabase project dashboard, navigate to the SQL Editor
2. Create a new query
3. Copy the entire content of `migrations/20250612_create_profiles_table.sql` from this repository
4. Paste it into the SQL Editor
5. Click "Run" to execute the query
6. Verify that the `profiles` table has been created in the Table Editor

### Option 2: Using the Supabase CLI

If you prefer using the Supabase CLI:

1. Install the Supabase CLI if you haven't already:
   ```bash
   npm install -g supabase
   ```

2. Clone this repository:
   ```bash
   git clone https://github.com/domdanao/homecard-supabase-setup.git
   cd homecard-supabase-setup
   ```

3. Link to your Supabase project:
   ```bash
   supabase link --project-ref YOUR_PROJECT_REF
   ```
   (Replace YOUR_PROJECT_REF with your Supabase project reference ID)

4. Apply the migrations:
   ```bash
   supabase migration up
   ```

## 3. Configure Authentication

1. In your Supabase dashboard, go to Authentication > Providers
2. Ensure Email provider is enabled
3. Configure any social providers you want to use (Google, Apple, Facebook)

## 4. Configure Email Templates

1. Go to Authentication > Email Templates
2. Customize the following templates:
   - Confirmation email
   - Invite email
   - Magic Link email
   - Reset password email

## 5. Configure URL Settings

1. Go to Authentication > URL Configuration
2. Set the Site URL to your production URL
3. Add the following to Redirect URLs:
   - `homecard://` (for mobile deep linking)
   - Any other URLs you need for development or testing

## 6. Update Your App Configuration

1. Open `lib/supabase/client.ts` in your HomeCard project
2. Update the Supabase URL and anon key with your project's values:

```typescript
const supabaseUrl = 'https://YOUR_PROJECT_ID.supabase.co';
const supabaseAnonKey = 'YOUR_ANON_KEY';
```

You can find these values in your Supabase project dashboard under Project Settings > API.

## 7. Test Authentication

1. Run your HomeCard app
2. Try to create a new account
3. Verify that the user is created in Supabase (Authentication > Users)
4. Verify that a corresponding entry is created in the `profiles` table

## Troubleshooting

### User creation works but profile data isn't saved

Check that the trigger function `handle_new_user` is properly created and the trigger `on_auth_user_created` is active.

### Authentication errors

Ensure your Supabase URL and anon key are correctly set in your app configuration.

### Email verification not working

Check your URL configuration in Supabase to ensure the redirect URLs are properly set up for deep linking.