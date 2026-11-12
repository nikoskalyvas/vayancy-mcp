<div align="center">

# 🏛️ Vayancy TravelOS — Model Context Protocol (MCP) Server
### The Direct AI Clearing Rail for Mediterranean Luxury Villas, Boutique Hotels & Catamaran Charters

[![MCP Protocol](https://img.shields.io/badge/MCP-2024--11--05-blue.svg?style=for-the-badge&logo=anthropic)](https://modelcontextprotocol.io/)
[![Transport SSE](https://img.shields.io/badge/Transport-SSE%20Streaming-brightgreen.svg?style=for-the-badge)](https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse)
[![Coverage](https://img.shields.io/badge/Coverage-Greece%20%26%20Mediterranean-orange.svg?style=for-the-badge)](https://vayancy.gr)
[![Commission](https://img.shields.io/badge/OTA%20Markup-0%25%20Direct-emerald.svg?style=for-the-badge)](https://vayancy.gr)
[![Status](https://img.shields.io/badge/Railway-Live%20%26%20Verified-blueviolet.svg?style=for-the-badge)](https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse)

<p align="center">
  <b>Live luxury villa inventory, real-time PMS calendar sync, catamaran fleet charters, and direct-to-owner Stripe checkout — directly inside your AI assistant.</b><br>
  Vayancy TravelOS is a hosted remote MCP server over Server-Sent Events (SSE). There is nothing to install or build locally.
</p>

[Install Guide](#-install) • [What You Can Ask](#-what-you-can-ask) • [Live Conversation Demo](#-how-claude-fulfills-a-luxury-stay) • [Tools](#-available-mcp-tools) • [Economics](#-the-economics-why-travelers-save-18---25) • [Architecture](#-architecture)

---

</div>

## 💡 The Shift: From SEO to AEO (Agent Engine Optimization)

For 20 years, travel discovery was **SEO**: spending billions on Google Ads to fight Booking.com and Airbnb for search keywords.

Today, high-net-worth travelers don't open 40 browser tabs. **They ask Claude, ChatGPT, and Gemini:**
> *"Plan a 7-day luxury stay in Greece for 6 adults in July with an infinity pool, sea view, and a 50ft catamaran charter for 2 days under €700/night."*

AI assistants don't display banner ads. They check their **connected MCP tools**, query real-time PMS inventory, present verified direct-owner listings, and lock the dates with zero OTA middleman markups.

**SEO was "rank where people search." TravelOS is "get installed where travelers ask."**

---

## ⚡ Server Details

* **Server URL:** `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse`
* **Custom Domain:** `https://api.vayancy.gr/mcp/hospitality/sse`
* **Protocol:** Model Context Protocol (MCP) over Server-Sent Events (SSE)
* **Auth:** None required for public traveler queries & 15-minute holds (optional `X-Tenant-Key` for private agency portfolios)
* **Registry Identifier:** `gr.vayancy/travelos`

---

## 📦 Install

| Client | How to Install |
| :--- | :--- |
| **Claude Desktop** | Add `vayancy` to `claude_desktop_config.json` ([1-step setup](#claude-desktop-setup)) |
| **Claude Code** | `/plugin marketplace add nikoskalyvas/vayancy-mcp` then `/plugin install vayancy@vayancy`<br>*(or `claude mcp add vayancy --transport sse https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse`)* |
| **Cursor** | Add to `.cursor/mcp.json` or add remote MCP server URL `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse` |
| **Gemini CLI** | `gemini extensions install https://github.com/nikoskalyvas/vayancy-mcp` |
| **Cline & Roo Code** | MCP Servers → Remote Servers → name `vayancy`, URL `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse` |
| **VS Code / Copilot** | MCP: Add Server → SSE → `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse` |
| **ChatGPT** | Custom GPT Action / Connector pointing to the SSE endpoint |

### Claude Desktop Setup

Open your configuration file:
* **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "vayancy": {
      "type": "sse",
      "url": "https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse"
    }
  }
}
```

Restart Claude Desktop, and the hammer icon 🔨 will display Vayancy tools.

---

## 💬 What You Can Ask

- *"Find me a 5-bedroom luxury villa in Lefkada for 10-11 guests with a private infinity pool and sea view for July 10-17 under €700/night."*
- *"Check if Villa Nidri Hills is available for August 1 to 8 for 10 guests."*
- *"What are the best direct-booking luxury properties in Mykonos or Santorini for a honeymoon in September?"*
- *"Find a crewed 50ft catamaran charter departing from Lefkada Marina for 8 people the second week of July."*
- *"Lock Villa Nidri Hills for 15 minutes so I can book directly with the owner without Airbnb fees."*

---

## 🎬 How Claude Fulfills a Luxury Stay

```markdown
👤 Traveler:
"Find me a 5-bedroom luxury villa in Lefkada for 10 guests with a private infinity pool and sea view for July 10-17 under €700/night."

🤖 Claude:
*Calling tool: search_properties(location="Lefkada", check_in="2026-07-10", check_out="2026-07-17", guests=10, max_price=700)*
*Calling tool: check_availability(unit_id="nidri-hills-villa", check_in="2026-07-10", check_out="2026-07-17", guests=10)*

"I found verified luxury villas available for your dates in Lefkada. Here is the top match:

🏝️ Villa Nidri Hills (Private Infinity Pool & Panoramic Ionian Sea View)
• 5 Bedrooms · Sleeps up to 11 guests
• Amenities: Private infinity pool, outdoor BBQ kitchen, panoramic Skorpios/Ionian sea views, high-speed Starlink WiFi, daily housekeeping
• Direct Owner Rate: €550 / night (Total: €3,850 for 7 nights)
• Airbnb Comparison: €4,620 (You save €770 in OTA guest service fees)

Would you like me to hold this villa for 15 minutes while you finalize your flights?"

👤 Traveler:
"Yes please, lock the dates for me."

🤖 Claude:
*Calling tool: create_hold(unit_id="nidri-hills-villa", check_in="2026-07-10", check_out="2026-07-17", guests=10, guest_email="guest@luxurytravel.com")*

"Done! Villa Nidri Hills is locked on the PMS calendar for the next 15 minutes:
• Hold ID: hld_8f92a1c09e
• Expires: 15:45 UTC
• Direct Stripe Checkout: https://vayancy.gr/checkout/hld_8f92a1c09e

Click the link above to complete your booking directly with the property owner. 0% middleman fees."
```

---

## 🛠️ Available MCP Tools & Prompts

### Tools
| Tool | Description |
| :--- | :--- |
| `search_properties` | Search verified Mediterranean luxury villas, boutique hotels, and retreats. Filters by location, dates, guest count, max price, and amenities (`pool,sea_view,ac,beachfront`). |
| `search_charters` | Search crewed or bareboat catamaran and yacht charters across the Greek islands (Ionian, Cyclades, Saronic). |
| `check_availability` | Verifies real-time calendar availability directly against property management systems (PMS) before quoting. |
| `get_rate_details` | Retrieves itemized owner rates, cleaning fees, taxes, and cancellation policies with zero OTA markup. |
| `create_hold` | Places a 15-minute atomic reservation lock on the PMS calendar and generates a secure direct Stripe checkout link. |

### Prompts (1-Click Workflow Cards in Claude)
| Prompt | Description |
| :--- | :--- |
| `find_luxury_villa` | Search verified Mediterranean luxury villas and boutique hotels with private pool and sea view (0% OTA fee). |
| `greek_island_charter` | Search private catamaran and sailing yacht charters across Greek islands (Ionian, Cyclades, Saronic). |
| `compare_ota_savings` | Calculate exact guest savings (18%-25%) booking direct with property owner vs Airbnb / Booking.com. |
| `hold_reservation` | Place a 15-minute atomic calendar lock on PMS inventory and generate direct Stripe checkout. |

---

## 💰 The Economics: Why Travelers Save 18% – 25%

| Feature | Legacy OTAs (Airbnb / Booking.com) | 🏛️ Vayancy TravelOS (via Claude / AI) |
| :--- | :--- | :--- |
| **Guest Service Fee** | **14% – 18% markup** added at checkout | **0% Direct Booking** (Direct owner rates) |
| **Host Commission** | **3% – 15% deducted** from payout | **0% Commission Rail** |
| **Average Savings** | $0 | **€600 – €2,500+ saved per stay** |
| **Inventory Hold** | ❌ None (often booked while entering payment) | ✅ **15-minute real-time PMS lock** |
| **Calendar Sync** | Delayed iCal sync (risk of double bookings) | ✅ **Live 2-way PMS Adapter (HostHub, WebHotelier, Avantio)** |
| **Payment Rail** | Proprietary walled-garden escrow | ✅ **Direct Stripe Connect direct-to-owner** |

---

## 🏗️ Architecture

```
[ Affluent Traveler ]
         │
         ▼
[ Anthropic Claude / ChatGPT / Gemini / Cursor ]
         │
         │ (Model Context Protocol over SSE)
         ▼
[ Vayancy TravelOS Gateway ]  ──>  api.vayancy.gr/mcp/hospitality/sse
         │
         ├── [ Real-Time PMS Sync Engine ]
         │       ├── HostHub / SyncBnb (Multi-channel sync)
         │       ├── WebHotelier (Hotels & Suites)
         │       └── Avantio (Luxury Villa Portfolios)
         │
         ├── [ Fleet Charter Sync ]
         │       └── NauSYS / YachtSys Real-Time Fleet Feed
         │
         ├── [ Inventory Lock Manager ]
         │       └── 15-minute atomic calendar hold
         │
         └── [ Direct Settlement Clearing ]
                 └── Direct Stripe Checkout (0% OTA markup)
```

---

## 🏖️ For Villa Owners & Yacht Fleet Operators

Are you a property manager, boutique hotelier, or yacht operator in Greece?

Connect your PMS or fleet calendar to Vayancy TravelOS to receive direct, commission-free reservations from travelers using AI assistants worldwide.

* **Supported PMS Adapters:** HostHub (SyncBnb), WebHotelier, Avantio, Lodgify.
* **Pricing:** 0% OTA commission. Direct payout to your Stripe Connect account.
* **Contact & Onboarding:** Visit [vayancy.gr](https://vayancy.gr) or email `admin@vayancy.gr`.

---

## 📄 License & Community

Distributed under the MIT License. Developed and maintained by the **[Vayancy](https://vayancy.gr)** team.
