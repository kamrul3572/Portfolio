# 🎨 UI Redesign Prompt — Portfolio Website (kamrul.bd)

> **প্রম্পটের কাজ:** এই ওয়েবসাইটের **UI/ভিজ্যুয়াল ডিজাইন** নতুন করে সাজানো।
> **গুরুত্বপূর্ণ:** শুধুমাত্র দেখতে কেমন হবে সেটা পরিবর্তন করবে। **কনটেন্ট, টেক্সট, 기능 (theme toggle, language toggle, মোবাইল মেনু, contact form, i18n dictionary), সেমান্টিক HTML স্ট্রাকচার কোনোটা পরিবর্তন করা যাবে না।** নতুন কোনো লাইব্রেরি/Framework যোগ করা যাবে না (pure HTML + CSS + JS থাকবে)। `data-i18n` অ্যাট্রিবিউট, `id`, `class` (নতুন class যোগ করা যাবে, কিন্তু existing class মুছে ফেলা বারণ, যাতে JS ভেঙে না যায়) — সব অক্ষত রাখতে হবে।

---

## ০. ডিজাইন ফিলসফি (Design Philosophy)

এই পোর্টফোলিওটা MD Kamrul Islam-এর — **Electrical & IoT Engineer / Diploma student**। লক্ষ্য: ইউনিভার্সিটি অ্যাডমিশনের সময় academic recruiter/প্রফেসরের চোখে এটা যেন **পেশাদার, পরিচ্ছন্ন, আধুনিক** লাগে, আর candidate-এর সিরিয়াসনেস ও প্রযুক্তি দক্ষতা ফুটে ওঠে।

**৫টি মূল নীতি:**
1. **পরিচ্ছন্নতা (Clarity):** একসাথে কম রঙ, কম জমাট লেআউট। ভিজ্যুয়াল নয়েজ কমাতে হবে।
2. **ধারাবাহিকতা (Consistency):** সব কার্ড, বাটন, চিপ, আইকন ব্যাজ একই design language-এ হবে। ইনলাইন `style="..."` চারদিকে ছড়ানো — এগুলো কমিয়ে reusable class-এ আনা।
3. **ভিজ্যুয়াল হায়ারার্কি (Hierarchy):** সব সেকশন টাইটেল যদি একই gradient-এ হয়, তবে কোনোটা আর জোর পায় না। গ্রেডিয়েন্ট কম, কম্পোজড করে প্রয়োগ।
4. **আধুনিকতা (Modern feel):** সূক্ষ্ম glow, proper spacing, consistent radius। কিন্তু অপ্রয়োজনীয় অ্যানিমেশন/ঠাসাঠাসি নয়।
5. **প্রফেশনাল টোন:** "hobby project" look না — "production candidate portfolio" look।

---

## ১. যা যা **সঠিক** ও **রাখা উচিত** (Don't break these)

- ✅ ডার্ক + লাইট থিম দুটোই কাজ করে — দুইটা থিমেই redesign-টা consistent হতে হবে।
- ✅ EN/BN ল্যাঙ্গুয়েজ টগল কাজ করে — টেক্সট হ্যান্ডেলিং ঠিক রাখো।
- ✅ Hero অ্যাভাটার (gradient ring) ডিজাইনটা ভালো — কিন্তু নিচে তরিফাই করা হয়েছে।
- ✅ Glassmorphism card ধারণা — রাখা যাবে, তবে **সামান্য** বেশি transparent/blur বাদ দিয়ে readability বাড়ান।
- ✅ Sticky navbar, smooth scroll, Active-section highlight (Intersection Observer) — কাজ চলবে।
- ✅ Contact form (mailto), social links, Google Maps location links — সব ফাংশনাল থাকবে।
- ⚠️**নোট:** Social links বর্তমানে platform homepage-এ যায় (linkedin.com, github.com…) — এটা content/ও cozojunction ব্যাপার, UI প্রম্পট হিসেবে **স্পর্শ করবে না**, কিন্তু design-এ social icons-এর consistency ঠিক রাখবে। (এগুলো আসল প্রোফাইল লিংক হলে সেট আলাদা কাজ।)

---

## ২. ডিজাইন টোকেন (Design System) — Root Variables

বর্তমানে `:root`-এ অনেক accent ভেরিয়েবল আছে (cyan, electric, purple, amber, emerald + gradient)। **রঙ কমিয়ে এককভাবে ব্যবহার:**

**নির্দেশনা — কালার প্যালেট সুশৃঙ্খল করো:**

| উপাদান | প্রস্তাবিত মান (value) |
|---|---|
| Primary accent (বাটন, active link, focus) | Cyan/Blue — `#06b6d4` → `#3b82f6` রেঞ্জ। একটাই প্রধান accent হোক। |
| Neutral (bg, text, border) | বর্তমান dark: `#070a12` / `#0d1322` / `#0f172a` / `#f8fafc` / `#94a3b8` / `#64748b` — ভালো, ধরে রাখো। |
| Semantic সবুজ (success, "✓" ফলাফল, GPA highlight, skill-high) | শুধু `#10b981` → এটা "positive/success" বোঝাতে। |
| Semantic হলুদ (warning/basic) | শুধু `#f59e0b` → "foundational/basic" level বোঝাতে। |
| Semantic নীল (intermediate) | শুধু `#3b82f6` → "medium" level। |
| Purple / Pink / random border-top colors | **অপ্রয়োজনীয় বৈচিত্র্য — বাদ দাও।** Medal/badge-এ শুধু gold/silver/bronze (emerald/amber/blue) semantic ব্যবহার হবে। |

**নিয়ম:**
- **গ্রেডিয়েন্ট মুছে ফেলো most section titles থেকে।** `gradient-text` শুধুমাত্র **Hero-র নাম** এবং **একটা CTA button**-এ রাখবে। বাকি section title হবে solid primary accent color + নিচে ছোট সূক্ষ্ম underline/bar divider।
- **Achievements-এর random প্রতিটা কার্ডে ভিন্ন color border-top (green/cyan/pink) মুছে দাও** — সব medal card একই neutral card হবে, শুধু badge (Gold=amber, Silver=blue, Bronze=emerald) দিয়ে পার্থক্য দেখাবে।
- **Skills chip-এর left border color (green/blue/amber) ধরে রাখা যায়** — এটা semantic (level) দেখায়, কিন্তু সূক্ষ্ম ও consistent রাখবে।
- **Language card-এর প্রতিটা আলাদা gradient progress bar না** — সব একই primary gradient ধরে রাখো, শুধু percentage পার্থক্য হবে।

**Typography:**
- Font stack ঠিক রাখো: Outfit (heading) + Inter (body) + Hind Siliguri (Bangla fallback)।
- Type scale (`--font-size-*` clamps) ঠিক থাকবে। কিন্তু **section-title** টাইপ সাইজ একটু কমান: ২xl-এর বেশি যাবে না, margin-consistent (২rem)।
- Spacing gap/বড় paragraph হয়ে শ্বাস নেওয়ার জায়গা থাকবে (section padding 5rem ঠিক আছে)।

---

## ৩. গ্লোবাল/সিস্টেম্যাটিক ফিক্স

1. **ইনলাইন style-এর লাগাম:** এখন চারদিকে `style="color:#..."` / `margin-top: 2rem` ইত্যাদি ছড়ানো। এগুলো নতুন reusable utility class-এ রূপান্তর করো (যেমন `.mt-2`, `.text-muted`, `.color-success` ইত্যাদি)। গঠনমূলকভাবে HTML cleaner করবে। (মনে রেখো: text মান change করা যাবে না, শুধু styling logic class-এ তোলা।)
2. **সব card radius & padding একরকম:** `border-radius: 20px`, padding `2.25rem` (desktop) / `1.5rem` (mobile) — সব glass-card-এ uniform। badge/icon radius-ও এক ধাপে।
3. **অতিরিক্ত shadow/blur কমান:** Glassmorphism-এ readability বেশি প্রাধান্য। `backdrop-filter: blur` desktop-এ `16px`→`12px`, mobile-এ `8px` এলাকায় রাখো। Card bg একটু opaque যাতে text স্পষ্ট।
4. **হোভার এফেক্ট consistent:** সব কার্ডে একই transform (`translateY(-4px)`) + border glow। অদ্ভুত আলাদা hover বাদ।

---

## ৪. সেকশন-বাই-সেকশন নির্দেশনা

### ৪.১ Navbar (`.navbar`)
- **সমস্যা:** এক পেজে ৯টি nav link — desktop-এ navbar ঠাসা দেখায়।
- **সমাধান:** Desktop-এ nav link textস্পেসিং/ওয়ার্ড আরামদায়ক করো, font-weight 500, hover underline animation ঠিক রাখো। Desktop-এ সব item দেখাবে কিন্তু **gap/ব্যবধান বাড়িয়ে** পরিষ্কার করো। (মোবাইলে drawer-এ সব যাবে।)
- Theme toggle ও English toggle বাটন — icon + text-এ **alt/aria-label ঠিক** আছে। Desktop-এ toggle গুলোকে সামান্য টাইট (gap 0.75rem) সাজাও।

### ৪.২ Hero (`.hero`)
- **সমস্যা:** Avatar 320px circle বড়, hero column 0.8fr — desktop-এ ভারসাম্য। Content column-এ অনেক সামগ্রী stacked।
- **সমাধান:** hero-grid ratio ঠিক করো (`1.15fr 0.85fr` প্রায়)। অ্যাভাটার radius ভালো, কিন্তু **অ্যাভাটারের নিচে সামান্য space** ও gradient ring-এর glow নরম করো (shadow 0 0 35px, opacity ±10%)। 
- Hero-badge pill + meta-chips একই design family (রাউন্ডেড, subtle border)। meta-chip আইকন ও টেক্সট gap consistent।
- **Hero title**: gradient name ছাড়া বাকি "Hello, I'm" solid। Tagline text-secondary। CTA দুটো বাটন same height (min-height 48px)।
- Social icons: uniform 44px circle, hover subtle lift। ok রাখো। WhatsApp-এর green hover বিশেষ রাখা যেতে পারে।

### ৪.৩ About (`.about-grid`)
- **সমস্যা:** Professional Summary ও Career Objective দুটি কার্ডের টেক্সট পরিমাণ ভিন্ন → height mismatch। আর নিচে তৃতীয় বড় কার্ডে (Hobbies & FOSS) inline grid — লেআউট দূর্বল।
- **সমাধান:** `about-grid`-এর দুই কার্ড equal height (align-items: stretch আছে — ঠিক রাখো, content-কে flex column handle করো)। Padding consistent। 
- **Hobbies/FOSS bar:** এটা সামান্য আলাদা visual ট্রিটমেন্ট দাও (উদাহরণ: soft panel bg, বা gradient left border) যাতে "about" সেকশনের ভেতরে subtitle-ভাগ বোঝা যায়, কিন্তু একই card language-এ।
- **FOSS icon:** Ubuntu orange (`#e95420`) ও FOSS green — এই দুটো brand color রাখা okay, কিন্তু সূক্ষ্ম chip হিসেবে।

### ৪.৪ Education (`.timeline`)
- **সমস্যা:** Timeline ঠিক আছে কিন্তু "CGPA progression" tags বিক্ষিপ্ত দেখায়।
- **সমাধান:** Timeline dot pulsing glow ধরে রাখো। **CGPA badge-গুলো** সমান আকার, uniform gap, smallest chip (score)। শেষের emerald color শুধু S6 (highest 3.76)-এ highlight রাখো। Bachelor aspiration item-এ purple accent সূক্ষ্ম রাখা যায় (পুরো section-এ একটাই non-primary accent হিসেবে, বা বাদ দিয়ে primary accent-এ মিশিয়ে দাও)।
- **Timeline-company icon** + org text inline alignment ঠিক রাখো (`gap: 0.5rem`)।

### ৪.৫ Skills (`.skills-category`)
- **সমস্যা:** High/Medium/Basic level chips + soft skills grid — তথ্যভিত্তিক কিন্তু visually flat।
- **সমাধান:** Level label-এর icon badge-এর color semantic (green/blue/amber) Consistent। skill-chip density ঠিক (radius 14px, gap 0.85rem)।
- **Soft skills grid** — বর্তমানে icon + title + desc। এখানে icon-কে card-এর উপরে center করুন, প্রতিটা card সমান height & padding, hover subtle lift। title-bold, desc-muted। Grid minmax(200px,1fr) ঠিক আছে → 3-5 টা সুন্দরভাবে সাজাবে।

### ৪.৬ Projects (`.projects-grid`)
- **সমস্যা:** ৩টি কার্ড ভালো, কিন্তু `auto-fit minmax(320px,1fr)`-এ page ওঠার পর entire row ভরে কার্ড লম্বা ফাঁকা দেখায়।
- **সমাধান:** প্রজেক্ট কার্ডে **সমতুল্য visual richness** দাও: উপরের project-cat (uppercase small), icon badge, title, desc, tech pills (ছোট rounded), footer-এ result (green check) + Visit button। সব কার্ড **equal height** (flex column, desc flex-grow)। tech-pill-গুলো ছোট consistent rounded (radius 6px) ধরে রাখো।
- Visit button-এ external icon ঠিক রাখো। Grid gap 2rem।

### ৪.৭ Experience (`.timeline` reuse)
- **সমস্যা:** মাত্র ১টা timeline item — section sparse।
- **সমাধান:** Section header-এর পর card কে **প্রশস্ত ও আবদ্ধ** করে দেখাও (max-width ~1000px, centered)। Timeline layout ঠিক, bullet list icon (▹ accent) ধরে রাখো। Internship data (role, org, duration, bullets) চমত্কারভাবে আলাদা করো — timeline-এর line continuous (বাধে না) হবে।

### ৪.৮ Achievements (`.achievements-grid`)
- **সমস্যা:** 
  - ৫টি কার্ডের **রঙ বিক্ষিপ্ত** (নীল, সবুজ, purple, cyan, pink badge + কিছুতে random border-top) — অগোছালো দেখায়।
  - "Qualified for National" ও "Upcoming" আইটেম mixed level।
  - ৪র্থ/৫ম কার্ডে ২টি paragraph (অতিরিক্ত meta)।
- **সমাধান:** 
  - সব badge **uniform**: Gold `🥇 1st` (amber bg), Silver `🥈 2nd` (blue), Bronze `4th` (emerald/neutral), এবং "Qualified/Aspiring" neutral pill। Border-top random গুলো **সব বাদ**।
  - প্রতিটা কার্ডে **তারিখ/status** একরকম meta style।
  - Poor color consistency: শুধুমাত্র badge color-এ medal পার্থক্য।
  - **আরও ভালো:** সবচেয়ে উল্লেখযোগ্য (Divisional 1st / National qualified) কার্ড-কে hero treat (soft primary border) করো, বাকি neutral।

### ৪.৯ Certificates (`.cert-card-enhanced`)
- **সমস্যা:** Section **খুব sparse** — মাত্র ১টি কার্ড max-width 800px-এ, page wide বাকি ফাঁকা। এটা এখানে সবচেয়ে দুর্বল ভিজ্যুয়াল অংশ।
- **সমাধান:**
  - কার্ডটাকে ভালোভাবে present করো — "VERIFIED NATIONAL CREDENTIAL" badge (emerald) + seal icon ঠিক।
  - **মজবুত প্রফেশনাল কার্ড:** top bar (badge + seal) → title → issuer (accent) → ৩টি detail item (Duration / Total Hours / Skill Qualification) grid-এ → centering।
  - **Section heading সামঞ্জস্য:** কার্ডকে center-align/balanced padding দেয়; যাতে sparse না লাগে। যদি (ভবিষ্যতে) আরও certificate যোগ করার জায়গা থাকে, grid-ready markup রাখো (কিন্তু বর্তমানে only visible data)। স্পেস নষ্ট না করে কার্ড বড়/রিচ করো।
  - `max-width: 800px` বজায় রাখা যেতে পারে, কিন্তু container-এ center & ভালো white-space রাখো।

### ৪.১০ Languages (`.language-grid-redesigned`)
- **সমস্যা:** ৩টি কার্ড, প্রতিটা আলাদা gradient progress bar + আলাদা accent color — অসম।
- **সমাধান:**
  - সব কার্ড **একই design**: icon badge + percentage pill (উপর-ডানে) + language name + detail text + **একই primary gradient progress bar** + skill matrix pills (✓/✗)।
  - Percentage pill color: Native=emerald, Fluent=primary cyan/blue, Spoken=amber — semantic level। কিন্তু progress bar সব এক gradient।
  - Grid `minmax(280px,1fr)` ধরে রাখো — desktop-এ ৩টি কার্ড ভালোভাবে বসবে।

### ৪.১১ Contact (`.contact-grid`)
- **সমস্যা:** Left info column + right form card। ছোট spacing/noise।
- **সমাধান:**
  - Contact-info items (email/WhatsApp/address) uniform — icon badge + label(muted) + value। 
  - Address map links (Sylhet & Brahmanbaria) — এই location-map-link-গুলো সামান্য বড় tap target দাও (padding) ও আইকন (cyan/purple) ঠিক।
  - **Form:** label + input consistent (radius 14px, focus ring primary) — বর্তমান ভালো, ধরে রাখো। Submit button full-width primary। Form-এর ভেতরে (উদাহরণ) প্রফেশনাল spacing।
  - `contact-grid` ratio 0.95fr/1.05fr desktop ঠিক, mobile-এ stack (1fr) ঠিক।

### ৪.১২ Footer (`footer`)
- **সমস্যা:** সহজ। 
- **সমাধান:** Social icons center, copyright muted। Footer-এ সামান্য top border + bg-secondary already ঠিক। ভালো padding (3rem) রাখো। মাঝেমাঝে flex column।

---

## ৫. রেসপনসিভ / মোবাইল

- 💡 Mobile (≤992px): hero grid column-এ, avatar উপরে (order -1 ঠিক)।
- ≤768px: nav menu → right drawer (280px), hamburger দেখাবে। Drawer-এ linkগুলো large touch-friendly (`gap 1.75rem`, font-size base)।
- ≤768px: `.btn` full-width — ঠিক আছে। Card padding 1.5rem।
- ≤480px: container padding 1.1rem, avatar 220px।
- **টেস্ট:** 360px / 390px / 768px / 1024px / 1440px-এ কোনও horizontal scroll যেন না হয়, ও text কাটা না যায়।

---

## ৬. অ্যাক্সেসিবিলিটি (A11y)

- Focus state: keyboard user-এর জন্য স্পষ্ট focus ring (primary, `outline`, radius অনুযায়ী) — form inputs ও buttons-এ।
- Toggle buttons (theme/language): hover + focus + (button icon-এ `title` আগে থেকেই আছে — ঠিক রাখো)।
- Color contrast: muted text (`#64748b`) যেন background-এ পড়তে অক্ষম না হয় — প্রয়োজনে মান একটু গাঢ় করো (দরকার পড়লে semantic adjustment)।
- সঠিক `alt` text আছে — ঠিক রাখো।
- বোতাম `min-height` টাচ টার্গেট (48px) ঠিক রাখো।

---

## ৭. পারফরম্যান্স

- ধরে রাখো: font preconnect, `content-visibility: auto` off-screen sections, `translateZ(0)` GPU। 
- নতুন কোনও ভারী image/animation আনা যাবে না। backdrop-filter বেশি pending এড়াও (performance)।
- No new external JS library/CDN.

---

## ৮. যা **না** করবে (Do NOT)

- ❌ কনটেন্ট/টেক্সট/ডেটা change নয় (নাম, তারিখ, GPA, টাইটেল, বর্ণনা, i18n dictionary — সব same)।
- ❌ ফাংশন ভাঙবে না: theme toggle, language toggle, mobile menu, active-section, contact mailto — সব কাজ থাকবে।
- ❌ existing `id` / `data-i18n` / JS-referenced class মুছে ফেলা যাবে না।
- ❌ নতুন framework/library (React, Tailwind CDN, jQuery) নয়। Pure CSS/HTML/JS।
- ❌ অতিরিক্ত/অপ্রয়োজনীয় অ্যানিমেশন নয়। Minimal subtle transition (`0.25s`)।
- ❌ পূর্ণ gradients everywhere — নয়। অপ্রয়োজনীয় রং/বিবিধতা এড়াও।
- ❌ হোভারে বেশি জোর দেওয়া/অস্বাভাবিক disconnect নয়। All hover = subtle lift + glow।

---

## ৯. সাকসেস ক্রাইটেরিয়া (Checklist — "done" কেমন)

- [ ] সব section-এ একরকম design token (radius, padding, shadow, spacing)।
- [ ] কালার নয়েজ কমে গেছে; primary accent + semantic (success/warning/level) মাত্র।
- [ ] গ্রেডিয়েন্ট শুধু ২-৩ জায়গায় (Hero name + primary button)।
- [ ] Achievements ও Languages section এ harmonious (uniform card)।
- [ ] Certificates section আর sparse/ফাঁকা লাগছে না।
- [ ] ডার্ক ও লাইট থিম দুটোতেই সব content readable।
- [ ] EN/BN দুটো ল্যাংগুয়েজ-এ লেআউট ঠিক (Bangla text wrap ভালো)।
- [ ] কোনো horizontal scroll নেই (360px→1440px)।
- [ ] সব বাটন/লিংক কার্যকর, active-nav হাইলাইট কাজ করে।
- [ ] অপ্রয়োজনীয় ইনলাইন style কমিয়ে reusable class-এ আনা হয়েছে।
- [ ] কোনো JS error নেই (console clean)।

---

**আউটপুট প্রত্যাশা:** AI এজেন্ট `index.html`-টি সম্পাদনা করে দেবে (শুধুমাত্র `<style>` ব্লক + framework/html class মার্কআপ), **কনটেন্ট ও ফাংশন অপরিবর্তিত রেখে**। শেষে চেঞ্জের summary দেবে (কোন কোন section কীভাবে বদলেছে)।