# Production Deployment Guide

## 1. Introduction

This guide explains how to deploy the Universal Offline POS system to a production environment on Vercel. The production environment is the live environment that is used by your customers.

## 2. Prerequisites

- A Vercel account.
- The project pushed to a GitHub repository.
- A custom domain name.

## 3. Vercel Project Setup

1.  **Create a new project on Vercel** and connect it to your GitHub repository.
2.  **Configure the build settings**:
    - **Framework Preset**: Next.js
    - **Build Command**: `pnpm build`
    - **Install Command**: `pnpm install`
    - **Output Directory**: `.next`
3.  **Configure environment variables**:
    - `NEXT_PUBLIC_SUPABASE_URL`: The URL of your production Supabase project.
    - `NEXT_PUBLIC_SUPABASE_ANON_KEY`: The `anon` key of your production Supabase project.
4.  **Configure custom domain**: Add your custom domain to the Vercel project and configure the DNS settings as instructed.

## 4. Deployment

Vercel will automatically deploy the application whenever you push a new commit to the `main` branch of your GitHub repository. It is recommended to use a Git branching strategy (e.g., GitFlow) to manage your production releases.

## 5. Production Database

It is recommended to use a separate Supabase project for the production environment. This ensures that your production data is isolated from your staging and local data. You should also enable daily backups for your production database.
