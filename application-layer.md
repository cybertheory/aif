# Application Layer API

The Automated Integration Framework (AIF) provides an API that allows developers to build applications that leverage the framework's capabilities. This document outlines the API endpoints and usage guidelines.

## API Overview

The AIF Application Layer API uses RESTful principles and returns JSON responses. All API requests should be made to the base URL of your AIF installation.

Base URL: `https://your-aif-instance.com/api/v1`

## Authentication

All API requests must include an API key in the header:

Authorization: Bearer YOUR_API_KEY

## Endpoints

### 1. Query Integrated Data

Retrieve data from integrated systems based on a natural language query.

# Get /query
Parameters:
- `q` (required): The natural language query string

Example:
GET /query?q=Show me all customers who made a purchase in the last 30 days


### 2. Perform Cross-System Action

Execute an action that may involve multiple integrated systems.

POST /action
Request body:
```json
{
  "action": "create_invoice",
  "parameters": {
    "customer_id": "123",
    "items": [
      {"product_id": "456", "quantity": 2},
      {"product_id": "789", "quantity": 1}
    ]
  }
}
```

## 3. Get Schema Information
Retrieve schema information for a specific object type across all integrated systems.
GET /schemas/{object_type}

Example:
GET /schemas/customer


## 4. Initiate Integration Job
Start a new integration job between two systems.

POST /integrations/jobs

Request body:
```json
{
  "source_system": "CRM",
  "target_system": "ERP",
  "object_type": "customer",
  "action": "sync"
}
```
## 5. Get Integration Status

Check the status of an integration job.

GET /integrations/jobs/{job_id}

Error Handling
The API uses standard HTTP status codes to indicate the success or failure of requests. In case of an error, the response will include a JSON object with an error key providing more details about the error.
Example error response:
```json
{
  "error": {
    "code": "invalid_query",
    "message": "The provided query could not be processed. Please rephrase and try again."
  }
}
```

## Rate Limiting

The API enforces rate limiting to ensure fair usage. The current limits are:

1000 requests per hour
10 requests per second

If you exceed these limits, you'll receive a 429 Too Many Requests response.

## Webhook Support
For long-running operations, you can provide a webhook URL to receive notifications about job completion or important events.

To register a webhook:

POST /webhooks

Request body:

```json
Copy{
  "url": "https://your-app.com/aif-webhook",
  "events": ["job.completed", "integration.error"]
}
```

## SDK Support

To simplify integration with the AIF API, we provide SDKs for popular programming languages:

Python: aif-python-sdk
JavaScript: aif-js-sdk
Java: aif-java-sdk

These SDKs provide convenient wrapper functions for all API endpoints and handle authentication and error management.
Best Practices

Use appropriate error handling in your applications to gracefully manage API errors.
Implement exponential backoff for retries in case of rate limiting or temporary server issues.
Keep your API key secure and rotate it regularly.
Monitor your API usage to stay within rate limits and optimize your requests.

For further assistance or to report issues, please contact our support team or open an issue in the AIF GitHub repository.