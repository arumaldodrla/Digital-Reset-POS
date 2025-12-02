# Yappy Payment Connector

## 1. Overview

The Yappy payment connector integrates the Universal Offline POS system with Yappy, a popular mobile payment platform in Panamá. This integration allows you to accept payments from your customers using Yappy.

## 2. Features

- **QR Code Payments**: Generate a unique QR code for each transaction that customers can scan with their Yappy app to make a payment.
- **Payment Links**: Send a payment link to customers via email or SMS, which they can use to make a payment with their Yappy app.
- **Real-time Payment Status**: Get real-time updates on the status of each payment.

## 3. Configuration

To configure the Yappy payment connector, you will need to provide the following information:

- **Yappy Merchant ID**: Your Yappy merchant ID.
- **Yappy Access Token**: Your Yappy access token.

This information can be obtained from your Yappy for Business account. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Payment Initiation**: When a customer chooses to pay with Yappy, the POS sends a request to the Yappy API to create a new payment.
2.  **QR Code/Payment Link Generation**: The Yappy API returns a unique QR code and payment link for the transaction.
3.  **Payment Confirmation**: The customer scans the QR code or clicks the payment link to make a payment with their Yappy app. Once the payment is complete, Yappy sends a webhook to the POS to confirm the payment.
4.  **Order Completion**: The POS receives the webhook, updates the order status to "completed", and prints a receipt for the customer.
