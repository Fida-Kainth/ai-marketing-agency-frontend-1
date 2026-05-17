# AI Marketing Agency - Frontend

Modern, responsive frontend application built with Next.js 14 for the AI Marketing Agency platform.

## 🚀 Features

### User Features
- **Authentication**: Email/password, Google OAuth, Facebook OAuth
- **Dashboard**: Comprehensive analytics and insights
- **AI Tools**:
  - Content generation (blog posts, social media, ads)
  - Image generation with DALL-E
  - SEO optimization suggestions
  - Chatbot builder
  - values are assigned. 
- **Campaign Management**: Create, edit, and track 
marketing campaigns
- **Social Media**: Schedule and automate posts
- **Analytics**: Real-time performance metrics
- **Client Management**: Organize and manage clients
- **Billing**: View invoices and payment history
- **Profile**: Manage account settings and preferences

### Admin Features
- User management
- Platform statistics
- System settings
- Audit logs

## 🛠️ Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **Authentication**: JWT with HTTP-only cookies
- **State Management**: React Context API
- **HTTP Client**: Native Fetch API
- **Forms**: React Hook Form (if needed)
- **UI Components**: Custom components with Tailwind
- **Icons**: Heroicons or Lucide React

## 📋 Prerequisites

- Node.js (v18.0.0 or higher)
- npm or yarn
- Backend API running (see backend README)

## 🔧 Installation

1. **Navigate to frontend directory**:
```bash
cd frontend
```

2. **Install dependencies**:
```bash
npm install
```

3. **Set up environment variables**:
```bash
cp .env.example .env.local
```

Edit `.env.local` with your configuration:
```env
NEXT_PUBLIC_API_URL=http://localhost:3000
```

## 🚦 Running the Application

### Development Mode
```bash
npm run dev
```

The application will be available at `http://localhost:3001`

### Production Mode
```bash
# Build the application
npm run build

# Start the production server
npm start
```

### Linting
```bash
# Run ESLint
npm run lint

# Fix linting issues
npm run lint:fix
```

## 📁 Project Structure

```
frontend/
├── public/                 # Static assets
│   ├── images/            # Images
│   ├── icons/             # Icons
│   └── ...
│
├── src/
│   ├── app/               # Next.js 14 App Router
│   │   ├── (auth)/       # Auth routes group
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   │
│   │   ├── (dashboard)/  # Dashboard routes group
│   │   │   ├── dashboard/
│   │   │   ├── campaigns/
│   │   │   ├── clients/
│   │   │   ├── analytics/
│   │   │   └── settings/
│   │   │
│   │   ├── admin/        # Admin routes
│   │   ├── ai/           # AI tools
│   │   │   ├── content/
│   │   │   └── images/
│   │   │
│   │   ├── layout.tsx    # Root layout
│   │   ├── page.tsx      # Home page
│   │   └── globals.css   # Global styles
│   │
│   ├── components/        # Reusable components
│   │   ├── auth/         # Auth components
│   │   ├── chatbot/      # Chatbot components
│   │   ├── layout/       # Layout components
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   └── Sidebar.tsx
│   │   ├── ui/           # UI components
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Card.tsx
│   │   │   └── Modal.tsx
│   │   └── ...
│   │
│   └── lib/              # Utilities and helpers
│       ├── api.ts        # API client
│       ├── auth.ts       # Auth utilities
│       ├── auth-context.tsx  # Auth context
│       ├── utils.ts      # Helper functions
│       └── constants.ts  # Constants
│
├── .env.example          # Environment variables template
├── .env.local            # Local environment variables (git-ignored)
├── .gitignore
├── next.config.ts        # Next.js configuration
├── tailwind.config.js    # Tailwind CSS configuration
├── tsconfig.json         # TypeScript configuration
├── package.json
└── README.md
```

## 🎨 Styling

This project uses Tailwind CSS for styling. The configuration can be found in `tailwind.config.js`.

### Custom Colors
```javascript
// Example custom colors in tailwind.config.js
colors: {
  primary: '#3B82F6',
  secondary: '#8B5CF6',
  accent: '#10B981',
}
```

## 🔐 Authentication

The app uses JWT-based authentication with HTTP-only cookies for security.

### Auth Flow
1. User logs in via `/auth/login`
2. Backend returns JWT token
3. Token is stored in HTTP-only cookie
4. Token is sent with each API request
5. Protected routes check authentication status

### Protected Routes
Use the `AuthContext` to protect routes:

```typescript
'use client';

import { useAuth } from '@/lib/auth-context';
import { useRouter } from 'next/navigation';
import { useEffect } from 'react';

export default function ProtectedPage() {
  const { user, loading } = useAuth();
  const router = useRouter();

  useEffect(() => {
    if (!loading && !user) {
      router.push('/auth/login');
    }
  }, [user, loading, router]);

  if (loading) return <div>Loading...</div>;
  if (!user) return null;

  return <div>Protected Content</div>;
}
```

## 🌐 API Integration

The API client is located in `src/lib/api.ts`:

```typescript
// Example API call
import { apiClient } from '@/lib/api';

const campaigns = await apiClient.get('/campaigns');
const newCampaign = await apiClient.post('/campaigns', data);
```

## 📱 Pages Overview

### Public Pages
- `/` - Landing page
- `/auth/login` - Login page
- `/auth/register` - Registration
- `/auth/forgot-password` - Password recovery
- `/services` - Services overview
- `/pricing` - Pricing plans
- `/contact` - Contact form
- `/blog` - Blog posts

### Protected Pages
- `/dashboard` - User dashboard
- `/campaigns` - Campaign management
- `/campaigns/create` - Create campaign
- `/campaigns/[id]/edit` - Edit campaign
- `/clients` - Client management
- `/ai/content` - AI content generator
- `/ai-images` - AI image generator
- `/chatbot` - Chatbot builder
- `/chatbot-demo` - Chatbot demo
- `/analytics` - Analytics dashboard
- `/profile` - User profile
- `/settings` - Account settings

### Admin Pages
- `/admin` - Admin dashboard
- `/admin/users` - User management
- `/admin/settings` - System settings

## 🔧 Configuration

### Next.js Config
Key settings in `next.config.ts`:

```typescript
const config = {
  reactStrictMode: true,
  images: {
    domains: ['localhost', 'your-api-domain.com'],
  },
};
```

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `NEXT_PUBLIC_API_URL` | Backend API URL | ✅ |
| `NEXT_PUBLIC_GOOGLE_CLIENT_ID` | Google OAuth Client ID | For OAuth |
| `NEXT_PUBLIC_FACEBOOK_APP_ID` | Facebook App ID | For OAuth |
| `NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY` | Stripe Publishable Key | For payments |

## 🚀 Deployment

### Vercel (Recommended)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### Manual Deployment
```bash
# Build
npm run build

# The output will be in the .next folder
# Deploy the entire project to your hosting provider
```

### Environment Variables in Production
Make sure to set all required environment variables in your hosting provider's dashboard.

## 🧪 Testing

```bash
# Run tests (if configured)
npm run test

# Run tests in watch mode
npm run test:watch
```

## 📊 Performance Optimization

- **Image Optimization**: Use Next.js `<Image>` component
- **Code Splitting**: Automatic with Next.js App Router
- **Lazy Loading**: Use `dynamic` imports for heavy components
- **Caching**: Leverage Next.js caching strategies

```typescript
// Example: Dynamic import
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('@/components/HeavyComponent'), {
  loading: () => <p>Loading...</p>,
});
```

## 🔒 Security Best Practices

- Never expose sensitive data in client-side code
- Use environment variables for configuration
- Validate all user inputs
- Sanitize data before rendering
- Use HTTPS in production
- Implement CSP (Content Security Policy)
- Keep dependencies updated

## 📝 Code Style

This project follows:
- ESLint configuration
- Prettier for code formatting
- TypeScript strict mode

```bash
# Format code
npm run format

# Check types
npm run type-check
```

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Update documentation if needed
5. Submit a pull request

## 🐛 Troubleshooting

### Common Issues

**Issue**: API calls failing
- Check if backend is running
- Verify `NEXT_PUBLIC_API_URL` in `.env.local`
- Check browser console for CORS errors

**Issue**: Authentication not working
- Clear browser cookies
- Check JWT token expiration
- Verify backend authentication endpoints

**Issue**: Styles not loading
- Run `npm run dev` again
- Clear `.next` folder and rebuild

## 📄 License

ISC

## 👨‍💻 Support

For support, email aimarketingagencyhelp@gmail.com or create an issue in the repository.

## 🔄 Version History

- **v1.0.0** - Initial release
  - Next.js 14 App Router
  - Authentication system
  - Dashboard and campaign management
  - AI tools integration
  - Responsive design
#   A I - m a r k e t i n g - c h e c k 
 
 