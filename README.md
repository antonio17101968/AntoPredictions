# AntoPredictions

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AntoPredictions — O Futuro É Previsível</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
:root{
  --black:#050507;--black2:#0a0a0f;--surface:#111118;--surface2:#18181f;
  --border:rgba(255,255,255,0.06);--border2:rgba(255,255,255,0.12);
  --cyan:#00f5d4;--cyan2:#00c4aa;--cyan-dim:rgba(0,245,212,0.06);
  --red:#ff6b6b;--white:#ffffff;--gray:#9898a8;--gray2:#5a5a6e;
}
html{scroll-behavior:smooth;}
body{font-family:'Space Grotesk',sans-serif;background:var(--black);color:var(--white);overflow-x:hidden;cursor:none;}
.cursor{position:fixed;width:10px;height:10px;background:var(--cyan);border-radius:50%;pointer-events:none;z-index:9999;transition:transform 0.15s ease;mix-blend-mode:difference;}
.cursor-ring{position:fixed;width:36px;height:36px;border:1px solid rgba(0,245,212,0.4);border-radius:50%;pointer-events:none;z-index:9998;transition:all 0.25s ease;transform:translate(-13px,-13px);}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(0,245,212,0.025) 1px,transparent 1px),linear-gradient(90deg,rgba(0,245,212,0.025) 1px,transparent 1px);background-size:60px 60px;pointer-events:none;z-index:0;}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:100;display:flex;align-items:center;justify-content:space-between;padding:1.25rem 3rem;background:rgba(5,5,7,0.85);backdrop-filter:blur(20px);border-bottom:1px solid var(--border);}
.logo{font-family:'Space Mono',monospace;font-size:1.1rem;color:var(--white);letter-spacing:0.05em;text-decoration:none;display:flex;align-items:center;gap:0.5rem;}
.logo-bracket{color:var(--cyan);}
.logo-dot{width:6px;height:6px;background:var(--cyan);border-radius:50%;animation:blink 1.5s step-end infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:0;}}
nav ul{display:flex;list-style:none;gap:2.5rem;align-items:center;}
nav ul a{font-size:0.8rem;font-weight:500;color:var(--gray);text-decoration:none;letter-spacing:0.08em;text-transform:uppercase;transition:color 0.2s;}
nav ul a:hover{color:var(--cyan);}
.nav-cta{background:transparent!important;color:var(--cyan)!important;padding:0.55rem 1.4rem;border:1px solid var(--cyan)!important;border-radius:2px!important;font-family:'Space Mono',monospace!important;font-size:0.75rem!important;letter-spacing:0.1em!important;transition:background 0.2s,box-shadow 0.2s!important;}
.nav-cta:hover{background:rgba(0,245,212,0.1)!important;box-shadow:0 0 20px rgba(0,245,212,0.2)!important;}

/* HERO */
.hero{min-height:100vh;display:grid;grid-template-columns:1fr 1fr;align-items:center;gap:4rem;padding:8rem 4rem 5rem;position:relative;z-index:2;max-width:1300px;margin:0 auto;}
.glow-orb{position:absolute;top:50%;left:30%;transform:translate(-50%,-60%);width:600px;height:600px;background:radial-gradient(circle,rgba(0,245,212,0.06) 0%,transparent 65%);pointer-events:none;}
.hero-left{display:flex;flex-direction:column;align-items:flex-start;}
.hero-tag{font-family:'Space Mono',monospace;font-size:0.72rem;letter-spacing:0.2em;text-transform:uppercase;color:var(--cyan);margin-bottom:2rem;display:flex;align-items:center;gap:0.75rem;animation:fadeUp 0.6s ease both;}
.hero-tag::before{content:'//';color:var(--gray2);}
h1{font-size:clamp(3rem,5.5vw,5.5rem);font-weight:700;line-height:0.95;letter-spacing:-0.04em;color:var(--white);margin-bottom:1.75rem;animation:fadeUp 0.7s 0.1s ease both;}
h1 .accent{color:transparent;-webkit-text-stroke:1px var(--cyan);}
h1 .glow-word{color:var(--cyan);text-shadow:0 0 40px rgba(0,245,212,0.4);}
.hero-sub{font-size:1rem;color:var(--gray);max-width:48ch;line-height:1.75;margin-bottom:2.5rem;animation:fadeUp 0.7s 0.2s ease both;}
.hero-ctas{display:flex;gap:1rem;flex-wrap:wrap;animation:fadeUp 0.7s 0.3s ease both;}

/* HERO CHART */
.hero-chart-wrap{position:relative;z-index:2;animation:fadeUp 0.9s 0.3s ease both;}
.hero-chart-card{background:var(--black2);border:1px solid var(--border2);padding:1.5rem;position:relative;overflow:hidden;}
.hero-chart-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);}
.hero-chart-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:1.25rem;}
.hero-chart-title{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--gray);letter-spacing:0.1em;text-transform:uppercase;}
.hero-chart-price{text-align:right;}
.hero-chart-pct{font-family:'Space Mono',monospace;font-size:1.6rem;font-weight:700;color:var(--cyan);display:block;text-shadow:0 0 20px rgba(0,245,212,0.3);}
.hero-chart-label{font-family:'Space Mono',monospace;font-size:0.65rem;color:var(--gray2);letter-spacing:0.1em;}
.hero-chart-canvas{position:relative;height:180px;}
.chart-live-badge{display:inline-flex;align-items:center;gap:0.4rem;font-family:'Space Mono',monospace;font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-top:1rem;}
.chart-live-dot{width:5px;height:5px;background:var(--cyan);border-radius:50%;animation:blink 1s step-end infinite;}

/* BUTTONS */
.btn-primary{background:var(--cyan);color:var(--black);font-family:'Space Mono',monospace;font-size:0.8rem;font-weight:700;letter-spacing:0.1em;text-transform:uppercase;padding:0.9rem 2rem;border:none;border-radius:2px;cursor:pointer;text-decoration:none;display:inline-block;transition:box-shadow 0.2s,transform 0.15s;}
.btn-primary:hover{box-shadow:0 0 30px rgba(0,245,212,0.4),0 0 60px rgba(0,245,212,0.15);transform:translateY(-2px);}
.btn-secondary{background:transparent;color:var(--white);font-family:'Space Mono',monospace;font-size:0.8rem;letter-spacing:0.1em;text-transform:uppercase;padding:0.9rem 2rem;border:1px solid var(--border2);border-radius:2px;cursor:pointer;text-decoration:none;display:inline-block;transition:border-color 0.2s,color 0.2s,transform 0.15s;}
.btn-secondary:hover{border-color:rgba(0,245,212,0.4);color:var(--cyan);transform:translateY(-2px);}

/* TICKER */
.ticker-wrap{background:var(--surface);border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:0.85rem 0;overflow:hidden;position:relative;z-index:2;}
.ticker{display:flex;gap:3rem;animation:ticker 30s linear infinite;width:max-content;}
@keyframes ticker{from{transform:translateX(0);}to{transform:translateX(-50%);}}
.ticker-item{display:flex;align-items:center;gap:0.75rem;font-family:'Space Mono',monospace;font-size:0.75rem;letter-spacing:0.05em;white-space:nowrap;color:var(--gray);}
.ticker-label{color:var(--white);font-weight:700;}
.ticker-yes{color:var(--cyan);}
.ticker-no{color:var(--red);}
.ticker-sep{color:var(--gray2);}

/* STATS */
.stats-bar{display:flex;justify-content:center;padding:4rem 2rem;position:relative;z-index:2;}
.stats-inner{display:grid;grid-template-columns:repeat(4,1fr);max-width:900px;width:100%;gap:0;}
.stat-item{text-align:center;padding:2rem;border-right:1px solid var(--border);position:relative;}
.stat-item:last-child{border-right:none;}
.stat-item::before{content:'';position:absolute;top:0;left:50%;transform:translateX(-50%);width:40px;height:1px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);}
.stat-number{font-family:'Space Mono',monospace;font-size:2rem;color:var(--cyan);letter-spacing:-0.02em;display:block;margin-bottom:0.5rem;text-shadow:0 0 20px rgba(0,245,212,0.3);}
.stat-label{font-size:0.72rem;color:var(--gray2);font-weight:500;letter-spacing:0.1em;text-transform:uppercase;}

/* SECTIONS */
section{padding:6rem 2rem;max-width:1100px;margin:0 auto;position:relative;z-index:2;}
.section-tag{font-family:'Space Mono',monospace;font-size:0.7rem;letter-spacing:0.2em;text-transform:uppercase;color:var(--cyan);margin-bottom:1rem;display:flex;align-items:center;gap:0.75rem;}
.section-tag::before{content:'//';color:var(--gray2);}
.section-title{font-size:clamp(2rem,4vw,3rem);font-weight:700;line-height:1.05;letter-spacing:-0.03em;color:var(--white);max-width:18ch;margin-bottom:1rem;}
.section-sub{font-size:0.95rem;color:var(--gray);max-width:52ch;line-height:1.75;margin-bottom:3.5rem;}

/* MARKETS + VOLUME CHART */
.markets-and-chart{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--border);border:1px solid var(--border);}
.markets-col{display:flex;flex-direction:column;gap:1px;background:var(--border);}
.market-card{background:var(--black2);padding:1.75rem;transition:background 0.2s;cursor:pointer;position:relative;overflow:hidden;flex:1;}
.market-card::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--cyan-dim),transparent);opacity:0;transition:opacity 0.3s;}
.market-card:hover::before{opacity:1;}
.market-card:hover{background:var(--surface);}
.market-category{font-family:'Space Mono',monospace;font-size:0.65rem;letter-spacing:0.15em;text-transform:uppercase;color:var(--cyan2);margin-bottom:0.75rem;display:flex;align-items:center;gap:0.5rem;}
.market-category::before{content:'';width:4px;height:4px;background:var(--cyan);border-radius:50%;}
.market-question{font-size:0.95rem;font-weight:600;color:var(--white);line-height:1.4;margin-bottom:1.25rem;}
.market-bars{display:flex;flex-direction:column;gap:0.65rem;margin-bottom:1.25rem;}
.bar-row{display:flex;align-items:center;gap:0.75rem;}
.bar-label{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--gray);min-width:28px;}
.bar-track{flex:1;height:3px;background:rgba(255,255,255,0.06);position:relative;}
.bar-fill-yes{height:100%;background:linear-gradient(90deg,var(--cyan2),var(--cyan));position:relative;}
.bar-fill-yes::after{content:'';position:absolute;right:0;top:-3px;width:8px;height:8px;background:var(--cyan);border-radius:50%;box-shadow:0 0 8px rgba(0,245,212,0.6);}
.bar-fill-no{height:100%;background:linear-gradient(90deg,#8b3030,var(--red));position:relative;}
.bar-fill-no::after{content:'';position:absolute;right:0;top:-3px;width:8px;height:8px;background:var(--red);border-radius:50%;}
.bar-pct{font-family:'Space Mono',monospace;font-size:0.78rem;font-weight:700;min-width:36px;text-align:right;}
.bar-pct.yes-pct{color:var(--cyan);}
.bar-pct.no-pct{color:var(--red);}
.market-meta{display:flex;justify-content:space-between;padding-top:1rem;border-top:1px solid var(--border);font-family:'Space Mono',monospace;font-size:0.68rem;color:var(--gray2);}
.market-volume{color:var(--white);font-weight:700;}

/* VOLUME CHART PANEL */
.volume-panel{background:var(--black2);padding:2rem;display:flex;flex-direction:column;}
.volume-header{margin-bottom:1.5rem;}
.volume-title{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--gray);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:0.5rem;}
.volume-big{font-family:'Space Mono',monospace;font-size:2rem;font-weight:700;color:var(--white);text-shadow:0 0 20px rgba(255,255,255,0.1);}
.volume-change{font-family:'Space Mono',monospace;font-size:0.75rem;color:var(--cyan);margin-left:0.5rem;}
.volume-chart-wrap{flex:1;position:relative;min-height:280px;}

/* PROBABILITY HISTORY */
.prob-section{background:var(--surface);border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:6rem 2rem;position:relative;z-index:2;}
.prob-inner{max-width:1100px;margin:0 auto;}
.prob-grid{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:var(--border);border:1px solid var(--border);margin-top:3rem;}
.prob-card{background:var(--black2);padding:2rem;position:relative;overflow:hidden;}
.prob-card::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);opacity:0.4;}
.prob-card-header{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:1.25rem;}
.prob-card-title{font-size:0.9rem;font-weight:600;color:var(--white);max-width:28ch;line-height:1.4;}
.prob-badge{font-family:'Space Mono',monospace;font-size:0.7rem;padding:0.3rem 0.7rem;border:1px solid rgba(0,245,212,0.3);color:var(--cyan);background:rgba(0,245,212,0.06);}
.prob-chart-wrap{position:relative;height:160px;margin-bottom:1rem;}
.prob-meta{display:flex;justify-content:space-between;font-family:'Space Mono',monospace;font-size:0.68rem;color:var(--gray2);}

/* DONUT SECTION */
.donut-section{padding:6rem 2rem;max-width:1100px;margin:0 auto;position:relative;z-index:2;}
.donut-grid{display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center;margin-top:3rem;}
.donut-wrap{position:relative;display:flex;align-items:center;justify-content:center;}
.donut-canvas{max-width:300px;max-height:300px;}
.donut-center{position:absolute;text-align:center;}
.donut-value{font-family:'Space Mono',monospace;font-size:2rem;font-weight:700;color:var(--cyan);display:block;text-shadow:0 0 20px rgba(0,245,212,0.3);}
.donut-sub{font-family:'Space Mono',monospace;font-size:0.65rem;color:var(--gray2);letter-spacing:0.1em;}
.donut-legend{display:flex;flex-direction:column;gap:1.25rem;}
.legend-item{display:flex;align-items:center;gap:1rem;padding:1rem;border:1px solid var(--border);background:var(--black2);transition:border-color 0.2s;}
.legend-item:hover{border-color:rgba(0,245,212,0.2);}
.legend-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0;}
.legend-info{flex:1;}
.legend-label{font-size:0.85rem;font-weight:600;color:var(--white);margin-bottom:0.2rem;}
.legend-val{font-family:'Space Mono',monospace;font-size:0.75rem;color:var(--gray2);}
.legend-pct{font-family:'Space Mono',monospace;font-size:1rem;font-weight:700;color:var(--white);}

/* STEPS */
.steps{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:1px;background:var(--border);border:1px solid var(--border);margin-top:3.5rem;}
.step-card{background:var(--black2);padding:2.5rem 2rem;position:relative;transition:background 0.2s;}
.step-card:hover{background:var(--surface);}
.step-card::after{content:'';position:absolute;top:0;left:0;width:100%;height:2px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);opacity:0;transition:opacity 0.3s;}
.step-card:hover::after{opacity:1;}
.step-number{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--cyan);letter-spacing:0.15em;margin-bottom:1.5rem;display:flex;align-items:center;gap:0.5rem;}
.step-number::before{content:'STEP';}
.step-card h3{font-size:1rem;font-weight:600;color:var(--white);margin-bottom:0.75rem;}
.step-card p{font-size:0.875rem;color:var(--gray);line-height:1.7;}

/* FEATURES */
.features-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--border);border:1px solid var(--border);}
.feature-card{background:var(--black2);padding:2rem;transition:background 0.2s;}
.feature-card:hover{background:var(--surface);}
.feature-icon{font-family:'Space Mono',monospace;font-size:1.5rem;color:var(--cyan);margin-bottom:1.25rem;opacity:0.7;}
.feature-card h3{font-size:0.95rem;font-weight:600;color:var(--white);margin-bottom:0.6rem;}
.feature-card p{font-size:0.85rem;color:var(--gray);line-height:1.7;}

/* TRUST */
.trust-full{background:var(--surface);border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:6rem 2rem;position:relative;z-index:2;overflow:hidden;}
.trust-full::before{content:'';position:absolute;right:-200px;top:50%;transform:translateY(-50%);width:500px;height:500px;background:radial-gradient(circle,rgba(0,245,212,0.05) 0%,transparent 65%);pointer-events:none;}
.trust-inner{max-width:1100px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:5rem;align-items:center;}
.trust-items{display:flex;flex-direction:column;gap:1.25rem;}
.trust-item{display:flex;gap:1.25rem;align-items:flex-start;padding:1.25rem;border:1px solid var(--border);background:var(--black2);transition:border-color 0.2s;}
.trust-item:hover{border-color:rgba(0,245,212,0.2);}
.trust-check{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--cyan);flex-shrink:0;margin-top:2px;}
.trust-item-text h4{font-size:0.9rem;font-weight:600;color:var(--white);margin-bottom:0.3rem;}
.trust-item-text p{font-size:0.82rem;color:var(--gray);line-height:1.65;}

/* TERMINAL */
.terminal-section{max-width:700px;margin:0 auto;padding:6rem 2rem;text-align:center;position:relative;z-index:2;}
.terminal{background:var(--black2);border:1px solid var(--border2);border-radius:4px;overflow:hidden;margin-bottom:2rem;text-align:left;}
.terminal-bar{background:var(--surface2);padding:0.75rem 1rem;display:flex;align-items:center;gap:0.5rem;border-bottom:1px solid var(--border);}
.dot{width:10px;height:10px;border-radius:50%;}
.dot-r{background:var(--red);}
.dot-y{background:#ffd166;}
.dot-g{background:var(--cyan);}
.term-title{font-family:'Space Mono',monospace;font-size:0.72rem;color:var(--gray2);margin-left:0.5rem;}
.terminal-body{padding:1.5rem;}
.term-line{font-family:'Space Mono',monospace;font-size:0.82rem;line-height:2;display:flex;gap:0.75rem;}
.term-prompt{color:var(--cyan);}
.term-cmd{color:var(--white);}
.term-comment{color:var(--gray2);}
.term-output{color:var(--cyan2);}
.term-cursor{display:inline-block;width:8px;height:14px;background:var(--cyan);animation:blink 1s step-end infinite;vertical-align:middle;}
.cta-headline{font-size:clamp(1.75rem,4vw,2.75rem);font-weight:700;letter-spacing:-0.03em;color:var(--white);margin-bottom:1rem;line-height:1.1;}
.cta-sub{font-size:0.95rem;color:var(--gray);line-height:1.7;margin-bottom:2rem;}
.hero-ctas{display:flex;gap:1rem;flex-wrap:wrap;justify-content:center;}

/* FOOTER */
footer{background:var(--black);border-top:1px solid var(--border);padding:2.5rem 3rem;display:flex;align-items:center;justify-content:space-between;position:relative;z-index:2;}
.footer-logo{font-family:'Space Mono',monospace;font-size:1rem;color:var(--white);text-decoration:none;}
.footer-logo span{color:var(--cyan);}
footer p{font-family:'Space Mono',monospace;font-size:0.7rem;color:var(--gray2);letter-spacing:0.05em;}

/* ANIM */
@keyframes fadeUp{from{opacity:0;transform:translateY(28px);}to{opacity:1;transform:translateY(0);}}
.fade-up{opacity:0;transform:translateY(24px);transition:opacity 0.7s ease,transform 0.7s ease;}
.fade-up.visible{opacity:1;transform:translateY(0);}

@media(max-width:1000px){
  .hero{grid-template-columns:1fr;padding:7rem 2rem 4rem;}
  .hero-left{align-items:center;text-align:center;}
  .markets-and-chart,.prob-grid,.donut-grid,.trust-inner{grid-template-columns:1fr;}
  nav{padding:1rem 1.5rem;}
  nav ul li:not(:last-child){display:none;}
  .stats-inner{grid-template-columns:repeat(2,1fr);}
  .features-grid{grid-template-columns:1fr;}
  footer{flex-direction:column;gap:1rem;text-align:center;}
}
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <a href="#" class="logo">
    <span class="logo-bracket">[</span>ANTO<span class="logo-bracket">]</span>
    <span style="color:var(--gray2);font-size:0.9rem;">PREDICTIONS</span>
    <div class="logo-dot"></div>
  </a>
  <ul>
    <li><a href="#mercados">Mercados</a></li>
    <li><a href="#como-funciona">Protocolo</a></li>
    <li><a href="#seguranca">Segurança</a></li>
    <li><a href="#entrar" class="nav-cta">INICIAR</a></li>
  </ul>
</nav>

<!-- HERO - 2 cols with live chart -->
<div style="position:relative;z-index:2;">
  <div class="hero">
    <div class="glow-orb"></div>
    <div class="hero-left">
      <div class="hero-tag">Plataforma de Predições · Beta Aberto · 2026</div>
      <h1>O futuro<br>é <span class="glow-word">legível.</span><br><span class="accent">Leia-o.</span></h1>
      <p class="hero-sub">AntoPredictions é o mercado de predições brasileiro. Analise, posicione-se e lucre com eventos de política, economia e geopolítica.</p>
      <div class="hero-ctas">
        <a href="#entrar" class="btn-primary">Acessar Plataforma</a>
        <a href="#mercados" class="btn-secondary">Ver Mercados</a>
      </div>
    </div>

    <!-- HERO LIVE CHART -->
    <div class="hero-chart-wrap">
      <div class="hero-chart-card">
        <div class="hero-chart-header">
          <div>
            <div class="hero-chart-title">ELEIÇÃO SP 2026 · CANDIDATO GOV.</div>
            <div class="hero-chart-label" style="margin-top:4px;">PROBABILIDADE · 90 DIAS</div>
          </div>
          <div class="hero-chart-price">
            <span class="hero-chart-pct" id="livePrice">62%</span>
            <span class="hero-chart-label">▲ +4.2% hoje</span>
          </div>
        </div>
        <div class="hero-chart-canvas">
          <canvas id="heroChart"></canvas>
        </div>
        <div class="chart-live-badge"><div class="chart-live-dot"></div> AO VIVO · ATUALIZA A CADA 30S</div>
      </div>
    </div>
  </div>
</div>

<!-- TICKER -->
<div class="ticker-wrap">
  <div class="ticker">
    <div class="ticker-item"><span class="ticker-label">SELIC&lt;10% 2026</span><span class="ticker-yes">SIM 28%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 72%</span></div>
    <div class="ticker-item"><span class="ticker-label">CESSAR-FOGO ME</span><span class="ticker-yes">SIM 34%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 66%</span></div>
    <div class="ticker-item"><span class="ticker-label">ELEIÇÃO SP 2026</span><span class="ticker-yes">SIM 62%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 38%</span></div>
    <div class="ticker-item"><span class="ticker-label">IBOVESPA 150K</span><span class="ticker-yes">SIM 45%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 55%</span></div>
    <div class="ticker-item"><span class="ticker-label">INFLAÇÃO&lt;4%</span><span class="ticker-yes">SIM 51%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 49%</span></div>
    <div class="ticker-item"><span class="ticker-label">DÓLAR&lt;R$5</span><span class="ticker-yes">SIM 18%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 82%</span></div>
    <div class="ticker-item"><span class="ticker-label">SELIC&lt;10% 2026</span><span class="ticker-yes">SIM 28%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 72%</span></div>
    <div class="ticker-item"><span class="ticker-label">CESSAR-FOGO ME</span><span class="ticker-yes">SIM 34%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 66%</span></div>
    <div class="ticker-item"><span class="ticker-label">ELEIÇÃO SP 2026</span><span class="ticker-yes">SIM 62%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 38%</span></div>
    <div class="ticker-item"><span class="ticker-label">IBOVESPA 150K</span><span class="ticker-yes">SIM 45%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 55%</span></div>
    <div class="ticker-item"><span class="ticker-label">INFLAÇÃO&lt;4%</span><span class="ticker-yes">SIM 51%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 49%</span></div>
    <div class="ticker-item"><span class="ticker-label">DÓLAR&lt;R$5</span><span class="ticker-yes">SIM 18%</span><span class="ticker-sep">/</span><span class="ticker-no">NÃO 82%</span></div>
  </div>
</div>

<!-- STATS -->
<div class="stats-bar">
  <div class="stats-inner">
    <div class="stat-item fade-up"><span class="stat-number">R$4.2M</span><span class="stat-label">Volume Total</span></div>
    <div class="stat-item fade-up"><span class="stat-number">18.4K</span><span class="stat-label">Usuários Ativos</span></div>
    <div class="stat-item fade-up"><span class="stat-number">340+</span><span class="stat-label">Mercados Abertos</span></div>
    <div class="stat-item fade-up"><span class="stat-number">94%</span><span class="stat-label">Precisão Histórica</span></div>
  </div>
</div>

<!-- MERCADOS + VOLUME CHART -->
<section id="mercados">
  <span class="section-tag">Mercados em Destaque</span>
  <h2 class="section-title fade-up">Eventos que definem o mundo</h2>
  <p class="section-sub fade-up">Dados em tempo real. Probabilidades calculadas pelo mercado. Sem achismo.</p>

  <div class="markets-and-chart fade-up">
    <div class="markets-col">
      <div class="market-card">
        <div class="market-category">Política Brasil</div>
        <div class="market-question">O candidato do governo vencerá as eleições municipais de 2026 em São Paulo?</div>
        <div class="market-bars">
          <div class="bar-row"><span class="bar-label">SIM</span><div class="bar-track"><div class="bar-fill-yes" style="width:62%"></div></div><span class="bar-pct yes-pct">62%</span></div>
          <div class="bar-row"><span class="bar-label">NÃO</span><div class="bar-track"><div class="bar-fill-no" style="width:38%"></div></div><span class="bar-pct no-pct">38%</span></div>
        </div>
        <div class="market-meta"><span>ENCERRA DEZ/2026</span><span class="market-volume">VOL R$182.4K</span></div>
      </div>
      <div class="market-card">
        <div class="market-category">Geopolítica</div>
        <div class="market-question">Haverá cessar-fogo formal no Oriente Médio antes de Dezembro de 2026?</div>
        <div class="market-bars">
          <div class="bar-row"><span class="bar-label">SIM</span><div class="bar-track"><div class="bar-fill-yes" style="width:34%"></div></div><span class="bar-pct yes-pct">34%</span></div>
          <div class="bar-row"><span class="bar-label">NÃO</span><div class="bar-track"><div class="bar-fill-no" style="width:66%"></div></div><span class="bar-pct no-pct">66%</span></div>
        </div>
        <div class="market-meta"><span>ENCERRA DEZ/2026</span><span class="market-volume">VOL R$310K</span></div>
      </div>
      <div class="market-card">
        <div class="market-category">Economia</div>
        <div class="market-question">A taxa Selic estará abaixo de 10% ao final do ano de 2026?</div>
        <div class="market-bars">
          <div class="bar-row"><span class="bar-label">SIM</span><div class="bar-track"><div class="bar-fill-yes" style="width:28%"></div></div><span class="bar-pct yes-pct">28%</span></div>
          <div class="bar-row"><span class="bar-label">NÃO</span><div class="bar-track"><div class="bar-fill-no" style="width:72%"></div></div><span class="bar-pct no-pct">72%</span></div>
        </div>
        <div class="market-meta"><span>ENCERRA DEZ/2026</span><span class="market-volume">VOL R$95.7K</span></div>
      </div>
    </div>

    <!-- VOLUME CHART -->
    <div class="volume-panel">
      <div class="volume-header">
        <div class="volume-title">Volume Negociado · Últimos 12 Meses</div>
        <div style="display:flex;align-items:baseline;gap:0.5rem;margin-top:0.5rem;">
          <span class="volume-big">R$ 4.2M</span>
          <span class="volume-change">▲ +38% vs ano anterior</span>
        </div>
      </div>
      <div class="volume-chart-wrap">
        <canvas id="volumeChart"></canvas>
      </div>
    </div>
  </div>
</section>

<!-- PROBABILITY HISTORY -->
<div class="prob-section">
  <div class="prob-inner">
    <span class="section-tag">Histórico de Probabilidade</span>
    <h2 class="section-title fade-up">Veja como o mercado<br>pensa em tempo real</h2>
    <p class="section-sub fade-up">A curva de probabilidade revela quando o consenso muda — e quem estava certo.</p>
    <div class="prob-grid fade-up">
      <div class="prob-card">
        <div class="prob-card-header">
          <div class="prob-card-title">Eleição SP 2026 — Candidato do Governo</div>
          <span class="prob-badge">62%</span>
        </div>
        <div class="prob-chart-wrap">
          <canvas id="probChart1"></canvas>
        </div>
        <div class="prob-meta"><span>Jan 2026</span><span>Abr 2026</span></div>
      </div>
      <div class="prob-card">
        <div class="prob-card-header">
          <div class="prob-card-title">Cessar-Fogo Oriente Médio — Dez 2026</div>
          <span class="prob-badge" style="border-color:rgba(255,107,107,0.3);color:var(--red);background:rgba(255,107,107,0.06);">34%</span>
        </div>
        <div class="prob-chart-wrap">
          <canvas id="probChart2"></canvas>
        </div>
        <div class="prob-meta"><span>Jan 2026</span><span>Abr 2026</span></div>
      </div>
    </div>
  </div>
</div>

<!-- DONUT: DISTRIBUIÇÃO DE MERCADOS -->
<div class="donut-section">
  <span class="section-tag">Distribuição de Mercados</span>
  <h2 class="section-title fade-up">340+ mercados em<br>todas as categorias</h2>
  <p class="section-sub fade-up">De eleições a guerras, de economia a tecnologia — cobrimos o que molda o futuro.</p>
  <div class="donut-grid fade-up">
    <div class="donut-wrap">
      <canvas id="donutChart" class="donut-canvas"></canvas>
      <div class="donut-center">
        <span class="donut-value">340</span>
        <span class="donut-sub">MERCADOS</span>
      </div>
    </div>
    <div class="donut-legend">
      <div class="legend-item">
        <div class="legend-dot" style="background:#00f5d4;box-shadow:0 0 8px rgba(0,245,212,0.5);"></div>
        <div class="legend-info"><div class="legend-label">Política</div><div class="legend-val">Eleições, partidos, candidatos</div></div>
        <span class="legend-pct">34%</span>
      </div>
      <div class="legend-item">
        <div class="legend-dot" style="background:#4d9fff;box-shadow:0 0 8px rgba(77,159,255,0.5);"></div>
        <div class="legend-info"><div class="legend-label">Economia</div><div class="legend-val">Juros, câmbio, inflação</div></div>
        <span class="legend-pct">28%</span>
      </div>
      <div class="legend-item">
        <div class="legend-dot" style="background:#ff6b6b;box-shadow:0 0 8px rgba(255,107,107,0.5);"></div>
        <div class="legend-info"><div class="legend-label">Geopolítica</div><div class="legend-val">Conflitos, acordos, diplomacia</div></div>
        <span class="legend-pct">22%</span>
      </div>
      <div class="legend-item">
        <div class="legend-dot" style="background:#ffd166;box-shadow:0 0 8px rgba(255,209,102,0.5);"></div>
        <div class="legend-info"><div class="legend-label">Tecnologia & Outros</div><div class="legend-val">IA, cripto, ciência</div></div>
        <span class="legend-pct">16%</span>
      </div>
    </div>
  </div>
</div>

<!-- COMO FUNCIONA -->
<section id="como-funciona">
  <span class="section-tag">Protocolo</span>
  <h2 class="section-title fade-up">Simples por design.<br>Poderoso por natureza.</h2>
  <p class="section-sub fade-up">Quatro etapas entre você e o mercado.</p>
  <div class="steps fade-up">
    <div class="step-card"><div class="step-number">01</div><h3>Crie sua conta</h3><p>Cadastro em menos de 2 minutos. Verificação de identidade e depósito via PIX. Simples e seguro.</p></div>
    <div class="step-card"><div class="step-number">02</div><h3>Selecione um mercado</h3><p>Centenas de mercados com dados, análises e histórico. Filtre por categoria, prazo e liquidez.</p></div>
    <div class="step-card"><div class="step-number">03</div><h3>Execute sua posição</h3><p>Compre ações de SIM ou NÃO. O preço reflete a probabilidade agregada em tempo real.</p></div>
    <div class="step-card"><div class="step-number">04</div><h3>Receba seus ganhos</h3><p>Acertou? Cada ação vale R$1,00 na resolução. Saque instantâneo via PIX para sua conta.</p></div>
  </div>
</section>

<!-- FEATURES -->
<section>
  <span class="section-tag">Infraestrutura</span>
  <h2 class="section-title fade-up">Construída para quem exige o melhor</h2>
  <p class="section-sub fade-up">Ferramentas de nível institucional. Acessíveis a qualquer pessoa.</p>
  <div class="features-grid fade-up">
    <div class="feature-card"><div class="feature-icon">▲</div><h3>Dados em Tempo Real</h3><p>Preços, volume e variação ao vivo. Gráficos históricos completos para cada mercado.</p></div>
    <div class="feature-card"><div class="feature-icon">◈</div><h3>Resolução Auditável</h3><p>Critérios públicos e imutáveis. Oráculos verificados por múltiplas fontes independentes.</p></div>
    <div class="feature-card"><div class="feature-icon">⬡</div><h3>Liquidez Garantida</h3><p>Market makers asseguram liquidez nos principais mercados. Sempre há contraparte.</p></div>
    <div class="feature-card"><div class="feature-icon">◎</div><h3>Analytics Avançados</h3><p>Acompanhe P&L, taxa de acerto, retorno ajustado ao risco e evolução histórica.</p></div>
    <div class="feature-card"><div class="feature-icon">⊕</div><h3>PIX Instantâneo</h3><p>Depósitos e saques em segundos. Sem taxas ocultas. Sem burocracia desnecessária.</p></div>
    <div class="feature-card"><div class="feature-icon">⟁</div><h3>API para Traders</h3><p>Acesso programático via REST API. Automatize estratégias com suas ferramentas.</p></div>
  </div>
</section>

<!-- TRUST -->
<div class="trust-full" id="seguranca">
  <div class="trust-inner">
    <div class="fade-up">
      <span class="section-tag">Segurança</span>
      <h2 class="section-title">Confiança não se declara. Se comprova.</h2>
      <p class="section-sub" style="margin-bottom:2rem;">Cada centavo rastreável. Cada decisão, auditável. Os mais altos padrões do mercado financeiro brasileiro.</p>
      <a href="#entrar" class="btn-primary">Acessar Plataforma</a>
    </div>
    <div class="trust-items fade-up">
      <div class="trust-item"><span class="trust-check">[✓]</span><div class="trust-item-text"><h4>Recursos Segregados</h4><p>Fundos em conta separada e auditada. Nunca misturados com capital operacional.</p></div></div>
      <div class="trust-item"><span class="trust-check">[✓]</span><div class="trust-item-text"><h4>Criptografia TLS 1.3</h4><p>Toda comunicação criptografada com os padrões mais modernos disponíveis.</p></div></div>
      <div class="trust-item"><span class="trust-check">[✓]</span><div class="trust-item-text"><h4>Auditoria Semestral</h4><p>Auditores independentes verificam sistemas e relatórios financeiros semestralmente.</p></div></div>
      <div class="trust-item"><span class="trust-check">[✓]</span><div class="trust-item-text"><h4>KYC e Anti-Fraude</h4><p>Verificação de identidade rigorosa. Ambiente justo para todos os participantes.</p></div></div>
    </div>
  </div>
</div>

<!-- TERMINAL CTA -->
<div class="terminal-section" id="entrar">
  <div class="terminal fade-up">
    <div class="terminal-bar">
      <div class="dot dot-r"></div><div class="dot dot-y"></div><div class="dot dot-g"></div>
      <span class="term-title">anto-predictions ~ bash</span>
    </div>
    <div class="terminal-body">
      <div class="term-line"><span class="term-prompt">$</span><span class="term-cmd">anto register --user=voce@email.com</span></div>
      <div class="term-line"><span class="term-output">✓ Conta criada com sucesso</span></div>
      <div class="term-line"><span class="term-prompt">$</span><span class="term-cmd">anto deposit --amount=500 --method=pix</span></div>
      <div class="term-line"><span class="term-output">✓ R$500.00 creditados · saldo: R$500.00</span></div>
      <div class="term-line"><span class="term-prompt">$</span><span class="term-cmd">anto buy --market=eleicao-sp --side=yes --qty=100</span></div>
      <div class="term-line"><span class="term-output">✓ 100 ações SIM @ R$0.62 · custo: R$62.00</span></div>
      <div class="term-line"><span class="term-prompt">$</span><span class="term-comment"># potencial de retorno: R$100.00</span></div>
      <div class="term-line"><span class="term-prompt">$</span><span class="term-cursor"></span></div>
    </div>
  </div>
  <h2 class="cta-headline fade-up">Pronto para prever<br>o próximo movimento?</h2>
  <p class="cta-sub fade-up">Junte-se a 18.400 brasileiros que já monetizam sua análise. Sem taxa de cadastro.</p>
  <div class="hero-ctas fade-up">
    <a href="#" class="btn-primary">Criar Conta Grátis</a>
    <a href="#mercados" class="btn-secondary">Explorar Mercados</a>
  </div>
</div>

<footer>
  <a href="#" class="footer-logo">[ANTO]<span>PREDICTIONS</span></a>
  <p>© 2026 ANTOPREDICTIONS · TODOS OS DIREITOS RESERVADOS · CONFORMIDADE COM A LEGISLAÇÃO BRASILEIRA</p>
</footer>

<script>
// CURSOR
const cursor=document.getElementById('cursor'),ring=document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cursor.style.left=(mx-5)+'px';cursor.style.top=(my-5)+'px';});
(function anim(){rx+=(mx-rx-5)*0.12;ry+=(my-ry-5)*0.12;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(anim);})();
document.querySelectorAll('a,button').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.transform='scale(2)';ring.style.transform='translate(-13px,-13px) scale(1.5)';});
  el.addEventListener('mouseleave',()=>{cursor.style.transform='scale(1)';ring.style.transform='translate(-13px,-13px) scale(1)';});
});

// SCROLL ANIM
const obs=new IntersectionObserver(entries=>{entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');obs.unobserve(e.target);}});},{threshold:0.1});
document.querySelectorAll('.fade-up').forEach(el=>obs.observe(el));

// CHART DEFAULTS
Chart.defaults.color='#5a5a6e';
Chart.defaults.font.family="'Space Mono', monospace";
Chart.defaults.font.size=10;

const CYAN='#00f5d4';
const CYAN2='#00c4aa';
const RED='#ff6b6b';
const BLUE='#4d9fff';
const YELLOW='#ffd166';

// ─── HERO CHART: live probability line ───
const heroLabels=[];
const heroData=[];
let base=54;
for(let i=89;i>=0;i--){
  const d=new Date();d.setDate(d.getDate()-i);
  heroLabels.push(i===0?'Hoje':i%15===0?d.toLocaleDateString('pt-BR',{day:'2-digit',month:'2-digit'}):'');
  base+=((Math.random()-0.45)*1.8);
  base=Math.max(30,Math.min(80,base));
  heroData.push(parseFloat(base.toFixed(1)));
}
heroData[heroData.length-1]=62;

new Chart(document.getElementById('heroChart'),{
  type:'line',
  data:{
    labels:heroLabels,
    datasets:[{
      data:heroData,
      borderColor:CYAN,
      borderWidth:2,
      pointRadius:0,
      pointHoverRadius:4,
      pointHoverBackgroundColor:CYAN,
      fill:true,
      backgroundColor:(ctx)=>{
        const g=ctx.chart.ctx.createLinearGradient(0,0,0,ctx.chart.height);
        g.addColorStop(0,'rgba(0,245,212,0.18)');
        g.addColorStop(1,'rgba(0,245,212,0)');
        return g;
      },
      tension:0.4
    }]
  },
  options:{
    responsive:true,maintainAspectRatio:false,
    animation:{duration:1200,easing:'easeInOutQuart'},
    interaction:{mode:'index',intersect:false},
    plugins:{legend:{display:false},tooltip:{
      backgroundColor:'rgba(10,10,15,0.95)',
      borderColor:'rgba(0,245,212,0.3)',borderWidth:1,
      titleColor:CYAN,bodyColor:'#fff',
      callbacks:{label:ctx=>`  SIM: ${ctx.raw}%`}
    }},
    scales:{
      x:{grid:{color:'rgba(255,255,255,0.04)',drawBorder:false},ticks:{color:'#5a5a6e',maxRotation:0,autoSkip:true,maxTicksLimit:4}},
      y:{grid:{color:'rgba(255,255,255,0.04)',drawBorder:false},ticks:{color:'#5a5a6e',callback:v=>v+'%'},min:20,max:85}
    }
  }
});

// simulate live price jitter
setInterval(()=>{
  const el=document.getElementById('livePrice');
  if(!el)return;
  const jitter=(Math.random()-0.5)*0.4;
  const cur=parseFloat(el.textContent)+jitter;
  el.textContent=Math.max(55,Math.min(70,cur)).toFixed(1)+'%';
},4000);

// ─── VOLUME CHART: bar chart (Mai 2025 → Abr 2026) ───
const months=['Mai/25','Jun/25','Jul/25','Ago/25','Set/25','Out/25','Nov/25','Dez/25','Jan/26','Fev/26','Mar/26','Abr/26'];
const volData=[180000,210000,195000,260000,290000,310000,275000,340000,380000,420000,395000,460000];

new Chart(document.getElementById('volumeChart'),{
  type:'bar',
  data:{
    labels:months,
    datasets:[{
      data:volData,
      backgroundColor:volData.map((_,i)=>i===11?CYAN:'rgba(0,245,212,0.15)'),
      borderColor:volData.map((_,i)=>i===11?CYAN:'rgba(0,245,212,0.35)'),
      borderWidth:1,
      borderRadius:2,
      hoverBackgroundColor:'rgba(0,245,212,0.35)'
    }]
  },
  options:{
    responsive:true,maintainAspectRatio:false,
    animation:{duration:1400,easing:'easeInOutQuart'},
    plugins:{legend:{display:false},tooltip:{
      backgroundColor:'rgba(10,10,15,0.95)',
      borderColor:'rgba(0,245,212,0.3)',borderWidth:1,
      titleColor:CYAN,bodyColor:'#fff',
      callbacks:{label:ctx=>`  R$ ${(ctx.raw/1000).toFixed(0)}K`}
    }},
    scales:{
      x:{grid:{display:false},ticks:{color:'#5a5a6e'}},
      y:{grid:{color:'rgba(255,255,255,0.04)',drawBorder:false},ticks:{color:'#5a5a6e',callback:v=>'R$'+(v/1000)+'K'}}
    }
  }
});

// ─── PROB CHARTS ───
const probLabels=[];
const prob1Data=[];
const prob2Data=[];
let p1=50,p2=44;
for(let i=119;i>=0;i--){
  const d=new Date();d.setDate(d.getDate()-i);
  probLabels.push(i%30===0?d.toLocaleDateString('pt-BR',{day:'2-digit',month:'2-digit'}):'');
  p1+=((Math.random()-0.44)*1.2);p1=Math.max(35,Math.min(75,p1));
  p2+=((Math.random()-0.5)*2);p2=Math.max(20,Math.min(55,p2));
  prob1Data.push(parseFloat(p1.toFixed(1)));
  prob2Data.push(parseFloat(p2.toFixed(1)));
}
prob1Data[prob1Data.length-1]=62;
prob2Data[prob2Data.length-1]=34;

new Chart(document.getElementById('probChart1'),{
  type:'line',
  data:{labels:probLabels,datasets:[{
    data:prob1Data,borderColor:CYAN,borderWidth:1.5,pointRadius:0,fill:true,
    backgroundColor:ctx=>{const g=ctx.chart.ctx.createLinearGradient(0,0,0,ctx.chart.height);g.addColorStop(0,'rgba(0,245,212,0.15)');g.addColorStop(1,'rgba(0,245,212,0)');return g;},
    tension:0.4
  }]},
  options:{responsive:true,maintainAspectRatio:false,animation:{duration:1000},
    plugins:{legend:{display:false},tooltip:{backgroundColor:'rgba(10,10,15,0.95)',borderColor:'rgba(0,245,212,0.3)',borderWidth:1,titleColor:CYAN,bodyColor:'#fff',callbacks:{label:ctx=>`  SIM: ${ctx.raw}%`}}},
    scales:{x:{grid:{display:false},ticks:{color:'#5a5a6e',maxTicksLimit:4}},y:{grid:{color:'rgba(255,255,255,0.04)',drawBorder:false},ticks:{color:'#5a5a6e',callback:v=>v+'%'},min:25,max:80}}
  }
});

new Chart(document.getElementById('probChart2'),{
  type:'line',
  data:{labels:probLabels,datasets:[{
    data:prob2Data,borderColor:RED,borderWidth:1.5,pointRadius:0,fill:true,
    backgroundColor:ctx=>{const g=ctx.chart.ctx.createLinearGradient(0,0,0,ctx.chart.height);g.addColorStop(0,'rgba(255,107,107,0.15)');g.addColorStop(1,'rgba(255,107,107,0)');return g;},
    tension:0.4
  }]},
  options:{responsive:true,maintainAspectRatio:false,animation:{duration:1000},
    plugins:{legend:{display:false},tooltip:{backgroundColor:'rgba(10,10,15,0.95)',borderColor:'rgba(255,107,107,0.3)',borderWidth:1,titleColor:RED,bodyColor:'#fff',callbacks:{label:ctx=>`  SIM: ${ctx.raw}%`}}},
    scales:{x:{grid:{display:false},ticks:{color:'#5a5a6e',maxTicksLimit:4}},y:{grid:{color:'rgba(255,255,255,0.04)',drawBorder:false},ticks:{color:'#5a5a6e',callback:v=>v+'%'},min:10,max:65}}
  }
});

// ─── DONUT CHART ───
new Chart(document.getElementById('donutChart'),{
  type:'doughnut',
  data:{
    labels:['Política','Economia','Geopolítica','Tecnologia & Outros'],
    datasets:[{
      data:[34,28,22,16],
      backgroundColor:['rgba(0,245,212,0.85)','rgba(77,159,255,0.85)','rgba(255,107,107,0.85)','rgba(255,209,102,0.85)'],
      borderColor:['#050507'],
      borderWidth:3,
      hoverOffset:8
    }]
  },
  options:{
    responsive:true,maintainAspectRatio:true,cutout:'72%',
    animation:{duration:1200,easing:'easeInOutQuart'},
    plugins:{
      legend:{display:false},
      tooltip:{backgroundColor:'rgba(10,10,15,0.95)',borderColor:'rgba(0,245,212,0.3)',borderWidth:1,titleColor:CYAN,bodyColor:'#fff',callbacks:{label:ctx=>`  ${ctx.label}: ${ctx.raw}%`}}
    }
  }
});
</script>
</body>
</html>
