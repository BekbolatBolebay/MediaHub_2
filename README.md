# MediaHub - Creative Platform

A mobile-first Next.js application for media professionals to connect, find opportunities, and grow their careers.

## Features

- **Mobile-First Design**: Optimized for small screens with responsive layouts
- **Dark Theme**: Professional dark theme with cyan/purple accents
- **Authentication System**: Login, register, and password reset pages with validation
- **Bottom Navigation**: 5-tab navigation (Home, Jobs, Upload, Learn, Profile)
- **Test Mode Toggle**: Developer feature for testing (visible to dev users)
- **Accessibility**: Full ARIA support, keyboard navigation, and screen reader compatibility
- **Upload & Delivery System**: Professional media upload, client preview, and delivery workflow

## Pages

- **Home**: Media feed with infinite scroll, category tiles, and interactive media cards
- **Jobs**: Job listings with search, filters, and detailed job cards
- **Upload**: Multi-file uploader with progress tracking, media management, and client delivery
- **Learn**: Course catalog with categories, search, and detailed course info
- **Profile**: User profile with posts, achievements, and activity tabs
- **Auth**: Login, register, and password reset pages with form validation

## Upload & Delivery System

The comprehensive upload system includes:

### Multi-File Upload
- Drag & drop interface with progress tracking
- Support for images, videos, audio, and documents up to 500MB
- Automatic low-res preview generation
- Real-time upload status and error handling

### Media Management
- Metadata editing (title, description, category, tags, pricing)
- Visibility controls (public, unlisted, private)
- Preview generation and quality toggles
- Batch operations and file organization

### Client Preview System
- Send preview modal with client search and selection
- DRM protection options (watermarks, download restrictions)
- Time-limited and view-limited preview links
- Custom messaging and branding options

### Feedback Workflow
- Client feedback widget with thumbs up/down ratings
- Comment system for detailed feedback
- Revision request handling and tracking
- Status management (pending, approved, revision requested)

### Delivery System
- Full-resolution file delivery with signed URLs
- 48-hour expiry and download limits
- Secure delivery tracking and analytics
- Automated client notifications

## Required Environment Variables

### Firebase Configuration
\`\`\`env
# Firebase Authentication
FIREBASE_API_KEY=your_firebase_api_key
FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_STORAGE_BUCKET=your_project.appspot.com
FIREBASE_MESSAGING_SENDER_ID=your_sender_id
FIREBASE_APP_ID=your_app_id

# Optional: Firebase Analytics
FIREBASE_MEASUREMENT_ID=your_measurement_id
\`\`\`

### Cloudflare R2 Storage
\`\`\`env
# R2 Configuration for direct uploads
CF_ACCOUNT_ID=your_cloudflare_account_id
CF_R2_ACCESS_KEY_ID=your_r2_access_key
CF_R2_SECRET_ACCESS_KEY=your_r2_secret_key
CF_R2_BUCKET=your_r2_bucket_name
\`\`\`

## API Endpoints

The upload system expects these API endpoints:

### Presigned Upload URLs
\`\`\`typescript
POST /api/r2/presign
Body: { filename: string, contentType: string }
Response: { url: string, key: string }
\`\`\`

### Preview Link Generation
\`\`\`typescript
POST /api/preview/create
Body: { 
  fileId: string, 
  clientEmail: string, 
  drmOptions: {
    watermark: boolean,
    disableDownload: boolean,
    timeLimit: string,
    viewLimit: string
  }
}
Response: { previewUrl: string, expiresAt: string }
\`\`\`

### Delivery URL Generation
\`\`\`typescript
POST /api/delivery/generate
Body: { fileId: string, clientEmail: string }
Response: { downloadUrl: string, expiresAt: string }
\`\`\`

## Tech Stack

- **Framework**: Next.js 14 with App Router
- **Styling**: Tailwind CSS v4 with custom design tokens
- **Components**: shadcn/ui component library
- **Icons**: Lucide React
- **Fonts**: Geist Sans & Geist Mono
- **State Management**: React Context for authentication
- **Storage**: Cloudflare R2 with presigned uploads
- **Database**: Firestore for metadata and delivery tracking
- **TypeScript**: Full type safety

## Getting Started

1. Clone the repository
2. Install dependencies: `npm install`
3. Add environment variables to `.env.local`
4. Set up Cloudflare R2 bucket and API keys
5. Configure Firebase project and authentication
6. Run development server: `npm run dev`
7. Open [http://localhost:3000](http://localhost:3000)

## Authentication

The app includes a mock authentication system that can be easily replaced with Firebase Auth. The current implementation includes:

- Login with email/password
- User registration with validation
- Password reset functionality
- Test mode toggle for developers
- Protected routes and user context

## Design System

- **Colors**: Dark theme with semantic design tokens
- **Typography**: Geist font family with proper hierarchy
- **Components**: Rounded cards with soft shadows
- **Spacing**: Consistent spacing scale using Tailwind
- **Accessibility**: WCAG compliant with proper contrast ratios

## Deployment

Deploy to Vercel with one click or push to GitHub and connect your repository.

## License

MIT License - feel free to use this project as a starting point for your own applications.
