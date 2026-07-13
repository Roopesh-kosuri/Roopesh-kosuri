<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Roopesh • Portfolio</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{
font-family:Inter,Arial,sans-serif;color:#fff;background:#050816;overflow-x:hidden}
#bg{
position:fixed;inset:0;z-index:-2;
background:linear-gradient(-45deg,#0b1020,#111827,#172554,#0f172a);
background-size:400% 400%;
animation:grad 16s ease infinite}
@keyframes grad{0%{background-position:0 50%}50%{background-position:100% 50%}100%{background-position:0 50%}}
canvas{position:fixed;inset:0;z-index:-1}
nav{
position:fixed;top:16px;left:50%;transform:translateX(-50%);
backdrop-filter:blur(14px);
background:rgba(255,255,255,.08);
padding:12px 22px;border-radius:999px;border:1px solid rgba(255,255,255,.15)}
nav a{color:#fff;text-decoration:none;margin:0 12px}
.hero{min-height:100vh;display:grid;place-items:center;text-align:center;padding:20px}
h1{font-size:clamp(3rem,8vw,6rem)}
.gradtxt{
background:linear-gradient(90deg,#7dd3fc,#a78bfa,#34d399);
-webkit-background-clip:text;color:transparent}
.type{font-size:1.3rem;opacity:.9;height:32px}
.btns{margin-top:28px;display:flex;gap:16px;justify-content:center;flex-wrap:wrap}
.btn{
padding:14px 26px;border-radius:14px;border:1px solid rgba(255,255,255,.2);
background:rgba(255,255,255,.08);color:#fff;text-decoration:none;
transition:.3s}
.btn:hover{transform:translateY(-4px) scale(1.03);background:rgba(255,255,255,.16)}
section{max-width:1100px;margin:auto;padding:90px 20px}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:24px}
.card{
background:rgba(255,255,255,.07);
backdrop-filter:blur(12px);
border:1px solid rgba(255,255,255,.12);
border-radius:22px;padding:24px;
transition:.35s;transform-style:preserve-3d}
.card:hover{transform:rotateX(6deg) rotateY(-6deg) translateY(-8px)}
.bar{height:10px;background:#1f2937;border-radius:99px;margin-top:10px}
.fill{height:100%;border-radius:99px;background:linear-gradient(90deg,#38bdf8,#8b5cf6)}
footer{text-align:center;padding:40px;opacity:.7}
.reveal{opacity:0;transform:translateY(30px);transition:1s}
.reveal.show{opacity:1;transform:none}
</style>
</head>
<body>
<div id="bg"></div>
<canvas id="c"></canvas>

<nav>
<a href="#about">About</a>
<a href="#skills">Skills</a>
<a href="#projects">Projects</a>
</nav>

<div class="hero">
<div>
<h1 class="gradtxt">ROOPESH</h1>
<div class="type" id="type"></div>
<div class="btns">
<a class="btn" href="#">GitHub</a>
<a class="btn" href="#">LinkedIn</a>
</div>
</div>
</div>

<section id="about" class="reveal">
<h2>About Me</h2><br>
<p>AI Developer • Game Developer • Defense Tech Enthusiast. Building modern software with clean design and smooth experiences.</p>
</section>

<section id="skills" class="reveal">
<h2>Skills</h2><br>
<div class="grid">
<div class="card"><h3>Python</h3><div class="bar"><div class="fill" style="width:90%"></div></div></div>
<div class="card"><h3>AI / ML</h3><div class="bar"><div class="fill" style="width:85%"></div></div></div>
<div class="card"><h3>Unity</h3><div class="bar"><div class="fill" style="width:75%"></div></div></div>
</div>
</section>

<section id="projects" class="reveal">
<h2>Projects</h2><br>
<div class="grid">
<div class="card"><h3>FogWatch</h3><p>Psychological survival horror game.</p></div>
<div class="card"><h3>AI Assistant</h3><p>Desktop AI with automation.</p></div>
<div class="card"><h3>Portfolio</h3><p>Animated premium website.</p></div>
</div>
</section>

<footer>© 2026 Roopesh Ram Varma Kosuri</footer>

<script>
const words=["AI Developer","Game Developer","AIML Student","Future Builder"];
let wi=0,ci=0,del=false;
const t=document.getElementById("type");
setInterval(()=>{
let w=words[wi];
if(!del){ci++; if(ci>w.length){del=true;setTimeout(()=>{},500)}}
else{ci--; if(ci==0){del=false;wi=(wi+1)%words.length}}
t.textContent=w.slice(0,ci);
},100);

const obs=new IntersectionObserver(es=>es.forEach(e=>e.target.classList.toggle("show",e.isIntersecting)),{threshold:.2});
document.querySelectorAll(".reveal").forEach(x=>obs.observe(x));

const c=document.getElementById("c"),ctx=c.getContext("2d");
function rs(){c.width=innerWidth;c.height=innerHeight}rs();onresize=rs;
let pts=[...Array(90)].map(()=>({x:Math.random()*c.width,y:Math.random()*c.height,vx:(Math.random()-.5)*0.5,vy:(Math.random()-.5)*0.5}));
function draw(){
ctx.clearRect(0,0,c.width,c.height);
for(let p of pts){
p.x+=p.vx;p.y+=p.vy;
if(p.x<0||p.x>c.width)p.vx*=-1;
if(p.y<0||p.y>c.height)p.vy*=-1;
ctx.beginPath();ctx.arc(p.x,p.y,2,0,7);ctx.fillStyle="white";ctx.fill();
}
for(let i=0;i<pts.length;i++)for(let j=i+1;j<pts.length;j++){
let a=pts[i],b=pts[j],d=Math.hypot(a.x-b.x,a.y-b.y);
if(d<120){ctx.strokeStyle="rgba(255,255,255,"+(1-d/120)*.15+")";ctx.beginPath();ctx.moveTo(a.x,a.y);ctx.lineTo(b.x,b.y);ctx.stroke();}
}
requestAnimationFrame(draw)}
draw();
</script>
</body>
</html>
