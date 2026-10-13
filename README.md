<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Aprende a leer</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#eaf4ff;--ink:#1b2440;--card:#fff;--accent:#5b45e0;--on:#fff;--sun:#ffc83d;--ok:#1fa97a;--bad:#e5484d;--line:#c9d8f0;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#131a30;--ink:#eef1ff;--card:#1f2847;--accent:#8c7bff;--on:#10142b;--line:#33406a}}
:root[data-theme="dark"]{--bg:#131a30;--ink:#eef1ff;--card:#1f2847;--accent:#8c7bff;--on:#10142b;--line:#33406a}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:'Fredoka',system-ui,sans-serif;font-size:18px;min-height:100vh}
main{max-width:560px;margin:0 auto;padding:14px 16px 40px}
header{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px}
h1{font-size:1.3rem;margin:0}h2{margin:0 0 12px}
.hd{display:flex;gap:8px;align-items:center}
#stars{background:var(--sun);color:#3a2a00;border-radius:99px;padding:4px 14px;font-weight:700}
button{font:inherit;color:inherit;cursor:pointer}
button:focus-visible,input:focus-visible{outline:3px solid var(--accent);outline-offset:3px}
.menu{display:grid;gap:12px;margin-bottom:12px}
.big{background:var(--card);border:2px solid var(--line);border-radius:22px;padding:16px;text-align:left;display:flex;gap:14px;align-items:center;width:100%}
.big b{display:block;font-size:1.2rem}.big span{font-size:.9rem;opacity:.75}.big i{font-style:normal;font-size:2rem}
.back{background:none;border:0;font-weight:600;padding:8px 0;color:var(--accent)}
.stage{background:var(--card);border:2px solid var(--line);border-radius:26px;padding:22px 16px;text-align:center}
.pic{font-size:4.5rem;line-height:1.1}
.word{display:flex;justify-content:center;gap:6px;margin:14px 0;flex-wrap:wrap}
.l{font-size:3.2rem;font-weight:700;border-radius:16px;padding:0 8px;transition:all .15s}
.l.on{background:var(--sun);color:#3a2a00;transform:scale(1.15)}
.row{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-top:10px}
.btn{background:var(--accent);color:var(--on);border:0;border-radius:16px;padding:14px 20px;font-weight:600}
.btn.alt{background:transparent;color:var(--ink);border:2px solid var(--line)}
.btn.rec{background:var(--bad);color:#fff}
input{font:inherit;padding:12px;border-radius:14px;border:2px solid var(--line);background:var(--bg);color:var(--ink);min-width:0;flex:1}
.fb{min-height:2.4em;margin-top:12px;font-weight:600}
.fb.ok{color:var(--ok)}.fb.no{color:var(--bad)}
.grid{display:grid;grid-template-columns:repeat(5,1fr);gap:10px}
.k{aspect-ratio:1;font-size:2rem;font-weight:700;background:var(--card);border:2px solid var(--line);border-radius:18px;padding:0}
.k.cur{border-color:var(--accent);background:var(--sun);color:#3a2a00}
.k:disabled{opacity:.45;cursor:default}
.slot{width:58px;height:70px;border-bottom:5px solid var(--line);font-size:2.8rem;font-weight:700}
.txt{font-size:2rem;line-height:1.5;font-weight:600;text-align:left;padding:6px 4px}
.in{animation:in .45s both}
@keyframes in{from{opacity:0;transform:translateY(12px)}}
.big.go{background:var(--accent);color:var(--on);border-color:var(--accent)}
.btn.sm{padding:8px 14px;font-size:.9rem}
.shake{animation:sh .3s}
@keyframes sh{25%{transform:translateX(-6px)}75%{transform:translateX(6px)}}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style>
</head>
<body>
<main>
<header><h1>📖 Leer</h1><div class="hd"><div class="hd" id="hd"></div><button class="back" id="th" aria-label="Cambiar tema"></button></div></header>
<div id="app"></div>
</main>
<script>
/* ===== CONFIGURACIÓN (editable) ===== */
// Orden de aprendizaje: una letra por nivel
const ORDER='a e i o u l m s n h d f p t r b v ñ y k c z q g j w x ll ch'.split(' ');
// Palabras de cada nivel (solo letras ya aprendidas). Formato: palabra+emoji opcional, separadas por espacio
const WD={l:'ala ola aula',m:'mama mula lima malo',s:'sol☀️ mesa🪑 sala isla🏝️',n:'luna🌙 mano✋ mono🐒 nena',h:'hola hilo🧵 humo💨 hueso🦴',d:'dado🎲 dedo nido🪺 mundo🌍',f:'fila fino fideo fama',p:'sopa🍲 mapa🗺️ pelo pulpo🐙',t:'pato🦆 lata🥫 tomate🍅 tinta',r:'pera🍐 rana🐸 mira pared',b:'bota👢 libro📖 nube☁️ bolsa',v:'vaso🥛 vela🕯️ uva🍇 nave🚀',ñ:'niño👦 piña🍍 baño🛁 uña',y:'yoyo yema🥚 yate🛥️ rey👑',k:'kilo⚖️ koala🐨 kayak🛶 karate🥋',c:'casa🏠 cama🛏️ cola cuna',z:'zapato👟 zumo🧃 taza luz💡',q:'queso🧀 paquete📦 quiero',g:'gato🐱 goma lago gusano🐛',j:'ojo👁️ caja jirafa🦒 tijeras✂️',w:'kiwi🥝 wifi📶 web🌐',x:'taxi🚕 texto boxeo🥊',ll:'lluvia🌧️ llave🔑 silla pollo🍗',ch:'leche🥛 coche🚗 noche mochila🎒'};
// Sílabas de cada nivel (se practican entre las letras y las palabras). Sin entrada = sin sílabas
const SYL={l:'la le li lo lu',m:'ma me mi mo mu',s:'sa se si so su',n:'na ne ni no nu',h:'ha he hi ho hu',d:'da de di do du',f:'fa fe fi fo fu',p:'pa pe pi po pu',t:'ta te ti to tu',r:'ra re ri ro ru',b:'ba be bi bo bu',v:'va ve vi vo vu',ñ:'ña ñe ñi ño ñu',y:'ya ye yi yo yu',k:'ka ke ki ko ku',c:'ca co cu',z:'za ze zi zo zu ce ci',q:'que qui',g:'ga go gu gue gui',j:'ja je ji jo ju ge gi',w:'wa we wi',ll:'lla lle lli llo llu',ch:'cha che chi cho chu'};
// Niveles extra tras las letras: sílabas inversas y trabadas. g = etiqueta corta del botón, t = título, s = sílabas, w = palabras
const EXTRA=[
{g:'al',t:'Sílabas inversas: L y R',s:'al el il ol ul ar er ir or ur',w:'sal🧂 papel mar🌊 color🎨'},
{g:'as',t:'Sílabas inversas: S y N',s:'as es is os us an en in on un',w:'isla🏝️ pasta🍝 mosca🪰 pan🍞'},
{g:'am',t:'Sílabas inversas: M, D y Z',s:'am em im om um ad ed id od ud az ez iz oz uz',w:'campo🏕️ tambor🥁 pez🐟 azul💙'},
{g:'bl',t:'Trabadas: bl y br',s:'bla ble bli blo blu bra bre bri bro bru',w:'blusa👚 tabla brazo💪 bruja🧙'},
{g:'cl',t:'Trabadas: cl y cr',s:'cla cle cli clo clu cra cre cri cro cru',w:'clase🏫 clavo🔩 crema🧴 cruz'},
{g:'fl',t:'Trabadas: fl y fr',s:'fla fle fli flo flu fra fre fri fro fru',w:'flor🌸 flaco fruta🍎 fresa🍓'},
{g:'gl',t:'Trabadas: gl y gr',s:'gla gle gli glo glu gra gre gri gro gru',w:'globo🎈 regla📏 tigre🐯 gris'},
{g:'dr',t:'Trabadas: dr y tr',s:'dra dre dri dro dru tra tre tri tro tru',w:'cuadro🖼️ madre👩 tren🚆 trigo🌾'},
{g:'pl',t:'Trabadas: pl y pr',s:'pla ple pli plo plu pra pre pri pro pru',w:'plato🍽️ pluma🪶 playa🏖️ premio🏆'}];
// Textos decodificables: [texto, pregunta (la lee la voz), [opción correcta, otras opciones...]]. El nivel en que se desbloquea se calcula solo, según las letras que use
const TX0=[
['Mamá ama a mi mula.','¿Qué ama mamá?',['🐴','🍎']],
['Mi mamá usa la sal.','¿Qué usa mamá?',['🧂','🍬']],
['Mi mamá sale a la isla.','¿A dónde sale mamá?',['🏝️','🪑']],
['Mi mono ama la luna.','¿Qué ama el mono?',['🌙','🍌']],
['Ana ama su mono.','¿Qué ama Ana?',['🐒','🌙']],
['Mamá da un dado a la nena.','¿Qué da mamá?',['🎲','🍎']],
['Papá usa una pala.','¿Qué usa papá?',['⛏️','🍲']],
['Mi mamá pone sopa en la mesa.','¿Qué pone mamá en la mesa?',['🍲','🍎']],
['El pato está en la sala.','¿Quién está en la sala?',['🦆','🐻']],
['Mi mamá pone tomate en la sopa.','¿Qué pone en la sopa?',['🍅','🍌']],
['El pato está en la sala. El pato es de papá. El pato no es de mamá.','¿De quién es el pato?',['👨','👩']],
['Una rana está en la mesa.','¿Quién está en la mesa?',['🐸','🐀']],
['Rosa tiene una pera. Rosa pone la pera en la mesa. Mamá toma la pera.','¿Qué tiene Rosa?',['🍐','🍎']],
['Mi bebé tiene una bota.','¿Qué tiene el bebé?',['👢','🧸']],
['Tito tiene un libro. Es un libro de ratas. Tito abre el libro.','¿Qué abre Tito?',['📖','📦']],
['Ana ve una uva en la mesa.','¿Qué ve Ana?',['🍇','🍌']],
['El niño pone una piña en la mesa.','¿Qué pone el niño?',['🍍','🍇']],
['Yo uso mi yoyo en la sala.','¿Con qué juega?',['🪀','⚽']],
['Hay un pato en el río.','¿Qué hay en el río?',['🦆','🐻']],
['La nena está en la cama.','¿Dónde está la nena?',['🛏️','🪑']],
['Mi casa tiene una sala. En la sala hay una mesa. En la mesa hay una sopa.','¿Qué hay en la mesa?',['🍲','🍎']],
['Hay un pez en el mar.','¿Qué hay en el mar?',['🐟','🐻']],
['Hay un gato en mi casa. El gato es de mamá. El gato come pan.','¿Qué come el gato?',['🍞','🐟']],
['Mi papá tiene una caja.','¿Qué tiene papá?',['📦','🎁']],
['Hoy llueve en la calle.','¿Qué hay hoy?',['🌧️','☀️']],
['Mamá lleva una llave.','¿Qué lleva mamá?',['🔑','🍎']],
['Mi mamá toma leche.','¿Qué toma mamá?',['🥛','🍵']],
['Papá tiene un coche. El coche es rojo. Papá sale en el coche.','¿De qué color es el coche?',['🔴','🔵']]];
const TX=TX0.map(([x,q,o])=>({x,q,o,n:(x.match(/\./g)||[]).length,l:Math.max(...x.toLowerCase().match(/ll|ch|[a-zñ]/g).map(u=>ORDER.indexOf(u)))}));
let lastX=null;
const FR_FROM=14; // desde este nivel (0 = A; 14 = R, la mitad de las letras) se añade una frase o lectura al final de cada nivel
// Texto que lee la voz sintética para cada sonido (se sustituye por tus audios)
const SND={l:'lll',m:'mmm',s:'sss',n:'nnn',f:'fff',r:'rrr',h:'hache. Esta letra no suena',v:'b',c:'k',q:'k',w:'u',x:'ks',z:'zzz'};
// Tus grabaciones: 'l:m' = sonido de la letra m, 'w:mesa' = palabra mesa. Valor: URL o data:audio
const AUD={};
const PASS=0.5; // fracción de palabras bien leídas para superar la letra
/* ===================================== */
const $=s=>document.querySelector(s),app=$('#app');
const rand=n=>Math.floor(Math.random()*n),shuf=a=>a.map(x=>[Math.random(),x]).sort((a,b)=>a[0]-b[0]).map(x=>x[1]);
const wait=ms=>new Promise(r=>setTimeout(r,ms));
const cap=u=>u[0].toUpperCase()+u.slice(1);
const units=w=>w.match(/ll|ch|[a-zñ]/g);
const sylsTo=i=>LV.slice(0,i+1).flatMap(l=>l.s);
const pw=s=>(s||'').split(' ').filter(Boolean).map(x=>{const w=x.match(/^[a-zñ]+/)[0];return[w,x.slice(w.length)]});
const LV=ORDER.map(u=>({u,g:u,w:pw(WD[u]),s:(SYL[u]||'').split(' ').filter(Boolean)})).concat(EXTRA.map(e=>({u:e.t,g:e.g,x:1,w:pw(e.w),s:e.s.split(' ')})));
function speak(t,rate=.8){return new Promise(r=>{try{speechSynthesis.cancel();const u=new SpeechSynthesisUtterance(t);u.lang='es-ES';u.rate=rate;const v=speechSynthesis.getVoices().find(v=>v.lang.startsWith('es'));if(v)u.voice=v;u.onend=r;u.onerror=r;speechSynthesis.speak(u)}catch(e){r()}})}
const say=(k,t,r)=>AUD[k]?new Promise(res=>{try{const a=new Audio(AUD[k]);a.onended=res;a.onerror=res;a.play().catch(res)}catch(e){res()}}):speak(t,r);
const snd=u=>say('l:'+u,SND[u]||u,.6),wd=w=>say('w:'+w,w,.65);
const norm=s=>s.normalize('NFD').replace(/[\u0300-\u036f]/g,'').toLowerCase().replace(/[^a-z ]/g,'').trim();
let P;try{P=JSON.parse(localStorage.getItem('ar2'))}catch(e){}
if(!P||!P.ps)P={ps:[],c:-1};
const save=()=>{try{localStorage.setItem('ar2',JSON.stringify(P))}catch(e){}};
const pr=()=>P.ps[P.c];
// Repaso espaciado: caja 0-5; intervalos: ya, 10 min, 1 día, 3 días, 7 días, 14 días
const INT=[0,6e5,864e5,2592e5,6048e5,12096e5];
const stat=u=>(pr().s=pr().s||{})[u]||{b:0,d:0};
function rec(u,ok){const p=pr();p.s=p.s||{};const s=stat(u);s.b=ok?Math.min(s.b+1,5):0;s.d=Date.now()+INT[s.b];p.s[u]=s;save()}
let lastT=null;
function nextLetter(known){const now=Date.now(),ok=known.filter(u=>u!==lastT||known.length==1),due=ok.filter(u=>stat(u).d<=now);let t;
 if(due.length){const w=due.map(u=>6-stat(u).b);let r=Math.random()*w.reduce((a,b)=>a+b,0),k=0;while((r-=w[k])>0)k++;t=due[k]}
 else t=ok.slice().sort((a,b)=>stat(a).d-stat(b).d)[0];
 lastT=t;return t}
function setTheme(t){document.documentElement.dataset.theme=t;try{localStorage.setItem('arth',t)}catch(e){}$('#th').textContent=t=='dark'?'☀️ Claro':'🌙 Oscuro'}
let th='light';try{th=localStorage.getItem('arth')||'light'}catch(e){}
let T=0;
const draw=h=>{T++;try{speechSynthesis.cancel()}catch(e){}app.innerHTML=h;return T};
const BACK='<button class="back" onclick="home()">← Inicio</button>';
const fb=(t,c)=>{const e=$('#fb');if(e){e.textContent=t;e.className='fb '+(c||'')}};
function hdr(){const p=pr();$('#hd').innerHTML=p?`<button class="back" onclick="profiles()">👤 ${p.n}</button><span id="stars">⭐ ${p.st}</span>`:''}
const star=()=>{pr().st++;save();hdr()};

function profiles(){T++;hdr();
 app.innerHTML=`<div class="stage"><h2>¿Quién va a leer?</h2><div class="menu">${P.ps.map((p,i)=>`<button class="big" onclick="pick(${i})"><i>🧒</i><div><b>${p.n}</b><span>Va por: ${cap(LV[p.lv].g)} · ⭐ ${p.st}</span></div></button>`).join('')}</div><div class="row"><input id="nm" maxlength="20" placeholder="Nombre del niño o niña" aria-label="Nombre"><button class="btn" onclick="addP()">Crear perfil</button></div></div>`}
function pick(i){P.c=i;save();home()}
function addP(){const n=$('#nm').value.replace(/[<>&"'`]/g,'').trim();if(!n)return;P.ps.push({n,lv:0,st:0});P.c=P.ps.length-1;save();home()}

function home(){const p=pr();if(!p)return profiles();hdr();const n=dueList().length;
 draw(`<div class="stage in"><div class="pic">👋</div><h2 style="margin:8px 0 0">¡Hola, ${p.n}!</h2></div><div class="menu" style="margin-top:14px"><button class="big go in" style="animation-delay:.1s" onclick="level(${p.lv})"><i>▶️</i><div><b>Aprender</b><span>${p.st?'Seguir':'Empezar'}: ${cap(LV[p.lv].g)}</span></div></button><button class="big in" style="animation-delay:.2s" onclick="practice()"><i>🎮</i><div><b>Practicar</b><span>Juega con lo que ya sabes</span></div></button>${n?`<button class="big in" style="animation-delay:.3s" onclick="review()"><i>🔁</i><div><b>Repaso de hoy</b><span>${n} para recordar</span></div></button>`:''}</div><div class="row in" style="animation-delay:.4s"><button class="btn alt sm" onclick="map()">🗺️ Mapa de letras</button><button class="btn alt sm" onclick="adults()">🔒 Adultos</button></div>`)}
function dueList(){const n=Date.now();return Object.entries(pr().s||{}).filter(([k,v])=>v.d<=n).map(x=>x[0])}
function review(){const ks=shuf(dueList()).slice(0,6),all=sylsTo(pr().lv);let n=0;
 const nx=()=>{if(n>=ks.length)return draw(BACK+'<div class="stage"><div class="pic">🌟</div><h2>¡Repaso hecho!</h2><div class="row"><button class="btn" onclick="home()">Inicio</button></div></div>');
  const k=ks[n++];ORDER.includes(k)?itemChoose(pr().lv,nx,k):itemSylChoose([k],all,nx)};nx()}
function adults(){const a=3+rand(6),b=4+rand(6);draw(BACK+`<div class="stage"><h2>Zona de adultos</h2><p>¿Cuánto es ${a} + ${b}?</p><div class="row"><input id="ans" inputmode="numeric" aria-label="Respuesta"><button class="btn" id="ok">Entrar</button></div><div class="fb" id="fb"></div></div>`);
 $('#ok').onclick=()=>+$('#ans').value==a+b?panel():fb('Respuesta incorrecta','no')}
function panel(){const p=pr(),weak=Object.entries(p.s||{}).filter(([k,v])=>v.b<=1).map(x=>x[0]).join(' · ')||'—';
 draw(BACK+`<div class="stage" style="text-align:left"><h2>${p.n}</h2><p>Nivel actual: <b>${LV[p.lv].g}</b> (${p.lv+1} de ${LV.length})<br>Estrellas: <b>${p.st}</b><br>Les cuestan: <b>${weak}</b></p><div class="row"><button class="btn alt" onclick="sure(this,resetP)">Reiniciar progreso</button><button class="btn rec" onclick="sure(this,delP)">Borrar perfil</button></div><div class="row"><button class="btn alt sm" onclick="micTest()">🎤 Probar micrófono</button></div><div class="fb" id="fb" style="white-space:pre-line"></div></div>`)}
async function micTest(){const o=[];
 o.push('Dentro de otra página: '+(window.top!==window?'sí':'no'));
 try{const pp=document.permissionsPolicy||document.featurePolicy;o.push('Política de la página: '+(pp&&pp.allowsFeature?(pp.allowsFeature('microphone')?'micrófono permitido':'micrófono NO permitido'):'sin datos'))}catch(e){o.push('Política de la página: sin datos')}
 try{const s=await navigator.permissions.query({name:'microphone'});o.push('Permiso de Chrome: '+s.state)}catch(e){o.push('Permiso de Chrome: sin datos')}
 try{const st=await navigator.mediaDevices.getUserMedia({audio:true});st.getTracks().forEach(t=>t.stop());o.push('Micrófono: funciona ✔')}catch(e){o.push('Micrófono: '+e.name)}
 fb(o.join('\n'))}
function sure(b,f){if(b.dataset.s)return f();b.dataset.s=1;b.textContent='¿Seguro? Pulsa otra vez'}
function resetP(){const p=pr();p.lv=0;p.st=0;p.s={};save();home()}
function delP(){P.ps.splice(P.c,1);P.c=-1;save();profiles()}
function map(){const p=pr();draw(BACK+`<p class="fb">Elige un nivel</p><div class="grid">${LV.map((l,i)=>`<button class="k${i==p.lv?' cur':''}" ${i>p.lv?'disabled aria-label="bloqueada"':''} onclick="level(${i})">${i>p.lv?'🔒':l.g}</button>`).join('')}</div><div class="row" style="margin-top:18px"><button class="btn" onclick="practice()">🎮 Practicar</button></div>`)}

function level(i){const L=LV[i],u=L.u;const my=draw(BACK+`<div class="stage"><div class="fb">${L.x?'Nuevo reto':'Letra nueva'}</div><div class="pic" style="font-size:${L.x?'2rem':'4.5rem'}">${L.x?u:cap(u)+' '+u}</div><div class="row">${L.x?'':'<button class="btn alt" id="h">🔊 Escuchar</button>'}<button class="btn" id="go">Empezar ➜</button></div></div>`);
 if(!L.x){$('#h').onclick=()=>snd(u);snd(u)}$('#go').onclick=()=>run(i)}

function run(i){const reads=shuf(LV[i].w).slice(0,4);let n=0,h=0;lastT=null;const S=LV[i].s,all=sylsTo(i),syl=S.length?[d=>itemSylIntro(i,d),...[0,1,2,3].map(()=>d=>itemSylChoose(S,all,d)),...shuf(S).slice(0,2).map(s=>d=>itemBuild(s,'',d))]:[];const C=TX.filter(t=>t.l<=i),P1=C.filter(t=>t.l==i),pk=P1.length?P1:C,txs=i>=FR_FROM&&C.length?[d=>itemText(pk[rand(pk.length)],d)]:[];
 const steps=[0,1,2,3].slice(0,LV[i].x?0:i?4:2).map(()=>d=>itemChoose(i,d)).concat(syl,reads.map(r=>d=>itemRead(r[0],r[1],ok=>{if(ok)h++;d()})),txs);
 const nx=()=>{if(n<steps.length)steps[n++](nx);else end()};
 function end(){const p=pr(),ok=!reads.length||h>=Math.ceil(reads.length*PASS);
  if(ok&&i==p.lv&&i<LV.length-1){p.lv++;save()}
  const last=i>=LV.length-1;
  draw(BACK+(ok?`<div class="stage"><div class="pic">🎉</div><h2>¡Nivel superado!</h2><div class="row">${last?'':`<button class="btn" onclick="level(${i+1})">Siguiente: ${cap(LV[i+1].g)}</button>`}<button class="btn alt" onclick="home()">Inicio</button></div></div>`:`<div class="stage"><div class="pic">💪</div><h2>Casi. Vamos otra vez.</h2><div class="row"><button class="btn" onclick="run(${i})">Repetir</button></div></div>`))}
 nx()}

function itemChoose(i,d,f){const known=ORDER.slice(0,i+1),pool=known.slice();for(let k=0;pool.length<3;k++)if(!pool.includes(ORDER[k]))pool.push(ORDER[k]);
 const t=f||nextLetter(known);let miss=false;
 const o=shuf([t,...shuf(pool.filter(x=>x!==t)).slice(0,2)]);
 const my=draw(BACK+`<div class="stage"><p class="fb" style="margin:0">¿Qué letra suena?</p><div class="row"><button class="btn" id="h">🔊 Escuchar</button></div><div class="grid" style="grid-template-columns:repeat(3,1fr);margin-top:16px">${o.map((u,k)=>`<button class="k" id="o${k}">${u}</button>`).join('')}</div><div class="fb" id="fb"></div></div>`);
 $('#h').onclick=()=>snd(t);snd(t);
 o.forEach((u,k)=>$('#o'+k).onclick=async()=>{if(u==t){if(!miss)rec(t,true);star();fb('¡Sí!','ok');await wait(700);if(my===T)d()}else{const b=$('#o'+k);b.classList.add('shake');setTimeout(()=>b.classList.remove('shake'),300);if(!miss){miss=true;rec(t,false)}fb('Escucha otra vez','no')}})}

function itemSylIntro(i,d){const L=LV[i].s;
 const my=draw(BACK+`<div class="stage"><p class="fb" style="margin:0">Toca y escucha cómo se juntan los sonidos</p><div class="grid" style="grid-template-columns:repeat(3,1fr);margin-top:14px">${L.map((s,k)=>`<button class="k" id="y${k}" style="font-size:1.8rem">${s}</button>`).join('')}</div><div class="row"><button class="btn" id="n">Seguir ➜</button></div></div>`);
 L.forEach((s,k)=>$('#y'+k).onclick=async()=>{for(const u of units(s)){if(my!==T)return;await snd(u);await wait(100)}if(my===T)await say('s:'+s,s,.7)});$('#n').onclick=()=>d()}
function itemSylChoose(pool,all,d){const t=nextLetter(pool),U=units(t);let
