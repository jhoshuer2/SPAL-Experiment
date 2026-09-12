# Spal Design System

A design system for **SPAL** — *Spending • Profiting • Analysing • Looping* — a mobile-first, voice-first business companion for informal and small entrepreneurs across Africa (food sellers, market traders, salon/kiosk/bar owners, fashion vendors). It replaces spreadsheets and mental math with a friendly, conversational assistant: record a sale or expense in seconds, see your real (cash-basis) profit, chat with an AI coach, and grow.

This system was built by exploring SPAL's production codebase and its own internal design roadmap, then **elevating the visual craft** — sharper typographic hierarchy, calmer rhythm, layered depth, a proprietary geometric symbol language — without changing the product's structure or flows. Where the shipped app and its own design roadmap disagreed on a value, the shipped code won (ground truth); the roadmap's *philosophy* shaped how existing tokens were organized and used.

## Sources
- **GitHub:** [github.com/MrItrends/spal](https://github.com/MrItrends/spal) (branch `master`) — a Next.js 16 / Tailwind v4 / Framer Motion PWA. Explore it directly for the full product: API routes, Supabase schema, the AI advisor system, gamification, voice recording, etc. — everything not reflected here (this system focuses on visual language + a representative UI kit, not full functional parity).
- Two documents inside that repo shaped this system directly: `DESIGN.md` (the product's own aspirational "Design Operating System" — v2 vision for a more premium, distinctive SPAL) and `SPAL_DESIGN_SYSTEM.md` (a build reference reflecting what's actually implemented today). Both are worth reading in full if you continue this work.
- If you have write access to the repo, treat this design system as a companion reference — pull real component code from `components/ui/`, `components/shared/`, `components/records/` etc. for anything beyond the primitives rebuilt here.

## Fonts — flagged substitution
Production SPAL loads **Satoshi** (display/brand voice) via a licensed Fontshare CDN link and **Inter Tight** (body) via `next/font`/Google Fonts. Neither is redistributable as a committed static file under their license, so `tokens/fonts.css` loads both the same way — by URL — rather than bundling binaries. This is the *real* typeface pairing, not a substitute; no further action needed unless you'd prefer self-hosted font files, in which case send them over and this file can point at local `@font-face` rules instead.

## Iconography — flagged substitution
Production SPAL uses **`hugeicons-react`** exclusively (per `SPAL_DESIGN_SYSTEM.md`: "Icons: hugeicons-react ONLY... no emoji as UI icons") — a React-component icon library with no plain browser/CDN distribution, so it can't be copied into a static design system. The repo's own `package.json` already lists **`lucide-react`** as a secondary dependency, and Lucide ships a CDN-friendly build with a near-identical geometric, consistent-stroke, rounded-terminal style — so components/cards in this system use inline SVG glyphs styled to match that language rather than a copied hugeicons export. If you have access to the hugeicons license/assets, swap them in for full fidelity.
No emoji are used as functional UI icons anywhere in this system, matching source.

## Content fundamentals
- **Voice:** a friendly, encouraging business coach — never a spreadsheet. Plain WhatsApp-level language, the "3-second rule" (a user should understand any line in 3 seconds).
- **You, not I:** copy speaks directly to the owner — "Your Sales Today", "Track your sales, understand your profit, and grow."
- **Celebrate, never shame:** *"You spent more money than you made today"* — not *"Your expenditure exceeded your revenue."*
- **Banned words:** expenditure, revenue, liabilities, assets, ledger, reconcile — any accounting jargon.
- **Buttons are short action phrases:** "Record Sale", "Mark paid", "Head Back Home" — verb-first, no punctuation.
- **Empty states are encouraging, not apologetic:** *"No activity yet today"* + a direct next step, never a guilt trip.
- **Emoji:** used sparingly and only in celebratory microcopy ("Welcome to {Business}! 🎉", "Nice one! 🎉") — never as functional icons or in persistent UI chrome.
- **Numbers carry weight:** currency defaults to ₦ (NGN) via `formatCurrency()`; big figures always get the bold/tabular treatment — they're the emotional core of every screen.

## Visual foundations
- **Color philosophy — "one confident accent."** Navy (`--spal-navy`) is the dominant tone for text and structure. Green (`--spal-green`) is the *single* primary accent — sales, primary CTAs, success. Blue, purple and orange are supporting, purpose-bound colors (profit/AI, coach, expenses) that never appear at equal visual weight to green on one screen. Orange in particular is an *expense-only* action color, never a co-equal brand color.
- **Signature app background.** The canvas is a soft sage-green tint (`--spal-bg #EEF3E9`), not white or gray — this tint alone is recognizably SPAL.
- **Typography.** Satoshi (display, tight −0.02em tracking, bold) for headings and big numbers; Inter Tight for body copy. Never Poppins (explicitly banned in source — "heavily associated with generic startup and AI-generated products"). Financial figures get a distinct oversized, tabular, high-contrast treatment (see `guidelines/type-numbers.html`).
- **Spacing rhythm.** Tight *inside* components (4–12px gaps), generous *between* sections (24–32px) and consistent 20px page margins — the contrast between tight and generous is what reads as "considered" rather than "padded."
- **Corner-radius hierarchy.** Seven explicit steps (10/14/18/20/24/28/full) — each a distinct size class, never one blanket `border-radius`. Inputs (14) read smaller/tighter than stat cards (20) which read smaller than sheets (28).
- **Depth is layered, not heavy.** Every shadow token is two co-authored layers — a tight near-black contact shadow plus a soft, larger, low-opacity ambient falloff — never a single heavy `box-shadow`. See `guidelines/elevation-shadows.html`.
- **Cards, used sparingly.** Per the product's own roadmap: prefer borderless sections with generous padding over stacking cards; when a card is used it gets a hairline border and one of the two-layer shadows, never a colored left border.
- **Backgrounds.** Mostly flat, tinted surfaces. Gradients are reserved for exactly two contexts: the onboarding/AI voice canvases (soft multi-stop washes) and one "vivid" hero-card family (profit/sale/expense). No photography in the core product UI; when photography does appear (marketing) it's real entrepreneurs in authentic African environments, natural light — never corporate stock photos, handshakes, or staged "startup" imagery.
- **Motion — "flow, never bounce."** `easeOut`/custom-cubic only (`cubic-bezier(0.4,0,0.2,1)` default, `(0.22,1,0.36,1)` for entrances); real spring physics are explicitly banned. Entrances fade + rise 8–12px, staggered ~40ms apart. A single celebratory cubic (`(0.34,1.2,0.64,1)`) is allowed only for onboarding/badge-unlock delight moments.
- **Press states are tactile, not chromatic.** Buttons/pills/cards scale to 0.96–0.98 on press; color never flashes or darkens on tap.
- **Hover states** (desktop-canvas only, since this is a mobile-first PWA): subtle background lightening on menu rows, opacity dips on links — never a color hue change.
- **Transparency & blur** appear in exactly two places: the frosted bottom nav (`saturate(180%) blur(20px)` over 88% white) and glass cards over colored/photo backgrounds (`blur(20px)` over ~14% white). Never used decoratively elsewhere.
- **Borders** are hairline (1–1.5px) and low-contrast (`neutral-200` or `rgba` tints) — they define edges, they don't decorate.

## The signature — five things that make it recognizably SPAL
1. **Spacing system:** tight-in/generous-between rhythm + a 7-step radius hierarchy (never uniform rounding).
2. **Color philosophy:** navy-dominant, one confident green accent, purpose-bound supporting hues that are never co-equal.
3. **Motion language:** *flow* — easeOut/custom-cubic, fade+rise entrances, 0.96–0.98 tactile press, zero spring/bounce.
4. **Typography rhythm:** Satoshi display + Inter Tight body, tight tracking, oversized tabular treatment for money.
5. **Recurring motif — the geometric symbol system:** proprietary abstract marks (expanding rings, orbital motion, ascending layers, radiating structure...) standing in for icons/mascots wherever a business concept needs a visual anchor. This was defined in the product's own roadmap but not yet built in code — `components/brand/SpalSymbol.jsx` operationalizes it. Apply it consistently in empty states, loading states, onboarding and section dividers and it becomes the thing people recognize before they see the logo.

## Components
Built as faithful reconstructions of the real `components/ui/` + `components/shared/` + `components/gamification/` inventory, elevated in visual craft:
- **Core** (`components/core/`) — `Button`, `Card`, `Badge`, `Input`, `PillChip`
- **Feedback** (`components/feedback/`) — `InsightCard`, `UndoToast`, `Skeleton`/`SkeletonRow`
- **Navigation** (`components/navigation/`) — `BottomNav`, `TopNavPills`, `QuickMenuFab`
- **Brand** (`components/brand/`) — `SparkAvatar`, `SpalSymbol`
- **Gamification** (`components/gamification/`) — `WeeklyChallengeCard`

**Intentional additions** (not literal 1:1 source files, added because the source *describes* the pattern without a shared component): `Skeleton`/`SkeletonRow` (DESIGN.md mandates "skeleton screens, not spinners"), `TopNavPills` (the identical nav-pill row was duplicated inline across Home/Records/Insights — factored out here), `SpalSymbol` (DESIGN.md's "proprietary geometric symbol system" spec, not yet built in the app).

**Not yet built** — the source defines more component families than this pass covered; flagging rather than silently omitting, per this system's own build rules:
`AddRecordSheet`, `ExportSheet`, `SwipeableRow`, `CameraCapture` (records/), `VoiceRecorder` (voice/), `PaywallGate` (paywall/), `AchievementsSection`, `BadgeCelebration` (gamification/), `DateTimePicker`, `HomeCoachmarks`, `PWAInstallPrompt`, `RegisterSW` (shared/). The Add Sale/Expense bottom sheet *is* demonstrated as a working composition inside the mobile-app UI kit (`ui_kits/mobile-app/AddRecordSheet.jsx`) — just not yet promoted to a standalone reusable component card. Ask to continue and these can be built out in a follow-up pass.

## UI kit
`ui_kits/mobile-app/` — an interactive click-through of the one product surface in this codebase (the SPAL mobile PWA): onboarding splash → Home (profit hero, sale/expense split, owed banner, recent activity) → Records (filterable, date-grouped ledger) → Add Sale/Expense bottom sheet, with the Quick Menu FAB wired throughout. Built directly from the real screen source (`app/(main)/home`, `app/(main)/records`, `app/(onboarding)/welcome`, `components/records/AddRecordSheet.tsx`), not from screenshots.

## Index
```
styles.css                 → root stylesheet, @imports every token file below
tokens/
  fonts.css                 webfont loading (Satoshi via Fontshare, Inter Tight via Google Fonts)
  colors.css                 brand, tints, neutrals, semantic surfaces, category palette
  typography.css             type scale, weights, tracking
  spacing.css                spacing scale, radius hierarchy, shell width
  effects.css                 shadows, motion easing/duration, gradients
guidelines/                 18 foundation specimen cards (Colors, Type, Spacing, Motion, Elevation, Brand)
assets/
  logo/spal-wordmark.webp
  brand/spal-ai-orb.webp      the SPAL AI mascot orb — the one non-geometric brand asset
  illustrations/              onboarding preview cards, empty-state mascots, get-started decoration
  backgrounds/                splash + AI-voice-canvas backgrounds
  icons/                       real nav icons (SVG) + app icons (PNG) copied from source
components/
  core/          Button, Card, Badge, Input, PillChip
  feedback/      InsightCard, UndoToast, Skeleton
  navigation/    BottomNav, TopNavPills, QuickMenuFab
  brand/         SparkAvatar, SpalSymbol
  gamification/  WeeklyChallengeCard
ui_kits/mobile-app/   interactive click-through of the SPAL mobile PWA
thumbnail.html         homepage tile
SKILL.md               Claude-Code-compatible skill export
github.md               source-repo sync record
```

## Caveats & where to help next
- **Fonts/icons are flagged substitutions** (see above) — both are the *real* choices, just loaded/drawn differently than production for licensing/portability reasons. Send real font files or hugeicons assets if you'd like exact parity.
- **Component coverage is partial** — 13 of ~23 source component files were rebuilt (see "Not yet built" above). Say the word and the rest get built out.
- **One UI kit, three screens** — Insights, Goals, the AI chat (`/ask`), Inventory, Profile, and the full onboarding flow (business type, tracking method, etc.) all exist in source but aren't recreated yet.
- **The geometric symbol system is new code**, not a copy of anything shipped — it operationalizes DESIGN.md's spec. Look at `components/brand/SpalSymbol.jsx` and the `guidelines/brand-symbols.html` card and tell me if the shapes feel right for the brand; this is the single highest-leverage thing to get right for a memorable identity.

**My ask:** tell me which of the above to prioritize — more screens, the remaining components, or refining the symbol system/motion further — and I'll keep iterating until this feels unmistakably SPAL.
