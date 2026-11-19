<!DOCTYPE html>
<html lang="es-MX">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Liberache Versión Revista</title>
<meta name="description" content="Revista de Estudio Liberache: recorridos virtuales, prototipo de tu casa con planos, materiales y presupuesto. Tepic y Xalisco.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,400..900;1,6..96,400..900&family=Jost:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
/* Una revista física sobre la mesa: portada, pliegos a dos hojas, didona y filetes finos, rojo de cabecera. */
:root{
  --table:#D7D3CC; --paper:#FBFAF8; --white:#FFFFFF; --ink:#111111; --muted:#6C6964; --rule:#DAD7D1;
  --red:#9E1B1E; --blush:#F1E7E1; --plan:#2B4C9B; --night:#0F0F10;
  --ok:#2E7A4E; --warn:#A8701B; --bad:#AF3A3A;
  --didone:'Bodoni Moda','Didot','Bodoni 72',Georgia,serif;
  --sans:'Jost','Futura','Avenir Next',system-ui,sans-serif;
  --mono:'IBM Plex Mono',ui-monospace,Menlo,monospace;
  --pw:480px; --ph:650px;
  color-scheme: light;
}
*{box-sizing:border-box}
[hidden]{display:none!important}
html,body{height:100%}
body{margin:0;background:radial-gradient(ellipse at 50% 40%,#E4E1DB 0%,var(--table) 60%,#C9C4BB 100%);color:var(--ink);font:400 15px/1.55 var(--sans);-webkit-font-smoothing:antialiased;overflow:hidden}
@media (prefers-reduced-motion: reduce){*{transition:none!important;animation:none!important}}
h1,h2,h3{margin:0;font-family:var(--didone);font-weight:500;line-height:1;text-wrap:balance}
p{margin:0}
a{color:inherit}
:focus-visible{outline:2px solid var(--red);outline-offset:2px}
.kicker{font:500 max(10px,1.9cqw)/1.3 var(--sans);letter-spacing:.24em;text-transform:uppercase;color:var(--red)}
.num{font-variant-numeric:tabular-nums lining-nums}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:.6em;min-height:44px;padding:.75em 1.3em;font:500 .74rem/1 var(--sans);letter-spacing:.18em;text-transform:uppercase;text-decoration:none;border:1px solid var(--ink);cursor:pointer;border-radius:0;transition:background .2s,color .2s}
.btn-ink{background:var(--ink);color:#fff}.btn-ink:hover{background:var(--red);border-color:var(--red)}
.btn-line{background:transparent;color:var(--ink)}.btn-line:hover{background:var(--ink);color:#fff}
.btn-red{background:var(--red);border-color:var(--red);color:#fff}.btn-red:hover{background:#7E1416}
.btn-paper{border-color:#EDEBE6;color:#EDEBE6;background:transparent}.btn-paper:hover{background:#EDEBE6;color:var(--ink)}

/* ===== mesa, libro y hojas ===== */
.stage{height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:10px;padding:12px 0 0}
.book{position:relative;width:calc(var(--pw) * 2);height:var(--ph);perspective:3000px;transition:transform .76s cubic-bezier(.45,.05,.25,1)}
.book.is-closed-front{transform:translateX(calc(var(--pw) * -.5))}
.book.is-closed-back{transform:translateX(calc(var(--pw) * .5))}
.slot{position:absolute;top:0;width:var(--pw);height:var(--ph)}
#slotL{left:0}#slotR{left:var(--pw)}
.slot:not(:empty){box-shadow:0 26px 60px -24px rgba(0,0,0,.5),0 2px 6px rgba(0,0,0,.08)}
.book.single{width:var(--pw)}
.book.single #slotL{display:none}
.book.single #slotR{left:0}
.leaf{position:absolute;top:0;width:var(--pw);height:var(--ph);transform-style:preserve-3d;transition:transform .76s cubic-bezier(.45,.05,.25,1);z-index:30}
.leaf.fwd{left:var(--pw);transform-origin:left center}
.leaf.bwd{left:0;transform-origin:right center}
.single .leaf.fwd{left:0}
.face{position:absolute;inset:0;backface-visibility:hidden;-webkit-backface-visibility:hidden;overflow:hidden;background:var(--white);box-shadow:0 20px 50px -20px rgba(0,0,0,.45)}
.face-back{transform:rotateY(180deg)}
.face .edge{display:none}
#slotL > .pg::after{content:'';position:absolute;top:0;bottom:0;right:0;width:9%;background:linear-gradient(270deg,rgba(0,0,0,.16),rgba(0,0,0,0));pointer-events:none;z-index:4}
#slotR > .pg::after{content:'';position:absolute;top:0;bottom:0;left:0;width:9%;background:linear-gradient(90deg,rgba(0,0,0,.18),rgba(0,0,0,0));pointer-events:none;z-index:4}
.single #slotR > .pg::after{display:none}
.book.is-closed-front #slotR > .pg::after,.book.is-closed-back #slotL > .pg::after{display:none}
.edge{position:absolute;top:0;bottom:0;width:max(22px,5cqw);border:0;background:transparent;cursor:pointer;z-index:6;padding:0}
.edge-r{right:0}.edge-l{left:0}
#slotL .edge-r,#slotR .edge-l{display:none}
.single #slotR .edge-l{display:block}
.edge:hover{background:linear-gradient(90deg,rgba(0,0,0,0),rgba(0,0,0,.05))}
.edge-l:hover{background:linear-gradient(270deg,rgba(0,0,0,0),rgba(0,0,0,.05))}
.edge-r::after{content:'';position:absolute;right:0;bottom:0;border-style:solid;border-width:0 0 26px 26px;border-color:transparent transparent #E7E3DC transparent;filter:drop-shadow(-2px -2px 2px rgba(0,0,0,.15));transition:border-width .2s}
.edge-r:hover::after{border-width:0 0 44px 44px}
.edge-l::after{content:'';position:absolute;left:0;bottom:0;border-style:solid;border-width:26px 0 0 26px;border-color:transparent transparent transparent #E7E3DC;filter:drop-shadow(2px -2px 2px rgba(0,0,0,.15));transition:border-width .2s}
.edge-l:hover::after{border-width:44px 0 0 44px}
.pg-tour .edge-r{background:linear-gradient(90deg,rgba(0,0,0,0),rgba(0,0,0,.45))}
.pg-tour .edge-r::before{content:'›';position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);color:#fff;font:400 28px/1 var(--didone)}

.controls{display:flex;align-items:center;gap:6px;height:52px}
.controls button{appearance:none;border:1px solid rgba(17,17,17,.25);background:rgba(251,250,248,.85);height:38px;padding:0 14px;font:500 .68rem/1 var(--sans);letter-spacing:.18em;text-transform:uppercase;cursor:pointer;color:var(--ink)}
.controls button:disabled{opacity:.35;cursor:default}
.controls .ctl-arrow{font:400 1.3rem/1 var(--didone);padding:0 14px;letter-spacing:0}
.ctl-count{min-width:120px;text-align:center;font:italic 500 1rem var(--didone)}
.ctl-hint{font:italic 400 .95rem var(--didone);color:#4A4743;margin-left:10px}
@media (max-width:860px){.ctl-hint{display:none}}

/* ===== página base ===== */
#store{display:none}
.pg{position:relative;width:100%;height:100%;background:var(--white);container-type:size;overflow:hidden;display:flex;flex-direction:column;padding:calc(var(--pw) * .075) calc(var(--pw) * .08) calc(var(--pw) * .05);gap:calc(var(--ph) * .024);font-size:max(12.5px,calc(var(--pw) * .028))}
.folio{margin-top:auto;display:flex;justify-content:space-between;align-items:baseline;padding-top:1.6cqh;border-top:1px solid var(--rule);font:500 max(9px,1.7cqw)/1 var(--sans);letter-spacing:.22em;text-transform:uppercase;color:var(--muted)}
.folio b{font:500 max(12px,2.8cqw) var(--didone);letter-spacing:0;color:var(--ink)}
.pg-dark{background:var(--night);color:#EDEBE6}
.pg-dark .folio{border-color:#2A2A2C;color:#8E8A83}.pg-dark .folio b{color:#EDEBE6}

/* portada */
.pg-cover{padding:0;cursor:pointer;background:#DCE1E4}
.cover-img{position:absolute;inset:0;background:linear-gradient(180deg,#DCE2E5 0%,#E7E5E0 62%,#C8C3B9 100%);background-size:cover;background-position:center 70%}
.cover-img:not(.has-photo)::after{content:'';position:absolute;left:12%;right:12%;bottom:12%;height:38%;background:no-repeat center/contain url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 250 160'%3E%3Cpath d='M20 150 V70 H120 V40 H230 V150 Z M34 86 h70 v44 h-70z M136 54 h80 v34 h-80z M140 102 h28 v48 h-28z M184 102 h32 v26 h-32z M0 150 H250' fill='none' stroke='%23333' stroke-width='1'/%3E%3C/svg%3E")}
.cover-in{position:relative;z-index:2;height:100%;display:flex;flex-direction:column;padding:4.5cqw 5.5cqw 5cqw}
.cover-rail{display:flex;justify-content:space-between;font:500 max(9px,1.7cqw)/1 var(--sans);letter-spacing:.24em;text-transform:uppercase}
.cover-mast{font:600 15.4cqw/.84 var(--didone);letter-spacing:-.045em;text-align:center;margin:1.6cqw -1cqw 0;white-space:nowrap}
.cover-tag{text-align:center;font:italic 400 max(12px,2.9cqw)/1.2 var(--didone);margin-top:.8cqw}
.cover-lines{margin-top:5cqh;display:grid;gap:2.2cqh;max-width:46%}
.cl{display:grid;gap:.6cqh}
.cl .kicker{font-size:max(9px,1.7cqw)}
.cl p{font:500 max(13px,3.2cqw)/1.12 var(--didone)}
.cl p b{font:500 max(9px,1.6cqw) var(--sans);letter-spacing:.14em;color:var(--red);margin-left:.4em}
.cover-big{margin-top:auto;padding:4cqw 5cqw 0;color:#fff;text-shadow:0 2px 18px rgba(0,0,0,.35)}
.cover-big p{font:italic 500 max(26px,8.4cqw)/.95 var(--didone);letter-spacing:-.02em}
.cover-foot{display:flex;justify-content:space-between;align-items:end;margin-top:3cqw;color:#fff;font:500 max(9px,1.7cqw)/1.4 var(--sans);letter-spacing:.22em;text-transform:uppercase;text-shadow:0 1px 8px rgba(0,0,0,.4)}
.cover-shade{position:absolute;left:0;right:0;bottom:0;height:46%;background:linear-gradient(180deg,rgba(0,0,0,0),rgba(0,0,0,.55));z-index:1;pointer-events:none}
.open-hint{display:inline-flex;align-items:center;gap:8px;background:#fff;color:var(--ink);text-shadow:none;padding:8px 12px}

/* índice */
.idx-title{font:italic 500 17cqw/.85 var(--didone);letter-spacing:-.03em}
.idx{list-style:none;margin:0;padding:0;border-top:1px solid var(--ink)}
.idx > li{border-bottom:1px solid var(--rule)}
.idx button{appearance:none;background:none;border:0;width:100%;display:flex;align-items:baseline;gap:2.4cqw;text-align:left;cursor:pointer;color:var(--ink);padding:1.5cqh 0;font:inherit}
.idx button:hover span{color:var(--red)}
.idx-item em{font:italic 500 max(15px,4.2cqw)/1 var(--didone);color:var(--red);min-width:7cqw}
.idx-item span{font:500 max(15px,4cqw)/1.1 var(--didone);display:grid}
.idx-item small{font:400 max(10px,2.1cqw)/1.3 var(--sans);color:var(--muted)}
.idx i{flex:1;border-bottom:1px dotted #B9B4AB;transform:translateY(-.3em)}
.idx b{font:500 max(12px,2.8cqw) var(--didone)}
.idx ol{list-style:none;margin:0 0 1.2cqh;padding:0 0 0 9.4cqw}
.idx-sub{padding:.5cqh 0!important}
.idx-sub span{font:400 max(12px,2.6cqw)/1.2 var(--sans)}
.idx-ed{display:grid;gap:1cqh;padding-top:1cqh}
.idx-ed p{font:italic 400 max(12px,2.7cqw)/1.45 var(--didone);color:#333}

/* apertura de recorridos */
.open-num{font:italic 500 30cqw/.8 var(--didone);color:var(--red);letter-spacing:-.04em}
.open-title{font:500 13cqw/.9 var(--didone);letter-spacing:-.03em}
.open-deck{font:italic 400 max(13px,3.2cqw)/1.35 var(--didone);color:#333}
.rec-list{list-style:none;margin:0;padding:0;border-top:1px solid var(--ink)}
.rec-list li{border-bottom:1px solid var(--rule)}
.rec-list button{appearance:none;background:none;border:0;width:100%;display:flex;align-items:center;gap:3cqw;text-align:left;cursor:pointer;padding:1.4cqh 0;color:var(--ink);font:inherit}
.rec-list em{font:italic 500 max(18px,5cqw)/1 var(--didone);color:var(--red)}
.rec-list span{flex:1;display:grid;font:500 max(14px,3.4cqw)/1.15 var(--didone)}
.rec-list small{font:400 max(10px,2cqw)/1.4 var(--sans);color:var(--muted)}
.rec-list b{font:500 max(10px,1.9cqw) var(--sans);letter-spacing:.14em;color:var(--muted)}
.rec-list button:hover span{color:var(--red)}
.how{font-size:max(11px,2.3cqw);color:var(--muted)}

/* proyecto */
.proj-title{font:italic 500 15cqw/.86 var(--didone);letter-spacing:-.03em}
.proj-head{font:500 max(16px,4.6cqw)/1.12 var(--didone)}
.proj-dek{color:var(--muted)}
.proj-dek::first-letter{font:500 3.3em/.8 var(--didone);float:left;margin:.06em .1em 0 0;color:var(--ink)}
.specs{display:grid;margin:0;border-top:1px solid var(--ink)}
.specs div{display:grid;grid-template-columns:32% 1fr;gap:2cqw;padding:1cqh 0;border-bottom:1px solid var(--rule)}
.specs dt{font:500 max(9px,1.7cqw)/1.7 var(--sans);letter-spacing:.2em;text-transform:uppercase;color:var(--muted)}
.specs dd{margin:0}
.proj-actions{display:flex;gap:8px;flex-wrap:wrap}
.proj-hint{font:italic 400 max(12px,2.7cqw) var(--didone);color:var(--red)}
.pg-tour{padding:0;gap:0;background:#141415}
.tour-frame{position:relative;flex:1;min-height:0;background:#141415}
.tour-frame iframe{position:absolute;inset:0;width:100%;height:100%;border:0;display:block}
.tour-poster{position:absolute;inset:0;display:grid;place-items:center;background:radial-gradient(ellipse at 30% 20%,#2A2A2C,#111113 70%);color:#EDEBE6;z-index:2}
.poster-inner{display:grid;gap:2cqh;justify-items:center;text-align:center;padding:6cqw}
.poster-num{font:italic 500 34cqw/.8 var(--didone);color:transparent;-webkit-text-stroke:1px #CFC9BE}
.poster-art{width:62cqw}.poster-art svg{width:100%;height:auto}
.poster-art svg *{fill:none;stroke:#BFB8AB;stroke-width:1}
.poster-msg{font:500 max(10px,1.9cqw)/1.5 var(--sans);letter-spacing:.2em;text-transform:uppercase;color:#CFC9BE}
.tour-cap{display:flex;justify-content:space-between;gap:12px;padding:1.6cqh 6cqw;background:var(--white);border-top:1px solid var(--rule);font:500 max(9px,1.7cqw)/1.6 var(--sans);letter-spacing:.2em;text-transform:uppercase;color:var(--muted)}
.tour-cap em{font:italic 500 max(13px,2.9cqw)/1.2 var(--didone);letter-spacing:0;text-transform:none;color:var(--ink)}

/* configurador en páginas */
.pg-cfg{gap:calc(var(--ph) * .016);padding-bottom:calc(var(--pw) * .04)}
.pg-cfg-head{display:flex;align-items:baseline;gap:3cqw;border-bottom:1px solid var(--ink);padding-bottom:1.4cqh}
.pg-cfg-head em{font:italic 500 max(30px,10cqw)/.8 var(--didone);color:var(--red)}
.pg-cfg-head h2{font-size:max(22px,6.6cqw);letter-spacing:-.02em}
.pg-scroll{flex:1;min-height:0;overflow:auto;padding-right:6px;margin-right:-6px;overscroll-behavior:contain}
.pg-scroll::-webkit-scrollbar{width:4px}.pg-scroll::-webkit-scrollbar-thumb{background:#C9C4BB}
/* configurador */
.cfg-grid{display:grid;grid-template-columns:minmax(300px,380px) minmax(0,1fr);gap:clamp(20px,3vw,40px);align-items:start}
@media (max-width:1000px){.cfg-grid{grid-template-columns:1fr}}
form.cfg{background:var(--white);border:1px solid var(--rule);padding:24px;display:grid;gap:20px;position:sticky;top:16px}
@media (max-width:1000px){form.cfg{position:static}}
.prog{display:grid;gap:6px}
.prog-track{height:2px;background:var(--rule)}
.prog-bar{display:block;height:100%;background:var(--red);width:0;transition:width .3s}
.prog-txt{font:500 .68rem/1.2 var(--sans);letter-spacing:.16em;text-transform:uppercase;color:var(--muted)}
fieldset{border:0;margin:0;padding:0;display:grid;gap:8px;min-width:0}
legend{font:500 1.1rem/1.2 var(--didone);padding:0;margin-bottom:10px}
.hint{font-size:.84rem;color:var(--muted)}
.seg{display:flex;flex-wrap:wrap;gap:6px}
.seg label{flex:1 1 auto;position:relative}
.seg input{position:absolute;opacity:0;inset:0;margin:0;cursor:pointer}
.seg label>span{display:flex;align-items:center;justify-content:center;min-height:42px;padding:6px 10px;border:1px solid var(--rule);background:var(--white);font:400 .9rem var(--sans);text-align:center;cursor:pointer}
.seg input:checked+span{background:var(--ink);color:#fff;border-color:var(--ink)}
.seg input:focus-visible+span{outline:2px solid var(--red);outline-offset:2px}
.acab label{flex:1 1 100%}
.acab label>span{flex-direction:column;align-items:flex-start;text-align:left;gap:3px;padding:12px 14px}
.acab b{font:500 1.05rem var(--didone)}
.acab small{font-size:.8rem;opacity:.75}
.acab .acab-precio{font:500 .74rem/1 var(--mono);opacity:.85}
.dims{display:grid;grid-template-columns:1fr auto 1fr auto;gap:8px;align-items:center}
.dims input{width:100%;min-height:44px;padding:6px 10px;border:1px solid var(--rule);font:500 1rem var(--mono);background:var(--white);border-radius:0}
.dims .x{color:var(--muted)}
.area-out{font:500 .85rem var(--mono);color:var(--plan)}
input[type=range]{width:100%;accent-color:var(--red)}
.budget-out{font:500 2rem/1 var(--didone)}
.gen{width:100%}
.res{display:grid;gap:18px;min-width:0}
.res-head{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:10px}
.pill{display:inline-flex;align-items:center;padding:5px 12px;font:500 .68rem/1.2 var(--sans);letter-spacing:.18em;text-transform:uppercase;border:1px solid var(--ink)}
.pill-ok{background:var(--ink);color:#fff}
.pill-warn{background:var(--blush);border-color:var(--red);color:var(--red)}
.kpis{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));border-top:1px solid var(--ink);border-bottom:1px solid var(--ink)}
.kpi{padding:14px 16px 16px;display:grid;gap:6px;align-content:start;border-right:1px solid var(--rule)}
.kpi:last-child{border-right:0}
.kpi small{font:500 .66rem/1.2 var(--sans);text-transform:uppercase;letter-spacing:.2em;color:var(--muted)}
.kpi strong{font:500 2.1rem/1 var(--didone);font-variant-numeric:lining-nums tabular-nums}
.status{display:grid;gap:4px;padding:14px 16px;border-left:3px solid}
.status b{font:500 1.15rem/1.15 var(--didone)}
.status span{font-size:.84rem;color:var(--muted)}
.status-ok{border-color:var(--ok)}.status-warn{border-color:var(--warn)}.status-bad{border-color:var(--bad)}
@media (max-width:720px){.kpis{grid-template-columns:repeat(2,minmax(0,1fr))}.kpi:nth-child(2){border-right:0}.kpi{border-bottom:1px solid var(--rule)}}
.advice{background:var(--blush);padding:16px 18px;display:grid;gap:8px;font-size:.95rem}
.advice b{font-family:var(--didone);font-weight:600}
.tabs{display:flex;gap:0;border-bottom:1px solid var(--rule);overflow-x:auto}
.tab{appearance:none;border:0;background:none;padding:12px 16px;font:500 .72rem var(--sans);letter-spacing:.2em;text-transform:uppercase;color:var(--muted);border-bottom:2px solid transparent;cursor:pointer;white-space:nowrap}
.tab[aria-selected=true]{color:var(--ink);border-color:var(--red)}
.viewer{position:relative;height:clamp(360px,60vh,620px);overflow:hidden;background:#DDE3E6;touch-action:none;outline:none}
.viewer:fullscreen{height:100%}
.viewer canvas{display:block;width:100%;height:100%;cursor:grab}
.v-bar{position:absolute;left:10px;right:10px;top:10px;display:flex;flex-wrap:wrap;gap:6px;align-items:center;pointer-events:none}
.v-bar>*{pointer-events:auto}
.vmode,.chip,.v-full{appearance:none;border:1px solid rgba(17,17,17,.2);background:rgba(255,255,255,.94);padding:8px 12px;font:500 .66rem var(--sans);letter-spacing:.16em;text-transform:uppercase;cursor:pointer;color:var(--ink)}
.vmode[aria-pressed=true]{background:var(--ink);color:#fff;border-color:var(--ink)}
.lvl-chips{display:flex;gap:6px}
.v-full{margin-left:auto}
.v-help{position:absolute;left:10px;bottom:10px;font:500 .72rem var(--mono);background:rgba(17,17,17,.75);color:#fff;padding:5px 9px}
.walk-room{position:absolute;right:10px;bottom:10px;font:italic 500 1rem var(--didone);background:rgba(17,17,17,.82);color:#fff;padding:7px 12px}
.pad{position:absolute;right:12px;bottom:52px;display:grid;grid-template-columns:repeat(3,46px);grid-template-rows:repeat(2,46px);gap:6px}
.pad button{appearance:none;border:0;background:rgba(17,17,17,.72);color:#fff;font-size:1.1rem;touch-action:none;cursor:pointer}
.pad .u{grid-column:2}.pad .tl{grid-column:1;grid-row:2}.pad .d{grid-column:2;grid-row:2}.pad .tr{grid-column:3;grid-row:2}
.viewer-msg{position:absolute;inset:auto 10px 50px 10px;background:#fff;padding:12px 14px;font-size:.9rem}
.plan-wrap{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:16px;background:var(--white);border:1px solid var(--rule);padding:18px}
.plan-fig{margin:0;display:grid;gap:6px}
.plan-fig figcaption{font:italic 500 1.1rem var(--didone);color:var(--ink)}
.plan-svg{width:100%;height:auto;max-height:560px}
.plan-svg .lot{fill:none;stroke:#B9B3A8;stroke-width:.05;stroke-dasharray:.3 .2}
.plan-svg .pl-wall{stroke:#151515;stroke-width:.16;stroke-linecap:square}
.plan-svg .pl-wall.low{stroke-width:.08;stroke:#6C6964}
.plan-svg .pl-win{stroke:var(--plan);stroke-width:.07}
.plan-svg .pl-door{fill:none;stroke:var(--red);stroke-width:.03}
.plan-svg .pl-step{stroke:#9A958C;stroke-width:.025}
.plan-svg .pl-dim{stroke:#9A958C;stroke-width:.025}
.plan-svg .pl-arrow{fill:none;stroke:var(--red);stroke-width:.08;stroke-linecap:round;stroke-linejoin:round}
.plan-svg text{font-family:var(--mono);fill:#151515}
.plan-svg .pl-area{fill:#6C6964}
.plan-svg .pl-cota,.plan-svg .pl-small{fill:#6C6964;font-size:.36px}
.plan-svg .pl-small{font-size:.3px}
.tbl-wrap{overflow-x:auto;background:var(--white);border:1px solid var(--rule)}
table{border-collapse:collapse;width:100%;font-size:.93rem}
th,td{text-align:left;padding:11px 14px;border-bottom:1px solid #ECE9E4;vertical-align:top}
th{font:500 .66rem var(--sans);text-transform:uppercase;letter-spacing:.2em;color:var(--muted)}
td.num{text-align:right;font-family:var(--mono);white-space:nowrap}
.note{font-size:.85rem;color:var(--muted);margin-top:10px;max-width:75ch}
.cost-card{background:var(--white);border:1px solid var(--rule);padding:20px;display:grid;gap:16px}
.cost-top{display:flex;flex-wrap:wrap;justify-content:space-between;gap:12px;align-items:end}
.cost-top strong{font:500 2.6rem/1 var(--didone)}
.meter{position:relative;height:8px;background:#ECE9E4;display:flex;overflow:hidden}
.meter-fill{height:100%}.m-ok{background:var(--ok)}.m-warn{background:var(--warn)}.m-bad{background:var(--bad)}
.meter-over{height:100%;background:repeating-linear-gradient(45deg,var(--bad) 0 6px,#D98C8C 6px 12px)}
.meter-legend{display:flex;justify-content:space-between;font:500 .72rem var(--mono);color:var(--muted)}
.bar-row{display:grid;grid-template-columns:minmax(140px,1.4fr) 2fr auto;gap:12px;align-items:center;font-size:.9rem}
.bar-track{height:8px;background:#F0EDE8;overflow:hidden}
.bar-fill{display:block;height:100%;background:var(--ink)}
.bar-val{font-family:var(--mono);font-size:.84rem}
@media (max-width:560px){.bar-row{grid-template-columns:1fr auto}.bar-track{grid-column:1/-1;grid-row:2}}
.cta{background:var(--night);color:#EDEBE6;padding:clamp(22px,3vw,34px);display:grid;grid-template-columns:minmax(0,1.4fr) auto;gap:22px;align-items:center}
.cta h3{font:italic 500 clamp(1.7rem,2.6vw,2.3rem)/1.05 var(--didone)}
.cta p{color:#BDB8AF;margin-top:10px;font-size:.96rem;max-width:58ch}
.cta-side{display:grid;gap:8px;justify-items:end}
.cta-folio{font:500 .74rem var(--mono);color:#98938A}
@media (max-width:760px){.cta{grid-template-columns:1fr}.cta-side{justify-items:start}}
.inm{border:1px solid var(--red);padding:14px 16px;display:flex;flex-wrap:wrap;gap:12px;align-items:center;justify-content:space-between;font-size:.94rem}
.inm a{font:500 .72rem var(--sans);letter-spacing:.18em;text-transform:uppercase;color:var(--red)}
.gen-ov{position:fixed;inset:0;z-index:50;background:rgba(15,15,16,.88);display:grid;place-items:center;padding:20px}
.gen-card{background:var(--paper);padding:28px;max-width:470px;width:100%;display:grid;gap:16px}
.gen-card ol{list-style:none;margin:0;padding:0;display:grid;gap:11px;font-size:.96rem}
.gen-card li{display:grid;grid-template-columns:22px 1fr;gap:10px;color:#A29E97}
.gen-card li::before{content:'';width:14px;height:14px;margin-top:5px;border:2px solid #CFCAC2;border-radius:50%}
.gen-card li.doing{color:var(--ink)}
.gen-card li.doing::before{border-color:var(--red);border-top-color:transparent;animation:spin .7s linear infinite}
.gen-card li.done{color:var(--ink)}
.gen-card li.done::before{background:var(--ink);border-color:var(--ink)}
@keyframes spin{to{transform:rotate(360deg)}}


form.cfg{position:static;border:0;padding:0;background:none;gap:16px}
.kpis{grid-template-columns:repeat(2,minmax(0,1fr))}
.kpi:nth-child(2){border-right:0}
.kpi:nth-child(-n+2){border-bottom:1px solid var(--rule)}
.kpi strong{font-size:1.6rem}
.viewer{height:max(260px,64cqw)}
.cta{grid-template-columns:1fr}
.cta-side{justify-items:start}
.cta h3{font-size:1.5rem}
.res{gap:14px}

/* fidelidad, método, preguntas */
.big-quote{font:italic 400 max(26px,8.6cqw)/1.02 var(--didone);letter-spacing:-.01em}
.big-quote::before{content:'«';color:var(--red)}.big-quote::after{content:'»';color:var(--red)}
.checks{list-style:none;padding:0;margin:0;border-top:1px solid var(--ink)}
.checks li{padding:1.4cqh 0;border-bottom:1px solid var(--rule);display:grid;grid-template-columns:8cqw 1fr;gap:2cqw}
.checks li span{font:italic 500 max(14px,3.4cqw) var(--didone);color:var(--red)}
.cmp{position:relative;flex:1;min-height:0;overflow:hidden;background:#C9C6BE}
.cmp-layer{position:absolute;inset:0;display:grid;place-items:center}
.cmp-layer svg{width:84%;height:84%}
.cmp-bottom{background:linear-gradient(180deg,#E3DED5,#C9C2B5)}
.cmp-bottom svg *{fill:#F3F0EA;stroke:#6F6A60;stroke-width:1}
.cmp-top{background:linear-gradient(180deg,#1C1C1E,#2B2B2E);clip-path:inset(0 50% 0 0)}
.cmp-top svg *{fill:none;stroke:#D7D0C4;stroke-width:1}
.cmp-tag{position:absolute;top:12px;font:500 .62rem var(--sans);letter-spacing:.2em;text-transform:uppercase;padding:5px 9px;background:var(--white);color:var(--ink)}
.cmp-line{position:absolute;top:0;bottom:0;left:50%;width:1px;background:#fff;pointer-events:none}
.cmp-range{position:absolute;inset:auto 12px 12px 12px;width:calc(100% - 24px);accent-color:var(--red)}
.cmp-note{font:italic 400 max(12px,2.6cqw) var(--didone);color:var(--muted)}
.sec-head{display:grid;gap:1cqh}
.sec-head h2{font-size:max(26px,9cqw);letter-spacing:-.025em}
.steps{display:grid;gap:0;border-top:1px solid var(--ink)}
.step{display:grid;grid-template-columns:12cqw 1fr;gap:3cqw;padding:1.8cqh 0;border-bottom:1px solid var(--rule)}
.step .n{font:italic 500 max(22px,7cqw)/.9 var(--didone);color:var(--red)}
.step h3{font-size:max(16px,4.2cqw)}
.step p{color:var(--muted);margin-top:.6cqh}
.faq{display:grid;border-top:1px solid var(--ink);overflow:auto}
.faq details{border-bottom:1px solid var(--rule);padding:1.5cqh 0}
.faq summary{font:500 max(14px,3.5cqw)/1.25 var(--didone);cursor:pointer;list-style:none;display:flex;justify-content:space-between;gap:12px}
.faq summary::after{content:'+';font:300 1.2rem var(--sans);color:var(--red)}
.faq details[open] summary::after{content:'−'}
.faq p{margin-top:1cqh;color:var(--muted)}
.contact-big{font:italic 500 max(34px,12cqw)/.9 var(--didone);letter-spacing:-.03em}
.contact-lines{display:grid;gap:1.4cqh}
.colofon dl{display:grid;margin:0;border-top:1px solid var(--ink)}
.colofon dl div{display:grid;grid-template-columns:38% 1fr;gap:2cqw;padding:1.2cqh 0;border-bottom:1px solid var(--rule)}
.colofon dt{font:500 max(9px,1.7cqw)/1.7 var(--sans);letter-spacing:.2em;text-transform:uppercase;color:var(--muted)}
.colofon dd{margin:0}
.pg-back{justify-content:space-between;padding:calc(var(--pw) * .08)}
.back-mark{font:600 9cqw/1 var(--didone);letter-spacing:-.03em}
.back-quote{font:italic 400 max(26px,8cqw)/1.05 var(--didone)}
.back-foot{display:grid;gap:2cqh;font:500 max(9px,1.8cqw)/1.6 var(--sans);letter-spacing:.2em;text-transform:uppercase;color:#A6A199}
#to-cover{justify-self:start}
</style>
</head>
<body>
<div class="stage">
  <div class="book is-closed-front" id="book" aria-label="Revista Liberache">
    <div class="slot" id="slotL"></div>
    <div class="slot" id="slotR"></div>
    <div class="leaf" id="leaf" hidden><div class="face face-front" id="leafFront"></div><div class="face face-back" id="leafBack"></div></div>
  </div>
  <nav class="controls" aria-label="Pasar página">
    <button type="button" class="ctl-arrow" id="ctl-prev" aria-label="Página anterior">‹</button>
    <button type="button" id="ctl-index">Índice</button>
    <span class="ctl-count" id="ctl-count" aria-live="polite"></span>
    <button type="button" class="ctl-arrow" id="ctl-next" aria-label="Página siguiente">›</button>
    <span class="ctl-hint" id="ctl-hint">Toca la portada para abrir la revista</span>
  </nav>
</div>

<div id="store">

  <section class="pg pg-cover" data-id="cover" aria-label="Portada">
    <div class="cover-img" id="cover-img"></div>
    <div class="cover-shade"></div>
    <div class="cover-in">
      <div class="cover-rail"><span>Nº 01 · Noviembre 2026</span><span>Tepic &amp; Xalisco</span></div>
      <h1 class="cover-mast">LIBERACHE</h1>
      <p class="cover-tag">Arquitectura · Interiorismo · Construcción</p>
      <div class="cover-lines">
        <div class="cl"><span class="kicker">Recorridos</span><p>Tres casas que se caminan antes de existir <b data-pageref="rec"></b></p></div>
        <div class="cl"><span class="kicker">El prototipo</span><p>Tu terreno, tu presupuesto, tu casa en 3D <b data-pageref="cfgL"></b></p></div>
        <div class="cl"><span class="kicker">Fidelidad</span><p>Del render a la obra, sin traducciones <b data-pageref="fidL"></b></p></div>
      </div>
      <div class="cover-big"><p>Recorre tu casa antes de construirla.</p></div>
      <div class="cover-foot"><span>Edición de cortesía</span><span class="open-hint">Abrir revista →</span></div>
    </div>
  </section>

  <section class="pg" data-id="indice" aria-label="Índice">
    <p class="kicker">En este número</p>
    <h2 class="idx-title">Índice</h2>
    <ol class="idx" id="idx"></ol>
    <div class="idx-ed">
      <p class="kicker">Editorial</p>
      <p>Una casa se decide con el corazón y se construye con números. Aquí la recorres primero, sabes cuánto cuesta y qué lleva, y después la construimos tal cual la aprobaste.</p>
    </div>
    <footer class="folio"><span>Liberache Nº 01</span><b></b></footer>
  </section>

  <section class="pg" data-id="rec" aria-label="Recorridos">
    <span class="open-num">01</span>
    <h2 class="open-title">Recorridos</h2>
    <p class="open-deck">Proyectos del estudio en recorrido virtual. Entra, mira alrededor y camina de un espacio a otro como si ya estuvieras ahí.</p>
    <ol class="rec-list" id="rec-list"></ol>
    <p class="how">Arrastra dentro de cada recorrido para mirar. Para pasar de página toca el borde derecho de la hoja.</p>
    <footer class="folio"><span>Recorridos</span><b></b></footer>
  </section>

  <section class="pg pg-cfg no-flip" data-id="cfgL" aria-label="Diseña la tuya">
    <div class="pg-cfg-head"><em>02</em><div><p class="kicker">El prototipo</p><h2>Diseña la tuya</h2></div></div>
    <div class="pg-scroll">
      <form id="cfg" class="cfg" novalidate>
        <div class="prog" aria-live="polite">
          <div class="prog-track"><span class="prog-bar" id="prog-bar"></span></div>
          <span class="prog-txt" id="prog-txt"></span>
        </div>
        <fieldset data-field="tipo">
          <legend>¿Qué quieres construir?</legend>
          <div class="seg">
            <label><input type="radio" name="tipo" id="tipo-casa" value="casa" checked><span>Casa</span></label>
            <label><input type="radio" name="tipo" id="tipo-negocio" value="negocio"><span>Negocio</span></label>
          </div>
        </fieldset>
        <fieldset data-field="terreno-medidas">
          <legend>Medidas del terreno</legend>
          <div class="dims">
            <input type="number" id="frente" name="frente" min="6" max="40" step="0.5" value="10" aria-label="Frente en metros" inputmode="decimal">
            <span class="x">×</span>
            <input type="number" id="fondo" name="fondo" min="10" max="60" step="0.5" value="20" aria-label="Fondo en metros" inputmode="decimal">
            <span class="x">m</span>
          </div>
          <p class="hint">Frente × fondo · <span class="area-out" id="area-terreno"></span></p>
        </fieldset>
        <fieldset data-field="terreno">
          <legend>¿Ya tienes el terreno?</legend>
          <div class="seg">
            <label><input type="radio" name="terreno" id="terreno-si" value="si" checked><span>Sí, ya lo tengo</span></label>
            <label><input type="radio" name="terreno" id="terreno-no" value="no"><span>Todavía no</span></label>
          </div>
        </fieldset>
        <fieldset data-field="niveles">
          <legend>Niveles</legend>
          <div class="seg">
            <label><input type="radio" name="niveles" id="niv-1" value="1"><span>1</span></label>
            <label><input type="radio" name="niveles" id="niv-2" value="2" checked><span>2</span></label>
            <label><input type="radio" name="niveles" id="niv-3" value="3"><span>3</span></label>
          </div>
        </fieldset>
        <fieldset data-field="programa" id="fs-recamaras">
          <legend>Recámaras</legend>
          <div class="seg">
            <label><input type="radio" name="recamaras" id="rec-1" value="1"><span>1</span></label>
            <label><input type="radio" name="recamaras" id="rec-2" value="2"><span>2</span></label>
            <label><input type="radio" name="recamaras" id="rec-3" value="3" checked><span>3</span></label>
            <label><input type="radio" name="recamaras" id="rec-4" value="4"><span>4</span></label>
          </div>
        </fieldset>
        <fieldset data-field="programa" id="fs-giro" hidden>
          <legend>Giro del negocio</legend>
          <div class="seg">
            <label><input type="radio" name="giro" id="giro-local" value="local" checked><span>Local comercial</span></label>
            <label><input type="radio" name="giro" id="giro-cons" value="consultorio"><span>Consultorios</span></label>
            <label><input type="radio" name="giro" id="giro-rest" value="restaurante"><span>Restaurante o café</span></label>
          </div>
        </fieldset>
        <fieldset data-field="acabado">
          <legend>Nivel de acabados</legend>
          <div class="seg acab">
            <label><input type="radio" name="acabado" id="acab-esencial" value="esencial"><span><b>Esencial</b><small>Piso cerámico, cancelería de aluminio, muebles de línea</small><span class="acab-precio" data-k="esencial"></span></span></label>
            <label><input type="radio" name="acabado" id="acab-confort" value="confort" checked><span><b>Confort</b><small>Porcelanato, cocina integral, volados en fachada</small><span class="acab-precio" data-k="confort"></span></span></label>
            <label><input type="radio" name="acabado" id="acab-premium" value="premium"><span><b>Premium</b><small>Gran formato, celosía de madera, vestidor</small><span class="acab-precio" data-k="premium"></span></span></label>
          </div>
        </fieldset>
        <fieldset data-field="presupuesto">
          <legend>Presupuesto total para construir</legend>
          <span class="budget-out num" id="presupuesto-out"></span>
          <input type="range" id="presupuesto" name="presupuesto" min="800000" max="20000000" step="50000" value="3200000" aria-describedby="presupuesto-hint">
          <p class="hint" id="presupuesto-hint"></p>
        </fieldset>
        <fieldset data-field="inicio">
          <legend>¿Cuándo quieres empezar?</legend>
          <div class="seg">
            <label><input type="radio" name="inicio" id="ini-1" value="0-3"><span>Antes de 3 meses</span></label>
            <label><input type="radio" name="inicio" id="ini-2" value="3-6" checked><span>3 a 6 meses</span></label>
            <label><input type="radio" name="inicio" id="ini-3" value="6-12"><span>6 a 12 meses</span></label>
            <label><input type="radio" name="inicio" id="ini-4" value="explorando"><span>Estoy explorando</span></label>
          </div>
        </fieldset>
        <button type="submit" class="btn btn-red gen" id="gen-btn">Generar mi prototipo</button>
      </form>
    </div>
    <footer class="folio"><span>Diseña la tuya</span><b></b></footer>
  </section>

  <section class="pg pg-cfg no-flip" data-id="cfgR" aria-label="Tu prototipo">
    <div class="pg-scroll">
      <div class="res" id="resultado">
        <div class="res-head">
          <span class="pill" id="res-state">Prototipo de ejemplo</span>
          <span class="hint">Sin terreno, licencias ni honorarios.</span>
        </div>
        <div class="kpis">
          <div class="kpi"><small>Construcción</small><strong class="num"><span id="k-area"></span> m²</strong></div>
          <div class="kpi"><small>Costo estimado</small><strong class="num" id="k-costo"></strong></div>
          <div class="kpi"><small>Huella</small><strong class="num" id="k-huella" style="font-size:1.25rem"></strong><span class="hint" id="k-niveles"></span></div>
          <div class="kpi" style="padding:0"><div class="status" id="k-status"></div></div>
        </div>
        <div class="advice" id="advice" hidden></div>
        <div class="tabs" role="tablist" aria-label="Resultados">
          <button class="tab" role="tab" id="t-3d" data-t="3d" aria-controls="p-3d" aria-selected="true">3D</button>
          <button class="tab" role="tab" id="t-plan" data-t="plan" aria-controls="p-plan" aria-selected="false">Planos</button>
          <button class="tab" role="tab" id="t-mat" data-t="mat" aria-controls="p-mat" aria-selected="false">Materiales</button>
          <button class="tab" role="tab" id="t-cost" data-t="cost" aria-controls="p-cost" aria-selected="false">Presupuesto</button>
        </div>
        <div class="tabpanel" id="p-3d" role="tabpanel" aria-labelledby="t-3d">
          <div class="viewer" id="viewer" tabindex="0" aria-label="Visor 3D del prototipo">
            <canvas id="viewer-canvas"></canvas>
            <div class="v-bar">
              <button type="button" class="vmode" data-m="exterior" aria-pressed="true">Exterior</button>
              <button type="button" class="vmode" data-m="maqueta" aria-pressed="false">Maqueta</button>
              <button type="button" class="vmode" data-m="walk" aria-pressed="false">Recorrer</button>
              <div class="lvl-chips" id="lvl-chips" hidden></div>
              <button type="button" class="v-full" id="v-full">⤢</button>
            </div>
            <span class="v-help" id="v-help">Arrastra para girar</span>
            <div id="walk-ui" hidden>
              <span class="walk-room" id="walk-room"></span>
              <div class="pad" aria-label="Controles de recorrido">
                <button type="button" class="u" data-key="f" aria-label="Avanzar">▲</button>
                <button type="button" class="tl" data-key="tl" aria-label="Girar a la izquierda">↶</button>
                <button type="button" class="d" data-key="b" aria-label="Retroceder">▼</button>
                <button type="button" class="tr" data-key="tr" aria-label="Girar a la derecha">↷</button>
              </div>
            </div>
            <p class="viewer-msg" id="viewer-msg" hidden></p>
          </div>
        </div>
        <div class="tabpanel" id="p-plan" role="tabpanel" aria-labelledby="t-plan" hidden>
          <div class="plan-wrap" id="plan-wrap"></div>
          <p class="note">Planta esquemática generada automáticamente; el diseño final se resuelve con el arquitecto.</p>
        </div>
        <div class="tabpanel" id="p-mat" role="tabpanel" aria-labelledby="t-mat" hidden>
          <div class="tbl-wrap"><table><thead><tr><th>Material</th><th style="text-align:right">Cantidad</th><th>Unidad</th></tr></thead><tbody id="mat-body"></tbody></table></div>
          <p class="note" id="mat-note"></p>
        </div>
        <div class="tabpanel" id="p-cost" role="tabpanel" aria-labelledby="t-cost" hidden>
          <div class="cost-card">
            <div class="cost-top">
              <div><p class="hint">Costo estimado</p><strong class="num" id="cost-total"></strong><p class="hint num" id="cost-m2"></p></div>
              <div style="text-align:right"><p class="hint">Tu presupuesto</p><p class="num" style="font:500 1.2rem var(--didone)" id="cost-budget"></p></div>
            </div>
            <div>
              <div class="meter" role="img" aria-label="Costo contra presupuesto"><span class="meter-fill" id="meter-fill"></span><span class="meter-over" id="meter-over"></span></div>
              <div class="meter-legend"><span>$0</span><span>100 % de tu presupuesto</span></div>
            </div>
            <div style="display:grid;gap:10px" id="cost-body"></div>
          </div>
        </div>
        <div class="cta">
          <div>
            <h3>¿Te gustó? Ahora hagámosla tuya.</h3>
            <p>El arquitecto Rigo y su equipo diseñan tu proyecto a la medida, con recorrido realista y visor de realidad virtual. Respetamos el presupuesto que tú defines.</p>
          </div>
          <div class="cta-side">
            <a class="btn btn-red" id="cta-wa" href="#" target="_blank" rel="noopener">Quiero mi diseño por WhatsApp</a>
            <span class="cta-folio" id="cta-folio"></span>
            <span class="cta-folio">WhatsApp <span id="wa-num"></span></span>
          </div>
        </div>
        <div class="inm" id="cta-inm" hidden>
          <span>¿Aún no tienes terreno? Alta Inmobiliaria te ayuda a encontrarlo.</span>
          <a id="cta-inm-a" href="#" target="_blank" rel="noopener">Buscar terreno →</a>
        </div>
      </div>
    </div>
    <footer class="folio"><span>Tu prototipo</span><b></b></footer>
  </section>

  <section class="pg" data-id="fidL" aria-label="Fidelidad de obra">
    <p class="kicker">03 · Fidelidad de obra</p>
    <p class="big-quote">Lo que ves es lo que se construye.</p>
    <ul class="checks">
      <li><span>i.</span>El recorrido sale del mismo modelo que los planos, las cantidades y el presupuesto.</li>
      <li><span>ii.</span>Apruebas cada espacio, material y color en pantalla antes de iniciar obra.</li>
      <li><span>iii.</span>En cada etapa de obra te mostramos el comparativo render contra foto.</li>
    </ul>
    <footer class="folio"><span>Fidelidad</span><b></b></footer>
  </section>

  <section class="pg" data-id="fidR" aria-label="Render contra obra">
    <div class="sec-head"><p class="kicker">Antes y después</p><h2>Del render a la obra.</h2></div>
    <div class="cmp no-flip-zone" aria-label="Comparativo render contra obra">
      <div class="cmp-layer cmp-bottom" aria-hidden="true"><svg viewBox="0 0 200 120"><path d="M20 110 V45 H110 V25 H180 V110 Z"/><path d="M30 60 h60 v35 h-60z M120 35 h50 v28 h-50z M125 72 h20 v38 h-20z"/></svg></div>
      <div class="cmp-layer cmp-top" id="cmp-top" aria-hidden="true"><svg viewBox="0 0 200 120"><path d="M20 110 V45 H110 V25 H180 V110 Z"/><path d="M30 60 h60 v35 h-60z M120 35 h50 v28 h-50z M125 72 h20 v38 h-20z M0 110 H200"/></svg></div>
      <span class="cmp-line" id="cmp-line"></span>
      <span class="cmp-tag" style="left:12px">Render</span>
      <span class="cmp-tag" style="right:12px">Obra</span>
      <input type="range" class="cmp-range" id="cmp-range" min="0" max="100" value="50" aria-label="Deslizar entre render y obra">
    </div>
    <p class="cmp-note">Ejemplo ilustrativo; aquí van pares reales de render y foto de obra.</p>
    <footer class="folio"><span>Fidelidad</span><b></b></footer>
  </section>

  <section class="pg" data-id="metodo" aria-label="Cómo trabajamos">
    <div class="sec-head"><p class="kicker">04 · Cómo trabajamos</p><h2>De tu idea a la llave.</h2></div>
    <div class="steps">
      <div class="step"><span class="n">i.</span><div><h3>Escuchamos tu sueño</h3><p>Terreno, necesidades, estilo y presupuesto tope.</p></div></div>
      <div class="step"><span class="n">ii.</span><div><h3>Lo recorres en 3D y VR</h3><p>Ajustamos el diseño contigo hasta que te veas viviendo ahí.</p></div></div>
      <div class="step"><span class="n">iii.</span><div><h3>Números antes de obra</h3><p>Presupuesto por partidas y explosión de insumos.</p></div></div>
      <div class="step"><span class="n">iv.</span><div><h3>Queda igual</h3><p>Obra con seguimiento y comparativo render contra foto.</p></div></div>
    </div>
    <footer class="folio"><span>Método</span><b></b></footer>
  </section>

  <section class="pg" data-id="faq" aria-label="Preguntas frecuentes">
    <div class="sec-head"><p class="kicker">05 · Preguntas</p><h2>Antes de empezar.</h2></div>
    <div class="faq">
      <details><summary>¿El prototipo ya es mi proyecto?</summary><p>No. Es un modelo automático para ver qué cabe en tu terreno con tu presupuesto. Tu proyecto lo diseña el arquitecto contigo.</p></details>
      <details><summary>¿Qué tan preciso es el costo?</summary><p>Es una estimación paramétrica de ±15 %. En el proyecto ejecutivo te entregamos el presupuesto por partidas.</p></details>
      <details><summary>¿Necesito visor de realidad virtual?</summary><p>No. Los recorridos se ven en celular o computadora; en la sesión de diseño te prestamos el visor.</p></details>
      <details><summary>¿Y si no tengo terreno?</summary><p>Te ayudamos a buscarlo con Alta Inmobiliaria, cuidando que le quede al proyecto.</p></details>
      <details><summary>¿También diseñan negocios?</summary><p>Sí: locales, consultorios, oficinas y restaurantes, con el mismo método.</p></details>
    </div>
    <footer class="folio"><span>Preguntas</span><b></b></footer>
  </section>

  <section class="pg pg-dark" data-id="contacto" aria-label="Contacto">
    <p class="kicker">06 · Contacto</p>
    <h2 class="contact-big">Hagamos tu casa.</h2>
    <div class="contact-lines">
      <p style="color:#BDB8AF">Cuéntanos de tu terreno y de tu presupuesto. Te respondemos por WhatsApp y agendamos tu sesión de diseño con recorrido virtual.</p>
      <a class="btn btn-red" id="contact-wa" href="#" target="_blank" rel="noopener" style="justify-self:start">Escribir por WhatsApp</a>
      <p class="cta-folio">WhatsApp <span id="contact-num"></span></p>
      <p style="color:#BDB8AF">¿Sin terreno? Alta Inmobiliaria te ayuda a encontrarlo.</p>
    </div>
    <footer class="folio"><span>Contacto</span><b></b></footer>
  </section>

  <section class="pg colofon" data-id="colofon" aria-label="Colofón">
    <p class="kicker">Colofón</p>
    <h2 style="font:italic 500 max(26px,9cqw)/.95 var(--didone)">Liberache Nº 01</h2>
    <dl>
      <div><dt>Edición</dt><dd>Noviembre 2026 · Tepic y Xalisco, Nayarit</dd></div>
      <div><dt>Dirección de proyecto</dt><dd>Arq. Rigo</dd></div>
      <div><dt>Estudio</dt><dd>Estudio Liberache · diseño y construcción</dd></div>
      <div><dt>Recorridos</dt><dd>D5 Render</dd></div>
      <div><dt>Bienes raíces</dt><dd>Alta Inmobiliaria</dd></div>
    </dl>
    <p class="how">Los costos del prototipo son estimaciones paramétricas y no incluyen terreno, licencias ni honorarios de proyecto.</p>
    <footer class="folio"><span>Colofón</span><b></b></footer>
  </section>

  <section class="pg pg-dark pg-back" data-id="back" aria-label="Contraportada">
    <span class="back-mark">LIBERACHE</span>
    <p class="back-quote">Casas que se recorren antes de existir.</p>
    <div class="back-foot">
      <span>Arquitectura · Interiorismo · Construcción</span>
      <span>Tepic &amp; Xalisco, Nayarit</span>
      <button type="button" class="btn btn-paper" id="to-cover">Volver a la portada ↺</button>
    </div>
  </section>
</div>

<div class="gen-ov" id="gen-overlay" hidden role="status" aria-live="polite">
  <div class="gen-card">
    <p class="kicker" style="font-size:.72rem">Generando tu prototipo</p>
    <ol id="gen-steps"></ol>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/build/three.min.js"></script>
<script>
/* ============================================================
   CONFIGURACIÓN — ajusta estos valores con datos reales del estudio
   ============================================================ */
var CONFIG = {
  estudio: 'Estudio Liberache',
  // Número de WhatsApp con lada internacional, sin espacios ni "+": 52 + 10 dígitos
  whatsapp: '520000000000',
  whatsappInmobiliaria: '520000000000',
  // Costo directo por m² (MXN). Valores de arranque: calíbralos con tus obras reales en Tepic/Xalisco.
  costoM2: { esencial: 13500, confort: 18500, premium: 26000 },
  factorNegocio: 1.0,
  retiroFrente: { casa: 3, negocio: 1.5 },
  retiroFondo: { casa: 2, negocio: 1.5 },
  reservaImprevistos: 0.05, // se deja fuera del cálculo de m² para imprevistos
  cos: 0.8,               // coeficiente de ocupación del suelo usado como tope
  alturaNivel: 3.0,       // entrepiso (m)
  partidas: [
    ['Preliminares y cimentación', 0.11],
    ['Estructura y muros (obra negra)', 0.31],
    ['Instalaciones hidráulica, sanitaria y eléctrica', 0.14],
    ['Acabados: pisos, aplanados y pintura', 0.24],
    ['Cancelería, carpintería y herrería', 0.12],
    ['Muebles de baño y cocina', 0.05],
    ['Indirectos y limpieza de obra', 0.03]
  ],
  // Recorridos D5 (cada uno es una "página" de la revista). Pega la liga de D5 Showreel en d5.
  // Los campos vacíos no se muestran.
  proyectos: [
    { nombre: 'Proyecto 01', tipo: 'Casa habitación', lugar: 'Tepic, Nayarit', superficie: '', niveles: '', anio: '',
      titular: 'Camínala antes de que exista.',
      entrada: 'Cada muro, cada material y cada entrada de luz, tal como se va a construir. Arrastra dentro del recorrido para mirar alrededor y salta de un espacio a otro.',
      d5: 'https://showreel.d5render.com/personal-krpano?directory=https://usa.asset.d5cdn.com/tourProject/pano_roam_1793743836892_4354783/&tourId=2117741596601872386' },
    { nombre: 'Proyecto 02', tipo: 'Casa habitación', lugar: 'Xalisco, Nayarit', superficie: '', niveles: '', anio: '',
      titular: 'La luz decide el diseño.',
      entrada: 'Recorre cómo entra el sol a cada hora antes de elegir dónde va cada ventana.',
      d5: '' },
    { nombre: 'Proyecto 03', tipo: 'Negocio', lugar: 'Tepic, Nayarit', superficie: '', niveles: '', anio: '',
      titular: 'Un local que vende desde la banqueta.',
      entrada: 'Fachada, aparador y recorrido del cliente, probados en realidad virtual antes de abrir.',
      d5: '' }
  ]
};

var ACABADOS = {
  esencial: { nombre: 'Esencial', desc: 'Piso cerámico, cancelería de aluminio, muebles de línea' },
  confort:  { nombre: 'Confort',  desc: 'Porcelanato, cocina integral, volados de fachada' },
  premium:  { nombre: 'Premium',  desc: 'Gran formato, madera, celosías, vestidor' }
};

/* ============================================================
   MOTOR: programa arquitectónico → distribución → muros → cantidades
   ============================================================ */
var EPS = 1e-6;
function clamp(v, a, b) { return Math.max(a, Math.min(b, v)); }
function sumArea(list) { return list.reduce(function (s, r) { return s + r.area; }, 0); }
function room(key, name, area, group, furn, floor, extra) {
  var r = { key: key, name: name, area: area, group: group, furn: furn, floor: floor };
  if (extra) for (var k in extra) r[k] = extra[k];
  return r;
}

function program(inp) {
  var N = inp.niveles, R = inp.recamaras, lv = [], k;
  if (inp.tipo === 'casa') {
    var sala = room('sala', 'Sala', 20, 'social', 'sala', 'porc');
    var comedor = room('comedor', 'Comedor', 13, 'social', 'comedor', 'porc');
    var cocina = room('cocina', 'Cocina', 11, 'social', 'cocina', 'tile');
    var lav = room('lav', 'Lavandería', 5, 'serv', 'lav', 'tile');
    var mb = room('mbano', 'Medio baño', 3, 'bath', 'mbano', 'tile');
    var rp = room('rp', 'Recámara principal', 16, 'priv', 'cama', 'wood');
    var bp = room('bp', 'Baño principal', 6, 'bath', 'bano', 'tile', { pref: 'rp' });
    var sec = [];
    for (var i = 2; i <= R; i++) sec.push(room('r' + i, 'Recámara ' + i, 11, 'priv', 'cama2', 'wood'));
    var bc = R >= 2 ? room('bc', 'Baño completo', 5, 'bath', 'bano', 'tile') : null;
    if (N === 1) {
      lv.push({ front: [sala, comedor, cocina], back: [rp, bp].concat(sec, [bc, lav]).filter(Boolean) });
    } else {
      var g = { front: [sala], back: [comedor, cocina, mb, lav] };
      if (R === 4) { var v = sec.pop(); v.name = 'Recámara de visitas'; g.front.push(v); }
      lv.push(g);
      var up = { front: sec.concat([bc]).filter(Boolean), back: [rp, bp] };
      if (inp.acabado === 'premium') up.back.push(room('vest', 'Vestidor', 4, 'serv', 'vest', 'wood', { pref: 'rp' }));
      if (R >= 3 || up.front.length === 0) up.front.push(room('estar', 'Estar familiar', 12, 'social', 'estar', 'wood'));
      lv.push(up);
      if (N === 3) {
        lv.push({
          front: [room('terraza', 'Terraza', 24, 'open', 'terraza', 'deck')],
          back: [room('estudio', 'Estudio', 10, 'priv', 'escritorio', 'wood'),
                 room('mb2', 'Medio baño', 3, 'bath', 'mbano', 'tile'),
                 room('bod', 'Bodega', 5, 'serv', 'bodega', 'conc')]
        });
      }
    }
  } else {
    var gi = inp.giro;
    if (gi === 'local') {
      lv.push({ front: [room('ventas', 'Área de ventas', 45, 'social', 'ventas', 'porc')],
                back: [room('bod', 'Bodega', 12, 'serv', 'bodega', 'conc'),
                       room('ofi', 'Oficina', 9, 'priv', 'escritorio', 'porc'),
                       room('bn', 'Baño', 5, 'bath', 'mbano', 'tile')] });
      for (k = 1; k < N; k++) lv.push({
        front: [room('ofr' + k, 'Oficina en renta', 36, 'social', 'oficinas', 'porc')],
        back: [room('bn' + k, 'Baño', 5, 'bath', 'mbano', 'tile'), room('arc' + k, 'Archivo', 6, 'serv', 'bodega', 'conc')] });
    } else if (gi === 'consultorio') {
      lv.push({ front: [room('rec', 'Recepción y espera', 20, 'social', 'recepcion', 'porc')],
                back: [room('c1', 'Consultorio 1', 14, 'priv', 'consult', 'porc'),
                       room('c2', 'Consultorio 2', 14, 'priv', 'consult', 'porc'),
                       room('bn', 'Baño', 5, 'bath', 'mbano', 'tile')] });
      for (k = 1; k < N; k++) lv.push({
        front: [room('ca' + k, 'Consultorio ' + (k * 3 + 0), 14, 'priv', 'consult', 'porc'),
                room('cb' + k, 'Consultorio ' + (k * 3 + 1), 14, 'priv', 'consult', 'porc')],
        back: [room('cc' + k, 'Consultorio ' + (k * 3 + 2), 14, 'priv', 'consult', 'porc'),
               room('bn' + k, 'Baño', 5, 'bath', 'mbano', 'tile')] });
    } else {
      lv.push({ front: [room('salon', 'Salón comedor', 50, 'social', 'mesas', 'porc')],
                back: [room('coc', 'Cocina', 18, 'serv', 'cocinapro', 'tile'),
                       room('bh', 'Baño hombres', 5, 'bath', 'mbano', 'tile'),
                       room('bm', 'Baño mujeres', 5, 'bath', 'mbano', 'tile'),
                       room('bod', 'Bodega', 6, 'serv', 'bodega', 'conc')] });
      for (k = 1; k < N; k++) {
        if (k === N - 1) lv.push({
          front: [room('ter' + k, 'Terraza comedor', 40, 'open', 'mesas', 'deck')],
          back: [room('bn' + k, 'Baño', 5, 'bath', 'mbano', 'tile'), room('srv' + k, 'Barra de servicio', 8, 'serv', 'bodega', 'tile')] });
        else lv.push({
          front: [room('sal' + k, 'Salón privado', 40, 'social', 'mesas', 'porc')],
          back: [room('bn' + k, 'Baño', 5, 'bath', 'mbano', 'tile'), room('bd' + k, 'Bodega', 6, 'serv', 'bodega', 'conc')] });
      }
    }
  }
  return lv;
}

/* Bisección ordenada: reparte las piezas en un rectángulo respetando el orden */
function bisect(list, r, out) {
  if (!list.length) return;
  if (list.length === 1) { out.push(Object.assign({}, list[0], { x0: r.x0, y0: r.y0, x1: r.x1, y1: r.y1 })); return; }
  var total = sumArea(list), acc = 0, best = 1, bestD = Infinity;
  for (var i = 1; i < list.length; i++) {
    acc += list[i - 1].area;
    var d = Math.abs(acc - total / 2);
    if (d < bestD) { bestD = d; best = i; }
  }
  var a = list.slice(0, best), b = list.slice(best), fa = sumArea(a) / total;
  var w = r.x1 - r.x0, h = r.y1 - r.y0;
  if (w >= h) {
    var xm = r.x0 + w * fa;
    bisect(a, { x0: r.x0, y0: r.y0, x1: xm, y1: r.y1 }, out);
    bisect(b, { x0: xm, y0: r.y0, x1: r.x1, y1: r.y1 }, out);
  } else {
    var ym = r.y0 + h * fa;
    bisect(a, { x0: r.x0, y0: r.y0, x1: r.x1, y1: ym }, out);
    bisect(b, { x0: r.x0, y0: ym, x1: r.x1, y1: r.y1 }, out);
  }
}

function buildProject(inp) {
  var prog = program(inp);
  var N = prog.length;
  var coreD = N > 1 ? 2.8 : 1.4;
  var sf = CONFIG.retiroFrente[inp.tipo], sb = CONFIG.retiroFondo[inp.tipo];
  var availD = Math.max(4, inp.fondo - sf - sb);
  var M = Math.max.apply(null, prog.map(function (l) { return sumArea(l.front) + sumArea(l.back); }));
  var costM2 = CONFIG.costoM2[inp.acabado] * (inp.tipo === 'negocio' ? CONFIG.factorNegocio : 1);
  var budgetArea = inp.presupuesto * (1 - CONFIG.reservaImprevistos) / costM2;

  function fit(W) {
    var C = W * coreD;
    var sBudget = (budgetArea / N - C) / M;
    var s = clamp(sBudget, 0.9, 1.45);
    var fp = s * M + C;
    var maxFp = Math.min(W * availD, CONFIG.cos * inp.frente * inp.fondo);
    var landLimited = false;
    if (fp > maxFp) { fp = maxFp; s = (fp - C) / M; landLimited = true; }
    return { C: C, s: s, fp: fp, sBudget: sBudget, landLimited: landLimited };
  }
  var W = inp.frente, f = fit(W);
  var tgtD = N > 1 ? 9.5 : 8;
  for (var it = 0; it < 5; it++) { if (f.fp / W < tgtD - 0.05 && W > 7) { W = clamp(f.fp / tgtD, 7, inp.frente); f = fit(W); } }
  W = Math.round(W * 100) / 100;
  var L = f.fp / W;

  var ratios = prog.map(function (l) { var a = sumArea(l.front), b = sumArea(l.back); return a / (a + b); });
  var r = ratios.reduce(function (s, x) { return s + x; }, 0) / ratios.length;
  var Lf = (L - coreD) * r;
  var front = { x0: 0, y0: 0, x1: W, y1: Lf };
  var back = { x0: 0, y0: Lf + coreD, x1: W, y1: L };
  var stairW = W < 6.5 ? 2.4 : 2.6;
  var stair = N > 1 ? { x0: W - stairW, y0: Lf, x1: W, y1: Lf + coreD } : null;

  var levels = prog.map(function (l, k) {
    var rooms = [];
    bisect(l.front, front, rooms);
    bisect(l.back, back, rooms);
    var hallName = k === 0 ? (inp.tipo === 'casa' ? 'Vestíbulo' : 'Pasillo') : 'Distribuidor';
    rooms.push(room('hall' + k, hallName, 0, 'circ', null, 'porc', { x0: 0, y0: Lf, x1: stair ? stair.x0 : W, y1: Lf + coreD, isHall: true }));
    if (stair) rooms.push(room('esc' + k, 'Escalera', 0, 'circ', null, 'porc', { x0: stair.x0, y0: stair.y0, x1: stair.x1, y1: stair.y1, isStair: true }));
    rooms.forEach(function (rm) { rm.w = rm.x1 - rm.x0; rm.h = rm.y1 - rm.y0; rm.area = rm.w * rm.h; });
    var walls = buildWalls(rooms, W, L, k, inp);
    return { k: k, rooms: rooms, segs: walls.segs, entrance: walls.entrance, unreached: walls.unreached };
  });

  var P = { inp: inp, N: N, W: W, L: L, Lf: Lf, coreD: coreD, stair: stair, sf: sf, sb: sb,
            levels: levels, costM2: costM2, budgetArea: budgetArea, s: f.s, landLimited: f.landLimited,
            H: CONFIG.alturaNivel };
  P.quant = quantities(P);
  P.cost = costing(P);
  return P;
}

/* ---------- muros, puertas y ventanas ---------- */
function buildWalls(rooms, W, L, k, inp) {
  var segs = [];
  rooms.forEach(function (a, i) {
    var edges = [
      { axis: 'h', c: a.y0, s0: a.x0, s1: a.x1, side: 'b' },
      { axis: 'h', c: a.y1, s0: a.x0, s1: a.x1, side: 't' },
      { axis: 'v', c: a.x0, s0: a.y0, s1: a.y1, side: 'l' },
      { axis: 'v', c: a.x1, s0: a.y0, s1: a.y1, side: 'r' }
    ];
    edges.forEach(function (e) {
      var parts = [];
      rooms.forEach(function (b, j) {
        if (j === i) return;
        var touch = false, o0, o1;
        if (e.side === 'b') { touch = Math.abs(b.y1 - e.c) < EPS; o0 = Math.max(e.s0, b.x0); o1 = Math.min(e.s1, b.x1); }
        if (e.side === 't') { touch = Math.abs(b.y0 - e.c) < EPS; o0 = Math.max(e.s0, b.x0); o1 = Math.min(e.s1, b.x1); }
        if (e.side === 'l') { touch = Math.abs(b.x1 - e.c) < EPS; o0 = Math.max(e.s0, b.y0); o1 = Math.min(e.s1, b.y1); }
        if (e.side === 'r') { touch = Math.abs(b.x0 - e.c) < EPS; o0 = Math.max(e.s0, b.y0); o1 = Math.min(e.s1, b.y1); }
        if (touch && o1 - o0 > 0.05) parts.push({ s0: o0, s1: o1, j: j });
      });
      parts.sort(function (p, q) { return p.s0 - q.s0; });
      var cur = e.s0;
      var pushExt = function (s0, s1) {
        if (s1 - s0 < 0.05) return;
        var side = null;
        if (e.side === 'b' && Math.abs(e.c) < EPS) side = 'front';
        else if (e.side === 't' && Math.abs(e.c - L) < EPS) side = 'back';
        else if (e.side === 'l' && Math.abs(e.c) < EPS) side = 'left';
        else if (e.side === 'r' && Math.abs(e.c - W) < EPS) side = 'right';
        segs.push({ axis: e.axis, c: e.c, s0: s0, s1: s1, a: i, b: -1, ext: true, side: side, openings: [] });
      };
      parts.forEach(function (p) {
        if (p.s0 > cur + 0.05) pushExt(cur, p.s0);
        if (i < p.j) segs.push({ axis: e.axis, c: e.c, s0: p.s0, s1: p.s1, a: i, b: p.j, ext: false, openings: [] });
        cur = Math.max(cur, p.s1);
      });
      if (cur < e.s1 - 0.05) pushExt(cur, e.s1);
    });
  });

  var isOpenGroup = function (g) { return g === 'social' || g === 'circ'; };
  segs.forEach(function (s) {
    s.len = s.s1 - s.s0;
    var A = rooms[s.a];
    if (s.ext) { s.low = A.group === 'open'; return; }
    var B = rooms[s.b];
    if ((A.group === 'social' && B.group === 'social') || (A.group === 'circ' && B.group === 'circ')) { s.omit = true; return; }
    if (isOpenGroup(A.group) && isOpenGroup(B.group)) {
      var wlen = Math.min(s.len - 0.5, 2.4);
      if (wlen >= 0.9) s.openings.push({ t0: (s.len - wlen) / 2, t1: (s.len + wlen) / 2, bottom: 0, top: 2.3, kind: 'wide' });
      else s.omit = true;
    }
  });

  // Conectividad: cada pieza recibe una puerta hacia una zona ya alcanzable
  var hallIdx = rooms.findIndex(function (r) { return r.isHall; });
  var reached = {}; reached[hallIdx] = true;
  var linkOpen = function () {
    var changed = true;
    while (changed) {
      changed = false;
      segs.forEach(function (s) {
        if (s.ext) return;
        var open = s.omit || s.openings.length > 0;
        if (!open) return;
        if (reached[s.a] && !reached[s.b]) { reached[s.b] = true; changed = true; }
        if (reached[s.b] && !reached[s.a]) { reached[s.a] = true; changed = true; }
      });
    }
  };
  linkOpen();
  var score = function (rFrom, rTo) {
    if (rTo.pref && rFrom.key === rTo.pref) return 10;
    if (rFrom.group === 'circ') return 3;
    if (rFrom.group === 'social') return 2;
    if (rTo.group === 'bath' && rFrom.group === 'priv') return 0.5;
    return 1;
  };
  var phase = function (filter) {
    var guard = 0;
    while (guard++ < 50) {
      var best = null;
      segs.forEach(function (s) {
        if (s.ext || s.omit || s.openings.length || s.len < 1.0) return;
        var from, to;
        if (reached[s.a] && !reached[s.b]) { from = s.a; to = s.b; }
        else if (reached[s.b] && !reached[s.a]) { from = s.b; to = s.a; }
        else return;
        if (!filter(rooms[to])) return;
        var sc = score(rooms[from], rooms[to]) + s.len * 0.01;
        if (!best || sc > best.sc) best = { s: s, sc: sc, to: to };
      });
      if (!best) break;
      var dw = 0.9, s = best.s;
      s.openings.push({ t0: (s.len - dw) / 2, t1: (s.len + dw) / 2, bottom: 0, top: 2.1, kind: 'door' });
      reached[best.to] = true;
      linkOpen();
    }
  };
  phase(function (r) { return r.group !== 'bath' && !r.pref; });
  phase(function () { return true; });

  // Acceso principal
  var entrance = null;
  if (k === 0) {
    var cands = segs.filter(function (s) { return s.ext && s.side === 'front'; });
    cands.sort(function (p, q) {
      var gp = rooms[p.a].group === 'social' ? 1 : 0, gq = rooms[q.a].group === 'social' ? 1 : 0;
      return (gq - gp) || (q.len - p.len);
    });
    var es = cands[0];
    if (es) {
      var store = inp.tipo === 'negocio' && (rooms[es.a].key === 'ventas' || rooms[es.a].key === 'salon' || rooms[es.a].key === 'rec');
      var dw2 = store ? 1.2 : 1.0;
      var t0 = es.len < 2.2 ? (es.len - dw2) / 2 : 0.45;
      es.openings.push({ t0: t0, t1: t0 + dw2, bottom: 0, top: 2.3, kind: 'entry' });
      es.entry = true;
      entrance = { x: es.s0 + t0 + dw2 / 2, y: 0 };
      if (store && es.len - (t0 + dw2) > 1.2) es.openings.push({ t0: t0 + dw2 + 0.15, t1: es.len - 0.3, bottom: 0.15, top: 2.5, kind: 'glass' });
      if (!store && es.len - (t0 + dw2) > 1.8) es.openings.push({ t0: t0 + dw2 + 0.5, t1: Math.min(es.len - 0.4, t0 + dw2 + 0.5 + 2.8), bottom: 0.5, top: 2.3, kind: 'window' });
      if (!reached[es.a]) reached[es.a] = true;
    }
  }

  // Ventanas en fachadas frontal y posterior (las laterales son colindancia)
  segs.forEach(function (s) {
    if (!s.ext || s.entry || s.low) return;
    if (s.side !== 'front' && s.side !== 'back') return;
    var A = rooms[s.a];
    if (A.group === 'circ' || s.len < 1.2) return;
    var w, bottom, top = 2.3, kind = 'window';
    if (A.group === 'bath') { w = 0.8; bottom = 1.6; top = 2.2; }
    else if (A.group === 'serv') { w = Math.min(1.2, s.len - 0.6); bottom = 1.2; top = 2.2; }
    else if (A.group === 'social' && s.side === 'back' && k === 0) { w = Math.min(s.len - 0.6, 3.2); bottom = 0; top = 2.4; kind = 'glass'; }
    else if (A.group === 'social') { w = Math.min(s.len - 0.8, 3.0); bottom = 0.45; }
    else { w = Math.min(s.len - 0.8, 1.8); bottom = 0.9; }
    if (w < 0.6) return;
    s.openings.push({ t0: (s.len - w) / 2, t1: (s.len + w) / 2, bottom: bottom, top: top, kind: kind });
  });
  // Acceso a terraza abierta desde su lado interior ya queda como puerta por conectividad

  var unreached = rooms.filter(function (r, i) { return !reached[i]; }).map(function (r) { return r.name; });
  segs.forEach(function (s) { s.openings.sort(function (p, q) { return p.t0 - q.t0; }); });
  return { segs: segs, entrance: entrance, unreached: unreached };
}

/* Divide un muro en piezas sólidas alrededor de sus vanos (alturas relativas al nivel) */
function wallPieces(s, H) {
  var pcs = [], cur = 0, top = s.low ? 1.1 : H;
  s.openings.forEach(function (o) {
    if (o.t0 > cur + 0.01) pcs.push({ t0: cur, t1: o.t0, b: 0, h: top });
    if (o.bottom > 0.01) pcs.push({ t0: o.t0, t1: o.t1, b: 0, h: o.bottom });
    if (o.top < top - 0.01) pcs.push({ t0: o.t0, t1: o.t1, b: o.top, h: top });
    cur = Math.max(cur, o.t1);
  });
  if (cur < s.len - 0.01) pcs.push({ t0: cur, t1: s.len, b: 0, h: top });
  return pcs;
}

/* ---------- cantidades de obra (paramétricas, tomadas del modelo) ---------- */
function quantities(P) {
  var H = P.H - 0.2, q = { wallLen: 0, wallArea: 0, extWallArea: 0, windowArea: 0, doors: 0, slabArea: 0, floorArea: 0,
    baths: 0, halfBaths: 0, rooms: 0, roofArea: 0, openArea: 0 };
  P.levels.forEach(function (lv) {
    lv.segs.forEach(function (s) {
      if (s.omit) return;
      q.wallLen += s.len;
      wallPieces(s, H).forEach(function (p) {
        var a = (p.t1 - p.t0) * (p.h - p.b);
        q.wallArea += a;
        if (s.ext) q.extWallArea += a;
      });
      s.openings.forEach(function (o) {
        if (o.kind === 'window' || o.kind === 'glass') q.windowArea += (o.t1 - o.t0) * (o.top - o.bottom);
        if (o.kind === 'door' || o.kind === 'entry') q.doors++;
      });
    });
    lv.rooms.forEach(function (r) {
      if (r.isStair) return;
      if (r.group === 'open') q.openArea += r.area; else q.floorArea += r.area;
      if (r.furn === 'bano') q.baths++;
      if (r.furn === 'mbano') q.halfBaths++;
      if (!r.isHall) q.rooms++;
    });
  });
  var fp = P.W * P.L;
  var stairHole = P.stair ? (P.stair.x1 - P.stair.x0) * (P.stair.y1 - P.stair.y0) : 0;
  q.footprint = fp;
  q.slabArea = (P.N - 1) * (fp - stairHole) + (fp - q.openArea);   // entrepisos + azotea
  q.roofArea = fp - q.openArea;
  q.builtArea = fp * P.N - q.openArea * 0.5;
  var concFound = fp * 0.09, concSlab = q.slabArea * 0.11, concFrame = q.wallLen * 0.075;
  q.concrete = concFound + concSlab + concFrame;
  q.steelKg = concFound * 70 + q.slabArea * 9 + concFrame * 110;
  var mortarJoint = q.wallArea * 0.012, plaster = q.wallArea * 2 * 0.015;
  q.cement = q.concrete * 7 + mortarJoint * 6 + plaster * 5.4;
  q.sand = q.concrete * 0.52 + (mortarJoint + plaster) * 1.05;
  q.gravel = q.concrete * 0.68;
  q.blocks = q.wallArea * 12.5 * 1.03;
  q.floorFinish = (q.floorArea + q.openArea) * 1.08;
  q.paintL = (q.wallArea * 2 + (q.floorArea)) * 2 / 10;
  q.waterproof = q.roofArea * 1.1;
  q.outlets = Math.round(q.rooms * 4 + q.floorArea / 12);
  return q;
}

function costing(P) {
  var q = P.quant, total = q.builtArea * P.costM2;
  var parts = CONFIG.partidas.map(function (p) { return { name: p[0], pct: p[1], amount: total * p[1] }; });
  var ratio = total / P.inp.presupuesto;
  var status = ratio <= 1.0 ? 'ok' : ratio <= 1.12 ? 'warn' : 'bad';
  var stage1 = P.N > 1 ? q.footprint * P.costM2 * 1.06 : null;
  var esencial = q.builtArea * CONFIG.costoM2.esencial * (P.inp.tipo === 'negocio' ? CONFIG.factorNegocio : 1);
  return { total: total, parts: parts, ratio: ratio, status: status, stage1: stage1, esencial: esencial };
}

function leadScore(inp) {
  var pts = (inp.presupuesto >= 2500000 ? 1 : 0) + (inp.terreno === 'si' ? 1 : 0) + ((inp.inicio === '0-3' || inp.inicio === '3-6') ? 1 : 0);
  return pts >= 3 ? 'A' : pts === 2 ? 'B' : 'C';
}

if (typeof module !== 'undefined') module.exports = { CONFIG: CONFIG, program: program, buildProject: buildProject, wallPieces: wallPieces, leadScore: leadScore };

</script>
<script>
/* ============================================================
   REVISTA HOJEABLE: portada → doble página → índice → secciones
   ============================================================ */
(function () {
  var $ = function (s, r) { return (r || document).querySelector(s); };
  var $$ = function (s, r) { return Array.prototype.slice.call((r || document).querySelectorAll(s)); };
  var store = $('#store'), book = $('#book'), slotL = $('#slotL'), slotR = $('#slotR');
  var leaf = $('#leaf'), lf = $('#leafFront'), lb = $('#leafBack');
  var reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  var DUR = reduce ? 0 : 760;
  var pad2 = function (n) { return (n < 10 ? '0' : '') + n; };
  var blocked = false, busy = false;
  function track(name, data) {
    try { (window.dataLayer = window.dataLayer || []).push(Object.assign({ event: name }, data || {})); } catch (e) {}
    try { if (window.fbq) window.fbq('trackCustom', name, data || {}); } catch (e) {}
  }

  /* ---- portada con render generado por el motor 3D ---- */
  window.onCoverRender = function (url) {
    if (!url) return;
    var img = $('#cover-img');
    img.style.backgroundImage = 'url(' + url + ')';
    img.classList.add('has-photo');
  };

  /* ---- páginas ---- */
  var P = {};
  $$('.pg', store).forEach(function (el) { P[el.dataset.id] = el; });
  var projects = CONFIG.proyectos;

  function art(i) {
    var v = [
      'M20 150 V70 H120 V40 H230 V150 Z M34 86 h70 v44 h-70z M136 54 h80 v34 h-80z M140 102 h28 v48 h-28z M184 102 h32 v26 h-32z',
      'M14 150 V86 H236 V150 Z M8 86 L242 78 M28 98 h86 v38 h-86z M132 98 h30 v52 h-30z M176 98 h44 v26 h-44z',
      'M40 150 V46 H210 V150 Z M40 98 H210 M52 110 h146 v40 h-146z M54 58 h52 v30 h-52z M118 58 h80 v30 h-80z'
    ][i % 3];
    return '<svg viewBox="0 0 250 160" aria-hidden="true"><path d="' + v + '"/><line x1="0" y1="150" x2="250" y2="150"/></svg>';
  }

  projects.forEach(function (p, i) {
    var t = document.createElement('section');
    t.className = 'pg pg-proj'; t.dataset.id = 'p' + i + 't';
    var rows = [['Ubicación', p.lugar], ['Programa', p.tipo], ['Superficie', p.superficie], ['Niveles', p.niveles], ['Año', p.anio], ['Visualización', 'D5 Render · 360°']]
      .filter(function (r) { return r[1]; })
      .map(function (r) { return '<div><dt>' + r[0] + '</dt><dd>' + r[1] + '</dd></div>'; }).join('');
    t.innerHTML = '<p class="kicker">Recorridos · ' + pad2(i + 1) + ' de ' + pad2(projects.length) + '</p>'
      + '<h2 class="proj-title">' + p.nombre + '</h2>'
      + '<p class="proj-head">' + (p.titular || '') + '</p>'
      + '<p class="proj-dek">' + (p.entrada || '') + '</p>'
      + '<dl class="specs">' + rows + '</dl>'
      + '<div class="proj-actions">' + (p.d5 ? '<a class="btn btn-ink" href="' + p.d5 + '" target="_blank" rel="noopener" data-full="' + i + '">Pantalla completa ↗</a>' : '') + '</div>'
      + '<p class="proj-hint">Arrastra dentro del recorrido para mirar alrededor →</p>'
      + '<footer class="folio"><span>Liberache · Recorridos</span><b></b></footer>';
    store.appendChild(t); P[t.dataset.id] = t;

    var v = document.createElement('section');
    v.className = 'pg pg-tour no-flip'; v.dataset.id = 'p' + i + 'v';
    v.innerHTML = '<div class="tour-frame"><div class="tour-poster"><div class="poster-inner">'
      + '<span class="poster-num">' + pad2(i + 1) + '</span><div class="poster-art">' + art(i) + '</div>'
      + '<p class="poster-msg"></p><a class="btn btn-paper poster-open" href="' + (p.d5 || '#') + '" target="_blank" rel="noopener" hidden>Abrir recorrido ↗</a>'
      + '</div></div></div>'
      + '<div class="tour-cap"><em>' + p.nombre + '</em><span>' + (p.d5 ? 'Recorrido 360° · D5 Render' : 'Recorrido en producción') + '</span></div>';
    var msg = v.querySelector('.poster-msg'), open = v.querySelector('.poster-open'), poster = v.querySelector('.tour-poster');
    v._show = function () {
      poster.hidden = false;
      if (!p.d5) { msg.textContent = 'Recorrido en producción'; return; }
      if (blocked) { msg.textContent = 'Esta vista no permite incrustar el recorrido.'; open.hidden = false; return; }
      if (v.querySelector('iframe')) return;
      msg.textContent = 'Cargando recorrido…';
      var f = document.createElement('iframe');
      f.src = p.d5; f.title = 'Recorrido virtual ' + p.nombre;
      f.setAttribute('allow', 'fullscreen; xr-spatial-tracking; gyroscope; accelerometer; autoplay');
      f.setAttribute('allowfullscreen', '');
      f.addEventListener('load', function () { if (!blocked) poster.hidden = true; });
      v.querySelector('.tour-frame').insertBefore(f, poster);
      track('recorrido_visto', { proyecto: i + 1 });
    };
    v._hide = function () {
      var f = v.querySelector('iframe'); if (f) f.remove();
      poster.hidden = false; msg.textContent = p.d5 ? '' : 'Recorrido en producción';
    };
    store.appendChild(v); P[v.dataset.id] = v;
  });
  document.addEventListener('securitypolicyviolation', function (e) {
    var d = e.effectiveDirective || e.violatedDirective || '';
    if (d.indexOf('frame') === 0 || d.indexOf('child') === 0) {
      blocked = true;
      $$('.pg-tour').forEach(function (v) { var f = v.querySelector('iframe'); if (f) f.remove(); if (v.parentNode !== store) v._show(); });
    }
  });

  /* ---- orden de páginas y pliegos ---- */
  var order = ['cover', 'indice', 'rec'];
  projects.forEach(function (p, i) { order.push('p' + i + 't', 'p' + i + 'v'); });
  order = order.concat(['cfgL', 'cfgR', 'fidL', 'fidR', 'metodo', 'faq', 'contacto', 'colofon', 'back']);
  var spreads = [{ L: null, R: 'cover' }];
  for (var k = 1; k < order.length - 1; k += 2) spreads.push({ L: order[k], R: order[k + 1] });
  spreads.push({ L: 'back', R: null });
  var pageNo = {}; order.forEach(function (id, i) { pageNo[id] = i + 1; });
  function spreadOf(id) { for (var i = 0; i < spreads.length; i++) if (spreads[i].L === id || spreads[i].R === id) return i; return 0; }

  order.forEach(function (id) {
    var el = P[id];
    var f = el.querySelector('.folio b'); if (f) f.textContent = pageNo[id];
    if (id !== 'cover' && id !== 'back') {
      var l = document.createElement('button'); l.type = 'button'; l.className = 'edge edge-l'; l.setAttribute('aria-label', 'Página anterior'); el.appendChild(l);
      var r = document.createElement('button'); r.type = 'button'; r.className = 'edge edge-r'; r.setAttribute('aria-label', 'Página siguiente'); el.appendChild(r);
    }
  });

  /* índice y referencias de página */
  var sections = [
    { n: '01', label: 'Recorridos', id: 'rec', subs: projects.map(function (p, i) { return { label: p.nombre, id: 'p' + i + 't' }; }) },
    { n: '02', label: 'Diseña la tuya', id: 'cfgL', note: 'Prototipo con 3D, planos y presupuesto' },
    { n: '03', label: 'Fidelidad de obra', id: 'fidL' },
    { n: '04', label: 'Cómo trabajamos', id: 'metodo' },
    { n: '05', label: 'Preguntas frecuentes', id: 'faq' },
    { n: '06', label: 'Contacto', id: 'contacto' }
  ];
  $('#idx').innerHTML = sections.map(function (s) {
    var subs = (s.subs || []).map(function (x) { return '<li><button type="button" class="idx-sub" data-go="' + x.id + '"><span>' + x.label + '</span><i></i><b>' + pageNo[x.id] + '</b></button></li>'; }).join('');
    return '<li><button type="button" class="idx-item" data-go="' + s.id + '"><em>' + s.n + '</em><span>' + s.label + (s.note ? '<small>' + s.note + '</small>' : '') + '</span><i></i><b>' + pageNo[s.id] + '</b></button>' + (subs ? '<ol>' + subs + '</ol>' : '') + '</li>';
  }).join('');
  $('#rec-list').innerHTML = projects.map(function (p, i) {
    return '<li><button type="button" data-go="p' + i + 't"><em>' + pad2(i + 1) + '</em><span>' + p.nombre + '<small>' + p.lugar + ' · ' + p.tipo + '</small></span><b>p. ' + pageNo['p' + i + 't'] + '</b></button></li>';
  }).join('');
  $$('[data-pageref]').forEach(function (el) { el.textContent = 'p. ' + pageNo[el.dataset.pageref]; });

  /* contacto */
  var wa = $('#contact-wa');
  if (wa) {
    wa.href = 'https://wa.me/' + CONFIG.whatsapp + '?text=' + encodeURIComponent('Hola, vi la revista de ' + CONFIG.estudio + ' y quiero diseñar mi proyecto con recorrido virtual.');
    $('#contact-num').textContent = '+' + CONFIG.whatsapp;
    wa.addEventListener('click', function () { track('cta_whatsapp', { origen: 'revista_contacto' }); });
  }

  /* ---- colocación ---- */
  var single = false, cs = 0, ci = 0;
  function put(slot, id) {
    while (slot.firstChild) store.appendChild(slot.firstChild);
    if (id) slot.appendChild(P[id]);
  }
  function visibleIds() { return single ? [order[ci]] : [spreads[cs].L, spreads[cs].R].filter(Boolean); }
  var shown = {};
  function settle() {
    var vis = visibleIds();
    Object.keys(shown).forEach(function (id) { if (vis.indexOf(id) < 0) { if (P[id]._hide) P[id]._hide(); delete shown[id]; } });
    vis.forEach(function (id) { if (!shown[id]) { shown[id] = 1; if (P[id]._show) P[id]._show(); } });
    var total = order.length;
    var label;
    if (single) label = ci === 0 ? 'Portada' : ci === total - 1 ? 'Contraportada' : (ci + 1) + ' / ' + total;
    else { var S = spreads[cs]; label = cs === 0 ? 'Portada' : cs === spreads.length - 1 ? 'Contraportada' : pageNo[S.L] + '–' + pageNo[S.R] + ' / ' + total; }
    $('#ctl-count').textContent = label;
    var atStart = single ? ci === 0 : cs === 0, atEnd = single ? ci === total - 1 : cs === spreads.length - 1;
    $('#ctl-prev').disabled = atStart; $('#ctl-next').disabled = atEnd;
    book.classList.toggle('is-closed-front', !single && cs === 0);
    book.classList.toggle('is-closed-back', !single && cs === spreads.length - 1);
    $('#ctl-hint').hidden = !atStart;
  }
  function placeStatic() {
    put(slotL, null); put(slotR, null);
    if (single) put(slotR, order[ci]);
    else { put(slotL, spreads[cs].L); put(slotR, spreads[cs].R); }
    settle();
  }

  function layout() {
    var want = window.innerWidth < 860;
    if (want !== single) {
      if (want) { var S = spreads[cs]; ci = order.indexOf(S.R || S.L); }
      else { cs = spreadOf(order[ci]); }
      single = want;
      book.classList.toggle('single', single);
      placeStatic();
    }
    var aw = window.innerWidth - (single ? 16 : 48), ah = window.innerHeight - 74 - (single ? 8 : 28);
    var pw, ph;
    if (single) { pw = aw; ph = Math.max(480, ah); }
    else { ph = Math.min(ah, (aw / 2) / 0.74); pw = ph * 0.74; }
    book.style.setProperty('--pw', Math.floor(pw) + 'px');
    book.style.setProperty('--ph', Math.floor(ph) + 'px');
  }

  /* ---- pasar página ---- */
  function hideLeaving(ids) { ids.forEach(function (id) { if (id && shown[id]) { if (P[id]._hide) P[id]._hide(); delete shown[id]; } }); }
  function animateLeaf(cls, from, to, done) {
    leaf.className = 'leaf ' + cls;
    leaf.style.transition = 'none';
    leaf.style.transform = 'rotateY(' + from + 'deg)';
    leaf.hidden = false;
    void leaf.offsetWidth;
    leaf.style.transition = '';
    leaf.style.transform = 'rotateY(' + to + 'deg)';
    setTimeout(function () {
      done();
      put(lf, null); put(lb, null);
      leaf.hidden = true; leaf.style.transform = '';
      busy = false; settle();
    }, DUR + 30);
  }
  function go(t, src) {
    if (busy) return;
    if (single) {
      if (t < 0 || t >= order.length || t === ci) return;
      busy = true;
      var cur = order[ci], nxt = order[t];
      track('revista_pagina', { pagina: t + 1, via: src || 'flecha' });
      hideLeaving([cur]);
      if (t > ci) { put(lf, cur); put(slotR, nxt); ci = t; animateLeaf('fwd', 0, -180, function () {}); }
      else { put(lf, nxt); ci = t; animateLeaf('fwd', -180, 0, function () { put(slotR, nxt); }); }
      return;
    }
    if (t < 0 || t >= spreads.length || t === cs) return;
    busy = true;
    var S = spreads[cs], T = spreads[t], fwd = t > cs;
    track('revista_pagina', { pagina: pageNo[T.L || T.R], via: src || 'flecha' });
    if (cs === 0) track('revista_abierta', {});
    hideLeaving([S.L, S.R]);
    if (fwd) {
      put(lf, S.R); put(lb, T.L); put(slotR, T.R);
      cs = t;
      book.classList.toggle('is-closed-front', false);
      book.classList.toggle('is-closed-back', t === spreads.length - 1);
      animateLeaf('fwd', 0, -180, function () { put(slotL, T.L); });
    } else {
      put(lf, S.L); put(lb, T.R); put(slotL, T.L);
      cs = t;
      book.classList.toggle('is-closed-back', false);
      book.classList.toggle('is-closed-front', t === 0);
      animateLeaf('bwd', 0, 180, function () { put(slotR, T.R); });
    }
  }
  function next(src) { go((single ? ci : cs) + 1, src); }
  function prev(src) { go((single ? ci : cs) - 1, src); }
  function goId(id, src) { go(single ? order.indexOf(id) : spreadOf(id), src); }

  /* clics: hoja derecha avanza, hoja izquierda regresa */
  var interactive = 'a,button,input,label,select,textarea,summary,details,canvas,iframe,.viewer,.no-flip-zone';
  book.addEventListener('click', function (e) {
    var go2 = e.target.closest('[data-go]');
    if (go2) { goId(go2.dataset.go, 'indice'); track('revista_indice', { destino: go2.dataset.go }); return; }
    var edge = e.target.closest('.edge');
    if (edge) { if (edge.classList.contains('edge-r')) next('borde'); else prev('borde'); return; }
    if (busy || e.target.closest(interactive)) return;
    var page = e.target.closest('.pg');
    if (!page || page.classList.contains('no-flip')) return;
    if (single) {
      var r = page.getBoundingClientRect();
      if (e.clientX - r.left > r.width * 0.4) next('hoja'); else prev('hoja');
    } else if (page.parentNode === slotR) next('hoja');
    else if (page.parentNode === slotL) prev('hoja');
  });
  $('#ctl-prev').addEventListener('click', function () { prev('control'); });
  $('#ctl-next').addEventListener('click', function () { next('control'); });
  $('#ctl-index').addEventListener('click', function () { goId('indice', 'control'); });
  $('#to-cover').addEventListener('click', function (e) { e.stopPropagation(); go(0, 'contraportada'); });
  document.addEventListener('keydown', function (e) {
    var t = e.target;
    if (t.closest && t.closest('input,textarea,select,.viewer')) return;
    if (e.key === 'ArrowRight' || e.key === 'PageDown') { e.preventDefault(); next('teclado'); }
    if (e.key === 'ArrowLeft' || e.key === 'PageUp') { e.preventDefault(); prev('teclado'); }
  });
  var sx = null, sy = null;
  book.addEventListener('touchstart', function (e) { if (e.target.closest('.viewer,iframe,input')) { sx = null; return; } sx = e.touches[0].clientX; sy = e.touches[0].clientY; }, { passive: true });
  book.addEventListener('touchend', function (e) {
    if (sx == null) return;
    var dx = e.changedTouches[0].clientX - sx, dy = e.changedTouches[0].clientY - sy; sx = null;
    if (Math.abs(dx) > 60 && Math.abs(dx) > Math.abs(dy) * 1.5) { if (dx < 0) next('deslizar'); else prev('deslizar'); }
  });

  var rt; window.addEventListener('resize', function () { clearTimeout(rt); rt = setTimeout(layout, 80); });
  single = !(window.innerWidth < 860);   // fuerza la primera colocación
  layout();
  track('revista_vista', {});
})();

</script>
<script>
/* ============================================================
   VISOR 3D: maqueta, vista exterior y recorrido en primera persona
   ============================================================ */
function Viewer3D(container, canvas, hud) {
  var T = window.THREE;
  var self = this;
  this.ok = !!T;
  if (!T) return;
  var renderer = new T.WebGLRenderer({ canvas: canvas, antialias: true, preserveDrawingBuffer: false });
  renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
  renderer.shadowMap.enabled = true;
  renderer.shadowMap.type = T.PCFSoftShadowMap;
  renderer.outputEncoding = T.sRGBEncoding;
  renderer.toneMapping = T.ACESFilmicToneMapping;
  renderer.toneMappingExposure = 1.05;

  var scene = new T.Scene();
  scene.background = new T.Color(0xdde3e6);
  scene.fog = new T.Fog(0xdde3e6, 60, 160);
  var camera = new T.PerspectiveCamera(40, 1, 0.05, 400);
  camera.rotation.order = 'YXZ';

  var hemi = new T.HemisphereLight(0xffffff, 0x8d877b, 0.62);
  scene.add(hemi);
  var amb = new T.AmbientLight(0xffffff, 0.12);
  scene.add(amb);
  var sun = new T.DirectionalLight(0xfff3e0, 1.05);
  sun.castShadow = true;
  sun.shadow.mapSize.set(2048, 2048);
  sun.shadow.bias = -0.0006;
  sun.shadow.normalBias = 0.02;
  scene.add(sun);
  scene.add(sun.target);

  /* ---- texturas procedurales ---- */
  function canvasTex(size, draw) {
    var c = document.createElement('canvas');
    c.width = c.height = size;
    var g = c.getContext('2d');
    draw(g, size);
    var t = new T.CanvasTexture(c);
    t.wrapS = t.wrapT = T.RepeatWrapping;
    t.encoding = T.sRGBEncoding;
    t.anisotropy = 4;
    return t;
  }
  function noise(g, s, a) {
    var img = g.getImageData(0, 0, s, s), d = img.data;
    for (var i = 0; i < d.length; i += 4) { var n = (Math.random() - 0.5) * a; d[i] += n; d[i + 1] += n; d[i + 2] += n; }
    g.putImageData(img, 0, 0);
  }
  var TEX = {
    wood: canvasTex(512, function (g, s) {
      var rows = 8, h = s / rows;
      for (var r = 0; r < rows; r++) {
        var off = (r % 2) * s * 0.45;
        for (var x = -s; x < s * 2; x += s * 0.9) {
          var tint = 150 + Math.random() * 30;
          g.fillStyle = 'rgb(' + (tint + 25) + ',' + (tint - 10) + ',' + (tint - 50) + ')';
          g.fillRect(x + off, r * h, s * 0.9, h);
          g.strokeStyle = 'rgba(60,40,20,0.35)'; g.lineWidth = 2;
          g.strokeRect(x + off, r * h, s * 0.9, h);
        }
      }
      noise(g, s, 18);
    }),
    porc: canvasTex(512, function (g, s) {
      g.fillStyle = '#e7e4de'; g.fillRect(0, 0, s, s); noise(g, s, 10);
      g.strokeStyle = 'rgba(120,115,105,0.45)'; g.lineWidth = 2;
      for (var i = 0; i <= 2; i++) { g.beginPath(); g.moveTo(i * s / 2, 0); g.lineTo(i * s / 2, s); g.stroke(); g.beginPath(); g.moveTo(0, i * s / 2); g.lineTo(s, i * s / 2); g.stroke(); }
    }),
    tile: canvasTex(256, function (g, s) {
      g.fillStyle = '#d9dcdc'; g.fillRect(0, 0, s, s); noise(g, s, 8);
      g.strokeStyle = 'rgba(100,105,105,0.5)'; g.lineWidth = 2;
      for (var i = 0; i <= 4; i++) { g.beginPath(); g.moveTo(i * s / 4, 0); g.lineTo(i * s / 4, s); g.stroke(); g.beginPath(); g.moveTo(0, i * s / 4); g.lineTo(s, i * s / 4); g.stroke(); }
    }),
    deck: canvasTex(256, function (g, s) {
      for (var r = 0; r < 8; r++) { var t = 110 + Math.random() * 25; g.fillStyle = 'rgb(' + (t + 20) + ',' + (t - 15) + ',' + (t - 45) + ')'; g.fillRect(0, r * s / 8, s, s / 8 - 3); }
      noise(g, s, 14);
    }),
    conc: canvasTex(256, function (g, s) { g.fillStyle = '#b9b7b1'; g.fillRect(0, 0, s, s); noise(g, s, 26); }),
    grass: canvasTex(256, function (g, s) { g.fillStyle = '#7d9161'; g.fillRect(0, 0, s, s); noise(g, s, 34); }),
    paving: canvasTex(256, function (g, s) {
      g.fillStyle = '#c9c4ba'; g.fillRect(0, 0, s, s); noise(g, s, 16);
      g.strokeStyle = 'rgba(90,85,80,0.4)'; g.lineWidth = 3;
      for (var i = 0; i <= 2; i++) { g.beginPath(); g.moveTo(0, i * s / 2); g.lineTo(s, i * s / 2); g.stroke(); }
    }),
    asphalt: canvasTex(256, function (g, s) { g.fillStyle = '#4a4c4f'; g.fillRect(0, 0, s, s); noise(g, s, 22); })
  };
  var TILE = { wood: 1.8, porc: 1.2, tile: 0.8, deck: 1.4, conc: 2.5, grass: 5, paving: 1.2, asphalt: 6 };
  var floorMats = {};
  Object.keys(TEX).forEach(function (k) { floorMats[k] = new T.MeshStandardMaterial({ map: TEX[k], roughness: k === 'porc' || k === 'tile' ? 0.45 : 0.85 }); });

  var M = {
    wall: new T.MeshStandardMaterial({ color: 0xf1efea, roughness: 0.92 }),
    slab: new T.MeshStandardMaterial({ color: 0xecebe7, roughness: 0.95 }),
    accent: new T.MeshStandardMaterial({ color: 0x2b2d30, roughness: 0.7 }),
    woodSlat: new T.MeshStandardMaterial({ color: 0x9a6b42, roughness: 0.7 }),
    glass: new T.MeshStandardMaterial({ color: 0x8fb1c2, roughness: 0.05, metalness: 0.2, transparent: true, opacity: 0.32, depthWrite: false }),
    frame: new T.MeshStandardMaterial({ color: 0x3a3c3f, roughness: 0.5, metalness: 0.4 }),
    door: new T.MeshStandardMaterial({ color: 0x7a5435, roughness: 0.6 }),
    fabric: new T.MeshStandardMaterial({ color: 0xb8b1a5, roughness: 0.95 }),
    fabric2: new T.MeshStandardMaterial({ color: 0x5f6f73, roughness: 0.95 }),
    white: new T.MeshStandardMaterial({ color: 0xf6f6f4, roughness: 0.4 }),
    dark: new T.MeshStandardMaterial({ color: 0x2f3134, roughness: 0.6 }),
    furnWood: new T.MeshStandardMaterial({ color: 0xa47b52, roughness: 0.7 }),
    rug: new T.MeshStandardMaterial({ color: 0xcfc6b6, roughness: 1 }),
    barda: new T.MeshStandardMaterial({ color: 0xc8c4bc, roughness: 0.95 }),
    trunk: new T.MeshStandardMaterial({ color: 0x6b5340, roughness: 0.9 }),
    leaf: new T.MeshStandardMaterial({ color: 0x5d7a45, roughness: 0.9, flatShading: true }),
    leaf2: new T.MeshStandardMaterial({ color: 0x7a9455, roughness: 0.9, flatShading: true }),
    stair: new T.MeshStandardMaterial({ color: 0xd8d3ca, roughness: 0.6 })
  };

  var world = new T.Group(); scene.add(world);
  var levelGroups = [], roofGroup = null, colliders = [], P = null;

  function addBox(parent, w, h, d, mat, x, y, z, noShadow) {
    if (w <= 0.001 || h <= 0.001 || d <= 0.001) return null;
    var m = new T.Mesh(new T.BoxGeometry(w, h, d), mat);
    m.position.set(x, y, z);
    if (!noShadow) { m.castShadow = true; m.receiveShadow = true; }
    parent.add(m);
    return m;
  }
  function addFloor(parent, x0, z0, x1, z1, y, key) {
    var w = x1 - x0, d = z1 - z0;
    if (w <= 0 || d <= 0) return;
    var geo = new T.PlaneGeometry(w, d);
    var uv = geo.attributes.uv, tile = TILE[key] || 1.5;
    for (var i = 0; i < uv.count; i++) uv.setXY(i, uv.getX(i) * w / tile, uv.getY(i) * d / tile);
    var m = new T.Mesh(geo, floorMats[key] || floorMats.porc);
    m.rotation.x = -Math.PI / 2;
    m.position.set(x0 + w / 2, y, z0 + d / 2);
    m.receiveShadow = true;
    parent.add(m);
  }
  function rectsMinus(r, h) {
    if (!h) return [r];
    var out = [];
    if (h.y0 > r.y0) out.push({ x0: r.x0, y0: r.y0, x1: r.x1, y1: h.y0 });
    if (h.y1 < r.y1) out.push({ x0: r.x0, y0: h.y1, x1: r.x1, y1: r.y1 });
    if (h.x0 > r.x0) out.push({ x0: r.x0, y0: h.y0, x1: h.x0, y1: h.y1 });
    if (h.x1 < r.x1) out.push({ x0: h.x1, y0: h.y0, x1: r.x1, y1: h.y1 });
    return out;
  }

  /* ---- muebles básicos, orientados al lado largo de cada pieza ---- */
  function furnish(g, r, y) {
    var cx = (r.x0 + r.x1) / 2, cz = (r.y0 + r.y1) / 2;
    var longX = r.w >= r.h, U = longX ? r.w : r.h, V = longX ? r.h : r.w;
    function put(u, v, wu, h, dv, mat, yb) {
      var x = longX ? cx + u : cx + v, z = longX ? cz + v : cz + u;
      var sx = longX ? wu : dv, sz = longX ? dv : wu;
      return addBox(g, sx, h, sz, mat, x, y + (yb || 0) + h / 2, z);
    }
    var e = V / 2;
    switch (r.furn) {
      case 'sala': case 'estar':
        if (U < 2.6 || V < 2.4) break;
        put(0, e - 0.55, Math.min(2.3, U - 0.6), 0.42, 0.85, M.fabric);
        put(0, e - 0.2, Math.min(2.3, U - 0.6), 0.4, 0.18, M.fabric, 0.4);
        put(0, e - 1.55, 1.1, 0.38, 0.55, M.furnWood);
        put(0, e - 1.4, Math.min(2.8, U - 0.4), 0.01, Math.min(2.0, V - 0.6), M.rug);
        if (r.furn === 'estar') put(0, -e + 0.2, 1.6, 0.5, 0.35, M.dark);
        break;
      case 'comedor':
        if (U < 2.4 || V < 2.2) break;
        put(0, 0, 1.8, 0.75, 0.95, M.furnWood);
        for (var i = -1; i <= 1; i++) { put(i * 0.6, 0.75, 0.45, 0.45, 0.45, M.fabric2); put(i * 0.6, -0.75, 0.45, 0.45, 0.45, M.fabric2); }
        break;
      case 'cocina':
        var cl = Math.min(U - 0.3, 3.6);
        put(0, e - 0.32, cl, 0.9, 0.62, M.white);
        put(0, e - 0.18, cl, 0.7, 0.35, M.furnWood, 1.5);
        if (V >= 3.0) put(0, -0.2, Math.min(1.8, U - 1.4), 0.92, 0.9, M.dark);
        break;
      case 'cama': case 'cama2':
        if (V < 2.5 || U < 2.2) break;
        var bw = r.furn === 'cama' ? 1.9 : 1.4;
        put(0, e - 1.05, bw, 0.5, 2.0, M.white);
        put(0, e - 0.08, bw + 0.1, 1.0, 0.08, M.furnWood);
        if (U > bw + 1.2) { put(bw / 2 + 0.3, e - 0.25, 0.45, 0.5, 0.4, M.furnWood); put(-bw / 2 - 0.3, e - 0.25, 0.45, 0.5, 0.4, M.furnWood); }
        break;
      case 'bano': case 'mbano':
        put(-U / 2 + 0.35, e - 0.33, 0.4, 0.42, 0.62, M.white);
        if (U > 1.6) put(-U / 2 + 1.15, e - 0.25, Math.min(0.9, U - 1.4), 0.85, 0.5, M.white);
        if (r.furn === 'bano' && U > 2.2) put(U / 2 - 0.9, 0, 0.02, 2.0, V - 0.2, M.glass);
        break;
      case 'lav': put(0, e - 0.35, 0.65, 0.9, 0.65, M.white); break;
      case 'vest': put(0, e - 0.3, U - 0.3, 2.1, 0.55, M.furnWood); break;
      case 'escritorio': case 'recepcion':
        if (U < 2 || V < 2) break;
        put(0, e - 0.75, 1.5, 0.75, 0.7, M.furnWood);
        put(0, e - 1.4, 0.5, 0.48, 0.5, M.fabric2);
        if (r.furn === 'recepcion') for (var j = -1; j <= 1; j++) put(j * 0.7, -e + 0.4, 0.5, 0.45, 0.5, M.fabric);
        break;
      case 'consult':
        if (U < 2.4 || V < 2.2) break;
        put(-U / 4, e - 0.6, 1.3, 0.75, 0.65, M.furnWood);
        put(U / 4, -e + 0.6, 1.9, 0.75, 0.7, M.white);
        break;
      case 'ventas':
        put(0, -e + 0.25, Math.max(1, U - 1.2), 1.8, 0.4, M.furnWood);
        put(0, e - 1.0, Math.min(2.4, U - 1), 1.0, 0.6, M.dark);
        break;
      case 'oficinas':
        for (var a = -1; a <= 1; a += 2) put(a * U / 4, 0, 1.6, 0.75, 1.2, M.white);
        break;
      case 'mesas': case 'terraza':
        var nx = Math.max(1, Math.floor((U - 0.6) / 2.1)), nv = Math.max(1, Math.floor((V - 0.6) / 2.1));
        for (var p = 0; p < nx; p++) for (var q = 0; q < nv; q++) {
          var uu = -U / 2 + (U / nx) * (p + 0.5), vv = -V / 2 + (V / nv) * (q + 0.5);
          if (r.furn === 'terraza') { put(uu, vv, 0.6, 0.35, 1.6, M.white); }
          else { put(uu, vv, 0.8, 0.75, 0.8, M.furnWood); put(uu - 0.6, vv, 0.42, 0.45, 0.42, M.fabric2); put(uu + 0.6, vv, 0.42, 0.45, 0.42, M.fabric2); }
        }
        if (r.furn === 'terraza') { put(-U / 2 + 0.4, e - 0.35, 0.6, 0.7, 0.6, M.leaf); put(U / 2 - 0.4, e - 0.35, 0.6, 0.7, 0.6, M.leaf2); }
        break;
      case 'cocinapro':
        put(0, e - 0.35, U - 0.4, 0.9, 0.7, M.white);
        put(0, -0.1, Math.max(0.8, U - 2), 0.9, 0.8, M.white);
        break;
      case 'bodega':
        put(0, e - 0.25, U - 0.3, 1.9, 0.45, M.frame);
        break;
    }
  }

  function stairMesh(g, st, y, H) {
    var sw = st.x1 - st.x0, run = (sw - 1.0) / 9, rise = H / 18;
    var halfD = (st.y1 - st.y0) / 2 - 0.1;
    for (var i = 0; i < 9; i++) {
      var top = (i + 1) * rise;
      addBox(g, run, top, halfD, M.stair, st.x0 + (i + 0.5) * run, y + top / 2, st.y0 + 0.05 + halfD / 2);
    }
    var land = 9 * rise;
    addBox(g, 0.95, land, st.y1 - st.y0 - 0.1, M.stair, st.x1 - 0.5, y + land / 2, (st.y0 + st.y1) / 2);
    for (var j = 0; j < 9; j++) {
      var t2 = land + (j + 1) * rise;
      addBox(g, run, t2, halfD, M.stair, st.x1 - 1.0 - (j + 0.5) * run, y + t2 / 2, st.y1 - 0.05 - halfD / 2);
    }
  }

  function clearWorld() {
    while (world.children.length) {
      var c = world.children.pop();
      c.traverse(function (o) { if (o.geometry) o.geometry.dispose(); });
    }
    levelGroups = []; colliders = [];
  }

  this.build = function (project) {
    P = project;
    clearWorld();
    var H = P.H, WH = H - 0.2, W = P.W, L = P.L, t = 0.15, inp = P.inp;
    var acab = inp.acabado;

    /* sitio */
    var site = new T.Group(); world.add(site);
    var F = inp.frente, D = inp.fondo, sf = P.sf;
    addFloor(site, -40, -sf - 40, F + 40, D - sf + 40, -0.06, 'grass');
    addFloor(site, -40, -sf - 9, F + 40, -sf - 2.2, -0.04, 'asphalt');
    addFloor(site, -40, -sf - 2.2, F + 40, -sf, -0.03, 'paving');
    addFloor(site, 0, -sf, Math.min(F, W), 0, -0.02, 'paving');
    addBox(site, 0.15, 1.9, D, M.barda, -0.25, 0.95, -sf + D / 2);
    addBox(site, 0.15, 1.9, D, M.barda, F + 0.08, 0.95, -sf + D / 2);
    addBox(site, F + 0.5, 1.9, 0.15, M.barda, F / 2, 0.95, D - sf + 0.08);
    var backFree = D - sf - L;
    if (backFree > 2.5) {
      var tree = function (x, z, s) {
        var tr = new T.Mesh(new T.CylinderGeometry(0.08 * s, 0.12 * s, 2.2 * s, 6), M.trunk); tr.position.set(x, 1.1 * s, z); tr.castShadow = true; site.add(tr);
        var lf = new T.Mesh(new T.IcosahedronGeometry(1.2 * s, 1), Math.random() > 0.5 ? M.leaf : M.leaf2); lf.position.set(x, 2.6 * s, z); lf.castShadow = true; site.add(lf);
      };
      tree(Math.min(F - 1.2, W * 0.75), L + backFree * 0.55, 1);
      if (F > 8) tree(1.4, L + backFree * 0.6, 0.8);
    }
    if (F - W > 2) addFloor(site, W, 0, F, Math.min(L, D - sf), -0.02, 'grass');

    /* niveles */
    P.levels.forEach(function (lv, k) {
      var g = new T.Group(); world.add(g); levelGroups.push(g);
      var y = k * H, col = [];
      var foot = { x0: 0, y0: 0, x1: W, y1: L };
      if (k === 0) addBox(g, W, 0.15, L, M.slab, W / 2, -0.075, L / 2);
      else rectsMinus(foot, P.stair).forEach(function (r) { addBox(g, r.x1 - r.x0, 0.2, r.y1 - r.y0, M.slab, (r.x0 + r.x1) / 2, y - 0.1, (r.y0 + r.y1) / 2); });
      lv.rooms.forEach(function (r) {
        if (r.isStair && k > 0) return;
        addFloor(g, r.x0, r.y0, r.x1, r.y1, y + 0.006, r.floor);
        furnish(g, r, y);
      });
      if (P.stair && k < P.N - 1) stairMesh(g, P.stair, y, H);
      if (P.stair && k > 0) {
        addBox(g, 0.03, 1.0, P.stair.y1 - P.stair.y0, M.glass, P.stair.x0, y + 0.5, (P.stair.y0 + P.stair.y1) / 2, true);
      }
      if (P.stair) col.push({ x0: P.stair.x0 + 0.05, x1: P.stair.x1, z0: P.stair.y0 + 0.05, z1: P.stair.y1 - 0.05 });

      lv.segs.forEach(function (s) {
        if (s.omit) return;
        var ext = s.ext ? t / 2 : 0;
        wallPieces(s, WH).forEach(function (p) {
          var a0 = s.s0 + p.t0 - (p.t0 < 0.01 ? ext : 0), a1 = s.s0 + p.t1 + (p.t1 > s.len - 0.01 ? ext : 0);
          var len = a1 - a0, h = p.h - p.b, cy = y + p.b + h / 2, mid = (a0 + a1) / 2;
          if (s.axis === 'h') addBox(g, len, h, t, M.wall, mid, cy, s.c);
          else addBox(g, t, h, len, M.wall, s.c, cy, mid);
          if (p.b < 0.5) {
            if (s.axis === 'h') col.push({ x0: a0, x1: a1, z0: s.c - t / 2, z1: s.c + t / 2 });
            else col.push({ x0: s.c - t / 2, x1: s.c + t / 2, z0: a0, z1: a1 });
          }
        });
        s.openings.forEach(function (o) {
          var a0 = s.s0 + o.t0, a1 = s.s0 + o.t1, len = a1 - a0, mid = (a0 + a1) / 2;
          if (o.kind === 'window' || o.kind === 'glass') {
            var h = o.top - o.bottom, cy = y + o.bottom + h / 2;
            if (s.axis === 'h') { addBox(g, len, h, 0.02, M.glass, mid, cy, s.c, true); addBox(g, len, 0.05, t + 0.02, M.frame, mid, y + o.bottom + 0.025, s.c, true); }
            else { addBox(g, 0.02, h, len, M.glass, s.c, cy, mid, true); addBox(g, t + 0.02, 0.05, len, M.frame, s.c, y + o.bottom + 0.025, mid, true); }
            if (o.kind === 'window' && h > 0.3 && o.bottom > 0) {
              if (s.axis === 'h') col.push({ x0: a0, x1: a1, z0: s.c - t / 2, z1: s.c + t / 2 });
              else col.push({ x0: s.c - t / 2, x1: s.c + t / 2, z0: a0, z1: a1 });
            }
          }
          if (o.kind === 'entry') {
            var leaf = new T.Mesh(new T.BoxGeometry(len - 0.05, o.top - 0.02, 0.05), M.door);
            var pivot = new T.Group();
            pivot.position.set(a0 + 0.02, y, s.c + 0.05);
            leaf.position.set((len - 0.05) / 2, (o.top - 0.02) / 2, 0);
            pivot.add(leaf); pivot.rotation.y = -1.15; leaf.castShadow = true;
            g.add(pivot);
          }
        });
      });
      levelGroups[k].userData.col = col;
    });

    /* azotea, pretiles y fachada */
    roofGroup = new T.Group(); world.add(roofGroup);
    var top = P.N * H, lastRooms = P.levels[P.N - 1].rooms;
    var open = lastRooms.filter(function (r) { return r.group === 'open'; });
    var roofRects = [{ x0: 0, y0: 0, x1: W, y1: L }];
    open.forEach(function (o) {
      var next = [];
      roofRects.forEach(function (r) {
        var ix0 = Math.max(r.x0, o.x0), ix1 = Math.min(r.x1, o.x1), iy0 = Math.max(r.y0, o.y0), iy1 = Math.min(r.y1, o.y1);
        if (ix1 - ix0 < 0.01 || iy1 - iy0 < 0.01) { next.push(r); return; }
        next = next.concat(rectsMinus(r, { x0: ix0, y0: iy0, x1: ix1, y1: iy1 }));
      });
      roofRects = next;
    });
    roofRects.forEach(function (r) { addBox(roofGroup, r.x1 - r.x0, 0.2, r.y1 - r.y0, M.slab, (r.x0 + r.x1) / 2, top - 0.1, (r.y0 + r.y1) / 2); });
    var par = 0.6, pt = 0.15;
    addBox(roofGroup, W + pt, par, pt, M.wall, W / 2, top + par / 2, 0);
    addBox(roofGroup, W + pt, par, pt, M.wall, W / 2, top + par / 2, L);
    addBox(roofGroup, pt, par, L, M.wall, 0, top + par / 2, L / 2);
    addBox(roofGroup, pt, par, L, M.wall, W, top + par / 2, L / 2);
    if (acab !== 'esencial') {
      for (var k2 = 1; k2 <= P.N; k2++) addBox(roofGroup, W + 0.3, 0.22, 0.75, M.accent, W / 2, k2 * H - 0.09, -0.36);
    }
    if (acab === 'premium' && P.N > 1) {
      var x0 = W * 0.55, n = Math.floor((W * 0.42) / 0.16);
      for (var i = 0; i < n; i++) addBox(roofGroup, 0.06, H - 0.25, 0.12, M.woodSlat, x0 + i * 0.16, (P.N - 1) * H + (H - 0.25) / 2, -0.55);
    }

    /* luz y cámara */
    var span = Math.max(F, D, 14);
    sun.position.set(W / 2 + 14, 26, L / 2 - 16);
    sun.target.position.set(W / 2, 0, L / 2);
    var sc = sun.shadow.camera;
    sc.left = -span; sc.right = span; sc.top = span; sc.bottom = -span; sc.near = 1; sc.far = 90;
    sc.updateProjectionMatrix();

    orbit.target = { x: W / 2, y: Math.min(P.N * H, 6) * 0.45, z: L / 2 };
    orbit.r = Math.max(W, L, P.N * H) * 2.3 + 6;
    self.setMode(self.mode || 'exterior', self.cutLevel);
    self.dirty = true;
  };

  /* ---- modos de vista ---- */
  var orbit = { theta: Math.PI - 0.72, phi: 1.12, r: 30, target: { x: 0, y: 0, z: 0 }, auto: true };
  var walker = { x: 0, z: 0, level: 0, yaw: Math.PI, pitch: 0, keys: {} };
  this.mode = 'exterior';
  this.cutLevel = 0;

  this.setMode = function (mode, level) {
    self.mode = mode;
    if (!P) return;
    if (mode === 'maqueta') self.cutLevel = level == null ? 0 : level;
    levelGroups.forEach(function (g, k) { g.visible = mode !== 'maqueta' || k <= self.cutLevel; });
    if (roofGroup) roofGroup.visible = mode !== 'maqueta';
    if (mode === 'walk') {
      camera.fov = 72; amb.intensity = 0.42; hemi.intensity = 0.7;
      self.goLevel(level == null ? 0 : level);
    } else {
      camera.fov = 40; amb.intensity = 0.12; hemi.intensity = 0.62;
    }
    camera.updateProjectionMatrix();
    self.dirty = true;
  };
  this.goLevel = function (k) {
    walker.level = k;
    var lv = P.levels[k];
    if (k === 0 && lv.entrance) { walker.x = lv.entrance.x; walker.z = 1.0; walker.yaw = Math.PI; }
    else {
      var hall = lv.rooms.filter(function (r) { return r.isHall; })[0];
      walker.x = (hall.x0 + hall.x1) / 2; walker.z = (hall.y0 + hall.y1) / 2; walker.yaw = 0;
    }
    walker.pitch = -0.05;
    self.dirty = true;
  };

  function collide() {
    var r = 0.26, col = (levelGroups[walker.level] && levelGroups[walker.level].userData.col) || [];
    for (var pass = 0; pass < 2; pass++) {
      col.forEach(function (b) {
        var cx = clamp(walker.x, b.x0, b.x1), cz = clamp(walker.z, b.z0, b.z1);
        var dx = walker.x - cx, dz = walker.z - cz, d2 = dx * dx + dz * dz;
        if (d2 < r * r) {
          var d = Math.sqrt(d2) || 0.0001;
          if (d2 === 0) { dx = 0; dz = -1; d = 1; }
          walker.x = cx + dx / d * r; walker.z = cz + dz / d * r;
        }
      });
    }
    var F = P.inp.frente, D = P.inp.fondo;
    walker.x = clamp(walker.x, 0.1, F - 0.1);
    walker.z = clamp(walker.z, -P.sf - 2, D - P.sf - 0.2);
  }

  function roomAt() {
    var lv = P.levels[walker.level];
    for (var i = 0; i < lv.rooms.length; i++) {
      var r = lv.rooms[i];
      if (walker.x >= r.x0 && walker.x <= r.x1 && walker.z >= r.y0 && walker.z <= r.y1) return r;
    }
    return null;
  }

  /* ---- controles ---- */
  var pointers = {}, lastPinch = 0;
  canvas.addEventListener('pointerdown', function (e) {
    pointers[e.pointerId] = { x: e.clientX, y: e.clientY };
    orbit.auto = false;
    try { canvas.setPointerCapture(e.pointerId); } catch (err) {}
  });
  canvas.addEventListener('pointermove', function (e) {
    var p = pointers[e.pointerId]; if (!p) return;
    var ids = Object.keys(pointers);
    if (ids.length === 2) {
      var a = pointers[ids[0]], b = pointers[ids[1]];
      p.x = e.clientX; p.y = e.clientY;
      var dist = Math.hypot(a.x - b.x, a.y - b.y);
      if (lastPinch && self.mode !== 'walk') orbit.r = clamp(orbit.r * lastPinch / dist, 6, 120);
      lastPinch = dist; self.dirty = true; return;
    }
    var dx = e.clientX - p.x, dy = e.clientY - p.y;
    p.x = e.clientX; p.y = e.clientY;
    if (self.mode === 'walk') { walker.yaw -= dx * 0.005; walker.pitch = clamp(walker.pitch - dy * 0.004, -1.1, 1.1); }
    else { orbit.theta -= dx * 0.006; orbit.phi = clamp(orbit.phi - dy * 0.006, 0.2, 1.48); }
    self.dirty = true;
  });
  function up(e) { delete pointers[e.pointerId]; lastPinch = 0; }
  canvas.addEventListener('pointerup', up);
  canvas.addEventListener('pointercancel', up);
  canvas.addEventListener('wheel', function (e) {
    if (self.mode === 'walk') return;
    e.preventDefault();
    orbit.r = clamp(orbit.r * (1 + Math.sign(e.deltaY) * 0.08), 6, 120);
    orbit.auto = false; self.dirty = true;
  }, { passive: false });
  canvas.tabIndex = 0;
  var keyMap = { KeyW: 'f', ArrowUp: 'f', KeyS: 'b', ArrowDown: 'b', KeyA: 'l', KeyD: 'r', ArrowLeft: 'tl', ArrowRight: 'tr', KeyQ: 'tl', KeyE: 'tr' };
  container.addEventListener('keydown', function (e) {
    if (self.mode !== 'walk') return;
    var k = keyMap[e.code]; if (!k) return;
    e.preventDefault(); walker.keys[k] = true;
  });
  container.addEventListener('keyup', function (e) { var k = keyMap[e.code]; if (k) walker.keys[k] = false; });
  this.press = function (k, on) { walker.keys[k] = on; };
  /* Fotografía fija del modelo (se usa como imagen de portada) */
  this.snapshot = function (w, h) {
    if (!P) return null;
    renderer.setSize(w, h, false);
    camera.aspect = w / h; camera.fov = 34; camera.updateProjectionMatrix();
    var tg = orbit.target, r = orbit.r * 1.3, th = Math.PI - 0.52, ph = 1.36;
    camera.position.set(tg.x + r * Math.sin(ph) * Math.sin(th), tg.y + r * Math.cos(ph), tg.z + r * Math.sin(ph) * Math.cos(th));
    camera.lookAt(tg.x, tg.y + 3.2, tg.z);
    renderer.render(scene, camera);
    var url = canvas.toDataURL('image/jpeg', 0.88);
    camera.fov = 40; resize();
    self.dirty = true;
    return url;
  };

  /* ---- bucle ---- */
  var visible = true, last = performance.now();
  if ('IntersectionObserver' in window) new IntersectionObserver(function (en) { visible = en[0].isIntersecting; }).observe(container);
  function resize() {
    var w = container.clientWidth, h = container.clientHeight;
    if (!w || !h) return;
    renderer.setSize(w, h, false);
    camera.aspect = w / h; camera.updateProjectionMatrix(); self.dirty = true;
  }
  if ('ResizeObserver' in window) new ResizeObserver(resize).observe(container);
  resize();
  var reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  function frame(now) {
    requestAnimationFrame(frame);
    var dt = Math.min(0.05, (now - last) / 1000); last = now;
    if (!visible || !P) return;
    var moving = false;
    if (self.mode === 'walk') {
      var k = walker.keys, sp = 1.7 * dt;
      if (k.tl) { walker.yaw += 1.6 * dt; moving = true; }
      if (k.tr) { walker.yaw -= 1.6 * dt; moving = true; }
      var fx = -Math.sin(walker.yaw), fz = -Math.cos(walker.yaw), rx = Math.cos(walker.yaw), rz = -Math.sin(walker.yaw);
      var mx = 0, mz = 0;
      if (k.f) { mx += fx; mz += fz; } if (k.b) { mx -= fx; mz -= fz; }
      if (k.r) { mx += rx; mz += rz; } if (k.l) { mx -= rx; mz -= rz; }
      if (mx || mz) { var n = Math.hypot(mx, mz); walker.x += mx / n * sp; walker.z += mz / n * sp; collide(); moving = true; }
      camera.position.set(walker.x, walker.level * P.H + 1.6, walker.z);
      camera.rotation.set(walker.pitch, walker.yaw, 0);
      if (moving || self.dirty) {
        var rm = roomAt();
        if (hud) hud.textContent = rm ? (rm.name + (rm.isHall || rm.isStair ? '' : ' · ' + rm.area.toFixed(1) + ' m²')) : 'Exterior';
      }
    } else {
      if (orbit.auto && !reduce) { orbit.theta += dt * 0.12; moving = true; }
      var tg = orbit.target, y = self.mode === 'maqueta' ? (self.cutLevel + 0.5) * P.H : tg.y;
      camera.position.set(tg.x + orbit.r * Math.sin(orbit.phi) * Math.sin(orbit.theta), y + orbit.r * Math.cos(orbit.phi), tg.z + orbit.r * Math.sin(orbit.phi) * Math.cos(orbit.theta));
      camera.lookAt(tg.x, y, tg.z);
    }
    if (moving || self.dirty) { renderer.render(scene, camera); self.dirty = false; }
  }
  requestAnimationFrame(frame);
}

</script>
<script>
/* ============================================================
   INTERFAZ: formulario, generación, planos, materiales, contacto
   ============================================================ */
(function () {
  var $ = function (s, r) { return (r || document).querySelector(s); };
  var $$ = function (s, r) { return Array.prototype.slice.call((r || document).querySelectorAll(s)); };
  var money = new Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN', maximumFractionDigits: 0 });
  var num1 = new Intl.NumberFormat('es-MX', { maximumFractionDigits: 1 });
  var num0 = new Intl.NumberFormat('es-MX', { maximumFractionDigits: 0 });
  var mm = function (v) { return '$' + (v / 1e6).toLocaleString('es-MX', { maximumFractionDigits: 2, minimumFractionDigits: 2 }) + ' M'; };

  /* ---- medición: eventos para Meta Pixel / Google Tag cuando la página viva en tu dominio ---- */
  function track(name, data) {
    data = data || {};
    try { (window.dataLayer = window.dataLayer || []).push(Object.assign({ event: name }, data)); } catch (e) {}
    try { if (window.fbq) window.fbq('trackCustom', name, data); } catch (e) {}
  }

  var form = $('#cfg');
  var viewer = null, project = null, generated = false, touched = {};
  var FIELDS = ['tipo', 'terreno-medidas', 'terreno', 'niveles', 'programa', 'acabado', 'presupuesto', 'inicio'];

  function readInp() {
    var v = function (n) { return form.elements[n].value; };
    return {
      tipo: v('tipo'), frente: clamp(parseFloat(v('frente')) || 10, 6, 40), fondo: clamp(parseFloat(v('fondo')) || 20, 10, 60),
      terreno: v('terreno'), niveles: parseInt(v('niveles'), 10), recamaras: parseInt(v('recamaras'), 10), giro: v('giro'),
      acabado: v('acabado'), presupuesto: parseInt(v('presupuesto'), 10), inicio: v('inicio')
    };
  }

  function syncForm() {
    var inp = readInp();
    $('#area-terreno').textContent = num0.format(inp.frente * inp.fondo) + ' m²';
    $('#presupuesto-out').textContent = money.format(inp.presupuesto);
    $('#fs-recamaras').hidden = inp.tipo !== 'casa';
    $('#fs-giro').hidden = inp.tipo !== 'negocio';
    $$('.acab-precio').forEach(function (el) {
      el.textContent = money.format(CONFIG.costoM2[el.dataset.k]) + '/m²';
    });
    var area = inp.presupuesto * (1 - CONFIG.reservaImprevistos) / CONFIG.costoM2[inp.acabado];
    $('#presupuesto-hint').textContent = 'Alcanza para unos ' + num0.format(area) + ' m² en acabado ' + ACABADOS[inp.acabado].nombre + ', con 5 % reservado para imprevistos.';
    var n = Object.keys(touched).length, total = FIELDS.length;
    $('#prog-bar').style.width = Math.round(n / total * 100) + '%';
    $('#prog-txt').textContent = n >= total ? 'Listo: ya puedes generar tu prototipo' : 'Revisaste ' + n + ' de ' + total + ' datos';
  }

  form.addEventListener('input', function (e) {
    var f = e.target.closest('[data-field]');
    if (f && !touched[f.dataset.field]) { touched[f.dataset.field] = 1; track('configurador_campo', { campo: f.dataset.field, n: Object.keys(touched).length }); }
    syncForm();
    if (generated) { $('#gen-btn').textContent = 'Actualizar mi prototipo'; $('#res-state').textContent = 'Cambiaste datos: actualiza para verlos'; $('#res-state').className = 'pill pill-warn'; }
  });

  /* ---- generación con trabajo visible ---- */
  var reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  form.addEventListener('submit', function (e) {
    e.preventDefault();
    var inp = readInp();
    track('configurador_generar', { tipo: inp.tipo, niveles: inp.niveles, acabado: inp.acabado, presupuesto: inp.presupuesto });
    var steps = [
      'Leyendo tu terreno de ' + num1.format(inp.frente) + ' × ' + num1.format(inp.fondo) + ' m y sus retiros',
      inp.tipo === 'casa' ? 'Distribuyendo ' + inp.recamaras + (inp.recamaras === 1 ? ' recámara' : ' recámaras') + ' en ' + inp.niveles + (inp.niveles === 1 ? ' nivel' : ' niveles') : 'Distribuyendo tu negocio en ' + inp.niveles + (inp.niveles === 1 ? ' nivel' : ' niveles'),
      'Levantando muros, losas y fachada en 3D',
      'Cuantificando block, cemento, acero y acabados',
      'Comparando el costo contra tu presupuesto'
    ];
    var ov = $('#gen-overlay'), list = $('#gen-steps');
    list.innerHTML = steps.map(function (s) { return '<li>' + s + '</li>'; }).join('');
    ov.hidden = false;
    var items = $$('li', list), i = 0, delay = reduce ? 80 : 620;
    (function next() {
      if (i > 0) items[i - 1].className = 'done';
      if (i < items.length) { items[i].className = 'doing'; i++; setTimeout(next, delay); }
      else setTimeout(function () { ov.hidden = true; render(inp, true); }, reduce ? 50 : 300);
    })();
  });

  function render(inp, byUser) {
    project = buildProject(inp);
    generated = generated || byUser;
    var c = project.cost, q = project.quant;
    $('#gen-btn').textContent = 'Generar mi prototipo';
    $('#res-state').textContent = byUser ? 'Tu prototipo' : 'Prototipo de ejemplo';
    $('#res-state').className = byUser ? 'pill pill-ok' : 'pill';
    $('#k-area').textContent = num0.format(q.builtArea);
    $('#k-costo').textContent = mm(c.total);
    $('#k-niveles').textContent = project.N + (project.N === 1 ? ' nivel' : ' niveles');
    $('#k-huella').textContent = num1.format(project.W) + ' × ' + num1.format(project.L) + ' m';
    var st = $('#k-status');
    var pct = Math.round(c.ratio * 100);
    st.className = 'status status-' + c.status;
    st.innerHTML = c.status === 'ok' ? '<b>Dentro de tu presupuesto</b><span>Usa el ' + pct + ' % de ' + mm(inp.presupuesto) + '</span>'
      : c.status === 'warn' ? '<b>Justo en el límite</b><span>' + pct + ' % de tu presupuesto</span>'
      : '<b>Excede tu presupuesto</b><span>' + pct + ' % de ' + mm(inp.presupuesto) + '</span>';
    renderAdvice(inp);
    renderPlan();
    renderMaterials();
    renderCost(inp);
    renderCTA(inp);
    if (viewer && viewer.ok) {
      try { viewer.build(project); } catch (err) { showViewerError(err); }
      updateLevelChips();
    }
    if (byUser) {
      track('configurador_resultado', { estado: c.status, m2: Math.round(q.builtArea), score: leadScore(inp) });
      var scr = $('#resultado').closest('.pg-scroll');
      if (scr) scr.scrollTop = 0;
      else $('#resultado').scrollIntoView({ behavior: reduce ? 'auto' : 'smooth', block: 'start' });
    }
  }

  function renderAdvice(inp) {
    var c = project.cost, msgs = [];
    if (c.status === 'bad' || c.status === 'warn') {
      if (c.stage1 && c.stage1 <= inp.presupuesto) msgs.push('<b>Construye por etapas.</b> La planta baja habitable, con estructura lista para crecer, cuesta cerca de ' + mm(c.stage1) + '.');
      if (inp.acabado !== 'esencial' && c.esencial <= inp.presupuesto * 1.02) msgs.push('<b>Ajusta acabados.</b> Con acabado Esencial el mismo proyecto queda en ' + mm(c.esencial) + '.');
      if (inp.tipo === 'casa' && inp.recamaras > 1) msgs.push('<b>Reduce el programa.</b> Una recámara menos baja el costo alrededor de ' + mm(13 * project.costM2) + '.');
    }
    if (project.landLimited) msgs.push('<b>Tu terreno marca el límite.</b> El área se ajustó a lo que cabe con retiros de ' + project.sf + ' m al frente y ' + project.sb + ' m al fondo. Un nivel más aprovecharía mejor tu presupuesto.');
    else if (c.ratio < 0.8) msgs.push('<b>Te sobra margen.</b> Puedes subir acabados o ampliar espacios; lo vemos con el arquitecto.');
    if (project.s < 0.92 && !project.landLimited && c.status !== 'ok') msgs.push('Para este programa las piezas quedan en su tamaño mínimo cómodo.');
    var box = $('#advice');
    box.innerHTML = msgs.map(function (m) { return '<p>' + m + '</p>'; }).join('');
    box.hidden = !msgs.length;
  }

  /* ---- plano arquitectónico en SVG ---- */
  var GROUP_FILL = { social: '#EEF1F7', priv: '#F4F1EA', bath: '#E8F0F0', serv: '#EFEFEC', circ: '#FAFAF8', open: '#EDF2E6' };
  function renderPlan() {
    var P = project, F = P.inp.frente, D = P.inp.fondo, sf = P.sf;
    var html = '';
    P.levels.forEach(function (lv, k) {
      var Y = function (y) { return (D - sf) - y; };
      var vb = [-1.4, -1.0, F + 2.8, D + 3.6].map(function (v) { return v.toFixed(2); }).join(' ');
      var s = '<svg viewBox="' + vb + '" role="img" aria-label="Planta ' + levelName(k) + '" class="plan-svg">';
      s += '<rect x="0" y="0" width="' + F + '" height="' + D + '" class="lot"/>';
      if (k === 0) {
        s += '<text x="' + (F / 2) + '" y="' + (D + 1.3) + '" class="pl-cota" text-anchor="middle">CALLE · frente ' + num1.format(F) + ' m</text>';
        s += '<text x="' + (F + 0.6) + '" y="' + (D / 2) + '" class="pl-cota" transform="rotate(90 ' + (F + 0.6) + ' ' + (D / 2) + ')" text-anchor="middle">fondo ' + num1.format(D) + ' m</text>';
        s += '<text x="' + (Math.min(F, P.W) / 2) + '" y="' + (Y(0) + sf / 2 + 0.15) + '" class="pl-small" text-anchor="middle">retiro ' + sf + ' m · cochera</text>';
      }
      lv.rooms.forEach(function (r) {
        s += '<rect x="' + r.x0 + '" y="' + Y(r.y1) + '" width="' + r.w + '" height="' + r.h + '" fill="' + (GROUP_FILL[r.group] || '#fff') + '"/>';
        if (r.isStair) {
          for (var i = 1; i < 9; i++) {
            var xs = r.x0 + i * (r.w - 1.0) / 9;
            s += '<line x1="' + xs + '" y1="' + Y(r.y0 + 0.05) + '" x2="' + xs + '" y2="' + Y(r.y0 + r.h / 2 - 0.05) + '" class="pl-step"/>';
            s += '<line x1="' + xs + '" y1="' + Y(r.y0 + r.h / 2 + 0.05) + '" x2="' + xs + '" y2="' + Y(r.y1 - 0.05) + '" class="pl-step"/>';
          }
        }
      });
      lv.segs.forEach(function (sg) {
        if (sg.omit) return;
        var pt = function (t) { return sg.axis === 'h' ? [sg.s0 + t, Y(sg.c)] : [sg.c, Y(sg.s0 + t)]; };
        var cur = 0;
        var line = function (t0, t1, cls) { var a = pt(t0), b = pt(t1); s += '<line x1="' + a[0] + '" y1="' + a[1] + '" x2="' + b[0] + '" y2="' + b[1] + '" class="' + cls + '"/>'; };
        sg.openings.forEach(function (o) {
          if (o.t0 > cur) line(cur, o.t0, sg.low ? 'pl-wall low' : 'pl-wall');
          if (o.kind === 'window' || o.kind === 'glass') {
            if (o.bottom > 0.01) line(o.t0, o.t1, 'pl-win');
            else line(o.t0, o.t1, 'pl-win');
          }
          if (o.kind === 'door' || o.kind === 'entry') {
            var a = pt(o.t0), w = o.t1 - o.t0, b = pt(o.t1);
            var dir = sg.axis === 'h' ? [0, -w] : [w, 0];
            s += '<path d="M' + a[0] + ' ' + a[1] + ' l' + dir[0] + ' ' + dir[1] + ' A' + w + ' ' + w + ' 0 0 ' + (sg.axis === 'h' ? 1 : 0) + ' ' + b[0] + ' ' + b[1] + '" class="pl-door"/>';
          }
          cur = Math.max(cur, o.t1);
        });
        if (cur < sg.len) line(cur, sg.len, sg.low ? 'pl-wall low' : 'pl-wall');
      });
      lv.rooms.forEach(function (r) {
        if (r.isStair) return;
        var cx = r.x0 + r.w / 2, cy = Y(r.y0 + r.h / 2);
        var label = r.name;
        if (r.w < 3.2 && label.length > 9) label = label.replace('Baño principal', 'Baño ppal.').replace('Recámara principal', 'Rec. principal').replace('Recámara de visitas', 'Rec. visitas').replace('Medio baño', '½ baño').replace('Baño completo', 'Baño').replace('Lavandería', 'Lavand.').replace('Estar familiar', 'Estar').replace('Recepción y espera', 'Recepción');
        var fs = clamp(Math.min(0.34, (r.w - 0.3) / (label.length * 0.62)), 0.13, 0.34);
        s += '<text x="' + cx + '" y="' + (cy - 0.05) + '" class="pl-name" style="font-size:' + fs + 'px" text-anchor="middle">' + label + '</text>';
        if (!r.isHall) s += '<text x="' + cx + '" y="' + (cy + fs + 0.1) + '" class="pl-area" style="font-size:' + (fs * 0.85) + 'px" text-anchor="middle">' + num1.format(r.area) + ' m²</text>';
      });
      if (k === 0 && lv.entrance) s += '<path d="M' + lv.entrance.x + ' ' + (Y(0) + 0.9) + ' l0 -0.7 m-0.22 0.25 l0.22 -0.25 l0.22 0.25" class="pl-arrow"/>';
      s += '<line x1="0" y1="' + (Y(0) + 0.45) + '" x2="' + P.W + '" y2="' + (Y(0) + 0.45) + '" class="pl-dim"/>';
      s += '<text x="' + (P.W / 2) + '" y="' + (Y(0) + 0.38) + '" class="pl-small" text-anchor="middle">' + num1.format(P.W) + ' m</text>';
      s += '</svg>';
      html += '<figure class="plan-fig"><figcaption>' + levelName(k) + '</figcaption>' + s + '</figure>';
    });
    $('#plan-wrap').innerHTML = html;
  }
  function levelName(k) { return ['Planta baja', 'Planta alta', 'Tercer nivel'][k] || ('Nivel ' + (k + 1)); }

  /* ---- materiales ---- */
  function renderMaterials() {
    var q = project.quant;
    var rows = [
      ['Concreto f′c 200 (cimentación, losas, castillos y cadenas)', q.concrete, 'm³', 1],
      ['Acero de refuerzo', q.steelKg / 1000, 'toneladas', 2],
      ['Block 15 × 20 × 40', q.blocks, 'piezas', 0],
      ['Cemento gris', q.cement, 'bultos de 50 kg', 0],
      ['Arena', q.sand, 'm³', 1],
      ['Grava', q.gravel, 'm³', 1],
      ['Piso (porcelanato, cerámico o madera según pieza)', q.floorFinish, 'm² con 8 % de merma', 0],
      ['Pintura vinílica, dos manos', q.paintL / 19, 'cubetas de 19 L', 0],
      ['Impermeabilizante', q.waterproof, 'm²', 0],
      ['Cancelería y vidrio', q.windowArea, 'm²', 1],
      ['Puertas', q.doors, 'piezas', 0],
      ['Baños completos / medios baños', q.baths + ' / ' + q.halfBaths, 'juegos', -1],
      ['Salidas eléctricas', q.outlets, 'salidas', 0]
    ];
    $('#mat-body').innerHTML = rows.map(function (r) {
      var v = r[3] < 0 ? r[1] : r[1].toLocaleString('es-MX', { maximumFractionDigits: r[3], minimumFractionDigits: r[3] });
      return '<tr><td>' + r[0] + '</td><td class="num">' + v + '</td><td>' + r[2] + '</td></tr>';
    }).join('');
    $('#mat-note').textContent = 'Cuantificado sobre el modelo: ' + num0.format(q.wallLen) + ' m lineales de muro, ' + num0.format(q.wallArea) + ' m² de muro neto y ' + num0.format(q.slabArea) + ' m² de losa. Es una estimación paramétrica de ±15 %; la explosión de insumos exacta se entrega con el proyecto ejecutivo.';
  }

  /* ---- presupuesto por partidas ---- */
  function renderCost(inp) {
    var c = project.cost, max = Math.max.apply(null, c.parts.map(function (p) { return p.amount; }));
    $('#cost-body').innerHTML = c.parts.map(function (p) {
      return '<div class="bar-row"><span class="bar-name">' + p.name + '</span><span class="bar-track"><span class="bar-fill" style="width:' + (p.amount / max * 100).toFixed(1) + '%"></span></span><span class="bar-val num">' + money.format(Math.round(p.amount / 1000) * 1000) + '</span></div>';
    }).join('');
    var used = clamp(c.total / inp.presupuesto, 0, 1.5);
    $('#meter-fill').style.width = (Math.min(used, 1) * 100).toFixed(1) + '%';
    $('#meter-fill').className = 'meter-fill m-' + c.status;
    $('#meter-over').style.width = used > 1 ? ((used - 1) / 0.5 * 33).toFixed(1) + '%' : '0';
    $('#cost-total').textContent = money.format(Math.round(c.total / 1000) * 1000);
    $('#cost-m2').textContent = money.format(project.costM2) + ' por m² · ' + num0.format(project.quant.builtArea) + ' m²';
    $('#cost-budget').textContent = money.format(inp.presupuesto);
  }

  /* ---- contacto con folio y calificación A/B/C ---- */
  function renderCTA(inp) {
    var P = project, q = P.quant, sc = leadScore(inp);
    var folio = 'LIB-' + Date.now().toString(36).slice(-5).toUpperCase() + '-' + sc;
    var desc = inp.tipo === 'casa'
      ? 'Casa · ' + P.N + (P.N === 1 ? ' nivel' : ' niveles') + ' · ' + inp.recamaras + (inp.recamaras === 1 ? ' recámara' : ' recámaras')
      : 'Negocio (' + { local: 'local comercial', consultorio: 'consultorios', restaurante: 'restaurante o café' }[inp.giro] + ') · ' + P.N + (P.N === 1 ? ' nivel' : ' niveles');
    var inicio = { '0-3': 'en menos de 3 meses', '3-6': 'en 3 a 6 meses', '6-12': 'en 6 a 12 meses', 'explorando': 'todavía explorando' }[inp.inicio];
    var msg = 'Hola, generé mi prototipo en la página de ' + CONFIG.estudio + ':\n'
      + '• ' + desc + ' · acabado ' + ACABADOS[inp.acabado].nombre + '\n'
      + '• Terreno ' + num1.format(inp.frente) + ' × ' + num1.format(inp.fondo) + ' m' + (inp.terreno === 'si' ? ' (ya lo tengo)' : ' (aún no tengo terreno)') + '\n'
      + '• ' + num0.format(q.builtArea) + ' m² · estimado ' + money.format(Math.round(P.cost.total / 1000) * 1000) + '\n'
      + '• Mi presupuesto: ' + money.format(inp.presupuesto) + ' · quiero iniciar ' + inicio + '\n'
      + 'Folio ' + folio + '\n'
      + 'Quiero que diseñen mi proyecto con recorrido virtual.';
    var a = $('#cta-wa');
    a.href = 'https://wa.me/' + CONFIG.whatsapp + '?text=' + encodeURIComponent(msg);
    a.dataset.score = sc;
    $('#cta-folio').textContent = 'Folio ' + folio;
    var inm = $('#cta-inm');
    inm.hidden = inp.terreno === 'si';
    $('#cta-inm-a').href = 'https://wa.me/' + CONFIG.whatsappInmobiliaria + '?text=' + encodeURIComponent('Hola, busco terreno de unos ' + num1.format(inp.frente) + ' × ' + num1.format(inp.fondo) + ' m en Tepic o Xalisco para construir. Folio ' + folio);
    $('#wa-num').textContent = '+' + CONFIG.whatsapp;
  }
  $('#cta-wa').addEventListener('click', function (e) { track('cta_whatsapp', { score: e.currentTarget.dataset.score }); });
  $('#cta-inm-a').addEventListener('click', function () { track('cta_inmobiliaria', {}); });

  /* ---- pestañas de resultados ---- */
  $$('.tab').forEach(function (b) {
    b.addEventListener('click', function () {
      $$('.tab').forEach(function (x) { x.setAttribute('aria-selected', x === b ? 'true' : 'false'); });
      $$('.tabpanel').forEach(function (p) { p.hidden = p.id !== b.getAttribute('aria-controls'); });
      track('resultado_pestana', { pestana: b.dataset.t });
      if (viewer && b.dataset.t === '3d') viewer.dirty = true;
    });
  });

  /* ---- visor ---- */
  function showViewerError(err) {
    $('#viewer-msg').hidden = false;
    $('#viewer-msg').textContent = 'El visor 3D no pudo cargar en este navegador. Revisa el plano y los materiales en las otras pestañas.';
    if (err && window.console) console.error(err);
  }
  function updateLevelChips() {
    var box = $('#lvl-chips');
    if (!project) return;
    box.innerHTML = project.levels.map(function (l, k) { return '<button type="button" class="chip" data-k="' + k + '">' + levelName(k) + '</button>'; }).join('');
    $$('.chip', box).forEach(function (b) {
      b.addEventListener('click', function () {
        var k = parseInt(b.dataset.k, 10);
        if (viewer.mode === 'walk') viewer.goLevel(k); else viewer.setMode('maqueta', k);
        markMode();
      });
    });
    markMode();
  }
  function markMode() {
    if (!viewer || !viewer.ok) return;
    $$('.vmode').forEach(function (b) { b.setAttribute('aria-pressed', b.dataset.m === viewer.mode ? 'true' : 'false'); });
    $('#lvl-chips').hidden = viewer.mode === 'exterior';
    $('#walk-ui').hidden = viewer.mode !== 'walk';
    $('#v-help').textContent = viewer.mode === 'walk' ? 'W A S D o flechas para caminar · arrastra para mirar' : 'Arrastra para girar · rueda o pellizco para acercar';
  }
  function initViewer() {
    viewer = new Viewer3D($('#viewer'), $('#viewer-canvas'), $('#walk-room'));
    if (!viewer.ok) { showViewerError(); return; }
    $$('.vmode').forEach(function (b) {
      b.addEventListener('click', function () {
        var m = b.dataset.m;
        viewer.setMode(m, m === 'maqueta' ? 0 : 0);
        track('visor_modo', { modo: m });
        markMode();
        if (m === 'walk') $('#viewer').focus();
      });
    });
    $$('[data-key]').forEach(function (b) {
      var k = b.dataset.key;
      var on = function (e) { e.preventDefault(); viewer.press(k, true); };
      var off = function () { viewer.press(k, false); };
      b.addEventListener('pointerdown', on); b.addEventListener('pointerup', off); b.addEventListener('pointerleave', off); b.addEventListener('pointercancel', off);
    });
    $('#v-full').addEventListener('click', function () {
      var el = $('#viewer');
      try {
        if (document.fullscreenElement) document.exitFullscreen();
        else if (el.requestFullscreen) el.requestFullscreen().catch(function () {});
      } catch (e) {}
    });
  }

  /* ---- comparador render / obra ---- */
  var cmp = $('#cmp-range');
  if (cmp) cmp.addEventListener('input', function () { $('#cmp-top').style.clipPath = 'inset(0 ' + (100 - cmp.value) + '% 0 0)'; $('#cmp-line').style.left = cmp.value + '%'; });

  /* ---- arranque: abre con un ejemplo real, sin esperar ---- */
  syncForm();
  initViewer();
  if (viewer && viewer.ok && typeof window.onCoverRender === 'function') {
    try {
      viewer.build(buildProject({ tipo: 'casa', niveles: 2, recamaras: 3, giro: 'local', frente: 12, fondo: 24, acabado: 'premium', presupuesto: 7500000, terreno: 'si', inicio: '3-6' }));
      window.onCoverRender(viewer.snapshot(900, 1200));
    } catch (err) { if (window.console) console.error(err); }
  }
  render(readInp(), false);
  track('configurador_visto', {});
})();

</script>
</body>
</html>
