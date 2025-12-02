# Shopify Connector

## 1. Overview

The Shopify connector integrates the Universal Offline POS system with Shopify, a leading e-commerce platform. This integration allows for seamless synchronization of products, inventory, orders, and customers between the two systems.

## 2. Features

- **Product Sync**: Sync products, variants, and collections from Shopify to the POS.
- **Inventory Sync**: Sync inventory levels from Shopify to the POS in real-time.
- **Order Sync**: Sync orders from Shopify to the POS, allowing for in-store pickup and returns.
- **Customer Sync**: Sync customer data from Shopify to the POS.

## 3. Configuration

To configure the Shopify connector, you will need to provide the following information:

- **Shopify Store URL**: The URL of your Shopify store (e.g., `your-store.myshopify.com`).
- **Shopify API Key**: Your Shopify API key.
- **Shopify API Password**: Your Shopify API password.

This information can be obtained from your Shopify admin dashboard. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Product Sync**: When the connector is first configured, it will perform a full sync of all products from Shopify to the POS. After the initial sync, it will use webhooks to receive real-time updates of new and updated products.
2.  **Inventory Sync**: The connector uses webhooks to receive real-time updates of inventory levels from Shopify. When an inventory level changes in Shopify, a webhook is sent to the POS, which then updates the local inventory level.
3.  **Order Sync**: The connector uses webhooks to receive real-time updates of new orders from Shopify. When a new order is created in Shopify, a webhook is sent to the POS, which then creates a new order in the local database.
4.  **Customer Sync**: The connector uses webhooks to receive real-time updates of new and updated customers from Shopify. When a new customer is created or an existing customer is updated in Shopify, a webhook is sent to the POS, which then creates or updates the customer in the local database.
