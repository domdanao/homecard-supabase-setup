# Supabase Setup for HomeCard

This repository contains the necessary Supabase setup files for the HomeCard application.

## Migrations

The `migrations` directory contains SQL scripts that need to be applied to your Supabase project to set up the required database schema.

### Applying Migrations

You can apply these migrations in several ways:

#### Option 1: Using the Supabase Dashboard

1. Log in to your Supabase dashboard
2. Navigate to the SQL Editor
3. Create a new query
4. Copy and paste the content of each migration file
5. Execute the query

#### Option 2: Using the Supabase CLI

If you have the Supabase CLI installed, you can apply migrations with:

```bash
supabase migration up
```

## Required Tables

### profiles

The `profiles` table extends the default Supabase auth.users table with additional user information:

- `id`: UUID (primary key, references auth.users)
- `full_name`: User's full name
- `phone_number`: User's phone number
- `avatar_url`: URL to user's avatar image
- `created_at`: Timestamp of profile creation
- `updated_at`: Timestamp of last profile update

The migration also sets up:

- Row Level Security (RLS) policies to ensure users can only access their own profile data
- A trigger to automatically update the `updated_at` timestamp
- A trigger to automatically create a profile entry when a new user signs up

## Authentication Setup

Ensure the following settings are configured in your Supabase project:

1. **Email Auth**: Enable Email/Password sign-in method in Authentication > Providers
2. **Email Templates**: Customize email templates in Authentication > Email Templates
3. **URL Configuration**: Set the Site URL and Redirect URLs in Authentication > URL Configuration
   - Site URL: Your app's production URL
   - Redirect URLs: Include `homecard://` for mobile app deep linking

## Environment Variables

Make sure to update the Supabase URL and anon key in your application with your actual project values.