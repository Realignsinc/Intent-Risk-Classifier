# Realigns AI – Intent & Risk Classifier

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![PHP](https://img.shields.io/badge/PHP-7.4%2B-blue.svg)

A lightweight, production-ready **AI decision gate** that classifies user input *before* any downstream AI generates a response.

This tool does **not** chat with users.  
It returns a **machine-readable decision signal** so your system can decide **what happens next**.

---

## 🔍 How It Works: Dual-Layer Decision Logic

### 1. SoR Layer (System of Record)
Deterministic rules using regex are evaluated first.

- ⚡ Instant classification for common intents (billing, crashes, refunds, etc.)
- 💰 Zero AI cost for obvious cases
- 🧱 Fully predictable behavior

### 2. Micro-AI Layer (Optional)
If no rule matches, input is sent to the **Realigns AI Gateway**.

- Understands complex phrasing
- Output is forced into a strict format:



intent: <category> | risk: <level> | action: <system_action>


---

## 🚀 Installation (Shared Hosting / cPanel)

### Option A: ZIP Upload (Recommended)

1. Download the ZIP from GitHub.
2. Upload it to:


public_html/realigns-ai/

3. Extract the ZIP **inside the same folder**.

✅ Final structure:


public_html/realigns-ai/
├── classify.php
├── config.php
├── rules.php
├── README.md


---

### Option B: Git (Advanced users only)

```bash
git clone https://github.com/realigns-ai/intent-risk-classifier.git
```
⚙️ Configuration

Edit config.php:
```
define('REALIGNS_API_KEY', 'your_key_here');
define('REALIGNS_API_URL', 'https://gpt-api.realignsinc.com/ai/chat');
```
📡 API Usage
Endpoint
```
POST /classify.php
```
Example Request

```
{
  "text": "I need help with a failed payment"
}
```
Example Response

```
{
  "result": "intent: billing | risk: low | action: allow"
}
```
# 🛡️ Hard Safety Enforcement

The classifier validates AI output against strict allow-lists.

Allowed Intents

billing

education

finance

support

general

Allowed Risks

low

medium

high

Allowed Actions

allow

caution

block

If the AI response is invalid or malformed, the system automatically falls back to:

intent: general | risk: medium | action: caution

## 🧰 Tech Stack

PHP 7.4+

cURL

JSON (stateless)

No database required

## 🧠 Why This Matters

Using LLMs without a gatekeeper leads to:

jailbreaks

unpredictable costs

unsafe automation

This tool ensures:

Deterministic behavior

Policy enforcement

Zero blind trust in AI output

## 📄 License

MIT License — free for commercial and personal use.
