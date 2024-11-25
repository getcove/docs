### Getting Started with Cove API

Welcome to the Cove API! This guide will help you set up and integrate Cove’s powerful Verification as a Service platform into your system. Follow these steps to begin your integration journey seamlessly.

***

### What Cove Provides

Cove equips you with the tools and information you need to get started:

* **Bearer Token:** Used to authenticate and identify your organization.

* **Application ID:** Links requests to the specific application being processed.

* **Sandbox Environment:** Use the following sandbox URL to test your integration:

```arduino
https://cove-stage.vercel.app/screening?propertyId=673d144cec42f3c5005d5595
```

*


***

### What You Need to Set Up

To start using the Cove API, you'll need to configure:

1. **Webhook URL:** Specify the URL where Cove will send webhook notifications for completed verifications, including applicant and financial data.

2. **Custom Branding:** Define the colors, logos, text, and other design elements for the connection page to match your application’s look and feel.

***

### API Integration Steps

#### 1. **Request API Credentials**

To interact with Cove’s API, you’ll need valid login credentials. Contact [concierge@getcove.co]() to request your credentials.

#### 2. **Authentication**

* Authenticate your requests by calling the `/login` endpoint with your credentials to generate a bearer token.

* Use the token in the `Authorization` header for all subsequent API calls:


```makefile
Authorization: Bearer <your_token>
```

*

#### 3. **Set Up the Webhook**

* Configure your webhook endpoint to receive notifications from Cove.

* Webhooks are triggered after each verification step, keeping you updated in real time.

#### 4. **Test in the Sandbox**

* Use the provided sandbox URL to simulate and validate your API integration.

* Test webhook functionality and endpoint calls to ensure smooth production deployment.

***

### API Features

The Cove API provides functionality to:

* Manage property data (e.g., create or fetch property details).

* Send screening requests to users for verification.

* Retrieve screening data, including financial and identity verification results.

***

### Example Authentication Flow

#### Request



```http
POST https://api-service-r7ykp.ondigitalocean.app/v1/auth/login
Content-Type: application/json

{
  "username": "your_username",
  "password": "your_password"
}
```



#### Response

```json
POST https://api-service-r7ykp.ondigitalocean.app/v1/auth/login
Content-Type: application/json

{
  "username": "your_username",
  "password": "your_password"
}
```

Use this access token in all subsequent requests as part of the `Authorization` header.

***

### Important Notes

* **Rate Limits:** Be mindful of [API rate and usage limits](https://learning.postman.com/docs/developer/postman-api/postman-api-rate-limits/).

* **HTTPS Only:** The API only supports HTTPS. Any HTTP requests will automatically redirect to HTTPS with a `301` response.

* **JSON Responses:** All API responses are formatted as JSON. Errors are also returned in JSON format.

***

### Need Help?

* View the complete documentation for all endpoints and usage examples: [Cove API Documentation](https://www.postman.com/getcove/external/collection/6lv6roh/cove-api)

* Contact support: [concierge@getcove.co]()

Start building with the Cove API today!