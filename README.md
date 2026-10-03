<!DOCTYPE html>
<html lang="it"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Il cristianesimo in Cina</title>
<style>
:root{--gold:#ffd166;--jade:#2ec4a0;--red:#e63946;--plum:#7b2cbf;--ink:#fff8e7;--bg:#14040a;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0d0207}}
:root[data-theme="dark"]{--bg:#0d0207}
*{box-sizing:border-box;margin:0}
html,body{height:100%;background:var(--bg);color:var(--ink);font-family:Georgia,'Songti SC',serif;overflow:hidden}
section{position:absolute;inset:0;display:none;flex-direction:column;justify-content:center;padding:5vh 7vw 10vh;overflow-y:auto;background-size:300% 300%;animation:flow 14s ease-in-out infinite alternate}
section.on{display:flex}
@keyframes flow{from{background-position:0 0}to{background-position:100% 100%}}
.g1{background-image:linear-gradient(120deg,#b5121b,#ff7b00,#7b2cbf,#b5121b)}
.g2{background-image:linear-gradient(120deg,#023e47,#2ec4a0,#1b2a6b,#023e47)}
.g3{background-image:linear-gradient(120deg,#5a189a,#e63946,#ff9e00,#5a189a)}
.g4{background-image:linear-gradient(120deg,#0b1f5c,#5a189a,#c1121f,#0b1f5c)}
.g5{background-image:linear-gradient(120deg,#a4161a,#6a0572,#10002b,#a4161a)}
.g6{background-image:linear-gradient(120deg,#0a6e5c,#0b4f6c,#f4a300,#0a6e5c)}
.g7{background-image:linear-gradient(120deg,#ffb703,#e63946,#7b2cbf,#ffb703)}
h1{font-size:clamp(2.3rem,7.5vw,5rem);line-height:1.05;background:linear-gradient(90deg,#fff3b0,#ffd166,#ff9e9e,#fff3b0);background-size:250% 100%;-webkit-background-clip:text;background-clip:text;color:transparent;animation:shine 5s linear infinite}
@keyframes shine{to{background-position:250% 0}}
h2{font-size:clamp(1.6rem,4.3vw,2.8rem);margin-bottom:.4em;text-shadow:0 2px 14px rgba(0,0,0,.4)}
h3{font-size:1.15rem;margin-bottom:.3em;color:var(--gold)}
p{font-size:clamp(.95rem,1.7vw,1.15rem);line-height:1.5;max-width:60ch}
.sub{font-size:clamp(1rem,2.2vw,1.5rem);margin-top:.8em;color:#fff3b0}
.r{position:relative;z-index:2}
.on .r{animation:pop .7s cubic-bezier(.2,1.3,.4,1) both;animation-delay:calc(var(--i)*.12s)}
@keyframes pop{from{opacity:0;transform:translateY(30px) scale(.9)}to{opacity:1;transform:none}}
.lan{position:fixed;bottom:-60px;z-index:1;font-size:2rem;animation:rise linear infinite;opacity:.75;pointer-events:none}
@keyframes rise{0%{transform:translate(0,0) rotate(-8deg)}50%{transform:translate(30px,-55vh) rotate(8deg)}100%{transform:translate(-20px,-115vh) rotate(-8deg)}}
.ring{position:absolute;right:-90px;top:50%;margin-top:-210px;width:420px;height:420px;border-radius:50%;border:3px dashed rgba(255,209,102,.6);animation:spin 30s linear infinite;z-index:1}
.ring::after{content:"";position:absolute;inset:40px;border-radius:50%;border:2px solid rgba(46,196,160,.7);animation:spin 18s linear infinite reverse}
@keyframes spin{to{transform:rotate(360deg)}}
.seal{position:absolute;right:calc(7vw + 40px);top:50%;margin-top:-50px;width:100px;height:100px;border-radius:10px;background:linear-gradient(135deg,#ffd166,#e63946);display:grid;place-items:center;font-size:3.6rem;color:#4a0404;z-index:2;animation:beat 2.4s ease-in-out infinite}
@keyframes beat{50%{transform:scale(1.15) rotate(6deg)}}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:16px;margin-top:16px}
.card{padding:16px 18px;border-radius:14px;background:rgba(255,255,255,.12);backdrop-filter:blur(6px);border:1px solid rgba(255,255,255,.3);border-top:4px solid var(--c,var(--gold));transition:transform .3s}
.card:hover{transform:translateY(-6px) rotate(-1deg)}
.card h3{color:var(--c,var(--gold))}
.card:nth-child(1){--c:#ffd166}.card:nth-child(2){--c:#5eead4}.card:nth-child(3){--c:#ff8fa3}.card:nth-child(4){--c:#c4a1ff}
.float{animation:bob 4s ease-in-out infinite}
@keyframes bob{50%{transform:translateY(-8px)}}
.tl{position:relative;display:flex;margin-top:30px;overflow-x:auto;padding:14px 0 8px}
.tl::before{content:"";position:absolute;top:22px;left:0;height:4px;width:100%;background:linear-gradient(90deg,#ffd166,#ff8fa3,#5eead4,#c4a1ff,#ffd166);background-size:300% 100%;animation:shine 6s linear infinite}
.ev{flex:1 0 150px;padding:26px 10px 0 0;position:relative}
.ev::before{content:"";position:absolute;top:8px;left:0;width:18px;height:18px;border-radius:50%;background:var(--c);box-shadow:0 0 0 0 var(--c);animation:pulse 2.4s infinite;animation-delay:calc(var(--i)*.4s)}
@keyframes pulse{70%{box-shadow:0 0 0 14px transparent}}
.ev b{display:block;font-size:1.3rem;color:var(--c)}
.ev span{font-size:.92rem;line-height:1.35;display:block}
.dots{display:grid;grid-template-columns:repeat(10,1fr);gap:clamp(5px,1.1vw,10px);width:min(330px,80vw)}
.dots i{aspect-ratio:1;border-radius:50%;background:rgba(255,255,255,.15);transition:all .5s cubic-bezier(.2,1.6,.4,1);transition-delay:var(--d)}
.dots i.l{background:radial-gradient(circle at 30% 30%,#fff3b0,#ffb703);box-shadow:0 0 12px #ffd166;transform:scale(1.15)}
.dots i.l:nth-child(odd){animation:tw 2s infinite}
@keyframes tw{50%{box-shadow:0 0 22px #ff9e00}}
.chart{display:flex;flex-wrap:wrap;gap:28px;align-items:center;margin-top:12px}
.tabs{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:12px}
.tabs button{border:2px solid var(--gold);background:rgba(0,0,0,.25);color:var(--ink);padding:8px 14px;border-radius:999px;font:inherit;cursor:pointer;transition:.3s}
.tabs button.a{background:var(--gold);color:#4a0404;font-weight:bold}
.num{font-size:clamp(3.4rem,10vw,6rem);line-height:1;font-weight:bold;background:linear-gradient(90deg,#ffd166,#ff8fa3);-webkit-background-clip:text;background-clip:text;color:transparent}
.two{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:18px;margin-top:14px}
.road{display:flex;align-items:center;gap:10px;margin-top:16px;font-size:1.05rem;flex-wrap:wrap}
.road .city{padding:6px 12px;border-radius:999px;background:rgba(255,255,255,.18)}
.road .arr{flex:1 1 60px;height:4px;border-radius:2px;background:repeating-linear-gradient(90deg,#ffd166 0 10px,transparent 10px 20px);background-size:40px 4px;animation:march 1s linear infinite}
@keyframes march{to{background-position:40px 0}}
nav{position:fixed;bottom:calc(14px + env(safe-area-inset-bottom,0px));left:0;right:0;display:flex;justify-content:center;align-items:center;gap:16px;z-index:9}
nav button{width:40px;height:40px;border:0;border-radius:50%;background:linear-gradient(135deg,#ffd166,#ff8fa3);color:#4a0404;font-size:1.3rem;cursor:pointer}
nav button:focus-visible,.tabs button:focus-visible{outline:3px solid #fff}
#ct{min-width:52px;text-align:center;font-size:.9rem}
#bar{position:fixed;top:env(safe-area-inset-top,0px);left:0;height:5px;width:0;background:linear-gradient(90deg,#ffd166,#5eead4,#c4a1ff,#ff8fa3);transition:width .5s;z-index:9}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style></head><body>
<div id="bar"></div>

<section class="g1 on">
  <div class="ring"></div><div class="seal">信</div>
  <h1 class="r" style="--i:0">Il cristianesimo<br>in Cina</h1>
  <p class="sub r" style="--i:2">Radici antiche, controllo di Stato e una fede che cresce nell'ombra</p>
  <p class="r" style="--i:3;margin-top:1.6em">🏮 dal 1949 a oggi</p>
</section>

<section class="g2">
  <h2 class="r" style="--i:0">Tra tolleranza e repressione</h2>
  <div class="tl">
    <div class="ev r" style="--i:1;--c:#ffd166"><b>1949</b><span>Nasce la Repubblica Popolare Cinese: il PCC, ufficialmente ateo, prende il potere</span></div>
    <div class="ev r" style="--i:2;--c:#ff8fa3"><b>Anni '50</b><span>Missionari stranieri espulsi; nascono le organizzazioni patriottiche di Stato</span></div>
    <div class="ev r" style="--i:3;--c:#c4a1ff"><b>1966–76</b><span>Rivoluzione Culturale: ogni espressione religiosa è bandita e nascono le chiese domestiche</span></div>
    <div class="ev r" style="--i:4;--c:#ff6b6b"><b>Oggi</b><span>Religione ammessa solo se sottomessa al Partito</span></div>
  </div>
  <p class="r float" style="--i:5;margin-top:22px">Paradosso: la clandestinità ha alimentato una crescita esponenziale dei credenti.</p>
</section>

<section class="g3">
  <h2 class="r" style="--i:0">Quanti sono i cristiani?</h2>
  <div class="tabs r" style="--i:1" id="tabs">
    <button data-v="2" data-t="1–2" data-n="Sondaggi ufficiali">Sondaggi ufficiali</button>
    <button data-v="5" data-t="5,1" data-n="CIA World Factbook">CIA Factbook</button>
    <button data-v="7" data-t="6,7" data-n="Open Doors · circa 96,7 milioni">Open Doors</button>
  </div>
  <div class="chart r" style="--i:2">
    <div class="dots" id="dots"></div>
    <div><div class="num"><span id="pc">5,1</span>%</div><p id="pn"></p><p style="font-size:.9rem;margin-top:10px;opacity:.9">Ogni pallino è 1 persona su 100. Molti fedeli non si dichiarano per paura di ritorsioni.</p></div>
  </div>
</section>

<section class="g4">
  <h2 class="r" style="--i:0">Un doppio binario</h2>
  <div class="two">
    <div class="card r float" style="--i:1"><h3>⛩ Chiese ufficiali</h3><p>Registrate e controllate dallo Stato: TSPM per i protestanti, CPA per i cattolici.</p></div>
    <div class="card r float" style="--i:2;animation-delay:-2s;--c:#5eead4"><h3>🏠 Chiese domestiche</h3><p>Reti clandestine in case, uffici e magazzini, lontane dall'ingerenza del governo.</p></div>
  </div>
  <div class="r" style="--i:3;margin-top:24px"><div class="num">17°</div><p>posto nella World Watch List di Porte Aperte</p></div>
</section>

<section class="g5">
  <h2 class="r" style="--i:0">Sotto Xi Jinping: controllo tecnologico</h2>
  <p class="r" style="--i:1">Niente esecuzioni di massa, ma una pressione costante.</p>
  <div class="grid">
    <div class="card r float" style="--i:2"><h3>☭ Sinizzazione</h3><p>Fede allineata ai valori socialisti: croci rimosse, sermoni modificati.</p></div>
    <div class="card r float" style="--i:3;animation-delay:-1.3s"><h3>🚫 Minori esclusi</h3><p>Vietati agli under-18 culto, catechismo e campi estivi.</p></div>
    <div class="card r float" style="--i:4;animation-delay:-2.6s"><h3>📹 Sorveglianza</h3><p>Riconoscimento facciale, raid, multe, arresti e confisca di Bibbie.</p></div>
  </div>
</section>

<section class="g6">
  <h2 class="r" style="--i:0">Missionari: da stranieri a cinesi</h2>
  <div class="two">
    <div class="card r" style="--i:1"><div class="num">0%</div><p>Missionari stranieri ufficialmente presenti: evangelizzare è reato e i tentmakers sono stati espulsi.</p></div>
    <div class="card r" style="--i:2;--c:#5eead4"><h3>🐉 Ritorno a Gerusalemme</h3><p>Le chiese domestiche inviano missionari cinesi verso Paesi buddisti, induisti e islamici.</p></div>
  </div>
  <div class="road r" style="--i:3"><span class="city">🏯 Cina</span><span class="arr"></span><span class="city">🐪 Via della Seta</span><span class="arr"></span><span class="city">🕌 Gerusalemme</span></div>
</section>

<section class="g7">
  <h2 class="r" style="--i:0">Motivi di preghiera</h2>
  <div class="grid">
    <div class="card r float" style="--i:1"><h3>🏮 Leader</h3><p>Saggezza e forza per i pastori sotto sorveglianza.</p></div>
    <div class="card r float" style="--i:2;animation-delay:-1s"><h3>🌱 Nuove generazioni</h3><p>Vie sicure per insegnare la Bibbia ai figli.</p></div>
    <div class="card r float" style="--i:3;animation-delay:-2s"><h3>🛡 Convertiti</h3><p>Resilienza contro la doppia emarginazione.</p></div>
    <div class="card r float" style="--i:4;animation-delay:-3s"><h3>🕊 Libertà</h3><p>Politiche meno restrittive, senza scegliere tra Dio e Stato.</p></div>
  </div>
</section>

<nav><button id="p" aria-label="Indietro">‹</button><span id="ct"></span><button id="n" aria-label="Avanti">›</button></nav>
<script>
var s=[].slice.call(document.querySelectorAll('section')),i=0,ct=document.getElementById('ct'),bar=document.getElementById('bar');
for(var k=0;k<9;k++){var l=document.createElement('div');l.className='lan';l.textContent=k%3?'🏮':'🧧';l.style.left=(k*12+3)+'%';l.style.animationDuration=(16+k*2)+'s';l.style.animationDelay=(-k*3)+'s';document.body.appendChild(l)}
function go(n){i=Math.max(0,Math.min(s.length-1,n));s.forEach(function(e,j){e.classList.toggle('on',j===i)});ct.textContent=(i+1)+' / '+s.length;bar.style.width=((i+1)/s.length*100)+'%';if(i===2)pick(1)}
document.getElementById('p').onclick=function(){go(i-1)};
document.getElementById('n').onclick=function(){go(i+1)};
document.addEventListener('keydown',function(e){if(e.key==='ArrowRight'||e.key===' ')go(i+1);if(e.key==='ArrowLeft')go(i-1)});
var x=0;document.addEventListener('touchstart',function(e){x=e.touches[0].clientX});
document.addEventListener('touchend',function(e){var d=e.changedTouches[0].clientX-x;if(Math.abs(d)>60)go(d<0?i+1:i-1)});
var dots=document.getElementById('dots'),tb=[].slice.call(document.querySelectorAll('#tabs button')),auto,cur=0;
for(k=0;k<100;k++){var d=document.createElement('i');dots.appendChild(d)}
function pick(n){cur=n;var b=tb[n],v=+b.dataset.v;tb.forEach(function(t){t.classList.toggle('a',t===b)});
[].forEach.call(dots.children,function(e,j){e.style.setProperty('--d',(j<v?j*70:0)+'ms');e.classList.toggle('l',j<v)});
document.getElementById('pc').textContent=b.dataset.t;document.getElementById('pn').textContent=b.dataset.n}
tb.forEach(function(b,n){b.onclick=function(){clearInterval(auto);pick(n)}});
auto=setInterval(function(){if(i===2)pick((cur+1)%3)},3500);
go(0);
</script></body></html>
