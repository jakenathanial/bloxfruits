# RentAFruit - Setup Guide

## 🎮 Welcome to RentAFruit!

Your premium dark futuristic trading and hunting platform for Roblox Blox Fruits is now ready!

## ✅ What's Been Built

### Core Features
- ✨ **Home Page** - Premium landing with live stats
- 🔄 **Trade System** - Create trades, browse deals, and chat
- 🐋 **Leviathan Hunt** - Create/join hunt rooms with real-time coordination
- 👤 **User Profiles** - Manage your boats and Roblox username
- 🛡️ **Admin Dashboard** - Full fruit management system

### Technical Stack
- **Frontend**: React + Tailwind CSS + Motion (animations)
- **Backend**: Supabase Edge Functions (Hono server)
- **Database**: Supabase PostgreSQL (via KV store)
- **Auth**: Supabase Auth (Google + Discord OAuth)
- **Real-time**: Polling-based updates (every 3-5 seconds)

## 🚀 Next Steps

### 1. Deploy the Supabase Edge Function

Your server code is in `/supabase/functions/server/index.tsx`. You need to deploy it:

Go to your Supabase project dashboard → Edge Functions → Deploy the `server` function.

The server will be available at:
`https://ecsphtqkydxyllbzhdcg.supabase.co/functions/v1/make-server-75b8ebf1`

### 2. Set Up OAuth Providers

#### Google OAuth
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create OAuth credentials
3. Add to Supabase: Dashboard → Authentication → Providers → Google
4. **Important**: Add authorized redirect URL: `https://ecsphtqkydxyllbzhdcg.supabase.co/auth/v1/callback`

Full guide: https://supabase.com/docs/guides/auth/social-login/auth-google

#### Discord OAuth
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create application and OAuth2 credentials
3. Add to Supabase: Dashboard → Authentication → Providers → Discord
4. **Important**: Add redirect URL: `https://ecsphtqkydxyllbzhdcg.supabase.co/auth/v1/callback`

Full guide: https://supabase.com/docs/guides/auth/social-login/auth-discord

### 3. Create Your First Admin User

After deploying, you'll need to manually set your user as admin:

1. Sign in to the app with Google or Discord
2. Go to Supabase Dashboard → Table Editor → `kv_store_75b8ebf1`
3. Find your user entry (key starts with `user:`)
4. Edit the value JSON and set `"isAdmin": true`
5. Save and refresh the app

### 4. Add Fruits (Admin Only)

Once you're an admin:
1. Go to Admin Dashboard in the app
2. Click "Add Fruit"
3. Fill in:
   - Fruit name (required)
   - Image URL (use direct image links)
   - Rarity (Common to Mythical)
   - Type (Natural, Elemental, etc.)
   - Value (optional)
   - Description (optional)

## 🎨 Design Features

### Premium Dark Theme
- Black base with purple/blue gradient accents
- Smooth hover effects and transitions
- Responsive mobile-first design
- Custom scrollbars and selections
- Glow effects on interactive elements

### Animations
- Gradient backgrounds
- Scale transforms on hover
- Smooth page transitions
- Real-time updates (auto-refresh)

## 📱 User Flow

### Public Users (No Login)
- Browse all trades
- View hunt rooms
- See stats

### Logged-In Users
- Create trades
- Join/create hunt rooms
- Chat in trades and rooms
- Edit profile (boats, Roblox username)

### Admin Users
- All user features
- Add/edit/delete fruits
- Delete any trade
- Full moderation access

## 🔧 Troubleshooting

### OAuth Login Not Working
- Ensure providers are configured in Supabase
- Check redirect URLs match exactly
- Verify edge function is deployed

### Chat Not Updating
- Messages poll every 3 seconds
- Check browser console for errors
- Verify edge function is running

### Rooms Expiring
- Rooms auto-delete after 1 hour
- Empty rooms are deleted immediately
- This is by design for cleanup

## 🛡️ Security Notes

- **Row Level Security**: Not implemented (using KV store)
- **Admin Access**: Manually granted via database
- **API Keys**: Server-side only (SERVICE_ROLE_KEY)
- **Make is for prototypes**: Not production-grade security

## 📊 Database Schema (KV Store)

All data is stored in `kv_store_75b8ebf1` table with these key patterns:

- `user:{userId}` - User profiles
- `fruit:{fruitId}` - Fruit definitions
- `trade:{tradeId}` - Trade listings
- `trade-chat:{tradeId}:{messageId}` - Trade chat messages
- `room:{roomId}` - Hunt rooms
- `room-chat:{roomId}:{messageId}` - Room chat messages

## 🎯 Feature Highlights

### Trade System
- Up to 4 fruits offered
- Up to 4 fruits requested
- Public chat per trade
- Real-time updates

### Hunt Rooms
- Tiki Outpost or Hydra Island
- 5-7 players max
- Beast Hunter Boat requirement warning
- Fast Boat detection
- 1-hour auto-expiration

### User Profiles
- Display name
- Fast Boat ownership
- Beast Hunter Boat ownership
- Boat info shows in hunt rooms

## 🌟 Enjoy RentAFruit!

Your platform is ready to help Blox Fruits players trade and hunt together!

**Support**: Remember to deploy your edge function and configure OAuth providers to enable full functionality.
