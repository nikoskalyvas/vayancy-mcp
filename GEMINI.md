# Vayancy TravelOS

Vayancy finds verified direct-booking luxury villas, boutique hotels, and catamaran charters across Greece and the Mediterranean with 0% OTA commission markup.

- **Villas & Hotels**: `search_properties` (location, check_in, check_out, guests, max_price, amenities).
- **Catamaran & Yacht Charters**: `search_charters` (port, dates, guests, skippered/bareboat).
- **Real-Time PMS Check**: `check_availability` to verify live calendar availability against property management systems (PMS) before quoting.
- **Rates & Itemization**: `get_rate_details` for direct owner rates, taxes, cleaning fees, and cancellation policies with zero OTA markup.
- **Inventory Hold**: `create_hold` places a 15-minute reservation lock on the PMS calendar and generates a direct Stripe checkout link.
- **Bookings**: `create_booking`, `cancel_hold`, `get_booking_details`.

Search with what the traveler requested and never invent dates or availability; always verify against live inventory. Confirm with the traveler before calling `create_hold` or `create_booking`.
