# Next.js Social Feed App

A modern social media feed application built with Next.js 14, featuring optimistic UI updates, server actions, and Cloudinary image uploads.

## Features

- 📝 **Create Posts** - Share posts with title, content, and images
- ❤️ **Like System** - Like/unlike posts with optimistic UI updates
- 🖼️ **Image Upload** - Upload and optimize images via Cloudinary
- ⚡ **Server Actions** - Modern Next.js server-side mutations
- 🎨 **Responsive Design** - Mobile-friendly interface
- 🔄 **Optimistic Updates** - Instant UI feedback using React's `useOptimistic` hook
- 💾 **SQLite Database** - Local database with better-sqlite3
- 🚀 **Loading States** - Suspense boundaries for better UX

## Tech Stack

- **Framework:** Next.js 14.1.0 (App Router)
- **React:** 18.x with Server Components
- **Database:** SQLite (better-sqlite3)
- **Image Hosting:** Cloudinary
- **Styling:** CSS Modules
- **Font:** Google Fonts (Merriweather)

## Getting Started

### Prerequisites

- Node.js 18+ installed
- A Cloudinary account ([Sign up free](https://cloudinary.com/users/register/free))

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd 08-optimization
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   
   Create a `.env` file in the root directory:
   ```bash
   CLOUDINARY_CLOUD_NAME=your_cloud_name_here
   CLOUDINARY_API_KEY=your_api_key_here
   CLOUDINARY_API_SECRET=your_api_secret_here
   ```

   **To find your Cloudinary credentials:**
   - Go to [Cloudinary Console](https://console.cloudinary.com/)
   - Find the "Product Environment Credentials" section on your dashboard
   - Copy the Cloud Name, API Key, and API Secret

4. **Run the development server**
   ```bash
   npm run dev
   ```

5. **Open the app**
   
   Navigate to [http://localhost:3000](http://localhost:3000)

## Project Structure

```
08-optimization/
├── actions/
│   └── posts.js           # Server actions for post operations
├── app/
│   ├── globals.css        # Global styles
│   ├── layout.js          # Root layout
│   ├── page.js            # Home page
│   ├── feed/
│   │   ├── page.js        # Feed page
│   │   ├── loading.js     # Loading state
│   │   └── error.js       # Error boundary
│   └── new-post/
│       ├── page.js        # Create post page
│       └── error.js       # Error boundary
├── components/
│   ├── header.js          # Navigation header
│   ├── posts.js           # Posts list with optimistic updates
│   ├── post-form.js       # Create post form
│   ├── form-submit.js     # Submit button component
│   └── like-icon.js       # Like button SVG
├── lib/
│   ├── posts.js           # Database queries
│   ├── cloudinary.js      # Image upload utility
│   └── format.js          # Date formatting
└── assets/
    └── logo.png           # App logo
```

## Key Features Explained

### Optimistic UI Updates

The app uses React's `useOptimistic` hook to provide instant feedback when users like/unlike posts:

```javascript
const [optimisticPosts, updateOptimisticPosts] = useOptimistic(posts, ...);
```

This creates a responsive user experience without waiting for server confirmation.

### Server Actions

All mutations use Next.js server actions for type-safe, server-side operations:

- `createPost` - Create new posts with image upload
- `togglePostLikeStatus` - Like/unlike posts

### Image Optimization

Images are uploaded to Cloudinary and rendered using Next.js `Image` component for automatic optimization:

- Automatic format selection (WebP, AVIF)
- Responsive image sizing
- Lazy loading
- Blur placeholder support

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm start` - Start production server
- `npm run lint` - Run ESLint

## Database

The app uses SQLite with better-sqlite3 for local data persistence. The database stores:

- Posts (title, content, image URL, user ID, creation date)
- Likes (post ID, user ID)
- Users (basic user information)

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `CLOUDINARY_CLOUD_NAME` | Your Cloudinary cloud name | ✅ Yes |
| `CLOUDINARY_API_KEY` | Your Cloudinary API key | ✅ Yes |
| `CLOUDINARY_API_SECRET` | Your Cloudinary API secret | ✅ Yes |

## Troubleshooting

### Module Not Found: Can't resolve 'next/image'

Make sure the import is correct:
```javascript
import Image from 'next/image'; // ✅ Correct
// NOT: import Image from '/next/image'; // ❌ Wrong
```

### Cloudinary Upload Fails

- Verify your `.env` file has the correct credentials
- Check that the credentials don't have quotes around them
- Restart the dev server after updating `.env`

### Images Not Displaying

- Ensure the `.post-image` container has `position: relative`
- For dynamic images, use the `fill` prop with explicit container dimensions
- Add Cloudinary domain to `next.config.mjs`:
  ```javascript
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'res.cloudinary.com',
      },
    ],
  }
  ```

## Learning Resources

This project demonstrates:

- ✅ Next.js App Router and Server Components
- ✅ React Server Actions
- ✅ Optimistic UI updates
- ✅ Image optimization with Cloudinary
- ✅ Form handling and validation
- ✅ Error boundaries and loading states
- ✅ Revalidation and caching strategies

## License

This project is for educational purposes.

## Acknowledgments

Built as part of a Next.js optimization learning module.
