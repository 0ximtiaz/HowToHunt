# HowToHunt

# 🧠 Bug Bounty Burp Deep Testing Playbook (Top-Tier Bugs with Full Demo)

This is a deep, practical, copy-follow guide to test high ROI bugs using Burp Suite.

🚀 CORE RULE
Same request + small change = vulnerability chance

# 🎯 MASTER DEMO TARGET
```jsx
GET /api/v1/orders?order_id=8472&user_id=221 HTTP/1.1
Host: target.com
Cookie: session=abc123
Authorization: Bearer token123
```
🥇 1. IDOR (OBJECT ACCESS)

🔧 Test
```jsx
order_id=8472 → 8473
```
📥 Vulnerable Response
```jsx
{
  "order_id": 8473,
  "user_id": 999,
  "item": "iPhone"
}
```
🚨 Result

Other user data visible → IDOR

🥈 2. USER MISMATCH (ADVANCED IDOR)

🔧 Test

order_id=8472&user_id=221
→
order_id=8472&user_id=999

📥 Vulnerable Response

{
  "order_id": 8472,
  "user_id": 999
}

🚨 Result

Backend trusts user input → Logic flaw + IDOR

🥉 3. ACCESS CONTROL

🔧 Test

Remove:

Cookie
Authorization

📥 Vulnerable Response

200 OK
order data returned

🚨 Result

No auth needed → Broken access control

🥇 4. HIDDEN PARAMETER (PRIV ESCALATION)

🔧 Test

&admin=true
&role=admin
&view=all

📥 Vulnerable Response

{
  "orders": "ALL USERS DATA"
}

🚨 Result

Hidden param unlock → Privilege escalation

🥈 5. METHOD ABUSE

🔧 Test

GET → POST

📥 Vulnerable Response

order deleted successfully

🚨 Result

Unauthorized method allowed → API misconfig

🥉 6. BUSINESS LOGIC BUG

🔧 Request

POST /api/pay
{
  "order_id": 8472,
  "amount": 1200
}

🔧 Test

amount = 1

📥 Vulnerable Response

payment successful

🚨 Result

Price manipulation → Business logic flaw

🧠 ADVANCED TEST BLOCK (MUST APPLY)

🔹 PARAM REMOVAL

/api/orders?order_id=8472

🔹 NULL TEST

order_id=null
order_id=0

🔹 DUPLICATE PARAM

order_id=8472&order_id=8473

🔹 TYPE CONFUSION

order_id="8472"
order_id=8472.0

🔹 HEADER TEST

X-Forwarded-For: 127.0.0.1
X-Original-URL: /admin

🧠 RESPONSE ANALYSIS (CRITICAL)

Check:

Data changed?

Different user data?

More data returned?

Auth bypass?

Response size change?

🔥 FULL PRO LOOP

1. Capture request
2. Send to repeater
3. Change ONE param
4. Send request
5. Compare response
6. Repeat

🧠 WHAT YOU ARE ATTACKING

Identity (user কে?)

Authorization (allowed?)

Logic (flow correct?)

⚡ HIGH ROI BUG FOCUS

Only care about:

IDOR

Access control

Business logic

Auth issues

🧠 FINAL TRUTH

Burp = experiment lab
You = decision engine

🚀 PRACTICE RULE

1 request → 10 tests

30 requests → strong skill

Repeat daily

Happy Hunting 🔥


