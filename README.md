# RetailerHub-API
API Specifications

## Order Ingestion API

**Base URL**  
https://api.retailerhub.ai/api

**Authentication**  
All requests must include this header:  
`X-Api-Key`: API key provided by RetailerHub

---

## Endpoints

### POST /v1/order

**Description**  
Ingest a new order by submitting any valid JSON payload. Stores the payload and triggers asynchronous order-creation workflows.

**Request**  
- **URL:** `POST /v1/order`  
- **Headers:**  
  - `X-Api-Key`: Your organization’s API key  

**Example**  
```json
{
  "orderId": "12345",
  "items": [
    { "sku": "ABC", "qty": 2 }
  ],
  "customer": { "name": "John Doe" }
}
```

**Response**  
- **Status Code:** `202 Accepted`  
- **Body:** Acknowledges receipt of the order for processing.

---

### PUT /v1/{id}/order

**Description**  
Replace an existing order with a new full JSON object. Overwrites the entire existing object (no schema validation).

**Request**  
- **URL:** `PUT /v1/{id}/order`  
- **Headers:**  
  - `X-Api-Key`: Your organization’s API key  
- **Body:** Full JSON object (no schema restrictions)

**Example**  
```json
{
  "orderId": "12345",
  "items": [
    { "sku": "XYZ", "qty": 1 }
  ],
  "customer": { "name": "Jane Smith" }
}
```

**Response**  
- **Status Code:** `202 Accepted`  
- **Body:** Confirms receipt of the new order data and replacement of the original.

---

## Notes
- Maximum payload size: 3 MB  
- Orders are processed asynchronously  
- Keep your API key secure and never share it publicly
