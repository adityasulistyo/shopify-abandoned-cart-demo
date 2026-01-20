# Smart Abandoned Cart Recovery System (COD Optimized)
<img width="1440" height="900" alt="Screenshot 2026-01-20 at 17 56 01" src="https://github.com/user-attachments/assets/78366b3e-0869-423e-838b-71661d4ff143" />

[![Live Demo](https://img.shields.io/badge/🔴_Live_Demo-Click_Here-red?style=for-the-badge&logo=github)](https://adityasulistyo.github.io/shopify-abandoned-cart-demo/) 
[![Tech Stack](https://img.shields.io/badge/Tech-JavaScript_ES6_%7C_Webflow_%7C_Shopify_API-blue?style=for-the-badge)](https://github.com/adityasulistyo)

> **A "Headless" middleware solution to capture partial leads from Webflow landing pages and sync them to Shopify Draft Orders in real-time.**

---

## Overview

In high-volume Cash on Delivery (COD) markets, **60-70% of users drop off** after filling in their details but before clicking "Submit". Standard forms lose this data forever.

This project implements a **Heuristic Abandoned Cart Listener** that detects user intent. It captures typed data (Name/Phone) immediately when a user stops interacting with the form, ensuring the sales team can follow up via WhatsApp even if the order wasn't completed.

### 🔴 Try the Live Simulation
**[View Live Demo](https://adityasulistyo.github.io/shopify-abandoned-cart-demo/)**
*(Instruction: Type your name, then wait 3 seconds to trigger the detection logic)*


---

## How It Works (The Logic)

The system does not rely on the standard `submit` event. Instead, it uses a **debounce algorithm** to monitor user activity.

1.  **Event Listener:** Watches for keystrokes in specific fields (Name, WhatsApp).
2.  **Debounce Timer:** Every keystroke resets a timer (set to 30s in prod, 3s in demo).
3.  **Trigger:** If the timer runs out (user is idle/hesitant), the system flags it as an "Abandoned Cart".
4.  **Action:** The partial data is securely pushed to a Webhook (connected to Shopify/CRM).

```javascript
// Core Logic Snippet
let timer;
const IDLE_TIMEOUT = 30000; // 30 Seconds

input.addEventListener('input', () => {
    // Reset timer while user is typing
    clearTimeout(timer);
    
    // If user stops typing for 30s, assume abandonment and capture data
    timer = setTimeout(syncToShopifyDraftOrder, IDLE_TIMEOUT);
});

---

## Architecture

This solution is designed for **Headless Commerce** setups (e.g., Webflow Front-end + Shopify Back-end).

```mermaid
graph LR
    A[User Types Data] --> B{Idle for 30s?};
    B -- Yes --> C[Frontend Script];
    C -->|Secure Payload| D[Webhook (Make/Zapier)];
    D -->|Admin API| E[Shopify Draft Order];
    E --> F[WhatsApp Team Follow-up]

* **Security First:** No API Keys are exposed on the client side. The frontend only talks to a secure webhook endpoint.
* **Performance:** Lightweight Vanilla JS (No jQuery dependencies).
* **UX:** Non-intrusive. The user doesn't know the data is being saved in the background.

---

## Key Features

* ✅ **Real-time Detection:** Captures data *before* submission.
* ✅ **Visual Feedback:** (Demo Mode) UI indicators for "Typing", "Waiting", and "Abandoned".
* ✅ **Validation:** Ensures empty data isn't sent to the server to save API calls.
* ✅ **Conversion Focused:** Designed specifically for single-page COD landing pages.

---

## Tech Stack

* **Frontend:** HTML5, CSS3 (Glassmorphism UI), Vanilla JavaScript.
* **Simulation:** The live demo simulates the backend response for testing purposes.
* **Intended Backend:** Node.js / Make.com Webhooks integrated with Shopify Admin API.

---

### Author

**Aditya Sulistyo**
*Expert in Web Development & Automation Integration*

[Open for Hire] | [View Portfolio](https://www.google.com/url?sa=E&source=gmail&q=https://github.com/adityasulistyo)
