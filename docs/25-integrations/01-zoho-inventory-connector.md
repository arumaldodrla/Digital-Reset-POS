# Zoho Inventory Connector

## 1. Overview

The Zoho Inventory connector integrates the Universal Offline POS system with Zoho Inventory, a comprehensive inventory management solution. This integration allows for seamless synchronization of products, stock levels, and other inventory-related data between the two systems.

## 2. Features

- **Product Sync**: Sync products, variants, and categories from Zoho Inventory to the POS.
- **Stock Level Sync**: Sync stock levels from Zoho Inventory to the POS in real-time.
- **Sales Sync**: Post sales and returns from the POS to Zoho Inventory to automatically update stock levels.
- **Purchase Order Sync**: Sync purchase orders from Zoho Inventory to the POS.

## 3. Configuration

To configure the Zoho Inventory connector, you will need to provide the following information:

- **Zoho Inventory API Key**: Your Zoho Inventory API key.
- **Zoho Inventory Organization ID**: The ID of your Zoho Inventory organization.

This information can be obtained from your Zoho Inventory account. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Product Sync**: When the connector is first configured, it will perform a full sync of all products from Zoho Inventory to the POS. After the initial sync, it will periodically poll Zoho Inventory for new and updated products.
2.  **Stock Level Sync**: The connector uses webhooks to receive real-time updates of stock levels from Zoho Inventory. When a stock level changes in Zoho Inventory, a webhook is sent to the POS, which then updates the local stock level.
3.  **Sales Sync**: When a sale is made on the POS, the connector creates a new sales order in Zoho Inventory. This automatically updates the stock level of the sold items.
4.  **Purchase Order Sync**: When a purchase order is created in Zoho Inventory, it is synced to the POS. This allows you to receive items against the purchase order directly from the POS.
