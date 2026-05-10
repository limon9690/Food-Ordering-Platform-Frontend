# Food Ordering Platform Frontend

Production-ready Next.js frontend for a multi-role food marketplace where users can discover home-cooked meals, place orders, and manage activity through role-based dashboards.

## Project Links

- Live URL: https://foodhub-frontend-puce.vercel.app/
- Backend GitHub Repository: https://github.com/limon9690/Food-Ordering-Platform-Backend

## Table of Contents

1. [Overview](#overview)
2. [Project Links](#project-links)
3. [Core Features](#core-features)
4. [Tech Stack](#tech-stack)
5. [Project Structure](#project-structure)
6. [Getting Started](#getting-started)
7. [Environment Variables](#environment-variables)
8. [Available Scripts](#available-scripts)
9. [Role and Access Model](#role-and-access-model)
10. [API Integration](#api-integration)
11. [Deployment Notes](#deployment-notes)
12. [Troubleshooting](#troubleshooting)

## Overview

FoodHub connects customers with local providers who publish meals.

The app supports three user roles:

- USER: browse meals and providers, manage cart, place and track orders
- PROVIDER: onboard as provider, manage menu, update order status
- ADMIN: monitor users and manage platform data such as categories

## Core Features

- Landing page with featured meals and providers
- Meal browsing with search and category filters
- Meal detail pages with provider info and reviews
- Provider discovery pages
- Client-side cart with checkout flow
- Order placement, listing, details, and cancellation actions
- Role-aware dashboard navigation and pages
- Provider onboarding flow
- Authentication with session-based access control
- Light and dark mode theming

## Tech Stack

- Framework: Next.js 16 (App Router)
- Language: TypeScript
- UI: Tailwind CSS v4, shadcn/ui, Radix UI, Lucide icons
- Forms and validation: TanStack Form, Zod
- Auth client: better-auth
- Notifications: Sonner

## Project Structure

```text
src/
	app/
		page.tsx                    # Home page
		meals/                      # Meal list and detail pages
		providers/                  # Provider list and detail pages
		cart/                       # Cart screen
		checkout/                   # Checkout flow
		become-a-provider/          # Provider onboarding
		dashboard/                  # Role-based dashboard areas
			admin/
			provider/
			orders/
			profile/
	components/                   # Shared UI and feature components
	service/                      # Server-side API call wrappers
	lib/                          # Auth client and utilities
	proxy.ts                      # Route protection and role checks
```

## Getting Started

### Prerequisites

- Node.js 20+
- pnpm 9+
- Running backend API for FoodHub

### Install and Run

```bash
pnpm install
pnpm dev
```

App will run at http://localhost:3000.

## Environment Variables

Create a local environment file (for example, .env.local) and set the following variables:

| Variable | Required | Description |
| --- | --- | --- |
| API_URL | Yes | Base URL of the backend API for server-side requests |
| NEXT_PUBLIC_API_URL | Recommended | Public API base URL for client-accessible flows |

Example:

```env
API_URL=http://localhost:5000/api
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

## Available Scripts

```bash
pnpm dev      # Start development server
pnpm build    # Create production build
pnpm start    # Start production server
pnpm lint     # Run ESLint
```

## Role and Access Model

Protected routes are enforced with a request proxy matcher.

- Protected: dashboard pages, cart, checkout, become-a-provider
- PROVIDER-only: provider dashboard sections
- ADMIN-only: admin dashboard sections
- USER-only: cart, checkout, provider onboarding

If a user is not authenticated, they are redirected to the login page.

## API Integration

The frontend is designed to work with a separate backend service.

- Most API interactions are handled in src/service
- Auth calls include credentials and cookies
- Next config includes auth route rewrite support for backend auth endpoints

## Deployment Notes

- Ensure all required environment variables are set in the deployment platform
- Confirm the backend API domain allows credentials and cookies for this frontend domain
- Run a production check before release:

```bash
pnpm lint
pnpm build
```