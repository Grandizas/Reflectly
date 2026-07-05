<template>
  <div class="landing">
    <!-- NAV -->
    <header class="nav">
      <div class="nav-inner">
        <a href="#top" class="brand">
          <span class="brand-mark"><span class="brand-dot" /></span>
          <span class="brand-name">Reflection</span>
        </a>
        <nav class="nav-links">
          <a href="#how">How it works</a>
          <a href="#insights">Insights</a>
          <a href="#pricing">Pricing</a>
          <a href="#faq">FAQ</a>
        </nav>
        <div class="nav-actions">
          <button class="btn-text">Sign in</button>
          <button class="btn-dark">Get started</button>
        </div>
      </div>
    </header>

    <!-- HERO -->
    <section id="top" class="hero">
      <div class="hero-copy">
        <div class="badge"><span class="badge-dot" />Now with AI reflections</div>
        <h1 class="hero-title">Understand yourself, one reflection at a time.</h1>
        <p class="hero-sub">Reflection helps you capture your thoughts and discover the patterns that quietly improve your life.</p>
        <div class="hero-cta">
          <button class="btn-primary">Start Reflecting</button>
          <a href="#insights" class="btn-outline">
            <svg width="15" height="15" viewBox="0 0 24 24" fill="none"><path d="M6 4l14 8-14 8V4z" fill="#111" /></svg>
            See Demo
          </a>
        </div>
        <div class="hero-meta">
          <span>No credit card</span><span class="meta-dot" /><span>Private by design</span><span class="meta-dot" /><span>2 min a day</span>
        </div>
      </div>
      <div class="hero-visual">
        <ReflectionOrb />
      </div>
    </section>

    <!-- TRUST -->
    <div class="trust">
      <span>4.9 ★ App Store</span><span>Featured on Product Hunt</span><span>120k reflections written</span>
    </div>

    <!-- HOW IT WORKS -->
    <section id="how" class="section wrap">
      <div class="section-head center">
        <div class="eyebrow">How it works</div>
        <h2 class="h2 narrow">Three quiet minutes. A clearer mind.</h2>
      </div>
      <div class="grid-3">
        <div v-for="s in steps" :key="s.n" class="step-card">
          <div class="step-num">{{ s.n }}</div>
          <div class="step-title">{{ s.title }}</div>
          <div class="step-body">{{ s.body }}</div>
        </div>
      </div>
    </section>

    <!-- AI INSIGHTS -->
    <section id="insights" class="band">
      <div class="wrap feature-2col">
        <div>
          <div class="eyebrow">AI Insights</div>
          <h2 class="h2">Patterns you'd never notice on your own.</h2>
          <p class="lead">Reflection reads gently between the lines of your entries and surfaces the connections that shape how you feel — no dashboards to configure, no numbers to crunch.</p>
          <div class="checklist">
            <div v-for="p in aiPoints" :key="p" class="check-item">
              <span class="check-badge">
                <svg width="11" height="11" viewBox="0 0 24 24" fill="none"><path d="M5 13l4 4L19 7" stroke="#6366F1" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" /></svg>
              </span>{{ p }}
            </div>
          </div>
        </div>
        <div class="reflection-card">
          <div class="reflection-label">
            <svg width="15" height="15" viewBox="0 0 24 24" fill="none"><path d="M12 3l1.9 5.1L19 10l-5.1 1.9L12 17l-1.9-5.1L5 10l5.1-1.9L12 3z" fill="#6366F1" /></svg>
            This week's reflection
          </div>
          <div class="reflection-quote">"Your happiest days almost always follow a morning walk. On the three days you skipped it, your gratitude notes were noticeably shorter."</div>
          <div class="tag-row">
            <span class="tag">movement</span>
            <span class="tag">gratitude</span>
            <span class="tag">mornings</span>
          </div>
        </div>
      </div>
    </section>

    <!-- FEATURE ROWS -->
    <section class="wrap section grid-2">
      <div class="feature-panel">
        <div class="eyebrow">Daily Reflection</div>
        <h3 class="h3">A calm, guided space</h3>
        <p class="panel-lead">Five thoughtful prompts, one soft page. No streak pressure, no gamified noise — just room to think.</p>
        <div class="prompt-box">
          <div class="prompt-q">What made today meaningful?</div>
          <div class="prompt-a">Slow coffee before anyone woke up, and finishing the chapter I'd been avoiding.</div>
        </div>
      </div>
      <div class="feature-panel">
        <div class="eyebrow">Long-term Patterns</div>
        <h3 class="h3">Watch yourself grow</h3>
        <p class="panel-lead">Months of small entries become a quiet map of your moods, habits, and the things that keep you well.</p>
        <div class="bars">
          <div v-for="(b, i) in miniBars" :key="i" class="bar" :style="{ background: b.c, height: b.h }" />
        </div>
      </div>
    </section>

    <!-- TESTIMONIALS -->
    <section class="band">
      <div class="wrap section-inner">
        <div class="section-head center">
          <div class="eyebrow">Loved every evening</div>
          <h2 class="h2">The gentlest part of my day.</h2>
        </div>
        <div class="grid-3">
          <div v-for="t in testimonials" :key="t.name" class="testimonial">
            <div class="testimonial-quote">"{{ t.quote }}"</div>
            <div class="testimonial-author">
              <div class="avatar" :style="{ background: t.c }">{{ t.initial }}</div>
              <div>
                <div class="author-name">{{ t.name }}</div>
                <div class="author-role">{{ t.role }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- PRICING -->
    <section id="pricing" class="wrap section">
      <div class="section-head center">
        <div class="eyebrow">Pricing</div>
        <h2 class="h2">Start free. Upgrade when it clicks.</h2>
      </div>
      <div class="grid-3 pricing">
        <div
          v-for="p in plans"
          :key="p.name"
          class="plan"
          :style="{ background: p.bg, border: '1px solid ' + p.border, boxShadow: p.shadow }"
        >
          <div v-if="p.featured" class="plan-badge">Popular</div>
          <div class="plan-name" :style="{ color: p.nameC }">{{ p.name }}</div>
          <div class="plan-price">
            <span class="price-amount" :style="{ color: p.priceC }">{{ p.price }}</span>
            <span class="price-per" :style="{ color: p.subC }">{{ p.per }}</span>
          </div>
          <div class="plan-tag" :style="{ color: p.subC }">{{ p.tag }}</div>
          <button
            class="plan-btn"
            :style="{ background: p.btnBg, color: p.btnC, border: '1px solid ' + p.btnBorder }"
          >{{ p.cta }}</button>
          <div class="plan-feats">
            <div v-for="f in p.feats" :key="f" class="plan-feat" :style="{ color: p.featC }">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M5 13l4 4L19 7" :stroke="p.check" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" /></svg>
              {{ f }}
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ -->
    <section id="faq" class="wrap faq-wrap">
      <div class="section-head center">
        <h2 class="h2 sm">Questions, answered.</h2>
      </div>
      <div class="faq-list">
        <div v-for="(f, i) in faqs" :key="f.q" class="faq-item">
          <button class="faq-q" @click="toggleFaq(i)">
            {{ f.q }}
            <span class="faq-icon" :style="{ transform: f.open ? 'rotate(45deg)' : 'rotate(0deg)' }">+</span>
          </button>
          <div v-if="f.open" class="faq-a">{{ f.a }}</div>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section class="wrap cta-wrap">
      <div class="cta">
        <div class="cta-glow" />
        <div class="cta-inner">
          <h2 class="cta-title">Meet yourself this evening.</h2>
          <p class="cta-sub">Your first reflection takes two minutes. The clarity lasts longer.</p>
          <button class="btn-light">Start Reflecting</button>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="footer-inner">
        <div class="brand">
          <span class="brand-mark sm"><span class="brand-dot" /></span>
          <span class="brand-name">Reflection</span>
        </div>
        <div class="footer-links"><span>Privacy</span><span>Terms</span><span>Blog</span><span>Contact</span></div>
        <div class="footer-copy">© 2026 Reflection Labs</div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

useHead({
  title: 'Reflection — Understand yourself, one reflection at a time',
  link: [
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' },
    {
      rel: 'stylesheet',
      href: 'https://fonts.googleapis.com/css2?family=Hanken+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap',
    },
  ],
})

const steps = [
  { n: '01', title: 'Write for two minutes', body: 'Five soft prompts guide you. No blank page, no pressure to be profound.' },
  { n: '02', title: 'Let the AI notice', body: 'Reflection quietly reads your entries and finds the threads between them.' },
  { n: '03', title: 'See yourself clearly', body: 'Patterns, moods, and gentle observations surface over the weeks and months.' },
]

const aiPoints = [
  'Connects moods to your habits automatically',
  'Weekly and monthly written reflections',
  'Nothing to configure — it just listens',
]

const miniBars = [40, 55, 48, 66, 60, 74, 68, 82, 76, 88, 80, 94].map((h, i) => ({
  h: h + '%',
  c: i > 7 ? '#6366F1' : '#C3C7F7',
}))

const testimonials = [
  { quote: 'The first app I actually open every night. It feels like it respects my attention.', name: 'Maya R.', role: 'Product designer', c: '#6366F1', initial: 'M' },
  { quote: 'It told me my best days follow a morning walk. I didn’t believe it — then I checked.', name: 'Daniel K.', role: 'Founder', c: '#22A06B', initial: 'D' },
  { quote: 'Calm, quiet, and beautiful. It never once made me feel behind.', name: 'Sofia L.', role: 'Therapist', c: '#8B5CF6', initial: 'S' },
]

interface Plan {
  name: string
  nameC: string
  price: string
  per: string
  tag: string
  cta: string
  featured: boolean
  bg: string
  border: string
  shadow: string
  priceC: string
  subC: string
  btnBg: string
  btnC: string
  btnBorder: string
  featC: string
  check: string
  feats: string[]
}

const plans: Plan[] = [
  {
    name: 'Free', nameC: '#111', price: '$0', per: '', tag: 'For getting started', cta: 'Start free', featured: false,
    bg: '#fff', border: '#F0F0F2', shadow: '0 1px 3px rgba(17,17,17,.03)', priceC: '#111', subC: '#9A9AA2',
    btnBg: '#fff', btnC: '#111', btnBorder: '#E6E6E9', featC: '#6B6B72', check: '#9A9AA2',
    feats: ['Daily guided reflection', '7 days of history', 'Basic mood tracking'],
  },
  {
    name: 'Pro', nameC: '#4F46E5', price: '$8', per: '/mo', tag: 'For the daily reflector', cta: 'Start Pro', featured: true,
    bg: '#fff', border: '#C7C9F9', shadow: '0 20px 50px -24px rgba(99,102,241,.35)', priceC: '#111', subC: '#9A9AA2',
    btnBg: '#6366F1', btnC: '#fff', btnBorder: '#6366F1', featC: '#3F3F46', check: '#6366F1',
    feats: ['Everything in Free', 'Unlimited history', 'AI insights & weekly summaries', 'Mood trends & patterns'],
  },
  {
    name: 'Premium', nameC: '#111', price: '$16', per: '/mo', tag: 'For going deeper', cta: 'Start Premium', featured: false,
    bg: '#fff', border: '#F0F0F2', shadow: '0 1px 3px rgba(17,17,17,.03)', priceC: '#111', subC: '#9A9AA2',
    btnBg: '#fff', btnC: '#111', btnBorder: '#E6E6E9', featC: '#6B6B72', check: '#9A9AA2',
    feats: ['Everything in Pro', 'Monthly AI observations', 'Goal tracking', 'Export & backup'],
  },
]

const faqs = ref([
  { q: 'Is my writing private?', a: 'Completely. Your entries are end-to-end encrypted by default — not even we can read them.', open: true },
  { q: 'Do I have to write every day?', a: 'Never. Reflection is designed to be gentle. Write when it helps; skip when it doesn’t. No guilt, no broken-streak shaming.', open: false },
  { q: 'How does the AI work?', a: 'It reads only your own entries to surface patterns and write short summaries. It never trains on your data or shares it.', open: false },
  { q: 'Can I export my reflections?', a: 'Yes. On Premium you can export everything as a beautiful PDF or plain text, any time.', open: false },
])

function toggleFaq(i: number) {
  if (!faqs.value[i]) return;
  const wasOpen = faqs.value[i].open
  faqs.value.forEach((f) => (f.open = false))
  faqs.value[i].open = !wasOpen
}
</script>

<style scoped>
.landing {
  --ink: #111111;
  --muted: #6b6b72;
  --muted2: #9a9aa2;
  --indigo: #6366f1;
  --line: #f0f0f2;
  --line2: #ececee;
  min-height: 100vh;
  background: #ffffff;
  color: var(--ink);
  font-family: 'Hanken Grotesk', -apple-system, system-ui, sans-serif;
  -webkit-font-smoothing: antialiased;
}
.wrap {
  max-width: 1160px;
  margin: 0 auto;
  padding-left: 32px;
  padding-right: 32px;
}

/* NAV */
.nav {
  position: sticky;
  top: 0;
  z-index: 50;
  backdrop-filter: blur(14px);
  background: rgba(255, 255, 255, 0.72);
  border-bottom: 1px solid var(--line);
}
.nav-inner {
  max-width: 1160px;
  margin: 0 auto;
  padding: 0 32px;
  height: 68px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.brand {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  color: var(--ink);
}
.brand-mark {
  width: 24px;
  height: 24px;
  border-radius: 8px;
  background: var(--indigo);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(99, 102, 241, 0.35);
}
.brand-mark.sm {
  width: 22px;
  height: 22px;
  border-radius: 7px;
}
.brand-dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: #fff;
}
.brand-name {
  font-size: 17px;
  font-weight: 600;
  letter-spacing: -0.02em;
}
.nav-links {
  display: flex;
  align-items: center;
  gap: 34px;
  font-size: 14.5px;
  color: var(--muted);
  font-weight: 500;
}
.nav-links a {
  color: inherit;
  text-decoration: none;
  cursor: pointer;
}
.nav-links a:hover {
  color: var(--ink);
}
.nav-actions {
  display: flex;
  align-items: center;
  gap: 16px;
}
.btn-text {
  background: none;
  border: none;
  font-size: 14.5px;
  font-weight: 500;
  color: var(--ink);
  cursor: pointer;
}
.btn-dark {
  background: var(--ink);
  color: #fff;
  border: none;
  font-size: 14.5px;
  font-weight: 500;
  padding: 9px 18px;
  border-radius: 11px;
  cursor: pointer;
}

/* HERO */
.hero {
  max-width: 1160px;
  margin: 0 auto;
  padding: 96px 32px 40px;
  display: grid;
  grid-template-columns: 1.05fr 0.95fr;
  gap: 48px;
  align-items: center;
}
.hero-copy {
  animation: rflFade 0.8s ease both;
}
.badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 12px;
  border: 1px solid var(--line2);
  border-radius: 999px;
  font-size: 13px;
  color: var(--muted);
  font-weight: 500;
  margin-bottom: 28px;
}
.badge-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--indigo);
}
.hero-title {
  font-size: 60px;
  line-height: 1.04;
  letter-spacing: -0.035em;
  font-weight: 600;
  margin: 0 0 22px;
  max-width: 12ch;
}
.hero-sub {
  font-size: 19px;
  line-height: 1.55;
  color: var(--muted);
  margin: 0 0 36px;
  max-width: 44ch;
}
.hero-cta {
  display: flex;
  gap: 14px;
  align-items: center;
}
.btn-primary {
  background: var(--indigo);
  color: #fff;
  border: none;
  font-size: 15.5px;
  font-weight: 600;
  padding: 14px 26px;
  border-radius: 13px;
  box-shadow: 0 6px 18px rgba(99, 102, 241, 0.32);
  cursor: pointer;
}
.btn-outline {
  background: #fff;
  color: var(--ink);
  border: 1px solid #e6e6e9;
  font-size: 15.5px;
  font-weight: 600;
  padding: 14px 24px;
  border-radius: 13px;
  display: flex;
  align-items: center;
  gap: 9px;
  text-decoration: none;
  cursor: pointer;
}
.hero-meta {
  display: flex;
  align-items: center;
  gap: 22px;
  margin-top: 44px;
  color: var(--muted2);
  font-size: 13.5px;
  flex-wrap: wrap;
}
.meta-dot {
  width: 3px;
  height: 3px;
  border-radius: 50%;
  background: #d4d4d8;
}
.hero-visual {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* TRUST */
.trust {
  max-width: 1160px;
  margin: 0 auto;
  padding: 24px 32px 90px;
  display: flex;
  justify-content: center;
  gap: 44px;
  color: #c4c4cb;
  font-size: 14px;
  font-weight: 600;
  flex-wrap: wrap;
}

/* SECTIONS */
.section {
  padding-top: 0;
  padding-bottom: 100px;
}
.section-head {
  margin-bottom: 56px;
}
.section-head.center {
  text-align: center;
}
.eyebrow {
  font-size: 13px;
  font-weight: 600;
  color: var(--indigo);
  letter-spacing: 0.06em;
  text-transform: uppercase;
  margin-bottom: 14px;
}
.h2 {
  font-size: 40px;
  letter-spacing: -0.03em;
  font-weight: 600;
  margin: 0 auto;
  line-height: 1.1;
}
.h2.narrow {
  max-width: 16ch;
}
.h2.sm {
  font-size: 34px;
}
.h3 {
  font-size: 26px;
  letter-spacing: -0.02em;
  font-weight: 600;
  margin: 0 0 12px;
}

.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
.grid-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

/* STEPS */
.step-card {
  background: #fafafa;
  border: 1px solid var(--line);
  border-radius: 16px;
  padding: 30px;
}
.step-num {
  width: 38px;
  height: 38px;
  border-radius: 11px;
  background: #fff;
  border: 1px solid var(--line2);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  color: var(--indigo);
  margin-bottom: 22px;
}
.step-title {
  font-size: 18px;
  font-weight: 600;
  letter-spacing: -0.01em;
  margin-bottom: 8px;
}
.step-body {
  font-size: 14.5px;
  line-height: 1.55;
  color: var(--muted);
}

/* BAND */
.band {
  background: #fafafa;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
}
.section-inner {
  padding-top: 100px;
  padding-bottom: 100px;
}
.feature-2col {
  padding-top: 100px;
  padding-bottom: 100px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}
.lead {
  font-size: 17px;
  line-height: 1.6;
  color: var(--muted);
  margin: 0 0 28px;
  max-width: 42ch;
}
.checklist {
  display: flex;
  flex-direction: column;
  gap: 14px;
}
.check-item {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 15px;
  color: var(--ink);
}
.check-badge {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #eef0fe;
  display: flex;
  align-items: center;
  justify-content: center;
  flex: none;
}
.reflection-card {
  background: #fff;
  border: 1px solid var(--line2);
  border-radius: 18px;
  padding: 26px;
  box-shadow: 0 1px 3px rgba(17, 17, 17, 0.04), 0 20px 50px -24px rgba(17, 17, 17, 0.16);
}
.reflection-label {
  display: flex;
  align-items: center;
  gap: 9px;
  margin-bottom: 20px;
  color: var(--indigo);
  font-size: 13px;
  font-weight: 600;
}
.reflection-quote {
  font-size: 20px;
  line-height: 1.45;
  font-weight: 500;
  letter-spacing: -0.01em;
  color: var(--ink);
}
.tag-row {
  display: flex;
  gap: 8px;
  margin-top: 22px;
  flex-wrap: wrap;
}
.tag {
  font-size: 12.5px;
  color: var(--muted);
  background: #fafafa;
  border: 1px solid var(--line);
  padding: 5px 11px;
  border-radius: 999px;
}

/* FEATURE PANELS */
.grid-2 {
  padding-top: 100px;
}
.feature-panel {
  background: #fff;
  border: 1px solid var(--line);
  border-radius: 18px;
  padding: 38px;
  box-shadow: 0 1px 3px rgba(17, 17, 17, 0.03);
}
.panel-lead {
  font-size: 15.5px;
  line-height: 1.6;
  color: var(--muted);
  margin: 0 0 26px;
}
.prompt-box {
  border: 1px solid var(--line);
  border-radius: 14px;
  padding: 20px;
  background: #fafafa;
}
.prompt-q {
  font-size: 13px;
  color: var(--muted2);
  margin-bottom: 8px;
}
.prompt-a {
  font-size: 15px;
  color: var(--ink);
  line-height: 1.5;
}
.bars {
  display: flex;
  align-items: flex-end;
  gap: 6px;
  height: 96px;
  padding: 0 2px;
}
.bar {
  flex: 1;
  border-radius: 5px 5px 3px 3px;
}

/* TESTIMONIALS */
.testimonial {
  background: #fff;
  border: 1px solid var(--line);
  border-radius: 16px;
  padding: 28px;
}
.testimonial-quote {
  font-size: 16px;
  line-height: 1.55;
  color: #222;
  margin-bottom: 22px;
  letter-spacing: -0.01em;
}
.testimonial-author {
  display: flex;
  align-items: center;
  gap: 12px;
}
.avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 14px;
  font-weight: 600;
}
.author-name {
  font-size: 14px;
  font-weight: 600;
}
.author-role {
  font-size: 13px;
  color: var(--muted2);
}

/* PRICING */
.pricing {
  align-items: start;
}
.plan {
  border-radius: 18px;
  padding: 32px;
  position: relative;
}
.plan-badge {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 11.5px;
  font-weight: 600;
  color: #fff;
  background: var(--indigo);
  padding: 4px 10px;
  border-radius: 999px;
}
.plan-name {
  font-size: 15px;
  font-weight: 600;
  margin-bottom: 6px;
}
.plan-price {
  display: flex;
  align-items: baseline;
  gap: 4px;
  margin-bottom: 6px;
}
.price-amount {
  font-size: 40px;
  font-weight: 600;
  letter-spacing: -0.03em;
}
.price-per {
  font-size: 14px;
}
.plan-tag {
  font-size: 14px;
  margin-bottom: 24px;
}
.plan-btn {
  width: 100%;
  border-radius: 12px;
  padding: 12px;
  font-size: 14.5px;
  font-weight: 600;
  margin-bottom: 24px;
  cursor: pointer;
}
.plan-feats {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.plan-feat {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 14px;
}

/* FAQ */
.faq-wrap {
  max-width: 760px;
  margin: 0 auto;
  padding-top: 40px;
  padding-bottom: 110px;
}
.faq-wrap .section-head {
  margin-bottom: 44px;
}
.faq-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.faq-item {
  border: 1px solid var(--line);
  border-radius: 14px;
  background: #fff;
  overflow: hidden;
}
.faq-q {
  width: 100%;
  background: none;
  border: none;
  text-align: left;
  padding: 20px 22px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  font-weight: 500;
  color: var(--ink);
  cursor: pointer;
}
.faq-icon {
  color: var(--muted2);
  font-size: 20px;
  transition: transform 0.2s;
}
.faq-a {
  padding: 0 22px 22px;
  font-size: 15px;
  line-height: 1.6;
  color: var(--muted);
}

/* CTA */
.cta-wrap {
  margin-bottom: 90px;
}
.cta {
  background: var(--ink);
  border-radius: 24px;
  padding: 64px 40px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.cta-glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(60% 120% at 50% -10%, rgba(99, 102, 241, 0.35), transparent 60%);
}
.cta-inner {
  position: relative;
}
.cta-title {
  font-size: 38px;
  letter-spacing: -0.03em;
  font-weight: 600;
  margin: 0 0 14px;
  color: #fff;
}
.cta-sub {
  font-size: 17px;
  color: rgba(255, 255, 255, 0.6);
  margin: 0 0 30px;
}
.btn-light {
  background: #fff;
  color: var(--ink);
  border: none;
  font-size: 15.5px;
  font-weight: 600;
  padding: 14px 28px;
  border-radius: 13px;
  cursor: pointer;
}

/* FOOTER */
.footer {
  border-top: 1px solid var(--line);
}
.footer-inner {
  max-width: 1160px;
  margin: 0 auto;
  padding: 44px 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}
.footer-links {
  display: flex;
  gap: 28px;
  font-size: 14px;
  color: var(--muted);
}
.footer-copy {
  font-size: 13.5px;
  color: #b4b4bb;
}

@keyframes rflFade {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* RESPONSIVE */
@media (max-width: 900px) {
  .hero {
    grid-template-columns: 1fr;
    padding-top: 64px;
    text-align: center;
  }
  .hero-title {
    font-size: 42px;
    max-width: none;
  }
  .hero-sub {
    max-width: none;
  }
  .hero-cta,
  .hero-meta,
  .badge {
    justify-content: center;
  }
  .hero-visual {
    order: -1;
  }
  .feature-2col,
  .grid-3,
  .grid-2 {
    grid-template-columns: 1fr;
  }
  .nav-links {
    display: none;
  }
  .h2 {
    font-size: 30px;
  }
}
@media (max-width: 520px) {
  .wrap,
  .nav-inner,
  .hero,
  .trust,
  .footer-inner {
    padding-left: 20px;
    padding-right: 20px;
  }
  .cta {
    padding: 44px 24px;
  }
}
</style>
