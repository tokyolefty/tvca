# TVCA New Website — Project Notes

## Overview

New website for **Tokyo Tower View Clinic Azabujuban** (東京タワーヴュークリニック麻布十番).  
Eventual production host: `sakura.ad.jp` (Japan).  
Current test/staging: GitHub Pages or Netlify (free, static).

**GitHub repo:** https://github.com/tokyolefty/tvca

---

## Files

| File | Description |
|---|---|
| `index.html` | Main site — hero, services, hours, access, footer |
| `form.html` | Appointment request form — bilingual, Formspree-ready |
| `PROJECT.md` | This file |

---

## Design System

### Colors
| Token | Hex | Usage |
|---|---|---|
| `--navy` | `#1c2b3a` | Primary dark — headings, header, hero bg, buttons |
| `--navy-deep` | `#111d28` | Top bar, footer, contact strip |
| `--gold` | `#b8935a` | Accent — eyebrows, labels, CTA hover, active toggle |
| `--gold-light` | `#d4ab72` | Gold hover state |
| `--ivory` | `#faf9f7` | Page background |
| `--white` | `#ffffff` | Card backgrounds, header |
| `--stone` | `#f2f0ec` | Section alternate background, form sidebars |
| `--muted` | `#6b6b6b` | Body text, secondary labels |
| `--border` | `#e0ddd8` | Dividers, input borders |

Inspired by: https://www.donaldsonplasticsurgery.com/ — luxury medical, navy/gold/ivory palette.

### Typography
| Language | Font | Weights |
|---|---|---|
| Japanese | Noto Sans JP | 300, 400, 500, 700 |
| English | Inter | 300, 400, 500, 600 |
| Display headings | Cormorant Garamond | 400, 500, 600, italic |

### Layout
- Max content width: `1200px`
- Section padding: `96px 32px`
- Responsive breakpoints: `960px` (2-col → 1-col), `640px` (mobile)

---

## Bilingual System (JP / EN)

All text is driven by a JavaScript translations object — no `display:none` CSS hacks.

### How it works
1. Every text element has a `data-i18n="key"` attribute
2. `T.jp` and `T.en` objects hold all translations
3. `setLang('jp' | 'en')` iterates all elements and sets `textContent`
4. For HTML content (e.g. `<br>` in hero title), use `data-i18n-html="key"` instead
5. Language preference is saved to `localStorage` and auto-detected from browser on first visit

### Language toggle
- Located in the **top bar** (always visible on all screen sizes)
- Styled as a bordered pill with `JP` / `EN` buttons
- Active language shows gold background

---

## Pages

### index.html — Main Site

#### Sections (top to bottom)
1. **Top bar** — phone, hours, JP/EN toggle
2. **Sticky header** — brand name, nav links (Services / Hours / Access), Book CTA button
3. **Hero** — navy gradient, serif headline, description, two CTA buttons, specialty card panel (desktop only)
4. **Stats divider** — 3 min walk / EN/JP / 6 days / Online
5. **Services** — 3×2 grid, numbered 01–06, gold underline hover
6. **Hours** — table + contact info aside
7. **Access** — address/station/director/phone + Google Maps embed
8. **Contact strip** — dark navy, large gold phone number
9. **Footer** — brand, services column, info column, copyright

#### Services listed
| # | JP | EN |
|---|---|---|
| 01 | 内科・一般診療 | Internal Medicine |
| 02 | 心療内科・精神科 | Mental Health & Psychiatry |
| 03 | トラベルクリニック | Travel Medicine |
| 04 | COVID-19・ワクチン | COVID-19 & Vaccines |
| 05 | 漢方・アレルギー | Herbal Medicine & Allergy |
| 06 | 往診・オンライン診療 | House Calls & Telemedicine |

#### Clinic info
- **Address:** 〒106-0045 東京都港区麻布十番2-14-6 イイダビル1階 (IIDA BLDG. 1F, 2-14-6 Azabujuban, Minato-ku, Tokyo)
- **TEL:** 03-6809-3207
- **FAX:** 03-6809-3227
- **Director:** 林 哲也 / Tetsuya Hayashi, MD (Shinshu University School of Medicine)
- **Station:** Azabujuban Station, 3-min walk

#### Hours
| Day | Morning | Afternoon |
|---|---|---|
| Mon, Tue, Wed, Fri | 9:30–12:30 | 14:30–18:00 |
| Saturday | 9:30–12:30 | 14:30–18:00 |
| Thursday | Closed | 14:30–18:00 |
| Sun / Holidays | Closed | Closed (by appointment) |

---

### form.html — Appointment Form

Fully bilingual form matching the main site design.

#### Fields
| Field | Type | Required |
|---|---|---|
| Visit type (New / Returning) | Radio | Yes |
| Full name / 氏名 | Text | Yes |
| Furigana / ふりがな | Text | No |
| Date of birth / 生年月日 | Date | Yes |
| Gender / 性別 | Select | No |
| Phone / 電話番号 | Tel | Yes |
| Email / メールアドレス | Email | Yes |
| Consultation type / 診療内容 | Select | Yes |
| Preferred date / 希望日 | Date | No |
| Preferred time / 希望時間帯 | Select | No |
| Message / ご質問 | Textarea | No |
| Privacy consent | Checkbox | Yes |

#### Email delivery — Formspree setup (REQUIRED)
The form is ready but needs a Formspree account to actually deliver emails.

1. Go to https://formspree.io → sign up free (50 submissions/month on free tier)
2. Click **New Form** → enter the doctor's email address
3. Copy the form ID (looks like `xpwzabcd`)
4. Open `form.html` and find this line:
   ```html
   action="https://formspree.io/f/YOUR_FORM_ID"
   ```
5. Replace `YOUR_FORM_ID` with your actual ID:
   ```html
   action="https://formspree.io/f/xpwzabcd"
   ```
6. Push the change to GitHub — done.

---

## Hosting

### Current: GitHub Pages (free)
1. Go to https://github.com/tokyolefty/tvca → **Settings** → **Pages**
2. Source: `main` branch, `/ (root)` folder
3. Save → live at `https://tokyolefty.github.io/tvca`

### Alternative test host: Netlify Drop (free, instant)
1. Go to https://netlify.com/drop
2. Drag the `TVCA New Website` folder onto the page
3. Get a shareable URL immediately (no account needed)

### Production: sakura.ad.jp
When ready to go live on `sakura.ad.jp`:
1. Upload `index.html` and `form.html` to the sakura server via FTP/SFTP
2. Point the domain DNS to the server
3. No build step required — pure static HTML/CSS/JS

---

## Known Remaining Tasks

- [ ] **Formspree setup** — replace `YOUR_FORM_ID` in `form.html` with real ID after account creation
- [ ] **Google Maps embed** — the map URL in `index.html` is approximate; replace with a proper embed URL from Google Maps for the exact address
- [ ] **Enable GitHub Pages** — go to repo Settings → Pages to activate free hosting
- [ ] **Hero image** — currently using a solid navy gradient; could add a real photo of the clinic interior with a dark overlay for a more premium feel
- [ ] **Privacy Policy page** — the form references a privacy policy; a simple `privacy.html` page should be created
