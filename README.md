[index-3.html](https://github.com/user-attachments/files/34240318/index-3.html)
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Лига пенальти</title>
<style>
:root{--bg:#eef3ea;--fg:#16210f;--card:#fff;--ac:#1f9d3a;--mut:#8a9585;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#111611;--fg:#eaf2e6;--card:#1b231a;--ac:#3ec45a}}
:root[data-theme="dark"]{--bg:#111611;--fg:#eaf2e6;--card:#1b231a;--ac:#3ec45a}
[hidden]{display:none!important}
html,body{margin:0;background:var(--bg);color:var(--fg);font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif}
.wrap{max-width:820px;margin:0 auto;padding:12px}
h1{font-size:22px;margin:4px 0 10px}
button{background:var(--ac);color:#fff;border:0;border-radius:10px;padding:12px 20px;font-size:16px;font-weight:600;cursor:pointer}
button.alt{background:var(--card);color:var(--fg);border:1px solid var(--mut)}
button:active{transform:scale(.97)}
.row{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;margin:10px 0}
#teams{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:8px}
#teams button{background:var(--card);color:var(--fg);display:flex;align-items:center;gap:8px;text-align:left;font-size:15px;border:1px solid var(--mut)}
.dot{display:inline-block;width:14px;height:14px;border-radius:50%;border:1px solid #0006;flex:none}
#bInfo{text-align:center;font-size:17px;font-weight:700;margin:6px 0}
#bwrap{overflow-x:auto}
#bracket{display:flex;gap:12px;min-width:820px}
.col{flex:1;display:flex;flex-direction:column;justify-content:space-around;gap:8px}
.col h3{margin:0;text-align:center;font-size:14px;color:var(--mut)}
.mt{background:var(--card);border-radius:8px;padding:4px 6px}
.tr{display:flex;align-items:center;gap:6px;font-size:13px;padding:3px 2px;opacity:.55}
.tr span{flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tr.w{opacity:1;font-weight:700}
.tr.me{color:var(--ac)}
#hud{display:flex;justify-content:space-between;align-items:center;background:var(--card);border-radius:12px;padding:10px 14px;gap:8px}
#title{font-size:13px;color:var(--mut)}
#score{font-size:19px;font-weight:700}
#dots{font-size:13px;letter-spacing:1px;text-align:right;line-height:1.4}
canvas{width:100%;display:block;border-radius:12px;margin:10px 0;touch-action:none;cursor:crosshair}
#msg{min-height:28px;text-align:center;font-size:18px;font-weight:700}
small{display:block;text-align:center;opacity:.7;margin-top:8px}
.tw{max-height:430px;overflow:auto;background:var(--card);border-radius:10px}
table{width:100%;border-collapse:collapse;font-size:13px}
th{position:sticky;top:0;background:var(--card);color:var(--mut);text-align:left;padding:6px}
td{padding:5px 6px;border-top:1px solid #8884}
tr.q1 td:first-child{border-left:4px solid #2ecc71}tr.q2 td:first-child{border-left:4px solid #f1c40f}tr.q3 td:first-child{border-left:4px solid #e63946}
tr.me td{background:#2ecc7126;font-weight:700}
#shotUI label{font-size:15px}#pw{vertical-align:middle;width:150px}
#medals{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:8px;margin-top:8px}
.md{background:var(--card);border-radius:10px;padding:8px;text-align:center;opacity:.45;border:2px solid transparent}
.md div{font-size:30px}.md small{margin-top:2px}.md.on{opacity:1;border-color:#f1c40f}
#stats{font-size:14px;opacity:.8}h3.h{margin:16px 0 4px}
#toast{position:fixed;top:12px;left:50%;transform:translate(-50%,-80px);background:#f1c40f;color:#111;font-weight:700;padding:10px 16px;border-radius:10px;z-index:9;transition:transform .35s;max-width:90%;text-align:center}
#toast.on{transform:translate(-50%,0)}
</style>
</head>
<body>
<div id="toast"></div>
<div class="wrap">
<h1 style="display:flex;justify-content:space-between;align-items:center">🏆 Лига пенальти<button id="mute" class="alt" style="padding:6px 12px" aria-label="Звук">🔊</button></h1>

<section id="menu">
<p>Новый формат: общий этап из 8 туров (36 клубов, ты играешь все свои матчи). Топ-8 сразу в 1/8 финала, места 9–24 играют стыковые матчи, остальные вылетают. Дальше 1/8, четвертьфинал, полуфинал и финал с кубком.</p>
<div class="row" id="cont"></div>
<div id="teams"></div>
<h3 class="h">🏅 Коллекция достижений</h3><div id="stats"></div><div id="medals"></div>
</section>

<section id="lv" hidden>
<div id="lInfo" style="text-align:center;font-weight:700;margin:6px 0"></div>
<div class="tw"><table id="tbl"></table></div>
<div class="row"><button id="lGo"></button><button id="lMenu" class="alt" onclick="show('menu')">В меню</button></div>
</section>

<section id="bv" hidden>
<div id="bInfo"></div>
<div id="bwrap"><div id="bracket"></div></div>
<div class="row"><button id="goBtn"></button><button id="newBtn" class="alt">Сменить клуб</button></div>
</section>

<section id="gv" hidden>
<div id="hud"><div><div id="title"></div><div id="score"></div></div><div id="dots"></div></div>
<canvas id="c" width="800" height="500"></canvas>
<div id="msg"></div>
<div class="row" id="saveBtns">
<button data-z="0">← Влево</button><button data-z="1">↓ Центр</button><button data-z="2">Вправо →</button>
</div>
<div id="shotUI"><div class="row" id="types"></div><div class="row"><label>Сила: <input type="range" id="pw" min="40" max="100" value="70"> <b id="pwv">70</b>%</label></div></div>
<div class="row"><button id="contBtn" hidden>Дальше</button></div>
<small id="hint"></small>
</section>
</div>

<script>
const $=id=>document.getElementById(id);
const cv=$('c'),ctx=cv.getContext('2d');
const T=[["Реал Мадрид","#e8e8e8",.80],["Барселона","#a50044",.78],["Манчестер Сити","#6cabdd",.80],["Бавария","#dc052d",.78],
["ПСЖ","#004170",.76],["Ливерпуль","#c8102e",.77],["Арсенал","#ef0107",.77],["Интер","#0068a8",.75],
["Милан","#fb090b",.74],["Ювентус","#333333",.74],["Атлетико","#cb3524",.73],["Боруссия Д","#fde100",.73],
["Наполи","#12a0d7",.72],["Порту","#003f87",.71],["Бенфика","#e30613",.71],["Челси","#034694",.74],
["Манчестер Юнайтед","#da291c",.76],["Тоттенхэм","#132257",.74],["Ньюкасл","#241f20",.72],["Астон Вилла","#670e36",.72],
["Байер","#e32221",.76],["РБ Лейпциг","#dd0741",.73],["Рома","#8e1f2f",.72],["Лацио","#87d8f7",.70],
["Севилья","#f43333",.71],["Реал Сосьедад","#0067b1",.70],["Марсель","#2faee0",.70],["Лион","#1c3f94",.70],
["Спортинг","#008057",.72],["Аякс","#d2122e",.71],["Галатасарай","#fdb913",.71],["Фенербахче","#ffed00",.70],
["Селтик","#16973b",.69],["Црвена Звезда","#c8102e",.68],["Шахтёр","#f58220",.70],["Динамо Киев","#0057b8",.69],
["Зенит","#00a3e0",.72],["Спартак","#d71920",.69],["ЦСКА","#e4002b",.68],["Локомотив","#007a3d",.67],
["Краснодар","#1a8a3d",.69],["Динамо Москва","#1f4fa3",.66],["Динамо Минск","#1d5fbf",.66],["БАТЭ","#f4c20d",.66]];
const RN=['Стыковые матчи','1/8 финала','Четвертьфинал','Полуфинал','Финал'],RS=['Стык','1/8','1/4','1/2','Финал'],LAST=4;
const G={x1:200,x2:600,y1:90,y2:250},ZX=[267,400,533];
const dot=i=>`<i class="dot" style="background:${T[i][1]}"></i>`;
let me,R,round,alive,M,anim,aim,busy,cer,dtGlobal=0;

function show(id){['menu','lv','bv','gv'].forEach(x=>$(x).hidden=x!==id);if(id==='menu')updateCont()}
$('teams').innerHTML=T.map((t,i)=>`<button data-i="${i}">${dot(i)}${t[0]}</button>`).join('');
$('teams').onclick=e=>{const b=e.target.closest('button');if(b)startTour(+b.dataset.i)};
$('newBtn').onclick=()=>show('menu');

/* ---------- турнир ---------- */
function shuffle(a){for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a}
let LG,SEEDS;
const SK='pl2';
function saveG(){try{localStorage.setItem(SK,JSON.stringify({me,R,round,alive,LG,SEEDS}))}catch(e){}}
function loadG(){try{return JSON.parse(localStorage.getItem(SK))}catch(e){return null}}
function clearG(){try{localStorage.removeItem(SK)}catch(e){}}
const MK='pl_stats';
let ST={goals:0,saves:0,wins:0,cups:0,gs:0,ws:0,bgs:0,bws:0,medals:[]};
try{Object.assign(ST,JSON.parse(localStorage.getItem(MK))||{})}catch(e){}
const saveS=()=>{try{localStorage.setItem(MK,JSON.stringify(ST))}catch(e){}};
const MD=[{id:'b',i:'🥉',n:'Бронза',d:'10 голов',f:q=>q.goals>=10,p:q=>q.goals+'/10'},
{id:'s',i:'🥈',n:'Серебро',d:'50 голов',f:q=>q.goals>=50,p:q=>q.goals+'/50'},
{id:'g',i:'🥇',n:'Золото',d:'100 голов',f:q=>q.goals>=100,p:q=>q.goals+'/100'},
{id:'w',i:'🧱',n:'Стена',d:'10 отражённых ударов',f:q=>q.saves>=10,p:q=>q.saves+'/10'},
{id:'v',i:'🔥',n:'Победитель',d:'5 побед подряд',f:q=>q.bws>=5,p:q=>q.bws+'/5'},
{id:'n',i:'🎯',n:'Снайпер',d:'25 голов подряд',f:q=>q.bgs>=25,p:q=>q.bgs+'/25'},
{id:'c',i:'🏆',n:'Чемпион',d:'Выиграй кубок',f:q=>q.cups>=1,p:q=>q.cups+'/1'}];
let tq=0;
function toast(t){const el=$('toast');el.textContent=t;el.classList.add('on');clearTimeout(tq);tq=setTimeout(()=>el.classList.remove('on'),3500)}
function check(){ST.bgs=Math.max(ST.bgs,ST.gs);ST.bws=Math.max(ST.bws,ST.ws);
for(const m of MD)if(!ST.medals.includes(m.id)&&m.f(ST)){ST.medals.push(m.id);toast(m.i+' Награда: '+m.n+' ('+m.d+')')}
saveS()}
function renderMedals(){
$('stats').textContent='Забито: '+ST.goals+' · Отбито: '+ST.saves+' · Побед: '+ST.wins+' · Кубков: '+ST.cups;
$('medals').innerHTML=MD.map(m=>{const o=ST.medals.includes(m.id);return `<div class="md${o?' on':''}"><div>${m.i}</div><b>${m.n}</b><small>${m.d}</small><small>${o?'Получена!':m.p(ST)}</small></div>`}).join('')}
function updateCont(){
const g=loadG(),el=$('cont'),ok=g&&g.me!=null;
el.innerHTML=ok?'<button id="resume">▶ Продолжить: '+T[g.me][0]+'</button><button id="fresh" class="alt">Новая игра</button>':'';
if(ok){$('resume').onclick=()=>{({me,R,round,alive,LG,SEEDS}=g);R?showBracket():showLeague()};
$('fresh').onclick=()=>{if(confirm('Начать заново? Текущий турнир сбросится, награды и статистика останутся.')){clearG();updateCont()}}}
renderMedals();
}
const rgb=h=>[1,3,5].map(i=>parseInt(h.slice(i,i+2),16));
const cd=(a,b)=>{const A=rgb(a),B=rgb(b);return Math.hypot(A[0]-B[0],A[1]-B[1],A[2]-B[2])};
const awayK=h=>{const c=rgb(h);return (.3*c[0]+.59*c[1]+.11*c[2])/255>.55?'#1b2a49':'#f4f4f4'};
const GP=['#ff9f1c','#b6ff3b','#c77dff','#ff5d8f','#2ee6d6'];
const gkK=i=>{for(let k=0;k<5;k++){const c=GP[(i+k)%5];if(cd(c,T[i][1])>110)return c}return GP[0]};
function simShoot(a,b,n){n=n||5;let sa=0,sb=0;const ra=T[a][2],rb=T[b][2];
for(let i=0;i<n;i++){if(Math.random()<ra)sa++;if(Math.random()<rb)sb++}
while(sa===sb){if(Math.random()<ra)sa++;if(Math.random()<rb)sb++}
return{sa,sb,w:sa>sb?a:b}}
/* общий этап: 36 клубов, 8 туров */
function startTour(i){
me=i;alive=true;round=0;R=null;
const P=shuffle([me,...shuffle([...T.keys()].filter(x=>x!==me)).slice(0,35)]);
LG={P,st:{},day:0,opp:null};
P.forEach(t=>LG.st[t]={g:0,w:0,l:0,gf:0,ga:0,r:Math.random()});
nextDay();
}
function rec(a,b,sa,sb){const A=LG.st[a],B=LG.st[b];A.g++;B.g++;A.gf+=sa;A.ga+=sb;B.gf+=sb;B.ga+=sa;if(sa>sb){A.w++;B.l++}else{B.w++;A.l++}}
function nextDay(){
const o=shuffle([...LG.P]);
for(let k=0;k<36;k+=2){const a=o[k],b=o[k+1];
if(a===me||b===me){LG.opp=a===me?b:a;continue}
const r=simShoot(a,b,3);rec(a,b,r.sa,r.sb)}
saveG();showLeague();
}
const rank=()=>[...LG.P].sort((a,b)=>{const A=LG.st[a],B=LG.st[b];return B.w-A.w||(B.gf-B.ga)-(A.gf-A.ga)||B.gf-A.gf||B.r-A.r});
function showLeague(){
const rk=rank(),done=LG.day>=8,pos=rk.indexOf(me);
$('tbl').innerHTML='<tr><th>#</th><th>Клуб</th><th>И</th><th>В</th><th>П</th><th>Мячи</th><th>О</th></tr>'+rk.map((t,i)=>{const q=LG.st[t];
return `<tr class="${i<8?'q1':i<24?'q2':'q3'}${t===me?' me':''}"><td>${i+1}</td><td>${dot(t)} ${T[t][0]}</td><td>${q.g}</td><td>${q.w}</td><td>${q.l}</td><td>${q.gf}:${q.ga}</td><td><b>${q.w*3}</b></td></tr>`}).join('');
if(!done){$('lInfo').textContent='Общий этап: тур '+(LG.day+1)+' из 8. Ты на '+(pos+1)+' месте';
$('lGo').textContent='⚽ Играть: '+T[me][0]+' vs '+T[LG.opp][0];$('lGo').onclick=()=>startMatch(LG.opp)}
else{const m=pos<8?'Топ-8: сразу в 1/8 финала! 🔥':pos<24?'Стыковые матчи (9–24 места)':'Ты выбыл (25–36 места) 😔';
$('lInfo').textContent='Общий этап завершён: '+(pos+1)+' место. '+m;
$('lGo').textContent=pos<24?'Дальше':'Досмотреть турнир';$('lGo').onclick=()=>startKnock()}
show('lv');
}
function afterLeague(win){
rec(me,LG.opp,M.y,M.c);LG.day++;LG.opp=null;
if(LG.day<8)nextDay();else{saveG();showLeague()}
}
/* плей-офф */
function startKnock(){
const rk=rank(),pos=rk.indexOf(me),po=rk.slice(8,24);SEEDS=rk.slice(0,8);
R=[Array.from({length:8},(_,j)=>({a:po[j],b:po[15-j]})),Array.from({length:8},()=>({})),Array.from({length:4},()=>({})),Array.from({length:2},()=>({})),[{}]];
round=0;alive=pos<24;simRound();
if(alive&&pos<8&&!pend())advance();
if(!alive)while(round<LAST)advance();
showBracket();
}
function simRound(){for(const m of R[round]){
if(m.w!==undefined)continue;
if(alive&&(m.a===me||m.b===me))continue;
Object.assign(m,simShoot(m.a,m.b));}}
function advance(){
if(round===0){for(let k=0;k<8;k++)R[1][k]={a:SEEDS[k],b:R[0][7-k].w}}
else for(let k=0;k<R[round+1].length;k++)R[round+1][k]={a:R[round][2*k].w,b:R[round][2*k+1].w};
round++;simRound()}
function pend(){return R[round].find(m=>m.w===undefined&&(m.a===me||m.b===me))}
function row(m,k){const t=m[k];if(t===undefined)return'<div class="tr">?</div>';
const w=m.w!==undefined&&m.w===t,sc=m.w===undefined?'':(k==='a'?m.sa:m.sb);
return`<div class="tr${w?' w':''}${t===me?' me':''}">${dot(t)}<span>${T[t][0]}</span><b>${sc}</b></div>`}
function showBracket(){
(!alive||R[LAST][0].w!==undefined?clearG:saveG)();
$('bracket').innerHTML=R.map((rd,ri)=>`<div class="col"><h3>${RS[ri]}</h3>${rd.map(m=>`<div class="mt">${row(m,'a')}${row(m,'b')}</div>`).join('')}</div>`).join('');
const pm=alive&&pend();
if(pm){const opp=pm.a===me?pm.b:pm.a;
$('bInfo').textContent=RN[round]+': '+T[me][0]+' vs '+T[opp][0];
$('goBtn').textContent='⚽ Играть матч';$('goBtn').hidden=false;$('goBtn').onclick=()=>startMatch();}
else{const f=R[LAST][0];$('goBtn').hidden=true;
$('bInfo').textContent='Вылет. Чемпион Европы: '+(f.w!==undefined?T[f.w][0]:'?');}
show('bv');
}
function afterMatch(win){
const m=pend();
m.sa=m.a===me?M.y:M.c;m.sb=m.b===me?M.y:M.c;
m.w=win?me:(m.a===me?m.b:m.a);
if(!win)alive=false;
if(round===LAST){if(win)startCer();else showBracket();return}
advance();
if(!alive)while(round<LAST)advance();
showBracket();
}

/* ---------- матч ---------- */
function startMatch(lo){
const lg=lo!==undefined;let opp=lo;
if(!lg){const m=pend();opp=m.a===me?m.b:m.a}
M={opp,y:0,c:0,yk:[],ck:[],turn:'you',n:lg?3:5,lg};
cer=null;aim={x:400,y:170};$('contBtn').hidden=true;
$('title').innerHTML=(lg?'Общий этап, тур '+(LG.day+1)+' из 8':RN[round])+': '+dot(me)+T[me][0]+' vs '+dot(opp)+T[opp][0];
$('hint').textContent='Тип удара и сила влияют на точность и скорость. Паненка летит в центр и срабатывает, если вратарь прыгнет в угол!';
show('gv');setTurn();ui();
}
function setTurn(){
anim=null;busy=false;
$('saveBtns').hidden=M.turn!=='cpu';$('shotUI').hidden=M.turn!=='you';
$('msg').textContent=M.turn==='you'?'Твой удар! Выбери тип и силу, потом кликни по воротам':'Прыгай! Выбери сторону';
}
function ui(){
$('score').textContent=M.y+' : '+M.c;
const n=Math.max(M.n,M.yk.length,M.ck.length);
const d=a=>{let s='';for(let i=0;i<n;i++)s+=i<a.length?(a[i]?'🟢':'🔴'):'⚪';return s};
$('dots').innerHTML='Ты: '+d(M.yk)+'<br>Он: '+d(M.ck);
}
function pos(e){const r=cv.getBoundingClientRect();return{x:(e.clientX-r.left)*800/r.width,y:(e.clientY-r.top)*500/r.height}}
cv.addEventListener('pointermove',e=>{if(M&&!cer&&M.turn==='you'&&!busy)aim=pos(e)});
cv.addEventListener('pointerdown',e=>{if(M&&!cer&&M.turn==='you'&&!busy){aim=pos(e);shoot()}});
const saved=(kx,tx,ty,rx)=>((tx-kx)/(rx||66))**2+((ty-170)/80)**2<1;
const TY=[{n:'Обычный',j:24,d:.55,rx:66},{n:'Точный',j:8,d:.7,rx:66},{n:'Мощный',j:38,d:.38,rx:52},{n:'Паненка',j:0,d:.95,rx:0}];
let tyI=0;
$('types').innerHTML=TY.map((t,i)=>`<button class="alt" data-t="${i}">${t.n}</button>`).join('');
function selTy(i){tyI=i;document.querySelectorAll('#types button').forEach((b,k)=>{b.style.background=k===i?'var(--ac)':'';b.style.color=k===i?'#fff':''})}
$('types').onclick=e=>{const b=e.target.closest('button');if(b)selTy(+b.dataset.t)};selTy(0);
$('pw').oninput=()=>$('pwv').textContent=$('pw').value;
function shoot(){
busy=true;const k=TY[tyI],p=+$('pw').value/100;
let tx,ty,res,z,d=k.d*(1.25-p*.5),arc=1;
if(tyI===3){
z=Math.random()<.28?1:(Math.random()<.5?0:2);
tx=400+(Math.random()-.5)*20;d=.95;arc=3;
const miss=Math.random()<.06;ty=miss?40:135;res=miss?'miss':(z===1?'save':'goal');
}else{
const j=k.j*(.6+p*.8);
tx=Math.max(170,Math.min(630,aim.x))+(Math.random()-.5)*j;
ty=Math.max(70,Math.min(270,aim.y))+(Math.random()-.5)*j-(p>.92?Math.random()*40:0);
const az=tx<333?0:tx>467?2:1;
z=Math.random()<.2+(T[M.opp][2]-.7)?az:Math.floor(Math.random()*3);
const inG=tx>G.x1&&tx<G.x2&&ty>G.y1&&ty<G.y2;
res=!inG?'miss':(saved(ZX[z],tx,ty,k.rx-(p*100-60)*.15)?'save':'goal');
}
anim={kn:(M.turn==='you'?M.yk.length:M.ck.length),w:.45,t:0,tx,ty,k1:ZX[z],res,who:'you',d,arc};
}
function dive(z){
if(!M||cer||M.turn!=='cpu'||busy)return;busy=true;
const pan=Math.random()<.1,tz=Math.floor(Math.random()*3),miss=!pan&&Math.random()<.18-(T[M.opp][2]-.7)*.5;
let tx,ty,res,d=.55,arc=1;
if(pan){tx=400+(Math.random()-.5)*20;ty=135;d=.95;arc=3;res=z===1?'save':'goal'}
else{tx=miss?(Math.random()<.5?170:630):ZX[tz]+(Math.random()-.5)*90;ty=100+Math.random()*130;res=miss?'miss':(saved(ZX[z],tx,ty)?'save':'goal')}
anim={kn:(M.turn==='you'?M.yk.length:M.ck.length),w:.45,t:0,tx,ty,k1:ZX[z],res,who:'cpu',d,arc};
}
document.querySelectorAll('#saveBtns button').forEach(b=>b.onclick=()=>dive(+b.dataset.z));
addEventListener('keydown',e=>{const m={ArrowLeft:0,ArrowDown:1,ArrowRight:2};if(e.key in m)dive(m[e.key])});
function finish(){
const a=anim,ok=a.res==='goal';
if(a.who==='you'){M.yk.push(ok);if(ok)M.y++}else{M.ck.push(ok);if(ok)M.c++}
if(a.who==='you'){if(ok){ST.goals++;ST.gs++}else ST.gs=0}else if(a.res==='save')ST.saves++;
check();
$('msg').textContent=ok?(a.who==='you'?'ГОЛ! 🎉':'Он забил… 😬'):a.res==='save'?(a.who==='you'?'Вратарь отбил! 🧤':'Ты поймал! 🧤🔥'):(a.who==='you'?'Мимо ворот! 😅':'Он промахнулся! 😎');
(ok?sfxGoal:a.res==='save'?sfxSave:sfxMiss)();
ui();setTimeout(afterKick,1600);
}
function afterKick(){
const n=M.n,yl=n-M.yk.length,cl=n-M.ck.length;let done=false;
if(M.yk.length<=n&&M.ck.length<=n){if(M.y>M.c+Math.max(cl,0)||M.c>M.y+Math.max(yl,0))done=true}
if(M.turn==='cpu'&&M.yk.length>=n&&M.ck.length===M.yk.length&&M.y!==M.c)done=true;
if(done)return endMatch();
M.turn=M.turn==='you'?'cpu':'you';setTurn();
}
function endMatch(){
anim=null;M.turn='end';$('saveBtns').hidden=true;$('shotUI').hidden=true;
const win=M.y>M.c;
if(win){ST.ws++;ST.wins++}else ST.ws=0;check();
$('msg').textContent=win?'✅ Победа в серии '+M.y+':'+M.c+'!':'❌ Поражение в серии '+M.y+':'+M.c;
$('contBtn').textContent=!M.lg&&win&&round===LAST?'🏆 Получить кубок':'Дальше';
$('contBtn').hidden=false;$('contBtn').onclick=()=>M.lg?afterLeague(win):afterMatch(win);
}

/* ---------- церемония ---------- */
function startCer(){ST.cups++;check();clearG();sfxFanfare();
cer={t:0,p:Array.from({length:160},()=>({x:Math.random()*800,y:-Math.random()*600,v:70+Math.random()*130,c:`hsl(${Math.random()*360} 90% 60%)`,s:4+Math.random()*5,r:Math.random()*6}))};
show('gv');$('saveBtns').hidden=true;$('contBtn').hidden=true;
$('title').textContent='Финал выигран!';$('score').textContent='';$('dots').textContent='';
$('hint').textContent='';$('msg').textContent='Вручение кубка…';
}
function cup(cx,cy,s){
ctx.save();ctx.translate(cx,cy);ctx.scale(s,s);
const g=ctx.createLinearGradient(-60,0,60,0);g.addColorStop(0,'#b8860b');g.addColorStop(.5,'#ffe066');g.addColorStop(1,'#b8860b');
ctx.fillStyle=g;ctx.strokeStyle=g;ctx.lineWidth=10;
ctx.beginPath();ctx.arc(-52,-30,22,Math.PI*.5,Math.PI*1.5);ctx.stroke();
ctx.beginPath();ctx.arc(52,-30,22,Math.PI*1.5,Math.PI*.5);ctx.stroke();
ctx.beginPath();ctx.moveTo(-50,-70);ctx.lineTo(50,-70);ctx.quadraticCurveTo(52,10,0,32);ctx.quadraticCurveTo(-52,10,-50,-70);ctx.fill();
ctx.fillRect(-8,30,16,42);ctx.fillRect(-32,68,64,14);ctx.fillRect(-44,82,88,16);
ctx.fillStyle='rgba(255,255,255,.35)';ctx.fillRect(-36,-62,10,60);
ctx.restore();
}
function drawCer(){
cer.t+=dtGlobal;const t=cer.t;
const g=ctx.createLinearGradient(0,0,0,500);g.addColorStop(0,'#0b1330');g.addColorStop(1,'#1b2a6b');
ctx.fillStyle=g;ctx.fillRect(0,0,800,500);
ctx.fillStyle='rgba(255,255,255,.07)';
ctx.beginPath();ctx.moveTo(0,0);ctx.lineTo(120,0);ctx.lineTo(480,430);ctx.lineTo(300,430);ctx.fill();
ctx.beginPath();ctx.moveTo(800,0);ctx.lineTo(680,0);ctx.lineTo(320,430);ctx.lineTo(500,430);ctx.fill();
ctx.fillStyle='#2a2f45';ctx.fillRect(250,400,300,100);
ctx.fillStyle='#ffd700';ctx.font='bold 40px system-ui';ctx.textAlign='center';ctx.fillText('1',400,455);
const e=Math.min(1,Math.max(0,(t-1.2)/2.2)),k=1-Math.pow(1-e,3);
if(t>1.2){const glow=ctx.createRadialGradient(400,0,0,400,0,160);
ctx.save();ctx.translate(0,330-170*k+60);ctx.fillStyle='rgba(255,224,102,.25)';ctx.beginPath();ctx.arc(400,-10,110*k,0,7);ctx.fill();ctx.restore();
cup(400,330-170*k+60,.55+.5*k);}
if(t>3.4){$('msg').textContent='🏆 ЧЕМПИОН ЕВРОПЫ!';
ctx.font='bold 34px system-ui';
ctx.fillStyle=T[me][1];ctx.beginPath();ctx.arc(400-ctx.measureText(T[me][0]).width/2-22,61,11,0,7);ctx.fill();
ctx.fillStyle='#fff';ctx.fillText(T[me][0],400,72);
if($('contBtn').hidden){$('contBtn').textContent='Новый турнир';$('contBtn').hidden=false;$('contBtn').onclick=()=>show('menu');}}
if(t>1.5)for(const p of cer.p){p.y+=p.v*dtGlobal;p.r+=dtGlobal*4;if(p.y>510){p.y=-10;p.x=Math.random()*800}
ctx.save();ctx.translate(p.x,p.y);ctx.rotate(p.r);ctx.fillStyle=p.c;ctx.fillRect(-p.s/2,-p.s/4,p.s,p.s/2);ctx.restore();}
}

/* ---------- отрисовка ---------- */
/* ---------- звук (всё генерируется в браузере) ---------- */
let AC,master,NB,step=0,nextT=0,mus=true;
function audio(){
if(AC){if(AC.state==='suspended')AC.resume();return}
try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){return}
master=AC.createGain();master.gain.value=mus?.5:0;master.connect(AC.destination);
NB=AC.createBuffer(1,AC.sampleRate*2,AC.sampleRate);const d=NB.getChannelData(0);for(let i=0;i<d.length;i++)d[i]=Math.random()*2-1;
nextT=AC.currentTime+.1;setInterval(sched,100);
const n=AC.createBufferSource();n.buffer=NB;n.loop=true;const f=AC.createBiquadFilter();f.type='lowpass';f.frequency.value=500;
const g=AC.createGain();g.gain.value=.05;n.connect(f);f.connect(g);g.connect(master);n.start();
}
document.addEventListener('pointerdown',audio);
$('mute').onclick=()=>{audio();mus=!mus;$('mute').textContent=mus?'🔊':'🔇';if(master)master.gain.value=mus?.5:0};
function tone(f,t,d,ty,v,f2){const o=AC.createOscillator(),g=AC.createGain();o.type=ty;o.frequency.setValueAtTime(f,t);if(f2)o.frequency.exponentialRampToValueAtTime(f2,t+d);
g.gain.setValueAtTime(v,t);g.gain.exponentialRampToValueAtTime(.001,t+d);o.connect(g);g.connect(master);o.start(t);o.stop(t+d+.02)}
function noise(t,d,v,fr,ty,sw){const s=AC.createBufferSource();s.buffer=NB;const f=AC.createBiquadFilter();f.type=ty;f.frequency.value=fr;const g=AC.createGain();
if(sw){g.gain.setValueAtTime(.001,t);g.gain.linearRampToValueAtTime(v,t+d*.3)}else g.gain.setValueAtTime(v,t);
g.gain.exponentialRampToValueAtTime(.001,t+d);s.connect(f);f.connect(g);g.connect(master);s.start(t);s.stop(t+d+.05)}
const BR=[110,87.31,130.81,98],AR=[[440,523.25,659.25,523.25],[349.23,440,523.25,440],[523.25,659.25,783.99,659.25],[392,493.88,587.33,493.88]];
function sched(){if(!AC)return;while(nextT<AC.currentTime+.25){const s=step%16,b=Math.floor(step/16)%4,t=nextT;
if(s%4===0)tone(120,t,.15,'sine',.5,40);
if(s%8===4)noise(t,.12,.25,1800,'bandpass');
if(s%2===1)noise(t,.04,.08,7000,'highpass');
if(s%4===2)tone(BR[b],t,.2,'triangle',.3);
if(s%2===0)tone(AR[b][(s/2)%4],t,.14,'square',.035);
nextT+=60/124/4;step++}}
const sfxKick=()=>{if(!AC)return;const t=AC.currentTime;tone(180,t,.12,'sine',.7,50);noise(t,.06,.3,1200,'lowpass')};
const sfxGoal=()=>{if(!AC)return;const t=AC.currentTime;noise(t,1.6,.5,1500,'bandpass',1);[523.25,659.25,783.99,1046.5].forEach((f,i)=>tone(f,t+i*.09,.5,'triangle',.18))};
const sfxSave=()=>{if(!AC)return;const t=AC.currentTime;tone(90,t,.2,'sine',.6,50);noise(t,.15,.3,900,'lowpass');noise(t+.1,.6,.2,1000,'bandpass',1)};
const sfxMiss=()=>{if(!AC)return;const t=AC.currentTime;tone(400,t,.5,'sawtooth',.1,150);noise(t,.9,.25,700,'bandpass',1)};
const sfxFanfare=()=>{if(!AC)return;const t=AC.currentTime;[523.25,659.25,783.99,1046.5,783.99,1046.5,1318.5].forEach((f,i)=>tone(f,t+i*.22,.45,'square',.09));noise(t+.8,3,.5,1600,'bandpass',1)};

/* ---------- цикл ---------- */
let last=0,now=0;
function loop(ts){
const dt=Math.min(.05,(ts-last)/1000||0);last=ts;now=ts/1000;dtGlobal=dt;
if(!$('gv').hidden){
if(cer)drawCer();
else if(M){
if(anim){
if(anim.w>0){anim.w-=dt;if(anim.w<=0&&!anim.k){anim.k=1;sfxKick()}}
else if(anim.t<1){anim.t=Math.min(1,anim.t+dt/(anim.d||.55));if(anim.t>=1&&!anim.done){anim.done=true;anim.ft=now;finish()}}
}
draw();}
}
requestAnimationFrame(loop);
}

/* ---------- живые человечки ---------- */
const CC=['#e63946','#f1c40f','#3498db','#ffffff','#2ecc71','#e67e22'];
function person(x,y,col,o){
const L=o.lean||0,sx=x+L,sy=y-34;ctx.lineCap='round';
ctx.strokeStyle='#1d2433';ctx.lineWidth=9;ctx.beginPath();
ctx.moveTo(x-5,y);ctx.lineTo(x-5+o.fl[0],y+o.fl[1]);ctx.moveTo(x+5,y);ctx.lineTo(x+5+o.fr[0],y+o.fr[1]);ctx.stroke();
ctx.strokeStyle=col;ctx.lineWidth=26;ctx.beginPath();ctx.moveTo(x,y);ctx.lineTo(sx,sy);ctx.stroke();
if(o.num){const mx=x+L*.5,my=y-17;ctx.fillStyle=o.tc;ctx.textAlign='center';ctx.font='bold 7px system-ui';ctx.fillText(o.tag,mx,my-4);ctx.font='bold 13px system-ui';ctx.fillText(o.num,mx,my+9);ctx.textAlign='left'}
ctx.lineWidth=7;ctx.beginPath();
ctx.moveTo(sx-9,sy+2);ctx.lineTo(sx-9+o.al[0],sy+2+o.al[1]);ctx.moveTo(sx+9,sy+2);ctx.lineTo(sx+9+o.ar[0],sy+2+o.ar[1]);ctx.stroke();
if(o.g){ctx.fillStyle='#b6ff3b';[[sx-9+o.al[0],sy+2+o.al[1]],[sx+9+o.ar[0],sy+2+o.ar[1]]].forEach(h=>{ctx.beginPath();ctx.arc(h[0],h[1],6,0,7);ctx.fill()})}
ctx.fillStyle='#f1c9a0';ctx.beginPath();ctx.arc(sx+L*.2,sy-18,10,0,7);ctx.fill();
ctx.fillStyle='#3b2a1a';ctx.beginPath();ctx.arc(sx+L*.2,sy-21,10,Math.PI,0);ctx.fill();
}
const tagOf=i=>{const w=T[i][0].split(' ');return(w.length>1?w.map(x=>x[0]).join(''):w[0].slice(0,3)).toUpperCase()};
const txc=h=>{const c=rgb(h);return(.3*c[0]+.59*c[1]+.11*c[2])/255>.55?'#111':'#fff'};
const shNum=(t,k)=>2+((t*7+k*5+3)%23);
function pent(x,y,r){ctx.beginPath();for(let i=0;i<5;i++){const t=-Math.PI/2+i*1.2566;ctx.lineTo(x+Math.cos(t)*r,y+Math.sin(t)*r)}ctx.closePath();ctx.fill()}
function drawBall(x,y,r,ang){
ctx.save();ctx.translate(x,y);ctx.rotate(ang);
ctx.beginPath();ctx.arc(0,0,r,0,7);ctx.fillStyle='#fff';ctx.fill();ctx.clip();
ctx.fillStyle='#1c1c1c';pent(0,0,r*.38);
for(let i=0;i<5;i++){const t=i*1.2566;pent(Math.cos(t)*r*.98,Math.sin(t)*r*.98,r*.3)}
const g=ctx.createRadialGradient(-r*.35,-r*.35,r*.1,0,0,r);g.addColorStop(0,'rgba(255,255,255,0)');g.addColorStop(1,'rgba(0,0,0,.28)');
ctx.fillStyle=g;ctx.fillRect(-r,-r,2*r,2*r);ctx.restore();
ctx.beginPath();ctx.arc(x,y,r,0,7);ctx.strokeStyle='#8a8a8a';ctx.lineWidth=1;ctx.stroke();
}
function draw(){
ctx.textAlign='left';ctx.clearRect(0,0,800,500);
for(let i=0;i<10;i++){ctx.fillStyle=i%2?'#2f9a3d':'#34a844';ctx.fillRect(0,i*50,800,50)}
const a=anim,hot=a&&a.done&&a.res==='goal'&&now-a.ft<1.8;
ctx.fillStyle='#1b2236';ctx.fillRect(0,0,800,62);
for(let r=0;r<3;r++)for(let i=0;i<40;i++){const b=Math.abs(Math.sin(now*(hot?7:2)+i*1.7+r))*(hot?9:2);
ctx.fillStyle=CC[(i*3+r*5)%CC.length];ctx.beginPath();ctx.arc(10+i*20+(r%2)*10,50-r*16-b,7,0,7);ctx.fill()}
ctx.strokeStyle='rgba(255,255,255,.8)';ctx.lineWidth=3;
ctx.strokeRect(120,250,560,300);ctx.strokeRect(260,250,280,90);
ctx.beginPath();ctx.moveTo(0,250);ctx.lineTo(800,250);ctx.stroke();
ctx.save();ctx.beginPath();ctx.rect(G.x1,G.y1,400,160);ctx.clip();
ctx.fillStyle='rgba(10,25,10,.38)';ctx.fillRect(G.x1,G.y1,400,160);
ctx.strokeStyle='rgba(255,255,255,.17)';ctx.lineWidth=1;
for(let i=-160;i<400;i+=26){ctx.beginPath();ctx.moveTo(G.x1+i,G.y1);ctx.lineTo(G.x1+i+160,G.y2);ctx.moveTo(G.x1+i+160,G.y1);ctx.lineTo(G.x1+i,G.y2);ctx.stroke()}
ctx.restore();
const mo=T[me][1];let oo=T[M.opp][1];if(cd(mo,oo)<110)oo=awayK(oo);const kcol=gkK(M.turn==='cpu'?me:M.opp),scol=M.turn==='cpu'?oo:mo;
const flying=a&&a.w<=0,tt=a?a.t:0,e=1-Math.pow(1-Math.min(1,tt*1.6),3);
let bx=400,by=430,br=14;
if(flying){bx=400+(a.tx-400)*tt;by=430+(a.ty-430)*tt-Math.sin(tt*Math.PI)*40*(a.arc||1);br=14-6*tt}
// вратарь
const k1=a?a.k1:400,sway=(!a||a.w>0)?Math.sin(now*2.5)*14:0,kx=400+(flying?(k1-400)*e:0)+sway;
const sv=!!(a&&a.res==='save'),el=a&&a.done?now-a.ft:0,land=Math.min(1,el/.4),hug=Math.min(1,el/.3);
const d=flying?(Math.sign(k1-400)||0):0,lean=flying?(k1-400)*.18*e*(1+land*.8):0;
const hip=226-14*e*(1-land)+10*land,sx=kx+lean,sy=hip-34;
const cl=(dx,dy)=>{const L=Math.hypot(dx,dy),m=80;return L>m?[dx*m/L,dy*m/L]:[dx,dy]};
let al,ar;
if(flying&&sv){al=cl((a.tx-sx+9)*e,(a.ty-sy)*e);ar=cl((a.tx-sx-9)*e,(a.ty-sy)*e);
al=[al[0]*(1-hug)+10*hug,al[1]*(1-hug)+16*hug];ar=[ar[0]*(1-hug)-10*hug,ar[1]*(1-hug)+16*hug]}
else if(flying){al=[-10+d*28*e,-30*e];ar=[10+d*28*e,-30*e]}
else{const w=Math.sin(now*6)*6;al=[-26,-12+w];ar=[26,-12-w]}
const kTeam=M.turn==='cpu'?me:M.opp,sTeam=M.turn==='cpu'?M.opp:me;
person(kx,hip,kcol,{lean,g:1,al,ar,fl:[-8-d*14*e,22-8*e],fr:[8-d*14*e,22-12*e],num:1,tag:tagOf(kTeam),tc:txc(kcol)});
ctx.strokeStyle='#fff';ctx.lineWidth=6;ctx.lineCap='square';
ctx.beginPath();ctx.moveTo(G.x1,G.y2);ctx.lineTo(G.x1,G.y1);ctx.lineTo(G.x2,G.y1);ctx.lineTo(G.x2,G.y2);ctx.stroke();
// бьющий игрок
const kn=a?a.kn:(M.turn==='you'?M.yk.length:M.ck.length);
const run=a?1-Math.max(0,a.w)/.45:0,px=250+110*run;let py=444,fl=[-6,22],fr=[6,22],pal=[-10,12],par=[10,12];
if(a&&a.w>0){const q=Math.sin(now*20)*12;fl=[q,22];fr=[-q,22];pal=[-q*.7,12];par=[q*.7,12]}
else if(a&&!a.done){const q=Math.min(1,tt*3);fr=[26-14*q,20-8*q];fl=[-6,22];pal=[10,10];par=[-10,10]}
if(a&&a.done){
if(a.res==='goal'&&el<2){py-=Math.abs(Math.sin(el*7))*20;pal=[-12,-26];par=[12,-26]}
else if(a.res!=='goal'){pal=[-8,-20];par=[8,-20]}}
person(px,py,scol,{fl,fr,al:pal,ar:par,num:shNum(sTeam,kn),tag:tagOf(sTeam),tc:txc(scol)});
// мяч: тень, вращение, падение в сетке, мяч в руках
let hx=bx,hy=by;
if(a&&a.done){
if(sv){const mx=sx+(al[0]+ar[0])/2,my=sy+2+(al[1]+ar[1])/2;hx=bx+(mx-bx)*hug;hy=by+(my-by)*hug}
else{const gy=a.res==='miss'?262:244,t1=Math.sqrt(2*Math.max(1,gy-a.ty)/700);
if(el<t1)hy=a.ty+350*el*el;else{const q=el-t1;hy=gy-16*Math.abs(Math.sin(q*8))*Math.exp(-q*2.5)}}}
const gs=(!a||a.w>0)?440:(!a.done?430+(a.ty-430)*tt+8:250),hh=Math.max(0,gs-hy);
ctx.fillStyle='rgba(0,0,0,'+(.32/(1+hh/50))+')';ctx.beginPath();ctx.ellipse(hx,gs,br*1.1,br*.38,0,0,7);ctx.fill();
drawBall(hx,hy,br,(a&&a.w<=0?tt*18:0)+(a&&a.done?Math.min(el,.8)*8:0));
if(M.turn==='you'&&!busy){
const x=Math.max(170,Math.min(630,aim.x)),y=Math.max(70,Math.min(270,aim.y));
ctx.strokeStyle='#e63946';ctx.lineWidth=3;ctx.beginPath();ctx.arc(x,y,16,0,7);
ctx.moveTo(x-24,y);ctx.lineTo(x+24,y);ctx.moveTo(x,y-24);ctx.lineTo(x,y+24);ctx.stroke()}
}
updateCont();requestAnimationFrame(loop);
</script>
</body>
</html>
