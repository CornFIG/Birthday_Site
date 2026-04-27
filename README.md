<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>🎂 Happy Birthday!</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />

<style>
/* ============================================================
   BIRTHDAY APP — Pastel Blue Theme
   ============================================================ */

/* ── CSS Variables ── */
:root {
  --blue:        #90c8f0;
  --blue-deep:   #4a9fd4;
  --blue-dark:   #2d7bb5;
  --sky:         #daeeff;
  --ice:         #eef7ff;
  --periwinkle:  #b8d4f5;
  --mint:        #c8eef5;
  --gold:        #7ec8e3;
  --gold-light:  #b3e5f7;
  --cream:       #f0f8ff;
  --white:       #ffffff;
  --text-dark:   #1a3a52;
  --text-mid:    #4a7a9b;
  --text-light:  #8bb8d4;
  --shadow-sm:   0 4px 16px rgba(74,159,212,0.14);
  --shadow-md:   0 8px 32px rgba(74,159,212,0.2);
  --shadow-lg:   0 16px 48px rgba(74,159,212,0.26);
  --radius-sm:   12px;
  --radius-md:   20px;
  --radius-lg:   32px;
  --duration:    0.55s;
  --ease:        cubic-bezier(0.4, 0, 0.2, 1);
}

/* ── Reset & Base ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--cream);
  color: var(--text-dark);
  min-height: 100vh;
  overflow-x: hidden;
  background-image:
    radial-gradient(circle at 80% 10%, rgba(144,200,240,0.22) 0%, transparent 50%),
    radial-gradient(circle at 10% 90%, rgba(126,200,227,0.15) 0%, transparent 50%),
    radial-gradient(var(--periwinkle) 1px, transparent 1px);
  background-size: 100% 100%, 100% 100%, 28px 28px;
}

/* ── App (SPA container) ── */
.app { position: relative; width: 100%; min-height: 100vh; }

/* ── Pages ── */
.page {
  display: none;
  width: 100%;
  min-height: 100vh;
  padding: 80px 16px 100px;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity var(--duration) var(--ease), transform var(--duration) var(--ease);
}

.page.active {
  display: flex;
  opacity: 1;
  transform: translateY(0);
}

.page.exit {
  opacity: 0;
  transform: translateY(-30px);
}

.page-inner {
  width: 100%;
  max-width: 680px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 28px;
}

/* ── Animate-in helpers ── */
.animate-in {
  opacity: 0;
  transform: translateY(22px);
  transition: opacity 0.6s var(--ease), transform 0.6s var(--ease);
}
.page.active .animate-in { opacity: 1; transform: translateY(0); }
.page.active .delay-1    { transition-delay: 0.12s; }
.page.active .delay-2    { transition-delay: 0.24s; }
.page.active .delay-3    { transition-delay: 0.36s; }

/* ── Navigation dots ── */
.nav-dots {
  position: fixed;
  top: 50%;
  right: 18px;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 10px;
  z-index: 200;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 2px solid var(--blue);
  background: transparent;
  cursor: pointer;
  transition: background 0.3s, transform 0.3s;
  padding: 0;
}

.dot.active {
  background: var(--blue-deep);
  transform: scale(1.4);
}

/* ── Music button ── */
.music-btn {
  position: fixed;
  top: 18px;
  left: 18px;
  z-index: 200;
  background: var(--white);
  border: none;
  border-radius: 50%;
  width: 42px;
  height: 42px;
  font-size: 18px;
  box-shadow: var(--shadow-sm);
  cursor: pointer;
  transition: transform 0.2s;
}
.music-btn:hover { transform: scale(1.12); }

/* ── Page header ── */
.page-header { text-align: center; }

.tag {
  display: inline-block;
  background: linear-gradient(135deg, var(--blue), var(--gold-light));
  color: var(--white);
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  padding: 5px 16px;
  border-radius: 100px;
  margin-bottom: 14px;
  box-shadow: var(--shadow-sm);
}

.title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.2rem, 6vw, 3.4rem);
  font-weight: 700;
  line-height: 1.15;
  color: var(--text-dark);
}

.title em {
  font-style: italic;
  color: var(--blue-deep);
}

/* ── Balloons ── */
.balloons {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  overflow: hidden;
  z-index: 0;
}

.balloon {
  position: absolute;
  font-size: clamp(1.6rem, 4vw, 2.8rem);
  animation: floatBalloon 8s ease-in-out infinite;
  opacity: 0.5;
}
.b1 { left: 5%;  animation-delay: 0s;   animation-duration: 9s; }
.b2 { left: 88%; animation-delay: 3s;   animation-duration: 7s; }
.b3 { left: 50%; animation-delay: 5.5s; animation-duration: 10s; }

@keyframes floatBalloon {
  0%   { transform: translateY(100vh); opacity: 0; }
  10%  { opacity: 0.5; }
  90%  { opacity: 0.5; }
  100% { transform: translateY(-120px); opacity: 0; }
}

/* ── Photo Grid ── */
.photo-grid {
  display: grid;
  width: 100%;
  gap: 12px;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 180px 140px;
}

.photo-card {
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-md);
  transition: transform 0.3s var(--ease), box-shadow 0.3s var(--ease);
  cursor: pointer;
}

.photo-card:hover {
  transform: translateY(-4px) scale(1.02);
  box-shadow: var(--shadow-lg);
}

.photo-main        { grid-column: 1; grid-row: 1 / 3; }
.photo-side-top    { grid-column: 2; grid-row: 1; }
.photo-side-bottom { grid-column: 2; grid-row: 2; }

.photo-placeholder {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, var(--sky), var(--mint));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 6px;
  border: 2px dashed var(--blue);
}

.photo-icon { font-size: 2rem; }

.photo-placeholder p {
  font-size: 0.68rem;
  color: var(--text-light);
  text-align: center;
  padding: 0 8px;
  font-family: monospace;
}

.photo-card img { width: 100%; height: 100%; object-fit: cover; display: block; }

/* ── Message Card ── */
.message-card {
  background: var(--white);
  border-radius: var(--radius-lg);
  padding: 32px 28px 28px;
  box-shadow: var(--shadow-md);
  position: relative;
  text-align: center;
  width: 100%;
  border: 1px solid rgba(144,200,240,0.35);
}

.quote-mark {
  font-family: 'Playfair Display', serif;
  font-size: 6rem;
  color: var(--blue);
  line-height: 0.5;
  position: absolute;
  top: 18px; left: 22px;
  opacity: 0.25;
}

.message-text {
  font-size: 1.05rem;
  line-height: 1.75;
  color: var(--text-mid);
  position: relative;
  z-index: 1;
}

.message-signature {
  margin-top: 16px;
  font-size: 0.88rem;
  color: var(--blue-deep);
  font-style: italic;
}

/* ── Buttons ── */
.btn-next, .btn-prev {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 32px;
  border-radius: 100px;
  border: none;
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: transform 0.25s var(--ease), box-shadow 0.25s var(--ease);
}

.btn-next {
  background: linear-gradient(135deg, var(--blue-deep), var(--blue-dark));
  color: var(--white);
  box-shadow: 0 4px 20px rgba(74,159,212,0.38);
}

.btn-next:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 28px rgba(74,159,212,0.5);
}

.btn-prev {
  background: var(--white);
  color: var(--text-mid);
  box-shadow: var(--shadow-sm);
  border: 1px solid rgba(144,200,240,0.45);
}

.btn-prev:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.nav-btns {
  display: flex;
  gap: 14px;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}

.arrow { display: inline-block; transition: transform 0.2s; }
.btn-next:hover .arrow { transform: translateX(4px); }

/* ── Video Page ── */
.video-wrapper {
  position: relative;
  width: 100%;
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-lg);
  background: #0a1a2e;
  aspect-ratio: 16 / 9;
}

.video-wrapper video,
.video-wrapper iframe {
  width: 100%;
  height: 100%;
  display: block;
  border-radius: var(--radius-lg);
}

.video-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, rgba(144,200,240,0.9), rgba(74,159,212,0.85));
  cursor: pointer;
  transition: opacity 0.4s var(--ease);
  z-index: 10;
  border-radius: var(--radius-lg);
}

.video-overlay.hidden { opacity: 0; pointer-events: none; }

.play-btn-circle {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  background: var(--white);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 0 12px rgba(255,255,255,0.22);
  animation: pulsePulse 1.8s ease-in-out infinite;
  transition: transform 0.2s;
}

.play-btn-circle:hover { transform: scale(1.1); }

.play-icon {
  font-size: 1.6rem;
  margin-left: 5px;
  color: var(--blue-deep);
}

.video-hint {
  color: var(--white);
  font-size: 0.85rem;
  margin-top: 16px;
  font-weight: 500;
  letter-spacing: 0.04em;
}

@keyframes pulsePulse {
  0%,100% { box-shadow: 0 0 0 12px rgba(255,255,255,0.22); }
  50%      { box-shadow: 0 0 0 22px rgba(255,255,255,0.08); }
}

.video-caption {
  color: var(--text-mid);
  font-size: 0.92rem;
  text-align: center;
  font-style: italic;
}

/* ── Gift / Present Page ── */
.gift-stage {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  min-height: 260px;
}

.gift-box {
  position: relative;
  width: 200px;
  height: 200px;
  cursor: pointer;
  user-select: none;
  transition: transform 0.3s var(--ease);
}

.gift-box:hover { transform: scale(1.04) rotate(-1deg); }

/* Wrapped state */
.gift-wrapped {
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, var(--blue), var(--blue-deep));
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  overflow: hidden;
  transition: opacity 0.4s var(--ease), transform 0.4s var(--ease);
}

.gift-box.unwrapped .gift-wrapped {
  opacity: 0;
  transform: scale(0.8) rotate(8deg);
  pointer-events: none;
}

.gift-ribbon-h, .gift-ribbon-v {
  position: absolute;
  background: var(--white);
  opacity: 0.6;
}
.gift-ribbon-h { left: 0; right: 0; height: 14px; top: 50%; transform: translateY(-50%); }
.gift-ribbon-v { top: 0; bottom: 0; width: 14px; left: 50%; transform: translateX(-50%); }

.gift-bow {
  font-size: 3rem;
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  filter: drop-shadow(0 2px 4px rgba(0,0,0,0.15));
  animation: bounceBow 2s ease-in-out infinite;
}

@keyframes bounceBow {
  0%,100% { transform: translateX(-50%) translateY(0); }
  50%      { transform: translateX(-50%) translateY(-8px); }
}

.gift-shine {
  position: absolute;
  top: -30%; left: -30%;
  width: 60%; height: 60%;
  background: rgba(255,255,255,0.2);
  border-radius: 50%;
  filter: blur(18px);
}

.gift-tap-hint {
  color: rgba(255,255,255,0.88);
  font-size: 0.78rem;
  position: absolute;
  bottom: 14px;
  font-weight: 500;
  letter-spacing: 0.04em;
}

/* Unwrapped state */
.gift-unwrapped {
  position: absolute;
  inset: 0;
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-lg);
  opacity: 0;
  transform: scale(0.7) rotate(-8deg);
  transition: opacity 0.5s 0.15s var(--ease), transform 0.5s 0.15s var(--ease);
  pointer-events: none;
}

.gift-box.unwrapped .gift-unwrapped {
  opacity: 1;
  transform: scale(1) rotate(0deg);
  pointer-events: auto;
}

.gift-image-placeholder {
  width: 100%; height: 100%;
  background: linear-gradient(135deg, var(--ice), var(--mint));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border: 2px dashed var(--blue);
  border-radius: var(--radius-lg);
}

.gift-img-icon { font-size: 3rem; }
.gift-img-label {
  font-size: 0.7rem;
  color: var(--text-light);
  font-family: monospace;
  text-align: center;
  padding: 0 10px;
}

.gift-img { width: 100%; height: 100%; object-fit: cover; display: block; }

/* Sparkle ring */
.sparkle-ring {
  position: absolute;
  width: 220px; height: 220px;
  border-radius: 50%;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.4s;
}

.sparkle-ring.active {
  opacity: 1;
  animation: sparkleRingSpin 1.5s linear infinite;
  background: conic-gradient(
    var(--gold-light), var(--blue), var(--mint), var(--gold-light)
  );
  -webkit-mask: radial-gradient(circle, transparent 90px, black 91px, black 100%, transparent 101%);
  mask: radial-gradient(circle, transparent 90px, black 91px, black 100%, transparent 101%);
}

@keyframes sparkleRingSpin { to { transform: rotate(360deg); } }

.gift-message {
  background: var(--white);
  border-radius: var(--radius-md);
  padding: 20px 28px;
  box-shadow: var(--shadow-sm);
  text-align: center;
  color: var(--text-mid);
  font-size: 1rem;
  line-height: 1.65;
  width: 100%;
  border: 1px solid rgba(144,200,240,0.3);
  font-style: italic;
}

/* ── Surprise / Interactive Page ── */
.surprise-reveal {
  width: 100%;
  min-height: 160px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.surprise-lock {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  transition: opacity 0.4s, transform 0.4s;
}

.surprise-lock.hidden {
  opacity: 0;
  transform: scale(0.8);
  pointer-events: none;
  display: none;
}

.lock-icon {
  font-size: 3.5rem;
  animation: rockGently 3s ease-in-out infinite;
}

@keyframes rockGently {
  0%,100% { transform: rotate(-5deg); }
  50%      { transform: rotate(5deg); }
}

.lock-hint { color: var(--text-light); font-size: 0.88rem; text-align: center; }

.surprise-message {
  display: none;
  flex-direction: column;
  align-items: center;
  gap: 16px;
  text-align: center;
  width: 100%;
  animation: popIn 0.5s var(--ease);
}

.surprise-message.visible { display: flex; }

.surprise-emoji { font-size: 3.5rem; animation: bounceStar 1s ease-in-out infinite; }

@keyframes bounceStar {
  0%,100% { transform: scale(1); }
  50%      { transform: scale(1.18); }
}

.surprise-text {
  background: var(--white);
  border-radius: var(--radius-lg);
  padding: 28px 32px;
  box-shadow: var(--shadow-lg);
  font-size: 1.08rem;
  line-height: 1.7;
  color: var(--text-mid);
  border: 2px solid var(--blue);
  width: 100%;
}

@keyframes popIn {
  0%   { opacity: 0; transform: scale(0.6) rotate(-5deg); }
  100% { opacity: 1; transform: scale(1)   rotate(0deg); }
}

/* Confetti Button */
.btn-confetti {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: linear-gradient(135deg, var(--blue-dark), var(--blue-deep), var(--blue));
  background-size: 200% 200%;
  animation: gradientShift 3s ease infinite;
  color: var(--white);
  border: none;
  border-radius: 100px;
  padding: 16px 36px;
  font-size: 1.05rem;
  font-weight: 600;
  font-family: 'DM Sans', sans-serif;
  cursor: pointer;
  box-shadow: 0 6px 24px rgba(74,159,212,0.42);
  transition: transform 0.25s var(--ease);
}

.btn-confetti:hover  { transform: scale(1.05) translateY(-2px); }
.btn-confetti:active { transform: scale(0.97); }
.btn-confetti-icon   { font-size: 1.3rem; }

@keyframes gradientShift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Emoji Rain area */
.emoji-rain-area {
  width: 100%;
  min-height: 100px;
  border-radius: var(--radius-lg);
  border: 2px dashed rgba(144,200,240,0.55);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  background: rgba(255,255,255,0.5);
  backdrop-filter: blur(6px);
}

.emoji-rain-hint {
  color: var(--text-light);
  font-size: 0.88rem;
  text-align: center;
  pointer-events: none;
  user-select: none;
}

.emoji-float {
  position: absolute;
  font-size: 1.6rem;
  pointer-events: none;
  animation: floatUp 1.4s ease-out forwards;
  user-select: none;
}

@keyframes floatUp {
  0%   { transform: translateY(0) scale(1);    opacity: 1; }
  100% { transform: translateY(-90px) scale(0.4); opacity: 0; }
}

/* Candles section */
.candles-section {
  width: 100%;
  background: var(--white);
  border-radius: var(--radius-lg);
  padding: 24px 28px;
  box-shadow: var(--shadow-sm);
  text-align: center;
  border: 1px solid rgba(144,200,240,0.28);
}

.candles-label {
  font-size: 0.95rem;
  color: var(--text-mid);
  margin-bottom: 18px;
  font-weight: 500;
}

.candles-row {
  display: flex;
  justify-content: center;
  gap: 18px;
  flex-wrap: wrap;
}

.candle {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: transform 0.2s;
  user-select: none;
}

.candle:hover { transform: scale(1.15); }

.flame {
  font-size: 1.4rem;
  display: block;
  animation: flickerFlame 0.8s ease-in-out infinite alternate;
  transition: opacity 0.3s;
}

.candle[data-lit="false"] .flame {
  opacity: 0;
  animation: none;
}

@keyframes flickerFlame {
  0%   { transform: scale(1) rotate(-3deg); }
  100% { transform: scale(1.1) rotate(3deg); }
}

.candle-body { font-size: 1.6rem; display: block; }

.candles-done {
  margin-top: 16px;
  font-size: 1rem;
  color: var(--blue-deep);
  font-weight: 600;
  opacity: 0;
  transform: scale(0.8);
  transition: opacity 0.4s, transform 0.4s;
}

.candles-done.visible { opacity: 1; transform: scale(1); }

/* ── Confetti canvas ── */
#confettiCanvas {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  z-index: 500;
}

/* ── Responsive — Desktop ── */
@media (min-width: 768px) {
  .page { padding: 60px 48px 80px; }

  .photo-grid {
    grid-template-columns: 1.5fr 1fr;
    grid-template-rows: 200px 160px;
    gap: 16px;
  }

  .gift-box { width: 240px; height: 240px; }
  .sparkle-ring { width: 260px; height: 260px; }
  .nav-dots { right: 28px; gap: 14px; }
  .dot { width: 12px; height: 12px; }
  .emoji-rain-area { min-height: 120px; }
}

@media (min-width: 1024px) {
  .photo-grid {
    grid-template-columns: 1.6fr 1fr;
    grid-template-rows: 240px 180px;
  }
}

/* ── Utility ── */
.hidden { display: none !important; }
</style>
</head>
<body>

  <!-- ✨ Background Music (optional, muted by default) -->
  <audio id="bg-music" loop>
    <source src="[INSERT_MUSIC_URL_HERE]" type="audio/mpeg" />
  </audio>

  <!-- 🔊 Music Toggle Button -->
  <button class="music-btn" id="musicBtn" aria-label="Toggle music">🔇</button>

  <!-- ── Navigation Dots ── -->
  <nav class="nav-dots" id="navDots" aria-label="Page navigation">
    <button class="dot active" data-page="0" aria-label="Birthday Wishes"></button>
    <button class="dot"        data-page="1" aria-label="Video"></button>
    <button class="dot"        data-page="2" aria-label="Present"></button>
    <button class="dot"        data-page="3" aria-label="Surprise"></button>
  </nav>

  <!-- ── App Wrapper ── -->
  <div class="app" id="app">

    <!-- ══════════════════════════════════════════
         PAGE 1 — 🎉 BIRTHDAY WISHES
    ══════════════════════════════════════════ -->
    <section class="page" id="page-0" data-page="0">
      <div class="page-inner">

        <div class="balloons" aria-hidden="true">
          <span class="balloon b1">🎈</span>
          <span class="balloon b2">🎈</span>
          <span class="balloon b3">🎈</span>
        </div>

        <header class="page-header animate-in">
          <span class="tag">Happy Birthday</span>
          <h1 class="title">It's Your<br /><em>Special Day</em></h1>
        </header>

        <!-- Photo Gallery -->
        <div class="photo-grid animate-in delay-1">
          <div class="photo-card photo-main">
            <div class="photo-placeholder">
              <span class="photo-icon">📸</span>
              <p>[INSERT_IMAGE_1]</p>
            </div>
          </div>
          <div class="photo-card photo-side-top">
            <div class="photo-placeholder">
              <span class="photo-icon">📸</span>
              <p>[INSERT_IMAGE_2]</p>
            </div>
          </div>
          <div class="photo-card photo-side-bottom">
            <div class="photo-placeholder">
              <span class="photo-icon">📸</span>
              <p>[INSERT_IMAGE_3]</p>
            </div>
          </div>
        </div>

        <!-- Birthday Message -->
        <div class="message-card animate-in delay-2">
          <div class="quote-mark">"</div>
          <p class="message-text">[INSERT_BIRTHDAY_MESSAGE_HERE]</p>
          <div class="message-signature">— With all the love 💙</div>
        </div>

        <button class="btn-next animate-in delay-3" data-goto="1">
          Keep Going <span class="arrow">→</span>
        </button>

      </div>
    </section>

    <!-- ══════════════════════════════════════════
         PAGE 2 — 🎥 VIDEO
    ══════════════════════════════════════════ -->
    <section class="page" id="page-1" data-page="1">
      <div class="page-inner">

        <header class="page-header animate-in">
          <span class="tag">A Little Something</span>
          <h2 class="title">For Your<br /><em>Eyes Only</em> 🎬</h2>
        </header>

        <div class="video-wrapper animate-in delay-1">
          <div class="video-overlay" id="videoOverlay">
            <div class="play-btn-circle">
              <span class="play-icon">▶</span>
            </div>
            <p class="video-hint">Tap to play your special video</p>
          </div>
          <video id="birthdayVideo" controls poster="" preload="metadata">
            <source src="[INSERT_VIDEO_URL_OR_FILE_HERE]" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
          <!-- To embed YouTube/Vimeo instead, replace the <video> above with:
          <iframe src="[INSERT_YOUTUBE_EMBED_URL_HERE]" title="Birthday Video"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen></iframe>
          -->
        </div>

        <p class="video-caption animate-in delay-2">Made just for you — press play and enjoy! 🥰</p>

        <div class="nav-btns animate-in delay-3">
          <button class="btn-prev" data-goto="0">← Back</button>
          <button class="btn-next" data-goto="2">Next <span class="arrow">→</span></button>
        </div>

      </div>
    </section>

    <!-- ══════════════════════════════════════════
         PAGE 3 — 🎁 PRESENT
    ══════════════════════════════════════════ -->
    <section class="page" id="page-2" data-page="2">
      <div class="page-inner">

        <header class="page-header animate-in">
          <span class="tag">A Gift for You</span>
          <h2 class="title">Something<br /><em>Special</em> 🎁</h2>
        </header>

        <div class="gift-stage animate-in delay-1">
          <div class="gift-box" id="giftBox" title="Click to unwrap!">

            <!-- Unwrapped (hidden until click) -->
            <div class="gift-unwrapped" id="giftUnwrapped">
              <div class="gift-image-placeholder">
                <span class="gift-img-icon">🎀</span>
                <p class="gift-img-label">[INSERT_GIFT_IMAGE_HERE]</p>
                <!-- Replace with: <img src="your-image.jpg" alt="Your gift" class="gift-img" /> -->
              </div>
            </div>

            <!-- Wrapped -->
            <div class="gift-wrapped" id="giftWrapped">
              <div class="gift-ribbon-h"></div>
              <div class="gift-ribbon-v"></div>
              <div class="gift-bow">🎀</div>
              <div class="gift-shine"></div>
              <p class="gift-tap-hint">Tap to unwrap!</p>
            </div>
          </div>

          <div class="sparkle-ring" id="sparkleRing" aria-hidden="true"></div>
        </div>

        <div class="gift-message animate-in delay-2" id="giftMessage">
          <p>[INSERT_GIFT_MESSAGE_HERE]</p>
        </div>

        <div class="nav-btns animate-in delay-3">
          <button class="btn-prev" data-goto="1">← Back</button>
          <button class="btn-next" data-goto="3">Final Surprise <span class="arrow">→</span></button>
        </div>

      </div>
    </section>

    <!-- ══════════════════════════════════════════
         PAGE 4 — 🎊 SURPRISE / INTERACTIVE
    ══════════════════════════════════════════ -->
    <section class="page" id="page-3" data-page="3">
      <div class="page-inner">

        <header class="page-header animate-in">
          <span class="tag">🎊 The Big Finale</span>
          <h2 class="title"><em>Surprise!</em></h2>
        </header>

        <!-- Hidden message reveal -->
        <div class="surprise-reveal animate-in delay-1" id="surpriseReveal">
          <div class="surprise-lock" id="surpriseLock">
            <div class="lock-icon">🔮</div>
            <p class="lock-hint">Press the button below to reveal your surprise!</p>
          </div>
          <div class="surprise-message" id="surpriseMessage">
            <div class="surprise-emoji">🌟</div>
            <p class="surprise-text">[INSERT_SURPRISE_MESSAGE_HERE]</p>
          </div>
        </div>

        <!-- Confetti Button -->
        <button class="btn-confetti animate-in delay-2" id="confettiBtn">
          <span class="btn-confetti-icon">🎊</span>
          Reveal Your Surprise!
        </button>

        <!-- Emoji Rain -->
        <div class="emoji-rain-area animate-in delay-2" id="emojiArea">
          <p class="emoji-rain-hint">Tap anywhere in this box to celebrate! 🥳</p>
        </div>

        <!-- Candles -->
        <div class="candles-section animate-in delay-3">
          <p class="candles-label">Blow out your candles! 🎂</p>
          <div class="candles-row" id="candlesRow">
            <div class="candle" data-lit="true"><span class="flame">🔥</span><span class="candle-body">🕯️</span></div>
            <div class="candle" data-lit="true"><span class="flame">🔥</span><span class="candle-body">🕯️</span></div>
            <div class="candle" data-lit="true"><span class="flame">🔥</span><span class="candle-body">🕯️</span></div>
            <div class="candle" data-lit="true"><span class="flame">🔥</span><span class="candle-body">🕯️</span></div>
            <div class="candle" data-lit="true"><span class="flame">🔥</span><span class="candle-body">🕯️</span></div>
          </div>
          <p class="candles-done" id="candlesDone">🎉 Make a wish!</p>
        </div>

        <button class="btn-prev animate-in delay-3" data-goto="2">← Back</button>

      </div>

      <canvas id="confettiCanvas"></canvas>
    </section>

  </div><!-- /.app -->

<script>
/* ============================================================
   BIRTHDAY APP — JavaScript
   ============================================================ */

/* ── SPA Navigation ── */
let currentPage = 0;
const TOTAL_PAGES = 4;

function goToPage(index) {
  if (index < 0 || index >= TOTAL_PAGES) return;
  const current = document.querySelector('.page.active');
  const target  = document.getElementById(`page-${index}`);
  if (!target || current === target) return;

  if (current) {
    current.classList.add('exit');
    setTimeout(() => current.classList.remove('active', 'exit'), 350);
  }

  setTimeout(() => {
    target.classList.add('active');
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }, 180);

  currentPage = index;
  updateDots();
}

function updateDots() {
  document.querySelectorAll('.dot').forEach((dot, i) => {
    dot.classList.toggle('active', i === currentPage);
  });
}

// Navigation buttons
document.querySelectorAll('[data-goto]').forEach(btn => {
  btn.addEventListener('click', () => goToPage(parseInt(btn.dataset.goto, 10)));
});

// Nav dots
document.querySelectorAll('.dot').forEach(dot => {
  dot.addEventListener('click', () => goToPage(parseInt(dot.dataset.page, 10)));
});

// Keyboard navigation
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') goToPage(currentPage + 1);
  if (e.key === 'ArrowLeft'  || e.key === 'ArrowUp')   goToPage(currentPage - 1);
});

// Show page 0 on load
document.getElementById('page-0').classList.add('active');

/* ── Music Toggle ── */
const bgMusic    = document.getElementById('bg-music');
const musicBtn   = document.getElementById('musicBtn');
let musicPlaying = false;

musicBtn.addEventListener('click', () => {
  if (musicPlaying) {
    bgMusic.pause();
    musicBtn.textContent = '🔇';
    musicPlaying = false;
  } else {
    bgMusic.play().catch(() => {
      console.info('Set a valid audio URL at [INSERT_MUSIC_URL_HERE]');
    });
    musicBtn.textContent = '🔊';
    musicPlaying = true;
  }
});

/* ── Video Overlay ── */
const videoOverlay  = document.getElementById('videoOverlay');
const birthdayVideo = document.getElementById('birthdayVideo');

if (videoOverlay && birthdayVideo) {
  videoOverlay.addEventListener('click', () => {
    videoOverlay.classList.add('hidden');
    birthdayVideo.play().catch(() => {
      console.info('Set a real video URL in [INSERT_VIDEO_URL_OR_FILE_HERE]');
    });
  });
}

/* ── Gift Box Unwrap ── */
const giftBox     = document.getElementById('giftBox');
const sparkleRing = document.getElementById('sparkleRing');
const giftMessage = document.getElementById('giftMessage');

if (giftBox) {
  giftBox.addEventListener('click', () => {
    if (giftBox.classList.contains('unwrapped')) return;
    giftBox.classList.add('unwrapped');
    sparkleRing.classList.add('active');

    giftBox.animate([
      { transform: 'rotate(-5deg) scale(1.05)' },
      { transform: 'rotate(5deg) scale(1.08)' },
      { transform: 'rotate(-3deg) scale(1.04)' },
      { transform: 'rotate(0deg) scale(1)' },
    ], { duration: 400, easing: 'ease-out' });

    if (giftMessage) {
      giftMessage.style.animation = 'popIn 0.5s 0.3s ease both';
    }

    launchConfetti(60, true);
  });
}

/* ── Surprise Reveal ── */
const confettiBtn     = document.getElementById('confettiBtn');
const surpriseLock    = document.getElementById('surpriseLock');
const surpriseMessage = document.getElementById('surpriseMessage');
let surpriseRevealed  = false;

if (confettiBtn) {
  confettiBtn.addEventListener('click', () => {
    if (!surpriseRevealed) {
      surpriseLock.classList.add('hidden');
      surpriseMessage.classList.add('visible');
      confettiBtn.textContent = '🎊 More Confetti!';
      surpriseRevealed = true;
    }
    launchConfetti(200, false);
  });
}

/* ── Emoji Rain ── */
const emojiArea = document.getElementById('emojiArea');
const EMOJIS    = ['🎉','🎊','🎈','💙','✨','🌟','🥳','🎂','🍰','🌸','💐','🦋','⭐','🫐'];

if (emojiArea) {
  emojiArea.addEventListener('click', e => spawnEmoji(e));
  emojiArea.addEventListener('touchstart', e => {
    e.preventDefault();
    spawnEmoji(e.touches[0]);
  }, { passive: false });
}

function spawnEmoji(e) {
  const rect  = emojiArea.getBoundingClientRect();
  const x     = (e.clientX || e.pageX) - rect.left;
  const y     = (e.clientY || e.pageY) - rect.top;
  const emoji = EMOJIS[Math.floor(Math.random() * EMOJIS.length)];

  const el = document.createElement('span');
  el.classList.add('emoji-float');
  el.textContent  = emoji;
  el.style.left   = `${x}px`;
  el.style.top    = `${y}px`;
  el.style.fontSize = `${1.2 + Math.random() * 1.2}rem`;
  emojiArea.appendChild(el);
  el.addEventListener('animationend', () => el.remove());
}

/* ── Candles ── */
const candles     = document.querySelectorAll('.candle');
const candlesDone = document.getElementById('candlesDone');
let litCount      = candles.length;

candles.forEach(candle => {
  candle.addEventListener('click', () => {
    if (candle.dataset.lit === 'false') return;
    candle.dataset.lit = 'false';
    litCount--;

    candle.animate([
      { transform: 'scale(1.2)' },
      { transform: 'scale(0.9)' },
      { transform: 'scale(1)' }
    ], { duration: 300, easing: 'ease-out' });

    if (litCount === 0) {
      candlesDone.classList.add('visible');
      launchConfetti(120, false);
    }
  });
});

/* ── Confetti Engine ── */
const canvas = document.getElementById('confettiCanvas');
const ctx    = canvas.getContext('2d');
let confettiParticles = [];
let animFrameId       = null;

function resizeCanvas() {
  canvas.width  = window.innerWidth;
  canvas.height = window.innerHeight;
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

// Pastel blue confetti palette
const CONFETTI_COLORS = [
  '#90c8f0','#4a9fd4','#2d7bb5','#b3e5f7',
  '#daeeff','#c8eef5','#b8d4f5','#7ec8e3',
  '#ffffff','#a8d8ea','#63b3d6'
];

const CONFETTI_SHAPES = ['circle','rect','triangle'];

function launchConfetti(count, mini) {
  for (let i = 0; i < count; i++) confettiParticles.push(createParticle(mini));
  if (!animFrameId) animFrameId = requestAnimationFrame(updateConfetti);
}

function createParticle(mini) {
  const x = mini
    ? canvas.width / 2 + (Math.random() - 0.5) * 200
    : Math.random() * canvas.width;
  return {
    x,
    y: mini ? canvas.height / 2 : -10,
    vx: (Math.random() - 0.5) * (mini ? 5 : 8),
    vy: Math.random() * (mini ? 4 : 6) + 2,
    size: Math.random() * 8 + 4,
    color: CONFETTI_COLORS[Math.floor(Math.random() * CONFETTI_COLORS.length)],
    shape: CONFETTI_SHAPES[Math.floor(Math.random() * CONFETTI_SHAPES.length)],
    rotation: Math.random() * Math.PI * 2,
    rotationSpeed: (Math.random() - 0.5) * 0.18,
    life: 1,
    decay: 0.008 + Math.random() * 0.006,
    gravity: 0.12 + Math.random() * 0.08,
  };
}

function updateConfetti() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  confettiParticles = confettiParticles.filter(p => p.life > 0);

  confettiParticles.forEach(p => {
    p.x        += p.vx;
    p.y        += p.vy;
    p.vy       += p.gravity;
    p.rotation += p.rotationSpeed;
    p.life     -= p.decay;

    ctx.save();
    ctx.globalAlpha = Math.max(0, p.life);
    ctx.translate(p.x, p.y);
    ctx.rotate(p.rotation);
    ctx.fillStyle = p.color;

    const s = p.size;
    switch (p.shape) {
      case 'circle':
        ctx.beginPath();
        ctx.arc(0, 0, s / 2, 0, Math.PI * 2);
        ctx.fill();
        break;
      case 'rect':
        ctx.fillRect(-s / 2, -s / 4, s, s / 2);
        break;
      case 'triangle':
        ctx.beginPath();
        ctx.moveTo(0, -s / 2);
        ctx.lineTo(s / 2, s / 2);
        ctx.lineTo(-s / 2, s / 2);
        ctx.closePath();
        ctx.fill();
        break;
    }
    ctx.restore();
  });

  if (confettiParticles.length > 0) {
    animFrameId = requestAnimationFrame(updateConfetti);
  } else {
    animFrameId = null;
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }
}

/* ── Swipe Gestures (mobile) ── */
let touchStartX = 0;
let touchStartY = 0;

document.addEventListener('touchstart', e => {
  touchStartX = e.touches[0].clientX;
  touchStartY = e.touches[0].clientY;
}, { passive: true });

document.addEventListener('touchend', e => {
  const dx = e.changedTouches[0].clientX - touchStartX;
  const dy = e.changedTouches[0].clientY - touchStartY;
  if (Math.abs(dx) > Math.abs(dy) && Math.abs(dx) > 50) {
    if (dx < 0) goToPage(currentPage + 1);
    else         goToPage(currentPage - 1);
  }
}, { passive: true });

/* ── Inject popIn keyframe ── */
const s = document.createElement('style');
s.textContent = `
  @keyframes popIn {
    0%   { opacity: 0; transform: scale(0.6) rotate(-5deg); }
    100% { opacity: 1; transform: scale(1)   rotate(0deg);  }
  }
`;
document.head.appendChild(s);

console.log('%c💙 Happy Birthday! 💙', 'font-size:24px;color:#4a9fd4;font-weight:bold;');
</script>
</body>
</html>
