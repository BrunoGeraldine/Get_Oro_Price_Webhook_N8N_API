
<p align="center">
  <img src="./img/Integration between Provider_API .jpg" width="1400" alt="Gold Price Integration"/>
</p>


# Gold Price Integration

This project contains a production-ready n8n solution for collecting gold price data, storing it in SQL Server, exposing it through a REST endpoint, and managing operational errors with centralized logging and email alerts.

## What This Solution Does

- Fetches the latest gold price from an external XML provider
- Retrieves the exchange-rate data required by the pricing model
- Stores current, historical, and daily records in SQL Server
- Exposes the latest price through a webhook-based JSON API
- Logs execution results and sends alerts when failures occur

## Project Components


<table align="center">
  <tr>
    <td><img src="./img/Webhook - Gold Price Rest API.jpg" width="750" alt="Webhook - Gold Price REST API" /></td>
    <td><img src="./img/Metal Rates Integration - Error LOG.jpg" width="750" alt="Metal Rates Integration - Error LOG" /></td>
  </tr>
</table>

<p align="center">
  <sub>"Webhook - Gold Price REST API"</sub>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <sub>"Metal Rates Integration - Error LOG"</sub>
</p>


The production workflows are stored in [Workflow-in-production](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production):

- [Gold Price.json](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production/Gold%20Price.json)
  Main scheduled workflow for data collection, transformation, and SQL persistence.

- [Metal Rates Integration - Error LOG.json](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production/Metal%20Rates%20Integration%20-%20Error%20LOG.json)
  Dedicated workflow for centralized error capture, SQL logging, and email notification.


- [Webhook - Gold Price REST API.json](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production/Webhook%20-%20Gold%20Price%20REST%20API.json)
  Read-only REST API workflow that returns the latest gold price as JSON.

- [doc_flusso_n8n.md](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production/doc_flusso_n8n.md)
  Full technical documentation for every workflow step and process.

## Data Flow

1. A scheduled workflow calls the external provider and the FX API.
2. The payloads are merged and filtered for valid 24K gold data.
3. SQL statements write records to current, history, and daily tables.
4. A separate webhook workflow exposes the latest value to other systems.
5. A dedicated error workflow records failures and sends alerts.

## Expected SQL Tables

The workflows reference the following tables:

- `Metal_Rates_Current`
- `Metal_Rates_History`
- `Metal_Rates_Daily`
- `Integration_Log`

## Before Using in Production

- Configure the real provider URL in the main workflow
- Map the SQL credentials after importing the workflows into n8n
- Update the SMTP configuration and recipient addresses
- Confirm that the SQL table names match your target database
- Test the scheduler, SQL writes, webhook response, and error notifications

## Notes

- The workflow files and labels have been sanitized.
- Some connection names, URLs, and email addresses are placeholders and must be updated in the target environment.
- The technical behavior is documented in detail in [doc_flusso_n8n.md](/home/bgeraldine/projetos/repos/Get_Oro_Price_Webhook_N8N_API/Workflow-in-production/doc_flusso_n8n.md).
