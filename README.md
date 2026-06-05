
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Melbourne Parking</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Syne:wght@700;800&display=swap" rel="stylesheet">
<style>
  :root{--bg:#0a0f0d;--card:#131d16;--border:#1c2b1f;--accent:#3dff7a;--adim:#0f2e1a;--warn:#ff6b3d;--wdim:#2e140a;--text:#ddeae0;--muted:#557060;--mono:'DM Mono',monospace;--display:'Syne',sans-serif}
  *{box-sizing:border-box;margin:0;padding:0}
  body{background:var(--bg);color:var(--text);font-family:var(--mono);min-height:100vh;-webkit-font-smoothing:antialiased}
  body::before{content:'';position:fixed;inset:0;pointer-events:none;background-image:linear-gradient(rgba(61,255,122,.025) 1px,transparent 1px),linear-gradient(90deg,rgba(61,255,122,.025) 1px,transparent 1px);background-size:36px 36px}
  .app{position:relative;z-index:1;max-width:480px;margin:0 auto;padding-bottom:60px}
  header{padding:24px 18px 18px;border-bottom:1px solid var(--border);background:linear-gradient(180deg,rgba(61,255,122,.07) 0%,transparent 100%)}
  .htop{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px}
  .logo h1{font-family:var(--display);font-size:24px;font-weight:800;letter-spacing:-.3px;line-height:1}
  .logo h1 em{color:var(--accent);font-style:normal}
  .logo p{font-size:9px;color:var(--muted);letter-spacing:.18em;text-transform:uppercase;margin-top:4px}
  .pill{display:flex;align-items:center;gap:5px;background:var(--adim);border:1px solid rgba(61,255,122,.4);border-radius:20px;padding:5px 10px;font-size:9px;color:var(--accent);letter-spacing:.12em;text-transform:uppercase}
  .dot{width:5px;height:5px;background:var(--accent);border-radius:50%;animation:pulse 2s ease-in-out infinite}
  @keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.3;transform:scale(.6)}}
  .stats{display:grid;grid-template-columns:repeat(3,1fr);gap:7px}
  .stat{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:10px 8px;text-align:center}
  .sn{font-family:var(--display);font-size:20px;font-weight:800;line-height:1}
  .g{color:var(--accent)}.r{color:var(--warn)}.w{color:var(--text)}
  .sl{font-size:8px;color:var(--muted);letter-spacing:.14em;text-transform:uppercase;margin-top:3px}
  .controls{padding:12px 18px;border-bottom:1px solid var(--border);display:flex;gap:8px;flex-direction:column}
  .sw{position:relative}
  .sw svg{position:absolute;left:11px;top:50%;transform:translateY(-50%);color:var(--muted);pointer-events:none}
  input{width:100%;background:var(--card);border:1px solid var(--border);border-radius:8px;color:var(--text);font-family:var(--mono);font-size:13px;padding:10px 10px 10px 36px;outline:none;transition:border-color .15s;-webkit-appearance:none}
  input:focus{border-color:var(--accent)}
  input::placeholder{color:var(--muted)}
  .fr{display:flex;gap:7px}
  .fb{flex:1;background:var(--card);border:1px solid var(--border);border-radius:7px;color:var(--muted);font-family:var(--mono);font-size:10px;letter-spacing:.08em;padding:8px 4px;cursor:pointer;transition:all .12s;text-transform:uppercase}
  .fb.a-all{border-color:var(--text);color:var(--text)}
  .fb.a-av{border-color:var(--accent);color:var(--accent);background:var(--adim)}
  .fb.a-fl{border-color:var(--warn);color:var(--warn);background:var(--wdim)}
  .rb{background:var(--card);border:1px solid var(--border);border-radius:7px;color:var(--muted);padding:8px 12px;cursor:pointer;transition:all .12s;display:flex;align-items:center}
  .rb.spin svg{animation:spin .7s linear infinite}
  @keyframes spin{to{transform:rotate(360deg)}}
  .upd{padding:6px 18px 0;font-size:9px;color:var(--muted);text-align:right}
  .list{padding:10px 18px;display:flex;flex-direction:column;gap:7px}
  .rc{font-size:9px;color:var(--muted);letter-spacing:.14em;text-transform:uppercase;padding:2px 0}
  .sc{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:13px;cursor:pointer;transition:border-color .12s;animation:up .2s ease both}
  .sc.open{border-color:rgba(61,255,122,.5)}
  @keyframes up{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
  .st{display:flex;align-items:center;margin-bottom:9px}
  .name{font-family:var(--display);font-size:14px;font-weight:700;flex:1;min-width:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
  .tot{font-size:9px;color:var(--muted);margin:0 8px;white-space:nowrap}
  .arr{font-size:10px;color:var(--muted);transition:transform .18s;flex-shrink:0}
  .sc.open .arr{transform:rotate(180deg)}
  .bar{height:5px;background:var(--wdim);border-radius:3px;overflow:hidden;margin-bottom:8px}
  .fill{height:100%;border-radius:3px;background:var(--accent);transition:width .5s cubic-bezier(.4,0,.2,1)}
  .ct{display:flex;gap:10px;font-size:10px}
  .cf{color:var(--accent)}.co{color:var(--warn)}
  .bg{margin-top:10px;border-top:1px solid var(--border);padding-top:10px;display:grid;grid-template-columns:repeat(auto-fill,minmax(48px,1fr));gap:5px}
  .bay{border-radius:6px;padding:5px 3px;text-align:center;font-size:9px;line-height:1.3}
  .bay.free{background:var(--adim);border:1px solid rgba(61,255,122,.25);color:var(--accent)}
  .bay.occ{background:var(--wdim);border:1px solid rgba(255,107,61,.25);color:var(--warn)}
  .bay span{display:block;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
  .bay small{font-size:8px;opacity:.6}
  .loader{display:flex;flex-direction:column;align-items:center;gap:12px;padding:48px 20px;color:var(--muted);font-size:11px}
  .dots{display:flex;gap:4px}
  .dots span{width:5px;height:5px;background:var(--accent);border-radius:50%;animation:db .9s ease-in-out infinite}
  .dots span:nth-child(2){animation-delay:.15s}.dots span:nth-child(3){animation-delay:.3s}
  @keyframes db{0%,80%,100%{transform:scale(.5);opacity:.3}40%{transform:scale(1);opacity:1}}
  .msg{padding:32px 20px;text-align:center;font-size:12px;color:var(--muted);line-height:1.6}
  .msg.err{color:var(--warn)}
  .msg .sub{font-size:10px;color:var(--muted);margin-top:8px;font-style:italic}
</style>
</head>
<body>
<div class="app">
  <header>
    <div class="htop">
      <div class="logo"><h1>MELB<em>PARK</em></h1><p>City of Melbourne · Live Sensor Data</p></div>
      <div class="pill"><div class="dot"></div>Live</div>
    </div>
    <div class="stats">
      <div class="stat"><div class="sn w" id="sT">—</div><div class="sl">Total Bays</div></div>
      <div class="stat"><div class="sn g" id="sF">—</div><div class="sl">Available</div></div>
      <div class="stat"><div class="sn r" id="sO">—</div><div class="sl">Occupied</div></div>
    </div>
  </header>
  <div class="controls">
    <div class="sw">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
      <input type="text" id="srch" placeholder="Search street name…" oninput="render()">
    </div>
    <div class="fr">
      <button class="fb a-all" id="f-all" onclick="setF('all')">All</button>
      <button class="fb" id="f-av" onclick="setF('av')">Available</button>
      <button class="fb" id="f-fl" onclick="setF('fl')">Full</button>
      <button class="rb" id="rbtn" onclick="load()">
        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
          <path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8"/><path d="M21 3v5h-5"/>
          <path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16"/><path d="M8 16H3v5"/>
        </svg>
      </button>
    </div>
  </div>
  <div id="upd" class="upd"></div>
  <div id="content"></div>
</div>
<script>
let streets={},filter='all',expanded=null;

async function load(){
  document.getElementById('rbtn').classList.add('spin');
  document.getElementById('content').innerHTML='<div class="loader"><div class="dots"><span></span><span></span><span></span></div><span>Fetching live bay data…</span></div>';
  try{
    let all=[],offset=0;
    while(true){
      const r=await fetch(`https://data.melbourne.vic.gov.au/api/explore/v2.1/catalog/datasets/on-street-parking-bay-sensors/records?limit=100&offset=${offset}`);
      if(!r.ok) throw new Error(`HTTP ${r.status}`);
      const j=await r.json();
      const rows=j.results||[];
      all=all.concat(rows);
      if(rows.length<100) break;
      offset+=100;
      if(offset>=3000) break;
    }
    if(!all.length) throw new Error('No data returned from API');
    process(all);
    document.getElementById('upd').textContent='Updated '+new Date().toLocaleTimeString('en-AU',{hour:'2-digit',minute:'2-digit',second:'2-digit'});
  }catch(e){
    document.getElementById('content').innerHTML=`<div class="msg err">⚠ Could not load parking data<div class="sub">${e.message}</div></div>`;
  }
  document.getElementById('rbtn').classList.remove('spin');
}

function process(rows){
  streets={};
  for(const r of rows){
    const street=String(r.street_marker||r.st_marker_id||'UNKNOWN').trim().toUpperCase();
    if(!streets[street]) streets[street]={free:0,occupied:0,bays:[]};
    const occ=String(r.status||'').toLowerCase()==='present';
    occ?streets[street].occupied++:streets[street].free++;
    streets[street].bays.push({id:String(r.bay_id||'?'),occ});
  }
  const total=rows.length;
  const free=rows.filter(r=>String(r.status||'').toLowerCase()!=='present').length;
  document.getElementById('sT').textContent=total.toLocaleString();
  document.getElementById('sF').textContent=free.toLocaleString();
  document.getElementById('sO').textContent=(total-free).toLocaleString();
  render();
}

function setF(f){
  filter=f;
  document.getElementById('f-all').className='fb'+(f==='all'?' a-all':'');
  document.getElementById('f-av').className='fb'+(f==='av'?' a-av':'');
  document.getElementById('f-fl').className='fb'+(f==='fl'?' a-fl':'');
  render();
}

function render(){
  const q=document.getElementById('srch').value.toLowerCase().trim();
  const el=document.getElementById('content');
  if(!Object.keys(streets).length) return;
  let e=Object.entries(streets);
  if(q) e=e.filter(([n])=>n.toLowerCase().includes(q));
  if(filter==='av') e=e.filter(([,s])=>s.free>0);
  if(filter==='fl') e=e.filter(([,s])=>s.free===0);
  e.sort((a,b)=>b[1].free-a[1].free);
  if(!e.length){el.innerHTML='<div class="msg">No streets match.</div>';return;}
  const cards=e.map(([name,d],i)=>{
    const total=d.free+d.occupied;
    const pct=total>0?Math.round(d.free/total*100):0;
    const isOpen=expanded===name;
    const disp=name.length>36?name.slice(0,35)+'…':name;
    const bays=isOpen?`<div class="bg">${d.bays.map(b=>`<div class="bay ${b.occ?'occ':'free'}"><span>${b.id}</span><small>${b.occ?'occ':'free'}</small></div>`).join('')}</div>`:'';
    return `<div class="sc${isOpen?' open':''}" style="animation-delay:${Math.min(i*.025,.4)}s" onclick="tog('${name.replace(/'/g,"\\'")}')">
      <div class="st"><span class="name">${disp}</span><span class="tot">${total} bays</span><span class="arr">▾</span></div>
      <div class="bar"><div class="fill" style="width:${pct}%"></div></div>
      <div class="ct"><span class="cf">▪ ${d.free} free</span><span class="co">▪ ${d.occupied} occupied</span></div>
      ${bays}</div>`;
  }).join('');
  el.innerHTML=`<div class="list"><div class="rc">${e.length} street${e.length!==1?'s':''}</div>${cards}</div>`;
}

function tog(name){expanded=expanded===name?null:name;render();}
load();
</script>
</body>
</html>
