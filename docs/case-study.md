# Airfare Price Monitoring Dashboard

**Turning “did the price drop yet?” into an automated yes or no.**

## The problem

Booking a multi-city trip means tracking several flight legs and airlines at once. Without a single view across the itinerary, manual checks become repetitive and it is easy to miss a useful price drop.

The project started with a real five-leg Egypt itinerary:

`Berlin → Hurghada → Cairo → Luxor → Berlin`

## The approach

The dashboard separates the data layer from the decision layer:

1. **Trips** stores one row per itinerary and assigns a reusable Trip ID.
2. **Price tracker** stores one row per route leg and compares the latest and previous price.
3. **Apps Script and the flight-price API** fetch and update prices.
4. **Price History** stores each snapshot against its Trip ID.
5. **Dashboard** turns the latest state into KPIs, route-level recommendations and a price comparison chart.

The output is deliberately decision-oriented. A meaningful drop becomes `BOOK`, a stable price becomes `MONITOR`, and an increase remains visible as a route that needs attention.

## Reusability

The project is not tied to one itinerary. Adding another trip means creating a new Trip ID and adding the matching route rows. The existing tracker, history log and dashboard can then filter to that itinerary without being rebuilt.

## Current status

The flight-price API is implemented and connected. Manual refresh is available. The scheduled trigger is currently paused, so the current workflow is transparent about what runs on demand and what is not running continuously.

## What I would build next

- A sustainable scheduled refresh cadence
- Email or Slack alerts for configurable price-drop thresholds
- A “book by” estimate using route-level price volatility
- Trip-level filtering across every workbook tab
