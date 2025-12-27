<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>Soikat Mondal</title>

<style>
html,body{
  margin:0;padding:0;
  width:100%;height:100%;
  overflow:hidden;
  background:#020205;
  display:flex;
  justify-content:center;
  align-items:center;
  font-family:'Segoe UI',sans-serif;
}
.bg-animation{
  position:absolute;inset:0;
  background:
    linear-gradient(transparent 95%,rgba(0,255,200,.1) 50%),
    linear-gradient(90deg,transparent 95%,rgba(100,0,255,.1) 50%);
  background-size:30px 30px;
  animation:moveGrid 15s linear infinite;
}
@keyframes moveGrid{
  from{background-position:0 0}
  to{background-position:30px 30px}
}
.iframe-box{
  width:100%;max-width:450px;height:98%;
  background:#000;border-radius:15px;
  border:3px solid #00ffff;
  box-shadow:0 0 20px #00ffff,inset 0 0 20px #00ffff;
  animation:boxPulse 2s infinite alternate;
  z-index:5;
}
@keyframes boxPulse{
  from{box-shadow:0 0 15px #00ffff}
  to{box-shadow:0 0 40px #00ffff}
}
iframe{width:100%;height:100%;border:none}
.box-container{
  position:fixed;
  top:80px;left:30px;
  width:160px;
  z-index:9999;
  cursor:grab;
  touch-action:none;
}
.box-container::before{
  content:'';
  position:absolute;inset:-3px;
  background:linear-gradient(45deg,#ff0000,#ff00de,#0011ff,#00eeff,#00ff22,#ffee00);
  background-size:400%;
  filter:blur(6px);
  border-radius:25px;
  animation:glowing 8s linear infinite;
  z-index:-1;
}
@keyframes glowing{
  0%{background-position:0 0}
  50%{background-position:400% 0}
  100%{background-position:0 0}
}
.box{
  background:rgba(10,10,20,.95);
  border-radius:25px;
  padding:12px 5px;
  text-align:center;
  color:#fff;
}
.profile-pic{
  width:45px;height:45px;
  border-radius:50%;
  border:2px solid #00ffff;
  box-shadow:0 0 8px #00ffff;
}
.title{
  font-size:11px;font-weight:800;
  background:linear-gradient(to right,#00ffff,#ff00ff);
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
  margin:8px 0;
}
#loginPart input{
  width:80%;padding:5px;
  background:#000;border:1px solid #00ffff;
  border-radius:15px;
  color:#fff;font-size:11px;
  text-align:center;
}
button,.btn-telegram{
  width:85%;padding:5px 0;
  border-radius:15px;border:none;
  font-size:10px;font-weight:bold;
  margin-top:5px;cursor:pointer;
}
.btn-login{background:linear-gradient(90deg,#00ffff,#0066ff);color:#000}
.btn-telegram{background:linear-gradient(90deg,#ff0055,#ff4400);color:#fff}
#wrong{color:#ff3333;font-size:9px;display:none}
.signal-box{
  background:rgba(255,255,255,.05);
  border-radius:15px;
  padding:5px;
}
.signal{
  font-size:18px;font-weight:900;margin:3px 0;
}
.countdown{font-size:14px;font-weight:bold;color:yellow}
</style>
</head>

<body>

<div class="bg-animation"></div>

<div class="iframe-box">
  <iframe src="https://hgnice.cc/#/register?invitationCode=473341624762"></iframe>
</div>

<div class="box-container" id="signalBox">
  <div class="box">
    <img src="https://image2url.com/images/1766337349984-8212453d-649a-44d5-ab22-944945c6125e.jpg" class="profile-pic">
    <div class="title">✰•° Kᴀʟᴀʀ☠️Tʀᴀᴅᴇ °•✰</div>

    <div id="loginPart">
      <input id="passInput" placeholder="Password">
      <button class="btn-login" onclick="attemptLogin()">LOGIN</button>
      <a href="https://t.me/+42zejxTnR2NkZTll" target="_blank" class="btn-telegram">TELEGRAM</a>
      <div id="wrong">WRONG PASS!</div>
    </div>

    <div id="signalPart" style="display:none">
      <div class="signal-box">
        <div style="font-size:8px">RESULT</div>
        <div class="signal" id="predicted">WAIT</div>
        <div class="countdown"><span id="countdown">30</span>s</div>
      </div>
    </div>
  </div>
</div>

<audio id="sound" src="https://actions.google.com/sounds/v1/alarms/beep_short.ogg" preload="auto"></audio>

<script>
/* Login */
const correctPassword="Soikat@#12";
const sound=document.getElementById("sound");
function attemptLogin(){
  if(passInput.value===correctPassword){
    loginPart.style.display="none";
    signalPart.style.display="block";
    sound.play().then(()=>sound.pause());
    startSignal();
  }else{
    wrong.style.display="block";
    setTimeout(()=>wrong.style.display="none",1500);
  }
}

/* Drag */
const box=document.getElementById("signalBox");
let drag=false,ox=0,oy=0;
const ignore=e=>["INPUT","BUTTON","A"].includes(e.target.tagName);
box.addEventListener("mousedown",e=>{
  if(ignore(e))return;
  drag=true;
  ox=e.clientX-box.offsetLeft;
  oy=e.clientY-box.offsetTop;
});
document.addEventListener("mousemove",e=>{
  if(!drag)return;
  box.style.left=(e.clientX-ox)+"px";
  box.style.top=(e.clientY-oy)+"px";
});
document.addEventListener("mouseup",()=>drag=false);
box.addEventListener("touchstart",e=>{
  if(ignore(e))return;
  drag=true;
  let t=e.touches[0];
  ox=t.clientX-box.offsetLeft;
  oy=t.clientY-box.offsetTop;
});
document.addEventListener("touchmove",e=>{
  if(!drag)return;
  let t=e.touches[0];
  box.style.left=(t.clientX-ox)+"px";
  box.style.top=(t.clientY-oy)+"px";
},{passive:false});
document.addEventListener("touchend",()=>drag=false);

/* ===== HEALTHY RANDOM CORE (HIDDEN) ===== */
const todaySeed = new Date().toDateString();
let history = JSON.parse(localStorage.getItem("hx_"+todaySeed) || "[]");

function remember(type){
  history.push(type);
  if(history.length>8) history.shift();
  localStorage.setItem("hx_"+todaySeed, JSON.stringify(history));
}

function pickType(){
  let big = history.filter(x=>x==="BIG").length;
  let small = history.filter(x=>x==="SMALL").length;

  if(big - small >= 2) return "SMALL";
  if(small - big >= 2) return "BIG";

  // light randomness
  return Math.random() < 0.52 ? "BIG" : "SMALL";
}

/* Signal */
let current=-1;
function startSignal(){requestAnimationFrame(loop);}
function loop(){
  let now=Date.now();
  let id=Math.floor(now/30000);
  if(id!==current){current=id;generateSignal();}
  countdown.innerText=Math.ceil(30-(now%30000)/1000);
  requestAnimationFrame(loop);
}

function generateSignal(){
  let type = pickType();

  let bigNums=["5","6","7","8","9"];
  let smallNums=["0","1","2","3","4"];
  let nums = type==="BIG"?bigNums:smallNums;

  let a = nums[Math.floor(Math.random()*nums.length)];
  let b = nums[Math.floor(Math.random()*nums.length)];

  predicted.innerText = type+" "+a+","+b;

  if(type==="BIG"){
    predicted.style.color="#00ff3c";
    predicted.style.textShadow="0 0 6px #00ff3c,0 0 15px #00ff3c";
  }else{
    predicted.style.color="#ff2a2a";
    predicted.style.textShadow="0 0 6px #ff2a2a,0 0 15px #ff2a2a";
  }

  remember(type);
  sound.currentTime=0;
  sound.play().catch(()=>{});
}
</script>

</body>
</html>
