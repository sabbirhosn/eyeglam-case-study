# EyeGlam — E-Commerce Case Study

**Live site:** [eyeglambd.com](https://eyeglambd.com)

EyeGlam is a production eyewear e-commerce store serving customers in Bangladesh, which I designed, built, and operate end-to-end as a solo developer. This repository documents the architecture, key features, and technical decisions behind it. The source code is private because it powers a live business; this case study explains how it works.

---

## Overview

EyeGlam sells premium sunglasses and optical frames online, with delivery inside and outside Dhaka, cash-on-delivery support, and WhatsApp-based ordering — patterns that match how customers in Bangladesh actually shop. The site runs in production with real customers and a physical retail counterpart in Dhaka.

**My role:** everything — product design, frontend, backend, database, deployment, and ongoing operations.

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js (App Router) + React |
| Language | TypeScript |
| Styling | Tailwind CSS |
| Database | PostgreSQL (Supabase) |
| Backend | Next.js API routes + custom admin panel |
| Media | ImageKit CDN with `next/image` optimization |
| Hosting | Netlify, behind Cloudflare |

## Key Features

**Product catalog** — Browsable catalog with category filters (Men, Women, Kids, Magnetic Clip) and frame-shape filters (aviator, wayfarer, cat-eye, and more), driven by URL query parameters so every filtered view is shareable and indexable.

**Cart and wishlist** — Persistent cart and wishlist that survive navigation and page reloads, designed mobile-first since most traffic comes from phones.

**Wholesale portal** — A dedicated B2B page where retailers can inquire about bulk orders, separating wholesale flows from the consumer storefront.

**Style guide** — An interactive face-shape guide (round, square, oval, heart, diamond, oblong) that recommends frame styles and links directly into pre-filtered catalog views — turning styling advice into a conversion path.

**Custom frames** — A flow for customers to request personalized frames beyond the standard catalog.

**Custom admin panel** — An internal dashboard for managing products, images, pricing, and orders without touching code.

---

## Technical Challenges

### 1. Image performance on a photo-heavy storefront

**Problem.** An eyewear store lives and dies by product photography. Every page displays dozens of high-resolution images, and most customers browse on mid-range phones over mobile networks — full-size images made early versions slow to load.

**Solution.** I moved all media to ImageKit CDN and routed every image through Next.js `next/image`, which serves automatically resized, WebP-converted variants per device. Combined with lazy loading below the fold and Cloudflare edge caching in front of the site, product pages stay fast even with large galleries, without manually preprocessing each photo before upload.

### 2. Reliable cart and state management

**Problem.** Cart state has to feel instant and never lose items — across page navigations, reloads, and the add-to-cart interactions scattered throughout the catalog, lookbook, and product pages. Early on, state updates from different components could fall out of sync.

**Solution.** I centralized cart and wishlist state in a single client-side store shared by every component, with persistence so a returning visitor finds their cart intact. Add-to-cart updates are optimistic — the UI responds immediately while the state syncs in the background — which keeps the experience smooth on slower connections.

### 3. A custom admin panel for daily operations

**Problem.** The store changes daily — new arrivals, price updates, sales, stock changes — and it's operated without a developer in the loop. Off-the-shelf CMS options didn't fit the workflow (bilingual product entry, ImageKit uploads, category/shape tagging), so hand-editing data was not sustainable.

**Solution.** I built a custom admin dashboard on Next.js API routes backed by PostgreSQL (Supabase). It handles product CRUD, image uploads straight to ImageKit, pricing and sale management, and order tracking. Because it shares types and infrastructure with the storefront, a product added in the admin is immediately live on the site with correct filters, images, and SEO metadata.

---

## Screenshots

<!-- Add screenshots to a /screenshots folder and update the paths below -->

| View | Preview |
|---|---|
| Homepage | `screenshots/home.png` |
| Product catalog with filters | `screenshots/catalog.png` |
| Product detail page | `screenshots/product.png` |
| Style guide | `screenshots/style-guide.png` |
| Admin panel | `screenshots/admin.png` |

---

## What I'd Do Next

Planned improvements include online payment integration, order-status notifications, and analytics-driven merchandising. I'm also exploring agentic AI workflows (MCP, LLM APIs) to automate parts of store operations, such as product description generation and customer support triage.

---

## About Me

I'm **Muhammad Sabbir Hossain**, a self-taught full-stack developer. EyeGlam is my proof of work: a real product with real customers, built solo from first commit to production.

- 💼 [LinkedIn](https://www.linkedin.com/in/muhammad-sabbir-hossain-83aa64250/)
- 🐙 [GitHub](https://github.com/Sabbirhosn)
- ✉️ [asakashthereble@gmail.com](mailto:asakashthereble@gmail.com)
