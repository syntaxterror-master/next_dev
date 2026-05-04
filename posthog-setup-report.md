<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvent Next.js App Router project. Here is a summary of all changes made:

- **`instrumentation-client.ts`** (created) — Initializes PostHog on the client side using the Next.js 15.3+ `instrumentation-client` convention. Configured with the EU host via a reverse proxy (`/ingest`), automatic exception capture for error tracking, and debug mode in development.
- **`next.config.ts`** (updated) — Added reverse proxy rewrites routing `/ingest/*` to the EU PostHog endpoints (`eu.i.posthog.com` and `eu-assets.i.posthog.com`), plus `skipTrailingSlashRedirect: true` required for PostHog API compatibility.
- **`.env.local`** (created) — Added `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables. Covered by `.gitignore`.
- **`components/ExploreBtn.tsx`** (updated) — Added `explore_events_clicked` capture in the existing click handler when a user clicks the "Explore Events" CTA.
- **`components/EventCard.tsx`** (updated) — Converted to a client component and added `event_card_clicked` capture with rich properties (`event_title`, `event_slug`, `event_location`, `event_date`) when a user clicks through to an event detail page.
- **`components/Navbar.tsx`** (updated) — Converted to a client component and added `nav_create_event_clicked` capture on the "Create Event" navigation link.

## Events

| Event name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicked the "Explore Events" CTA button on the homepage | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicked an event card to view its detail page (top of conversion funnel) | `components/EventCard.tsx` |
| `nav_create_event_clicked` | User clicked "Create Event" in the navbar — signals organizer intent | `components/Navbar.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics:** https://eu.posthog.com/project/171008/dashboard/656690
- **Event engagement over time** (line chart of all three events): https://eu.posthog.com/project/171008/insights/o7QxGwu3
- **CTA to event detail conversion funnel** (explore → card click): https://eu.posthog.com/project/171008/insights/w5phSzQG
- **Most clicked events by title** (bar chart breakdown): https://eu.posthog.com/project/171008/insights/r3Mg5xyt
- **Event clicks by location** (bar chart breakdown): https://eu.posthog.com/project/171008/insights/Wnm4BJip
- **Create Event intent (weekly)** (area chart, unique users): https://eu.posthog.com/project/171008/insights/jpyqVzcc

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
