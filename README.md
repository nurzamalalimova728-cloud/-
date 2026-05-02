# -<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TypeRace СНГ — Тренажёр печати</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Exo+2:wght@300;400;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0a0e1a;
  --bg2: #111827;
  --bg3: #1a2235;
  --accent: #00d4ff;
  --accent2: #7c3aed;
  --green: #10b981;
  --red: #ef4444;
  --yellow: #f59e0b;
  --text: #e2e8f0;
  --text2: #94a3b8;
  --border: rgba(0,212,255,0.2);
}
* { margin:0; padding:0; box-sizing:border-box; }
body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Exo 2', sans-serif;
  min-height: 100vh;
  overflow-x: hidden;
}
body::before {
  content:'';
  position:fixed; top:0; left:0; right:0; bottom:0;
  background: radial-gradient(ellipse at 20% 50%, rgba(124,58,237,0.08) 0%, transparent 60%),
              radial-gradient(ellipse at 80% 20%, rgba(0,212,255,0.06) 0%, transparent 50%);
  pointer-events:none; z-index:0;
}
.screen { display:none; position:relative; z-index:1; }
.screen.active { display:block; }

/* ===== HEADER ===== */
header {
  display:flex; align-items:center; justify-content:space-between;
  padding: 16px 32px;
  border-bottom: 1px solid var(--border);
  background: rgba(10,14,26,0.9);
  backdrop-filter: blur(12px);
  position: sticky; top:0; z-index:100;
}
.logo {
  font-family: 'Orbitron', monospace;
  font-size: 22px; font-weight:900;
  color: var(--accent);
  text-shadow: 0 0 20px rgba(0,212,255,0.4);
  letter-spacing: 2px;
}
.logo span { color: var(--accent2); }
nav { display:flex; gap:8px; align-items:center; }
.nav-btn {
  background: transparent;
  border: 1px solid var(--border);
  color: var(--text2);
  padding: 8px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-family: 'Exo 2', sans-serif;
  font-size: 14px;
  transition: all 0.2s;
}
.nav-btn:hover { border-color: var(--accent); color: var(--accent); }
.nav-btn.primary {
  background: var(--accent);
  color: #000;
  border-color: var(--accent);
  font-weight: 600;
}
.nav-btn.primary:hover { background: #00b8d9; }

/* ===== LANGUAGE SELECTOR ===== */
.lang-select {
  background: var(--bg2);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 8px 12px;
  border-radius: 8px;
  font-family: 'Exo 2', sans-serif;
  font-size: 14px;
  cursor: pointer;
}
.lang-select:focus { outline: none; border-color: var(--accent); }

/* ===== HOME SCREEN ===== */
.hero {
  text-align:center;
  padding: 80px 32px 60px;
}
.hero h1 {
  font-family: 'Orbitron', monospace;
  font-size: clamp(32px, 6vw, 72px);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 20px;
}
.hero h1 .line1 { color: var(--text); }
.hero h1 .line2 { color: var(--accent); text-shadow: 0 0 30px rgba(0,212,255,0.5); }
.hero p {
  font-size: 18px;
  color: var(--text2);
  max-width: 600px;
  margin: 0 auto 48px;
  line-height: 1.7;
}
.modes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  max-width: 960px;
  margin: 0 auto;
  padding: 0 16px;
}
.mode-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 28px;
  cursor: pointer;
  transition: all 0.3s;
  text-align: left;
  position: relative;
  overflow: hidden;
}
.mode-card::before {
  content:'';
  position:absolute; top:0; left:0; right:0; height:3px;
  border-radius:16px 16px 0 0;
}
.mode-card.easy::before { background: var(--green); }
.mode-card.medium::before { background: var(--yellow); }
.mode-card.hard::before { background: var(--red); }
.mode-card:hover {
  transform: translateY(-4px);
  border-color: rgba(0,212,255,0.4);
  box-shadow: 0 20px 40px rgba(0,0,0,0.4);
}
.mode-icon { font-size: 36px; margin-bottom: 16px; }
.mode-name {
  font-family: 'Orbitron', monospace;
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 8px;
}
.mode-card.easy .mode-name { color: var(--green); }
.mode-card.medium .mode-name { color: var(--yellow); }
.mode-card.hard .mode-name { color: var(--red); }
.mode-desc { color: var(--text2); font-size: 14px; line-height: 1.6; }
.mode-stats {
  display: flex; gap: 12px; margin-top: 16px; flex-wrap: wrap;
}
.stat-badge {
  background: var(--bg3);
  border-radius: 6px;
  padding: 4px 10px;
  font-size: 12px;
  color: var(--text2);
}

/* ===== GAME SCREEN ===== */
.game-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 24px 16px;
}
.game-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
  flex-wrap: wrap;
  gap: 12px;
}
.timer-display {
  font-family: 'Orbitron', monospace;
  font-size: 48px;
  font-weight: 900;
  color: var(--accent);
  text-shadow: 0 0 20px rgba(0,212,255,0.5);
  min-width: 120px;
  text-align: center;
}
.timer-display.warning { color: var(--yellow); text-shadow: 0 0 20px rgba(245,158,11,0.5); }
.timer-display.danger { color: var(--red); text-shadow: 0 0 20px rgba(239,68,68,0.5); animation: pulse 0.5s infinite alternate; }
@keyframes pulse { from { opacity:1; } to { opacity:0.6; } }
.score-display {
  text-align: right;
}
.score-num {
  font-family: 'Orbitron', monospace;
  font-size: 36px;
  font-weight: 700;
  color: var(--accent2);
}
.score-label { font-size: 12px; color: var(--text2); }

.progress-bar {
  height: 4px;
  background: var(--bg3);
  border-radius: 2px;
  margin-bottom: 24px;
  overflow: hidden;
}
.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--accent), var(--accent2));
  border-radius: 2px;
  transition: width 1s linear;
}

/* Countdown */
.countdown-overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.85);
  z-index: 200;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 16px;
}
.countdown-overlay.show { display: flex; }
.countdown-num {
  font-family: 'Orbitron', monospace;
  font-size: 120px;
  font-weight: 900;
  color: var(--accent);
  text-shadow: 0 0 60px rgba(0,212,255,0.8);
  animation: countAnim 0.8s ease-out;
}
@keyframes countAnim {
  from { transform: scale(2); opacity:0; }
  to { transform: scale(1); opacity:1; }
}
.countdown-msg {
  font-size: 20px;
  color: var(--text2);
  font-family: 'Orbitron', monospace;
}

/* Words display */
.words-area {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 28px;
  margin-bottom: 20px;
  min-height: 120px;
  position: relative;
}
.current-word-display {
  font-family: 'Orbitron', monospace;
  font-size: clamp(28px, 5vw, 52px);
  font-weight: 700;
  text-align: center;
  letter-spacing: 6px;
  color: var(--text);
  min-height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2px;
}
.char { transition: color 0.1s; }
.char.correct { color: var(--green); }
.char.wrong { color: var(--red); text-decoration: underline; }
.char.current { color: var(--accent); border-bottom: 2px solid var(--accent); }
.char.pending { color: var(--text2); }

.next-words {
  display: flex;
  gap: 16px;
  justify-content: center;
  margin-top: 16px;
  flex-wrap: wrap;
}
.next-word {
  font-size: 16px;
  color: var(--text2);
  opacity: 0.5;
  padding: 4px 8px;
  background: var(--bg3);
  border-radius: 6px;
  font-family: 'Exo 2', sans-serif;
}

.input-area {
  display: flex;
  gap: 12px;
  align-items: center;
}
.typing-input {
  flex: 1;
  background: var(--bg2);
  border: 2px solid var(--border);
  color: var(--text);
  padding: 16px 20px;
  border-radius: 12px;
  font-size: 20px;
  font-family: 'Exo 2', sans-serif;
  outline: none;
  transition: border-color 0.2s;
  letter-spacing: 2px;
}
.typing-input:focus { border-color: var(--accent); }
.typing-input.correct-state { border-color: var(--green); }
.typing-input.wrong-state { border-color: var(--red); }

.score-popup {
  position: fixed;
  pointer-events: none;
  font-family: 'Orbitron', monospace;
  font-size: 24px;
  font-weight: 700;
  animation: floatUp 1s ease-out forwards;
  z-index: 300;
}
.score-popup.positive { color: var(--green); }
.score-popup.negative { color: var(--red); }
@keyframes floatUp {
  from { transform: translateY(0); opacity:1; }
  to { transform: translateY(-80px); opacity:0; }
}

.live-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-top: 20px;
}
.live-stat {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 12px;
  text-align: center;
}
.live-stat-val {
  font-family: 'Orbitron', monospace;
  font-size: 22px;
  font-weight: 700;
  color: var(--accent);
}
.live-stat-label { font-size: 11px; color: var(--text2); margin-top: 4px; }

/* ===== RESULTS SCREEN ===== */
.results-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 16px;
}
.result-title {
  font-family: 'Orbitron', monospace;
  font-size: 32px;
  font-weight: 900;
  text-align: center;
  margin-bottom: 8px;
}
.result-comment {
  text-align: center;
  font-size: 18px;
  color: var(--text2);
  margin-bottom: 40px;
  font-style: italic;
}
.results-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 16px;
  margin-bottom: 32px;
}
.result-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 20px;
  text-align: center;
}
.result-val {
  font-family: 'Orbitron', monospace;
  font-size: 32px;
  font-weight: 700;
  color: var(--accent);
  margin-bottom: 8px;
}
.result-label { font-size: 13px; color: var(--text2); }

.chart-container {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 24px;
  margin-bottom: 24px;
}
.chart-title {
  font-family: 'Orbitron', monospace;
  font-size: 16px;
  margin-bottom: 20px;
  color: var(--text2);
}
.bar-chart { display: flex; gap: 12px; align-items: flex-end; height: 120px; }
.bar-item { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 6px; }
.bar { width: 100%; border-radius: 6px 6px 0 0; transition: height 0.5s ease; min-height: 4px; }
.bar-label { font-size: 11px; color: var(--text2); text-align: center; }
.bar-val { font-size: 11px; font-weight: 600; }

.accuracy-bar {
  height: 24px;
  background: var(--bg3);
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  margin: 12px 0;
}
.acc-correct { background: var(--green); display: flex; align-items: center; justify-content: center; font-size: 12px; color: #000; font-weight: 600; transition: width 0.8s ease; }
.acc-wrong { background: var(--red); display: flex; align-items: center; justify-content: center; font-size: 12px; color: #fff; font-weight: 600; transition: width 0.8s ease; }

.result-actions { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
.btn-big {
  background: var(--accent);
  color: #000;
  border: none;
  padding: 14px 32px;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 700;
  cursor: pointer;
  font-family: 'Orbitron', monospace;
  transition: all 0.2s;
  letter-spacing: 1px;
}
.btn-big:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(0,212,255,0.3); }
.btn-big.secondary {
  background: var(--bg2);
  color: var(--text);
  border: 1px solid var(--border);
}
.btn-big.secondary:hover { border-color: var(--accent); color: var(--accent); }

/* ===== LEADERBOARD ===== */
.leaderboard-container {
  max-width: 700px;
  margin: 0 auto;
  padding: 40px 16px;
}
.section-title {
  font-family: 'Orbitron', monospace;
  font-size: 28px;
  font-weight: 700;
  color: var(--accent);
  margin-bottom: 8px;
  text-align: center;
}
.section-sub { text-align: center; color: var(--text2); margin-bottom: 32px; font-size: 14px; }
.lb-table { width: 100%; border-collapse: collapse; }
.lb-table th {
  text-align: left;
  padding: 12px 16px;
  font-size: 12px;
  color: var(--text2);
  border-bottom: 1px solid var(--border);
  font-family: 'Orbitron', monospace;
  font-weight: 400;
  letter-spacing: 1px;
}
.lb-table td { padding: 14px 16px; border-bottom: 1px solid rgba(255,255,255,0.05); }
.lb-table tr:hover td { background: rgba(0,212,255,0.04); }
.rank-num {
  font-family: 'Orbitron', monospace;
  font-weight: 700;
  font-size: 18px;
}
.rank-1 { color: #fbbf24; }
.rank-2 { color: #94a3b8; }
.rank-3 { color: #cd7f32; }
.nick { font-weight: 600; font-size: 15px; }
.wpm-val { font-family: 'Orbitron', monospace; color: var(--accent); font-weight: 700; }
.lang-badge {
  background: var(--bg3);
  padding: 3px 8px;
  border-radius: 4px;
  font-size: 12px;
  color: var(--text2);
}
.you-row td { background: rgba(0,212,255,0.05) !important; }
.you-badge {
  background: var(--accent);
  color: #000;
  font-size: 10px;
  padding: 2px 6px;
  border-radius: 4px;
  margin-left: 6px;
  font-weight: 700;
}

/* ===== AUTH MODAL ===== */
.modal-overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.8);
  z-index: 500;
  align-items: center;
  justify-content: center;
}
.modal-overlay.show { display: flex; }
.modal {
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 40px;
  width: 100%;
  max-width: 420px;
  position: relative;
}
.modal h2 {
  font-family: 'Orbitron', monospace;
  font-size: 24px;
  color: var(--accent);
  margin-bottom: 24px;
  text-align: center;
}
.form-group { margin-bottom: 16px; }
.form-label { display: block; font-size: 13px; color: var(--text2); margin-bottom: 6px; }
.form-input {
  width: 100%;
  background: var(--bg3);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 12px 16px;
  border-radius: 10px;
  font-size: 15px;
  font-family: 'Exo 2', sans-serif;
  outline: none;
  transition: border-color 0.2s;
}
.form-input:focus { border-color: var(--accent); }
.form-error { font-size: 12px; color: var(--red); margin-top: 4px; display: none; }
.modal-close {
  position: absolute;
  top: 16px; right: 16px;
  background: transparent;
  border: none;
  color: var(--text2);
  font-size: 24px;
  cursor: pointer;
  line-height: 1;
}
.modal-close:hover { color: var(--text); }
.auth-tabs { display: flex; margin-bottom: 24px; background: var(--bg3); border-radius: 10px; padding: 4px; }
.auth-tab {
  flex: 1; padding: 10px; text-align: center;
  border-radius: 8px; cursor: pointer;
  font-size: 14px; color: var(--text2);
  transition: all 0.2s;
  border: none; background: transparent;
  font-family: 'Exo 2', sans-serif;
}
.auth-tab.active { background: var(--accent); color: #000; font-weight: 600; }
.user-info {
  display: flex; align-items: center; gap: 10px;
}
.avatar {
  width: 36px; height: 36px;
  background: var(--accent2);
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: 14px; color: #fff;
  font-family: 'Orbitron', monospace;
}
.user-nick { font-size: 14px; font-weight: 600; }
.user-score { font-size: 12px; color: var(--text2); }

/* Notifications */
.toast {
  position: fixed;
  bottom: 32px; left: 50%;
  transform: translateX(-50%) translateY(100px);
  background: var(--bg2);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 14px 24px;
  font-size: 15px;
  z-index: 1000;
  transition: transform 0.3s ease;
  max-width: 400px;
  text-align: center;
}
.toast.show { transform: translateX(-50%) translateY(0); }
.toast.success { border-color: var(--green); color: var(--green); }
.toast.error { border-color: var(--red); color: var(--red); }

/* Responsive */
@media (max-width: 600px) {
  header { padding: 12px 16px; }
  .logo { font-size: 16px; }
  .hero { padding: 40px 16px 32px; }
  .timer-display { font-size: 36px; }
  .score-num { font-size: 24px; }
  .current-word-display { font-size: 24px; letter-spacing: 4px; }
}
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <div class="logo">TYPE<span>RACE</span> СНГ</div>
  <nav>
    <select class="lang-select" id="uiLang" onchange="changeUILang(this.value)">
      <option value="ru">🇷🇺 Русский</option>
      <option value="kg">🇰🇬 Кыргызча</option>
      <option value="en">🇺🇸 English</option>
      <option value="uz">🇺🇿 O'zbekcha</option>
      <option value="kk">🇰🇿 Қазақша</option>
    </select>
    <button class="nav-btn" onclick="showScreen('leaderboard')" id="nav-lb">🏆 Рейтинг</button>
    <div id="authArea">
      <button class="nav-btn primary" onclick="openAuth()" id="nav-login">Войти</button>
    </div>
  </nav>
</header>

<!-- COUNTDOWN OVERLAY -->
<div class="countdown-overlay" id="countdownOverlay">
  <div class="countdown-num" id="countdownNum">3</div>
  <div class="countdown-msg" id="countdownMsg">Готовься!</div>
</div>

<!-- HOME SCREEN -->
<div class="screen active" id="screen-home">
  <div class="hero">
    <h1>
      <div class="line1" id="hero-line1">Тренажёр</div>
      <div class="line2" id="hero-line2">СКОРОСТНОЙ ПЕЧАТИ</div>
    </h1>
    <p id="hero-sub">Соревнуйся с игроками СНГ. Выбери язык, уровень — и докажи, кто быстрее!</p>
  </div>

  <div style="max-width:300px;margin:0 auto 32px;padding:0 16px;">
    <label style="font-size:13px;color:var(--text2);display:block;margin-bottom:8px;" id="label-typing-lang">Язык для печати:</label>
    <select class="lang-select" style="width:100%;font-size:15px;padding:12px 16px;" id="typingLang">
      <option value="ru">🇷🇺 Русский</option>
      <option value="kg">🇰🇬 Кыргызча</option>
      <option value="en">🇺🇸 English</option>
      <option value="uz">🇺🇿 O'zbekcha</option>
      <option value="kk">🇰🇿 Қазақша</option>
    </select>
  </div>

  <div class="modes-grid" id="modesGrid">
    <div class="mode-card easy" onclick="startGame('easy')">
      <div class="mode-icon">🌱</div>
      <div class="mode-name" id="mode-easy-name">ЛЁГКИЙ</div>
      <div class="mode-desc" id="mode-easy-desc">5 минут, слова идут медленно. Очки не отнимаются. Идеально для начинающих.</div>
      <div class="mode-stats">
        <span class="stat-badge" id="mode-easy-t">⏱ 5 минут</span>
        <span class="stat-badge">+200 / +100 / +50 очков</span>
        <span class="stat-badge" id="mode-easy-pen">✅ Без штрафов</span>
      </div>
    </div>
    <div class="mode-card medium" onclick="startGame('medium')">
      <div class="mode-icon">⚡</div>
      <div class="mode-name" id="mode-med-name">СРЕДНИЙ</div>
      <div class="mode-desc" id="mode-med-desc">3 минуты. За каждую неправильную букву −30 очков. Нужна концентрация.</div>
      <div class="mode-stats">
        <span class="stat-badge" id="mode-med-t">⏱ 3 минуты</span>
        <span class="stat-badge">+200 / +100 / +50 очков</span>
        <span class="stat-badge" id="mode-med-pen">❌ −30 за ошибку</span>
      </div>
    </div>
    <div class="mode-card hard" onclick="startGame('hard')">
      <div class="mode-icon">🔥</div>
      <div class="mode-name" id="mode-hard-name">СЛОЖНЫЙ</div>
      <div class="mode-desc" id="mode-hard-desc">1 минута. Достигни цели! −50 очков за каждую ошибку. Только для лучших.</div>
      <div class="mode-stats">
        <span class="stat-badge" id="mode-hard-t">⏱ 1 минута</span>
        <span class="stat-badge">+200 / +100 / +50 очков</span>
        <span class="stat-badge" id="mode-hard-pen">💀 −50 за ошибку</span>
      </div>
    </div>
  </div>
</div>

<!-- GAME SCREEN -->
<div class="screen" id="screen-game">
  <div class="game-container">
    <div class="game-header">
      <div>
        <div class="timer-display" id="timerDisplay">5:00</div>
        <div style="font-size:12px;color:var(--text2);text-align:center;margin-top:4px;" id="timerLabel">ВРЕМЯ</div>
      </div>
      <div style="text-align:center;">
        <div style="font-size:13px;color:var(--text2);margin-bottom:4px;" id="modeLabel">ЛЁГКИЙ</div>
        <div style="font-size:13px;color:var(--text2);" id="langLabel">🇷🇺 Русский</div>
      </div>
      <div class="score-display">
        <div class="score-num" id="scoreDisplay">0</div>
        <div class="score-label" id="scoreLabel">ОЧКИ</div>
      </div>
    </div>

    <div class="progress-bar">
      <div class="progress-fill" id="progressFill" style="width:100%"></div>
    </div>

    <div class="words-area">
      <div class="current-word-display" id="wordDisplay"></div>
      <div class="next-words" id="nextWords"></div>
    </div>

    <div class="input-area">
      <input type="text" class="typing-input" id="typingInput"
        autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"
        placeholder="Начни печатать...">
    </div>

    <div class="live-stats">
      <div class="live-stat">
        <div class="live-stat-val" id="liveWPM">0</div>
        <div class="live-stat-label" id="liveWPMLabel">СЛОВ/МИН</div>
      </div>
      <div class="live-stat">
        <div class="live-stat-val" id="liveAcc">100%</div>
        <div class="live-stat-label" id="liveAccLabel">ТОЧНОСТЬ</div>
      </div>
      <div class="live-stat">
        <div class="live-stat-val" id="liveWords">0</div>
        <div class="live-stat-label" id="liveWordsLabel">СЛОВ</div>
      </div>
    </div>

    <div style="text-align:center;margin-top:20px;">
      <button class="nav-btn" onclick="quitGame()" id="quitBtn">← Выйти</button>
    </div>
  </div>
</div>

<!-- RESULTS SCREEN -->
<div class="screen" id="screen-results">
  <div class="results-container">
    <div class="result-title" id="resultTitle">🎉 Результат</div>
    <div class="result-comment" id="resultComment"></div>

    <div class="results-grid">
      <div class="result-card">
        <div class="result-val" id="res-score">0</div>
        <div class="result-label" id="res-score-l">ОЧКИ</div>
      </div>
      <div class="result-card">
        <div class="result-val" id="res-wpm">0</div>
        <div class="result-label" id="res-wpm-l">СЛОВ/МИН</div>
      </div>
      <div class="result-card">
        <div class="result-val" id="res-acc">0%</div>
        <div class="result-label" id="res-acc-l">ТОЧНОСТЬ</div>
      </div>
      <div class="result-card">
        <div class="result-val" id="res-words">0</div>
        <div class="result-label" id="res-words-l">СЛОВ НАБРАНО</div>
      </div>
    </div>

    <div class="chart-container">
      <div class="chart-title" id="chart-acc-title">ТОЧНОСТЬ НАБОРА</div>
      <div style="margin-bottom:8px;">
        <div style="display:flex;justify-content:space-between;font-size:13px;color:var(--text2);margin-bottom:6px;">
          <span id="correct-label">✅ Правильных</span>
          <span id="wrong-label">❌ Ошибок</span>
        </div>
        <div class="accuracy-bar">
          <div class="acc-correct" id="accCorrectBar" style="width:100%"><span id="accCorrectPct">100%</span></div>
          <div class="acc-wrong" id="accWrongBar" style="width:0%"><span id="accWrongPct">0%</span></div>
        </div>
      </div>
      <div style="display:flex;justify-content:space-between;font-size:13px;margin-top:8px;">
        <span style="color:var(--green);" id="correctCount">0 правильных букв</span>
        <span style="color:var(--red);" id="wrongCount">0 ошибок</span>
      </div>
    </div>

    <div class="chart-container">
      <div class="chart-title" id="chart-speed-title">СКОРОСТЬ ПО ВРЕМЕНИ (слов/мин)</div>
      <div class="bar-chart" id="speedChart"></div>
    </div>

    <div class="result-actions">
      <button class="btn-big" onclick="restartGame()" id="btn-again">🔄 Снова</button>
      <button class="btn-big secondary" onclick="showScreen('leaderboard')" id="btn-lb">🏆 Рейтинг</button>
      <button class="btn-big secondary" onclick="showScreen('home')" id="btn-home">🏠 Главная</button>
    </div>
  </div>
</div>

<!-- LEADERBOARD SCREEN -->
<div class="screen" id="screen-leaderboard">
  <div class="leaderboard-container">
    <div class="section-title" id="lb-title">🏆 РЕЙТИНГ СНГ</div>
    <div class="section-sub" id="lb-sub">Лучшие игроки по скорости набора</div>

    <div style="display:flex;gap:8px;margin-bottom:24px;flex-wrap:wrap;">
      <select class="lang-select" id="lbLangFilter" onchange="renderLeaderboard()">
        <option value="all">Все языки</option>
        <option value="ru">🇷🇺 Русский</option>
        <option value="kg">🇰🇬 Кыргызча</option>
        <option value="en">🇺🇸 English</option>
        <option value="uz">🇺🇿 O'zbekcha</option>
        <option value="kk">🇰🇿 Қазақша</option>
      </select>
      <select class="lang-select" id="lbModeFilter" onchange="renderLeaderboard()">
        <option value="all">Все уровни</option>
        <option value="easy">Лёгкий</option>
        <option value="medium">Средний</option>
        <option value="hard">Сложный</option>
      </select>
    </div>

    <table class="lb-table" id="lbTable">
      <thead>
        <tr>
          <th>#</th>
          <th id="lb-col-nick">НИК</th>
          <th id="lb-col-wpm">СКОРОСТЬ</th>
          <th id="lb-col-score">ОЧКИ</th>
          <th id="lb-col-lang">ЯЗЫК</th>
          <th id="lb-col-mode">РЕЖИМ</th>
        </tr>
      </thead>
      <tbody id="lbBody"></tbody>
    </table>

    <div style="text-align:center;margin-top:24px;">
      <button class="btn-big secondary" onclick="showScreen('home')" id="lb-back">← Назад</button>
    </div>
  </div>
</div>

<!-- AUTH MODAL -->
<div class="modal-overlay" id="authModal">
  <div class="modal">
    <button class="modal-close" onclick="closeAuth()">×</button>
    <h2 id="auth-title">ВХОД / РЕГИСТРАЦИЯ</h2>
    <div class="auth-tabs">
      <button class="auth-tab active" id="tab-login" onclick="switchTab('login')">Вход</button>
      <button class="auth-tab" id="tab-reg" onclick="switchTab('register')">Регистрация</button>
    </div>
    <div id="loginForm">
      <div class="form-group">
        <label class="form-label">Никнейм</label>
        <input type="text" class="form-input" id="loginNick" placeholder="Твой ник" maxlength="20">
      </div>
      <div class="form-group">
        <label class="form-label">Пароль</label>
        <input type="password" class="form-input" id="loginPass" placeholder="Пароль">
        <div class="form-error" id="loginError">Неверный ник или пароль</div>
      </div>
      <button class="btn-big" style="width:100%;margin-top:8px;" onclick="doLogin()">ВОЙТИ</button>
    </div>
    <div id="regForm" style="display:none;">
      <div class="form-group">
        <label class="form-label">Уникальный никнейм <span style="color:var(--accent)">*</span></label>
        <input type="text" class="form-input" id="regNick" placeholder="Например: SpeedKing_99" maxlength="20">
        <div class="form-error" id="regNickError">Этот ник уже занят</div>
      </div>
      <div class="form-group">
        <label class="form-label">Пароль</label>
        <input type="password" class="form-input" id="regPass" placeholder="Минимум 6 символов">
      </div>
      <div class="form-group">
        <label class="form-label">Подтверди пароль</label>
        <input type="password" class="form-input" id="regPass2" placeholder="Повтори пароль">
        <div class="form-error" id="regPassError">Пароли не совпадают</div>
      </div>
      <button class="btn-big" style="width:100%;margin-top:8px;" onclick="doRegister()">СОЗДАТЬ АККАУНТ</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ===================================================
//  WORD BANKS — by level (easy=3-7, medium=5-10, hard=7-15+)
// ===================================================
const WORDS = {
  ru: {
    easy: ["кот","дом","мир","год","рука","вода","небо","лес","гора","река","море","огонь","день","ночь","путь","свет","друг","сила","труд","мечта","слово","книга","школа","город","солнце","птица","рыба","звезда","весна","лето","осень","зима","земля","хлеб","молоко","масло","кофе","чайник","стакан","тарелка"],
    medium: ["время","жизнь","работа","семья","победа","радость","сердце","дорога","музыка","песня","танец","страна","природа","свобода","история","культура","здоровье","счастье","красота","ребёнок","учитель","студент","деревня","столица","погода","климат","животное","растение","движение","развитие"],
    hard: ["государство","образование","международный","правительство","окружающий","экономический","технология","информация","коммуникация","организация","представление","возможность","исследование","университет","достижение","самостоятельный","ответственность","взаимодействие","сотрудничество","промышленность","законодательство","психологический","философский","математический","электронный","демократия","конституция","революционный","переговоры","наблюдение"]
  },
  kg: {
    easy: ["үй","кол","сув","жер","от","тоо","жол","куш","ат","нан","күн","түн","дос","күч","тез","ыр","бий","айыл","нан","суу","көл","таш","гүл","жел","кар","жай","сыр","жаз","тил","эл"],
    medium: ["асман","убакыт","сөздөр","жашоо","китеп","мектеп","достук","жылдыз","токой","дарыя","деңиз","кубаныч","жүрөк","сүйүү","кийим","мезгил","адамдар","шаар","жеңиш","акырын","сулуу","акылдуу","жакшы","музыка","балык","айылдар","убакыт","жаратылыш","кыргыздар","тоолор"],
    hard: ["мамлекет","билим-берүү","маданият","экономика","технология","маалымат","байланыш","уюштуруу","мүмкүнчүлүк","изилдөө","университет","жетишкендик","өз алдынча","жооптуулук","кызматташуу","өнүгүү","мамилелер","демократия","конституция","революция","эл аралык","башкаруу","укук тартип","аймактар","калкы","маселеси","дипломатия","негиздер","принциптер","чечимдер"]
  },
  en: {
    easy: ["cat","dog","sun","sky","fire","tree","book","fish","bird","star","rain","moon","hand","road","home","king","fast","slow","kind","door","rock","lake","hill","wind","sand","leaf","cold","warm","real","good"],
    medium: ["water","earth","light","night","people","city","school","friend","power","music","dance","river","forest","family","beauty","wonder","health","energy","island","castle","flower","winter","summer","spring","travel","nature","planet","market","answer","reason"],
    hard: ["mountain","education","knowledge","government","technology","information","communication","organization","development","environment","international","responsibility","achievement","independence","university","experience","imagination","relationship","opportunity","understanding","administration","transportation","entertainment","conversation","professional","extraordinary","transformation","consideration","establishment","determination"]
  },
  uz: {
    easy: ["uy","qol","suv","yer","non","kun","tun","dos","tez","ot","tog'","ko'l","gul","yel","qor","yoz","til","xalq","tosh","yo'l"],
    medium: ["osmon","vaqt","hayot","kitob","maktab","do'stlik","yulduz","o'rmon","daryo","dengiz","quvonch","yurak","muhabbat","kiyim","fasl","odamlar","shahar","g'alaba","musiqa","baliq","qishloq","tabiat","bahor","yoz","kuz","qish","iqtisod","madaniyat","bilim","sog'liq"],
    hard: ["davlat","ta'lim","texnologiya","axborot","aloqa","tashkilot","imkoniyat","tadqiqot","universitet","yutuq","mustaqillik","hamkorlik","rivojlanish","munosabat","demokratiya","konstitutsiya","xalqaro","boshqaruv","javobgarlik","o'zaro munosabat","sanoat","qonunchilik","psixologik","falsafiy","matematikaviy","elektron","inqilob","muzokaralar","kuzatish","ishlab chiqarish"]
  },
  kk: {
    easy: ["үй","қол","су","жер","нан","күн","түн","дос","тез","ат","тау","көл","гүл","жел","қар","жаз","тіл","ел","тас","жол"],
    medium: ["аспан","уақыт","өмір","кітап","мектеп","достық","жұлдыз","орман","өзен","теңіз","қуаныш","жүрек","махаббат","киім","мезгіл","адамдар","қала","жеңіс","музыка","балық","ауыл","табиғат","көктем","жаз","күз","қыс","экономика","мәдениет","білім","денсаулық"],
    hard: ["мемлекет","білім беру","технология","ақпарат","байланыс","ұйымдастыру","мүмкіндік","зерттеу","университет","жетістік","тәуелсіздік","ынтымақтастық","даму","қатынас","демократия","конституция","халықаралық","басқару","жауапкершілік","өзара іс-қимыл","өнеркәсіп","заңнама","психологиялық","философиялық","математикалық","электрондық","революция","келіссөздер","бақылау","өндіріс"]
  }
};

// ===================================================
//  TRANSLATIONS — full UI in chosen language
// ===================================================
const T = {
  ru: {
    heroLine1:"Тренажёр", heroLine2:"СКОРОСТНОЙ ПЕЧАТИ",
    heroSub:"Соревнуйся с игроками СНГ. Выбери язык, уровень — и докажи, кто быстрее!",
    labelTypingLang:"Язык для печати:",
    modeEasyName:"ЛЁГКИЙ", modeMedName:"СРЕДНИЙ", modeHardName:"СЛОЖНЫЙ",
    modeEasyDesc:"5 минут, слова 3–7 букв. Очки не отнимаются. Идеально для начинающих.",
    modeMedDesc:"3 минуты, слова 5–10 букв. За каждую неправильную букву −30 очков.",
    modeHardDesc:"1 минута, слова 7–15+ букв. −50 очков за каждую ошибку. Только для лучших!",
    modeEasyT:"⏱ 5 минут", modeMedT:"⏱ 3 минуты", modeHardT:"⏱ 1 минута",
    modeEasyPen:"✅ Без штрафов", modeMedPen:"❌ −30 за ошибку", modeHardPen:"💀 −50 за ошибку",
    modeEasyChallenge:"Наберёшь 500 очков за 5 минут?", modeMedChallenge:"Наберёшь 1000 очков за 3 минуты?", modeHardChallenge:"Цель — 800 очков за 1 минуту. Сможешь?",
    scoreLabel:"ОЧКИ", timerLabel:"ВРЕМЯ", liveWPMLabel:"СЛОВ/МИН",
    liveAccLabel:"ТОЧНОСТЬ", liveWordsLabel:"СЛОВ",
    inputPlaceholder:"Начни печатать...",
    quitBtn:"← Выйти",
    navLB:"🏆 Рейтинг", navLogin:"Войти", navLogout:"Выйти",
    lbTitle:"🏆 РЕЙТИНГ СНГ", lbSub:"Лучшие игроки по скорости набора",
    lbColNick:"НИК", lbColWPM:"СКОРОСТЬ", lbColScore:"ОЧКИ", lbColLang:"ЯЗЫК", lbColMode:"РЕЖИМ",
    lbBack:"← Назад",
    resTitle:"📊 РЕЗУЛЬТАТ",
    resScoreL:"ОЧКИ", resWpmL:"СЛОВ/МИН", resAccL:"ТОЧНОСТЬ", resWordsL:"СЛОВ НАБРАНО",
    chartAccTitle:"ТОЧНОСТЬ НАБОРА", chartSpeedTitle:"СКОРОСТЬ ПО ВРЕМЕНИ (слов/мин)",
    correctLabel:"✅ Правильных", wrongLabel:"❌ Ошибок",
    btnAgain:"🔄 Снова", btnLB:"🏆 Рейтинг", btnHome:"🏠 Главная",
    countReady:"Готовься!",
    goodLuck:"Удачи! 🍀",
    authTitle:"ВХОД / РЕГИСТРАЦИЯ",
    tabLogin:"Вход", tabReg:"Регистрация",
    labelNick:"Никнейм", labelPass:"Пароль", labelPass2:"Подтверди пароль",
    placeholderNick:"Твой ник", placeholderNick2:"Например: SpeedKing_99",
    placeholderPass:"Пароль", placeholderPass2:"Минимум 6 символов", placeholderPass3:"Повтори пароль",
    btnLogin:"ВОЙТИ", btnRegister:"СОЗДАТЬ АККАУНТ",
    errLogin:"Неверный ник или пароль",
    errNickShort:"Минимум 3 символа", errNickTaken:"Этот ник уже занят",
    errPassMismatch:"Пароли не совпадают", errPassShort:"Минимум 6 символов",
    toastWelcome:"Добро пожаловать, ", toastLogout:"Вы вышли из аккаунта",
    toastCreated:"Аккаунт создан! Добро пожаловать, ",
    confirmLogout:"Выйти из аккаунта ",
    comment: {
      excellent: "Потрясающий результат! Ты настоящий чемпион клавиатуры! 🏆",
      good: "Отлично! Продолжай в том же духе! 💪",
      ok: "Неплохо, но есть куда расти. Тренируйся больше! 📈",
      poor: "Ничего страшного, продолжай тренироваться — всё получится! 😊"
    }
  },
  kg: {
    heroLine1:"Машыгуу", heroLine2:"ТЕЗ ТЕРҮҮНҮ ҮЙРӨН",
    heroSub:"СНГ оюнчулары менен аташ. Тилди, деңгээлди тандап — ким тезирээк экенин далилде!",
    labelTypingLang:"Терүү тили:",
    modeEasyName:"ЖЕҢИЛ", modeMedName:"ОРТО", modeHardName:"КЫЙЫН",
    modeEasyDesc:"5 мүнөт, 3–7 тамгалуу сөздөр. Очко алынбайт. Жаңы башталгандар үчүн.",
    modeMedDesc:"3 мүнөт, 5–10 тамгалуу сөздөр. Ар бир туура эмес тамга үчүн −30 очко.",
    modeHardDesc:"1 мүнөт, 7–15+ тамгалуу сөздөр. Ар бир ката үчүн −50 очко. Мыктылар үчүн!",
    modeEasyT:"⏱ 5 мүнөт", modeMedT:"⏱ 3 мүнөт", modeHardT:"⏱ 1 мүнөт",
    modeEasyPen:"✅ Айып жок", modeMedPen:"❌ −30 катадан", modeHardPen:"💀 −50 катадан",
    modeEasyChallenge:"5 мүнөт ичинде 500 очко топтой аласынбы?", modeMedChallenge:"3 мүнөт ичинде 1000 очко топтой аласынбы?", modeHardChallenge:"1 мүнөт ичинде 800 очко. Аракет кыласыңбы?",
    scoreLabel:"ОЧКО", timerLabel:"УБАКЫТ", liveWPMLabel:"СӨЗ/МИН",
    liveAccLabel:"ТАКТЫК", liveWordsLabel:"СӨЗ",
    inputPlaceholder:"Тере баштагыла...",
    quitBtn:"← Чыгуу",
    navLB:"🏆 Рейтинг", navLogin:"Кирүү", navLogout:"Чыгуу",
    lbTitle:"🏆 СНГ РЕЙТИНГИ", lbSub:"Эң тез терүүчүлөр",
    lbColNick:"НИК", lbColWPM:"ЫЛДАМДЫК", lbColScore:"ОЧКО", lbColLang:"ТИЛ", lbColMode:"ДЕҢГЭЭЛ",
    lbBack:"← Артка",
    resTitle:"📊 НАТЫЙЖА",
    resScoreL:"ОЧКО", resWpmL:"СӨЗ/МИН", resAccL:"ТАКТЫК", resWordsL:"ТЕРИЛГЕН СӨЗ",
    chartAccTitle:"ТЕРҮҮ ТАКТЫГЫ", chartSpeedTitle:"УБАКЫТКА ЖАРАША ЫЛДАМДЫК",
    correctLabel:"✅ Туура", wrongLabel:"❌ Каталар",
    btnAgain:"🔄 Кайра", btnLB:"🏆 Рейтинг", btnHome:"🏠 Башкы",
    countReady:"Даяр бол!",
    goodLuck:"Сизге ийгилик! 🍀",
    authTitle:"КИРҮҮ / КАТТАЛУУ",
    tabLogin:"Кирүү", tabReg:"Катталуу",
    labelNick:"Никнейм", labelPass:"Сырсөз", labelPass2:"Сырсөздү ырастоо",
    placeholderNick:"Сенин никтин", placeholderNick2:"Мисалы: TezTermeci_99",
    placeholderPass:"Сырсөз", placeholderPass2:"Минимум 6 белги", placeholderPass3:"Сырсөздү кайталоо",
    btnLogin:"КИРҮҮ", btnRegister:"АККАУНТ ТҮЗҮҮ",
    errLogin:"Ник же сырсөз туура эмес",
    errNickShort:"Минимум 3 белги", errNickTaken:"Бул ник буга чейин алынган",
    errPassMismatch:"Сырсөздөр дал келбейт", errPassShort:"Минимум 6 белги",
    toastWelcome:"Кош келиңиз, ", toastLogout:"Аккаунттан чыктыңыз",
    toastCreated:"Аккаунт түзүлдү! Кош келиңиз, ",
    confirmLogout:"Аккаунттан чыгасызбы? ",
    comment: {
      excellent: "Укмуштуу! Сен чыныгы клавиатура чемпионусуң! 🏆",
      good: "Жакшы! Ошентип улантавер! 💪",
      ok: "Анча эмес, бирок капа болбо, дагы да машыгып аракет кылсаң ийгиликке жетесиң! 📈",
      poor: "Эч нерсе эмес, машыгуун улантсаң баары жакшы болот! 😊"
    }
  },
  en: {
    heroLine1:"Trainer", heroLine2:"SPEED TYPING",
    heroSub:"Compete with CIS players. Choose language, level — and prove who's faster!",
    labelTypingLang:"Typing language:",
    modeEasyName:"EASY", modeMedName:"MEDIUM", modeHardName:"HARD",
    modeEasyDesc:"5 minutes, words 3–7 letters. No penalties. Perfect for beginners.",
    modeMedDesc:"3 minutes, words 5–10 letters. −30 points per wrong letter.",
    modeHardDesc:"1 minute, words 7–15+ letters. −50 points per mistake. Experts only!",
    modeEasyT:"⏱ 5 minutes", modeMedT:"⏱ 3 minutes", modeHardT:"⏱ 1 minute",
    modeEasyPen:"✅ No penalty", modeMedPen:"❌ −30 per error", modeHardPen:"💀 −50 per error",
    modeEasyChallenge:"Can you score 500 points in 5 minutes?", modeMedChallenge:"Can you score 1000 points in 3 minutes?", modeHardChallenge:"Goal: 800 points in 1 minute. Challenge accepted?",
    scoreLabel:"SCORE", timerLabel:"TIME", liveWPMLabel:"WPM",
    liveAccLabel:"ACCURACY", liveWordsLabel:"WORDS",
    inputPlaceholder:"Start typing...",
    quitBtn:"← Quit",
    navLB:"🏆 Leaderboard", navLogin:"Login", navLogout:"Logout",
    lbTitle:"🏆 CIS LEADERBOARD", lbSub:"Top typists by speed",
    lbColNick:"NICK", lbColWPM:"SPEED", lbColScore:"SCORE", lbColLang:"LANG", lbColMode:"MODE",
    lbBack:"← Back",
    resTitle:"📊 RESULT",
    resScoreL:"SCORE", resWpmL:"WPM", resAccL:"ACCURACY", resWordsL:"WORDS TYPED",
    chartAccTitle:"TYPING ACCURACY", chartSpeedTitle:"SPEED OVER TIME (wpm)",
    correctLabel:"✅ Correct", wrongLabel:"❌ Errors",
    btnAgain:"🔄 Again", btnLB:"🏆 Leaderboard", btnHome:"🏠 Home",
    countReady:"Get ready!",
    goodLuck:"Good luck! 🍀",
    authTitle:"LOGIN / REGISTER",
    tabLogin:"Login", tabReg:"Register",
    labelNick:"Nickname", labelPass:"Password", labelPass2:"Confirm password",
    placeholderNick:"Your nick", placeholderNick2:"Example: SpeedKing_99",
    placeholderPass:"Password", placeholderPass2:"Min 6 characters", placeholderPass3:"Repeat password",
    btnLogin:"LOGIN", btnRegister:"CREATE ACCOUNT",
    errLogin:"Wrong nickname or password",
    errNickShort:"Minimum 3 characters", errNickTaken:"This nickname is already taken",
    errPassMismatch:"Passwords don't match", errPassShort:"Minimum 6 characters",
    toastWelcome:"Welcome, ", toastLogout:"You have logged out",
    toastCreated:"Account created! Welcome, ",
    confirmLogout:"Log out of account ",
    comment: {
      excellent: "Amazing! You're a true keyboard champion! 🏆",
      good: "Great result! Keep it up! 💪",
      ok: "Not bad, but there's room to grow. Keep practicing! 📈",
      poor: "Don't worry, keep training — you'll get there! 😊"
    }
  },
  uz: {
    heroLine1:"Mashg'ulot", heroLine2:"TEZ YOZISHNI O'RGAN",
    heroSub:"MDH o'yinchilari bilan bellashing. Til va daraja tanlang — kim tezligini isbot qiling!",
    labelTypingLang:"Yozish tili:",
    modeEasyName:"OSON", modeMedName:"O'RTA", modeHardName:"QIYIN",
    modeEasyDesc:"5 daqiqa, 3–7 harfli so'zlar. Jarima yo'q. Boshluvchilar uchun ideal.",
    modeMedDesc:"3 daqiqa, 5–10 harfli so'zlar. Har noto'g'ri harf uchun −30 ball.",
    modeHardDesc:"1 daqiqa, 7–15+ harfli so'zlar. Har xato uchun −50 ball. Faqat eng yaxshilar!",
    modeEasyT:"⏱ 5 daqiqa", modeMedT:"⏱ 3 daqiqa", modeHardT:"⏱ 1 daqiqa",
    modeEasyPen:"✅ Jarimasisz", modeMedPen:"❌ −30 xato uchun", modeHardPen:"💀 −50 xato uchun",
    modeEasyChallenge:"5 daqiqada 500 ball to'play olasizmi?", modeMedChallenge:"3 daqiqada 1000 ball to'play olasizmi?", modeHardChallenge:"Maqsad: 1 daqiqada 800 ball. Qabul qilasizmi?",
    scoreLabel:"BALL", timerLabel:"VAQT", liveWPMLabel:"SO'Z/MIN",
    liveAccLabel:"ANIQLIK", liveWordsLabel:"SO'Z",
    inputPlaceholder:"Yoza boshlang...",
    quitBtn:"← Chiqish",
    navLB:"🏆 Reyting", navLogin:"Kirish", navLogout:"Chiqish",
    lbTitle:"🏆 MDH REYTINGI", lbSub:"Eng tez yozuvchilar",
    lbColNick:"NIK", lbColWPM:"TEZLIK", lbColScore:"BALL", lbColLang:"TIL", lbColMode:"DARAJA",
    lbBack:"← Orqaga",
    resTitle:"📊 NATIJA",
    resScoreL:"BALL", resWpmL:"SO'Z/MIN", resAccL:"ANIQLIK", resWordsL:"YOZILGAN SO'Z",
    chartAccTitle:"YOZISH ANIQLIGI", chartSpeedTitle:"VAQT BO'YICHA TEZLIK",
    correctLabel:"✅ To'g'ri", wrongLabel:"❌ Xatolar",
    btnAgain:"🔄 Qayta", btnLB:"🏆 Reyting", btnHome:"🏠 Bosh",
    countReady:"Tayyor bo'l!",
    goodLuck:"Omad tilayman! 🍀",
    authTitle:"KIRISH / RO'YXATDAN O'TISH",
    tabLogin:"Kirish", tabReg:"Ro'yxatdan o'tish",
    labelNick:"Taxallus", labelPass:"Parol", labelPass2:"Parolni tasdiqlash",
    placeholderNick:"Sizning nikiniz", placeholderNick2:"Masalan: FastHands_99",
    placeholderPass:"Parol", placeholderPass2:"Kamida 6 belgi", placeholderPass3:"Parolni takrorlang",
    btnLogin:"KIRISH", btnRegister:"HISOB YARATISH",
    errLogin:"Noto'g'ri taxallus yoki parol",
    errNickShort:"Kamida 3 belgi", errNickTaken:"Bu taxallus band",
    errPassMismatch:"Parollar mos kelmaydi", errPassShort:"Kamida 6 belgi",
    toastWelcome:"Xush kelibsiz, ", toastLogout:"Hisobdan chiqdingiz",
    toastCreated:"Hisob yaratildi! Xush kelibsiz, ",
    confirmLogout:"Hisobdan chiqish? ",
    comment: {
      excellent: "Ajoyib! Siz haqiqiy klaviatura chempionisiz! 🏆",
      good: "Zo'r natija! Shunday davom eting! 💪",
      ok: "Yomon emas, lekin o'sish uchun joy bor. Ko'proq mashq qiling! 📈",
      poor: "Xavotir olmasin, mashq davom ettirsangiz hammasi yaxshi bo'ladi! 😊"
    }
  },
  kk: {
    heroLine1:"Жаттықтырғыш", heroLine2:"ТЕЗ ТЕРУДІ ҮЙРЕН",
    heroSub:"ТМД ойыншыларымен жарысыңыз. Тіл мен деңгейді таңдаңыз — кім жылдамды дәлелдеңіз!",
    labelTypingLang:"Теру тілі:",
    modeEasyName:"ОҢАЙ", modeMedName:"ОРТАША", modeHardName:"ҚИЫН",
    modeEasyDesc:"5 минут, 3–7 әріпті сөздер. Айып жоқ. Жаңадан бастаушылар үшін.",
    modeMedDesc:"3 минут, 5–10 әріпті сөздер. Әр қате әріп үшін −30 ұпай.",
    modeHardDesc:"1 минут, 7–15+ әріпті сөздер. Әр қате үшін −50 ұпай. Тек үздіктер!",
    modeEasyT:"⏱ 5 минут", modeMedT:"⏱ 3 минут", modeHardT:"⏱ 1 минут",
    modeEasyPen:"✅ Айыпсыз", modeMedPen:"❌ −30 қате үшін", modeHardPen:"💀 −50 қате үшін",
    modeEasyChallenge:"5 минутта 500 ұпай жинай аласыз ба?", modeMedChallenge:"3 минутта 1000 ұпай жинай аласыз ба?", modeHardChallenge:"Мақсат: 1 минутта 800 ұпай. Қабылдайсыз ба?",
    scoreLabel:"ҰПАЙ", timerLabel:"УАҚЫТ", liveWPMLabel:"СӨЗ/МИН",
    liveAccLabel:"ДӘЛДІК", liveWordsLabel:"СӨЗ",
    inputPlaceholder:"Тере бастаңыз...",
    quitBtn:"← Шығу",
    navLB:"🏆 Рейтинг", navLogin:"Кіру", navLogout:"Шығу",
    lbTitle:"🏆 ТМД РЕЙТИНГІ", lbSub:"Ең жылдам теруші ойыншылар",
    lbColNick:"НИК", lbColWPM:"ЖЫЛДАМДЫҚ", lbColScore:"ҰПАЙ", lbColLang:"ТІЛ", lbColMode:"ДЕҢГЕЙ",
    lbBack:"← Артқа",
    resTitle:"📊 НӘТИЖЕ",
    resScoreL:"ҰПАЙ", resWpmL:"СӨЗ/МИН", resAccL:"ДӘЛДІК", resWordsL:"ТЕРІЛГЕН СӨЗ",
    chartAccTitle:"ТЕРУДІҢ ДӘЛДІГІ", chartSpeedTitle:"УАҚЫТҚА БАЙЛАНЫСТЫ ЖЫЛДАМДЫҚ",
    correctLabel:"✅ Дұрыс", wrongLabel:"❌ Қателер",
    btnAgain:"🔄 Қайта", btnLB:"🏆 Рейтинг", btnHome:"🏠 Басты",
    countReady:"Дайын бол!",
    goodLuck:"Сәттілік! 🍀",
    authTitle:"КІРУ / ТІРКЕЛУ",
    tabLogin:"Кіру", tabReg:"Тіркелу",
    labelNick:"Лақап ат", labelPass:"Құпиясөз", labelPass2:"Құпиясөзді растау",
    placeholderNick:"Сіздің лақап атыңыз", placeholderNick2:"Мысалы: JylдamTeruши_99",
    placeholderPass:"Құпиясөз", placeholderPass2:"Кемінде 6 таңба", placeholderPass3:"Құпиясөзді қайталаңыз",
    btnLogin:"КІРУ", btnRegister:"АККАУНТ ЖАСАУ",
    errLogin:"Лақап ат немесе құпиясөз қате",
    errNickShort:"Кемінде 3 таңба", errNickTaken:"Бұл лақап ат алынған",
    errPassMismatch:"Құпиясөздер сәйкес емес", errPassShort:"Кемінде 6 таңба",
    toastWelcome:"Қош келдіңіз, ", toastLogout:"Аккаунттан шықтыңыз",
    toastCreated:"Аккаунт жасалды! Қош келдіңіз, ",
    confirmLogout:"Аккаунттан шығасыз ба? ",
    comment: {
      excellent: "Керемет! Сіз нағыз пернетақта чемпионысыз! 🏆",
      good: "Тамаша нәтиже! Осылай жалғастыра беріңіз! 💪",
      ok: "Жаман емес, бірақ өсу орны бар. Көбірек жаттық! 📈",
      poor: "Алаңдамаңыз, жаттыға берсеңіз бәрі жақсы болады! 😊"
    }
  }
};

// ===================================================
//  GAME STATE
// ===================================================
const MODES = {
  easy:   { time: 300, penalty: 0,  bonusMulti: 1 },
  medium: { time: 180, penalty: 30, bonusMulti: 1 },
  hard:   { time: 60,  penalty: 50, bonusMulti: 1 }
};

let state = {
  screen: 'home',
  uiLang: 'ru',
  typingLang: 'ru',
  mode: 'easy',
  score: 0,
  timeLeft: 300,
  timerInterval: null,
  currentWord: '',
  wordQueue: [],
  wordsTyped: 0,
  correctChars: 0,
  wrongChars: 0,
  startTime: null,
  speedSamples: [],
  sampleInterval: null,
  gameActive: false
};

// localStorage mock users (in real app use backend)
let users = JSON.parse(localStorage.getItem('typerace_users') || '{}');
let leaderboard = JSON.parse(localStorage.getItem('typerace_lb') || '[]');
let currentUser = JSON.parse(localStorage.getItem('typerace_current') || 'null');

// Seed leaderboard if empty
if (leaderboard.length === 0) {
  leaderboard = [
    {nick:'SpeedKing_99',wpm:112,score:15400,lang:'ru',mode:'hard'},
    {nick:'КлавиатураМастер',wpm:98,score:12200,lang:'ru',mode:'medium'},
    {nick:'TezTermeci',wpm:87,score:10500,lang:'kg',mode:'hard'},
    {nick:'FastHands_UZ',wpm:82,score:9800,lang:'uz',mode:'medium'},
    {nick:'Жылдам_Тулпар',wpm:79,score:9100,lang:'kk',mode:'medium'},
    {nick:'TypeRacer_EN',wpm:105,score:8900,lang:'en',mode:'hard'},
    {nick:'ПечатьПро',wpm:74,score:7600,lang:'ru',mode:'easy'},
    {nick:'KeyboardNinja',wpm:91,score:11200,lang:'en',mode:'hard'},
    {nick:'Асель_КЗ',wpm:68,score:6800,lang:'kk',mode:'easy'},
    {nick:'ТаянычUZ',wpm:72,score:7200,lang:'uz',mode:'medium'},
  ];
  saveLeaderboard();
}

function saveLeaderboard() {
  localStorage.setItem('typerace_lb', JSON.stringify(leaderboard));
}

// ===================================================
//  UI LANGUAGE
// ===================================================
function changeUILang(lang) {
  state.uiLang = lang;
  applyTranslations();
}

function applyTranslations() {
  const t = T[state.uiLang];
  document.getElementById('hero-line1').textContent = t.heroLine1;
  document.getElementById('hero-line2').textContent = t.heroLine2;
  document.getElementById('hero-sub').textContent = t.heroSub;
  document.getElementById('label-typing-lang').textContent = t.labelTypingLang;
  document.getElementById('mode-easy-name').textContent = t.modeEasyName;
  document.getElementById('mode-med-name').textContent = t.modeMedName;
  document.getElementById('mode-hard-name').textContent = t.modeHardName;
  document.getElementById('mode-easy-desc').textContent = t.modeEasyDesc;
  document.getElementById('mode-med-desc').textContent = t.modeMedDesc;
  document.getElementById('mode-hard-desc').textContent = t.modeHardDesc;
  document.getElementById('mode-easy-t').textContent = t.modeEasyT;
  document.getElementById('mode-med-t').textContent = t.modeMedT;
  document.getElementById('mode-hard-t').textContent = t.modeHardT;
  document.getElementById('mode-easy-pen').textContent = t.modeEasyPen;
  document.getElementById('mode-med-pen').textContent = t.modeMedPen;
  document.getElementById('mode-hard-pen').textContent = t.modeHardPen;
  document.getElementById('scoreLabel').textContent = t.scoreLabel;
  document.getElementById('timerLabel').textContent = t.timerLabel;
  document.getElementById('liveWPMLabel').textContent = t.liveWPMLabel;
  document.getElementById('liveAccLabel').textContent = t.liveAccLabel;
  document.getElementById('liveWordsLabel').textContent = t.liveWordsLabel;
  document.getElementById('quitBtn').textContent = t.quitBtn;
  document.getElementById('nav-lb').textContent = t.navLB;
  document.getElementById('nav-login').textContent = currentUser ? currentUser.nick : t.navLogin;
  document.getElementById('lb-title').textContent = t.lbTitle;
  document.getElementById('lb-sub').textContent = t.lbSub;
  document.getElementById('lb-col-nick').textContent = t.lbColNick;
  document.getElementById('lb-col-wpm').textContent = t.lbColWPM;
  document.getElementById('lb-col-score').textContent = t.lbColScore;
  document.getElementById('lb-col-lang').textContent = t.lbColLang;
  document.getElementById('lb-col-mode').textContent = t.lbColMode;
  document.getElementById('lb-back').textContent = t.lbBack;
  document.getElementById('res-score-l').textContent = t.resScoreL;
  document.getElementById('res-wpm-l').textContent = t.resWpmL;
  document.getElementById('res-acc-l').textContent = t.resAccL;
  document.getElementById('res-words-l').textContent = t.resWordsL;
  document.getElementById('chart-acc-title').textContent = t.chartAccTitle;
  document.getElementById('chart-speed-title').textContent = t.chartSpeedTitle;
  document.getElementById('correct-label').textContent = t.correctLabel;
  document.getElementById('wrong-label').textContent = t.wrongLabel;
  document.getElementById('btn-again').textContent = t.btnAgain;
  document.getElementById('btn-lb').textContent = t.btnLB;
  document.getElementById('btn-home').textContent = t.btnHome;
}

// ===================================================
//  SCREENS
// ===================================================
function showScreen(name) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById('screen-' + name).classList.add('active');
  state.screen = name;
  if (name === 'leaderboard') renderLeaderboard();
}

// ===================================================
//  GAME FLOW
// ===================================================
function startGame(mode) {
  state.mode = mode;
  state.typingLang = document.getElementById('typingLang').value;
  state.score = 0;
  state.timeLeft = MODES[mode].time;
  state.wordsTyped = 0;
  state.correctChars = 0;
  state.wrongChars = 0;
  state.speedSamples = [];
  state.gameActive = false;

  // Build word queue
  const bank = [...WORDS[state.typingLang]];
  state.wordQueue = [];
  for (let i = 0; i < 200; i++) {
    state.wordQueue.push(bank[Math.floor(Math.random() * bank.length)]);
  }

  showScreen('game');
  updateTimerDisplay();
  document.getElementById('scoreDisplay').textContent = '0';
  document.getElementById('progressFill').style.width = '100%';

  const modeNames = {
    easy: T[state.uiLang].modeEasyName,
    medium: T[state.uiLang].modeMedName,
    hard: T[state.uiLang].modeHardName
  };
  const langNames = {ru:'🇷🇺 Русский',kg:'🇰🇬 Кыргызча',en:'🇺🇸 English',uz:'🇺🇿 O\'zbekcha',kk:'🇰🇿 Қазақша'};
  document.getElementById('modeLabel').textContent = modeNames[mode];
  document.getElementById('langLabel').textContent = langNames[state.typingLang];

  document.getElementById('typingInput').value = '';
  document.getElementById('typingInput').className = 'typing-input';

  startCountdown();
}

function startCountdown() {
  const overlay = document.getElementById('countdownOverlay');
  const numEl = document.getElementById('countdownNum');
  const msgEl = document.getElementById('countdownMsg');
  overlay.classList.add('show');
  msgEl.textContent = T[state.uiLang].countReady;

  let count = 3;
  numEl.textContent = count;

  const cd = setInterval(() => {
    count--;
    if (count > 0) {
      numEl.textContent = count;
      numEl.style.animation = 'none';
      void numEl.offsetWidth;
      numEl.style.animation = 'countAnim 0.8s ease-out';
    } else {
      overlay.classList.remove('show');
      clearInterval(cd);
      beginGame();
    }
  }, 1000);
}

function beginGame() {
  state.gameActive = true;
  state.startTime = Date.now();
  nextWord();
  document.getElementById('typingInput').focus();

  state.timerInterval = setInterval(() => {
    if (!state.gameActive) return;
    state.timeLeft--;
    updateTimerDisplay();

    const total = MODES[state.mode].time;
    document.getElementById('progressFill').style.width = (state.timeLeft / total * 100) + '%';

    // Speed sample every 10 seconds
    if (state.timeLeft % 10 === 0) {
      const elapsed = (Date.now() - state.startTime) / 60000;
      const wpm = elapsed > 0 ? Math.round(state.wordsTyped / elapsed) : 0;
      state.speedSamples.push(wpm);
    }

    // Update live stats
    const elapsed = (Date.now() - state.startTime) / 60000;
    const wpm = elapsed > 0.01 ? Math.round(state.wordsTyped / elapsed) : 0;
    document.getElementById('liveWPM').textContent = wpm;
    const total_chars = state.correctChars + state.wrongChars;
    const acc = total_chars > 0 ? Math.round(state.correctChars / total_chars * 100) : 100;
    document.getElementById('liveAcc').textContent = acc + '%';
    document.getElementById('liveWords').textContent = state.wordsTyped;

    if (state.timeLeft <= 0) endGame();

    // Timer color
    const timerEl = document.getElementById('timerDisplay');
    if (state.timeLeft <= 10) { timerEl.className = 'timer-display danger'; }
    else if (state.timeLeft <= MODES[state.mode].time * 0.3) { timerEl.className = 'timer-display warning'; }
    else { timerEl.className = 'timer-display'; }

  }, 1000);
}

function updateTimerDisplay() {
  const m = Math.floor(state.timeLeft / 60);
  const s = state.timeLeft % 60;
  document.getElementById('timerDisplay').textContent = m + ':' + String(s).padStart(2, '0');
}

function nextWord() {
  state.currentWord = state.wordQueue.shift();
  if (state.wordQueue.length < 20) {
    const bank = [...WORDS[state.typingLang]];
    for (let i = 0; i < 50; i++) state.wordQueue.push(bank[Math.floor(Math.random() * bank.length)]);
  }
  renderWordDisplay('');
  renderNextWords();
}

function renderWordDisplay(typed) {
  const word = state.currentWord;
  const display = document.getElementById('wordDisplay');
  let html = '';
  for (let i = 0; i < word.length; i++) {
    if (i < typed.length) {
      if (typed[i] === word[i]) html += `<span class="char correct">${word[i]}</span>`;
      else html += `<span class="char wrong">${word[i]}</span>`;
    } else if (i === typed.length) {
      html += `<span class="char current">${word[i]}</span>`;
    } else {
      html += `<span class="char pending">${word[i]}</span>`;
    }
  }
  display.innerHTML = html;
}

function renderNextWords() {
  const el = document.getElementById('nextWords');
  el.innerHTML = state.wordQueue.slice(0, 5).map(w => `<span class="next-word">${w}</span>`).join('');
}

// Input handling
document.getElementById('typingInput').addEventListener('input', function(e) {
  if (!state.gameActive) return;
  const typed = this.value;
  const word = state.currentWord;

  renderWordDisplay(typed);

  // Check each character for penalty
  if (typed.length > 0 && typed.length <= word.length) {
    const lastChar = typed[typed.length - 1];
    const expectedChar = word[typed.length - 1];
    if (lastChar !== expectedChar) {
      // Wrong character
      state.wrongChars++;
      if (state.mode !== 'easy') {
        const pen = MODES[state.mode].penalty;
        state.score = Math.max(0, state.score - pen);
        document.getElementById('scoreDisplay').textContent = state.score;
        showScorePopup(-pen);
      }
      this.className = 'typing-input wrong-state';
    } else {
      state.correctChars++;
      this.className = 'typing-input correct-state';
    }
  }

  // Word completed (space or exact match)
  if (typed.endsWith(' ') || typed === word) {
    const typedWord = typed.trim();
    const wordTime = (Date.now() - (this._wordStart || state.startTime)) / 1000;
    this._wordStart = Date.now();

    let bonus = 0;
    if (typedWord === word) {
      if (wordTime <= 3) bonus = 200;
      else if (wordTime <= 5) bonus = 100;
      else bonus = 50;
      state.score += bonus;
      state.wordsTyped++;
      showScorePopup(+bonus);
    }

    document.getElementById('scoreDisplay').textContent = state.score;
    this.value = '';
    this.className = 'typing-input';
    nextWord();
  }
});

document.getElementById('typingInput').addEventListener('keydown', function(e) {
  if (!this._wordStart) this._wordStart = Date.now();
});

function showScorePopup(val) {
  const input = document.getElementById('typingInput');
  const rect = input.getBoundingClientRect();
  const popup = document.createElement('div');
  popup.className = 'score-popup ' + (val > 0 ? 'positive' : 'negative');
  popup.textContent = (val > 0 ? '+' : '') + val;
  popup.style.left = (rect.left + rect.width / 2 - 30) + 'px';
  popup.style.top = (rect.top - 20) + 'px';
  document.body.appendChild(popup);
  setTimeout(() => popup.remove(), 1000);
}

function quitGame() {
  clearInterval(state.timerInterval);
  state.gameActive = false;
  showScreen('home');
}

function endGame() {
  clearInterval(state.timerInterval);
  state.gameActive = false;

  const elapsed = MODES[state.mode].time / 60;
  const wpm = Math.round(state.wordsTyped / elapsed);
  const totalChars = state.correctChars + state.wrongChars;
  const accuracy = totalChars > 0 ? Math.round(state.correctChars / totalChars * 100) : 100;

  // Save to leaderboard if user logged in
  if (currentUser) {
    leaderboard.push({
      nick: currentUser.nick,
      wpm, score: state.score,
      lang: state.typingLang,
      mode: state.mode
    });
    leaderboard.sort((a,b) => b.wpm - a.wpm);
    leaderboard = leaderboard.slice(0, 100);
    saveLeaderboard();
  }

  showResults(wpm, accuracy, wpm > 0 ? Math.round(state.wordsTyped / (wpm / wpm)) : state.wordsTyped);
}

function showResults(wpm, accuracy, wordsTyped) {
  showScreen('results');
  const t = T[state.uiLang];

  document.getElementById('res-score').textContent = state.score;
  document.getElementById('res-wpm').textContent = wpm;
  document.getElementById('res-acc').textContent = accuracy + '%';
  document.getElementById('res-words').textContent = state.wordsTyped;

  // Comment
  let commentKey = 'poor';
  if (wpm >= 80) commentKey = 'excellent';
  else if (wpm >= 50) commentKey = 'good';
  else if (wpm >= 30) commentKey = 'ok';
  document.getElementById('resultComment').textContent = t.comment[commentKey];
  document.getElementById('resultTitle').textContent = wpm >= 50 ? '🎉 ' + (t.resScoreL === 'ОЧКИ' ? 'Результат' : 'Result') : '📊 ' + (t.resScoreL === 'ОЧКИ' ? 'Результат' : 'Result');

  // Accuracy bar
  const correctPct = accuracy;
  const wrongPct = 100 - accuracy;
  document.getElementById('accCorrectBar').style.width = correctPct + '%';
  document.getElementById('accWrongBar').style.width = wrongPct + '%';
  document.getElementById('accCorrectPct').textContent = correctPct + '%';
  document.getElementById('accWrongPct').textContent = wrongPct + '%';
  document.getElementById('correctCount').textContent = state.correctChars + ' ' + (t.correctLabel.replace(/[✅❌]\s/,''));
  document.getElementById('wrongCount').textContent = state.wrongChars + ' ' + (t.wrongLabel.replace(/[✅❌]\s/,''));

  // Speed chart
  const chartEl = document.getElementById('speedChart');
  const samples = state.speedSamples.length > 0 ? state.speedSamples : [wpm];
  const maxWpm = Math.max(...samples, 1);
  chartEl.innerHTML = samples.map((s, i) => {
    const h = Math.max(8, Math.round(s / maxWpm * 100));
    const color = s >= 80 ? 'var(--green)' : s >= 40 ? 'var(--accent)' : 'var(--yellow)';
    return `<div class="bar-item">
      <div class="bar-val" style="color:${color};font-size:10px;">${s}</div>
      <div class="bar" style="height:${h}px;background:${color};"></div>
      <div class="bar-label">${(i+1)*10}s</div>
    </div>`;
  }).join('');
}

function restartGame() {
  startGame(state.mode);
}

// ===================================================
//  LEADERBOARD
// ===================================================
function renderLeaderboard() {
  const langF = document.getElementById('lbLangFilter').value;
  const modeF = document.getElementById('lbModeFilter').value;
  let data = leaderboard.filter(e =>
    (langF === 'all' || e.lang === langF) &&
    (modeF === 'all' || e.mode === modeF)
  );
  data = data.sort((a,b) => b.wpm - a.wpm).slice(0, 20);

  const langFlags = {ru:'🇷🇺',kg:'🇰🇬',en:'🇺🇸',uz:'🇺🇿',kk:'🇰🇿'};
  const modeNames = {easy:'🌱',medium:'⚡',hard:'🔥'};
  const tbody = document.getElementById('lbBody');
  tbody.innerHTML = data.map((e, i) => {
    const isYou = currentUser && e.nick === currentUser.nick;
    const rankClass = i === 0 ? 'rank-1' : i === 1 ? 'rank-2' : i === 2 ? 'rank-3' : '';
    return `<tr class="${isYou ? 'you-row' : ''}">
      <td><span class="rank-num ${rankClass}">${i+1}</span></td>
      <td><span class="nick">${e.nick}</span>${isYou ? '<span class="you-badge">YOU</span>' : ''}</td>
      <td><span class="wpm-val">${e.wpm} wpm</span></td>
      <td>${e.score}</td>
      <td><span class="lang-badge">${langFlags[e.lang] || ''} ${e.lang.toUpperCase()}</span></td>
      <td>${modeNames[e.mode] || ''}</td>
    </tr>`;
  }).join('');
}

// ===================================================
//  AUTH
// ===================================================
function openAuth() {
  if (currentUser) {
    // Show user menu / logout
    if (confirm('Выйти из аккаунта ' + currentUser.nick + '?')) {
      currentUser = null;
      localStorage.removeItem('typerace_current');
      updateAuthUI();
      showToast('Вы вышли из аккаунта', 'success');
    }
    return;
  }
  document.getElementById('authModal').classList.add('show');
}

function closeAuth() {
  document.getElementById('authModal').classList.remove('show');
  clearAuthErrors();
}

function switchTab(tab) {
  document.getElementById('loginForm').style.display = tab === 'login' ? 'block' : 'none';
  document.getElementById('regForm').style.display = tab === 'register' ? 'block' : 'none';
  document.getElementById('tab-login').className = 'auth-tab' + (tab === 'login' ? ' active' : '');
  document.getElementById('tab-reg').className = 'auth-tab' + (tab === 'register' ? ' active' : '');
  clearAuthErrors();
}

function clearAuthErrors() {
  ['loginError','regNickError','regPassError'].forEach(id => {
    document.getElementById(id).style.display = 'none';
  });
}

function doLogin() {
  const nick = document.getElementById('loginNick').value.trim();
  const pass = document.getElementById('loginPass').value;
  if (!nick || !pass) return;

  const user = users[nick.toLowerCase()];
  if (!user || user.pass !== btoa(pass)) {
    document.getElementById('loginError').style.display = 'block';
    return;
  }
  currentUser = { nick: user.nick };
  localStorage.setItem('typerace_current', JSON.stringify(currentUser));
  closeAuth();
  updateAuthUI();
  showToast('Добро пожаловать, ' + currentUser.nick + '! 🎉', 'success');
}

function doRegister() {
  const nick = document.getElementById('regNick').value.trim();
  const pass = document.getElementById('regPass').value;
  const pass2 = document.getElementById('regPass2').value;

  if (!nick || nick.length < 3) {
    document.getElementById('regNickError').textContent = 'Минимум 3 символа';
    document.getElementById('regNickError').style.display = 'block';
    return;
  }
  if (users[nick.toLowerCase()]) {
    document.getElementById('regNickError').textContent = 'Этот ник уже занят';
    document.getElementById('regNickError').style.display = 'block';
    return;
  }
  if (pass !== pass2) {
    document.getElementById('regPassError').style.display = 'block';
    return;
  }
  if (pass.length < 6) {
    document.getElementById('regPassError').textContent = 'Минимум 6 символов';
    document.getElementById('regPassError').style.display = 'block';
    return;
  }

  users[nick.toLowerCase()] = { nick, pass: btoa(pass) };
  localStorage.setItem('typerace_users', JSON.stringify(users));

  currentUser = { nick };
  localStorage.setItem('typerace_current', JSON.stringify(currentUser));
  closeAuth();
  updateAuthUI();
  showToast('Аккаунт создан! Добро пожаловать, ' + nick + '! 🎉', 'success');
}

function updateAuthUI() {
  const authArea = document.getElementById('authArea');
  if (currentUser) {
    const initials = currentUser.nick.slice(0,2).toUpperCase();
    authArea.innerHTML = `
      <div class="user-info" onclick="openAuth()" style="cursor:pointer;">
        <div class="avatar">${initials}</div>
        <div>
          <div class="user-nick">${currentUser.nick}</div>
          <div class="user-score">Выйти</div>
        </div>
      </div>`;
  } else {
    authArea.innerHTML = `<button class="nav-btn primary" onclick="openAuth()" id="nav-login">${T[state.uiLang].navLogin}</button>`;
  }
}

// ===================================================
//  TOAST
// ===================================================
function showToast(msg, type = '') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast ' + type;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

// Close modal on overlay click
document.getElementById('authModal').addEventListener('click', function(e) {
  if (e.target === this) closeAuth();
});

// ===================================================
//  INIT
// ===================================================
if (currentUser) updateAuthUI();
applyTranslations();
</script>
</body>
</html>
