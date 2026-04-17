## Live Preview - https://served-recipe-platform-my1m.vercel.app/

# AI Recipe Platform

AI Recipe Platform is a full-stack application that helps users cook with what they already have at home. It combines pantry scanning, AI recipe generation, saved recipes, and a recipe discovery experience in one product.

The project is split into two parts:
- a Next.js frontend for the app experience
- a Strapi backend for content and user-linked data storage

## What the app does

- Lets users sign up and sign in with Clerk
- Scans pantry images using Gemini Vision and extracts ingredients
- Generates structured recipes using Gemini with normalized categories and cuisines
- Fetches recipe images from Unsplash when available
- Saves recipes and pantry items to Strapi (PostgreSQL)
- Provides recipe discovery using TheMealDB (categories, cuisines, recipe of the day)
- Supports free and pro limits using Arcjet rate-limiting policies
- Exports recipes to PDF in the frontend

## Main features

### Pantry workflow

- Upload pantry/fridge photos
- Detect ingredients with quantity and confidence
- Save detected ingredients to personal pantry
- Add, edit, and delete pantry items manually

### Recipe workflow

- Search by recipe name
- Reuse existing recipes from the database when available
- Generate new recipes with AI when not found
- Save favorite recipes to a personal cookbook
- Read cooking instructions, tips, substitutions, and nutrition details

### Discovery workflow

- Browse by category and cuisine
- View recipe of the day
- Access external recipe lists through TheMealDB integration

### Plans and limits

- Free and Pro tier logic is handled in the app
- Example free limits currently used in UI and logic:
- Pantry scans: 10/month
- AI meal generations: 5/month
- Saved recipes: 3/month

## Tech stack

### Frontend

- Next.js 16 (App Router)
- React 19
- Tailwind CSS 4
- Clerk authentication
- Arcjet protection and rate limiting
- Radix UI primitives
- Sonner for toasts
- @react-pdf/renderer for PDF export

### Backend

- Strapi 5
- PostgreSQL (pg)
- Strapi Users & Permissions plugin

### AI and external APIs

- Google Gemini (text + vision)
- Unsplash (recipe imagery)
- TheMealDB (discovery data)

## Repository structure

```
ai-recipe-platform/
	frontend/   # Next.js application
	Backend/    # Strapi CMS/API
```

## Getting started

### 1) Prerequisites

- Node.js 20+
- npm
- PostgreSQL database for Strapi

### 2) Install dependencies

From the project root:

```bash
cd frontend && npm install
cd ../Backend && npm install
```

### 3) Configure environment variables

Create environment files for both apps.

For frontend, configure values used by server actions and auth:

```bash
# frontend/.env
NEXT_PUBLIC_STRAPI_URL=http://localhost:1337
STRAPI_API_TOKEN=your_strapi_api_token

NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

GEMINI_API_KEY=your_gemini_api_key
UNSPLASH_ACCESS_KEY=your_unsplash_access_key
```

For backend, configure database and Strapi values according to your local setup.

### 4) Run both services

Start backend:

```bash
cd Backend
npm run dev
```

Start frontend in a second terminal:

```bash
cd frontend
npm run dev
```

Then open http://localhost:3000.

## Useful scripts

Frontend:

- `npm run dev` - start development server
- `npm run build` - create production build
- `npm run start` - run production server
- `npm run lint` - run ESLint

Backend:

- `npm run dev` - start Strapi in development mode
- `npm run build` - build Strapi admin panel
- `npm run start` - run Strapi in production mode
- `npm run deploy` - deploy Strapi project

## Current data constraints used by AI recipe generation

- Category must be one of: breakfast, lunch, dinner, snack, dessert
- Cuisine is normalized to: italian, chinese, mexican, indian, american, thai, japanese, mediterranean, french, korean, vietnamese, spanish, greek, turkish, moroccan, brazilian, caribbean, middle-eastern, british, german, portuguese, other

## Notes

- `Backend` uses a capital B in folder name. Keep this exact path in commands.
- If you see hydration warnings during development, browser extensions can inject attributes into HTML and trigger harmless mismatches.

## License

This project is currently for personal/product development use. Add a formal license section when you are ready to open-source it.
