# Tenant Onboarding Guide

## 1. Overview

This guide explains how to onboard a new tenant (business) to the Universal Offline POS system. The process involves creating a new tenant, configuring the first location, and creating the first user.

## 2. Steps

### Step 1: Create a New Tenant

1.  Navigate to the super admin dashboard.
2.  Click on the "New Tenant" button.
3.  Enter the name of the business and click "Create".

This will create a new tenant in the database and assign it a unique `tenant_id`.

### Step 2: Create the First Location

1.  Navigate to the newly created tenant's dashboard.
2.  Click on the "New Location" button.
3.  Enter the name and address of the location and click "Create".

This will create a new location associated with the tenant.

### Step 3: Create the First User

1.  Navigate to the "Users" section of the tenant's dashboard.
2.  Click on the "New User" button.
3.  Enter the user's full name, email address, and select a role (e.g., "Admin").
4.  Click "Create".

This will create a new user in Supabase Auth and send an invitation email to the user. The user will need to click the link in the email to set their password and log in to the system.
