# Smart.atten..
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Smart Attendance</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@600;800&family=Manrope:wght@400;500;700&display=swap" rel="stylesheet">
<style>
:root{--bg:#f4f3ff;--ink:#14122b;--mute:#5b5878;--card:#ffffff;--line:#dcd9f5;--mint:#0fb89b;--violet:#6a4cff;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0b0a1c;--ink:#eeeaff;--mute:#a09cc4;--card:#15133a;--line:#2a2766;--mint:#27e8c4;--violet:#8d78ff}}
:root[data-theme="dark"]{--bg:#0b0a1c;--ink:#eeeaff;--mute:#a09cc4;--card:#15133a;--line:#2a2766;--mint:#27e8c4;--violet:#8d78ff}
html{scroll-behavior:smooth;scroll-padding-top:env(safe-area-inset-top,0px)}
*,*::before,*::after{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:Manrope,system-ui,sans-serif;line-height:1.6}
h1,h2,h3{font-family:Syne,system-ui,sans-serif;line-height:1.05;margin:0}
a{color:inherit}
.btn{display:inline-block;padding:.9rem 1.5rem;border-radius:999px;font-weight:700;text-decoration:none;transition:transform .2s,box-shadow .2s}
.btn:focus-visible{outline:3px solid #fff;outline-offset:3px}
.btn.main{background:linear-gradient(120deg,#27e8c4,#8d78ff);color:#07061a;box-shadow:0 10px 40px -10px #27e8c4aa}
.btn.main:hover{transform:translateY(-2px)}
.btn.ghost{border:1px solid #ffffff44;color:#fff}
.btn.ghost:hover{background:#ffffff14}
/* hero is always dark */
.hero{position:relative;min-height:100vh;min-height:100svh;background:radial-gradient(120% 90% at 70% 40%,#241a66 0%,#0b0a1c 60%);color:#eeeaff;overflow:hidden;display:flex;align-items:center}
#stage{position:absolute;inset:0;width:100%;height:100%}
nav{position:absolute;top:0;left:0;right:0;display:flex;justify-content:space-between;align-items:center;padding:1.2rem clamp(1.2rem,5vw,4rem);z-index:3}
.logo{font-family:Syne,sans-serif;font-weight:800;font-size:1.2rem;text-decoration:none}
nav a.l{margin-left:1.4rem;text-decoration:none;color:#c9c4f0;font-weight:500}
nav a.l:hover{color:#fff}
.copy{position:relative;z-index:2;padding:6rem clamp(1.2rem,5vw,4rem) 7rem;max-width:44rem;pointer-events:none}
.copy a{pointer-events:auto}
.copy h1{font-size:clamp(2.8rem,8vw,5.8rem);font-weight:800;letter-spacing:-.02em}
.copy p{font-size:1.15rem;color:#c9c4f0;max-width:34rem;margin:1.4rem 0 2rem}
.cta{display:flex;gap:.8rem;flex-wrap:wrap}
.live{position:absolute;z-index:2;left:clamp(1.2rem,5vw,4rem);bottom:calc(1.8rem + env(safe-area-inset-bottom,0px));display:flex;align-items:center;gap:1rem;padding:.8rem 1.2rem;border-radius:16px;background:#ffffff12;border:1px solid #ffffff22;backdrop-filter:blur(12px)}
.live b{font-family:Syne,sans-serif;font-size:1.8rem;color:#27e8c4;min-width:3.2ch;display:inline-block}
.live span{font-size:.9rem;color:#c9c4f0}
.dot{width:10px;height:10px;border-radius:50%;background:#27e8c4;animation:pulse 1.6s infinite}
@keyframes pulse{50%{box-shadow:0 0 0 8px #27e8c400;opacity:.6}0%{box-shadow:0 0 0 0 #27e8c488}}
/* content */
section{padding:5.5rem clamp(1.2rem,5vw,4rem);max-width:74rem;margin:0 auto}
h2{font-size:clamp(2rem,5vw,3.2rem);font-weight:800;letter-spacing:-.01em;max-width:22ch}
.lead{color:var(--mute);max-width:38rem;margin:1rem 0 3rem}
.steps{display:grid;grid-template-columns:repeat(auto-fit,minmax(15rem,1fr));gap:2rem;counter-reset:s}
.step{border-top:2px solid var(--line);padding-top:1.2rem;counter-increment:s}
.step::before{content:counter(s);font-family:Syne,sans-serif;font-weight:800;font-size:2.4rem;color:var(--violet)}
.step h3{font-size:1.4rem;margin:.4rem 0}
.step p,.tilt p{color:var(--mute);margin:0}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(16rem,1fr));gap:1.4rem;perspective:900px}
.tilt{background:var(--card);border:1px solid var(--line);border-radius:22px;padding:1.8rem;transition:transform .15s ease-out;transform-style:preserve-3d;will-change:transform}
.tilt h3{font-size:1.3rem;margin-bottom:.6rem;transform:translateZ(30px)}
.end{text-align:center;margin:0 auto 4rem;padding:4rem 1.5rem;border-radius:32px;background:linear-gradient(135deg,#2b1f7a,#0b0a1c);color:#eeeaff}
.end h2{margin:0 auto 1.6rem}
footer{text-align:center;color:var(--mute);padding:0 1rem 3rem;font-size:.9rem}
@media (max-width:640px){nav a.l{display:none}.live{right:1.2rem}}
@media (prefers-reduced-motion:reduce){.dot{animation:none}html{scroll-behavior:auto}.tilt{transition:none}}
</style>
</head>
<body>
<header class="hero">
  <canvas id="stage" aria-hidden="true"></canvas>
  <nav>
    <a class="logo" href="#">Smart Attendance</a>
    <div><a class="l" href="#how">How it works</a><a class="l" href="#features">Features</a><a class="l" href="#start">Login</a></div>
  </nav>
  <div class="copy">
    <h1>Attendance that marks itself.</h1>
    <p>Students walk in, the system recognises them, and the class register is done in seconds. No roll call, no proxies, no paper.</p>
    <div class="cta"><a class="btn main" href="#start">Open dashboard</a><a class="btn ghost" href="#how">See how it works</a></div>
  </div>
  <div class="live" role="status"><i class="dot"></i><div><b id="count">0</b><span>of 24 students marked present</span></div></div>
</header>

<main>
<section id="how">
  <h2>From doorway to report in three steps</h2>
  <p class="lead">Everything happens while the class settles in. Teachers only review the result.</p>
  <div class="steps">
    <div class="step"><h3>Scan</h3><p>The camera picks up each student as they enter the classroom.</p></div>
    <div class="step"><h3>Verify</h3><p>A liveness check confirms it is the real person, not a photo or a friend.</p></div>
    <div class="step"><h3>Report</h3><p>Attendance is saved instantly and shows up on the teacher’s dashboard.</p></div>
  </div>
</section>

<section id="features">
  <h2>Built for classrooms that move fast</h2>
  <p class="lead">Move your pointer over a card.</p>
  <div class="grid">
    <div class="tilt"><h3>Instant roll call</h3><p>A full class is marked while students find their seats.</p></div>
    <div class="tilt"><h3>Proxy-proof</h3><p>Each check is tied to a live face, so nobody can mark attendance for someone else.</p></div>
    <div class="tilt"><h3>Live reports</h3><p>See present, absent and late students per class, day or subject.</p></div>
    <div class="tilt"><h3>Low-attendance alerts</h3><p>Students who drop below the required percentage are flagged automatically.</p></div>
  </div>
</section>

<section id="start">
  <div class="end">
    <h2>Ready for your next class?</h2>
    <a class="btn main" href="#">Open dashboard</a>
  </div>
</section>
</main>
<footer>Smart Attendance, a student project.</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
(function(){
  var reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  var cv = document.getElementById('stage'), countEl = document.getElementById('count');
  if(!window.THREE){ countEl.textContent = '24'; return; }
  var R = new THREE.WebGLRenderer({canvas:cv, alpha:true, antialias:true});
  R.setPixelRatio(Math.min(devicePixelRatio,2));
  var scene = new THREE.Scene(), cam = new THREE.PerspectiveCamera(50,1,.1,100);
  var g = new THREE.Group(); scene.add(g);

  // point-cloud head of "identity" points
  var N = 2200, pos = new Float32Array(N*3), i, k;
  for(i=0;i<N;i++){
    var y = 1-(i/(N-1))*2, r = Math.sqrt(1-y*y), th = i*2.399963;
    pos[i*3]=Math.cos(th)*r*2; pos[i*3+1]=y*2.3; pos[i*3+2]=Math.sin(th)*r*2;
  }
  var pg = new THREE.BufferGeometry(); pg.setAttribute('position', new THREE.BufferAttribute(pos,3));
  var pts = new THREE.Points(pg, new THREE.PointsMaterial({color:0x27e8c4,size:.035,transparent:true,opacity:.85,blending:THREE.AdditiveBlending,depthWrite:false}));
  g.add(pts);
  var core = new THREE.Mesh(new THREE.IcosahedronGeometry(1.4,1), new THREE.MeshBasicMaterial({color:0x8d78ff,wireframe:true,transparent:true,opacity:.28}));
  g.add(core);

  // scanner ring
  var ring = new THREE.Mesh(new THREE.TorusGeometry(2.3,.015,8,160), new THREE.MeshBasicMaterial({color:0xffffff}));
  ring.rotation.x = Math.PI/2; g.add(ring);
  var disc = new THREE.Mesh(new THREE.CircleGeometry(2.3,64), new THREE.MeshBasicMaterial({color:0x27e8c4,transparent:true,opacity:.07,side:THREE.DoubleSide}));
  disc.rotation.x = Math.PI/2; g.add(disc);

  // 24 students orbiting; amber until the ring scans them
  var S = [], AMB = new THREE.Color(0xffb84d), MINT = new THREE.Color(0x27e8c4);
  for(k=0;k<24;k++){
    var m = new THREE.Mesh(new THREE.SphereGeometry(.09,16,16), new THREE.MeshBasicMaterial({color:AMB.clone()}));
    var a = k/24*Math.PI*2*2.6, yy = -2+(k*37%24)/24*4;
    m.position.set(Math.cos(a)*3.1, yy, Math.sin(a)*3.1); m.userData.done = false;
    g.add(m); S.push(m);
  }

  var mx=0,my=0;
  addEventListener('pointermove',function(e){mx=e.clientX/innerWidth-.5;my=e.clientY/innerHeight-.5;});
  function size(){
    var w=cv.clientWidth,h=cv.clientHeight; R.setSize(w,h,false); cam.aspect=w/h;
    var wide=w/h>1; cam.position.set(wide?2.2:0,0,wide?8.2:11.5); cam.lookAt(wide?1.2:0,0,0);
    g.position.set(wide?2.4:0,wide?0:1.4,0); cam.updateProjectionMatrix();
  }
  addEventListener('resize',size); size();

  var CYCLE=9, last=-1, t0=performance.now();
  function frame(now){
    var t=(now-t0)/1000, ph=(t%CYCLE)/CYCLE;           // 0..1 sweep
    var ry = Math.sin(ph*Math.PI*2-Math.PI/2)*.5+.5;   // smooth up/down
    ring.position.y = disc.position.y = -2.4+ry*4.8;
    if(ph<.02) S.forEach(function(s){s.userData.done=false;});
    var c=0;
    S.forEach(function(s){
      if(Math.abs(s.position.y-ring.position.y)<.22) s.userData.done=true;
      if(s.userData.done){c++; s.material.color.lerp(MINT,.15); s.scale.setScalar(1.4);}
      else {s.material.color.lerp(AMB,.15); s.scale.setScalar(1);}
    });
    if(c!==last){countEl.textContent=c;last=c;}
    g.rotation.y = t*.18 + mx*.6; g.rotation.x = my*.25; core.rotation.y = -t*.3;
    R.render(scene,cam);
    if(!reduce) requestAnimationFrame(frame);
  }
  if(reduce){ for(k=0;k<24;k++) S[k].userData.done=true; frame(1500); countEl.textContent='24'; } else requestAnimationFrame(frame);
})();

// 3D tilt on feature cards
(function(){
  if(matchMedia('(prefers-reduced-motion: reduce)').matches) return;
  document.querySelectorAll('.tilt').forEach(function(el){
    el.addEventListener('pointermove',function(e){
      var b=el.getBoundingClientRect(), x=(e.clientX-b.left)/b.width-.5, y=(e.clientY-b.top)/b.height-.5;
      el.style.transform='rotateY('+(x*14)+'deg) rotateX('+(-y*14)+'deg)';
    });
    el.addEventListener('pointerleave',function(){el.style.transform='';});
  });
})();
</script>
</body>
</html>
