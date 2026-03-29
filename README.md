# NovaaCards-store
Novaacards Gift Card Store
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Novaacards</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#080A0F;--s1:#0D1018;--s2:#131720;--s3:#181D28;
  --b1:rgba(255,255,255,0.06);--b2:rgba(255,255,255,0.1);--b3:rgba(255,255,255,0.15);
  --accent:#5B8EF0;--accent2:#8B5CF6;--ton:#0098EA;
  --green:#10B981;--yellow:#F59E0B;--red:#EF4444;
  --t1:#F0F2F8;--t2:#8892A8;--t3:#4A5268;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;overflow:hidden;}
body{background:var(--bg);color:var(--t1);font-family:'Inter',sans-serif;font-size:14px;}
.app{height:100vh;display:flex;flex-direction:column;max-width:430px;margin:0 auto;}
.pc{flex:1;overflow-y:auto;overflow-x:hidden;-webkit-overflow-scrolling:touch;padding-bottom:80px;}
.pc::-webkit-scrollbar{display:none;}
.bg-orbs{position:fixed;inset:0;pointer-events:none;z-index:0;overflow:hidden;}
.orb{position:absolute;border-radius:50%;filter:blur(80px);opacity:0.1;}
.orb1{width:400px;height:400px;background:#5B8EF0;top:-100px;right:-100px;animation:o1 12s ease-in-out infinite alternate;}
.orb2{width:350px;height:350px;background:#8B5CF6;bottom:-80px;left:-80px;animation:o2 15s ease-in-out infinite alternate;}
@keyframes o1{from{transform:translate(0,0)}to{transform:translate(-60px,80px)}}
@keyframes o2{from{transform:translate(0,0)}to{transform:translate(60px,-60px)}}

/* HEADER */
.hdr{padding:12px 16px;display:flex;align-items:center;justify-content:space-between;background:rgba(8,10,15,0.92);backdrop-filter:blur(20px);border-bottom:1px solid var(–b1);position:relative;z-index:10;flex-shrink:0;}
.hdr-l{display:flex;align-items:center;gap:10px;}
.logo{width:32px;height:32px;border-radius:9px;background:linear-gradient(135deg,var(–accent),var(–accent2));display:flex;align-items:center;justify-content:center;font-size:15px;box-shadow:0 0 16px rgba(91,142,240,0.4);}
.logo-n{font-size:15px;font-weight:800;letter-spacing:-0.5px;}
.hdr-r{display:flex;align-items:center;gap:7px;}
.pts-b{display:flex;align-items:center;gap:4px;background:rgba(245,158,11,0.12);border:1px solid rgba(245,158,11,0.2);padding:4px 9px;border-radius:20px;font-size:11px;font-weight:700;color:#FCD34D;}
.ldot{width:6px;height:6px;border-radius:50%;background:var(–green);box-shadow:0 0 6px var(–green);animation:blink 2s infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0.4}}

/* STATS */
.sbar{display:flex;background:var(–s1);border-bottom:1px solid var(–b1);}
.st{flex:1;text-align:center;padding:9px 4px;}
.sn{font-size:13px;font-weight:800;}
.sl{font-size:9px;color:var(–t2);margin-top:1px;font-weight:500;text-transform:uppercase;letter-spacing:0.5px;}

/* FLASH SALE */
.flash{margin:12px 14px;background:linear-gradient(135deg,#1A0800,#2A1000);border:1px solid rgba(239,68,68,0.3);border-radius:16px;padding:14px 16px;display:flex;align-items:center;justify-content:space-between;position:relative;overflow:hidden;}
.flash::before{content:’’;position:absolute;inset:0;background:linear-gradient(90deg,transparent,rgba(239,68,68,0.05),transparent);animation:shine 3s infinite;}
@keyframes shine{from{transform:translateX(-100%)}to{transform:translateX(100%)}}
.flash-l{flex:1;}
.flash-tag{display:inline-flex;align-items:center;gap:4px;background:rgba(239,68,68,0.15);border:1px solid rgba(239,68,68,0.3);color:#FCA5A5;font-size:9px;font-weight:700;letter-spacing:1px;text-transform:uppercase;padding:3px 8px;border-radius:20px;margin-bottom:6px;}
.flash-title{font-size:15px;font-weight:800;margin-bottom:3px;}
.flash-sub{font-size:11px;color:var(–t2);}
.flash-timer{text-align:center;}
.timer-label{font-size:9px;color:var(–t2);margin-bottom:4px;text-transform:uppercase;letter-spacing:1px;}
.timer{font-size:18px;font-weight:900;color:#FCA5A5;font-variant-numeric:tabular-nums;}

/* HERO */
.hero{margin:0 14px 12px;background:linear-gradient(135deg,#0C1829,#0D1020);border:1px solid rgba(91,142,240,0.2);border-radius:18px;padding:18px;position:relative;overflow:hidden;}
.hero::after{content:‘🎁’;position:absolute;right:14px;top:50%;transform:translateY(-50%);font-size:55px;opacity:0.07;}
.hero-pill{display:inline-flex;align-items:center;gap:4px;background:rgba(91,142,240,0.12);border:1px solid rgba(91,142,240,0.25);color:#93B4F8;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;padding:4px 10px;border-radius:20px;margin-bottom:9px;}
.hero h1{font-size:21px;font-weight:900;line-height:1.2;letter-spacing:-0.5px;margin-bottom:5px;}
.hero h1 span{background:linear-gradient(90deg,var(–accent),var(–accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;}
.hero p{font-size:11px;color:var(–t2);line-height:1.6;margin-bottom:12px;}
.hero-tags{display:flex;gap:5px;flex-wrap:wrap;}
.htag{font-size:10px;font-weight:500;color:var(–t2);background:rgba(255,255,255,0.05);border:1px solid var(–b2);padding:3px 9px;border-radius:20px;}

/* DISCOUNT BANNER */
.disc{margin:0 14px 12px;background:linear-gradient(135deg,#0A1A0A,#0D200D);border:1px solid rgba(16,185,129,0.25);border-radius:14px;padding:12px 14px;display:flex;align-items:center;gap:12px;}
.disc-icon{font-size:24px;}
.disc-text{flex:1;}
.disc-title{font-size:12px;font-weight:700;color:var(–green);margin-bottom:2px;}
.disc-sub{font-size:11px;color:var(–t2);}
.disc-code{background:rgba(16,185,129,0.1);border:1px solid rgba(16,185,129,0.3);color:var(–green);font-size:12px;font-weight:800;padding:6px 12px;border-radius:8px;letter-spacing:1px;cursor:pointer;font-family:inherit;}

/* SEARCH */
.sw{padding:0 14px 10px;}
.srch{display:flex;align-items:center;gap:8px;background:var(–s2);border:1px solid var(–b2);border-radius:12px;padding:10px 14px;}
.srch input{background:none;border:none;outline:none;color:var(–t1);font-family:inherit;font-size:13px;flex:1;}
.srch input::placeholder{color:var(–t3);}

/* CATS */
.cats{display:flex;gap:7px;overflow-x:auto;padding:0 14px 10px;scrollbar-width:none;}
.cats::-webkit-scrollbar{display:none;}
.cat{flex-shrink:0;padding:6px 13px;border-radius:20px;font-size:11px;font-weight:600;border:1px solid var(–b1);background:var(–s2);color:var(–t2);cursor:pointer;font-family:inherit;white-space:nowrap;transition:all 0.2s;}
.cat.on{background:linear-gradient(135deg,var(–accent),var(–accent2));color:#fff;border-color:transparent;box-shadow:0 4px 14px rgba(91,142,240,0.3);}

/* SECTION */
.sec{padding:0 14px;margin-bottom:18px;}
.sec-h{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;}
.sec-t{font-size:13px;font-weight:700;}
.sec-s{font-size:11px;color:var(–t2);}

/* GRID */
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.card{background:var(–s1);border:1px solid var(–b1);border-radius:14px;overflow:hidden;cursor:pointer;transition:all 0.2s;animation:up 0.3s ease-out both;position:relative;}
.card:active{transform:scale(0.97);}
@keyframes up{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

/* BADGES */
.badge-wrap{position:absolute;top:7px;left:7px;z-index:3;display:flex;gap:4px;flex-direction:column;}
.badge{font-size:9px;font-weight:800;padding:2px 7px;border-radius:5px;text-transform:uppercase;letter-spacing:0.5px;}
.b-hot{background:rgba(239,68,68,0.9);color:#fff;}
.b-new{background:rgba(16,185,129,0.9);color:#fff;}
.b-pop{background:rgba(245,158,11,0.9);color:#fff;}
.b-sale{background:rgba(139,92,246,0.9);color:#fff;}

/* CARD VISUAL */
.cv{height:90px;position:relative;overflow:hidden;display:flex;align-items:center;justify-content:center;}
.cv svg{position:absolute;inset:0;width:100%;height:100%;}
.cv-c{position:relative;z-index:2;text-align:center;}
.c-info{padding:9px 10px 10px;}
.c-name{font-size:12px;font-weight:700;margin-bottom:2px;}
.c-price{font-size:11px;color:var(–accent);font-weight:600;margin-bottom:5px;}
.c-foot{display:flex;align-items:center;justify-content:space-between;}
.c-chip{font-size:9px;font-weight:700;background:rgba(91,142,240,0.1);color:#93B4F8;padding:2px 6px;border-radius:4px;}
.c-buyers{font-size:9px;color:var(–t3);}

/* TRUST */
.tbox{margin:0 14px 18px;background:var(–s1);border:1px solid var(–b1);border-radius:14px;overflow:hidden;}
.ttitle{padding:11px 14px 8px;font-size:10px;font-weight:700;color:var(–t2);text-transform:uppercase;letter-spacing:1px;border-bottom:1px solid var(–b1);}
.trow{display:flex;align-items:center;gap:11px;padding:10px 14px;border-bottom:1px solid var(–b1);}
.trow:last-child{border:none;}
.ti{width:32px;height:32px;border-radius:9px;background:var(–s2);display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0;}
.tt{flex:1;}
.ttn{font-size:12px;font-weight:600;margin-bottom:1px;}
.ttd{font-size:10px;color:var(–t2);line-height:1.4;}
.tc{color:var(–green);font-weight:700;font-size:12px;}

/* REVIEWS */
.rs{display:flex;gap:9px;overflow-x:auto;padding:0 14px 12px;scrollbar-width:none;}
.rs::-webkit-scrollbar{display:none;}
.rv{flex-shrink:0;width:190px;background:var(–s1);border:1px solid var(–b1);border-radius:12px;padding:11px;}
.rv-s{color:#F59E0B;font-size:10px;margin-bottom:5px;}
.rv-t{font-size:11px;color:var(–t2);line-height:1.5;margin-bottom:7px;}
.rv-u{display:flex;align-items:center;gap:6px;}
.rv-a{width:20px;height:20px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:#fff;}
.rv-n{font-size:10px;font-weight:600;}
.rv-d{font-size:9px;color:var(–t3);}

/* SHEET */
.ov{position:fixed;inset:0;background:rgba(0,0,0,0.8);z-index:100;display:flex;align-items:flex-end;opacity:0;pointer-events:none;transition:opacity 0.25s;backdrop-filter:blur(10px);}
.ov.on{opacity:1;pointer-events:all;}
.sh{background:var(–s1);border-radius:22px 22px 0 0;border-top:1px solid var(–b2);width:100%;max-height:92vh;overflow-y:auto;transform:translateY(100%);transition:transform 0.3s cubic-bezier(0.34,1.1,0.64,1);}
.ov.on .sh{transform:translateY(0);}
.sh::-webkit-scrollbar{display:none;}
.handle{width:34px;height:4px;background:var(–b3);border-radius:2px;margin:9px auto 0;}
.sb{padding:14px 16px 34px;}
.sh-img{height:100px;border-radius:12px;overflow:hidden;display:flex;align-items:center;justify-content:center;margin-bottom:12px;position:relative;}
.sh-img svg{position:absolute;inset:0;width:100%;height:100%;}
.sh-img-c{position:relative;z-index:2;text-align:center;}
.sh-title{font-size:18px;font-weight:800;margin-bottom:3px;}
.sh-desc{font-size:12px;color:var(–t2);line-height:1.5;margin-bottom:14px;}
.lbl{font-size:10px;font-weight:700;color:var(–t2);text-transform:uppercase;letter-spacing:1px;margin-bottom:7px;}
.ag{display:grid;grid-template-columns:repeat(3,1fr);gap:6px;margin-bottom:14px;}
.ab{padding:8px 4px;border-radius:9px;border:1px solid var(–b1);background:var(–s2);color:var(–t1);font-size:12px;font-weight:700;cursor:pointer;text-align:center;font-family:inherit;transition:all 0.15s;}
.ab .as{font-size:9px;color:var(–t2);font-weight:400;margin-top:2px;}
.ab.on{border-color:var(–accent);background:rgba(91,142,240,0.12);color:var(–accent);}
.ab.on .as{color:var(–accent);opacity:0.7;}
.sum{background:var(–s2);border:1px solid var(–b1);border-radius:11px;padding:11px;margin-bottom:14px;}
.sr{display:flex;justify-content:space-between;font-size:12px;padding:4px 0;border-bottom:1px solid var(–b1);}
.sr:last-child{border:none;padding-bottom:0;}
.sl2{color:var(–t2);}
.sv{font-weight:600;}
.sv.a{color:var(–accent);font-size:14px;font-weight:800;}
.sv.g{color:var(–green);}
.sv.y{color:#FCD34D;}
.btn-main{width:100%;padding:14px;background:linear-gradient(135deg,var(–accent),var(–accent2));border:none;border-radius:12px;color:#fff;font-family:inherit;font-size:14px;font-weight:800;cursor:pointer;box-shadow:0 6px 20px rgba(91,142,240,0.3);transition:all 0.15s;}
.btn-main:active{transform:scale(0.98);}

/* PAYMENT */
.pms{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:12px;}
.pm{padding:11px 7px;border-radius:11px;border:1px solid var(–b1);background:var(–s2);cursor:pointer;text-align:center;transition:all 0.2s;font-family:inherit;}
.pm.on{border-color:var(–accent);background:rgba(91,142,240,0.1);}
.pm.ton{border-color:rgba(0,152,234,0.3);background:rgba(0,152,234,0.07);}
.pm.ton.on{border-color:var(–ton);background:rgba(0,152,234,0.14);}
.pm-ic{font-size:20px;margin-bottom:4px;}
.pm-n{font-size:11px;font-weight:700;}
.pm-s{font-size:9px;color:var(–t2);margin-top:2px;}
.pm.on .pm-n{color:var(–accent);}
.pm.ton.on .pm-n{color:#4FC3F7;}
.abox{background:var(–s2);border:1px solid rgba(91,142,240,0.2);border-radius:10px;padding:11px;font-family:monospace;font-size:11px;color:#93B4F8;word-break:break-all;letter-spacing:0.3px;margin-bottom:9px;line-height:1.6;}
.btn-copy{width:100%;padding:10px;border-radius:9px;border:1px solid rgba(91,142,240,0.25);background:rgba(91,142,240,0.07);color:var(–accent);font-size:12px;font-weight:700;cursor:pointer;font-family:inherit;margin-bottom:9px;}
.btn-ton{width:100%;padding:13px;border-radius:11px;background:linear-gradient(135deg,#0098EA,#006BB3);border:none;color:#fff;font-size:13px;font-weight:800;cursor:pointer;font-family:inherit;box-shadow:0 4px 14px rgba(0,152,234,0.35);margin-bottom:9px;}
.warn{background:rgba(245,158,11,0.07);border:1px solid rgba(245,158,11,0.18);border-radius:9px;padding:9px 11px;font-size:10px;color:#FCD34D;line-height:1.5;margin-bottom:11px;}
.btn-confirm{width:100%;padding:13px;border-radius:11px;background:linear-gradient(135deg,var(–green),#059669);border:none;color:#fff;font-size:13px;font-weight:800;cursor:pointer;font-family:inherit;box-shadow:0 4px 12px rgba(16,185,129,0.25);}

/* NAV */
.bnav{position:relative;z-index:10;background:rgba(8,10,15,0.95);backdrop-filter:blur(20px);border-top:1px solid var(–b1);display:flex;padding:8px 0 20px;flex-shrink:0;}
.nb{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;padding:4px 0;}
.ni{font-size:19px;opacity:0.3;transition:all 0.2s;}
.nl{font-size:9px;font-weight:600;color:var(–t3);transition:color 0.2s;}
.nb.on .ni{opacity:1;}
.nb.on .nl{color:var(–accent);}

/* PAGES */
.page{display:none;}
.page.on{display:block;}

/* PROFILE */
.ph{margin:12px;background:linear-gradient(135deg,#0C1829,#110D1E);border:1px solid var(–b2);border-radius:18px;padding:18px;text-align:center;}
.pav{width:68px;height:68px;border-radius:50%;background:linear-gradient(135deg,var(–accent),var(–accent2));display:flex;align-items:center;justify-content:center;font-size:24px;font-weight:800;margin:0 auto 10px;border:3px solid rgba(91,142,240,0.3);box-shadow:0 0 20px rgba(91,142,240,0.25);}
.pname{font-size:17px;font-weight:800;margin-bottom:2px;}
.pid{font-size:10px;color:var(–t2);margin-bottom:12px;}
.pstats{display:grid;grid-template-columns:1fr 1fr 1fr;gap:7px;}
.ps{background:rgba(255,255,255,0.04);border:1px solid var(–b1);border-radius:9px;padding:9px 5px;text-align:center;}
.psn{font-size:14px;font-weight:800;}
.psl{font-size:9px;color:var(–t2);margin-top:2px;text-transform:uppercase;letter-spacing:0.5px;}
.lyc{margin:0 12px 12px;background:linear-gradient(135deg,#1A1200,#251800);border:1px solid rgba(245,158,11,0.2);border-radius:14px;padding:14px;position:relative;overflow:hidden;}
.lyc::after{content:‘⭐’;position:absolute;right:14px;top:50%;transform:translateY(-50%);font-size:46px;opacity:0.1;}
.ly-l{font-size:10px;font-weight:700;color:#FCD34D;text-transform:uppercase;letter-spacing:1px;margin-bottom:5px;}
.ly-p{font-size:26px;font-weight:900;color:#FCD34D;margin-bottom:3px;}
.ly-s{font-size:10px;color:var(–t2);margin-bottom:10px;}
.ly-bg{background:rgba(255,255,255,0.08);border-radius:4px;height:5px;margin-bottom:5px;}
.ly-bar{height:5px;border-radius:4px;background:linear-gradient(90deg,#F59E0B,#FCD34D);transition:width 0.5s;}
.ly-n{font-size:10px;color:var(–t2);}
.refc{margin:0 12px 12px;background:var(–s1);border:1px solid var(–b1);border-radius:14px;padding:14px;}
.ref-t{font-size:12px;font-weight:700;margin-bottom:3px;}
.ref-d{font-size:10px;color:var(–t2);line-height:1.5;margin-bottom:10px;}
.ref-c{background:var(–s2);border:1px solid var(–b2);border-radius:9px;padding:10px 13px;display:flex;align-items:center;justify-content:space-between;margin-bottom:9px;}
.ref-ct{font-size:13px;font-weight:800;color:var(–accent);letter-spacing:1px;}
.ref-cp{background:rgba(91,142,240,0.1);border:1px solid rgba(91,142,240,0.2);color:var(–accent);font-size:10px;font-weight:700;padding:4px 10px;border-radius:5px;cursor:pointer;font-family:inherit;}
.ref-i{display:flex;gap:7px;}
.rii{flex:1;background:var(–s2);border:1px solid var(–b1);border-radius:9px;padding:9px;text-align:center;}
.riin{font-size:15px;font-weight:800;color:var(–accent);}
.riil{font-size:9px;color:var(–t2);margin-top:2px;}

/* ORDERS */
.empty{text-align:center;padding:46px 20px;}
.ei{font-size:38px;opacity:0.2;margin-bottom:10px;}
.et{font-size:15px;font-weight:700;margin-bottom:5px;}
.ed{font-size:11px;color:var(–t2);line-height:1.5;}
.oi{background:var(–s1);border:1px solid var(–b1);border-radius:12px;padding:12px;margin-bottom:8px;display:flex;align-items:center;gap:10px;}
.oie{font-size:22px;}
.oii{flex:1;}
.oin{font-size:12px;font-weight:700;margin-bottom:2px;}
.oip{font-size:10px;color:var(–t2);}
.oid{font-size:9px;color:var(–t3);margin-top:1px;}
.obp{font-size:10px;font-weight:700;padding:3px 7px;border-radius:5px;}
.op{background:rgba(245,158,11,0.1);color:#FCD34D;}
.od{background:rgba(16,185,129,0.1);color:var(–green);}

/* SUPPORT */
.sbox{margin:0 12px 12px;background:var(–s1);border:1px solid var(–b1);border-radius:14px;overflow:hidden;}
.srow{display:flex;align-items:center;gap:10px;padding:12px 13px;border-bottom:1px solid var(–b1);cursor:pointer;}
.srow:last-child{border:none;}
.si{width:32px;height:32px;border-radius:9px;background:var(–s2);display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0;}
.stt{flex:1;}
.stn{font-size:11px;font-weight:600;margin-bottom:1px;}
.std{font-size:10px;color:var(–t2);}

/* TOAST */
.toast{position:fixed;bottom:96px;left:50%;transform:translateX(-50%) translateY(8px);background:var(–s2);border:1px solid var(–b2);color:var(–t1);padding:8px 16px;border-radius:20px;font-size:11px;font-weight:600;opacity:0;transition:all 0.25s;z-index:999;white-space:nowrap;box-shadow:0 4px 18px rgba(0,0,0,0.5);}
.toast.on{opacity:1;transform:translateX(-50%) translateY(0);}
</style>

</head>
<body>
<div class="bg-orbs"><div class="orb orb1"></div><div class="orb orb2"></div></div>
<div class="app">
  <div class="hdr">
    <div class="hdr-l"><div class="logo">🎁</div><span class="logo-n">Novaacards</span></div>
    <div class="hdr-r"><div class="pts-b">⭐ <span id="hdr-pts">0</span> pts</div><div class="ldot"></div></div>
  </div>
  <div class="pc">

```
<!-- HOME -->
<div class="page on" id="pg-home">
  <div class="sbar">
    <div class="st"><div class="sn" style="color:var(--accent)">2,400+</div><div class="sl">Orders</div></div>
    <div class="st"><div class="sn" style="color:var(--yellow)">4.9⭐</div><div class="sl">Rating</div></div>
    <div class="st"><div class="sn" style="color:var(--green)">~5min</div><div class="sl">Delivery</div></div>
    <div class="st"><div class="sn" style="color:#4FC3F7">0%</div><div class="sl">Fees</div></div>
  </div>

  <!-- FLASH SALE -->
  <div class="flash">
    <div class="flash-l">
      <div class="flash-tag">🔥 Flash Sale</div>
      <div class="flash-title">5% OFF First Order</div>
      <div class="flash-sub">Use code NOVA5 at checkout</div>
    </div>
    <div class="flash-timer">
      <div class="timer-label">Ends in</div>
      <div class="timer" id="timer">23:59:59</div>
    </div>
  </div>

  <!-- HERO -->
  <div class="hero">
    <div class="hero-pill">⚡ Instant Delivery</div>
    <h1>Buy Gift Cards<br>with <span>Crypto</span></h1>
    <p>13 premium gift cards. USDT & TON accepted. Delivered in minutes. 100% authentic.</p>
    <div class="hero-tags">
      <div class="htag">🔒 Secure</div>
      <div class="htag">💎 TON Pay</div>
      <div class="htag">🌍 Global</div>
      <div class="htag">✅ Verified</div>
      <div class="htag">⭐ Loyalty</div>
    </div>
  </div>

  <!-- FIRST ORDER DISCOUNT -->
  <div class="disc">
    <div class="disc-icon">🎁</div>
    <div class="disc-text">
      <div class="disc-title">First Order Discount</div>
      <div class="disc-sub">Save 5% on your first purchase</div>
    </div>
    <button class="disc-code" onclick="copyDiscount()">NOVA5</button>
  </div>

  <div class="sw"><div class="srch"><span style="opacity:0.3;font-size:14px">🔍</span><input placeholder="Search gift cards..." oninput="doSearch(this.value)"></div></div>

  <div class="cats">
    <button class="cat on" onclick="filterCat('all',this)">🏪 All</button>
    <button class="cat" onclick="filterCat('gaming',this)">🎮 Gaming</button>
    <button class="cat" onclick="filterCat('streaming',this)">🎬 Streaming</button>
    <button class="cat" onclick="filterCat('shopping',this)">🛒 Shopping</button>
    <button class="cat" onclick="filterCat('music',this)">🎵 Music</button>
  </div>

  <div class="sec">
    <div class="sec-h"><div class="sec-t">🔥 Best Sellers</div><div class="sec-s" id="card-count">13 cards</div></div>
    <div class="grid" id="cards-grid"></div>
  </div>

  <div class="tbox">
    <div class="ttitle">Why 2,400+ customers trust us</div>
    <div class="trow"><div class="ti">🔐</div><div class="tt"><div class="ttn">Blockchain Verified</div><div class="ttd">Every payment verified on-chain. No fraud possible.</div></div><div class="tc">✓</div></div>
    <div class="trow"><div class="ti">⚡</div><div class="tt"><div class="ttn">Instant Delivery</div><div class="ttd">Card codes sent within minutes of confirmation.</div></div><div class="tc">✓</div></div>
    <div class="trow"><div class="ti">🛡️</div><div class="tt"><div class="ttn">100% Authentic Cards</div><div class="ttd">All cards sourced from official distributors only.</div></div><div class="tc">✓</div></div>
    <div class="trow"><div class="ti">💬</div><div class="tt"><div class="ttn">24/7 Live Support</div><div class="ttd">Real human support. Average reply under 3 minutes.</div></div><div class="tc">✓</div></div>
    <div class="trow"><div class="ti">⭐</div><div class="tt"><div class="ttn">Loyalty Rewards</div><div class="ttd">Earn 10 pts per $1. Redeem for discounts.</div></div><div class="tc">✓</div></div>
    <div class="trow"><div class="ti">🔄</div><div class="tt"><div class="ttn">Money Back Guarantee</div><div class="ttd">Invalid card? We replace it immediately.</div></div><div class="tc">✓</div></div>
  </div>

  <div class="sec"><div class="sec-h"><div class="sec-t">Customer Reviews</div><div class="sec-s">4.9 / 5.0 ⭐</div></div></div>
  <div class="rs">
    <div class="rv"><div class="rv-s">★★★★★</div><div class="rv-t">"Got my Amazon card in 5 min after USDT. Super fast!"</div><div class="rv-u"><div class="rv-a" style="background:#5B8EF0">A</div><div><div class="rv-n">Ahmed K.</div><div class="rv-d">2 days ago</div></div></div></div>
    <div class="rv"><div class="rv-s">★★★★★</div><div class="rv-t">"Bought PUBG UC, got it instantly. Best store on Telegram!"</div><div class="rv-u"><div class="rv-a" style="background:#8B5CF6">S</div><div><div class="rv-n">Sara M.</div><div class="rv-d">4 days ago</div></div></div></div>
    <div class="rv"><div class="rv-s">★★★★★</div><div class="rv-t">"Paid with TON wallet, Spotify card arrived instantly!"</div><div class="rv-u"><div class="rv-a" style="background:#10B981">M</div><div><div class="rv-n">Mohammed R.</div><div class="rv-d">1 week ago</div></div></div></div>
    <div class="rv"><div class="rv-s">★★★★★</div><div class="rv-t">"Very professional. Fast delivery. Using this forever!"</div><div class="rv-u"><div class="rv-a" style="background:#F59E0B">L</div><div><div class="rv-n">Layla H.</div><div class="rv-d">2 weeks ago</div></div></div></div>
    <div class="rv"><div class="rv-s">★★★★★</div><div class="rv-t">"Free Fire diamonds received in 3 minutes. Amazing!"</div><div class="rv-u"><div class="rv-a" style="background:#EF4444">K</div><div><div class="rv-n">Kareem A.</div><div class="rv-d">3 weeks ago</div></div></div></div>
  </div>
</div>

<!-- ORDERS -->
<div class="page" id="pg-orders">
  <div style="padding:12px">
    <div class="sec-h" style="margin-bottom:12px"><div class="sec-t">My Orders</div><div class="sec-s" id="orders-count">0 orders</div></div>
    <div class="empty" id="orders-empty"><div class="ei">📭</div><div class="et">No Orders Yet</div><div class="ed">Your purchased gift cards will appear here after payment confirmation.</div></div>
    <div id="orders-list"></div>
  </div>
</div>

<!-- PROFILE -->
<div class="page" id="pg-profile">
  <div class="ph">
    <div class="pav" id="prof-av">👤</div>
    <div class="pname" id="prof-name">Loading...</div>
    <div class="pid" id="prof-id">Telegram User</div>
    <div class="pstats">
      <div class="ps"><div class="psn" id="ps-orders">0</div><div class="psl">Orders</div></div>
      <div class="ps"><div class="psn" id="ps-pts" style="color:#FCD34D">0</div><div class="psl">Points</div></div>
      <div class="ps"><div class="psn" id="ps-refs" style="color:var(--accent)">0</div><div class="psl">Referrals</div></div>
    </div>
  </div>
  <div class="lyc">
    <div class="ly-l">⭐ Loyalty Points</div>
    <div class="ly-p" id="loy-pts">0</div>
    <div class="ly-s">Earn 10 pts per $1 spent</div>
    <div class="ly-bg"><div class="ly-bar" id="loy-bar" style="width:0%"></div></div>
    <div class="ly-n" id="loy-next">0 / 100 pts to next reward</div>
  </div>
  <div class="refc">
    <div class="ref-t">🎁 Referral Program</div>
    <div class="ref-d">Share your link and earn 50 points for every friend who buys!</div>
    <div class="ref-c"><div class="ref-ct" id="ref-code">NOVA-XXXX</div><button class="ref-cp" onclick="copyRef()">Copy Link</button></div>
    <div class="ref-i">
      <div class="rii"><div class="riin" id="ref-invited">0</div><div class="riil">Invited</div></div>
      <div class="rii"><div class="riin" id="ref-earned" style="color:#FCD34D">0</div><div class="riil">Pts Earned</div></div>
    </div>
  </div>
  <div class="tbox" style="margin:0 12px 12px">
    <div class="ttitle">Account</div>
    <div class="trow" onclick="navTo('orders')"><div class="ti">📦</div><div class="tt"><div class="ttn">My Orders</div><div class="ttd">View all your purchases</div></div><div style="color:var(--t2)">›</div></div>
    <div class="trow" onclick="navTo('support')"><div class="ti">💬</div><div class="tt"><div class="ttn">Support</div><div class="ttd">Get help from our team</div></div><div style="color:var(--t2)">›</div></div>
  </div>
</div>

<!-- SUPPORT -->
<div class="page" id="pg-support">
  <div style="padding:12px">
    <div class="sec-h" style="margin-bottom:12px"><div class="sec-t">Support</div></div>
    <div class="sbox">
      <div class="srow" onclick="openTg()"><div class="si">✈️</div><div class="stt"><div class="stn">Telegram Support</div><div class="std">Chat with us — avg. reply under 3 min</div></div><div style="color:var(--t2)">›</div></div>
      <div class="srow"><div class="si">❓</div><div class="stt"><div class="stn">How It Works</div><div class="std">Browse → Select → Pay → Receive code instantly</div></div></div>
      <div class="srow"><div class="si">💎</div><div class="stt"><div class="stn">Accepted Payments</div><div class="std">TON, USDT TRC20, USDT ERC20</div></div></div>
      <div class="srow"><div class="si">⚡</div><div class="stt"><div class="stn">Delivery Time</div><div class="std">1–15 minutes after blockchain confirmation</div></div></div>
      <div class="srow"><div class="si">🔄</div><div class="stt"><div class="stn">Refund Policy</div><div class="std">Invalid cards replaced immediately.</div></div></div>
      <div class="srow"><div class="si">🎁</div><div class="stt"><div class="stn">First Order Discount</div><div class="std">Use code NOVA5 for 5% off your first order</div></div></div>
      <div class="srow"><div class="si">⭐</div><div class="stt"><div class="stn">Loyalty Points</div><div class="std">Earn 10 pts per $1. Redeem for discounts.</div></div></div>
    </div>
  </div>
</div>
```

  </div>

  <div class="bnav">
    <div class="nb on" onclick="navTo('home',this)" id="nav-home"><div class="ni">🏪</div><div class="nl">Store</div></div>
    <div class="nb" onclick="navTo('orders',this)" id="nav-orders"><div class="ni">📦</div><div class="nl">Orders</div></div>
    <div class="nb" onclick="navTo('profile',this)" id="nav-profile"><div class="ni">👤</div><div class="nl">Profile</div></div>
    <div class="nb" onclick="navTo('support',this)" id="nav-support"><div class="ni">💬</div><div class="nl">Support</div></div>
  </div>
</div>

<!-- PRODUCT SHEET -->

<div class="ov" id="ov-product" onclick="closeOv(event,'ov-product')">
  <div class="sh"><div class="handle"></div><div class="sb" id="product-body"></div></div>
</div>

<!-- PAYMENT SHEET -->

<div class="ov" id="ov-pay" onclick="closeOv(event,'ov-pay')">
  <div class="sh"><div class="handle"></div><div class="sb" id="pay-body"></div></div>
</div>

<div class="toast" id="toast"></div>

<script>
const USDT_TRC='TERUMbyPWyMHMijgSBrYZ9UWk4UquBs3ub';
const USDT_ERC='TERUMbyPWyMHMijgSBrYZ9UWk4UquBs3ub';
const TON_ADDR='UQDNEWfXJe0hCYsfZ6q4oMKB5ns3Y8dOktNkm00CGL7WyhJy';
const BOT='Novaacards_bot';
const OWNER_ID='816394591';
const BOT_TOKEN='YOUR_BOT_TOKEN_HERE';
const tg=window.Telegram?.WebApp;
if(tg){tg.ready();tg.expand();}
const tgUser=tg?.initDataUnsafe?.user||{first_name:'Guest',id:'000000'};
let state=JSON.parse(localStorage.getItem('nova_state')||'null')||{pts:0,orders:[],refCount:0,refPts:0};
let selAmt=0,curProd=null,curNet='usdt-trc';
function saveState(){localStorage.setItem('nova_state',JSON.stringify(state));}

// CARD VISUALS
const V={
  amazon:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="amz" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#FF9900"/><stop offset="100%" style="stop-color:#E47911"/></linearGradient></defs><rect width="200" height="96" fill="url(#amz)"/><rect width="200" height="96" fill="rgba(0,0,0,0.18)"/><circle cx="160" cy="18" r="45" fill="rgba(255,255,255,0.05)"/><text x="100" y="42" font-family="Arial Black" font-size="22" font-weight="900" fill="white" text-anchor="middle">amazon</text><path d="M62 52 Q100 62 138 52" stroke="#FF9900" stroke-width="3" fill="none" stroke-linecap="round"/><polygon points="134,48 138,52 134,56" fill="#FF9900"/><text x="100" y="70" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.6)" text-anchor="middle" letter-spacing="3">GIFT CARD</text></svg>`,icon:'🛒'},
  googleplay:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="gp" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#01875F"/><stop offset="100%" style="stop-color:#00C853"/></linearGradient></defs><rect width="200" height="96" fill="url(#gp)"/><rect width="200" height="96" fill="rgba(0,0,0,0.15)"/><polygon points="25,22 25,74 58,48" fill="rgba(255,255,255,0.2)"/><text x="115" y="38" font-family="Arial" font-size="13" font-weight="700" fill="white" text-anchor="middle">Google Play</text><rect x="75" y="44" width="80" height="2" rx="1" fill="rgba(255,255,255,0.2)"/><text x="115" y="60" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.55)" text-anchor="middle" letter-spacing="2">GIFT CARD</text></svg>`,icon:'▶️'},
  itunes:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="it" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#FC3C44"/><stop offset="100%" style="stop-color:#BF0030"/></linearGradient></defs><rect width="200" height="96" fill="url(#it)"/><rect width="200" height="96" fill="rgba(0,0,0,0.18)"/><circle cx="100" cy="44" r="20" fill="rgba(255,255,255,0.12)" stroke="rgba(255,255,255,0.25)" stroke-width="1.5"/><polygon points="96,37 96,51 109,44" fill="white" opacity="0.85"/><text x="100" y="76" font-family="Arial" font-size="10" fill="rgba(255,255,255,0.55)" text-anchor="middle" letter-spacing="3">iTunes GIFT CARD</text></svg>`,icon:'🎵'},
  steam:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="st" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#1B2838"/><stop offset="100%" style="stop-color:#2A475E"/></linearGradient></defs><rect width="200" height="96" fill="url(#st)"/><circle cx="165" cy="18" r="50" fill="rgba(102,192,244,0.05)"/><text x="100" y="46" font-family="Arial Black" font-size="20" font-weight="900" fill="white" text-anchor="middle" letter-spacing="2">STEAM</text><rect x="35" y="52" width="130" height="2" rx="1" fill="rgba(102,192,244,0.35)"/><text x="100" y="68" font-family="Arial" font-size="9" fill="rgba(102,192,244,0.6)" text-anchor="middle" letter-spacing="3">WALLET CARD</text></svg>`,icon:'🎮'},
  netflix:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="nf" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#E50914"/><stop offset="100%" style="stop-color:#8B0000"/></linearGradient></defs><rect width="200" height="96" fill="url(#nf)"/><rect width="200" height="96" fill="rgba(0,0,0,0.25)"/><rect x="18" y="14" width="7" height="68" fill="rgba(255,255,255,0.85)"/><rect x="175" y="14" width="7" height="68" fill="rgba(255,255,255,0.85)"/><text x="100" y="56" font-family="Arial Black" font-size="18" font-weight="900" fill="white" text-anchor="middle" letter-spacing="1">NETFLIX</text><text x="100" y="72" font-family="Arial" font-size="8" fill="rgba(255,255,255,0.4)" text-anchor="middle" letter-spacing="3">GIFT CARD</text></svg>`,icon:'🎬'},
  playstation:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="ps" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#0072CE"/><stop offset="100%" style="stop-color:#003087"/></linearGradient></defs><rect width="200" height="96" fill="url(#ps)"/><rect width="200" height="96" fill="rgba(0,0,0,0.15)"/><circle cx="62" cy="48" r="10" fill="none" stroke="rgba(255,255,255,0.5)" stroke-width="2.5"/><rect x="75" y="40" width="5" height="20" rx="1.5" fill="rgba(255,255,255,0.5)"/><rect x="71" y="44" width="13" height="5" rx="1.5" fill="rgba(255,255,255,0.5)"/><circle cx="100" cy="48" r="5" fill="rgba(255,80,80,0.8)"/><circle cx="115" cy="40" r="5" fill="rgba(80,80,255,0.8)"/><circle cx="115" cy="56" r="5" fill="rgba(80,200,80,0.8)"/><circle cx="130" cy="48" r="5" fill="rgba(255,200,0,0.8)"/><text x="100" y="80" font-family="Arial" font-size="8" fill="rgba(255,255,255,0.4)" text-anchor="middle" letter-spacing="3">PLAYSTATION GIFT CARD</text></svg>`,icon:'🕹️'},
  xbox:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="xb" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#52B043"/><stop offset="100%" style="stop-color:#107C10"/></linearGradient></defs><rect width="200" height="96" fill="url(#xb)"/><rect width="200" height="96" fill="rgba(0,0,0,0.15)"/><circle cx="100" cy="44" r="26" fill="rgba(0,0,0,0.2)"/><circle cx="100" cy="44" r="20" fill="rgba(255,255,255,0.06)" stroke="rgba(255,255,255,0.12)" stroke-width="1"/><text x="100" y="50" font-family="Arial Black" font-size="18" font-weight="900" fill="rgba(255,255,255,0.9)" text-anchor="middle">XBOX</text><text x="100" y="78" font-family="Arial" font-size="8" fill="rgba(255,255,255,0.35)" text-anchor="middle" letter-spacing="3">GIFT CARD</text></svg>`,icon:'🟢'},
  spotify:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="sp" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#1DB954"/><stop offset="100%" style="stop-color:#158a3e"/></linearGradient></defs><rect width="200" height="96" fill="url(#sp)"/><rect width="200" height="96" fill="rgba(0,0,0,0.15)"/><circle cx="100" cy="42" r="22" fill="rgba(0,0,0,0.2)"/><path d="M85 34 Q100 30 115 34" stroke="white" stroke-width="3" fill="none" stroke-linecap="round" opacity="0.9"/><path d="M83 42 Q100 37 117 42" stroke="white" stroke-width="3" fill="none" stroke-linecap="round" opacity="0.9"/><path d="M86 50 Q100 46 114 50" stroke="white" stroke-width="3" fill="none" stroke-linecap="round" opacity="0.9"/><text x="100" y="76" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.55)" text-anchor="middle" letter-spacing="3">SPOTIFY GIFT CARD</text></svg>`,icon:'🎧'},
  pubg:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="pb" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#F5A623"/><stop offset="100%" style="stop-color:#C47D0E"/></linearGradient></defs><rect width="200" height="96" fill="url(#pb)"/><rect width="200" height="96" fill="rgba(0,0,0,0.35)"/><ellipse cx="100" cy="32" rx="18" ry="20" fill="none" stroke="rgba(245,166,35,0.8)" stroke-width="2.5"/><rect x="88" y="22" width="24" height="4" rx="2" fill="rgba(245,166,35,0.6)"/><text x="100" y="62" font-family="Arial Black" font-size="16" font-weight="900" fill="white" text-anchor="middle" letter-spacing="1">PUBG</text><text x="100" y="76" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.5)" text-anchor="middle" letter-spacing="2">UC VOUCHER</text></svg>`,icon:'🎯'},
  freefire:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="ff" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#FF4500"/><stop offset="100%" style="stop-color:#8B0000"/></linearGradient></defs><rect width="200" height="96" fill="url(#ff)"/><rect width="200" height="96" fill="rgba(0,0,0,0.2)"/><polygon points="100,15 108,35 100,30 92,35" fill="rgba(255,200,0,0.8)"/><polygon points="100,28 112,50 100,44 88,50" fill="rgba(255,100,0,0.7)"/><text x="100" y="66" font-family="Arial Black" font-size="13" font-weight="900" fill="white" text-anchor="middle" letter-spacing="1">FREE FIRE</text><text x="100" y="80" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.5)" text-anchor="middle" letter-spacing="2">DIAMONDS</text></svg>`,icon:'💎'},
  roblox:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="rb" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#E31414"/><stop offset="100%" style="stop-color:#A00000"/></linearGradient></defs><rect width="200" height="96" fill="url(#rb)"/><rect width="200" height="96" fill="rgba(0,0,0,0.15)"/><rect x="80" y="22" width="40" height="40" rx="4" fill="rgba(255,255,255,0.15)" transform="rotate(-15 100 42)"/><rect x="83" y="25" width="34" height="34" rx="3" fill="rgba(255,255,255,0.1)" transform="rotate(-15 100 42)"/><text x="100" y="74" font-family="Arial Black" font-size="14" font-weight="900" fill="white" text-anchor="middle" letter-spacing="1">ROBLOX</text></svg>`,icon:'🟥'},
  razer:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="rz" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#00FF00"/><stop offset="100%" style="stop-color:#007700"/></linearGradient></defs><rect width="200" height="96" fill="#0D0D0D"/><rect width="200" height="96" fill="rgba(0,255,0,0.03)"/><polygon points="100,16 115,36 108,36 120,56 100,46 80,56 92,36 85,36" fill="rgba(0,255,0,0.7)"/><text x="100" y="72" font-family="Arial Black" font-size="13" font-weight="900" fill="#00FF00" text-anchor="middle" letter-spacing="2" opacity="0.9">RAZER GOLD</text></svg>`,icon:'🐍'},
  apple:{svg:`<svg viewBox="0 0 200 96" xmlns="http://www.w3.org/2000/svg"><defs><linearGradient id="ap" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#555"/><stop offset="100%" style="stop-color:#111"/></linearGradient></defs><rect width="200" height="96" fill="url(#ap)"/><circle cx="100" cy="40" r="18" fill="rgba(255,255,255,0.08)" stroke="rgba(255,255,255,0.15)" stroke-width="1"/><text x="101" y="47" font-family="Arial" font-size="22" fill="white" text-anchor="middle" opacity="0.85"></text><text x="100" y="72" font-family="Arial" font-size="9" fill="rgba(255,255,255,0.45)" text-anchor="middle" letter-spacing="2">APP STORE GIFT CARD</text></svg>`,icon:'🍎'},
};

const products=[
  {id:1,name:'Amazon',key:'amazon',cat:'shopping',desc:'Shop millions of items on Amazon globally.',amts:['$10','$25','$50','$100','$200'],prices:['10.5 USDT','26 USDT','52 USDT','103 USDT','205 USDT'],usd:[10,25,50,100,200],badge:'hot',buyers:892},
  {id:2,name:'Google Play',key:'googleplay',cat:'gaming',desc:'Apps, games and subscriptions for Android.',amts:['$10','$25','$50','$100'],prices:['10.5 USDT','26 USDT','52 USDT','103 USDT'],usd:[10,25,50,100],badge:'hot',buyers:654},
  {id:3,name:'iTunes',key:'itunes',cat:'music',desc:'Music, movies and apps for Apple devices.',amts:['$10','$25','$50','$100'],prices:['10.5 USDT','26 USDT','52 USDT','103 USDT'],usd:[10,25,50,100],badge:'pop',buyers:743},
  {id:4,name:'Steam',key:'steam',cat:'gaming',desc:'Thousands of PC games on Steam.',amts:['$10','$20','$50','$100'],prices:['10.5 USDT','21 USDT','52 USDT','103 USDT'],usd:[10,20,50,100],badge:'',buyers:421},
  {id:5,name:'Netflix',key:'netflix',cat:'streaming',desc:'Stream shows and movies worldwide.',amts:['$15','$30','$50','$100'],prices:['15.5 USDT','31 USDT','52 USDT','103 USDT'],usd:[15,30,50,100],badge:'pop',buyers:567},
  {id:6,name:'PlayStation',key:'playstation',cat:'gaming',desc:'Games, PS Plus and DLC on PSN.',amts:['$10','$20','$50','$100'],prices:['10.5 USDT','21 USDT','52 USDT','103 USDT'],usd:[10,20,50,100],badge:'',buyers:312},
  {id:7,name:'Xbox',key:'xbox',cat:'gaming',desc:'Games and Xbox Game Pass content.',amts:['$10','$25','$50','$100'],prices:['10.5 USDT','26 USDT','52 USDT','103 USDT'],usd:[10,25,50,100],badge:'',buyers:278},
  {id:8,name:'Spotify',key:'spotify',cat:'music',desc:'Music streaming for all devices worldwide.',amts:['$10','$30','$60'],prices:['10.5 USDT','31 USDT','62 USDT'],usd:[10,30,60],badge:'new',buyers:445},
  {id:9,name:'PUBG Mobile',key:'pubg',cat:'gaming',desc:'UC voucher for PUBG Mobile. Works globally.',amts:['60 UC','325 UC','660 UC','1800 UC'],prices:['1.5 USDT','6 USDT','10 USDT','25 USDT'],usd:[1.5,6,10,25],badge:'hot',buyers:1243},
  {id:10,name:'Free Fire',key:'freefire',cat:'gaming',desc:'Diamonds for Free Fire. Instant delivery.',amts:['100 💎','310 💎','520 💎','1080 💎'],prices:['2 USDT','5 USDT','8 USDT','15 USDT'],usd:[2,5,8,15],badge:'hot',buyers:987},
  {id:11,name:'Roblox',key:'roblox',cat:'gaming',desc:'Robux for Roblox platform. Works worldwide.',amts:['400 Robux','800 Robux','1700 Robux'],prices:['5 USDT','10 USDT','20 USDT'],usd:[5,10,20],badge:'new',buyers:534},
  {id:12,name:'Razer Gold',key:'razer',cat:'gaming',desc:'Razer Gold for mobile and PC gaming.',amts:['$5','$10','$20','$50'],prices:['5.5 USDT','10.5 USDT','21 USDT','52 USDT'],usd:[5,10,20,50],badge:'new',buyers:189},
  {id:13,name:'Apple Store',key:'apple',cat:'shopping',desc:'App Store & iTunes for all Apple services.',amts:['$10','$25','$50','$100'],prices:['10.5 USDT','26 USDT','52 USDT','103 USDT'],usd:[10,25,50,100],badge:'pop',buyers:621},
];

const badgeMap={hot:'🔥 Hot',new:'✨ New',pop:'⭐ Popular',sale:'🏷️ Sale'};

function renderCards(list){
  const g=document.getElementById('cards-grid');
  document.getElementById('card-count').textContent=list.length+' cards';
  g.innerHTML=list.map((p,i)=>{
    const v=V[p.key];
    const bdg=p.badge?`<div class="badge-wrap"><div class="badge b-${p.badge}">${badgeMap[p.badge]}</div></div>`:'';
    return `<div class="card" style="animation-delay:${i*0.04}s" onclick="openProduct(${p.id})">
      <div class="cv">${v.svg}${bdg}</div>
      <div class="c-info">
        <div class="c-name">${p.name}</div>
        <div class="c-price">From ${p.prices[0]}</div>
        <div class="c-foot">
          <div class="c-chip">USDT·TON</div>
          <div class="c-buyers">👥 ${p.buyers}</div>
        </div>
      </div>
    </div>`;
  }).join('');
}

function filterCat(cat,btn){
  document.querySelectorAll('.cat').forEach(b=>b.classList.remove('on'));
  btn.classList.add('on');
  renderCards(cat==='all'?products:products.filter(p=>p.cat===cat));
}
function doSearch(q){renderCards(products.filter(p=>p.name.toLowerCase().includes(q.toLowerCase())));}

function openProduct(id){
  curProd=products.find(p=>p.id===id);selAmt=0;
  const v=V[curProd.key];
  document.getElementById('product-body').innerHTML=`
    <div class="sh-img">${v.svg}</div>
    <div class="sh-title">${curProd.name} Gift Card</div>
    <div class="sh-desc">${curProd.desc}</div>
    <div class="lbl">Select Amount</div>
    <div class="ag">${curProd.amts.map((a,i)=>`<div class="ab ${i===0?'on':''}" onclick="selAmt2(${i},this)">${a}<div class="as">${curProd.prices[i]}</div></div>`).join('')}</div>
    <div class="sum">
      <div class="sr"><span class="sl2">Item</span><span class="sv">${curProd.name} <span id="sv-amt">${curProd.amts[0]}</span></span></div>
      <div class="sr"><span class="sl2">You Pay</span><span class="sv a" id="sv-price">${curProd.prices[0]}</span></div>
      <div class="sr"><span class="sl2">Points Earned</span><span class="sv y" id="sv-pts">+${curProd.usd[0]*10} pts</span></div>
      <div class="sr"><span class="sl2">Delivery</span><span class="sv g">⚡ Instant</span></div>
    </div>
    <button class="btn-main" id="buy-btn" onclick="openPay()">Buy Now — ${curProd.prices[0]}</button>
  `;
  document.getElementById('ov-product').classList.add('on');
}

function selAmt2(i,el){
  selAmt=i;
  document.querySelectorAll('.ab').forEach(b=>b.classList.remove('on'));
  el.classList.add('on');
  document.getElementById('sv-amt').textContent=curProd.amts[i];
  document.getElementById('sv-price').textContent=curProd.prices[i];
  document.getElementById('sv-pts').textContent='+'+curProd.usd[i]*10+' pts';
  document.getElementById('buy-btn').textContent='Buy Now — '+curProd.prices[i];
}

function openPay(){
  document.getElementById('ov-product').classList.remove('on');
  const p=curProd,amt=p.amts[selAmt],price=p.prices[selAmt];
  curNet='usdt-trc';
  document.getElementById('pay-body').innerHTML=`
    <div style="text-align:center;margin-bottom:14px">
      <div style="font-size:30px;margin-bottom:7px">💳</div>
      <div style="font-size:16px;font-weight:800;margin-bottom:3px">Complete Payment</div>
      <div style="font-size:11px;color:var(--t2)">Send <strong style="color:var(--accent)">${price}</strong> for <strong>${p.name} ${amt}</strong></div>
    </div>
    <div class="lbl">Choose Payment Method</div>
    <div class="pms">
      <div class="pm ton" id="pm-ton" onclick="switchNet('ton',this)"><div class="pm-ic">💎</div><div class="pm-n">TON</div><div class="pm-s">Telegram Wallet</div></div>
      <div class="pm on" id="pm-trc" onclick="switchNet('usdt-trc',this)"><div class="pm-ic">💵</div><div class="pm-n">USDT</div><div class="pm-s">TRC20</div></div>
      <div class="pm" id="pm-erc" onclick="switchNet('usdt-erc',this)"><div class="pm-ic">💵</div><div class="pm-n">USDT</div><div class="pm-s">ERC20</div></div>
    </div>
    <div id="addr-sec">
      <div class="lbl">Send to this address</div>
      <div class="abox" id="pay-addr">${USDT_TRC}</div>
      <button class="btn-copy" onclick="copyAddr()">📋 Copy Address</button>
    </div>
    <button id="btn-ton" style="display:none" class="btn-ton" onclick="payTon()">💎 Open Telegram Wallet</button>
    <div class="warn">⚠️ Send exactly <strong>${price}</strong>. Wrong network = lost funds. Double-check!</div>
    <button class="btn-confirm" id="btn-confirm" onclick="confirmPay()">✅ I've Sent the Payment</button>
    <div style="font-size:10px;color:var(--t2);text-align:center;margin-top:10px;line-height:1.5;padding-bottom:4px">After confirming, we verify on-chain and deliver your card within 15 minutes.</div>
  `;
  document.getElementById('ov-pay').classList.add('on');
}

function switchNet(net,el){
  curNet=net;
  document.querySelectorAll('.pm').forEach(m=>m.classList.remove('on'));
  el.classList.add('on');
  const isTon=net==='ton';
  document.getElementById('pay-addr').textContent=net==='usdt-erc'?USDT_ERC:net==='ton'?TON_ADDR:USDT_TRC;
  document.getElementById('addr-sec').style.display=isTon?'none':'block';
  document.getElementById('btn-ton').style.display=isTon?'block':'none';
  document.getElementById('btn-confirm').style.display=isTon?'none':'block';
}

function payTon(){
  const p=curProd,price=p.prices[selAmt];
  const comment=encodeURIComponent('Novaacards '+p.name+' '+p.amts[selAmt]);
  window.open('ton://transfer/'+TON_ADDR+'?amount='+Math.round(parseFloat(price)*1e9)+'&text='+comment,'_blank');
  setTimeout(()=>{
    document.getElementById('btn-ton').style.display='none';
    document.getElementById('btn-confirm').style.display='block';
    document.getElementById('btn-confirm').textContent='✅ I Sent TON Payment';
  },1500);
}

function copyAddr(){navigator.clipboard?.writeText(document.getElementById('pay-addr').textContent);showToast('✅ Address copied!');}
function copyDiscount(){navigator.clipboard?.writeText('NOVA5');showToast('✅ Code NOVA5 copied!');}

async function confirmPay(){
  document.getElementById('ov-pay').classList.remove('on');
  const p=curProd,amt=p.amts[selAmt],price=p.prices[selAmt],pts=p.usd[selAmt]*10;
  const orderId='NOV-'+Date.now().toString().slice(-6);
  const userName=tgUser.first_name+(tgUser.last_name?' '+tgUser.last_name:'');
  const userHandle=tgUser.username?'@'+tgUser.username:'No username';
  const netLabels={'usdt-trc':'USDT TRC20','usdt-erc':'USDT ERC20','ton':'TON'};
  state.pts+=pts;
  state.orders.unshift({id:orderId,name:p.name+' '+amt,emoji:V[p.key].icon,price:price,pts:pts,status:'pending',date:new Date().toLocaleDateString(),net:netLabels[curNet]});
  saveState();updateUI();
  if(BOT_TOKEN!=='YOUR_BOT_TOKEN_HERE'){
    try{
      const msg=`🛒 NEW ORDER #${orderId}\n\n📦 ${p.name} ${amt}\n💰 ${price}\n🌐 ${netLabels[curNet]}\n👤 ${userName}\n🔗 ${userHandle}\n🆔 ${tgUser.id||'?'}\n📅 ${new Date().toLocaleString()}\n\n⚠️ Check wallet then send card!`;
      await fetch('https://api.telegram.org/bot'+BOT_TOKEN+'/sendMessage',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({chat_id:OWNER_ID,text:msg})});
    }catch(e){}
  }
  showToast('⏳ Order #'+orderId+' placed! +'+pts+' pts 🎉');
  navTo('orders');
}

function renderOrders(){
  const list=document.getElementById('orders-list');
  const empty=document.getElementById('orders-empty');
  document.getElementById('orders-count').textContent=state.orders.length+' orders';
  if(!state.orders.length){empty.style.display='block';list.innerHTML='';return;}
  empty.style.display='none';
  list.innerHTML=state.orders.map(o=>`
    <div class="oi">
      <div class="oie">${o.emoji}</div>
      <div class="oii"><div class="oin">${o.name}</div><div class="oip">Paid: ${o.price} · +${o.pts} pts · ${o.net||''}</div><div class="oid">${o.date} · #${o.id}</div></div>
      <div class="obp ${o.status==='done'?'od':'op'}">${o.status==='done'?'✅ Delivered':'⏳ Pending'}</div>
    </div>`).join('');
}

function renderProfile(){
  const name=tgUser.first_name+(tgUser.last_name?' '+tgUser.last_name:'');
  const initials=name.split(' ').map(n=>n[0]).join('').toUpperCase().slice(0,2);
  document.getElementById('prof-av').textContent=initials||'👤';
  document.getElementById('prof-name').textContent=name||'Guest';
  document.getElementById('prof-id').textContent='@'+(tgUser.username||'user')+' · ID: '+(tgUser.id||'---');
  document.getElementById('ps-orders').textContent=state.orders.length;
  document.getElementById('ps-pts').textContent=state.pts;
  document.getElementById('ps-refs').textContent=state.refCount;
  document.getElementById('loy-pts').textContent=state.pts;
  document.getElementById('loy-bar').style.width=Math.min((state.pts%100),100)+'%';
  document.getElementById('loy-next').textContent=(state.pts%100)+' / 100 pts to next reward';
  const code='NOVA-'+(tgUser.id||'0000').toString().slice(-4).toUpperCase();
  document.getElementById('ref-code').textContent=code;
  document.getElementById('ref-invited').textContent=state.refCount;
  document.getElementById('ref-earned').textContent=state.refPts;
}

function copyRef(){
  navigator.clipboard?.writeText('https://t.me/'+BOT+'?start='+document.getElementById('ref-code').textContent);
  showToast('✅ Referral link copied!');
}

function navTo(page,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('on'));
  document.querySelectorAll('.nb').forEach(n=>n.classList.remove('on'));
  document.getElementById('pg-'+page).classList.add('on');
  const nav=el||document.getElementById('nav-'+page);
  if(nav)nav.classList.add('on');
  document.querySelector('.pc').scrollTo(0,0);
  if(page==='orders')renderOrders();
  if(page==='profile')renderProfile();
}

function closeOv(e,id){if(e.target===document.getElementById(id))document.getElementById(id).classList.remove('on');}
function updateUI(){document.getElementById('hdr-pts').textContent=state.pts;}
function showToast(msg){const t=document.getElementById('toast');t.textContent=msg;t.classList.add('on');setTimeout(()=>t.classList.remove('on'),2500);}
function openTg(){window.open('https://t.me/'+BOT,'_blank');}

// FLASH SALE TIMER
function startTimer(){
  let h=23,m=59,s=59;
  setInterval(()=>{
    s--;if(s<0){s=59;m--;}if(m<0){m=59;h--;}if(h<0){h=23;}
    document.getElementById('timer').textContent=
      String(h).padStart(2,'0')+':'+String(m).padStart(2,'0')+':'+String(s).padStart(2,'0');
  },1000);
}

renderCards(products);updateUI();startTimer();
</script>

</body>
</html>
