# Memory Studio — paid edition rollout

**Status (October 28, 2026):** The private Render service runs a sandbox Stripe payment and signed-license issuer prototype. The public website accepts **no purchases**; public license delivery, desktop activation and installation have not passed acceptance testing. The listed prices are proposed *one-time* launch offers.

| Edition | Proposed price | Planned entitlement |
|---|---:|---|
| My Life (`my_life`) | $59 one-time | Private personal projects, bulk import, chronology, written stories and voice notes |
| Family Legacy (`family_legacy`) | $119 one-time | My Life + guided interview questions, relationships, family history, chapter/story planning |
| Creator Studio (`creator_studio`) | $249 one-time | Family Legacy + professional workflows, AI-assisted scripts, transcription, soundtrack mixing and production tools |
| Beta (`beta`) | $0 while testing | Limited testing access only, not a paid edition |

## Architecture
- **Identity:** Account-free, local-first Windows app. Do not require a Supabase account, cloud login or media upload to use paid desktop editions.
- **Access:** Private Render backend signs Ed25519 licenses after independently confirming a paid Stripe session; Windows app must verify the license locally and apply edition-wide feature gates. A browser success URL or user-editable field never grants an entitlement.
- **Checkout:** Stripe sandbox Checkout is deployed privately using three server-configured one-time Price IDs. No account is needed; checkout and license fulfillment require complete secret configuration, signed webhook and acceptance tests. The public website does not launch checkout.
- **Fulfillment:** Sandbox-only server verifies paid sessions and expected price IDs via Stripe, issues an idempotent signed license into a persistent orders store, and emails activation when SMTP is configured. Refunds/disputes and reliable production fulfillment remain release blockers.
- **App gating:** Every premium desktop operation must validate a locally verified license before running; controls alone are insufficient. These entitlement checks still require integration and full Windows testing.
- **AI/cloud consumption:** One-time desktop prices do not imply unlimited ongoing cloud video rendering, AI transcription, or storage. Define explicit fair-use limits or optional usage plans before paid launch; keep basic local use independent.
- **Family access:** Family Legacy does not automatically include multi-user collaboration; invites, consent and cross-account sharing are a separate later addition requiring authorization review.
- **Rollout checks:** two-account privacy test; no-payment access rejection; tier-specific request rejection; charge/refund replay testing; quota and billing cost assessment; desktop installer license checks; support and account recovery paths.

## When / order
1. **Now:** three sandbox Stripe prices, private FastAPI issuer and Render service are prepared; MemoryStudio.tv uses the correct checkout origin and return address. No live charges or website checkout.
2. **Next:** configure the remaining Render sandbox secrets and outbound license email, install the issuer's public verification key in Windows, and run paid sandbox checkout→webhook→license→email→offline activation tests.
3. **Before collecting real money:** finish desktop feature gates, restore/update testing, signed installer, live Stripe pricing, refunds/taxes/support and customer privacy policies. Then explicitly enable production checkout.
4. **Afterward:** scale cloud rendering and bulk phone imports. Do not advertise those as available in a paid package until actually shipped.

**Security:** Never commit Stripe secrets, webhook secrets or license-signing private keys to public GitHub Pages or the Windows client. Payments and signing run only on the private Render service; the website remains static.
