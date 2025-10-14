# Task Management System - Frontend

A modern, responsive frontend application built with Next.js 14, TypeScript, and TailwindCSS for managing tasks efficiently.

![Next.js](https://img.shields.io/badge/Next.js-14-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3-38bdf8)

## 🌟 Features

- 🎨 Modern and clean UI with TailwindCSS
- 📱 Fully responsive design (mobile-first approach)
- ⚡ Fast page loads with Next.js 14 App Router
- 🔐 Secure authentication with JWT
- 🎯 Intuitive task management interface
- 🔍 Real-time filtering and sorting
- ⚠️ Visual indicators for overdue tasks
- 🌈 Color-coded status badges
- 📝 Form validation and error handling
- 🔄 Loading states and user feedback

## 🛠️ Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript 5
- **Styling**: TailwindCSS 3
- **HTTP Client**: Axios
- **Date Handling**: date-fns
- **State Management**: React Context API
- **Form Handling**: Native React hooks

## 📁 Project Structure

```
task-management-frontend/
├── src/
│   ├── app/                      # Next.js 14 App Router
│   │   ├── login/               # Login page
│   │   │   └── page.tsx
│   │   ├── register/            # Registration page
│   │   │   └── page.tsx
│   │   ├── tasks/               # Task management
│   │   │   ├── [id]/
│   │   │   │   └── edit/
│   │   │   │       └── page.tsx  # Edit task page
│   │   │   ├── new/
│   │   │   │   └── page.tsx      # Create task page
│   │   │   └── page.tsx          # Tasks dashboard
│   │   ├── globals.css          # Global styles
│   │   ├── layout.tsx           # Root layout
│   │   └── page.tsx             # Home page (redirects)
│   │
│   ├── contexts/                # React Context
│   │   └── AuthContext.tsx      # Authentication context
│   │
│   ├── lib/                     # Utilities
│   │   └── api.ts               # Axios configuration
│   │
│   └── types/                   # TypeScript definitions
│       └── task.ts              # Task types
│
├── public/                      # Static assets
│   └── favicon.ico
│
├── .env.example                 # Environment variables template
├── .env.local                   # Local environment variables (gitignored)
├── .eslintrc.json              # ESLint configuration
├── .gitignore                  # Git ignore rules
├── Dockerfile                  # Docker configuration
├── next.config.js              # Next.js configuration
├── package.json                # Dependencies
├── postcss.config.js           # PostCSS configuration
├── tailwind.config.ts          # Tailwind configuration
├── tsconfig.json               # TypeScript configuration
└── README.md                   # This file
```

## 📦 Prerequisites

- Node.js 18+ 
- npm or yarn
- Backend API running (see [backend README](../task-management-backend/README.md))

## 🚀 Installation

### 1. Clone and Navigate

```bash
cd task-management-frontend
```

### 2. Install Dependencies

```bash
npm install
# or
yarn install
```

### 3. Environment Setup

Create `.env.local` file:

```env
NEXT_PUBLIC_API_URL=http://localhost:3000
```

For production, create `.env.production`:

```env
NEXT_PUBLIC_API_URL=https://your-backend-url.railway.app
```

## 🏃 Running the Application

### Development Mode

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3001](http://localhost:3001) in your browser.

### Production Build

```bash
# Build the application
npm run build

# Start production server
npm run start
```

### Docker

```bash
# Build Docker image
docker build -t task-management-frontend .

# Run container
docker run -p 3001:3000 -e NEXT_PUBLIC_API_URL=http://localhost:3000 task-management-frontend
```

## 🔧 Configuration

### Next.js Configuration

`next.config.js`:
```javascript
const nextConfig = {
  reactStrictMode: true,
  env: {
    NEXT_PUBLIC_API_URL: process.env.NEXT_PUBLIC_API_URL,
  },
  output: 'standalone', // For production optimization
}
```

### Tailwind Configuration

`tailwind.config.ts`:
```typescript
const config = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
      },
    },
  },
}
```

## 📱 Pages & Routes

### Public Routes

| Route | Description |
|-------|-------------|
| `/` | Home (redirects to login/tasks) |
| `/login` | User login page |
| `/register` | User registration page |

### Protected Routes (Requires Authentication)

| Route | Description |
|-------|-------------|
| `/tasks` | Tasks dashboard with filtering and sorting |
| `/tasks/new` | Create new task form |
| `/tasks/[id]/edit` | Edit existing task form |

## 🎨 UI Components

### Authentication Context

```typescript
// Usage example
import { useAuth } from '@/contexts/AuthContext';

function MyComponent() {
  const { user, token, login, logout } = useAuth();
  
  // Use authentication state and methods
}
```

### API Client

```typescript
// Usage example
import api from '@/lib/api';

// GET request
const response = await api.get('/tasks');

// POST request
const response = await api.post('/tasks', taskData);
```

## 🔐 Authentication Flow

1. **Registration**: User fills form → API validates → JWT token returned → Redirects to dashboard
2. **Login**: User enters credentials → API validates → JWT token returned → Stored in localStorage → Redirects to dashboard
3. **Protected Routes**: Check for token → If valid, show page → If invalid, redirect to login
4. **Logout**: Clear token and user data → Redirect to login

## 🎯 Features Implementation

### Task Filtering

```typescript
// Filter by status
const filteredTasks = tasks.filter(task => task.status === 'To Do');

// Sort by due date
const sortedTasks = tasks.sort((a, b) => 
  new Date(a.dueDate).getTime() - new Date(b.dueDate).getTime()
);
```

### Overdue Task Detection

```typescript
const isPastDue = (dueDate: string) => {
  return new Date(dueDate) < new Date();
};
```

### Remember Me Functionality

```typescript
// Login with remember me
await login(email, password, true); // 30-day token
await login(email, password, false); // 7-day token
```

## 🌐 Deployment

### Deploy to Vercel (Recommended)

1. **Push to GitHub**:
```bash
git add .
git commit -m "Deploy frontend"
git push origin main
```

2. **Connect to Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Import your GitHub repository
   - Set root directory: `task-management-frontend`

3. **Configure Environment Variables**:
```env
NEXT_PUBLIC_API_URL=https://your-backend-url.railway.app
```

4. **Deploy Settings**:
   - Framework: Next.js
   - Build Command: `npm run build`
   - Output Directory: `.next`

5. **Click Deploy**

### Deploy to Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Build the application
npm run build

# Deploy
netlify deploy --prod
```

### Deploy to Other Platforms

The application can be deployed to any platform that supports Node.js:
- Vercel (Recommended)
- Netlify
- AWS Amplify
- Google Cloud Platform
- Azure Static Web Apps

## 🧪 Testing

### Linting

```bash
npm run lint
```

### Type Checking

```bash
npx tsc --noEmit
```

### Manual Testing Checklist

- [ ] Registration with valid credentials
- [ ] Registration with invalid email
- [ ] Registration with weak password
- [ ] Login with valid credentials
- [ ] Login with invalid credentials
- [ ] Remember me functionality
- [ ] Create new task
- [ ] Edit existing task
- [ ] Delete task
- [ ] Filter tasks by status
- [ ] Sort tasks by different fields
- [ ] Logout functionality
- [ ] Protected route access without token
- [ ] Responsive design on mobile
- [ ] Responsive design on tablet

## 🎨 Styling Guidelines

### Color Scheme

```css
/* Primary Colors */
--primary-50: #eff6ff;
--primary-500: #3b82f6;
--primary-600: #2563eb;

/* Status Colors */
--todo: #gray-100;
--in-progress: #blue-100;
--completed: #green-100;

/* Alert Colors */
--error: #red-600;
--warning: #yellow-600;
--success: #green-600;
```

### Responsive Breakpoints

```css
/* Mobile */
sm: 640px

/* Tablet */
md: 768px

/* Desktop */
lg: 1024px
xl: 1280px
```

## 🔒 Security Best Practices

- ✅ JWT tokens stored in localStorage (consider httpOnly cookies for production)
- ✅ CSRF protection through token-based auth
- ✅ XSS prevention through React's default escaping
- ✅ Input validation on all forms
- ✅ HTTPS enforced in production
- ✅ Environment variables for sensitive data
- ✅ No sensitive data in client-side code

## 📊 Performance Optimization

- ✅ Next.js automatic code splitting
- ✅ Image optimization with Next.js Image component
- ✅ Route prefetching
- ✅ Lazy loading components
- ✅ Memoization of expensive computations
- ✅ Debouncing for search/filter inputs

## 🐛 Troubleshooting

### Issue: Cannot connect to backend

**Solution**: Check `NEXT_PUBLIC_API_URL` in `.env.local`

```bash
# Verify environment variable
echo $NEXT_PUBLIC_API_URL
```

### Issue: "Module not found" error

**Solution**: Clear cache and reinstall

```bash
rm -rf .next node_modules
npm install
npm run dev
```

### Issue: Build fails on Vercel

**Solution**: Check Node.js version

```json
// Add to package.json
"engines": {
  "node": ">=18.0.0"
}
```

### Issue: CORS error in production

**Solution**: Update backend CORS configuration with your Vercel URL

## 📝 Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_API_URL` | Backend API URL | `http://localhost:3000` |

**Note**: All variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.

## 🔄 Updating Dependencies

```bash
# Check for outdated packages
npm outdated

# Update all dependencies
npm update

# Update specific package
npm install package-name@latest
```

## 📚 Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [TailwindCSS Documentation](https://tailwindcss.com/docs)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 👥 Support

For issues specific to the frontend:
- Check [GitHub Issues](https://github.com/yourusername/task-management-system/issues)
- Review this documentation
- Check browser console for errors

---

**Built with ❤️ using Next.js and TailwindCSS**