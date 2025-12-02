# WooCommerce Connector

## 1. Overview

The WooCommerce connector integrates the Universal Offline POS system with WooCommerce, a popular open-source e-commerce platform for WordPress. This integration allows for seamless synchronization of products, inventory, orders, and customers between the two systems.

## 2. Features

- **Product Sync**: Sync products, variations, and categories from WooCommerce to the POS.
- **Inventory Sync**: Sync inventory levels from WooCommerce to the POS in real-time.
- **Order Sync**: Sync orders from WooCommerce to the POS, allowing for in-store pickup and returns.
- **Customer Sync**: Sync customer data from WooCommerce to the POS.

## 3. Configuration

To configure the WooCommerce connector, you will need to provide the following information:

- **WooCommerce Store URL**: The URL of your WordPress site with WooCommerce installed.
- **WooCommerce Consumer Key**: Your WooCommerce consumer key.
- **WooCommerce Consumer Secret**: Your WooCommerce consumer secret.

This information can be obtained from your WordPress admin dashboard. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Product Sync**: When the connector is first configured, it will perform a full sync of all products from WooCommerce to the POS. After the initial sync, it will use webhooks to receive real-time updates of new and updated products.
2.  **Inventory Sync**: The connector uses webhooks to receive real-time updates of inventory levels from WooCommerce. When an inventory level changes in WooCommerce, a webhook is sent to the POS, which then updates the local inventory level.
3.  **Order Sync**: The connector uses webhooks to receive real-time updates of new orders from WooCommerce. When a new order is created in WooCommerce, a webhook is sent to the POS, which then creates a new order in the local database.
4.  **Customer Sync**: The connector uses webhooks to receive real-time updates of new and updated customers from WooCommerce. When a new customer is created or an existing customer is updated in WooCommerce, a webhook is sent to the POS, which then creates or updates the customer in the local database.
