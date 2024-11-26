---
title: "Quickstart"
description: "Welcome to the Cove API Quickstart! This guide provides a detailed walkthrough of how to use the API, from setting up your account to conducting applicant screenings."
---

# Cove API Quickstart

## Introduction

The Cove API enables efficient management of rental properties. This guide provides a detailed walkthrough of how to use the API, from setting up your account to conducting applicant screenings.

## Base URL

```md
https://api-service-r7ykp.ondigitalocean.app
```

## Detailed Workflow

### Step 1: Request Login Credentials

To begin using the Cove API, you need login credentials. Send an email to [concierge@getcove.co](mailto:concierge@getcove.co) requesting access to your account and the dashboard.
Once you receive your credentials, you can authenticate and start making API calls.

---

### Step 2: Authenticate

Before accessing other endpoints, you must authenticate using the `/v1/auth/login` endpoint to obtain an access token.

#### Endpoint

```md
POST /v1/auth/login
```

#### Description

This endpoint validates your username and password. If successful, it returns an `accessToken` that you must include in all subsequent API calls.

#### Request Headers

- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### Request Body

```json
{
  "username": "<string>",
  "password": "<string>"
}
```

#### Example

```sh
curl -X POST https://api-service-r7ykp.ondigitalocean.app/v1/auth/login \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d '{
  "username": "your-username",
  "password": "your-password"
}'
```

- **Success (200)**:

  ```json
  {
    "accessToken": "<string>"
  }
  ```

- **Error (401)**: Unauthorized.

#### Usage of Token

Include the `accessToken` in the `Authorization` header for all subsequent requests:

```md
Authorization: <accessToken>
```

---

### Step 3: Create a Property

Before conducting a soft credit check for an applicant, you must create a property record using the `/v1/property` endpoint. This step establishes the property context for the screening process.

#### Endpoint

```md
POST /v1/property
```

#### Description

Creates a new property record in the system.

#### Headers

- `Authorization`: `<API Key>`
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### Request Body

```json
{
  "name": "<string>",
  "rent": "<integer>",
  "address": {
    "street": "<string>",
    "city": "<string>",
    "provinceState": "<string>",
    "country": "<string>",
    "postalCode": "<string>",
    "fullAddress": "<string>"
  }
}
```

#### Example

```sh
curl -X POST https://api-service-r7ykp.ondigitalocean.app/v1/property \
-H "Authorization: your-access-token" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d '{
  "name": "Sample Property",
  "rent": 1500,
  "address": {
    "street": "123 Main St",
    "city": "Sample City",
    "provinceState": "Sample State",
    "country": "Sample Country",
    "postalCode": "12345",
    "fullAddress": "123 Main St, Sample City, Sample State, Sample Country, 12345"
  }
}'
```

- **Success (200)**:

  ```json
  {
    "propertyId": "<string>"
  }
  ```

#### Notes

- The `propertyId` from this response is required for the next step.

---

### Step 4: Send Screening Link

Once the property is created, you can initiate a screening process by sending a link to the applicant. Use the `/v1/screening/send` endpoint for this.

#### Endpoint

```
POST /v1/screening/send
```

#### Description

Generates and sends a screening link to the applicant, enabling them to complete the screening process.

#### Headers

- `Authorization`: `<API Key>`
- `Content-Type`: `application/json`
- `Accept`: `application/json`

#### Request Body

```json
{
  "checkType": "CHECK_TYPE_DEEP_CHECK",
  "email": "<string>",
  "phone": "<string>",
  "firstName": "<string>",
  "lastName": "<string>",
  "propertyId": "<string>",
  "payer": "PAYER_SELF"
}
```

#### Example

```sh
curl -X POST https://api-service-r7ykp.ondigitalocean.app/v1/screening/send \
-H "Authorization: your-access-token" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d '{
  "checkType": "CHECK_TYPE_DEEP_CHECK",
  "email": "applicant@example.com",
  "phone": "+14160001111",
  "firstName": "John",
  "lastName": "Doe",
  "propertyId": "property-id-from-previous-step",
  "payer": "PAYER_SELF"
}'
```

- **Success (200)**:

  ```json
  {
    "userId": "<string>",
    "message": "<string>"
  }
  ```

#### Notes

- Provide accurate applicant information to ensure the screening link reaches the right individual.
- The `userId` from this response will be required for retrieving the screening results.

---

### Step 5: Retrieve Screening Data

Once the applicant completes the screening, you can fetch their results using the `/v1/screening/data/:userId` endpoint.

#### Endpoint

```
GET /v1/screening/data/:userId
```

#### Description

Retrieves detailed screening results for a specific applicant.

#### Headers

- `Authorization`: `<API Key>`
- `Accept`: `application/json`

#### URL Parameters

- `userId`: (Required) Unique identifier for the applicant.

#### Example

```sh
curl -X GET https://api-service-r7ykp.ondigitalocean.app/v1/screening/data/<userId> \
-H "Authorization: your-access-token" \
-H "Accept: application/json"
```

- **Success (200)**:

  ```json
  {
    "screening": { ... },
    "user": { ... }
  }
  ```

#### Notes

- Use this endpoint to evaluate the applicant’s suitability based on their screening data.

---

## Additional Information

- All endpoints require HTTPS communication.
- Errors are returned in JSON format with appropriate HTTP status codes.
- For detailed documentation, visit the [Cove API Docs](https://getcove.co/api).

---

## Need Help?

For further assistance, contact [concierge@getcove.co](mailto:concierge@getcove.co).
