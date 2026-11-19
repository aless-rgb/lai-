<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#14070d">
<title>Pour toi, mon amour</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;1,400;1,500&family=Pinyon+Script&display=swap" rel="stylesheet">
<style>
/* Plan : une carte de voeux verticale, nuit bordeaux, or rose, un seul sujet par écran. */
:root{
  --nuit:#14070d;
  --bordeaux:#3a1020;
  --rose:#eaaab6;
  --or:#dcb48f;
  --ivoire:#fbf0e8;
  --braise:#ff6f86;
  --serif:"Cormorant Garamond",Georgia,"Times New Roman",serif;
  --script:"Pinyon Script","Snell Roundhand","Apple Chancery",cursive;
  color-scheme:dark;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;margin:0;background:var(--nuit);overflow:hidden}
body{
  font-family:var(--serif);color:var(--ivoire);
  background:radial-gradient(120% 80% at 50% 0%,var(--bordeaux) 0%,var(--nuit) 70%);
  -webkit-user-select:none;user-select:none;touch-action:manipulation;
}
#fx{position:fixed;inset:0;width:100%;height:100%;pointer-events:none;z-index:0}
#stage{position:fixed;inset:0;z-index:1}

.bar{position:fixed;z-index:5;left:20px;right:20px;top:calc(env(safe-area-inset-top) + 14px);display:flex;gap:5px}
.bar i{flex:1;height:2px;border-radius:2px;background:rgba(251,240,232,.18);overflow:hidden;position:relative}
.bar i::after{content:"";position:absolute;inset:0;background:var(--or);transform:scaleX(0);transform-origin:left;transition:transform .6s ease}
.bar i.on::after{transform:scaleX(1)}

.slide{
  position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;gap:18px;
  padding:calc(env(safe-area-inset-top) + 60px) 30px calc(env(safe-area-inset-bottom) + 64px);
  opacity:0;visibility:hidden;transition:opacity .9s ease,visibility 0s .9s;
}
.slide.active{opacity:1;visibility:visible;transition:opacity .9s ease,visibility 0s}

/* entrées animées : l'état de repos est visible, l'animation part d'un état masqué */
.slide.active .a{animation:rise 1.1s cubic-bezier(.2,.7,.2,1) both;animation-delay:calc(var(--d,0) * 1s)}
.slide.active .ch{animation:chIn .9s ease both;animation-delay:calc(var(--b,0s) + var(--i) * 45ms)}
@keyframes rise{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:none}}
@keyframes chIn{from{opacity:0;transform:translateY(10px);filter:blur(6px)}to{opacity:1;transform:none;filter:none}}
.w{display:inline-block;white-space:nowrap}

.eyebrow{font-size:15px;letter-spacing:.32em;text-transform:uppercase;color:var(--or);margin:0}
h1,h2{margin:0;font-weight:500;text-wrap:balance}
.big{font-size:clamp(34px,10.5vw,52px);line-height:1.12;font-style:italic}
.txt{font-size:clamp(24px,7vw,31px);line-height:1.4;font-style:italic;max-width:19em;margin:0;text-wrap:balance}
.script{font-family:var(--script);font-weight:400;color:var(--or);line-height:1.05;margin:0}
.name{font-size:clamp(56px,19vw,92px);text-shadow:0 0 28px rgba(220,180,143,.45)}
.rule{width:64px;height:1px;background:linear-gradient(90deg,transparent,var(--or),transparent);border:0;margin:4px 0}

button{font:inherit;color:inherit;cursor:pointer}
.btn{
  position:relative;margin-top:10px;padding:15px 34px;border-radius:999px;border:1px solid var(--or);background:rgba(220,180,143,.08);
  font-size:20px;letter-spacing:.14em;text-transform:uppercase;color:var(--ivoire);
}
.btn:focus-visible{outline:2px solid var(--rose);outline-offset:4px}
.btn.pulse::after{content:"";position:absolute;inset:-1px;border-radius:inherit;border:1px solid var(--or);animation:ring 2.4s ease-out infinite}
@keyframes ring{from{opacity:.8;transform:scale(1)}to{opacity:0;transform:scale(1.35,1.7)}}

.orn{width:46px;height:46px;color:var(--or)}
.count{font-size:clamp(84px,28vw,130px);line-height:1;font-variant-numeric:tabular-nums;color:var(--rose);font-weight:500;text-shadow:0 0 34px rgba(255,111,134,.35)}

ul.list{list-style:none;margin:6px 0 0;padding:0;display:flex;flex-direction:column;gap:22px;max-width:20em}
ul.list li{font-size:clamp(22px,6.4vw,28px);line-height:1.3;font-style:italic;display:flex;flex-direction:column;align-items:center;gap:10px}
ul.list li::before{content:"";width:28px;height:1px;background:var(--or)}

#stars{width:min(86vw,340px);height:min(74vw,300px);display:block}

.candle{width:128px;height:230px;overflow:visible}
.flame{transform-origin:60px 78px;animation:flick 1.6s ease-in-out infinite}
@keyframes flick{0%,100%{transform:scale(1,1) rotate(-1.5deg)}35%{transform:scale(.94,1.06) rotate(2deg)}70%{transform:scale(1.04,.96) rotate(-2deg)}}
.glow{animation:glow 2.2s ease-in-out infinite}
@keyframes glow{0%,100%{opacity:.55}50%{opacity:.85}}
.slide.blown .flame,.slide.blown .glow{opacity:0;transition:opacity .5s ease;animation:none}
.smoke{opacity:0}
.slide.blown .smoke{animation:smoke 2.6s ease-out both}
@keyframes smoke{0%{opacity:0;transform:translateY(0)}20%{opacity:.7}100%{opacity:0;transform:translateY(-46px)}}
.swap{display:grid}
.swap>*{grid-area:1/1;transition:opacity .8s ease,transform .8s ease}
.swap .after{opacity:0;transform:translateY(10px);pointer-events:none}
.slide.blown .swap .before{opacity:0;transform:translateY(-10px);pointer-events:none}
.slide.blown .swap .after{opacity:1;transform:none;pointer-events:auto}

.heart{width:112px;height:112px;color:var(--braise);filter:drop-shadow(0 0 22px rgba(255,111,134,.55));animation:beat 1.7s ease-in-out infinite}
@keyframes beat{0%,100%{transform:scale(1)}14%{transform:scale(1.14)}28%{transform:scale(1)}42%{transform:scale(1.09)}56%{transform:scale(1)}}
.sign{font-size:46px}

#hint{position:fixed;z-index:4;left:0;right:0;bottom:calc(env(safe-area-inset-bottom) + 22px);text-align:center;font-size:14px;letter-spacing:.28em;text-transform:uppercase;color:rgba(251,240,232,.55);transition:opacity .6s;animation:hint 2.4s ease-in-out infinite}
#hint.off{opacity:0;animation:none}
@keyframes hint{0%,100%{opacity:.35}50%{opacity:.8}}

@media (prefers-reduced-motion:reduce){
  .slide.active .a,.slide.active .ch{animation-duration:.01s;animation-delay:0s}
  .flame,.glow,.heart,.btn.pulse::after,#hint{animation:none}
}
</style>
</head>
<body>
<canvas id="fx" aria-hidden="true"></canvas>
<div class="bar" id="bar" aria-hidden="true"></div>

<main id="stage">

  <section class="slide active" id="s-cover" aria-label="Ouverture">
    <svg class="orn a" style="--d:.1" viewBox="0 0 48 48" fill="none" stroke="currentColor" stroke-width="1.2" aria-hidden="true"><path d="M24 4v40M4 24h40M10 10l28 28M38 10L10 38" opacity=".55"/><circle cx="24" cy="24" r="6"/></svg>
    <p class="eyebrow a" style="--d:.3">Pour toi <svg viewBox="0 0 24 24" width="15" height="15" fill="#ff6f86" style="vertical-align:-1px" aria-label="cœur"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg></p>
    <h1 class="script name a" style="--d:.6;font-size:clamp(46px,15vw,76px)">Bon anniversaire</h1>
    <button class="btn pulse a" style="--d:1.2" id="open" type="button">Ouvrir</button>
  </section>

  <section class="slide" id="s-hello" aria-label="Joyeux anniversaire">
    <h2 class="big" data-split data-b=".3s">Joyeux anniversaire</h2>
    <p class="script name a" style="--d:1.9"><span data-bind="nom"></span></p>
    <hr class="rule a" style="--d:2.4">
    <p class="txt a" style="--d:2.6">Ce petit film est pour toi seule.</p>
  </section>

  <section class="slide" id="s-day" aria-label="Aujourd'hui">
    <p class="eyebrow a" style="--d:.2">Aujourd’hui</p>
    <h2 class="script name a" style="--d:.7;font-size:clamp(46px,15vw,72px)">Tu as 17 ans</h2>
    <p class="txt a" style="--d:1.9">Dans ces 17 ans, on a passé<br><span style="color:var(--rose);font-style:normal;font-weight:500">512 jours</span> ensemble,</p>
    <p class="txt a" style="--d:3.1">sans doute les meilleurs<br>de toute ma vie.</p>
  </section>

  <section class="slide" id="s-count" aria-label="Mille et une raisons">
    <p class="eyebrow a" style="--d:.1">Il y a</p>
    <div class="count a" style="--d:.3" id="counter">0</div>
    <p class="txt a" style="--d:.9">raisons de t’aimer,<br>et je continue d’en trouver.</p>
  </section>

  <section class="slide" id="s-reasons" aria-label="Ce que j'aime en toi">
    <p class="eyebrow a" style="--d:.1">Ce que j’aime en toi</p>
    <ul class="list" id="reasons"></ul>
    <p class="txt a" style="--d:4.6;font-size:clamp(19px,5.4vw,23px);color:var(--rose)">Si je devais tout citer, je n’aurais même pas assez de temps pour tout écrire.</p>
  </section>

  <section class="slide" id="s-stars" aria-label="Constellation">
    <canvas id="stars" aria-hidden="true"></canvas>
    <p class="txt a" style="--d:3">Entre toutes les étoiles,<br>tu restes ma préférée.</p>
  </section>

  <section class="slide" id="s-promise" aria-label="Promesses">
    <p class="eyebrow a" style="--d:.1">Je te promets</p>
    <p class="txt a" style="--d:.7;font-size:clamp(22px,6.2vw,28px)">une vie de rêve à mes côtés,</p>
    <p class="txt a" style="--d:1.8;font-size:clamp(22px,6.2vw,28px)">de l’amour au quotidien<br>et des fous rires,</p>
    <p class="txt a" style="--d:3;font-size:clamp(22px,6.2vw,28px)">même si la vie actuelle<br>n’est pas facile.</p>
    <p class="txt a" style="--d:4.4;font-size:clamp(22px,6.2vw,28px);color:var(--rose)">Je t’aime plus que tout.<br>Mon amour pour toi est infini.</p>
  </section>

  <section class="slide" id="s-candle" aria-label="Le voeu">
    <svg class="candle a" style="--d:.1" viewBox="0 0 120 230" aria-hidden="true">
      <defs>
        <radialGradient id="gl" cx="50%" cy="50%" r="50%"><stop offset="0" stop-color="#ffcf8a" stop-opacity=".85"/><stop offset="1" stop-color="#ffcf8a" stop-opacity="0"/></radialGradient>
        <linearGradient id="cd" x1="0" x2="1"><stop offset="0" stop-color="#f3c9cf"/><stop offset=".5" stop-color="#fbf0e8"/><stop offset="1" stop-color="#e3a9b4"/></linearGradient>
      </defs>
      <circle class="glow" cx="60" cy="70" r="56" fill="url(#gl)"/>
      <rect x="40" y="104" width="40" height="112" rx="4" fill="url(#cd)"/>
      <path d="M40 124h40M40 150h40M40 176h40" stroke="#dcb48f" stroke-width="1.2" opacity=".6"/>
      <rect x="58.5" y="92" width="3" height="14" rx="1.5" fill="#3a2a2a"/>
      <g class="flame"><path d="M60 52c9 13 12 22 5 34-3 5-7 6-10 0-6-11-3-22 5-34z" fill="#ffb347"/><path d="M60 66c4 7 5 12 2 17-1.6 2.6-4 2.6-5 0-2-5-1-10 3-17z" fill="#fff3c4"/></g>
      <path class="smoke" d="M60 84c-6-8 6-14 0-24s4-14 0-22" fill="none" stroke="#fbf0e8" stroke-width="2" stroke-linecap="round" opacity=".6"/>
    </svg>
    <div class="swap">
      <div class="before">
        <p class="txt a" style="--d:.5">Ferme les yeux,<br>fais un vœu.</p>
        <p style="margin:18px 0 0"><button class="btn a" style="--d:1.1" id="blow" type="button">Souffler la bougie</button></p>
      </div>
      <div class="after">
        <p class="script name" style="font-size:clamp(44px,14vw,68px)">Que ton vœu<br>se réalise</p>
      </div>
    </div>
  </section>

  <section class="slide" id="s-final" aria-label="Je t'aime">
    <svg class="heart a" style="--d:.1" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>
    <h2 class="script name a" style="--d:.6">Je t’aime</h2>
    <p class="txt a" style="--d:1.4">Joyeux anniversaire, mon cœur.</p>
    <p class="script sign a" style="--d:2.2" id="signature"></p>
    <button class="btn a" style="--d:3;font-size:15px;padding:11px 24px" id="replay" type="button">Revoir</button>
  </section>

</main>

<div id="hint">Touche pour continuer</div>

<script>
/* ===== À personnaliser ===== */
var CONFIG = {
  nom: "mon amour",            // prénom ou surnom
  signature: "Alessandro",     // signature en bas
  raisons: [                   // ce que tu aimes chez elle
    "Tes yeux",
    "Ton sourire",
    "Ton côté attentionné",
    "Et même, parfois, ta jalousie"
  ]
};
/* =========================== */

(function(){
  var reduce = window.matchMedia && matchMedia("(prefers-reduced-motion: reduce)").matches;
  var slides = Array.prototype.slice.call(document.querySelectorAll(".slide"));
  var bar = document.getElementById("bar");
  var hint = document.getElementById("hint");
  var idx = 0;

  /* textes */
  document.querySelectorAll("[data-bind='nom']").forEach(function(e){ e.textContent = CONFIG.nom; });
  document.getElementById("signature").textContent = CONFIG.signature;
  var ul = document.getElementById("reasons");
  CONFIG.raisons.forEach(function(t,i){
    var li = document.createElement("li");
    li.className = "a"; li.style.setProperty("--d", (0.6 + i * 0.9).toFixed(2));
    li.textContent = t; ul.appendChild(li);
  });
  document.querySelectorAll("[data-split]").forEach(function(el){
    var text = el.textContent, n = 0;
    el.setAttribute("aria-label", text); el.textContent = "";
    el.style.setProperty("--b", el.getAttribute("data-b") || "0s");
    text.split(" ").forEach(function(word, wi, all){
      var w = document.createElement("span"); w.className = "w"; w.setAttribute("aria-hidden","true");
      word.split("").forEach(function(ch){
        var s = document.createElement("span"); s.className = "ch"; s.style.setProperty("--i", n++); s.textContent = ch; w.appendChild(s);
      });
      el.appendChild(w);
      if (wi < all.length - 1){ el.appendChild(document.createTextNode(" ")); n++; }
    });
  });

  /* barre de progression */
  slides.forEach(function(){ bar.appendChild(document.createElement("i")); });

  /* ===== fond : pétales + éclats ===== */
  var fx = document.getElementById("fx"), c = fx.getContext("2d"), W, H, DPR;
  var petals = [], bursts = [], cols = ["234,170,182","220,180,143","255,111,134","251,240,232"];
  function resize(){
    DPR = Math.min(window.devicePixelRatio || 1, 2); W = innerWidth; H = innerHeight;
    fx.width = W * DPR; fx.height = H * DPR; c.setTransform(DPR,0,0,DPR,0,0);
  }
  function mkPetal(top){
    return { x:Math.random()*W, y: top ? -20 : Math.random()*H, r:4+Math.random()*7, vy:.25+Math.random()*.5,
      vx:(Math.random()-.5)*.3, rot:Math.random()*6.28, vr:(Math.random()-.5)*.02, ph:Math.random()*6.28,
      a:.2+Math.random()*.35, col:cols[(Math.random()*3)|0] };
  }
  function burst(x,y,n){
    if (reduce) return;
    for (var i=0;i<n;i++){
      var a = Math.random()*6.28, s = 1.5+Math.random()*4.5;
      bursts.push({ x:x, y:y, vx:Math.cos(a)*s, vy:Math.sin(a)*s-2, life:0, max:70+Math.random()*60,
        r:3+Math.random()*5, rot:Math.random()*6.28, vr:(Math.random()-.5)*.2, col:cols[(Math.random()*4)|0] });
    }
  }
  function petal(x,y,r,rot,col,a){
    c.save(); c.translate(x,y); c.rotate(rot); c.fillStyle = "rgba("+col+","+a+")";
    c.beginPath(); c.ellipse(0,0,r,r*.58,0,0,6.2832); c.fill(); c.restore();
  }
  function frame(){
    c.clearRect(0,0,W,H);
    petals.forEach(function(p){
      if (!reduce){ p.ph += .012; p.x += p.vx + Math.sin(p.ph)*.35; p.y += p.vy; p.rot += p.vr;
        if (p.y > H + 20){ Object.assign(p, mkPetal(true)); } }
      petal(p.x,p.y,p.r,p.rot,p.col,p.a);
    });
    for (var i=bursts.length-1;i>=0;i--){
      var b = bursts[i]; b.life++; b.vy += .07; b.vx *= .99; b.x += b.vx; b.y += b.vy; b.rot += b.vr;
      var a = Math.max(0, 1 - b.life/b.max);
      petal(b.x,b.y,b.r,b.rot,b.col,a*.9);
      if (b.life > b.max) bursts.splice(i,1);
    }
    if (!document.hidden) requestAnimationFrame(frame);
  }
  document.addEventListener("visibilitychange", function(){ if(!document.hidden) requestAnimationFrame(frame); });
  addEventListener("resize", resize);
  resize();
  for (var k=0;k<(reduce?10:24);k++) petals.push(mkPetal(false));
  if (reduce){ frame(); } else { requestAnimationFrame(frame); }

  /* ===== compteur ===== */
  var countRun = 0;
  function runCount(){
    var el = document.getElementById("counter"), target = 1001, dur = 2600, t0 = null, id = ++countRun;
    if (reduce){ el.textContent = target; return; }
    el.textContent = "0";
    setTimeout(function(){
      function step(ts){
        if (id !== countRun) return;
        if (!t0) t0 = ts;
        var p = Math.min((ts - t0)/dur, 1), e = 1 - Math.pow(1-p, 3);
        el.textContent = Math.round(e*target);
        if (p < 1) requestAnimationFrame(step);
      }
      requestAnimationFrame(step);
    }, 500);
  }

  /* ===== constellation en forme de coeur ===== */
  var starRun = 0;
  function runStars(){
    var cv = document.getElementById("stars"), id = ++starRun;
    var d = Math.min(window.devicePixelRatio||1, 2), w = cv.clientWidth, h = cv.clientHeight;
    cv.width = w*d; cv.height = h*d; var g = cv.getContext("2d"); g.setTransform(d,0,0,d,0,0);
    var N = 38, sc = Math.min(w/38, h/36), pts = [];
    for (var i=0;i<N;i++){
      var t = Math.PI + i/N*Math.PI*2;
      var x = 16*Math.pow(Math.sin(t),3), y = -(13*Math.cos(t)-5*Math.cos(2*t)-2*Math.cos(3*t)-Math.cos(4*t));
      pts.push({ x:w/2 + x*sc, y:h/2 + (y-1)*sc, at: 500 + i*75 });
    }
    var bg = []; for (var j=0;j<34;j++) bg.push({ x:Math.random()*w, y:Math.random()*h, r:.6+Math.random()*1.3, ph:Math.random()*6.28 });
    var t0 = null;
    function draw(ts){
      if (id !== starRun) return;
      if (!t0) t0 = ts; var t = reduce ? 1e6 : ts - t0;
      g.clearRect(0,0,w,h);
      bg.forEach(function(s){ var a = .25 + .35*Math.sin(t/700 + s.ph); g.fillStyle = "rgba(251,240,232,"+Math.max(a,.08)+")"; g.beginPath(); g.arc(s.x,s.y,s.r,0,6.2832); g.fill(); });
      var shown = pts.filter(function(p){ return t > p.at; });
      if (shown.length > 1){
        g.strokeStyle = "rgba(220,180,143,.55)"; g.lineWidth = 1; g.beginPath();
        shown.forEach(function(p,i){ i ? g.lineTo(p.x,p.y) : g.moveTo(p.x,p.y); });
        if (shown.length === N) g.closePath();
        g.stroke();
      }
      if (shown.length === N){
        var pulse = .08 + .05*Math.sin(t/500);
        g.fillStyle = "rgba(255,111,134,"+pulse+")"; g.fill();
      }
      shown.forEach(function(p){
        var age = Math.min((t - p.at)/500, 1), r = 2.2 + 1.2*Math.sin(t/400 + p.x);
        var grd = g.createRadialGradient(p.x,p.y,0,p.x,p.y,r*5);
        grd.addColorStop(0,"rgba(255,226,190,"+(.9*age)+")"); grd.addColorStop(1,"rgba(255,226,190,0)");
        g.fillStyle = grd; g.beginPath(); g.arc(p.x,p.y,r*5,0,6.2832); g.fill();
        g.fillStyle = "rgba(255,246,232,"+age+")"; g.beginPath(); g.arc(p.x,p.y,r*.7,0,6.2832); g.fill();
      });
      if (!reduce) requestAnimationFrame(draw);
    }
    requestAnimationFrame(draw);
  }

  /* ===== navigation ===== */
  var timers = [];
  function later(fn, ms){ timers.push(setTimeout(fn, ms)); }
  function show(n){
    if (n < 0 || n >= slides.length) return;
    timers.forEach(clearTimeout); timers = [];
    slides[idx].classList.remove("active");
    idx = n;
    var s = slides[idx];
    s.classList.remove("blown");
    void s.offsetWidth;
    s.classList.add("active");
    Array.prototype.forEach.call(bar.children, function(b,i){ b.classList.toggle("on", i <= idx); });
    hint.classList.toggle("off", idx === 0 || idx > 2);
    starRun++; countRun++;
    if (s.id === "s-count") runCount();
    if (s.id === "s-stars") runStars();
    if (s.id === "s-final"){ [500,1500,2600].forEach(function(ms,i){ later(function(){ burst(W*(.3+.2*i), H*.42, 26); }, ms); }); }
    if (s.id === "s-hello"){ later(function(){ burst(W/2, H*.4, 22); }, 1900); }
  }
  var downX = null, downY = 0;
  var stage = document.getElementById("stage");
  stage.addEventListener("pointerdown", function(e){ downX = e.clientX; downY = e.clientY; });
  stage.addEventListener("pointerup", function(e){
    if (downX === null) return;
    var dx = e.clientX - downX, dy = e.clientY - downY; downX = null;
    if (e.target.closest("button")) return;
    if (Math.abs(dx) > 50 && Math.abs(dx) > Math.abs(dy)){ show(idx + (dx < 0 ? 1 : -1)); return; }
    if (Math.abs(dx) < 12 && Math.abs(dy) < 12){ show(idx + (e.clientX < innerWidth*.3 ? -1 : 1)); }
  });
  addEventListener("keydown", function(e){
    if (e.key === "ArrowRight" || e.key === " ") show(idx+1);
    if (e.key === "ArrowLeft") show(idx-1);
  });
  document.getElementById("open").addEventListener("click", function(){ burst(W/2, H*.55, 30); show(1); });
  document.getElementById("blow").addEventListener("click", function(){
    slides[idx].classList.add("blown"); burst(W/2, H*.3, 46);
    later(function(){ burst(W*.3, H*.35, 24); burst(W*.7, H*.35, 24); }, 500);
  });
  document.getElementById("replay").addEventListener("click", function(){ show(0); });

  Array.prototype.forEach.call(bar.children, function(b,i){ b.classList.toggle("on", i === 0); });
})();
</script>
</body>
</html>