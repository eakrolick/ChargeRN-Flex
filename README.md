<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Bend ED — Charge RN Flex</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap');
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#0d1117;--s1:#161b22;--s2:#1c2331;--s3:#21262d;
  --b1:rgba(255,255,255,.07);--b2:rgba(255,255,255,.13);
  --t1:#e6edf3;--t2:#8b949e;--t3:#484f58;
  --green:#2ea043;--green-dim:rgba(46,160,67,.18);--green-line:rgba(46,160,67,.5);
  --blue:#58a6ff; --blue-dim:rgba(88,166,255,.15); --blue-line:rgba(88,166,255,.5);
  --amber:#e3b341;--amber-dim:rgba(227,179,65,.15);--amber-line:rgba(227,179,65,.5);
  --red:#f85149;  --red-dim:rgba(248,81,73,.15);   --red-line:rgba(248,81,73,.5);
  --purple:#b08eff;--purple-dim:rgba(176,142,255,.15);--purple-line:rgba(176,142,255,.4);
  --font:'DM Sans',system-ui,sans-serif;--mono:'DM Mono',monospace;
}
html,body{min-height:100%;overflow-x:hidden}
body{background:var(--bg);color:var(--t1);font-family:var(--font);font-size:14px}
.hdr{background:var(--s1);border-bottom:1px solid var(--b1);padding:10px 18px;
     display:flex;align-items:center;justify-content:space-between;
     position:sticky;top:0;z-index:50}
.hdr-title{font-size:13px;font-weight:600}
.hdr-sub{font-size:10px;color:var(--t3);font-family:var(--mono);margin-top:1px}
.clock{font-family:var(--mono);font-size:13px;color:var(--t2);display:flex;align-items:center;gap:7px}
.dot{width:7px;height:7px;border-radius:50%;background:var(--green);animation:blink 2.2s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}
.signal{margin:14px 16px 0;border-radius:12px;padding:14px 18px;border:1px solid;
        display:grid;grid-template-columns:48px 1fr auto;align-items:center;gap:12px}
.sig-icon{font-size:30px;text-align:center}
.sig-tag{font-size:10px;font-weight:600;letter-spacing:.12em;font-family:var(--mono);margin-bottom:2px}
.sig-msg{font-size:15px;font-weight:500;line-height:1.3}
.sig-sub{font-size:11px;margin-top:3px;opacity:.7}
.rec-block{text-align:right;flex-shrink:0}
.rec-now{font-size:28px;font-weight:600;font-family:var(--mono);line-height:1}
.rec-lbl{font-size:10px;color:var(--t2);margin-top:2px}
.rec-2hr{font-size:11px;margin-top:5px;font-family:var(--mono)}
.rec-2lbl{font-size:10px;color:var(--t3)}
.s-ok  {background:var(--green-dim); border-color:var(--green-line)}
.s-ok   .sig-tag,.s-ok   .rec-now{color:var(--green)}
.s-hold {background:var(--blue-dim);  border-color:var(--blue-line)}
.s-hold  .sig-tag,.s-hold  .rec-now{color:var(--blue)}
.s-watch{background:var(--amber-dim);border-color:var(--amber-line)}
.s-watch .sig-tag,.s-watch .rec-now{color:var(--amber)}
.s-call {background:var(--red-dim);  border-color:var(--red-line)}
.s-call  .sig-tag,.s-call  .rec-now{color:var(--red)}
.s-flex {background:var(--purple-dim);border-color:var(--purple-line)}
.s-flex  .sig-tag,.s-flex  .rec-now{color:var(--purple)}

/* Q3H strip */
.q3h{margin:10px 16px 0;background:var(--s1);border:1px solid var(--b1);border-radius:10px;
     padding:10px 14px;display:grid;grid-template-columns:1fr auto auto;gap:14px;align-items:center;
     transition:background .25s,border-color .25s}
.q3h.due{background:var(--amber-dim);border-color:var(--amber-line)}
.q3h.overdue{background:var(--red-dim);border-color:var(--red-line)}
.q3h-tag{font-size:9px;font-weight:600;letter-spacing:.12em;font-family:var(--mono);color:var(--t3)}
.q3h.due .q3h-tag{color:var(--amber)}
.q3h.overdue .q3h-tag{color:var(--red)}
.q3h-stat{font-size:12px;color:var(--t1);margin-top:2px;line-height:1.35}
.q3h-cd{font-family:var(--mono);font-size:13px;color:var(--t2);text-align:right;white-space:nowrap}
.q3h.due .q3h-cd{color:var(--amber)}
.q3h.overdue .q3h-cd{color:var(--red);font-weight:500}
.q3h-btn{background:var(--s2);border:1px solid var(--b2);color:var(--t1);
         font-family:var(--font);font-size:13px;font-weight:600;
         padding:9px 14px;border-radius:7px;cursor:pointer;
         touch-action:manipulation;-webkit-user-select:none;user-select:none;
         white-space:nowrap;transition:background .2s,transform .1s}
.q3h-btn:active{transform:scale(.96);background:var(--s3)}
.q3h.due .q3h-btn{background:var(--amber);color:#0d1117;border-color:var(--amber)}
.q3h.overdue .q3h-btn{background:var(--red);color:#fff;border-color:var(--red);animation:pulse 1.6s ease-in-out infinite}
@keyframes pulse{0%,100%{box-shadow:0 0 0 0 rgba(248,81,73,.5)}50%{box-shadow:0 0 0 8px rgba(248,81,73,0)}}
.q3h-flash{animation:flash .5s ease}
@keyframes flash{0%{background:var(--green)}100%{background:var(--s2)}}

.body{padding:12px 16px;display:grid;grid-template-columns:1fr 1fr;gap:12px}
@media(max-width:560px){.body{grid-template-columns:1fr}.q3h{grid-template-columns:1fr auto;gap:8px}.q3h-cd{display:none}}
.card{background:var(--s1);border:1px solid var(--b1);border-radius:10px;padding:12px 14px;margin-bottom:10px}
.card:last-child{margin-bottom:0}
.ctitle{font-size:9px;font-weight:600;letter-spacing:.10em;text-transform:uppercase;
        color:var(--t3);font-family:var(--mono);margin-bottom:10px}
.stepper{display:flex;align-items:center;border:1px solid var(--b2);border-radius:7px;overflow:hidden}
.sbtn{background:var(--s2);border:none;color:var(--t2);padding:7px 11px;cursor:pointer;
      font-size:17px;font-family:var(--font);user-select:none;-webkit-user-select:none;touch-action:manipulation}
.sbtn:active{background:var(--s3);color:var(--t1)}
.sval{background:var(--s1);border:none;color:var(--t1);font-size:15px;font-weight:500;
      font-family:var(--mono);text-align:center;width:38px;padding:7px 0;outline:none}
.sval-sm{width:32px;font-size:13px;padding:5px 0}
.sbtn-sm{padding:5px 9px;font-size:15px}
.esi-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:7px}
.esi-cell{display:flex;flex-direction:column;gap:4px}
.elbl{text-align:center;border-radius:5px;padding:3px 0;font-size:11px;font-weight:600;font-family:var(--mono)}
.l1{background:rgba(248,81,73,.2);color:#ff8070}
.l2{background:rgba(255,165,0,.2);color:#ffbb55}
.l3{background:rgba(227,179,65,.15);color:var(--amber)}
.l4{background:rgba(88,166,255,.15);color:var(--blue)}
.l5{background:rgba(46,160,67,.15);color:var(--green)}
.lb{background:rgba(176,142,255,.15);color:var(--purple)}
.rn-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
/* RN staffing */
.rn-total-row{display:flex;align-items:center;justify-content:space-between;padding-bottom:10px;border-bottom:1px solid var(--b1);margin-bottom:10px}
.rn-total-lbl{font-size:13px;color:var(--t1);font-weight:500}
.rn-total-sub{font-size:10px;color:var(--t3);font-family:var(--mono);margin-top:2px}
.rn-roles{display:grid;gap:8px;margin-bottom:10px}
.rn-role-row{display:flex;align-items:center;justify-content:space-between;font-size:12px;color:var(--t2)}
.rn-role-row .role-lbl{display:flex;align-items:center;gap:6px}
.rn-role-row .role-tag{font-size:9px;padding:1px 5px;border-radius:3px;font-family:var(--mono);
                       background:var(--s2);color:var(--t3);letter-spacing:.04em}
.rn-derived{display:flex;align-items:center;justify-content:space-between;
            padding-top:9px;border-top:1px solid var(--b1)}
.rn-derived-lbl{font-size:11px;color:var(--t2);font-family:var(--mono);letter-spacing:.04em;text-transform:uppercase}
.rn-derived-num{font-family:var(--mono);font-size:22px;font-weight:600;color:var(--blue)}
.rn-warn{font-size:11px;color:var(--amber);margin-top:6px;font-family:var(--mono);line-height:1.4}
.brk-sig{display:flex;align-items:center;gap:5px;padding:6px 10px;border-radius:6px;
         font-size:11px;font-weight:500;margin-top:9px;font-family:var(--mono);line-height:1.4}
.brk-ok   {background:var(--green-dim); color:var(--green);border:1px solid var(--green-line)}
.brk-short{background:var(--amber-dim);color:var(--amber);border:1px solid var(--amber-line)}
.brk-flex {background:var(--blue-dim); color:var(--blue); border:1px solid var(--blue-line)}
.brk-na   {background:var(--s2);       color:var(--t3);   border:1px solid var(--b1)}
.brk-note{font-size:10px;color:var(--t3);font-family:var(--mono);margin-top:5px;line-height:1.5}
.brk-mode{margin-top:10px;display:flex;align-items:center;justify-content:space-between;gap:8px}
.brk-mode-lbl{font-size:10px;color:var(--t3);font-family:var(--mono);letter-spacing:.05em;text-transform:uppercase}
.brk-mode-toggle{display:inline-flex;border:1px solid var(--b2);border-radius:6px;overflow:hidden}
.brk-mode-btn{background:var(--s2);border:none;color:var(--t2);padding:5px 10px;
              font-size:10px;font-weight:500;font-family:var(--mono);cursor:pointer;letter-spacing:.04em;
              touch-action:manipulation;transition:background .15s,color .15s}
.brk-mode-btn.active{background:var(--blue-dim);color:var(--blue)}
.brk-mode-btn:active{background:var(--s3)}
.brk-mode-suggest{font-size:10px;margin-top:6px;font-family:var(--mono);line-height:1.5}

/* Waiting room */
.wr-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px}
.wr-cell{display:flex;flex-direction:column;gap:4px}
.wlbl{text-align:center;border-radius:5px;padding:3px 0;font-size:10px;font-weight:600;font-family:var(--mono)}
.wr-proj{margin-top:9px;padding:8px 10px;border-radius:7px;font-size:12px;
         line-height:1.7;border-left:3px solid var(--t3);background:var(--s2)}
.wr-proj-hd{font-size:9px;font-weight:600;font-family:var(--mono);letter-spacing:.07em;margin-bottom:2px;color:var(--t3)}
/* Support staff */
.support-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.sup-block{background:var(--s2);border-radius:8px;padding:10px 12px}
.sup-title{font-size:10px;font-weight:600;color:var(--t2);font-family:var(--mono);
           margin-bottom:8px;letter-spacing:.05em;text-transform:uppercase}
.sup-row{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:7px}
.sup-row:last-of-type{margin-bottom:0}
.sup-lbl{font-size:11px;color:var(--t2)}
.sit-sig{display:flex;align-items:center;gap:5px;padding:5px 9px;border-radius:6px;
         font-size:11px;font-weight:500;margin-top:7px;font-family:var(--mono)}
.sit-ok  {background:var(--green-dim); color:var(--green);border:1px solid var(--green-line)}
.sit-warn{background:var(--amber-dim);color:var(--amber);border:1px solid var(--amber-line)}
.sit-bad {background:var(--red-dim);   color:var(--red);  border:1px solid var(--red-line)}
/* APE */
.ape-val{display:flex;align-items:baseline;gap:6px;margin-bottom:4px}
.ape-num{font-size:22px;font-weight:600;font-family:var(--mono)}
.ape-unit{font-size:11px;color:var(--t2)}
.ape-track{height:10px;background:var(--s3);border-radius:5px;overflow:hidden;margin:5px 0 4px}
.ape-fill{height:100%;border-radius:5px;transition:width .25s,background .25s}
.ape-zones{display:flex;justify-content:space-between;font-size:9px;color:var(--t3);font-family:var(--mono)}
.bktable{width:100%;border-collapse:collapse;font-size:12px}
.bktable td{padding:3px 0;border-bottom:1px solid var(--b1)}
.bktable tr:last-child td{border-bottom:none}
.bktable td:last-child{text-align:right;font-family:var(--mono);color:var(--t2)}
.bktable td:first-child{color:var(--t2)}
/* Bands */
.bands{display:grid;grid-template-columns:repeat(4,1fr);gap:5px;margin-top:8px}
.band{border-radius:6px;padding:7px 8px;border:1px solid}
.band-lbl{font-size:9px;font-family:var(--mono);font-weight:600;letter-spacing:.06em;margin-bottom:3px}
.band-rns{font-size:18px;font-weight:600;font-family:var(--mono)}
.band-sub{font-size:9px;margin-top:2px;opacity:.7}
/* Forecast */
.fc-wrap{display:flex;align-items:flex-end;gap:3px;height:46px;margin:8px 0 4px}
.fc-bar{flex:1;border-radius:3px 3px 0 0;min-height:3px}
.fc-now{background:rgba(88,166,255,.55)}
.fc-soon{background:rgba(88,166,255,.25)}
.fc-later{background:var(--s3)}
.fc-xl{display:flex;justify-content:space-between;font-size:9px;color:var(--t3);font-family:var(--mono)}
/* Scenarios */
.sc-item{display:flex;justify-content:space-between;align-items:center;
         padding:7px 9px;background:var(--s2);border-radius:7px;font-size:12px;margin-bottom:5px}
.sc-item:last-child{margin-bottom:0}

/* Shift log */
.log-empty{padding:14px 8px;text-align:center;color:var(--t3);font-size:11px;font-family:var(--mono);line-height:1.6}
.log-row{background:var(--s2);border-radius:7px;padding:8px 10px;margin-bottom:6px;
         display:grid;grid-template-columns:auto 1fr auto;gap:9px;align-items:start;
         border-left:3px solid var(--t3)}
.log-row:last-child{margin-bottom:0}
.log-row.k-optimal{border-left-color:var(--green)}
.log-row.k-hold{border-left-color:var(--blue)}
.log-row.k-watch{border-left-color:var(--amber)}
.log-row.k-callIn{border-left-color:var(--red)}
.log-row.k-flex{border-left-color:var(--purple)}
.log-time{font-family:var(--mono);font-size:13px;font-weight:500;color:var(--t1);min-width:46px}
.log-time-rel{font-size:9px;color:var(--t3);font-family:var(--mono);margin-top:1px}
.log-mid{min-width:0}
.log-headline{font-size:12px;color:var(--t1);font-family:var(--mono);font-weight:500;line-height:1.4}
.log-sub{font-size:10px;color:var(--t2);font-family:var(--mono);margin-top:2px;line-height:1.4}
.log-key{display:inline-block;font-size:9px;font-family:var(--mono);font-weight:600;
         padding:1px 6px;border-radius:3px;letter-spacing:.05em;margin-left:4px;vertical-align:middle}
.log-key.k-optimal{background:var(--green-dim);color:var(--green)}
.log-key.k-hold{background:var(--blue-dim);color:var(--blue)}
.log-key.k-watch{background:var(--amber-dim);color:var(--amber)}
.log-key.k-callIn{background:var(--red-dim);color:var(--red)}
.log-key.k-flex{background:var(--purple-dim);color:var(--purple)}
.log-actions{display:flex;flex-direction:column;gap:3px}
.log-x{background:transparent;border:none;color:var(--t3);font-size:16px;cursor:pointer;
       padding:2px 5px;line-height:1;font-family:var(--font)}
.log-x:active{color:var(--red)}
.log-expand{background:transparent;border:none;color:var(--t3);font-size:11px;cursor:pointer;
            padding:2px 5px;font-family:var(--mono)}
.log-detail{grid-column:1/-1;margin-top:7px;padding-top:7px;border-top:1px solid var(--b1);
            font-size:11px;color:var(--t2);font-family:var(--mono);line-height:1.7;display:none}
.log-detail.open{display:block}
.log-note-input{width:100%;background:var(--s1);border:1px solid var(--b2);color:var(--t1);
                font-family:var(--font);font-size:12px;padding:6px 8px;border-radius:5px;
                margin-top:6px;outline:none;resize:none}
.log-note-input:focus{border-color:var(--blue-line)}
.log-note-saved{font-style:italic;color:var(--t2);font-family:var(--font);font-size:11px;margin-top:4px}
.log-foot{display:flex;gap:6px;margin-top:9px;padding-top:9px;border-top:1px solid var(--b1)}
.log-foot button{flex:1;background:var(--s2);border:1px solid var(--b2);color:var(--t2);
                 font-family:var(--font);font-size:11px;font-weight:500;
                 padding:7px 10px;border-radius:6px;cursor:pointer;touch-action:manipulation}
.log-foot button:active{background:var(--s3);color:var(--t1)}
.log-foot .danger:active{color:var(--red);border-color:var(--red-line)}
.toast{position:fixed;bottom:18px;left:50%;transform:translateX(-50%);
       background:var(--green);color:#0d1117;font-weight:500;font-size:13px;
       padding:9px 16px;border-radius:8px;z-index:100;
       opacity:0;pointer-events:none;transition:opacity .25s,transform .25s}
.toast.show{opacity:1;transform:translateX(-50%) translateY(-4px)}

.footer{padding:6px 16px 14px;font-size:10px;color:var(--t3);line-height:1.6;font-family:var(--mono)}
</style>
</head>
<body>

<div class="hdr">
  <div><div class="hdr-title">Bend ED — Charge Flex</div>
       <div class="hdr-sub">APE · 3:1 floor · 4:1 target · BH sitters 1:1</div></div>
  <div class="clock"><span class="dot"></span><span id="clk">—</span></div>
</div>

<div class="signal s-ok" id="sig">
  <div class="sig-icon" id="sigI">✓</div>
  <div>
    <div class="sig-tag" id="sigT">OPTIMAL</div>
    <div class="sig-msg" id="sigM">Staffing matches workload</div>
    <div class="sig-sub" id="sigS">APE:RN within target</div>
  </div>
  <div class="rec-block">
    <div class="rec-now" id="recN">—</div>
    <div class="rec-lbl">rec. assignable RNs</div>
    <div class="rec-2hr" id="rec2">—</div>
    <div class="rec-2lbl">projected in 2 hrs</div>
  </div>
</div>

<!-- Q3H logging strip -->
<div class="q3h" id="q3h">
  <div>
    <div class="q3h-tag" id="q3hTag">Q3H LOG</div>
    <div class="q3h-stat" id="q3hStat">Tap "Log now" to start tracking this shift</div>
  </div>
  <div class="q3h-cd" id="q3hCd"></div>
  <button class="q3h-btn" id="q3hBtn" onclick="logSnapshot()">📸 Log now</button>
</div>

<div class="body">

<!-- ══ LEFT ══ -->
<div>
  <!-- Patients in rooms -->
  <div class="card">
    <div class="ctitle">Patients in rooms — ESI counts</div>
    <div class="esi-grid">
      <div class="esi-cell"><div class="elbl l1">ESI 1 · 5×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('e1',-1)">−</button><input class="sval" id="e1" value="0" oninput="go()"><button class="sbtn" onclick="adj('e1',1)">+</button></div></div>
      <div class="esi-cell"><div class="elbl l2">ESI 2 · 2×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('e2',-1)">−</button><input class="sval" id="e2" value="1" oninput="go()"><button class="sbtn" onclick="adj('e2',1)">+</button></div></div>
      <div class="esi-cell"><div class="elbl l3">ESI 3 · 1.5×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('e3',-1)">−</button><input class="sval" id="e3" value="10" oninput="go()"><button class="sbtn" onclick="adj('e3',1)">+</button></div></div>
      <div class="esi-cell"><div class="elbl l4">ESI 4 · 1×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('e4',-1)">−</button><input class="sval" id="e4" value="5" oninput="go()"><button class="sbtn" onclick="adj('e4',1)">+</button></div></div>
      <div class="esi-cell"><div class="elbl l5">ESI 5 · 0.6×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('e5',-1)">−</button><input class="sval" id="e5" value="2" oninput="go()"><button class="sbtn" onclick="adj('e5',1)">+</button></div></div>
      <div class="esi-cell"><div class="elbl lb">Boarding +0.5×</div>
        <div class="stepper"><button class="sbtn" onclick="adj('bd',-1)">−</button><input class="sval" id="bd" value="3" oninput="go()"><button class="sbtn" onclick="adj('bd',1)">+</button></div></div>
    </div>
    <div style="margin-top:10px;padding-top:9px;border-top:1px solid var(--b1)">
      <div class="rn-row">
        <span style="font-size:11px;color:var(--t3);font-family:var(--mono)">RN staffing →</span>
        <span id="rnAssignableHint" style="font-family:var(--mono);font-size:12px;color:var(--t2)">— assignable</span>
      </div>
    </div>
  </div>

  <!-- RN staffing -->
  <div class="card">
    <div class="ctitle">RN staffing — total roster</div>
    <div class="rn-total-row">
      <div>
        <div class="rn-total-lbl">Total RNs on floor</div>
        <div class="rn-total-sub">includes you · everyone clocked in</div>
      </div>
      <div class="stepper"><button class="sbtn" onclick="adj('rnTotal',-1)">−</button><input class="sval" id="rnTotal" value="16" style="width:46px" oninput="go()"><button class="sbtn" onclick="adj('rnTotal',1)">+</button></div>
    </div>
    <div class="rn-roles">
      <div class="rn-role-row">
        <span class="role-lbl">Charge <span class="role-tag">me</span></span>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('rnCharge',-1)">−</button><input class="sval sval-sm" id="rnCharge" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('rnCharge',1)">+</button></div>
      </div>
      <div class="rn-role-row">
        <span class="role-lbl">Triage</span>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('rnTriage',-1)">−</button><input class="sval sval-sm" id="rnTriage" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('rnTriage',1)">+</button></div>
      </div>
      <div class="rn-role-row">
        <span class="role-lbl">Trauma</span>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('rnTrauma',-1)">−</button><input class="sval sval-sm" id="rnTrauma" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('rnTrauma',1)">+</button></div>
      </div>
      <div class="rn-role-row">
        <span class="role-lbl">Break / floater</span>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('rnBreak',-1)">−</button><input class="sval sval-sm" id="rnBreak" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('rnBreak',1)">+</button></div>
      </div>
    </div>
    <div class="rn-derived">
      <span class="rn-derived-lbl">Assignable on floor</span>
      <span class="rn-derived-num" id="rnAssignable">12</span>
    </div>
    <div class="rn-warn" id="rnWarn" style="display:none"></div>
    <div class="brk-sig brk-na" id="brkSig">—</div>
    <div class="brk-note" id="brkNote"></div>
    <div class="brk-mode">
      <span class="brk-mode-lbl">Break mode</span>
      <div class="brk-mode-toggle">
        <button class="brk-mode-btn active" id="bmStd" onclick="setBreakMode('standard')">Standard · 75m</button>
        <button class="brk-mode-btn" id="bmCmp" onclick="setBreakMode('compressed')">Compressed · 60m</button>
      </div>
    </div>
    <div class="brk-mode-suggest" id="bmSuggest" style="display:none"></div>
  </div>

  <!-- Waiting room -->
  <div class="card">
    <div class="ctitle">Waiting room</div>
    <div class="wr-grid">
      <div class="wr-cell"><div class="wlbl" style="background:rgba(248,81,73,.15);color:#ff8070">ESI 1–2 triaged</div>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('wr12',-1)">−</button><input class="sval sval-sm" id="wr12" value="0" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('wr12',1)">+</button></div></div>
      <div class="wr-cell"><div class="wlbl" style="background:rgba(227,179,65,.12);color:var(--amber)">ESI 3 triaged</div>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('wr3',-1)">−</button><input class="sval sval-sm" id="wr3" value="3" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('wr3',1)">+</button></div></div>
      <div class="wr-cell"><div class="wlbl" style="background:rgba(88,166,255,.1);color:var(--blue)">ESI 4–5 triaged</div>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('wr45',-1)">−</button><input class="sval sval-sm" id="wr45" value="5" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('wr45',1)">+</button></div></div>
      <div class="wr-cell"><div class="wlbl" style="background:rgba(255,255,255,.05);color:var(--t2)">Untriaged</div>
        <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('wru',-1)">−</button><input class="sval sval-sm" id="wru" value="2" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('wru',1)">+</button></div></div>
    </div>
    <div class="wr-proj" id="wrProj">
      <div class="wr-proj-hd">IF WAITING ROOM CLEARS</div>
      <div id="wrProjText">—</div>
    </div>
  </div>

  <!-- Forecast -->
  <div class="card">
    <div class="ctitle">Arrival forecast — next 6 hours</div>
    <div class="fc-wrap" id="fcBars"></div>
    <div class="fc-xl" id="fcLbls"></div>
    <div style="font-size:11px;color:var(--t2);margin-top:4px" id="fcStat">—</div>
  </div>
</div>

<!-- ══ RIGHT ══ -->
<div>
  <!-- RN Workload -->
  <div class="card">
    <div class="ctitle">RN workload — acuity patient equivalents</div>
    <div class="ape-val">
      <div class="ape-num" id="apeNum">—</div>
      <div class="ape-unit">APE total</div>
      <div style="margin-left:auto;font-size:12px;font-family:var(--mono);color:var(--t2)" id="apeRatio">—</div>
    </div>
    <div class="ape-track"><div class="ape-fill" id="apeFill" style="width:0%"></div></div>
    <div class="ape-zones">
      <span style="color:var(--green)">3.0 floor</span><span>4.0 target</span><span style="color:var(--red)">5.5 max</span>
    </div>
    <table class="bktable" style="margin-top:8px"><tbody id="apeBreak"></tbody></table>
    <div class="bands" id="bands"></div>
    <div style="font-size:10px;color:var(--t3);margin-top:6px;font-family:var(--mono)" id="diffDisp">—</div>
  </div>

  <!-- Support staff -->
  <div class="card">
    <div class="ctitle">Support staff</div>
    <div class="support-grid">

      <div class="sup-block">
        <div class="sup-title">ED Techs</div>
        <div class="sup-row">
          <span class="sup-lbl">On floor</span>
          <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('techs',-1)">−</button><input class="sval sval-sm" id="techs" value="2" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('techs',1)">+</button></div>
        </div>
        <div id="techNote" style="font-size:10px;color:var(--t2);margin-top:5px;font-family:var(--mono);line-height:1.5">—</div>
        <div style="font-size:10px;color:var(--t3);margin-top:4px;font-family:var(--mono)">No ratio — informational</div>
      </div>

      <div class="sup-block">
        <div class="sup-title">BH Sitters — 1:1</div>
        <div class="sup-row">
          <span class="sup-lbl">Sitter patients</span>
          <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('sitp',-1)">−</button><input class="sval sval-sm" id="sitp" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('sitp',1)">+</button></div>
        </div>
        <div class="sup-row">
          <span class="sup-lbl">Sitters on floor</span>
          <div class="stepper"><button class="sbtn sbtn-sm" onclick="adj('sits',-1)">−</button><input class="sval sval-sm" id="sits" value="1" oninput="go()"><button class="sbtn sbtn-sm" onclick="adj('sits',1)">+</button></div>
        </div>
        <div class="sit-sig" id="sitSig">—</div>
        <div style="font-size:10px;color:var(--t3);margin-top:5px;font-family:var(--mono);line-height:1.4">Sitter pts in ESI census above. Sitter handles observation; RN provides care.</div>
      </div>

    </div>
  </div>

  <!-- What if -->
  <div class="card">
    <div class="ctitle">What if…</div>
    <div id="scenarios"></div>
  </div>

  <!-- Shift log (q3h) -->
  <div class="card">
    <div class="ctitle" style="display:flex;justify-content:space-between;align-items:center">
      <span>Shift log · q3h</span>
      <span id="logCount" style="font-size:9px;color:var(--t3)"></span>
    </div>
    <div id="logList"></div>
    <div class="log-foot" id="logFoot" style="display:none">
      <button onclick="copyShiftSummary()">📋 Copy summary</button>
      <button class="danger" onclick="resetShift()">Reset shift</button>
    </div>
  </div>
</div>

</div>

<div class="footer">
  APE: ESI 1=5× · ESI 2=2× · ESI 3=1.5× · ESI 4=1× · ESI 5=0.6× · Boarder +0.5× · Sitters 1:1 required · Arrival forecast: Epic SBH actual data n=19,746 · WR projection uses median acuity-to-APE conversion
</div>

<div class="toast" id="toast">Snapshot logged</div>

<script>
const APCT=[0.4886,0.4339,0.3525,0.3415,0.2978,0.3294,0.4376,0.6211,
            0.9395,1.2726,1.4233,1.4950,1.4670,1.4537,1.4573,1.4476,
            1.3710,1.4853,1.3953,1.4646,1.3418,1.1146,0.9237,0.6454];
const ASUM=APCT.reduce((a,b)=>a+b,0);
const W={1:5,2:2,3:1.5,4:1,5:.6,b:.5};
const g=id=>document.getElementById(id);
const n=(x,d=1)=>+x.toFixed(d);
const clamp=(v,lo,hi)=>Math.max(lo,Math.min(hi,v));
const HR=['12a','1a','2a','3a','4a','5a','6a','7a','8a','9a','10a','11a',
          '12p','1p','2p','3p','4p','5p','6p','7p','8p','9p','10p','11p'];
let curHr=new Date().getHours();

// ═══ Q3H Shift logging ═══
const STORAGE_KEY='bended_charge_shift_v1';
const Q3H_MS=3*60*60*1000;
const SHIFT_MAX_MS=14*60*60*1000;

let shift=loadShift();
let expandedIdx=-1;

function loadShift(){
  try{
    const raw=localStorage.getItem(STORAGE_KEY);
    if(raw){
      const s=JSON.parse(raw);
      if(s&&typeof s==='object'&&Array.isArray(s.snapshots)) return s;
    }
  }catch(e){}
  return {startTime:null,snapshots:[]};
}

function saveShift(){
  try{localStorage.setItem(STORAGE_KEY,JSON.stringify(shift));}catch(e){}
}

function adj(id,d){const el=g(id);el.value=clamp((parseInt(el.value)||0)+d,0,99);go();}

function ape(e1,e2,e3,e4,e5,bd){return e1*W[1]+e2*W[2]+e3*W[3]+e4*W[4]+e5*W[5]+bd*W.b;}

// Break/floater coverage rule (matched to Bend ED policy):
//   Standard breaks:   45 min lunch + 2×15 min = 75 min relief per RN  →  1 break per ~8 assignable
//   Compressed breaks: 30 min lunch + 2×15 min = 60 min relief per RN  →  1 break per ~10 assignable
//   Small floor (<6 assignable): no formal break coverage requirement
function breakCoverage(assignable,breakRn,breakMode){
  if(assignable<6) return {rec:0,divisor:null,status:'na',delta:0,breakMode};
  const divisor=breakMode==='compressed'?10:8;
  const rec=Math.max(1,Math.ceil(assignable/divisor));
  if(breakRn<rec) return {rec,divisor,status:'short',delta:rec-breakRn,breakMode};
  if(breakRn>rec) return {rec,divisor,status:'flex',delta:breakRn-rec,breakMode};
  return {rec,divisor,status:'ok',delta:0,breakMode};
}

function collectInputs(){
  const rnTotal=+g('rnTotal').value||0;
  const rnCharge=+g('rnCharge').value||0;
  const rnTriage=+g('rnTriage').value||0;
  const rnTrauma=+g('rnTrauma').value||0;
  const rnBreak=+g('rnBreak').value||0;
  const rn=Math.max(1,rnTotal-rnCharge-rnTriage-rnTrauma-rnBreak);
  return {
    e1:+g('e1').value||0,e2:+g('e2').value||0,e3:+g('e3').value||0,
    e4:+g('e4').value||0,e5:+g('e5').value||0,bd:+g('bd').value||0,
    rnTotal,rnCharge,rnTriage,rnTrauma,rnBreak,rn,
    wr12:+g('wr12').value||0,wr3:+g('wr3').value||0,wr45:+g('wr45').value||0,wru:+g('wru').value||0,
    sitp:+g('sitp').value||0,sits:+g('sits').value||0,techs:+g('techs').value||0
  };
}

function metricsFor(inputs,breakMode){
  const i=inputs;
  const bm=breakMode||'standard';
  const totalPts=i.e1+i.e2+i.e3+i.e4+i.e5;
  const totalApe=ape(i.e1,i.e2,i.e3,i.e4,i.e5,i.bd);
  const apeRn=totalApe/Math.max(1,i.rn);
  const rec=Math.ceil(totalApe/4.0);
  const recMax=Math.ceil(totalApe/5.5);
  const wrTotal=i.wr12+i.wr3+i.wr45+i.wru;
  const diff=i.rn-rec;
  let key='optimal';
  if(i.rn<recMax) key='callIn';
  else if(diff>2) key='flex';
  else if(diff>0) key='hold';
  else if(diff<0) key='watch';
  const bc=breakCoverage(i.rn,i.rnBreak||0,bm);
  return {totalPts,totalApe,apeRn,rec,recMax,wrTotal,diff,key,bc,breakMode:bm};
}

function setBreakMode(mode){
  shift.breakMode=mode;
  if(!shift.startTime) shift.startTime=Date.now();
  saveShift();
  go();
}

function logSnapshot(){
  if(!shift.startTime) shift.startTime=Date.now();
  const inputs=collectInputs();
  shift.snapshots.push({t:Date.now(),inputs,breakMode:shift.breakMode||'standard',note:''});
  saveShift();
  renderQ3H();
  renderLog();
  toast('Snapshot logged · '+fmtTime(Date.now()));
  // Visual flash on the button
  const btn=g('q3hBtn');
  btn.classList.add('q3h-flash');
  setTimeout(()=>btn.classList.remove('q3h-flash'),500);
}

function removeSnapshot(idx){
  if(!confirm('Remove this snapshot?')) return;
  shift.snapshots.splice(idx,1);
  if(shift.snapshots.length===0) shift.startTime=null;
  expandedIdx=-1;
  saveShift();
  renderQ3H();
  renderLog();
}

function toggleExpand(idx){
  expandedIdx=(expandedIdx===idx)?-1:idx;
  renderLog();
}

function updateNote(idx,val){
  if(!shift.snapshots[idx]) return;
  shift.snapshots[idx].note=val;
  saveShift();
}

function resetShift(){
  const count=shift.snapshots.length;
  if(count>0&&!confirm(`Reset shift? ${count} snapshot${count!==1?'s':''} will be cleared.`)) return;
  shift={startTime:null,snapshots:[]};
  expandedIdx=-1;
  saveShift();
  renderQ3H();
  renderLog();
}

function copyShiftSummary(){
  if(shift.snapshots.length===0){toast('Nothing to copy');return;}
  const start=new Date(shift.startTime);
  const lines=[];
  lines.push('═══ Bend ED Charge Shift Log ═══');
  lines.push(`Shift started: ${fmtTime(start)} · ${start.toLocaleDateString(undefined,{weekday:'short',month:'short',day:'numeric'})}`);
  lines.push(`Snapshots: ${shift.snapshots.length}`);
  lines.push('');
  shift.snapshots.forEach(s=>{
    const m=metricsFor(s.inputs,s.breakMode);
    const i=s.inputs;
    const total=i.rnTotal||i.rn;
    const bm=s.breakMode||'standard';
    lines.push(`[${fmtTime(s.t)}] ${m.totalPts} pts · APE ${n(m.totalApe,1)} · ${n(m.apeRn,2)}:1/RN · ${i.rn} assignable (${total} roster) · WR ${m.wrTotal} · ${keyLabel(m.key)}`);
    lines.push(`   ESI 1-5: ${i.e1}/${i.e2}/${i.e3}/${i.e4}/${i.e5} + ${i.bd} board · WR: ${i.wr12}/${i.wr3}/${i.wr45}/${i.wru} · BH ${i.sits}/${i.sitp} · Tech ${i.techs}`);
    if(i.rnTotal!==undefined) lines.push(`   Roster: ${i.rnTotal} total = ${i.rnCharge||0} charge + ${i.rnTriage||0} triage + ${i.rnTrauma||0} trauma + ${i.rnBreak||0} break + ${i.rn} assignable`);
    if(m.bc&&m.bc.status!=='na'){
      const bcLabel=m.bc.status==='ok'?'adequate':m.bc.status==='short'?`${m.bc.delta} short`:`${m.bc.delta} surplus`;
      lines.push(`   Break coverage: ${i.rnBreak||0}/${m.bc.rec} ${bcLabel} · mode: ${bm} (${bm==='compressed'?'60':'75'} min)`);
    }
    if(s.note&&s.note.trim()) lines.push(`   Note: ${s.note.trim()}`);
    lines.push('');
  });
  const text=lines.join('\n');
  if(navigator.clipboard&&navigator.clipboard.writeText){
    navigator.clipboard.writeText(text).then(()=>toast('Summary copied')).catch(()=>fallbackCopy(text));
  } else fallbackCopy(text);
}

function fallbackCopy(text){
  const ta=document.createElement('textarea');
  ta.value=text;ta.style.position='fixed';ta.style.opacity='0';
  document.body.appendChild(ta);ta.select();
  try{document.execCommand('copy');toast('Summary copied');}catch(e){toast('Copy failed');}
  document.body.removeChild(ta);
}

function fmtTime(t){
  const d=(t instanceof Date)?t:new Date(t);
  const h=d.getHours(),m=d.getMinutes();
  return `${h%12||12}:${String(m).padStart(2,'0')}${h>=12?'p':'a'}`;
}

function fmtDur(ms){
  const sec=Math.max(0,Math.round(ms/1000));
  const h=Math.floor(sec/3600),m=Math.floor((sec%3600)/60);
  if(h>0) return `${h}h ${m}m`;
  return `${m}m`;
}

function fmtCountdown(ms){
  const sec=Math.max(0,Math.round(ms/1000));
  const h=Math.floor(sec/3600),m=Math.floor((sec%3600)/60);
  return `${h}:${String(m).padStart(2,'0')}`;
}

function keyLabel(k){
  return {optimal:'OPTIMAL',hold:'HOLD',watch:'WATCH',callIn:'CALL IN',flex:'FLEX OFF'}[k]||k;
}

function toast(msg){
  const t=g('toast');t.textContent=msg;t.classList.add('show');
  clearTimeout(toast._tm);toast._tm=setTimeout(()=>t.classList.remove('show'),1800);
}

function renderQ3H(){
  const strip=g('q3h');
  const stat=g('q3hStat');
  const cd=g('q3hCd');
  const tag=g('q3hTag');
  const btn=g('q3hBtn');
  strip.classList.remove('due','overdue');
  tag.textContent='Q3H LOG';

  if(!shift.startTime||shift.snapshots.length===0){
    if(shift.startTime){
      const since=Date.now()-shift.startTime;
      stat.textContent=`Shift started ${fmtDur(since)} ago · 0 snapshots`;
    } else {
      stat.textContent='Tap "Log now" to start tracking this shift';
    }
    cd.textContent='';
    btn.textContent='📸 Log now';
    return;
  }

  const last=shift.snapshots[shift.snapshots.length-1];
  const since=Date.now()-last.t;
  const due=Q3H_MS-since;
  const count=shift.snapshots.length;

  stat.innerHTML=`Last logged <span style="color:var(--t1)">${fmtTime(last.t)}</span> · ${fmtDur(since)} ago · ${count} log${count!==1?'s':''} this shift`;

  if(due<=0){
    const over=-due;
    if(over>30*60*1000){
      strip.classList.add('overdue');
      tag.textContent='OVERDUE';
      cd.textContent=`+${fmtCountdown(over)} late`;
    } else {
      strip.classList.add('due');
      tag.textContent='DUE NOW';
      cd.textContent=`+${fmtCountdown(over)} late`;
    }
  } else if(due<=30*60*1000){
    strip.classList.add('due');
    tag.textContent='DUE SOON';
    cd.textContent=`in ${fmtCountdown(due)}`;
  } else {
    cd.textContent=`next in ${fmtCountdown(due)}`;
  }
  btn.textContent='📸 Log now';

  // Auto-suggest reset if shift > 14h
  if(shift.startTime&&Date.now()-shift.startTime>SHIFT_MAX_MS){
    stat.innerHTML+=' <span style="color:var(--amber)">· stale shift — consider Reset</span>';
  }
}

function renderLog(){
  const list=g('logList');
  const foot=g('logFoot');
  const cnt=g('logCount');
  const snaps=shift.snapshots;
  cnt.textContent=snaps.length>0?`${snaps.length} snapshot${snaps.length!==1?'s':''}`:'';
  foot.style.display=snaps.length>0?'flex':'none';

  if(snaps.length===0){
    list.innerHTML='<div class="log-empty">No snapshots yet.<br>Press <strong style="color:var(--t1)">📸 Log now</strong> above to capture a q3h checkpoint.</div>';
    return;
  }

  // Newest first
  const rows=snaps.map((s,idx)=>{
    const m=metricsFor(s.inputs,s.breakMode);
    const i=s.inputs;
    const apeColor=m.apeRn<=4?'var(--green)':m.apeRn<=5.5?'var(--amber)':'var(--red)';
    const since=Date.now()-s.t;
    const isOpen=expandedIdx===idx;

    const total=i.rnTotal||i.rn;
    const rosterLine=i.rnTotal!==undefined
      ? `Roster: <span style="color:var(--t1)">${total}</span> total = ${i.rnCharge||0} charge + ${i.rnTriage||0} triage + ${i.rnTrauma||0} trauma + ${i.rnBreak||0} break → <span style="color:var(--t1)">${i.rn}</span> assignable<br>`
      : `Staffing: <span style="color:var(--t1)">${i.rn}</span> RN (legacy)<br>`;
    const bc=m.bc||{status:'na'};
    const bcColor=bc.status==='ok'?'var(--green)':bc.status==='short'?'var(--amber)':bc.status==='flex'?'var(--blue)':'var(--t3)';
    const bcText=bc.status==='ok'?`adequate (${i.rnBreak||0}/${bc.rec})`
                :bc.status==='short'?`${bc.delta} short (${i.rnBreak||0}/${bc.rec})`
                :bc.status==='flex'?`${bc.delta} surplus (${i.rnBreak||0}/${bc.rec})`
                :'n/a';
    const bm=s.breakMode||'standard';
    const bcLine=i.rnTotal!==undefined?`Break coverage: <span style="color:${bcColor}">${bcText}</span> · mode <span style="color:var(--t1)">${bm}</span> (${bm==='compressed'?'60':'75'} min)<br>`:'';
    const detail=`
      <div class="log-detail ${isOpen?'open':''}" id="det${idx}">
        ESI 1–5: <span style="color:var(--t1)">${i.e1}/${i.e2}/${i.e3}/${i.e4}/${i.e5}</span> + ${i.bd} boarding<br>
        Waiting room: <span style="color:var(--t1)">${i.wr12}</span> ESI 1–2 · <span style="color:var(--t1)">${i.wr3}</span> ESI 3 · <span style="color:var(--t1)">${i.wr45}</span> ESI 4–5 · <span style="color:var(--t1)">${i.wru}</span> untriaged<br>
        ${rosterLine}
        ${bcLine}
        Support: BH <span style="color:var(--t1)">${i.sits}/${i.sitp}</span> · Tech <span style="color:var(--t1)">${i.techs}</span><br>
        Recommended: <span style="color:${apeColor}">${m.rec} assignable RN</span> · diff <span style="color:var(--t1)">${m.diff>=0?'+':''}${m.diff}</span>
        <textarea class="log-note-input" placeholder="Add note (handoff, events, plan…)" oninput="updateNote(${idx},this.value)" rows="2">${(s.note||'').replace(/</g,'&lt;')}</textarea>
      </div>`;

    const noteHint=s.note&&s.note.trim()?`<div class="log-note-saved">📝 ${s.note.trim().replace(/</g,'&lt;').slice(0,80)}${s.note.length>80?'…':''}</div>`:'';

    return `
      <div class="log-row k-${m.key}">
        <div>
          <div class="log-time">${fmtTime(s.t)}</div>
          <div class="log-time-rel">${fmtDur(since)} ago</div>
        </div>
        <div class="log-mid">
          <div class="log-headline">${m.totalPts} pts · APE ${n(m.totalApe,1)} · <span style="color:${apeColor}">${n(m.apeRn,2)}:1</span><span class="log-key k-${m.key}">${keyLabel(m.key)}</span></div>
          <div class="log-sub">${i.rn} assignable${i.rnTotal?` / ${i.rnTotal} roster`:''} · rec ${m.rec} · WR ${m.wrTotal} · BH ${i.sits}/${i.sitp}</div>
          ${noteHint}
        </div>
        <div class="log-actions">
          <button class="log-expand" onclick="toggleExpand(${idx})" title="Details">${isOpen?'▴':'▾'}</button>
          <button class="log-x" onclick="removeSnapshot(${idx})" title="Delete">×</button>
        </div>
        ${detail}
      </div>`;
  }).reverse().join('');

  list.innerHTML=rows;
}

// ═══ Existing tool: live signal computation ═══
function go(){
  const e1=+g('e1').value||0,e2=+g('e2').value||0,e3=+g('e3').value||0;
  const e4=+g('e4').value||0,e5=+g('e5').value||0,bd=+g('bd').value||0;
  const rnTotal=+g('rnTotal').value||0;
  const rnCharge=+g('rnCharge').value||0;
  const rnTriage=+g('rnTriage').value||0;
  const rnTrauma=+g('rnTrauma').value||0;
  const rnBreak=+g('rnBreak').value||0;
  const rnNonAssign=rnCharge+rnTriage+rnTrauma+rnBreak;
  const rn=Math.max(1,rnTotal-rnNonAssign);
  // Update the staffing card derived display + warning
  g('rnAssignable').textContent=rn;
  g('rnAssignableHint').textContent=`${rn} assignable · ${rnTotal} total roster`;
  const warn=g('rnWarn');
  if(rnTotal>0&&rnNonAssign>=rnTotal){
    warn.style.display='block';
    warn.textContent=`⚠ Non-assignable roles (${rnNonAssign}) ≥ total (${rnTotal}). Increase total or reduce role counts.`;
  } else if(rnTotal===0){
    warn.style.display='block';
    warn.textContent=`Set total RN count above to begin.`;
  } else {
    warn.style.display='none';
  }
  const wr12=+g('wr12').value||0,wr3=+g('wr3').value||0,wr45=+g('wr45').value||0,wru=+g('wru').value||0;
  const sitp=+g('sitp').value||0,sits=+g('sits').value||0,techs=+g('techs').value||0;
  const totalPts=e1+e2+e3+e4+e5;
  const totalApe=ape(e1,e2,e3,e4,e5,bd);
  const apeRn=totalApe/rn;
  const rec=Math.ceil(totalApe/4.0);
  const recMax=Math.ceil(totalApe/5.5);
  const diff=rn-rec;

  // Signal
  let key='optimal';
  if(rn<recMax) key='callIn';
  else if(diff>2) key='flex';
  else if(diff>0) key='hold';
  else if(diff<0) key='watch';

  const SCFG={
    optimal:{cls:'s-ok',  icon:'✓',tag:'OPTIMAL',  msg:'Staffing matches workload'},
    hold:   {cls:'s-hold',icon:'⏸',tag:'HOLD',     msg:`${diff} RN${diff!==1?'s':''} above — hold for arrivals`},
    watch:  {cls:'s-watch',icon:'!',tag:'WATCH',   msg:`${Math.abs(diff)} RN${Math.abs(diff)!==1?'s':''} below target`},
    callIn: {cls:'s-call',icon:'⚠',tag:'CALL IN',  msg:`${rec-rn} more RN${(rec-rn)!==1?'s':''} needed now`},
    flex:   {cls:'s-flex',icon:'↓',tag:'FLEX OFF', msg:`${Math.min(diff-1,3)} RN${Math.min(diff-1,3)!==1?'s':''} can flex off`},
  };
  const cfg=SCFG[key];
  g('sig').className='signal '+cfg.cls;
  g('sigI').textContent=cfg.icon;
  g('sigT').textContent=cfg.tag;
  g('sigM').textContent=cfg.msg;
  g('sigS').textContent=`${n(apeRn,2)}:1 APE per RN · rec ${rec} assignable`;
  g('recN').textContent=rec;

  // 2hr projection
  let arr2=0;
  for(let i=1;i<=2;i++) arr2+=148*APCT[(curHr+i)%24]/ASUM;
  const nPts=Math.round(arr2*.7);
  const ape2=ape(e1,e2,e3+Math.round(nPts*.55)-Math.round(totalPts*.12),e4+Math.round(nPts*.25),e5,bd+Math.round(nPts*.27));
  const r2=Math.ceil(Math.max(ape2,totalApe*.85)/4.0);
  g('rec2').textContent=`${r2>rec?'↑':r2<rec?'↓':'→'} ${r2} in 2 hrs`;

  // Break coverage chip + mode toggle (uses apeRn computed above)
  const breakMode=shift.breakMode||'standard';
  g('bmStd').classList.toggle('active',breakMode==='standard');
  g('bmCmp').classList.toggle('active',breakMode==='compressed');
  const sugg=g('bmSuggest');
  if(breakMode==='standard'&&apeRn>4.5){
    sugg.style.display='block';
    sugg.style.color='var(--amber)';
    sugg.textContent=`⚠ APE/RN ${n(apeRn,1)} — consider compressed breaks`;
  } else if(breakMode==='compressed'&&apeRn<=3.5){
    sugg.style.display='block';
    sugg.style.color='var(--green)';
    sugg.textContent=`↓ APE/RN ${n(apeRn,1)} — load eased, can return to standard breaks`;
  } else {
    sugg.style.display='none';
  }
  const bc=breakCoverage(rn,rnBreak,breakMode);
  const bSig=g('brkSig'),bNote=g('brkNote');
  const ruleNote=breakMode==='compressed'
    ? '1 break per ~10 assignable @ 60 min relief (30+15+15)'
    : '1 break per ~8 assignable @ 75 min relief (45+15+15)';
  if(bc.status==='na'){
    bSig.className='brk-sig brk-na';
    bSig.textContent='— small floor: break coverage flexible';
    bNote.textContent='Break/floater not formally required at this assignable count.';
  } else if(bc.status==='ok'){
    bSig.className='brk-sig brk-ok';
    bSig.textContent=`✓ Break coverage adequate · ${rnBreak}/${bc.rec}`;
    bNote.textContent=ruleNote;
  } else if(bc.status==='short'){
    bSig.className='brk-sig brk-short';
    bSig.textContent=`! ${bc.delta} more break/floater needed · ${rnBreak}/${bc.rec}`;
    bNote.textContent=`Risk of missed/late breaks. ${ruleNote}.`;
  } else {
    // surplus
    bSig.className='brk-sig brk-flex';
    bSig.textContent=`↓ ${bc.delta} break/floater can flex · ${rnBreak}/${bc.rec}`;
    bNote.textContent=`Eligible for productivity flex without compromising ${breakMode==='compressed'?'compressed':'standard'} break coverage.`;
  }

  // APE meter
  const ac=apeRn<=4?'var(--green)':apeRn<=5.5?'var(--amber)':'var(--red)';
  g('apeFill').style.cssText=`width:${Math.min(apeRn/5.5*100,100)}%;background:${ac}`;
  g('apeNum').textContent=n(totalApe,1);
  g('apeRatio').textContent=`${n(apeRn,2)}:1 per RN`;
  g('apeRatio').style.color=ac;

  // Breakdown
  const rows=[['ESI 1×'+e1,e1*W[1],'#ff8070'],['ESI 2×'+e2,e2*W[2],'#ffbb55'],
    ['ESI 3×'+e3,e3*W[3],'var(--amber)'],['ESI 4×'+e4,e4*W[4],'var(--blue)'],
    ['ESI 5×'+e5,e5*W[5],'var(--green)'],['Board×'+bd,bd*W.b,'var(--purple)']].filter(r=>r[1]>0);
  g('apeBreak').innerHTML=rows.map(([l,v,c])=>`<tr><td>${l}</td><td style="color:${c}">${n(v,1)}</td></tr>`).join('')
    +`<tr style="border-top:1px solid var(--b2)"><td style="font-weight:500;color:var(--t1)">Total APE</td><td style="color:${ac};font-weight:500">${n(totalApe,1)}</td></tr>`;

  // Bands
  const bandCfg=[{r:3.0,l:'Floor',s:'min',c:'var(--green)'},{r:4.0,l:'Target',s:'opt',c:'var(--blue)'},
                 {r:5.0,l:'Stretch',s:'mon',c:'var(--amber)'},{r:5.5,l:'Max',s:'unsafe',c:'var(--red)'}];
  g('bands').innerHTML=bandCfg.map(({r,l,s,c})=>{
    const bRec=Math.ceil(totalApe/r);
    const curr=rn===bRec;
    return`<div class="band" style="background:${c}18;border-color:${c}${curr?'88':'33'};${curr?'border-width:2px':''}">
      <div class="band-lbl" style="color:${c}">${l}</div>
      <div class="band-rns" style="color:${c}">${bRec}</div>
      <div class="band-sub" style="color:${c}">${s}</div></div>`;
  }).join('');
  g('diffDisp').textContent=`${rn} assignable · ${diff===0?'at target':diff>0?'+'+diff+' vs target':diff+' vs target'}`;

  // Waiting room
  const wrTotal=wr12+wr3+wr45+wru;
  const wrApe=wr12*2.5+wr3*1.5+wr45*0.8+wru*1.2;
  const proj=g('wrProj');
  if(wrTotal===0){
    proj.style.cssText='border-left-color:var(--t3);background:var(--s2)';
    g('wrProjText').innerHTML='<span style="color:var(--t3)">Waiting room is clear</span>';
  } else {
    const needAfter=Math.ceil((totalApe+wrApe)/4.0);
    const addl=needAfter-rn;
    const urgent=wr12>0;
    const uc=urgent?'var(--red)':'var(--amber)';
    proj.style.cssText=`border-left-color:${addl>0?uc:'var(--green)'};background:${addl>0?(urgent?'var(--red-dim)':'var(--amber-dim)'):'var(--green-dim)'}`;
    let txt=`<strong style="color:var(--t1)">${wrTotal} waiting</strong> · est. APE ${n(wrApe,1)}`;
    txt+=addl>0?`<br><span style="color:${uc};font-weight:500">+${addl} RN${addl!==1?'s':''} needed when roomed</span>`
               :`<br><span style="color:var(--green)">Current staff absorbs waiting room</span>`;
    if(wr12>0) txt+=`<br><span style="color:var(--red)">⚠ ${wr12} ESI 1–2 — prioritize rooming</span>`;
    g('wrProjText').innerHTML=txt;
  }

  // BH Sitters
  const sd=sits-sitp;
  const ss=g('sitSig');
  if(sitp===0){ss.className='sit-sig sit-ok';ss.textContent='✓ No sitter patients';}
  else if(sd>=0){ss.className='sit-sig sit-ok';ss.textContent=`✓ ${sits}/${sitp} covered${sd>0?' (+'+sd+' available)':''}`;}
  else if(sd===-1){ss.className='sit-sig sit-warn';ss.textContent=`! ${sits}/${sitp} — 1 sitter needed`;}
  else{ss.className='sit-sig sit-bad';ss.textContent=`⚠ ${sits}/${sitp} — ${Math.abs(sd)} sitters needed`;}

  // Techs
  const censusAll=totalPts+wrTotal;
  g('techNote').textContent=`${techs} on floor · census ${censusAll} total`;
  g('techNote').style.color=techs===0&&censusAll>10?'var(--amber)':'var(--t2)';

  // Scenarios
  const scens=[
    {l:'+ 2 ESI-3 walk-ins',       f:()=>ape(e1,e2,e3+2,e4,e5,bd)},
    {l:'+ 1 ESI-2 ALS arrival',    f:()=>ape(e1,e2+1,e3,e4,e5,bd)},
    {l:'+ 1 BH sitter patient',    f:()=>ape(e1,e2,e3+1,e4,e5,bd)},
    {l:'− 3 discharges',           f:()=>ape(e1,e2,e3,Math.max(0,e4-2),Math.max(0,e5-1),bd)},
    {l:'+ 1 admit → boarder',      f:()=>ape(e1,e2,e3,e4,e5,bd+1)},
    {l:'Waiting room all rooms in', f:()=>ape(e1+wr12,e2,e3+wr3,e4+wr45,e5,bd)},
  ];
  g('scenarios').innerHTML=scens.map(({l,f})=>{
    const a=f(), r=Math.ceil(a/4.0), d2=r-rn;
    const ok=d2<=0;
    const col=ok?'var(--green)':d2===1?'var(--amber)':'var(--red)';
    const txt=d2===0?'still OK':d2>0?`need +${d2} RN${d2!==1?'s':''}`:`${Math.abs(d2)} surplus`;
    return`<div class="sc-item"><span style="color:var(--t2)">${l}</span><span style="font-family:var(--mono);color:${col}">${txt}</span></div>`;
  }).join('');

  // Forecast
  const fa=[...Array(6)].map((_,i)=>148*APCT[(curHr+i)%24]/ASUM);
  const fm=Math.max(...fa,1);
  g('fcBars').innerHTML=fa.map((v,i)=>`<div class="fc-bar ${i===0?'fc-now':i<=2?'fc-soon':'fc-later'}" style="height:${Math.max(4,Math.round(v/fm*100))}%" title="${HR[(curHr+i)%24]}: ${v.toFixed(1)}/hr"></div>`).join('');
  g('fcLbls').innerHTML=fa.map((_,i)=>i%2===0?`<span>${HR[(curHr+i)%24]}</span>`:'<span></span>').join('');
  const n2=fa.slice(1,3).reduce((a,b)=>a+b,0);
  const n4=fa.slice(1,5).reduce((a,b)=>a+b,0);
  g('fcStat').textContent=`~${Math.round(n2)} arrivals next 2 hrs · ~${Math.round(n4)} next 4 hrs`;
}

function updateClock(){
  const now=new Date();curHr=now.getHours();
  const h=now.getHours(),m=now.getMinutes();
  g('clk').textContent=`${h%12||12}:${String(m).padStart(2,'0')} ${h>=12?'PM':'AM'}`;
  go();
  renderQ3H();
}

// Initial render
renderLog();
updateClock();
setInterval(updateClock,30000);
// Faster cadence for the q3h countdown so it ticks visibly
setInterval(renderQ3H,15000);
</script>
</body>
</html>
