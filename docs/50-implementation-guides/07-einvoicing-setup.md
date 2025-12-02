# E-Invoicing Setup

## 1. Overview

This guide explains how to set up the e-invoicing integration.

## 2. Steps

### Step 1: Configure the E-Invoicing Connector

1.  Navigate to the "Integrations" section of the admin backoffice.
2.  Select the e-invoicing connector for your country (e.g., "Panama DGI").
3.  Enter your API credentials and upload your digital certificate.

### Step 2: Test the Integration

1.  Create a new order on the POS and complete the sale.
2.  Navigate to the "Invoices" section of the admin backoffice and verify that a new invoice has been created with a status of "pending".
3.  After a few minutes, verify that the invoice status has changed to "completed" and that a fiscal number and QR code have been assigned.
