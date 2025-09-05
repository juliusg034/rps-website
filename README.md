# Rock Paper Scissors - Multiplayer Game

A modern, real-time Rock Paper Scissors game built with Next.js featuring multiplayer gameplay, AI opponents, and comprehensive player analytics.

## 🚀 Features

- **🤖 Bot Mode**: Play against AI with multiple difficulty levels (Easy, Medium, Hard, Expert)
- **👥 Multiplayer**: Real-time games with other players using Socket.io
- **📊 Analytics**: Comprehensive statistics and performance tracking
- **🏆 Leaderboards**: Compete with other players globally
- **🔐 Authentication**: Secure sign-in to track your progress
- **📱 Responsive**: Optimized for both desktop and mobile devices
- **⚡ Real-time**: Instant move updates and live game state synchronization

## 🛠️ Tech Stack

### Frontend
- **Next.js 14+** with App Router
- **TypeScript** for type safety
- **Tailwind CSS** for styling
- **Socket.io Client** for real-time communication

### Backend
- **Next.js API Routes** for REST endpoints
- **Socket.io** for WebSocket connections
- **PostgreSQL** with **Prisma ORM** for data persistence
- **Redis** for session management and caching
- **NextAuth.js** for authentication

### Infrastructure
- **Vercel** for hosting
- **Railway/Supabase** for database hosting
- **Upstash Redis** for caching layer

## 📋 Prerequisites

Before running this project, ensure you have:

- Node.js 18+ installed
- PostgreSQL database (local or hosted)
- Redis instance (local or hosted)
- Git for version control

## 🏃‍♂️ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/rock-paper-scissors.git
cd rock-paper-scissors
```

### 2. Install Dependencies
```bash
npm install
# or
yarn install
# or
pnpm install
```

### 3. Environment Setup
Create a `.env.local` file in the root directory:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/rps_db"

# Redis
REDIS_URL="redis://localhost:6379"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-secret-key-here"

# OAuth Providers (optional)
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"
GITHUB_ID="your-github-client-id"
GITHUB_SECRET="your-github-client-secret"
```

### 4. Database Setup
```bash
# Generate Prisma client
npx prisma generate

# Run database migrations
npx prisma db push

# Seed the database (optional)
npx prisma db seed
```

### 5. Run the Development Server
```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📁 Project Structure

```
src/
├── app/                    # Next.js App Router
│   ├── api/               # API routes
│   │   ├── auth/         # Authentication endpoints
│   │   ├── games/        # Game management
│   │   ├── stats/        # Statistics endpoints
│   │   └── socket/       # Socket.io handler
│   ├── game/             # Game pages
│   │   ├── [gameId]/    # Individual game page
│   │   └── lobby/       # Multiplayer lobby
│   ├── dashboard/        # User dashboard
│   ├── auth/            # Authentication pages
│   └── globals.css      # Global styles
├── components/            # Reusable components
│   ├── game/            # Game-specific components
│   ├── ui/              # UI components
│   └── layout/          # Layout components
├── lib/                  # Utility libraries
│   ├── db/              # Database utilities
│   ├── auth/            # Authentication config
│   ├── socket/          # Socket.io utilities
│   └── utils/           # General utilities
├── hooks/                # Custom React hooks
├── types/                # TypeScript type definitions
├── server/               # Server-side code
│   └── socket.js        # Socket.io server
└── prisma/              # Database schema and migrations
    ├── schema.prisma    # Database schema
    └── migrations/      # Migration files
```

## 🎮 Game Modes

### Single Player (Bot Mode)
- **Easy**: Random moves
- **Medium**: Slight pattern recognition
- **Hard**: Advanced pattern recognition with counter-strategies
- **Expert**: Machine learning-based adaptive gameplay

### Multiplayer
- **Quick Match**: Automatic matchmaking with players of similar skill
- **Private Game**: Create/join games with friends using game codes
- **Tournament Mode**: Bracket-style competitions (coming soon)

## 📊 Database Schema

### Core Tables
```sql
Users {
  id: String (Primary Key)
  email: String (Unique)
  username: String (Unique)
  createdAt: DateTime
  updatedAt: DateTime
}

Games {
  id: String (Primary Key)
  type: Enum ('bot', 'multiplayer')
  status: Enum ('waiting', 'active', 'completed')
  player1Id: String (Foreign Key)
  player2Id: String? (Foreign Key)
  winnerId: String? (Foreign Key)
  createdAt: DateTime
  completedAt: DateTime?
}

GameRounds {
  id: String (Primary Key)
  gameId: String (Foreign Key)
  roundNumber: Int
  player1Move: Enum ('rock', 'paper', 'scissors')
  player2Move: Enum ('rock', 'paper', 'scissors')
  winnerId: String? (Foreign Key)
  createdAt: DateTime
}

UserStats {
  userId: String (Primary Key, Foreign Key)
  totalGames: Int
  gamesWon: Int
  gamesLost: Int
  gamesTied: Int
  winRate: Decimal
  favoriteMove: Enum ('rock', 'paper', 'scissors')
  currentStreak: Int
  longestStreak: Int
  updatedAt: DateTime
}
```

## 🔧 API Endpoints

### Authentication
- `GET /api/auth/session` - Get current user session
- `POST /api/auth/signin` - Sign in user
- `POST /api/auth/signout` - Sign out user

### Games
- `POST /api/games/create` - Create new game
- `GET /api/games/[id]` - Get game details
- `POST /api/games/[id]/move` - Make a move
- `DELETE /api/games/[id]` - Delete/abandon game

### Statistics
- `GET /api/stats/user/[id]` - Get user statistics
- `GET /api/stats/leaderboard` - Get global leaderboard
- `GET /api/stats/history` - Get game history

### WebSocket Events
- `connection` - User connects
- `joinGame` - Join specific game room
- `makeMove` - Player makes a move
- `gameUpdate` - Real-time game state updates
- `disconnect` - Handle user disconnection

## 🚀 Deployment

### Vercel Deployment
1. Push your code to GitHub
2. Connect your repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy automatically on push

### Database Hosting
- **Supabase**: Includes PostgreSQL + Auth + Storage
- **PlanetScale**: Serverless MySQL-compatible database
- **Railway**: PostgreSQL + Redis hosting

### Redis Hosting
- **Upstash**: Serverless Redis with generous free tier
- **Redis Cloud**: Managed Redis hosting
- **Railway**: Redis hosting alongside your database

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 🐛 Bug Reports

Please use the [GitHub Issues](https://github.com/yourusername/rock-paper-scissors/issues) page to report bugs or request features.

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Socket.io team for real-time communication
- Vercel for hosting platform
- Prisma for database tooling
- Next.js team for the amazing framework


**Made with ❤️ by [Julius Gutierrez](https://github.com/juliusg034)**