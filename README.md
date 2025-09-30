# 💬 Chatty - Real-Time Chat Application

A modern, full-stack real-time chat application built with the MERN stack (MongoDB, Express, React, Node.js) featuring WebSocket communication, user authentication, and a beautiful UI with multiple themes.

## ✨ Features

### Core Functionality
- 🔐 **User Authentication** - Secure signup/login with JWT tokens and bcrypt password hashing
- 💬 **Real-Time Messaging** - Instant message delivery using Socket.IO
- 👥 **Online Status** - See who's online in real-time
- 🖼️ **Image Sharing** - Send and receive images in chat (with automatic compression)
- 📸 **Profile Pictures** - Upload and update profile pictures via Cloudinary
- 🎨 **Multiple Themes** - 32 beautiful themes powered by DaisyUI
- 📱 **Responsive Design** - Works seamlessly on desktop and mobile devices

### Technical Features
- WebSocket connections for real-time updates
- Automatic image compression before upload
- Cookie-based authentication with HTTP-only cookies
- Protected routes and middleware authorization
- MongoDB for data persistence
- Cloudinary integration for media storage

## 🛠️ Tech Stack

### Frontend
- **React** - UI library
- **Vite** - Build tool and dev server
- **Zustand** - State management
- **Axios** - HTTP client
- **Socket.IO Client** - WebSocket client
- **React Router** - Navigation
- **TailwindCSS** - Utility-first CSS
- **DaisyUI** - Component library
- **Lucide React** - Icons
- **React Hot Toast** - Notifications

### Backend
- **Node.js** - Runtime environment
- **Express** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM
- **Socket.IO** - WebSocket server
- **JWT** - Authentication tokens
- **Bcrypt** - Password hashing
- **Cloudinary** - Image hosting
- **Cookie Parser** - Cookie handling
- **CORS** - Cross-origin resource sharing

## 📁 Project Structure

```
fullstack-chat-app/
├── backend/
│   ├── src/
│   │   ├── controllers/      # Route controllers
│   │   │   ├── auth.controller.js
│   │   │   └── message.controller.js
│   │   ├── lib/              # Utilities and configurations
│   │   │   ├── cloudinary.js
│   │   │   ├── db.js
│   │   │   ├── socket.js
│   │   │   └── utils.js
│   │   ├── middleware/       # Express middleware
│   │   │   └── auth.middleware.js
│   │   ├── models/           # Mongoose models
│   │   │   ├── message.model.js
│   │   │   └── user.model.js
│   │   ├── routes/           # API routes
│   │   │   ├── auth.route.js
│   │   │   └── message.route.js
│   │   ├── seeds/            # Database seeders
│   │   │   └── user.seed.js
│   │   └── index.js          # Entry point
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/       # React components
│   │   │   ├── skeletons/    # Loading skeletons
│   │   │   ├── AuthImagePattern.jsx
│   │   │   ├── ChatContainer.jsx
│   │   │   ├── ChatHeader.jsx
│   │   │   ├── MessageInput.jsx
│   │   │   ├── Navbar.jsx
│   │   │   ├── NoChatSelected.jsx
│   │   │   └── SideBar.jsx
│   │   ├── pages/            # Page components
│   │   │   ├── HomePage.jsx
│   │   │   ├── LoginPage.jsx
│   │   │   ├── ProfilePage.jsx
│   │   │   ├── SettingsPage.jsx
│   │   │   └── SignUpPage.jsx
│   │   ├── store/            # Zustand stores
│   │   │   ├── useAuthStore.js
│   │   │   ├── useChatStore.js
│   │   │   └── useThemeStore.js
│   │   ├── lib/              # Utilities
│   │   │   ├── axios.js
│   │   │   └── utils.js
│   │   ├── constants/        # Constants
│   │   │   └── index.js
│   │   └── App.jsx           # Main app component
│   └── package.json
└── package.json              # Root package.json
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas account)
- Cloudinary account (for image uploads)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/shalevbd7/fullstack-chat-app.git
cd fullstack-chat-app
```

2. **Install dependencies**
```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

3. **Environment Variables**

Create a `.env` file in the `backend` directory:

```env
# Server
PORT=5001
NODE_ENV=development

# Database
MONGODB_URI=your_mongodb_connection_string

# JWT
JWT_SECRET=your_jwt_secret_key

# Cloudinary
CLOUDINAR_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINAR_API_KEY=your_cloudinary_api_key
CLOUDINAR_API_SECRET=your_cloudinary_api_secret

# Frontend URL (for CORS)
CLIENT_URL=http://localhost:5173
```

4. **Run the application**

```bash
# Run backend (from backend directory)
npm run dev

# Run frontend (from frontend directory, in a new terminal)
npm run dev
```

The application will be available at:
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:5001`

## 📡 API Endpoints

### Authentication
- `POST /api/auth/signup` - Register a new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/check` - Check authentication status
- `PUT /api/auth/update-profile` - Update user profile (protected)

### Messages
- `GET /api/messages/users` - Get all users for sidebar (protected)
- `GET /api/messages/:id` - Get messages with specific user (protected)
- `POST /api/messages/send/:id` - Send message to user (protected)

## 🎨 Available Themes

The application includes 32 beautiful themes:
- light, dark, cupcake, bumblebee, emerald, corporate
- synthwave, retro, cyberpunk, valentine, halloween
- garden, forest, aqua, lofi, pastel, fantasy
- wireframe, black, luxury, dracula, cmyk, autumn
- business, acid, lemonade, night, coffee, winter
- dim, nord, sunset

## 🗄️ Database Models

### User Model
```javascript
{
  email: String (required, unique),
  fullName: String (required),
  password: String (required, min 6 characters),
  profilePic: String (default: ""),
  timestamps: true
}
```

### Message Model
```javascript
{
  senderId: ObjectId (ref: User),
  receiverId: ObjectId (ref: User),
  text: String,
  image: String,
  timestamps: true
}
```

## 🔒 Security Features

- Password hashing with bcrypt (salt rounds: 10)
- HTTP-only cookies for JWT tokens
- JWT token expiration (7 days)
- Protected routes with authentication middleware
- CORS configuration for secure cross-origin requests
- Secure cookies in production environment

## 🌐 Socket.IO Events

### Client to Server
- `connection` - User connects
- `disconnect` - User disconnects

### Server to Client
- `getOnlineUsers` - Receive list of online users
- `newMessage` - Receive new message in real-time

## 📦 Build for Production

```bash
# From root directory
npm run build

# Start production server
npm start
```

This will:
1. Install backend dependencies
2. Install frontend dependencies
3. Build frontend for production
4. Serve the built frontend from the backend server

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

## 📝 License

This project is [ISC](LICENSE) licensed.

## 👤 Author

**Shalev Ben-David**
- GitHub: [@shalevbd7](https://github.com/shalevbd7)

## 🙏 Acknowledgments

- Socket.IO for real-time communication
- DaisyUI for beautiful UI components
- Cloudinary for image hosting
- MongoDB for database solution

---

Made with ❤️ using the MERN Stack
