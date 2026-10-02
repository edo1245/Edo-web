# Edo website 
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#07080f">

<title>EDO Web (Beta)</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>
:root{
    --bg:#07080f;
    --text:#eef0ff;
    --muted:#8f94b8;
    --glass:rgba(255,255,255,.045);
    --line:rgba(255,255,255,.09);
    --violet:#7c5cff;
    --cyan:#22d3ee;
    --grad:linear-gradient(135deg,#7c5cff,#22d3ee);
    --ease:cubic-bezier(.2,.7,.2,1);
}

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

[hidden]{ display:none !important; }

html{ -webkit-text-size-adjust:100%; }

body{
    font-family:'Sora',system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;
    background:var(--bg);
    color:var(--text);
    min-height:100vh;
    line-height:1.4;
}

body.locked{
    overflow:hidden;
    height:100vh;
}

button,input,textarea{ font-family:inherit; }

:focus-visible{
    outline:2px solid var(--cyan);
    outline-offset:3px;
}

/* =========================
   LATAR AURORA
========================= */

.aurora{
    position:fixed;
    inset:0;
    z-index:0;
    overflow:hidden;
    pointer-events:none;
}

.aurora i{
    position:absolute;
    border-radius:50%;
    background:radial-gradient(circle,var(--c) 0%,transparent 62%);
    animation:drift 24s ease-in-out infinite alternate;
}

.aurora i:nth-child(1){
    --c:rgba(124,92,255,.5);
    width:80vmax; height:80vmax;
    top:-42vmax; left:-30vmax;
}

.aurora i:nth-child(2){
    --c:rgba(34,211,238,.3);
    width:75vmax; height:75vmax;
    bottom:-45vmax; right:-35vmax;
    animation-duration:30s;
    animation-delay:-9s;
}

.aurora i:nth-child(3){
    --c:rgba(251,113,133,.18);
    width:50vmax; height:50vmax;
    top:35%; left:45%;
    animation-duration:36s;
    animation-delay:-16s;
}

.aurora::after{
    content:"";
    position:absolute;
    inset:0;
    background-image:
        linear-gradient(rgba(255,255,255,.035) 1px,transparent 1px),
        linear-gradient(90deg,rgba(255,255,255,.035) 1px,transparent 1px);
    background-size:48px 48px;
    -webkit-mask-image:radial-gradient(ellipse at 50% 0%,#000 0%,transparent 72%);
            mask-image:radial-gradient(ellipse at 50% 0%,#000 0%,transparent 72%);
}

@keyframes drift{
    to{ transform:translate(12vmax,8vmax) scale(1.15); }
}

@keyframes float{
    0%,100%{ transform:translateY(0); }
    50%{ transform:translateY(-12px); }
}

@keyframes floatHero{
    0%,100%{ transform:translateY(-50%) rotate(-8deg); }
    50%{ transform:translateY(calc(-50% - 14px)) rotate(-3deg); }
}

@keyframes rise{
    from{ opacity:0; transform:translateY(22px); }
    to{ opacity:1; transform:none; }
}

/* =========================
   INTRO
========================= */

#welcome{
    position:fixed;
    inset:0;
    z-index:100;
    display:grid;
    place-items:center;
    text-align:center;
    padding:24px;
    background:
        radial-gradient(120% 90% at 50% 0%,#1d1650 0%,#0b0b1d 48%,#06070d 100%);
    clip-path:circle(150% at var(--x,50%) var(--y,60%));
    transition:clip-path .95s cubic-bezier(.75,0,.2,1);
}

#welcome.wipe{
    clip-path:circle(0% at var(--x) var(--y));
}

#welcome::before{
    content:"";
    position:absolute;
    width:min(120vw,720px);
    height:min(120vw,720px);
    border-radius:50%;
    background:radial-gradient(circle,rgba(124,92,255,.35),transparent 65%);
    animation:pulse 5s ease-in-out infinite;
}

@keyframes pulse{
    0%,100%{ transform:scale(.9); opacity:.7; }
    50%{ transform:scale(1.08); opacity:1; }
}

.w-inner{
    position:relative;
    width:100%;
    max-width:440px;
}

.w-cube{
    width:116px;
    height:116px;
    margin:0 auto 22px;
    filter:drop-shadow(0 18px 38px rgba(124,92,255,.6));
    animation:cubeIn 1s var(--ease) both, float 4.2s ease-in-out 1s infinite;
}

.w-cube svg{ width:100%; height:100%; display:block; }

@keyframes cubeIn{
    from{ opacity:0; transform:translateY(30px) scale(.6) rotate(-25deg); }
    to{ opacity:1; transform:none; }
}

#welcome.go .w-cube{
    animation:cubeGo .75s cubic-bezier(.6,0,.3,1) forwards;
}

@keyframes cubeGo{
    0%{ transform:rotate(0) scale(1); }
    60%{ transform:rotate(300deg) scale(1.22); }
    100%{ transform:rotate(360deg) scale(1.05); }
}

.w-title{
    display:flex;
    justify-content:center;
    font-size:clamp(42px,13vw,66px);
    font-weight:800;
    letter-spacing:-.035em;
    line-height:1;
}

.w-title .ch{
    display:inline-block;
    opacity:0;
    transform:translateY(45%) rotate(5deg);
    animation:chIn .75s var(--ease) forwards;
    animation-delay:calc(.35s + var(--i) * .06s);
}

@keyframes chIn{
    to{ opacity:1; transform:none; }
}

.w-badge{
    display:inline-block;
    margin-top:14px;
    padding:4px 12px;
    border-radius:999px;
    font-size:12px;
    font-weight:700;
    color:#c4b5fd;
    background:rgba(124,92,255,.16);
    border:1px solid rgba(124,92,255,.4);
    opacity:0;
    animation:rise .7s var(--ease) .85s forwards;
}

.w-sub{
    max-width:340px;
    margin:16px auto 32px;
    color:var(--muted);
    font-size:15px;
    line-height:1.6;
    opacity:0;
    animation:rise .7s var(--ease) 1s forwards;
}

.enter-btn{
    position:relative;
    overflow:hidden;
    display:inline-flex;
    align-items:center;
    gap:10px;
    border:0;
    padding:16px 34px;
    border-radius:999px;
    background:var(--grad);
    color:#fff;
    font-size:16px;
    font-weight:700;
    cursor:pointer;
    box-shadow:0 14px 40px -10px rgba(124,92,255,.8);
    opacity:0;
    animation:rise .7s var(--ease) 1.15s forwards;
    transition:transform .25s var(--ease), filter .25s;
}

.enter-btn svg{
    width:20px; height:20px;
    transition:transform .25s var(--ease);
}

.enter-btn:hover{ transform:translateY(-3px); filter:brightness(1.08); }
.enter-btn:hover svg{ transform:translateX(4px); }
.enter-btn:active{ transform:scale(.97); }

.enter-btn::after{
    content:"";
    position:absolute;
    inset:0;
    background:linear-gradient(110deg,transparent 30%,rgba(255,255,255,.4) 50%,transparent 70%);
    transform:translateX(-130%);
    animation:shimmer 3s ease-in-out 2.2s infinite;
}

@keyframes shimmer{
    0%{ transform:translateX(-130%); }
    45%,100%{ transform:translateX(130%); }
}

#welcome.go .w-title,
#welcome.go .w-badge,
#welcome.go .w-sub,
#welcome.go .enter-btn{
    opacity:0 !important;
    transform:translateY(14px);
    transition:opacity .35s ease, transform .35s ease;
    animation:none;
}

/* =========================
   WEBSITE
========================= */

#website{
    position:relative;
    z-index:1;
}

.reveal{ opacity:0; }

.site-in .reveal{
    animation:rise .85s var(--ease) both;
    animation-delay:var(--d,0s);
}

.topbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    max-width:1040px;
    margin:0 auto;
    padding:20px 18px 6px;
}

.brand{
    display:flex;
    align-items:center;
    gap:10px;
    font-size:19px;
    font-weight:800;
    letter-spacing:-.02em;
}

.brand svg{ width:32px; height:32px; display:block; }

.beta{
    font-size:11px;
    font-weight:700;
    padding:3px 9px;
    border-radius:999px;
    color:#c4b5fd;
    background:rgba(124,92,255,.16);
    border:1px solid rgba(124,92,255,.38);
}

.wrap{
    max-width:1040px;
    margin:0 auto;
    padding:0 18px 56px;
}

/* search */

.search{
    position:relative;
    margin:12px 0 4px;
}

.search svg{
    position:absolute;
    left:16px;
    top:50%;
    width:20px; height:20px;
    transform:translateY(-50%);
    color:var(--muted);
    pointer-events:none;
}

.search input{
    width:100%;
    padding:16px 16px 16px 48px;
    border-radius:18px;
    border:1px solid var(--line);
    background:rgba(255,255,255,.06);
    color:var(--text);
    font-size:15px;
    outline:none;
    transition:border-color .2s, box-shadow .2s, background .2s;
}

.search input::placeholder{ color:#70759a; }

.search input:focus{
    border-color:rgba(124,92,255,.7);
    background:rgba(255,255,255,.08);
    box-shadow:0 0 0 4px rgba(124,92,255,.18);
}

/* tabs */

#tabs{
    position:sticky;
    top:0;
    z-index:30;
    display:flex;
    gap:8px;
    margin:0 -18px;
    padding:10px 18px 12px;
    overflow-x:auto;
    scrollbar-width:none;
    background:linear-gradient(rgba(7,8,15,.88),rgba(7,8,15,.55));
    -webkit-backdrop-filter:blur(14px);
            backdrop-filter:blur(14px);
}

#tabs::-webkit-scrollbar{ display:none; }

#tabs button{
    flex-shrink:0;
    padding:10px 17px;
    border-radius:999px;
    border:1px solid var(--line);
    background:var(--glass);
    color:var(--muted);
    font-size:13.5px;
    font-weight:600;
    cursor:pointer;
    transition:background .25s, color .25s, border-color .25s, box-shadow .25s, transform .15s;
}

#tabs button:hover{ color:var(--text); border-color:rgba(255,255,255,.2); }
#tabs button:active{ transform:scale(.96); }

#tabs button.active{
    background:var(--grad);
    border-color:transparent;
    color:#fff;
    box-shadow:0 8px 24px -8px rgba(124,92,255,.8);
}

/* hero */

.hero{
    position:relative;
    overflow:hidden;
    margin:10px 0 22px;
    padding:32px 24px 28px;
    border-radius:28px;
    border:1px solid var(--line);
    background:
        linear-gradient(135deg,rgba(124,92,255,.3),rgba(34,211,238,.1) 58%,rgba(255,255,255,.03));
}

.hero > *:not(.hero-cube){
    position:relative;
    z-index:2;
}

.hero h2{
    max-width:15em;
    font-size:clamp(27px,6.4vw,42px);
    font-weight:800;
    letter-spacing:-.03em;
    line-height:1.12;
}

.hero p{
    max-width:30em;
    margin:14px 0 22px;
    color:#b4b8d6;
    font-size:15px;
    line-height:1.65;
}

.hero-cta{
    display:flex;
    flex-wrap:wrap;
    gap:10px;
}

.btn-primary,
.btn-ghost{
    border:0;
    padding:13px 20px;
    border-radius:14px;
    font-size:14px;
    font-weight:700;
    cursor:pointer;
    transition:transform .2s var(--ease), filter .2s, background .2s;
}

.btn-primary{
    background:var(--grad);
    color:#fff;
    box-shadow:0 10px 28px -10px rgba(124,92,255,.85);
}

.btn-ghost{
    background:rgba(255,255,255,.08);
    color:var(--text);
    border:1px solid var(--line);
}

.btn-primary:hover,
.btn-ghost:hover{ transform:translateY(-2px); filter:brightness(1.1); }
.btn-primary:active,
.btn-ghost:active{ transform:scale(.97); }

.stats{
    display:flex;
    gap:28px;
    margin-top:26px;
}

.stat b{
    display:block;
    font-size:24px;
    font-weight:800;
    letter-spacing:-.02em;
}

.stat span{
    font-size:12.5px;
    color:var(--muted);
}

.hero-cube{
    position:absolute;
    right:-14px;
    top:50%;
    z-index:1;
    width:min(44%,230px);
    aspect-ratio:1;
    opacity:.95;
    filter:drop-shadow(0 22px 40px rgba(124,92,255,.5));
    animation:floatHero 6.5s ease-in-out infinite;
}

.hero-cube svg{ width:100%; height:100%; display:block; }

@media (max-width:560px){
    .hero{ padding:26px 20px 24px; }
    .hero-cube{
        width:150px;
        right:-34px;
        top:26%;
        opacity:.3;
    }
}

/* menu */

.block-title{
    font-size:17px;
    font-weight:700;
    letter-spacing:-.01em;
    margin:0 0 12px;
}

.menu-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(150px,1fr));
    gap:12px;
    margin-bottom:30px;
}

.tile{
    display:flex;
    flex-direction:column;
    align-items:flex-start;
    gap:14px;
    padding:16px;
    border-radius:20px;
    border:1px solid var(--line);
    background:var(--glass);
    color:var(--text);
    text-align:left;
    cursor:pointer;
    transition:transform .3s var(--ease), border-color .3s, background .3s, box-shadow .3s;
}

.site-in .tile{
    animation:rise .7s var(--ease) both;
    animation-delay:calc(.6s + var(--i) * 70ms);
}

.tile:hover{
    transform:translateY(-5px);
    border-color:var(--c);
    border-color:color-mix(in srgb,var(--c) 55%,transparent);
    background:color-mix(in srgb,var(--c) 9%,rgba(255,255,255,.04));
    box-shadow:0 18px 36px -18px var(--c);
}

.tile:active{ transform:scale(.97); }

.tile .ico{
    width:44px;
    height:44px;
    display:grid;
    place-items:center;
    border-radius:14px;
    color:var(--c);
    background:rgba(255,255,255,.07);
    background:color-mix(in srgb,var(--c) 17%,transparent);
}

.tile .ico svg{ width:22px; height:22px; }

.tile b{ display:block; font-size:15px; font-weight:700; }
.tile small{ display:block; margin-top:2px; font-size:12.5px; color:var(--muted); }

/* daftar file */

.view-head{
    display:flex;
    align-items:baseline;
    justify-content:space-between;
    gap:12px;
    margin:4px 0 14px;
}

.view-head h2{
    font-size:22px;
    font-weight:800;
    letter-spacing:-.02em;
}

.view-head .count{
    font-size:13px;
    color:var(--muted);
}

.grid{
    display:grid;
    gap:12px;
    grid-template-columns:1fr;
}

@media (min-width:720px){
    .grid{ grid-template-columns:1fr 1fr; }
}

.card{
    position:relative;
    display:flex;
    align-items:center;
    gap:14px;
    padding:14px;
    overflow:hidden;
    border-radius:20px;
    border:1px solid var(--line);
    background:var(--glass);
    transition:border-color .3s, transform .3s var(--ease);
}

.site-in .card{
    animation:rise .6s var(--ease) both;
    animation-delay:calc(min(var(--i),12) * 45ms);
}

.card::before{
    content:"";
    position:absolute;
    inset:0;
    background:radial-gradient(260px circle at var(--mx,50%) var(--my,0%),rgba(255,255,255,.1),transparent 70%);
    background:radial-gradient(260px circle at var(--mx,50%) var(--my,0%),color-mix(in srgb,var(--c) 24%,transparent),transparent 70%);
    opacity:0;
    transition:opacity .3s;
    pointer-events:none;
}

.card:hover{
    border-color:rgba(255,255,255,.2);
    border-color:color-mix(in srgb,var(--c) 45%,transparent);
}

.card:hover::before{ opacity:1; }

.card > *{ position:relative; }

.logo{
    position:relative;
    flex-shrink:0;
    width:60px;
    height:60px;
    display:grid;
    place-items:center;
    overflow:hidden;
    border-radius:17px;
    color:#fff;
    font-size:18px;
    font-weight:800;
    letter-spacing:-.02em;
    background:var(--c);
    background:linear-gradient(135deg,var(--c),color-mix(in srgb,var(--c) 45%,#000));
    box-shadow:inset 0 0 0 1px rgba(255,255,255,.2),0 10px 22px -10px var(--c);
}

.logo img{
    position:absolute;
    inset:0;
    width:100%;
    height:100%;
    object-fit:cover;
    background:#0d0e1a;
}

.info{
    flex:1;
    min-width:0;
}

.name{
    font-size:16px;
    font-weight:700;
    line-height:1.25;
    letter-spacing:-.01em;
    overflow-wrap:anywhere;
}

.tags{
    display:flex;
    flex-wrap:wrap;
    gap:6px;
    margin-top:9px;
}

.tag{
    padding:3px 9px;
    border-radius:999px;
    font-size:11.5px;
    font-weight:600;
}

.tag.cat{
    color:var(--c);
    background:rgba(255,255,255,.08);
    background:color-mix(in srgb,var(--c) 15%,transparent);
}

.tag.type{
    color:var(--muted);
    border:1px solid var(--line);
}

.dl{
    flex-shrink:0;
    display:inline-flex;
    align-items:center;
    gap:7px;
    padding:11px 15px;
    border-radius:14px;
    background:var(--grad);
    color:#fff;
    font-size:13.5px;
    font-weight:700;
    text-decoration:none;
    box-shadow:0 10px 24px -10px rgba(124,92,255,.8);
    transition:transform .2s var(--ease), filter .2s;
}

.dl svg{ width:17px; height:17px; }
.dl:hover{ transform:translateY(-2px); filter:brightness(1.1); }
.dl:active{ transform:scale(.96); }

@media (max-width:380px){
    .dl span{ display:none; }
    .dl{ padding:12px; }
}

.empty{
    grid-column:1/-1;
    padding:48px 12px;
    text-align:center;
    color:var(--muted);
    font-size:14px;
}

/* laporan */

.panel{
    padding:22px;
    border-radius:24px;
    border:1px solid var(--line);
    background:var(--glass);
    max-width:620px;
}

.panel label{
    display:block;
    margin:0 0 7px;
    font-size:13px;
    font-weight:600;
    color:#b4b8d6;
}

.panel input,
.panel textarea{
    width:100%;
    margin-bottom:16px;
    padding:14px 15px;
    border-radius:14px;
    border:1px solid var(--line);
    background:rgba(255,255,255,.05);
    color:var(--text);
    font-size:15px;
    outline:none;
    transition:border-color .2s, box-shadow .2s;
}

.panel textarea{
    min-height:130px;
    resize:vertical;
}

.panel input:focus,
.panel textarea:focus{
    border-color:rgba(124,92,255,.7);
    box-shadow:0 0 0 4px rgba(124,92,255,.18);
}

/* footer */

footer{
    position:relative;
    z-index:1;
    padding:26px 18px 34px;
    text-align:center;
    color:#5f6488;
    font-size:13px;
    border-top:1px solid var(--line);
}

@media (prefers-reduced-motion: reduce){
    *,*::before,*::after{
        animation:none !important;
        transition:none !important;
    }
    .reveal,
    .w-title .ch,
    .w-badge,
    .w-sub,
    .enter-btn{
        opacity:1 !important;
        transform:none !important;
    }
}
</style>
</head>

<body class="locked">

<!-- simbol blok isometrik (dipakai ulang) -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
    <defs>
        <linearGradient id="gTop" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0" stop-color="#d8ccff"/>
            <stop offset="1" stop-color="#8b6cff"/>
        </linearGradient>
        <linearGradient id="gLeft" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stop-color="#6d4df0"/>
            <stop offset="1" stop-color="#34259c"/>
        </linearGradient>
        <linearGradient id="gRight" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0" stop-color="#2ee0f5"/>
            <stop offset="1" stop-color="#0c6a85"/>
        </linearGradient>
        <symbol id="cube" viewBox="0 0 120 120">
            <polygon points="60,8 110,36 60,64 10,36" fill="url(#gTop)"/>
            <polygon points="10,36 60,64 60,116 10,88" fill="url(#gLeft)"/>
            <polygon points="110,36 60,64 60,116 110,88" fill="url(#gRight)"/>
            <path d="M35 22L85 50M85 22L35 50M35 50V102M10 62L60 90M85 50V102M60 90L110 62"
                  stroke="rgba(255,255,255,.2)" stroke-width="1.5" fill="none"/>
            <polygon points="60,8 110,36 60,64 10,36" fill="none"
                     stroke="rgba(255,255,255,.45)" stroke-width="1.5" stroke-linejoin="round"/>
        </symbol>
    </defs>
</svg>

<div class="aurora"><i></i><i></i><i></i></div>


<!-- =====================================================
     INTRO
===================================================== -->

<div id="welcome">

    <div class="w-inner">

        <div class="w-cube">
            <svg viewBox="0 0 120 120"><use href="#cube" width="120" height="120"/></svg>
        </div>

        <h1 class="w-title" id="wTitle" aria-label="EDO Web"></h1>

        <span class="w-badge">Beta</span>

        <p class="w-sub">
            Add-on, map, texture pack, APK, dan script Minecraft Bedrock dalam satu tempat.
        </p>

        <button class="enter-btn" id="enterBtn" type="button">
            Masuk
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"
                 stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="M13 6l6 6-6 6"/></svg>
        </button>

    </div>

</div>


<!-- =====================================================
     WEBSITE
===================================================== -->

<div id="website">

    <header class="topbar reveal" style="--d:0s">

        <div class="brand">
            <svg viewBox="0 0 120 120"><use href="#cube" width="120" height="120"/></svg>
            EDO Web
        </div>

        <span class="beta">Beta</span>

    </header>


    <main class="wrap">

        <div cl
