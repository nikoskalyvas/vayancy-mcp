<div align="center">

# 🏛️ Vayancy TravelOS — Model Context Protocol (MCP) Server
### The Direct AI Clearing Rail for Mediterranean Luxury Villas & Boutique Retreats

[![MCP Protocol](https://img.shields.io/badge/MCP-2024--11--05-blue.svg?style=for-the-badge&logo=anthropic)](https://modelcontextprotocol.io/)
[![Transport SSE](https://img.shields.io/badge/Transport-SSE%20Streaming-brightgreen.svg?style=for-the-badge)](https://api.vayancy.gr/mcp/hospitality/sse)
[![Inventory](https://img.shields.io/badge/Coverage-Greece%20%26%20Mediterranean-orange.svg?style=for-the-badge)](https://vayancy.gr)
[![Commission](https://img.shields.io/badge/OTA%20Markup-0%25%20Direct-emerald.svg?style=for-the-badge)](https://vayancy.gr)
[![Status](https://img.shields.io/badge/Railway-Live%20%26%20Verified-blueviolet.svg?style=for-the-badge)](https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse)

<p align="center">
  <b>Connect Claude, Cursor, and Windsurf directly to real-time Mediterranean property management systems (PMS).</b><br>
  Search verified private villas, verify live calendars, lock 15-minute reservation holds, and fulfill stays with direct Stripe checkout.
</p>

[Quick Start](#-10-second-quick-start-claude-desktop) • [Live Conversation Demo](#-how-claude-fulfills-a-luxury-stay) • [Economic Comparison](#-the-economics-why-travelers-save-18-25) • [Available Tools](#-available-mcp-tools) • [Architecture](#-architecture)

---

</div>

## 💡 The Shift: From SEO to AEO (Agent Engine Optimization)

For 20 years, travel discovery was **SEO**: spending millions on Google Ads to fight Booking.com and Airbnb for search keywords.

Today, high-net-worth travelers don't open 40 browser tabs. **They ask Claude:**
> *"Plan a 7-day luxury stay in Greece for 6 adults in July with an infinity pool, sea view, and private chef under €600/night."*

Claude doesn't show Google banner ads. It checks its **connected MCP tools**, queries real-time PMS inventory, presents verified villas directly in the chat, and locks the dates with zero OTA middleman markups.

**SEO was "rank where people search." TravelOS is "get installed where travelers ask."**

---

## ⚡ 10-Second Quick Start (Claude Desktop)

Add Vayancy TravelOS to your Claude Desktop configuration in one step:

* **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "vayancy-travelos": {
      "url": "https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse"
    }
  }
}
```

> **Custom Domain:** You can also connect via `https://api.vayancy.gr/mcp/hospitality/sse` once custom DNS propagation is complete.

---

## 💬 How Claude Fulfills a Luxury Stay

Here is the exact real-time interaction when Claude has Vayancy TravelOS connected:

```markdown
👤 Traveler:
"Find me a 4-bedroom luxury villa in Lefkada with a private infinity pool and sea view for July 10-17 under €600/night."

🤖 Claude:
*Calling tool: search_properties(location="Lefkada", check_in="2026-07-10", check_out="2026-07-17", guests=6, max_price=600)*
*Calling tool: check_availability(unit_id="nidri-hills-villa-1", check_in="2026-07-10", check_out="2026-07-17", guests=6)*

"I found 3 verified luxury villas available for your dates in Lefkada. Here is the top match:

🏝️ Villa Nidri Hills (Private Infinity Pool & Panoramic Ionian Sea View)
• 4 Bedrooms · 4 En-suite Bathrooms · Sleeps 8
• Private infinity pool, outdoor BBQ kitchen, high-speed Starlink WiFi, daily housekeeping
• Direct Owner Rate: €450 / night (Total: €3,150 for 7 nights)
• Airbnb Comparison: €3,780 (You save €630 in OTA guest service fees)

Would you like me to hold this villa for 15 minutes while you finalize your flights?"

👤 Traveler:
"Yes please, lock the dates for me."

🤖 Claude:
*Calling tool: create_hold(unit_id="nidri-hills-villa-1", check_in="2026-07-10", check_out="2026-07-17", guests=6, guest_email="guest@luxurytravel.com")*

"Done! Villa Nidri Hills is locked on the PMS calendar for the next 15 minutes:
• Hold ID: hld_8f92a1c09e
• Expires: 15:45 UTC
• Direct Stripe Checkout: https://vayancy.gr/checkout/hld_8f92a1c09e

Click the link above to complete your booking directly with the property owner. 0% middleman fees."
```

---

## 💰 The Economics: Why Travelers Save 18% – 25%

| Feature | Legacy OTAs (Airbnb / Booking.com) | 🏛️ Vayancy TravelOS (via Claude) |
| :--- | :--- | :--- |
| **Guest Service Fee** | **14% – 18% markup** added at checkout | **0% Direct Booking** (Direct owner rates) |
| **Host Commission** | **3% – 15% deducted** from payout | **0% Commission Rail** |
| **Average Savings** | \$0 | **€600 – €2,500+ saved per stay** |
| **Inventory Hold** | ❌ None (often booked while entering credit card) | ✅ **15-minute real-time PMS lock** |
| **Calendar Sync** | Delayed iCal sync (frequent double bookings) | ✅ **Live 2-way PMS Adapter (WebHotelier, Avantio, HostHub)** |
| **Payment Rail** | Proprietary walled-garden escrow | ✅ **Direct Stripe Connect direct-to-owner** |

---

## 🛠️ Available MCP Tools

### 1. `search_properties`
Queries verified Mediterranean direct-booking inventory filtered by location, dates, guest count, price, and luxury amenities.
```json
{
  "location": "Lefkada",
  "check_in": "2026-07-10",
  "check_out": "2026-07-17",
  "guests": 6,
  "max_price": 600,
  "amenities": "pool,sea_view,ac,beachfront,wifi"
}
```

### 2. `check_availability`
Checks real-time calendar availability for a specific accommodation against property management systems before quoting.
```json
{
  "unit_id": "nidri-hills-villa-1",
  "check_in": "2026-07-10",
  "check_out": "2026-07-17",
  "guests": 6
}
```

### 3. `get_rate_details`
Retrieves itemized direct-booking rates, taxes, cleaning fees, and cancellation policies with zero OTA markup.
```json
{
  "unit_id": "nidri-hills-villa-1",
  "check_in": "2026-07-10",
  "check_out": "2026-07-17",
  "guests": 6
}
```

### 4. `create_hold`
Places a 15-minute reservation lock on the property calendar and returns a secure, direct checkout URL.
```json
{
  "unit_id": "nidri-hills-villa-1",
  "check_in": "2026-07-10",
  "check_out": "2026-07-17",
  "guests": 6,
  "guest_email": "traveler@vayancy.gr"
}
```
**Returns:**
```json
{
  "success": true,
  "hold_id": "hld_4a9b8c2d",
  "expires_at": "2026-07-10T14:30:00Z",
  "checkout_url": "https://vayancy.gr/checkout/hld_4a9b8c2d"
}
```

---

## 🏗️ Architecture

```
[ Affluent Traveler ]
         │
         ▼
[ Anthropic Claude / AI Agent ]
         │
         │ (Model Context Protocol over SSE)
         ▼
[ Vayancy TravelOS Gateway ]  ──>  api.vayancy.gr/mcp/hospitality/sse
         │
         ├── [ Real-Time PMS Sync Engine ]
         │       ├── WebHotelier (Hotels & Suites)
         │       ├── Avantio (Luxury Villa Portfolios)
         │       └── HostHub / SyncBnb (Multi-channel sync)
         │
         ├── [ Inventory Lock Manager ]
         │       └── 15-minute atomic calendar hold
         │
         └── [ Direct Settlement Clearing ]
                 └── Direct Stripe Checkout (0% OTA markup)
```

---

## 🏖️ For Greek Villa Owners & Boutique Hotel Operators

Are you a property manager, boutique hotelier, or luxury villa owner in Greece?

Connect your PMS to Vayancy TravelOS to receive direct, commission-free reservations from travelers using Claude.

* **Supported PMS Adapters:** WebHotelier, Avantio, HostHub (SyncBnb), Lodgify.
* **Pricing:** 0% OTA commission. Direct payout to your Stripe Connect account.
* **Contact & Onboarding:** Visit [vayancy.gr](https://vayancy.gr) or contact `admin@vayancy.gr`.

---

## 🔒 Security & Privacy

* **Zero Authentication Required for Travelers:** All traveler search, availability, rate quote, and hold creation tools operate publicly over standard HTTPS/SSE.
* **No PII Stored by Claude:** Guest contact email is used solely to associate the 15-minute hold with the guest on Stripe Checkout.
* **Optional Agency Header:** Property management firms and multi-property operators can pass `X-Tenant-Key` to scope queries exclusively to their private managed portfolio.

---

## 📄 License & Community

Distributed under the MIT License. Developed and maintained by the **[Vayancy](https://vayancy.gr)** team.
