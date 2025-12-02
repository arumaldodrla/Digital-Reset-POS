# E-Invoicing Connectors

## 1. Overview

The Universal Offline POS system supports country-specific electronic invoicing (e-invoicing) through a set of pluggable connectors. This allows you to comply with local tax regulations and automatically generate electronic invoices for your sales.

## 2. Features

- **Automatic Invoice Generation**: Automatically generate electronic invoices for all sales and returns.
- **Digital Signatures**: Digitally sign invoices with a government-certified digital certificate.
- **Asynchronous Processing**: Invoices are processed asynchronously in the background, so your sales are not blocked if the tax authority API is slow or down.
- **Fiscal Number & QR Code**: Receive and store the official fiscal number and QR code for each invoice.

## 3. Configuration

To configure an e-invoicing connector, you will need to provide the following information:

- **Country**: The country for which you want to enable e-invoicing.
- **Digital Certificate**: Your government-certified digital certificate.
- **API Credentials**: Your API credentials for the tax authority API.

This information can be obtained from your local tax authority. Once you have this information, you can configure the connector in the POS admin backoffice.

## 4. Data Flow

1.  **Invoice Creation**: When a sale is made on the POS, a new invoice is created in the local database with a status of "pending".
2.  **Asynchronous Processing**: A background worker picks up the pending invoice and sends it to the tax authority API for processing.
3.  **Fiscalization**: The tax authority API processes the invoice, digitally signs it, and returns an official fiscal number and QR code.
4.  **Invoice Update**: The background worker receives the fiscal number and QR code and updates the invoice in the local database.
