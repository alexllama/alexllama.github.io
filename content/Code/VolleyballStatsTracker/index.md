---
title: "Volleyball Stats Tracker"
draft: false
date: 2026-04-12
description: "Volleyball Stats Tracker"
tags: ["volleyball", "tracker"]
showHero: false
---

<style>
.vb-app-box {
max-width: 550px;
margin: 0 auto;
background-color: #121212;
color: #ffffff;
font-family: sans-serif;
border-radius: 8px;
box-shadow: 0 10px 30px rgba(0,0,0,0.5);
overflow: hidden;
}
.vb-app-header {
position: sticky;
top: 0;
background: #1e1e1e;
padding: 12px 15px;
z-index: 50;
border-bottom: 2px solid #3498db;
display: flex;
justify-content: space-between;
align-items: center;
}
.vb-app-header h2 { margin: 0 !important; font-size: 1.1rem !important; color: #3498db !important; border: none !important; }
.vb-app-set-pill { font-weight: bold; background: #3498db; padding: 4px 10px; border-radius: 4px; color: white; }
.vb-app-body { padding: 15px; }
.vb-app-input-group {
background: #1e1e1e;
padding: 10px;
border-radius: 6px;
margin-bottom: 15px;
}
.vb-app-body input {
width: 100%;
padding: 12px;
margin: 4px 0 8px 0;
background: #2c2c2c;
border: 1px solid #444;
color: white;
border-radius: 4px;
box-sizing: border-box;
font-size: 16px;
}
.vb-app-grid {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 10px;
margin-bottom: 20px;
}
.vb-app-stat-card {
background: #2c2c2c;
padding: 12px;
border-radius: 6px;
text-align: center;
border-left: 4px solid #95a5a6;
}
.vb-app-stat-card.vb-hl { border-left-color: #27ae60; }
.vb-app-stat-card.vb-std { border-left-color: #3498db; }
.vb-app-label { font-size: 0.7rem; text-transform: uppercase; color: #bbb; display: block; margin-bottom: 4px; }
.vb-app-val { font-size: 1.8rem; font-weight: bold; margin: 4px 0; color: #fff; }
.vb-app-btns { display: flex; gap: 8px; }

/* Perfect centering for + and - */
.vb-app-box button {
flex: 1;
height: 55px; /* Fixed height for consistent hit area */
border: none;
border-radius: 4px;
font-weight: bold;
color: white;
font-size: 1.8rem;
cursor: pointer;
display: flex;
align-items: center;
justify-content: center;
line-height: 0;
padding: 0;
}

.vb-app-plus { background-color: #27ae60; }
.vb-app-minus { background-color: #e74c3c; opacity: 0.7; }

/* Wide utility buttons */
.vb-app-wide { 
width: 100%; 
margin-top: 10px; 
height: 60px !important; 
font-size: 1.1rem !important; 
}
.vb-app-next { background-color: #3498db; }
.vb-app-reset { background-color: #444; }
.vb-app-danger { background-color: transparent; border: 1px solid #e74c3c; color: #e74c3c; margin-top: 30px; margin-bottom: 40px; }
</style>

<div class="vb-app-box">
<div class="vb-app-header">
<div>
<h2 id="v-disp-n">Player Name</h2>
<span id="v-disp-t" style="font-size: 0.8rem; color: #aaa;">Team vs Opponent</span>
</div>
<div class="vb-app-set-pill">SET <span id="v-disp-s">1</span></div>
</div>
<div class="vb-app-body">
<div class="vb-app-input-group">
<input type="text" id="v-in-n" placeholder="Player Name" oninput="window.vbS()">
<input type="text" id="v-in-t" placeholder="Player Team" oninput="window.vbS()">
<input type="text" id="v-in-o" placeholder="Opponent" oninput="window.vbS()">
<div style="display: flex; gap: 8px;">
<input type="date" id="v-in-d" onchange="window.vbS()">
<input type="text" id="v-in-v" placeholder="Venue" oninput="window.vbS()">
</div>
</div>
<div class="vb-app-grid" id="vb-grid-target"></div>
<button class="vb-app-wide vb-app-next" onclick="window.vbNext()">Next Set (Clear Stats)</button>
<button class="vb-app-wide vb-app-reset" onclick="window.vbResS()">Reset Set</button>
<button class="vb-app-wide vb-app-danger" onclick="window.vbFull()">Full Reset Page</button>
</div>
</div>

<script>
(function() {
let stats = { blocks: 0, ace: 0, freeball: 0, dump: 0, kill: 0, serve: 0, push: 0, points: 0 };
let set = 1;
const labels = { blocks: "Blocks", ace: "Ace", freeball: "Free Ball", dump: "Dump", kill: "Kill", serve: "Serve", push: "Push", points: "Points Scored" };

window.vbS = function() {
const nEl = document.getElementById('v-in-n');
const tEl = document.getElementById('v-in-t');
const oEl = document.getElementById('v-in-o');
const dEl = document.getElementById('v-in-d');
const vEl = document.getElementById('v-in-v');
if(nEl) document.getElementById('v-disp-n').innerText = nEl.value || "Player Name";
if(tEl && oEl) document.getElementById('v-disp-t').innerText = (tEl.value || 'Team') + ' vs ' + (oEl.value || 'Opp');
document.getElementById('v-disp-s').innerText = set;
localStorage.setItem('vb_final_v6', JSON.stringify({
stats, set, meta: {
n: nEl ? nEl.value : "",
t: tEl ? tEl.value : "",
o: oEl ? oEl.value : "",
d: dEl ? dEl.value : "",
v: vEl ? vEl.value : ""
}
}));
};

window.vbR = function() {
const g = document.getElementById('vb-grid-target');
if(!g) return;
g.innerHTML = '';
for (const [k, v] of Object.entries(stats)) {
const isP = (k === 'ace' || k === 'kill' || k === 'points');
const d = document.createElement('div');
d.className = 'vb-app-stat-card ' + (isP ? 'vb-hl' : 'vb-std');
d.innerHTML = '<span class="vb-app-label">' + labels[k] + '</span><div class="vb-app-val">' + v + '</div>' +
'<div class="vb-app-btns">' +
'<button class="vb-app-minus" onclick="window.vbC(\'' + k + '\', -1)"><span>−</span></button>' +
'<button class="vb-app-plus" onclick="window.vbC(\'' + k + '\', 1)"><span>+</span></button>' +
'</div>';
g.appendChild(d);
}
};

window.vbC = function(k, a) {
stats[k] = Math.max(0, stats[k] + a);
if (a > 0 && (k === 'ace' || k === 'kill')) stats.points++;
window.vbS(); window.vbR();
};

window.vbNext = function() {
if (set < 3) { set++; for (let k in stats) stats[k] = 0; window.vbS(); window.vbR(); window.scrollTo(0,0); }
};

window.vbResS = function() {
if(confirm("Reset current set?")) { for (let k in stats) stats[k] = 0; window.vbS(); window.vbR(); }
};

window.vbFull = function() {
if(confirm("Full Reset? This wipes EVERYTHING.")) {
localStorage.removeItem('vb_final_v6');
const ids = ['v-in-n', 'v-in-t', 'v-in-o', 'v-in-d', 'v-in-v'];
ids.forEach(id => { const el = document.getElementById(id); if(el) el.value = ""; });
set = 1;
for (let k in stats) stats[k] = 0;
window.vbS(); 
location.reload();
}
};

const stored = localStorage.getItem('vb_final_v6');
if (stored) {
const d = JSON.parse(stored);
stats = d.stats; set = d.set;
if(document.getElementById('v-in-n')) document.getElementById('v-in-n').value = d.meta.n || "";
if(document.getElementById('v-in-t')) document.getElementById('v-in-t').value = d.meta.t || "";
if(document.getElementById('v-in-o')) document.getElementById('v-in-o').value = d.meta.o || "";
if(document.getElementById('v-in-d')) document.getElementById('v-in-d').value = d.meta.d || "";
if(document.getElementById('v-in-v')) document.getElementById('v-in-v').value = d.meta.v || "";
}
window.vbR(); window.vbS();
})();
</script>