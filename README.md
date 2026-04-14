# HowToHunt

# 🎯 TARGET URL (DEMO)

ধরো তুমি Burp-এ এটা ধরছো:
```jsx
GET /api/v1/orders?order_id=8472&user_id=221 HTTP/1.1
Host: app.target.com
Cookie: session=abc123
Authorization: Bearer eyJhbGci...

```
👉 এই 1টা endpoint দিয়েই আমরা multiple high ROI bug খুঁজবো।

# 🧠 STEP 1: BASELINE UNDERSTAND

👉 normal request send করো (Repeater)
📥 Response:
```jsx
200 OK
{
  "order_id": 8472,
  "user_id": 221,
  "item": "Laptop",
  "price": 1200
}

```
✔ এখন বুঝলাম:

*order data আসছে
*user-specific
