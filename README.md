# Vayancy TravelOS — Model Context Protocol (MCP) Server

[![MCP Protocol](https://img.shields.io/badge/MCP-2024--11--05-blue.svg)](https://modelcontextprotocol.io/)
[![Transport](https://img.shields.io/badge/Transport-SSE-success.svg)](https://api.vayancy.gr/mcp/hospitality/sse)
[![Coverage](https://img.shields.io/badge/Inventory-Greece%20%26%20Mediterranean-orange.svg)](https://vayancy.gr)
[![Zero Markup](https://img.shields.io/badge/OTA%20Markup-0%25%20Direct-green.svg)](https://vayancy.gr)
[![License](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

**Vayancy TravelOS** is the real-time Model Context Protocol (MCP) clearing rail connecting AI assistants directly to verified luxury villas, boutique hotels, and beachfront retreats across Greece and the Mediterranean.

Exposed over **Server-Sent Events (SSE)**, this server gives agents like Anthropic Claude, Cursor, and Windsurf native capabilities to search live inventory, verify real-time PMS calendars, quote direct rates, and lock 15-minute booking holds with instant Stripe checkout.

---

## ⚡ Quick Start: Claude Desktop

Add this to your Claude Desktop configuration file:

* **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
* **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "vayancy-travelos": {
      "url": "https://api.vayancy.gr/mcp/hospitality/sse"
    }
  }
}
```

> **Fallback / Development URL:** If `api.vayancy.gr` DNS is propagating, you can also connect directly via `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse`.

---

## 🛠️ Available MCP Tools

### 1. `search_properties`
Query verified Mediterranean direct-booking inventory filtered by location, dates, guest count, price, and amenities.
* **`location`** *(string, required)*: Island or region (e.g., `Mykonos`, `Santorini`, `Lefkada`, `Crete`, `Athens Riviera`, `Paros`, `Corfu`, `Rhodes`).
* **`check_in`** *(string, required)*: Check-in date in `YYYY-MM-DD` format.
* **`check_out`** *(string, required)*: Check-out date in `YYYY-MM-DD` format.
* **`guests`** *(integer, required)*: Total guest count.
* **`max_price`** *(number, optional)*: Maximum nightly budget in EUR.
* **`amenities`** *(string, optional)*: Comma-separated amenities (e.g. `pool,sea_view,ac,beachfront,wifi,chef,jacuzzi`).

### 2. `check_availability`
Check real-time calendar availability for a specific accommodation against property management systems.
* **`unit_id`** *(string, required)*: Accommodation identifier (e.g., `nidri-hills-villa-1`).
* **`check_in`** *(string, required)*: `YYYY-MM-DD`.
* **`check_out`** *(string, required)*: `YYYY-MM-DD`.
* **`guests`** *(integer, required)*: Guest count.

### 3. `get_rate_details`
Retrieve itemized direct-booking rates, taxes, cleaning fees, and cancellation policies with zero OTA markup.
* **`unit_id`** *(string, required)*: Accommodation identifier.
* **`check_in`** *(string, required)*: `YYYY-MM-DD`.
* **`check_out`** *(string, required)*: `YYYY-MM-DD`.
* **`guests`** *(integer, required)*: Guest count.

### 4. `create_hold`
Places a 15-minute reservation lock on the property calendar and returns a secure, direct checkout URL.
* **`unit_id`** *(string, required)*: Accommodation identifier.
* **`check_in`** *(string, required)*: `YYYY-MM-DD`.
* **`check_out`** *(string, required)*: `YYYY-MM-DD`.
* **`guests`** *(integer, required)*: Guest count.
* **`guest_email`** *(string, required)*: Primary guest contact email.
* **Returns:** `hold_id`, `expires_at`, and `checkout_url` (`https://vayancy.gr/checkout/{hold_id}`).

---

## 🔄 End-to-End Traveler Flow

```
[ Traveler ] ──( "Find 4-bedroom villa in Mykonos July 10-17" )──> [ Claude ]
                                                                      │
                                                      search_properties(...)
                                                                      │
                                                                      ▼
                                                         [ Vayancy TravelOS ]
                                                         (api.vayancy.gr/sse)
                                                                      │
                                             Parallel PMS Availability Engine
                                           (WebHotelier / Avantio / HostHub)
                                                                      │
[ Traveler ] <──( Presents 3 verified villas with live EUR rates )── [ Claude ]
     │
     └──( "Hold Villa Celina and book it" )────────────────────────> [ Claude ]
                                                                      │
                                                        create_hold(...)
                                                                      │
                                                                      ▼
                                                         [ Vayancy TravelOS ]
                                                         - Locks unit for 15m
                                                         - Returns Stripe link
                                                                      │
[ Traveler ] <──( "Here is your direct booking link: vayancy.gr/checkout/..." )
     │
     └──( Pays direct on Stripe Checkout )
            │
            ▼
     [ Stripe Webhook ] ──> [ Vayancy Settlement Engine ]
                                ├── Confirms booking in PMS
                                └── Direct payout to Owner
```

---

## 🔒 Security & Privacy

* **Zero Authentication Required for Travelers:** All traveler search, availability, rate quote, and hold creation tools operate publicly over standard HTTPS/SSE.
* **No PII Stored by Claude:** Guest contact email is used solely to associate the 15-minute hold with the guest on Stripe Checkout.
* **Optional Agency Header:** Property management firms and multi-property operators can pass `X-Tenant-Key` to scope queries exclusively to their private managed portfolio.

---

## 🌐 Endpoints

| Environment | Transport | SSE Endpoint | Messages Endpoint |
| :--- | :--- | :--- | :--- |
| **Production** | SSE | `https://api.vayancy.gr/mcp/hospitality/sse` | `https://api.vayancy.gr/mcp/hospitality/messages/` |
| **Failover / Edge** | SSE | `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/sse` | `https://vayancy-agentic-brain-production.up.railway.app/mcp/hospitality/messages/` |

---

## 📄 License

MIT License. Developed and maintained by [Vayancy](https://vayancy.gr).
