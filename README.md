<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#fff3f7">
<title>Hello Kitty · El pueblito de Rue</title>
<style>
*{box-sizing:border-box}
[hidden]{display:none!important}
html,body{margin:0;height:100%;overscroll-behavior:none}
body{min-height:100dvh;display:flex;flex-direction:column;padding:18px;gap:14px;color:#765762;background:radial-gradient(ellipse at top left,#ffe4ef,transparent 60%),#fff5f8;font-family:ui-rounded,"Trebuchet MS",sans-serif}
button{font:inherit;cursor:pointer;color:inherit;-webkit-tap-highlight-color:transparent}
button:focus-visible,canvas:focus-visible{outline:3px solid #bf8bd0;outline-offset:3px}
.top{display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap;padding:0 8px}
.brand{display:flex;gap:12px;align-items:center}
.logo{display:grid;place-items:center;width:52px;height:52px;background:white;border-radius:18px;font-size:30px;box-shadow:0 4px 0 #f2d9e3}
.eyebrow{font-size:10px;letter-spacing:2px;font-weight:bold;color:#bc8c9f}
h1{font-size:24px;margin:5px 0 0;letter-spacing:-.8px}
.actions{display:flex;gap:8px}
.soft{border:1px solid #efd1dd;background:#fff9fc;border-radius:14px;padding:10px 13px;font-size:12px}
.scene{position:relative;flex:1;min-height:360px;overflow:hidden;border:5px solid #fff;border-radius:26px;background:#d9edcf;box-shadow:0 12px 35px #b877971a}
canvas{display:block;width:100%;height:100%;position:absolute;inset:0;touch-action:none}
.hud{position:absolute;top:18px;left:18px;background:#fffaf2ef;border:1px solid #fff;border-radius:20px;padding:16px 18px;width:235px;box-shadow:0 5px 20px #816b7420;pointer-events:none}
.hud-title{font-size:10px;letter-spacing:1.7px;color:#bb8fa1;font-weight:bold}
.counter{display:flex;align-items:center;justify-content:space-between;margin:8px 0;font-size:15px;font-weight:bold}
.counter strong{color:#d6779c}
.track{height:7px;border-radius:8px;background:#f3e0e7;overflow:hidden}
#progress{height:100%;background:#e897b5;border-radius:8px;transition:width .3s}
.collection{display:flex;justify-content:space-between;font-size:11px;gap:5px;margin-top:11px;white-space:nowrap}
.corner{position:absolute;top:20px;right:20px;padding:9px 13px;border-radius:20px;background:#fffaf2da;font-size:11px;color:#879579;pointer-events:none}
.toast{position:absolute;top:129px;left:50%;transform:translate(-50%,-6px);opacity:0;transition:.2s;background:#fffaf3f5;border:1px solid #f1d9e4;padding:12px 18px;border-radius:18px;font-size:13px;text-align:center;max-width:85%;pointer-events:none;box-shadow:0 5px 15px #9b738f15}
.toast.visible{opacity:1;transform:translate(-50%,0)}
.sign-hint{position:absolute;bottom:24px;left:50%;transform:translateX(-50%);border-radius:18px;background:#fff8f1f2;border:2px solid #edc3d4;padding:12px 21px;text-align:center;pointer-events:none;white-space:nowrap}
.sign-hint small{display:block;color:#b692a1;font-size:10px;margin-bottom:4px}
.sign-hint strong{font-size:17px}
.overlay{position:absolute;inset:0;display:grid;place-items:center;padding:20px;background:#fff4f773;backdrop-filter:blur(4px);z-index:3}
.panel{text-align:center;max-width:395px;padding:27px 32px;background:#fffaf6;border:3px solid white;border-radius:30px;box-shadow:0 15px 50px #976b8c25}
.big-bow{font-size:56px;animation:float 3s ease-in-out infinite}
.panel h2{font-size:29px;letter-spacing:-1px;line-height:1.1;margin:16px 0 12px}
.panel p{font-size:14px;line-height:1.65;margin:10px 0 20px;color:#a0808e}
.pill{display:inline-block;padding:7px 12px;border-radius:20px;background:#f9e6ef;font-size:11px;color:#b67895}
.primary{background:#df88ac;color:white;border:0;border-radius:17px;padding:13px 24px;font-weight:bold;box-shadow:0 4px 0 #c87296}
.primary:active{transform:translateY(2px);box-shadow:0 2px 0 #c87296}
.controls{display:none;position:absolute;right:18px;bottom:18px;grid-template-columns:repeat(3,44px);grid-template-rows:repeat(3,44px);gap:4px;touch-action:none;user-select:none;-webkit-user-select:none}
.controls button{border:2px solid white;border-radius:14px;background:#fff7f1e8;font-size:18px;box-shadow:0 3px 0 #c8b3b85c;touch-action:none}
.controls button:active{background:#f5bfd5;transform:translateY(2px)}
.up{grid-area:1/2}.left{grid-area:2/1}.right{grid-area:2/3}.down{grid-area:3/2}
.pad-heart{grid-area:2/2;display:grid;place-items:center;color:#d982a6;font-size:19px}
footer{display:flex;justify-content:space-between;gap:8px;padding:0 10px;font-size:11px;color:#b28d9f;flex-wrap:wrap}
@keyframes float{50%{transform:translateY(-6px) rotate(4deg)}}
@media(pointer:coarse),(max-width:700px){
  .controls{display:grid}.sign-hint{bottom:172px}
}
@media(max-width:600px){
  body{padding:10px;gap:10px}.top{gap:10px;padding:2px}
  .logo{width:42px;height:42px;font-size:25px}
  h1{font-size:20px}.eyebrow{font-size:8px}.actions{margin-left:auto}
  .soft{padding:8px 10px;font-size:10px}
  .scene{border-radius:22px;min-height:350px}
  .hud{top:12px;left:12px;width:210px;padding:13px}.corner{display:none}
  .toast{top:119px;width:calc(100% - 24px);max-width:none;padding:10px;font-size:12px}
  .panel{padding:20px 22px}.panel h2{font-size:25px}.panel p{font-size:13px}
  footer{font-size:10px}.sign-hint{padding:10px 15px}
}
@media(prefers-reduced-motion:reduce){
  .big-bow{animation:none}.toast,#progress{transition:none}
}
</style>
</head>
<body>
<header class="top">
  <div class="brand">
    <div class="logo" aria-hidden="true">🎀</div>
    <div>
      <div class="eyebrow">HELLO KITTY · TU LUGAR FELIZ</div>
      <h1>El pueblito de Rue</h1>
    </div>
  </div>
  <div class="actions">
    <button id="sound" class="soft" aria-pressed="false">♫ Sonido: no</button>
    <button id="reset" class="soft" title="Empezar la colección de nuevo">↺ Nuevo paseo</button>
  </div>
</header>

<main class="scene" aria-label="Tu pueblito de Hello Kitty">
  <canvas id="world" tabindex="0" aria-label="Mueves a Hello Kitty con las flechas o WASD. Recoges tesoros al acercarte a ellos."></canvas>

  <div class="hud">
    <div class="hud-title">TU CESTITA DE TESOROS</div>
    <div class="counter">
      <span>Un poquito de magia</span>
      <strong><span id="count">0</span>/15</strong>
    </div>
    <div class="track"><div id="progress"></div></div>
    <div id="collection" class="collection"></div>
  </div>

  <div class="corner">✿ Paseas a tu ritmo</div>
  <div id="toast" class="toast" role="status" aria-live="polite"></div>

  <div id="signHint" class="sign-hint" hidden>
    <small>TE ACERCAS Y LEES…</small>
    <strong>♡ Rue estuvo aquí ♡</strong>
  </div>

  <div class="controls" role="group" aria-label="Controles para caminar">
    <button class="up" data-dir="arrowup" aria-label="Caminar hacia arriba">▲</button>
    <button class="left" data-dir="arrowleft" aria-label="Caminar hacia la izquierda">◀</button>
    <span class="pad-heart" aria-hidden="true">♡</span>
    <button class="right" data-dir="arrowright" aria-label="Caminar hacia la derecha">▶</button>
    <button class="down" data-dir="arrowdown" aria-label="Caminar hacia abajo">▼</button>
  </div>

  <div id="welcome" class="overlay">
    <div class="panel">
      <div class="big-bow" aria-hidden="true">🎀</div>
      <span class="pill">Un paseo contigo y Hello Kitty</span>
      <h2>Tu pequeño<br>rincón de felicidad</h2>
      <p>Tú llegas a un pueblito de casitas pastel y flores. Caminas con Hello Kitty, recoges quince tesoros y descubres carteles que dicen <b>“Rue estuvo aquí”</b>.</p>
      <button id="start" class="primary">Comenzar tu paseo ♡</button>
      <p style="margin:16px 0 0;font-size:11px">Usas WASD, las flechas o los botones táctiles.</p>
    </div>
  </div>

  <div id="finish" class="overlay" hidden>
    <div class="panel">
      <div class="big-bow" aria-hidden="true">🧺✨</div>
      <h2>¡Tu cesta está llena!</h2>
      <p>Has encontrado los quince tesoros y llenado tu paseo de cosas bonitas. El pueblito sigue esperándote.<br><b>Rue estuvo aquí ♡</b></p>
      <button id="continue" class="primary">Seguir paseando</button>
    </div>
  </div>
</main>

<footer>
  <span>♡ Caminas con WASD, flechas o controles táctiles.</span>
  <span>Tu paseo se guarda en este navegador.</span>
</footer>

<script>
'use strict';
const canvas = document.getElementById('world'), ctx = canvas.getContext('2d');
const $ = id => document.getElementById(id);
const W = 1800, H = 1280, KEY = 'rue-kitty-v1';

const houses = [
  {x:210,y:215,w:230,h:190,name:'Café Miau',wall:'#ffcedf',roof:'#ec8bac'},
  {x:765,y:175,w:250,h:195,name:'Casa del Lacito',wall:'#efe0ff',roof:'#b69add'},
  {x:1340,y:245,w:235,h:185,name:'La Pastelería',wall:'#fff0bf',roof:'#eead95'},
  {x:310,y:915,w:210,h:165,name:'La Florería',wall:'#d8f0dd',roof:'#91bfaa'}
];

const trees = [
  [140,145,1.2],[530,170,1],[650,355,.95],[1150,140,1.1],[1660,160,1.3],
  [1580,515,1.1],[160,575,1.1],[520,580,1],[1090,515,.95],[120,955,1.2],
  [210,1140,1],[650,1110,1.2],[970,1100,1],[1660,1110,1.1],[1700,850,1],[700,840,.9]
].map(([x,y,s],i)=>({x,y,s,pink:i%3!==0}));

const signs = [
  {x:570,y:485},{x:1040,y:810},{x:1550,y:1170},{x:220,y:800}
];

const types = [
  {icon:'🍓',name:'fresa'}, {icon:'🌼',name:'flor'}, {icon:'⭐',name:'estrella'},
  {icon:'🎀',name:'lacito'}, {icon:'🧁',name:'cupcake'}
];

const items = [
  [550,400,0],[370,520,0],[1490,550,0],[290,870,1],[600,990,1],[1080,1070,1],
  [1270,790,2],[1490,1180,2],[1390,1030,2],[560,210,3],[1040,340,3],[760,1040,3],
  [260,460,4],[1510,470,4],[880,900,4]
].map(([x,y,type],id)=>({x,y,type,id}));

const player = {x:900,y:795,step:0,moving:false};
const found = new Set(), keys = new Set(), touch = new Map(), particles = [];
const camera = {x:0,y:0};

let mode='welcome', cw=900, ch=600, zoom=1, dpr=1, time=0, last=0, saveTimer=0;
let audioContext=null, sound=false, toastTimer=0;
const clamp=(v,a,b)=>Math.max(a,Math.min(b,v));

function rr(x,y,w,h,r,fill,stroke){
  ctx.beginPath();ctx.roundRect(x,y,w,h,r);
  if(fill){ctx.fillStyle=fill;ctx.fill();}
  if(stroke){ctx.strokeStyle=stroke;ctx.lineWidth=2;ctx.stroke();}
}
function ellipse(x,y,rx,ry,color){
  ctx.beginPath();ctx.ellipse(x,y,rx,ry,0,0,Math.PI*2);
  ctx.fillStyle=color;ctx.fill();
}
function textAt(text,x,y,size=16,color='#765762'){
  ctx.font='600 '+size+'px ui-rounded, "Trebuchet MS", sans-serif';
  ctx.textAlign='center';ctx.textBaseline='middle';
  ctx.fillStyle=color;ctx.fillText(text,x,y);
}
function heart(x,y,s,color){
  ctx.save();ctx.translate(x,y);ctx.scale(s,s);ctx.beginPath();
  ctx.moveTo(0,5);ctx.bezierCurveTo(-18,-5,-9,-18,0,-8);
  ctx.bezierCurveTo(9,-18,18,-5,0,5);
  ctx.fillStyle=color;ctx.fill();ctx.restore();
}
function bow(x,y,s=1){
  ctx.save();ctx.translate(x,y);ctx.scale(s,s);
  ellipse(-9,0,11,9,'#e96596');ellipse(9,0,11,9,'#e96596');
  ellipse(-11,-2,5,4,'#fa9dba');ellipse(11,-2,5,4,'#fa9dba');
  ellipse(0,0,5,6,'#d84f85');ctx.restore();
}
function flower(x,y,s=1,color='#fff5fb'){
  for(let i=0;i<5;i++){
    const a=i*Math.PI*2/5;
    ellipse(x+Math.cos(a)*5*s,y+Math.sin(a)*5*s,4*s,4*s,color);
  }
  ellipse(x,y,3*s,3*s,'#f5cf73');
}
function rectHit(x,y,r,q){
  const dx=x-clamp(x,q.x,q.x+q.w),dy=y-clamp(y,q.y,q.y+q.h);
  return dx*dx+dy*dy<r*r;
}
function blocked(x,y){
  const r=17;
  if(x<30||x>W-30||y<30||y>H-30)return true;
  if(houses.some(h=>rectHit(x,y,r,{
    x:h.x+8,y:h.y+55,w:h.w-16,h:h.h-55
  })))return true;
  if(trees.some(t=>(x-t.x)**2+(y-t.y)**2<(r+16*t.s)**2))return true;
  if((x-900)**2+(y-625)**2<(r+59)**2)return true;
  if(x>1357&&x<1423)return false;
  const dx=x-clamp(x,1270,1500),dy=y-clamp(y,950,1030);
  return dx*dx+dy*dy<117*117;
}
function save(){
  try{
    localStorage.setItem(KEY,JSON.stringify({
      found:[...found],x:player.x,y:player.y
    }));
  }catch{}
}
try{
  const data=JSON.parse(localStorage.getItem(KEY)||'null');
  if(data){
    if(Array.isArray(data.found))data.found.forEach(id=>{
      if(Number.isInteger(id)&&id>=0&&id<items.length)found.add(id);
    });
    if(Number.isFinite(data.x)&&Number.isFinite(data.y)&&!blocked(data.x,data.y)){
      player.x=data.x;player.y=data.y;
    }
  }
}catch{}

function updateHUD(){
  $('count').textContent=found.size;
  $('progress').style.width=(found.size/items.length*100)+'%';
  $('collection').innerHTML=types.map((t,i)=>
    '<span>'+t.icon+' '+items.filter(v=>v.type===i&&found.has(v.id)).length+'/3</span>'
  ).join('');
}
function toast(message){
  $('toast').textContent=message;$('toast').classList.add('visible');
  clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>$('toast').classList.remove('visible'),3200);
}
function chime(complete=false){
  if(!sound||!audioContext)return;
  try{
    const start=audioContext.currentTime;
    (complete?[523,659,784,1047]:[659,880]).forEach((frequency,i)=>{
      const osc=audioContext.createOscillator(), gain=audioContext.createGain();
      osc.type='sine';osc.frequency.value=frequency;
      gain.gain.setValueAtTime(0,start+i*.09);
      gain.gain.linearRampToValueAtTime(.065,start+i*.09+.015);
      gain.gain.exponentialRampToValueAtTime(.001,start+i*.09+.3);
      osc.connect(gain);gain.connect(audioContext.destination);
      osc.start(start+i*.09);osc.stop(start+i*.09+.32);
    });
  }catch{}
}
function burst(x,y,big=false){
  for(let i=0;i<(big?70:16);i++)particles.push({
    x,y,vx:(Math.random()-.5)*(big?310:130),
    vy:-70-Math.random()*(big?260:90),
    life:big?2.5:1,max:big?2.5:1,
    color:['#ec8cac','#fff2bb','#b6a1df','#fff'][i%4]
  });
}
function clearInput(){
  keys.clear();touch.clear();player.moving=false;
}
function begin(){
  mode='play';$('welcome').hidden=true;clearInput();canvas.focus();
  toast(found.size?'Tu pueblito te estaba esperando.':'Llegas al pueblo. ¡Tu paseo comienza!');
}
$('start').addEventListener('click',begin);
$('continue').addEventListener('click',()=>{
  $('finish').hidden=true;mode='play';clearInput();canvas.focus();
  toast('Tu cesta está llena. Tú decides por dónde seguir paseando.');
});
$('reset').addEventListener('click',()=>{
  found.clear();player.x=900;player.y=795;particles.length=0;
  $('finish').hidden=true;updateHUD();save();
  if(mode!=='welcome'){
    mode='play';clearInput();canvas.focus();
    toast('Te espera un nuevo paseo y quince tesoros.');
  }
});
$('sound').addEventListener('click',()=>{
  try{
    if(!audioContext){
      const Audio=window.AudioContext||window.webkitAudioContext;
      if(!Audio)throw Error();
      audioContext=new Audio();
    }
    sound=!sound;
    if(sound)audioContext.resume().catch(()=>{});
    $('sound').setAttribute('aria-pressed',String(sound));
    $('sound').textContent=sound?'♫ Sonido: sí':'♫ Sonido: no';
    chime();
  }catch{toast('Puedes disfrutar de tu paseo sin sonido.');}
});

const validKeys=['arrowup','arrowdown','arrowleft','arrowright','w','a','s','d'];
window.addEventListener('keydown',e=>{
  const key=e.key.toLowerCase();
  if(mode==='play'&&validKeys.includes(key)){
    e.preventDefault();keys.add(key);
  }
});
window.addEventListener('keyup',e=>keys.delete(e.key.toLowerCase()));
window.addEventListener('blur',()=>{clearInput();save();});
document.addEventListener('visibilitychange',()=>{
  clearInput();save();last=0;
});

document.querySelectorAll('[data-dir]').forEach(button=>{
  button.addEventListener('pointerdown',e=>{
    e.preventDefault();
    if(mode!=='play')return;
    touch.set(e.pointerId,button.dataset.dir);
    button.setPointerCapture(e.pointerId);
  });
  const release=e=>touch.delete(e.pointerId);
  button.addEventListener('pointerup',release);
  button.addEventListener('pointercancel',release);
  button.addEventListener('lostpointercapture',release);
});

function resize(){
  const box=canvas.getBoundingClientRect();
  cw=box.width;ch=box.height;
  dpr=Math.min(window.devicePixelRatio||1,2);
  canvas.width=Math.round(cw*dpr);canvas.height=Math.round(ch*dpr);
  zoom=Math.max(.72,Math.min(1.1,cw/1050),cw/W,ch/H);
  camera.x=clamp(player.x-cw/zoom/2,0,Math.max(0,W-cw/zoom));
  camera.y=clamp(player.y-ch/zoom/2,0,Math.max(0,H-ch/zoom));
}
new ResizeObserver(resize).observe(canvas);
window.addEventListener('resize',resize);

const floor=document.createElement('canvas');
floor.width=W;floor.height=H;
const ground=floor.getContext('2d');

function makeGround(){
  ground.fillStyle='#d9edcf';ground.fillRect(0,0,W,H);
  let seed=42;
  const random=()=>{
    seed=(seed*1664525+1013904223)>>>0;
    return seed/4294967296;
  };
  for(let i=0;i<1800;i++){
    ground.fillStyle=i%3?'#c9e2bb':'#e9f3dc';
    ground.beginPath();
    ground.arc(random()*W,random()*H,1+random()*2,0,7);
    ground.fill();
  }
  function road(x,y,w,h){
    ground.beginPath();ground.roundRect(x,y,w,h,44);
    ground.fillStyle='#efdbba';ground.fill();
    ground.beginPath();ground.roundRect(x+5,y+5,w-10,h-10,40);
    ground.fillStyle='#fff2d9';ground.fill();
  }
  road(90,670,1610,100);
  road(850,90,100,1110);
  road(320,350,100,730);
  road(1400,350,100,430);
  road(300,1110,1250,80);

  ground.fillStyle='#fff2df';ground.beginPath();
  ground.ellipse(900,660,180,170,0,0,7);ground.fill();
  ground.strokeStyle='#efd0c2';ground.lineWidth=3;
  ground.beginPath();ground.ellipse(900,660,172,162,0,0,7);ground.stroke();

  ground.beginPath();ground.roundRect(1170,850,430,280,100);
  ground.fillStyle='#b0dbde';ground.fill();
  ground.lineWidth=10;ground.strokeStyle='#d2e6bc';ground.stroke();
  ground.beginPath();ground.roundRect(1181,861,408,258,92);
  ground.fillStyle='#c6e8e8';ground.fill();

  for(let i=0;i<12;i++){
    const x=1205+i%4*90,y=912+Math.floor(i/4)*60;
    ground.strokeStyle='#a4d3d9';ground.lineWidth=2;
    ground.beginPath();ground.moveTo(x,y);
    ground.quadraticCurveTo(x+14,y+6,x+29,y);ground.stroke();
  }

  ground.fillStyle='#ecd0a9';ground.fillRect(1340,820,100,330);
  for(let y=827;y<1148;y+=20){
    ground.strokeStyle='#d2ac8d';ground.lineWidth=2;
    ground.beginPath();ground.moveTo(1344,y);
    ground.lineTo(1436,y);ground.stroke();
  }
  ground.fillStyle='#fff4dd';
  ground.fillRect(1337,816,7,338);ground.fillRect(1436,816,7,338);
  for(let y=820;y<=1150;y+=55){
    ground.fillStyle='#fffaf2';
    ground.fillRect(1331,y,18,14);ground.fillRect(1431,y,18,14);
  }

  for(let row=0;row<2;row++)for(let col=0;col<7;col++){
    const x=1160+col*50,y=545+row*55;
    ground.beginPath();ground.roundRect(x,y,40,43,10);
    ground.fillStyle='#c8b293';ground.fill();
    for(let k=0;k<3;k++){
      const px=x+10+k*9,py=y+18+(k%2)*7;
      ground.fillStyle='#87b592';ground.beginPath();
      ground.ellipse(px,py,8,5,-.5,0,7);ground.fill();
      ground.fillStyle='#ee8da1';ground.beginPath();
      ground.arc(px,py+5,4,0,7);ground.fill();
    }
  }

  for(let i=0;i<370;i++){
    const x=random()*W,y=random()*H;
    const path=(y>660&&y<780)||(x>840&&x<960)||
      (x>310&&x<430&&y>340)||
      (x>1390&&x<1510&&y>340&&y<790)||
      (y>1100&&y<1200);
    if(path||(x>1150&&x<1615&&y>820&&y<1140)||
      houses.some(h=>x>h.x-20&&x<h.x+h.w+20&&y>h.y-20&&y<h.y+h.h+20))continue;
    const color=i%2?'#fff8ed':'#f5c4d8';
    for(let k=0;k<5;k++){
      const a=k*Math.PI*2/5;
      ground.fillStyle=color;ground.beginPath();
      ground.arc(x+Math.cos(a)*4,y+Math.sin(a)*4,3,0,7);ground.fill();
    }
    ground.fillStyle='#edc67e';ground.beginPath();
    ground.arc(x,y,2.5,0,7);ground.fill();
  }
  ground.font='600 18px "Trebuchet MS",sans-serif';
  ground.textAlign='center';ground.fillStyle='#88a17f';
  ground.fillText('Jardín de Fresas',1315,500);
  ground.fillText('Laguito Estrella',1385,1218);
  ground.fillText('Bosque de Algodón',200,1045);
}
makeGround();

function drawHouse(h){
  const {x,y,w,h:height}=h;
  ellipse(x+w/2,y+height+4,w*.55,15,'#9cbc9b55');
  rr(x,y+50,w,height-50,16,h.wall,'#ad8584');

  ctx.beginPath();ctx.moveTo(x-14,y+60);
  ctx.lineTo(x+w/2,y-8);ctx.lineTo(x+w+14,y+60);
  ctx.closePath();ctx.fillStyle=h.roof;ctx.fill();
  ctx.strokeStyle='#b5828e';ctx.lineWidth=3;ctx.stroke();
  bow(x+w/2,y+24,.9);

  rr(x+w/2-25,y+height-68,50,68,[24,24,0,0],'#fff7eb','#ad8584');
  ellipse(x+w/2+13,y+height-32,3,3,'#b48678');

  [x+40,x+w-40].forEach(wx=>{
    rr(wx-21,y+95,42,40,12,'#d7edf0','#ae9ba3');
    ctx.strokeStyle='#fff';ctx.lineWidth=3;ctx.beginPath();
    ctx.moveTo(wx,y+96);ctx.lineTo(wx,y+134);
    ctx.moveTo(wx-19,y+115);ctx.lineTo(wx+19,y+115);ctx.stroke();
    rr(wx-26,y+132,52,13,5,'#f5aac7');
    flower(wx-12,y+133,.7);flower(wx+12,y+133,.7);
  });

  rr(x+12,y+57,w-24,25,8,'#fff7ef');
  ctx.save();ctx.beginPath();
  ctx.roundRect(x+12,y+57,w-24,25,8);ctx.clip();
  for(let i=0;i<w/22;i++)rr(x+12+i*22,y+57,11,25,0,h.roof);
  ctx.restore();

  rr(x+w/2-77,y+height+9,154,27,13,'#fff7eb');
  textAt(h.name,x+w/2,y+height+23,14);
}
function drawTree(t){
  const {x,y,s}=t;
  ctx.save();ctx.translate(x,y);ctx.scale(s,s);
  ellipse(0,4,49,14,'#95b78b44');rr(-9,-62,18,65,7,'#bb977e');
  const c=t.pink?'#f2bfd1':'#a8d2b0';
  const highlight=t.pink?'#ffdae5':'#c3e3bb';
  ellipse(-28,-62,33,32,c);ellipse(28,-62,33,32,c);
  ellipse(0,-89,43,39,c);ellipse(-12,-101,27,20,highlight);
  if(t.pink){
    flower(-30,-70,.8);flower(23,-91,.8);flower(15,-49,.7);
  }
  ctx.restore();
}
function drawSign(s){
  rr(s.x-51,s.y-26,9,36,3,'#bf9783');
  rr(s.x+42,s.y-26,9,36,3,'#bf9783');
  rr(s.x-87,s.y-79,174,58,12,'#fff8ee','#dba1b7');
  heart(s.x-70,s.y-50,.5,'#e990b1');
  heart(s.x+70,s.y-50,.5,'#e990b1');
  textAt('Rue estuvo aquí',s.x,s.y-50,15);
  bow(s.x,s.y-82,.55);
}
function drawFountain(){
  ellipse(900,637,68,39,'#b6cdb055');
  ellipse(900,625,62,41,'#e5bdce');
  ellipse(900,618,56,34,'#fff4ee');
  ellipse(900,618,47,26,'#bae5ea');
  rr(889,574,22,41,8,'#fff3e6');
  ellipse(900,575,30,12,'#f8d9e4');
  heart(900,553,1.4,'#e58cac');
  for(let i=0;i<6;i++){
    const a=time*1.5+i*Math.PI/3;
    ellipse(900+Math.cos(a)*34,610+Math.sin(a)*14,2.5,4,'#fff');
  }
}
function drawKitty(){
  const {x,y,moving,step}=player;
  const walk=moving?Math.sin(step)*3:0;
  ctx.save();ctx.translate(x,y);

  ellipse(0,9,25,8,'#92768c33');
  ellipse(-9,4+walk,9,6,'#fff9fa');
  ellipse(9,4-walk,9,6,'#fff9fa');
  ellipse(-17,-8,7,11,'#fff');ellipse(17,-8,7,11,'#fff');

  ctx.beginPath();ctx.moveTo(-11,-19);ctx.lineTo(11,-19);
  ctx.lineTo(16,3);ctx.lineTo(-16,3);ctx.closePath();
  ctx.fillStyle='#ed8eb6';ctx.fill();
  heart(0,-7,.5,'#fff4ed');

  ctx.fillStyle='#fffdfb';ctx.strokeStyle='#c6a3b0';ctx.lineWidth=1.6;
  ctx.beginPath();ctx.moveTo(-25,-39);ctx.lineTo(-24,-60);
  ctx.lineTo(-10,-51);ctx.quadraticCurveTo(0,-56,11,-51);
  ctx.lineTo(24,-60);ctx.lineTo(25,-39);
  ctx.bezierCurveTo(36,-12,-36,-12,-25,-39);
  ctx.closePath();ctx.fill();ctx.stroke();

  ellipse(-10,-34,2.5,3.4,'#544348');
  ellipse(10,-34,2.5,3.4,'#544348');
  ellipse(0,-28,3.8,2.7,'#efc363');

  ctx.strokeStyle='#896d78';ctx.lineWidth=1.5;
  for(const side of [-1,1])for(let i=0;i<3;i++){
    ctx.beginPath();ctx.moveTo(side*20,-35+i*6);
    ctx.lineTo(side*31,-38+i*8);ctx.stroke();
  }
  bow(19,-49,.75);ctx.restore();
}
function drawItem(item){
  const bob=Math.sin(time*2.5+item.id)*4;
  ellipse(item.x,item.y+9,16,5,'#a98aaa28');
  ellipse(item.x,item.y-8+bob,21,21,'#fff8e6b8');
  textAt(types[item.type].icon,item.x,item.y-9+bob,27);
  const a=time*2+item.id;
  ellipse(item.x+Math.cos(a)*25,item.y-10+Math.sin(a)*20,2,2,'#fffdf7');
}

function step(dt){
  time+=dt;
  let dx=0,dy=0;
  const held=k=>keys.has(k)||[...touch.values()].includes(k);
  if(mode==='play'){
    dx=Number(held('d')||held('arrowright'))-
      Number(held('a')||held('arrowleft'));
    dy=Number(held('s')||held('arrowdown'))-
      Number(held('w')||held('arrowup'));
  }
  const length=Math.hypot(dx,dy);
  player.moving=length>0;
  if(length){
    dx=dx/length*205*dt;dy=dy/length*205*dt;
    if(!blocked(player.x+dx,player.y))player.x+=dx;
    if(!blocked(player.x,player.y+dy))player.y+=dy;
    player.step+=dt*13;
  }

  if(mode==='play'){
    items.forEach(item=>{
      if(!found.has(item.id)&&
        Math.hypot(item.x-player.x,item.y-player.y)<35){
        found.add(item.id);burst(item.x,item.y-10);
        updateHUD();save();chime();
        toast('Has encontrado '+(
          item.type===4?'un cupcake.':
          item.type===3?'un lacito.':
          'una '+types[item.type].name+'.'
        ));
        if(found.size===items.length){
          burst(player.x,player.y-35,true);chime(true);clearInput();
          mode='celebrate';
          $('finish').hidden=false;$('continue').focus();
        }
      }
    });
  }

  const near=signs.some(s=>
    Math.hypot(s.x-player.x,s.y-player.y)<130
  );
  $('signHint').hidden=!near;

  for(let i=particles.length-1;i>=0;i--){
    const p=particles[i];
    p.life-=dt;p.x+=p.vx*dt;p.y+=p.vy*dt;p.vy+=150*dt;
    if(p.life<=0)particles.splice(i,1);
  }

  camera.x+=(clamp(player.x-cw/zoom/2,0,Math.max(0,W-cw/zoom))-
    camera.x)*(1-Math.exp(-9*dt));
  camera.y+=(clamp(player.y-ch/zoom/2,0,Math.max(0,H-ch/zoom))-
    camera.y)*(1-Math.exp(-9*dt));

  saveTimer+=dt;
  if(saveTimer>1){
    if(player.moving)save();
    saveTimer=0;
  }
}

function render(){
  ctx.setTransform(dpr,0,0,dpr,0,0);
  ctx.clearRect(0,0,cw,ch);
  ctx.save();ctx.scale(zoom,zoom);
  ctx.translate(-camera.x,-camera.y);

  ctx.drawImage(floor,0,0);
  textAt('Plaza del Lacito',900,463,19,'#9e7c8d');

  const sprites=[
    ...houses.map(h=>({y:h.y+h.h,draw:()=>drawHouse(h)})),
    ...trees.map(t=>({y:t.y,draw:()=>drawTree(t)})),
    ...signs.map(s=>({y:s.y,draw:()=>drawSign(s)})),
    ...items.filter(i=>!found.has(i.id)).map(i=>({
      y:i.y,draw:()=>drawItem(i)
    })),
    {y:640,draw:drawFountain},
    {y:player.y,draw:drawKitty}
  ];
  sprites.sort((a,b)=>a.y-b.y).forEach(s=>s.draw());

  for(let i=0;i<7;i++){
    const x=300+i*215+Math.sin(time*.7+i)*35;
    const y=610+Math.cos(time*.5+i*2)*185;
    ctx.save();ctx.translate(x,y);
    const flap=.4+Math.abs(Math.sin(time*7+i))*.6;
    ellipse(-5*flap,0,6*flap,4,i%2?'#e9a4c6':'#c3a7df');
    ellipse(5*flap,0,6*flap,4,i%2?'#e9a4c6':'#c3a7df');
    ellipse(0,0,1.5,4,'#af89a4');ctx.restore();
  }
  particles.forEach(p=>{
    ctx.globalAlpha=p.life/p.max;heart(p.x,p.y,.4,p.color);
  });
  ctx.globalAlpha=1;ctx.restore();
}
function frame(stamp){
  const dt=last?Math.min((stamp-last)/1000,.04):0;
  last=stamp;
  if(!document.hidden)step(dt);
  render();requestAnimationFrame(frame);
}
updateHUD();resize();requestAnimationFrame(frame);
</script>
</body>
</html>
