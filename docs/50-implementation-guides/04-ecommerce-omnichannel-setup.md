# E-commerce and Omnichannel Setup

## 1. Overview

This guide explains how to set up the e-commerce and omnichannel features of the Universal Offline POS system. This allows you to sync your products, inventory, orders, and customers between your POS and your online store.

## 2. Steps

### Step 1: Configure the E-commerce Connector

1.  Navigate to the "Integrations" section of the admin backoffice.
2.  Select the e-commerce platform you want to connect to (e.g., Shopify, WooCommerce).
3.  Enter your API credentials and configure the connector settings.

### Step 2: Configure the Inventory Master

1.  In the connector settings, you can choose which system should be the "inventory master". This is the system that is considered the source of truth for inventory levels.
2.  If you choose the POS as the inventory master, then all inventory changes will be pushed from the POS to your online store.
3.  If you choose your online store as the inventory master, then all inventory changes will be pulled from your online store to the POS.

### Step 3: Test the Integration

1.  Create a new product in your online store and verify that it is synced to the POS.
2.  Make a sale on the POS and verify that the inventory level is updated in your online store.
3.  Create a new order in your online store and verify that it is synced to the POS.
