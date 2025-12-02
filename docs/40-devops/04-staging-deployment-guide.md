# Staging Deployment Guide

## 1. Introduction

This guide explains how to deploy the Universal Offline POS system to a staging environment on Vercel. The staging environment is used for testing and quality assurance before deploying to production.

## 2. Prerequisites

- A Vercel account.
- The project pushed to a GitHub repository.

## 3. Vercel Project Setup

1.  **Create a new project on Vercel** and connect it to your GitHub repository.
2.  **Configure the build settings**:
    - **Framework Preset**: Next.js
    - **Build Command**: `pnpm build`
    - **Install Command**: `pnpm install`
    - **Output Directory**: `.next`
3.  **Configure environment variables**:
    - `NEXT_PUBLIC_SUPABASE_URL`: The URL of your staging Supabase project.
    - `NEXT_PUBLIC_SUPABASE_ANON_KEY`: The `anon` key of your staging Supabase project.

## 4. Deployment

Vercel will automatically deploy the application whenever you push a new commit to the `main` branch of your GitHub repository. You can also manually trigger a deployment from the Vercel dashboard.

## 5. Staging Database

It is recommended to use a separate Supabase project for the staging environment. This ensures that your staging data is isolated from your production data. You can create a new Supabase project from the Supabase dashboard and use its URL and `anon` key in your Vercel environment variables.
