# Handoff: Assemble PWA — User App & Admin Panel

## Overview
**Assemble** is an AI fashion assistant PWA. Users photograph clothing items, build a digital closet, and get AI-generated outfit suggestions matched to occasion, budget, and personal style. Missing items are filled via affiliate-linked partner-store products. Monetization: credits (1 credit = 1 outfit generation), credit packs, subscriptions (Free / Plus / Pro), ads for free users, and featured/promoted placements. The product has **two interfaces**: a consumer-facing user app and a single-login admin panel for the platform owner.

This handoff contains two fully clickable greyscale prototypes covering every screen, action, modal, and flow described in the project proposal.

## About the Design Files
The files in this bundle are **design references created in HTML** — interactive prototypes showing intended structure, flow, and behavior. They are **not production code to copy directly**. The task is to **recreate these designs in the target codebase's environment** (e.g. React/Next.js, Vue, or whatever the team chooses for the PWA) using its established patterns and libraries. If no codebase exists yet, choose an appropriate PWA stack (e.g. React + service worker + installable manifest) and implement the designs there.

The prototypes are `.dc.html` design-component files. Each contains:
- an HTML **template** (inside `<x-dc>`) — all markup with inline styles; every screen is a `<sc-if>` block with a `data-screen-label` attribute naming it
- a **logic class** (`class Component`) — navigation state machine, modal state, chip/toggle/radio state, and action handlers

Read the template for layout/styling and the logic class for behavior/state.

## Fidelity
**Mid-to-high fidelity, greyscale wireframes.** Layout, spacing, hierarchy, copy, flows, and interactions are intentional and should be followed closely. Colors are deliberately monochrome (near-black `#1c1c1e`, greys, white) — final brand colors/typography are NOT decided; apply the eventual brand system on top. Image areas are grey-gradient placeholders awaiting real photography/renders.

## Files
- `User App Prototype.dc.html` — consumer app (32 screens + 19 modals/sheets)
- `Admin Prototype.dc.html` — admin panel (3 auth screens + 11 sections + 14 modals)

Both are responsive: resize to see mobile (bottom tab bar / hamburger drawer) vs desktop (side rail / dark sidebar) at a 900px / 880px breakpoint respectively.

## Screens / Views — User App

Navigation model: mobile = 5-item bottom tab bar (Home, Closet, center "Match" FAB-style button, Saved, Profile); desktop (≥900px) = left rail with the same destinations plus Shop and a credits card. Auth/onboarding screens hide all chrome. Content columns are centered, max-width 560px (forms) or 720px (grids).

### Auth & onboarding
- **Welcome** — hero placeholder, tagline "Dress right, every time", Create account / Log in buttons, Google & Apple social buttons (social auth skips to style profile), terms notice.
- **Sign up** — name, email, optional phone, password (with rule hints), terms checkbox → Verify.
- **Verify email** — 6 single-digit code inputs, resend timer, switch-to-phone link → Style profile.
- **Log in** — email/password, forgot-password link, social buttons → Home.
- **Forgot / Reset password** — email entry → new password + repeat with validation checklist → back to Log in.
- **Style profile (3 steps, progress bar)** — 1) dress-for radio (Women/Men/Both) + multi-select style chips (Casual, Business, Streetwear, Formal, Athletic, Church, Club) + occasion chips; 2) size selects (top/bottom/shoe) + budget radio ($/$$/$$$/No limit) + brand search with removable chips; 3) avatar setup — preview placeholder, take-selfie / pick-photo (opens photo-source sheet), body-type radio A–E, "use generic avatar" skip.

### Core
- **Home** — greeting, credits pill (→ Credits), bell with unread dot (→ Notifications), large dark "Match an outfit" CTA (→ wizard), quick-action grid (Add item / Shop matches / Saved looks), recent-outfit card row, closet summary row.
- **Closet** — search field, filter button (→ filter sheet), horizontally scrollable category radio chips (All/Shirts/Pants/Shoes/Jackets/Accessories), auto-fill item grid (min 110px), each item → Item detail; trailing dashed "Add item" tile.
- **Add item** — camera viewfinder placeholder with dashed crop guide, gallery + shutter + flip controls (shutter/gallery → AI detection), tips line.
- **AI detection / Confirm item** — photo, "AI detected: …" banner, editable name input, category/color/season selects, occasion tag chips, actions: Save to closet | Save & match (→ occasion step).
- **Item detail** — photo, favorite toggle, delete (→ confirm modal), retake/crop buttons, category/brand/size/notes fields, occasion chips, "Match an outfit with this" CTA, Save changes.

### Outfit wizard (3 steps + loading + results)
- **Pick base** — cards: use whole closet / snap new item / selectable closet grid (radio-select outline) → Occasion.
- **Occasion** — event radio chips (Dinner, Work, Club, Church, Ball, Vacation, Everyday), dress-code chips, time & place chips → Preferences.
- **Preferences** — source mode radio cards (Closet only / Closet + shopping / Shopping only), budget chips, boldness chips, "Generate · 1 credit" CTA (decrements credit balance), low-credit top-up link.
- **Generating** — spinner, cancel link; auto-advances to Results after ~1.8 s.
- **Results** — summary line of chosen parameters, 3 outfit option cards (items count, owned vs to-buy, est. cost) → Outfit detail; "Regenerate · 1 credit".
- **Outfit detail** — avatar preview panel + item list (owned rows with Swap links; missing item row dashed with price estimate and Shop button), "Why this works?" (explanation modal), actions: Save outfit (→ save-to-collection sheet), Share (→ share sheet), Shop missing.

### Shop & social
- **Shop** — context line ("Matching: Minimal belt…"), filter chips (open filter sheet), product grid with FEATURED badge, per-product save/hide mini-toggles → Product detail; affiliate disclosure footer.
- **Product detail** — photo, price/brand/store, match rationale, size & color selects, "Buy at PartnerStore ↗" (→ leaving-app confirm modal), "I bought this — add to closet" (→ confirm modal → closet).
- **Saved outfits** — collection radio chips (All/Work/Dinner/Vacation/Club) → Collection detail, outfit grid with "NEW MATCHES" badge, "+ Collection" (→ new-collection modal).
- **Collection detail** — rename link (modal), outfit cards each with ⋯ actions modal (move/share/delete), dashed "match a new outfit" tile.
- **Friend feedback** (shared-look recipient view) — outfit preview, vote buttons (👍 Wear it / 👎 Not this one / Suggest a change), comment list + composer, app-download prompt for non-users.

### Money & account
- **Profile** — avatar header with plan + Upgrade button, credits card, menu rows: Notifications (badge), Settings, Help center, Contact support, Invite a friend, Admin panel link, Log out (confirm modal).
- **Credits** — dark balance card, Buy credits (→ pack sheet → payment sheet → success modal; balance +50), subscription banner, recent usage ledger.
- **Plans** — Free / Plus (POPULAR) / Pro selectable cards, Subscribe CTA (label reflects selected plan), cancel-anytime note.
- **Notifications** — unread (outlined, dot) vs read items; each deep-links (new matches → Saved, friend vote → Feedback, low credits → Credits); admin broadcast item.
- **Settings** — account fields, change password (modal), notification toggles (push / product alerts / friend feedback / offers), privacy (private closet toggle, download data), Delete account (type-DELETE confirm modal → Welcome), Log out.
- **Help center** — search, 4 accordion FAQs, Contact support CTA.
- **Contact support** — topic select, message textarea, attach-screenshot dashed control, send (→ ticket-created success modal → Profile).

### Modals / sheets (bottom sheets on mobile, all dismissible via backdrop)
filter, delete-item confirm, photo source, save-to-collection, share, why-it-matches, swap item, leaving-app confirm, purchased confirm, new collection, rename, outfit actions, buy credits, payment, payment success, change password, delete account, logout confirm, support sent.

## Screens / Views — Admin Panel

Navigation model: desktop (≥880px) = dark (`#1c1c1e`) left sidebar, 216px, with 11 sections + logout + link to user prototype; below 880px the sidebar collapses to a ☰ hamburger opening a menu modal. Persistent white top bar: page title, global search, avatar. All content cards: white, 1px `#e5e5e5` border, 13px radius, on `#f4f4f5` canvas.

- **Login → 2FA → Forgot** — centered card; single secure admin login, authenticator code step, reset link.
- **Dashboard** — 5 KPI stat cards (users, generations, affiliate clicks, MRR, AI cost — each navigates to its section), 14-day bar chart, "Needs attention" list (open tickets, flagged AI users, broken affiliate links, ending campaign) deep-linking to sections.
- **Users** — search + plan/status filters + Export CSV; table (user, plan, credits, status badge) → **User detail modal** (stats trio incl. wardrobe *count only* privacy note, adjust credits modal with add/remove radio + reason field, suspend confirm, deletion-request action); pagination.
- **Products & affiliates** — search/filters, "+ Add product", MVP note (CSV/feeds later), table with thumbnail, price, clicks, state badge (Featured/Active/Inactive), AI tags, broken-link warning → **Product form modal** (image, name, price, category, affiliate URL, AI matching tags, state radio, delete/save).
- **Brand partners** — partner cards (type, commission %, products/clicks/est. revenue; paused = dimmed) → **Brand form modal** (name, type, commission, active toggle).
- **AI & cost control** — model selects (matching + vision), editable prompt template (monospace textarea), save (→ saved confirm) / test; credit cost per generation, free generations/month, daily cap inputs; safety-filter and auto-flag toggles; flagged-usage table with per-row Suspend; failed-requests count.
- **Credits & plans** — credit package cards (+ add/edit via package form modal with active + best-value toggles); subscription plan table (price, credits/mo, subscribers, Edit).
- **Ads & featured** — placement toggles with CTR readouts (home banner, results interstitial, shop sponsored slot); campaign table (type, dates, impressions, clicks) + **Campaign form modal** (name, type, slot, dates, end/save).
- **Notifications & content** — broadcast composer (title, body, audience select, send-now/schedule) → send confirm modal; help-center article list (published/draft, views) → **Article editor modal** (title, body, publish state radio).
- **Reports** — date-range select + Export CSV; four report cards: user growth & retention (bar chart), credits & AI cost, affiliate & product performance, outfits & engagement.
- **Support inbox** — status radio chips (Open/Waiting/Resolved), ticket list with unread dots and overdue flag → **Ticket detail modal** (message thread, internal note, reply composer, adjust-credits shortcut, mark resolved).
- **Admin settings** — email, change password modal, 2FA + session-timeout toggles, activity log, MVP single-login note.

## Interactions & Behavior
- **Navigation**: state-machine (`state.screen`), no page reloads. Back buttons pop a history stack (user app). Content scroll resets to top on navigation.
- **Modals**: `state.modal` (one at a time); backdrop click closes; inner click stopped. User app renders them as bottom sheets (rounded top, grab handle); admin as centered dialogs.
- **Selection controls**: multi-select chips toggle fill (`#1c1c1e` bg when on); radio groups are single-choice chips/cards; switches are 34×19px pills with animated knob (`transition: left .15s`).
- **Simulated logic to reproduce**: generate costs 1 credit (balance shown in header/rail/credits screens); payment success adds 50 credits; generating screen auto-advances ~1.8 s; logout/delete-account reset to Welcome; accordion FAQs expand/collapse.
- **Responsive**: user app swaps bottom tabs ↔ side rail at 900px; admin swaps sidebar ↔ hamburger menu at 880px. Grids use `repeat(auto-fill|auto-fit, minmax(…px, 1fr))` so they reflow at any width (mobile/tablet/desktop).
- **Hit targets**: interactive controls ≥ 34–44px.

## State Management (implementation guide)
- `screen` (current route — use real routing in production), `modal`, history stack
- `credits` (number, mutated by generate/purchase)
- `sel` map — multi-select chips, toggles, accordions, product save/hide
- `radio` map — single-choice groups (occasion, dress code, mode, budget, boldness, plan, pack, payment method, categories, collections, votes, ticket status…)
- `wide` — viewport breakpoint flag
- Real app additionally needs: auth/session, wardrobe items, outfits, products, collections, notifications, tickets — see proposal for data model hints.

## Design Tokens (greyscale placeholder palette)
- Ink / primary action: `#1c1c1e`; body text `#1c1c1e`; secondary `#555`; muted `#888`–`#999`
- Canvas: white (user app), `#f4f4f5` (admin); subtle fill `#f7f7f8`, row-hover/alt `#fafafa`
- Borders: `#e5e5e5` / `#e8e8e8` (cards, 1px), `#d6d6d6` (inputs, 1.5px), `#cfcfcf` (secondary buttons), dashed `#cfcfcf` (add/missing affordances)
- Image placeholders: `linear-gradient(135deg,#f0f0f0,#dcdcdc)` (darker variant for camera: `#e9e9e9→#d2d2d2`)
- Radii: 9–11px inputs/buttons, 12–16px cards/sheets, 999px chips/pills; sheets 20px top corners
- Type: system-ui stack; ~12–13px body, 11px labels (600), 17–19px screen titles (700–800), 24px KPI numbers (800); mono for section labels/URLs
- Icons: monochrome glyphs; any emoji are wrapped in `filter:grayscale(1)` — replace with a proper monochrome icon set (e.g. Lucide/Phosphor) in production

## Assets
No external assets. All imagery is CSS-gradient placeholders to be replaced with real photos (wardrobe items, products, avatar renders). Logos are text ("ASSEMBLE").

## PWA requirements (from proposal, not visualized)
Installable manifest + service worker, push notifications (matches/feedback/credit reminders/broadcasts), camera + gallery access for item capture, offline-tolerant closet browsing recommended.
