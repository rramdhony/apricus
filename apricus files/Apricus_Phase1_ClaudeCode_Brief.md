# Apricus Co Ltd — Phase 1 Completion Brief
## Instructions for Claude Code

**Live site:** https://apricus.ruben-ramdhony.workers.dev/  
**Deployment:** Cloudflare Worker (single JS file serving HTML inline)  
**Goal:** Complete all Phase 1 scope items in one session today.

Before starting, read the current worker file in full so you understand the complete HTML/CSS/JS structure. Do not assume anything — read first, then act.

---

## Working Rules

- Do not break anything that currently works.
- Do not change the visual design system (colours, typography, spacing) unless a task explicitly requires it.
- All changes must be mobile-responsive. Test mentally against a 375px viewport.
- No external dependencies may be added. Everything stays vanilla JS and inline CSS, consistent with the existing codebase.
- After completing all tasks, do a final read of the full worker file to check for regressions before confirming done.

---

## Task 1 — Hero Section: Global Messaging

**What to change:**

Replace the current hero headline and subheadline with messaging that reflects global ambitions, not just the Mauritian market.

**Current headline:**
> Your Trusted *Import Partner* in the Indian Ocean

**New headline:**
> Global Meat & Seafood Importer — *Indian Ocean Strategic Hub*

**Current subheadline/descriptor:**
> Apricus Co Ltd bridges global food producers and the Mauritian market. We specialise in sourcing premium quality poultry, edible oils, legumes, and essential food staples with full regulatory compliance and transparent credentials.

**New subheadline:**
> Apricus Co Ltd connects international producers with buyers across the Indian Ocean, SADC, Europe, and the Far East. We specialise in meat, seafood, and essential food staples, operating from Mauritius as a strategic import and distribution hub with full regulatory compliance.

**Also update the small tag above the headline:**

Current: `Established in Mauritius since 2020`  
New: `Indian Ocean Strategic Hub — Established 2020`

**CTA buttons:** Keep as-is. No change needed.

---

## Task 2 — Target Markets: Add Regional Reach

**What to change:**

In the "About Apricus" section, the current stat strip shows: `2020 / SADC / 5+ / MRA`

Update those stats as follows:

| Stat | Current | New |
|---|---|---|
| Year | 2020 | 2020 |
| Regional | SADC | SADC + Indian Ocean |
| Categories | 5+ | 6+ |
| Compliance | MRA | MRA Licensed |

Below the existing compliance tick list in the About section, add one new bullet point:

> ✓ Actively targeting export and supply markets across Europe, SADC, the Far East, and the Indian Ocean region

**Also:** In the sourcing flags row at the bottom of the Products section, add two flags:

Current: `🇹🇷 Turkey 🇪🇬 Egypt 🇧🇷 Brazil 🌏 Asia 🌍 SADC Region`  
New: `🇹🇷 Turkey 🇪🇬 Egypt 🇧🇷 Brazil 🇺🇦 Ukraine 🌏 Far East 🌍 SADC 🇪🇺 Europe`

---

## Task 3 — Factual Corrections and Pipeline Labelling

**What to change:**

The client has advised that some information needs to be more accurate about what is confirmed versus what is in progress. Apply these changes precisely:

**Products section — Seafood card:**

The current site has no seafood card. Add one (see Task 4 below). The existing "Regional & Institutional Supply" card currently has the label `Pipeline`. Keep that label.

**Products section — Legumes card:**

Current label: `Expanding Range`  
No change needed. This is accurate.

**About section — expansion copy:**

Current: `Expanding into the SADC region with a vision to become a leading regional importer`  
New: `Building a regional footprint across SADC and the Indian Ocean, with active supply discussions in Europe and the Far East`

**Hero and About section — remove any implication that seafood is already a core product:**

Seafood is being added as an expanding/new category, not a core category. Ensure the hero subheadline (updated in Task 1) says "meat, seafood, and essential food staples" which is accurate as an aspirational direction. The seafood product card (Task 4) must carry the label `New Category` not `Core Category`.

**Freeport Operator:**

Do not add any Freeport content to the site. This is not yet confirmed and should not appear.

---

## Task 4 — Add Seafood as a Product Card

**What to add:**

Insert a new product card in the Products section, positioned directly after the "Poultry & Meat" card (which stays as the first card).

**Card content:**

```
Icon: 🐟
Title: Seafood & Marine Products
Body: Frozen and fresh seafood including fish, shellfish, and processed marine products. Sourced from certified suppliers across the Indian Ocean, Asia, and beyond, targeting Mauritian and regional buyers.
Label: New Category
```

The label styling for `New Category` should visually match the existing `Pipeline` label (same colour/style), not the `Core Category` style. These are items in development, not confirmed core lines.

---

## Task 5 — Navigation Labels

**What to change:**

Update the top navigation anchor labels only. Do not change the anchor IDs as they are referenced throughout the page.

| Current Label | New Label | Anchor (unchanged) |
|---|---|---|
| About Us | About | #about |
| Our Products | Products | #products |
| Credentials | Compliance | #credentials |
| Contact Us | Contact | #contact |

Update both the top nav menu and the footer navigation column to match.

---

## Task 6 — Expand the Contact / Enquiry Form

**What to change:**

The current form has: First Name, Last Name, Company/Organisation, Email Address, Enquiry Type (dropdown), Message.

**Keep all existing fields.** Make the following additions and changes:

**1. Enquiry Type dropdown — replace current options with:**
```
-- Select enquiry type --
Supplier Enquiry (I want to supply Apricus)
Buyer / Wholesale Enquiry (I want to buy from Apricus)
Request for Quotation (RFQ)
Freeport / Trade Partnership
General Enquiry
```

**2. Add a new field after Company/Organisation:** Product Category Interest (dropdown, not required)
```
-- Select product category (optional) --
Meat & Poultry
Seafood & Marine Products
Edible Oils
Flour & Grains
Legumes & Pulses
Fresh & Frozen Vegetables
Multiple Categories / Full Range
Other
```

**3. Add a new field after Product Category Interest:** Country / Region (text input, not required)
- Label: `Country or Region`
- Placeholder: `e.g. South Africa, UAE, France`
- This tells Apricus where the enquirer is based or wants to trade with.

**4. Update the form heading and subtext:**

Current heading: `Send an Enquiry`  
New heading: `Send an Enquiry or RFQ`

Current subtext: `For supplier verification requests, wholesale enquiries, or general questions.`  
New subtext: `For supplier verification, wholesale enquiries, RFQ submissions, or trade partnership discussions. We respond within 2 business days.`

**5. Form submission:**

The form currently does client-side validation and shows a success message. Keep that exact behaviour. No backend changes. Just ensure the new fields are included in the validation logic if marked required (only Email Address and Enquiry Type are required; all new fields are optional).

---

## Task 7 — Custom Domain Preparation

**What to do:**

The client's domain is `apricus-mu.com`. DNS is not yet confirmed, so do not change any Cloudflare routing.

However, update the following references in the HTML that currently show placeholder or worker URL references:

- In the footer, the email shows `info@apricus-mu.com`. Confirm this is already correct and leave it.
- In the page `<title>` tag, if it currently reads anything other than `Apricus Co Ltd — Global Meat & Seafood Importer`, update it to: `Apricus Co Ltd — Global Meat & Seafood Importer`
- In the `<meta name="description">` tag (add one if it does not exist):
  ```
  Apricus Co Ltd is a Mauritius-based import and distribution specialist in meat, seafood, and essential food staples. Serving buyers and suppliers across the Indian Ocean, SADC, Europe, and the Far East.
  ```
- Add `<meta property="og:title">` and `<meta property="og:description">` matching the above, plus `<meta property="og:url" content="https://apricus-mu.com">` for when the domain goes live.

---

## Task 8 — Footer and Privacy Policy

**What to change:**

**Footer Compliance column:**

The current footer has a Compliance column with BRN, VAT, MRA links that go to `#`. Leave those as-is.

Add a working Privacy Policy link. The Privacy Policy page does not exist yet, so add it as an inline section rendered by a hash route.

**Implement a minimal Privacy Policy:**

When the user clicks the `Privacy Policy` link in the footer, scroll to or reveal a `#privacy` section at the bottom of the page (below the footer, or as a modal overlay — your choice of implementation, whichever is cleaner in the existing codebase).

The Privacy Policy content to display:

```
Privacy Policy — Apricus Co Ltd
Last updated: May 2026

1. Who We Are
Apricus Co Ltd is a registered company in Mauritius (BRN C20174608). Our registered address is Shivala Road, Isidore Rose, Republic of Mauritius. Contact: info@apricus-mu.com

2. What Information We Collect
We collect information you voluntarily submit through our enquiry form: your name, company name, email address, and enquiry details. We do not collect any information automatically beyond standard server logs.

3. How We Use Your Information
Information submitted through our enquiry form is used solely to respond to your enquiry or RFQ. We do not sell, share, or transfer your personal data to third parties except where required by Mauritian law.

4. Data Retention
Enquiry data is retained for up to 24 months for the purpose of correspondence records, after which it is securely deleted.

5. Your Rights
Under the Mauritius Data Protection Act 2017, you have the right to access, correct, or request deletion of any personal data we hold about you. Contact us at info@apricus-mu.com to exercise these rights.

6. Cookies
This website does not use tracking cookies or analytics. No personal data is collected through cookies.

7. Contact
For any privacy-related queries, contact: info@apricus-mu.com
```

**Footer bottom bar:**

Current: `© 2026 Apricus Co Ltd. All rights reserved. Registered in Mauritius. BRN C20174608`

Update to: `© 2026 Apricus Co Ltd. All rights reserved. Registered in Mauritius — BRN C20174608 | VAT 27831543`

---

## Task 9 — Phone Number Placeholder

**What to change:**

The contact section currently shows `+230 [TBC]` for the phone number.

Replace with: `+230 — contact via email or WhatsApp`

This avoids the placeholder looking unfinished. When the client provides the number, this can be updated in one line.

---

## Final Checks Before Confirming Done

### Part A — Feature Completion

Work through this checklist after all tasks are complete:

- [ ] Hero headline and subheadline updated
- [ ] "Indian Ocean Strategic Hub" tag above hero headline in place
- [ ] Regional markets bullet added to About section
- [ ] Sourcing flags row updated with Ukraine, Far East, Europe
- [ ] Seafood card added after Poultry & Meat, labelled "New Category"
- [ ] Nav labels updated in top menu and footer
- [ ] Contact form has new fields: Product Category, Country/Region
- [ ] Enquiry Type dropdown has updated options including RFQ
- [ ] Form heading updated to "Send an Enquiry or RFQ"
- [ ] Page title tag updated
- [ ] Meta description added
- [ ] OG tags added
- [ ] Privacy Policy content accessible from footer link
- [ ] Footer bottom bar shows VAT number
- [ ] Phone placeholder replaced with email/WhatsApp instruction
- [ ] No existing functionality broken

### Part B — Studio26 QA Standard

After Part A is complete, run the full **Studio26 QA Standard** checklist covering Functional QA, Mobile Responsiveness, and WCAG 2.1 AA Compliance. This standard applies to every Studio26 build without exception.

The standard is in: `Studio26_QA_Standard.md` (in the same directory as this brief).

**Do not mark this build as done until every item in the QA Standard sign-off checklist is checked.** If any item fails, fix it before proceeding. Document any item that cannot be resolved in this session with a specific note on what is blocking it.

Once both Part A and Part B are clean, deploy to the Cloudflare Worker and confirm the live URL is responding correctly.
