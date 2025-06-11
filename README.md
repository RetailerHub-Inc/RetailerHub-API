# RetailerHub-API
API specifications

📦 Order Ingestion API

This API allows retailers to submit order data to RetailerHub. Both POST and PUT endpoints support arbitrary JSON payloads. RetailerHub will map the incoming data to internal formats using custom mappers — no predefined schema is required.

🌐 Base URL

https://api.retailerhub.ai/api


⸻

🔐 Authentication

All requests must include the following header:

Header	Description
X-Api-Key	API key provided by RetailerHub


⸻

📤 POST /v1/order

Description

Ingest a new order by submitting any valid JSON payload. This endpoint stores the payload and triggers asynchronous order creation workflows.

Endpoint

POST /v1/order

Request
	•	Body: Any JSON payload (no enforced schema)
	•	Headers:
	•	X-Api-Key: Your organization’s API key

Example

{
  "orderId": "12345",
  "items": [
    { "sku": "ABC", "qty": 2 }
  ],
  "customer": {
    "name": "John Doe"
  }
}

Response
	•	Status Code: 202 Accepted
	•	Acknowledges receipt of the order for processing.

⸻

🔁 PUT /v1/id/order

Description

Replace an existing order with a new full JSON object. This will overwrite the entire existing object. No schema validation is applied; your payload is passed through as-is.

Endpoint

PUT /v1/id/order

Request
	•	Body: Full JSON object (no schema restrictions)
	•	Headers:
	•	X-Api-Key: Your organization’s API key

Example

{
  "orderId": "12345",
  "items": [
    { "sku": "XYZ", "qty": 1 }
  ],
  "customer": {
    "name": "Jane Smith"
  }
}

Response
	•	Status Code: 202 Accepted
	•	Confirms that the new order data has been received and will replace the original.

⸻

🛡 Notes
	•	Maximum payload size: 10 MB
	•	Orders are processed asynchronously
	•	Your API key must be kept secure and never shared publicly

⸻
