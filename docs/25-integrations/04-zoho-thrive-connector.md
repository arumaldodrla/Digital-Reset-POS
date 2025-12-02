# Zoho Thrive Connector

## 1. Overview

The Zoho Thrive connector integrates the Universal Offline POS system with Zoho Thrive, a loyalty marketing platform. This integration allows you to run a comprehensive loyalty program for your customers, with points, tiers, and custom rewards.

## 2. Features

- **Customer Enrollment**: Enroll customers in your loyalty program directly from the POS.
- **Points & Rewards**: Award points to customers for their purchases and allow them to redeem rewards at the point of sale.
- **Tier Management**: Automatically upgrade customers to higher tiers based on their spending.
- **Loyalty Data Display**: Display customer loyalty points and tier information at the point of sale.

## 3. Configuration

To configure the Zoho Thrive connector, you will need to provide the following information:

- **Zoho Thrive API Key**: Your Zoho Thrive API key.
- **Zoho Thrive Organization ID**: The ID of your Zoho Thrive organization.

This information can be obtained from your Zoho Thrive account. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Customer Enrollment**: When a new customer is enrolled in the loyalty program on the POS, the connector creates a new contact in Zoho Thrive.
2.  **Sales Sync**: When a sale is made on the POS, the connector sends the transaction details to Zoho Thrive. Zoho Thrive then calculates the points earned by the customer and updates their loyalty profile.
3.  **Reward Redemption**: When a customer redeems a reward on the POS, the connector sends the redemption details to Zoho Thrive. Zoho Thrive then updates the customer's loyalty profile to reflect the redeemed reward.
