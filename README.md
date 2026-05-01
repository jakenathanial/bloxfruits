# 🍎 RentAFruit

**Trade. Hunt. Rise.**

A modern, dark-themed gaming web application for trading legendary fruits and conquering epic Leviathan hunts.

![RentAFruit](https://img.shields.io/badge/React-18.3.1-blue) ![Tailwind](https://img.shields.io/badge/Tailwind-4.1.12-blue) ![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)

---

## ✨ Features

### 🏠 **Home Page**
- Hero section with animated gradient logo
- Real-time community stats dashboard
- Quick navigation to all features
- Fully responsive design

### 🔄 **Trading System**
- Browse active fruit trades in a responsive grid layout
- Create custom trades with up to 4 fruits on each side
- Rarity-based color coding (Common → Mythic)
- Real-time public chat for each trade
- Accept/reject trade functionality

### 🌊 **Leviathan Hunt**
- Choose between Tiki Outpost and Hydra Island
- Browse available hunt rooms
- Real-time room information (players, timer, equipment)
- Join hunt rooms with team coordination
- Inside-room view with live chat and player roster

### 👤 **User Profile**
- Customizable username and avatar
- Toggle boat equipment (Fast Boat, Beast Hunter)
- View personal statistics
- Track trading and hunting history

### 🛡️ **Admin Panel**
- Manage fruit database
- Add/edit/delete fruits
- Set rarity levels
- Simple table-based interface

---

## 🎨 Design System

### Color Palette
- **Primary (Neon Purple):** `#a855f7`
- **Secondary (Electric Blue):** `#06b6d4`
- **Accent (Gold):** `#fbbf24`
- **Background:** `#0a0a0f` (Deep Black)
- **Card Background:** `#13131a`

### Rarity Colors
- **Common:** Gray `#71717a`
- **Uncommon:** Green `#22c55e`
- **Rare:** Blue `#3b82f6`
- **Epic:** Purple `#a855f7`
- **Legendary:** Gold `#fbbf24`
- **Mythic:** Red `#f43f5e`

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- pnpm (recommended) or npm

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/rentafruit.git

# Navigate to project directory
cd rentafruit

# Install dependencies
pnpm install
# or
npm install

# Start development server
pnpm dev
# or
npm run dev
```

The app will be available at `http://localhost:5173`

---

## 📁 Project Structure

```
src/
├── app/
│   ├── components/           # Reusable components
│   │   ├── ui/              # Base UI components
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   └── Badge.tsx
│   │   ├── Navbar.tsx       # Desktop navigation
│   │   ├── BottomNav.tsx    # Mobile navigation
│   │   ├── TradeCard.tsx    # Trade display component
│   │   ├── ChatBox.tsx      # Chat modal
│   │   ├── FruitSelector.tsx # Fruit selection modal
│   │   └── RoomCard.tsx     # Hunt room card
│   │
│   ├── pages/               # Route pages
│   │   ├── HomePage.tsx
│   │   ├── TradePage.tsx
│   │   ├── CreateTradePage.tsx
│   │   ├── LeviathanPage.tsx
│   │   ├── RoomPage.tsx
│   │   ├── ProfilePage.tsx
│   │   └── AdminPage.tsx
│   │
│   ├── types/               # TypeScript types
│   │   └── index.ts
│   │
│   ├── data/                # Mock data
│   │   └── mockData.ts
│   │
│   ├── lib/                 # Utilities
│   │   └── utils.ts
│   │
│   └── App.tsx              # Main app component
│
├── styles/
│   └── theme.css            # Tailwind theme configuration
│
└── package.json
```

---

## 🧩 Tech Stack

- **Framework:** React 18.3.1 with TypeScript
- **Routing:** React Router 7.13.0
- **Styling:** Tailwind CSS v4
- **Icons:** Lucide React
- **Build Tool:** Vite 6.3.5
- **Package Manager:** pnpm

---

## 🌐 Deployment

### Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

Or use the [Vercel Dashboard](https://vercel.com):
1. Import your GitHub repository
2. Vercel auto-detects Vite configuration
3. Deploy!

### Deploy to Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Build project
pnpm build

# Deploy
netlify deploy --prod
```

Or use [Netlify Dashboard](https://app.netlify.com):
1. Connect GitHub repository
2. Build command: `pnpm build`
3. Publish directory: `dist`

### Deploy to GitHub Pages

```bash
# Install gh-pages
pnpm add -D gh-pages

# Add to package.json scripts:
{
  "predeploy": "pnpm build",
  "deploy": "gh-pages -d dist"
}

# Deploy
pnpm deploy
```

---

## 🔧 Configuration

### Environment Variables
Create a `.env` file for future backend integration:

```env
VITE_API_URL=your_api_url
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_anon_key
```

### Tailwind Configuration
Custom theme variables are defined in `src/styles/theme.css`. Modify colors and spacing there.

---

## 🎯 Features Roadmap

- [ ] Real-time WebSocket integration for chat
- [ ] Backend API with Supabase
- [ ] User authentication (OAuth, Email)
- [ ] Persistent data storage
- [ ] Notification system
- [ ] Leaderboards
- [ ] Achievements system
- [ ] Mobile app (React Native)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 Available Scripts

```bash
# Development server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview

# Type check
pnpm type-check
```

---

## 🔒 Backend Integration

This frontend is designed to integrate seamlessly with backends like **Supabase**, **Firebase**, or custom REST/GraphQL APIs.

### Supabase Example Schema

```sql
-- Users table
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  username TEXT UNIQUE NOT NULL,
  has_fast_boat BOOLEAN DEFAULT false,
  has_beast_hunter BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Fruits table
CREATE TABLE fruits (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  name TEXT NOT NULL,
  image TEXT NOT NULL,
  rarity TEXT NOT NULL
);

-- Trades table
CREATE TABLE trades (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id UUID REFERENCES users(id),
  offering JSONB NOT NULL,
  requesting JSONB NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Rooms table
CREATE TABLE rooms (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  host_id UUID REFERENCES users(id),
  destination TEXT NOT NULL,
  max_players INTEGER DEFAULT 7,
  timer INTEGER DEFAULT 300,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 📱 Mobile Support

- Fully responsive design
- Mobile-first approach
- Bottom navigation for mobile devices
- Touch-optimized interactions
- Works on all screen sizes (320px+)

---

## 🎮 Game Mechanics

### Trading
- Users can offer up to 4 fruits
- Request up to 4 fruits in return
- Public chat for negotiation
- Accept/reject functionality

### Leviathan Hunts
- Two destinations: Tiki Outpost & Hydra Island
- Rooms support 5-7 players
- Equipment bonuses:
  - **Fast Boat:** Better dodge capability
  - **Beast Hunter:** +25% damage to Leviathans
- Real-time countdown timer
- Team coordination via in-room chat

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👨‍💻 Author

Created with ❤️ by the RentAFruit Team

---

## 🙏 Acknowledgments

- React Team for the amazing framework
- Tailwind CSS for the utility-first CSS approach
- Lucide for beautiful icons
- The open-source community

---

## 📞 Support

For questions or support:
- Open an issue on GitHub
- Email: support@rentafruit.com
- Discord: [Join our community](https://discord.gg/rentafruit)

---

**Happy Trading and Hunting! 🎉**
