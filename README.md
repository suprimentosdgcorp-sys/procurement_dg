<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1">
<title>Suprimentos — Drogaria Globo</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
:root{
  --red:#b91c1c;--red-l:#fef2f2;--red-b:rgba(185,28,28,.15);
  --blue:#1e40af;--blue-l:#eff6ff;--blue-b:rgba(30,64,175,.15);
  --grn:#166534;--grn-l:#f0fdf4;--grn-b:rgba(22,101,52,.15);
  --amb:#92400e;--amb-l:#fffbeb;--amb-b:rgba(146,64,14,.15);
  --c50:#f8fafc;--c100:#f1f5f9;--c200:#e2e8f0;--c300:#cbd5e1;
  --c400:#94a3b8;--c500:#64748b;--c600:#475569;--c700:#334155;--c900:#0f172a;
  --wh:#fff;--bd:#e2e8f0;--tx:#0f172a;--tx2:#475569;--tx3:#94a3b8;
  --ff:'Segoe UI',system-ui,-apple-system,sans-serif;--fm:'SF Mono','Consolas',monospace;
  --r:6px;--r2:10px;--sh:0 1px 2px rgba(0,0,0,.06),0 1px 3px rgba(0,0,0,.08);
  --nh:52px;--fh:44px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html{font-size:14px;}
body{background:var(--c100);color:var(--tx);font-family:var(--ff);overflow-x:hidden;-webkit-font-smoothing:antialiased;}
/* NAV */
.nav{position:fixed;top:0;left:0;right:0;z-index:500;height:var(--nh);background:var(--wh);border-bottom:1px solid var(--bd);display:flex;align-items:center;padding:0 12px;box-shadow:var(--sh);}
.brand{display:flex;align-items:center;gap:8px;flex-shrink:0;padding-right:10px;}
.bmark{width:28px;height:28px;background:var(--red);border-radius:5px;display:flex;align-items:center;justify-content:center;font-weight:800;color:var(--wh);font-size:11px;}
.bname{font-size:12px;font-weight:700;color:var(--c900);line-height:1.15;}
.bsub{font-size:9.5px;color:var(--tx3);}
@media(max-width:599px){.bsub{display:none;}}
.tabs{display:flex;align-items:center;gap:1px;flex:1;overflow-x:auto;padding:0 4px;}
.tabs::-webkit-scrollbar{display:none;}
.tab{height:30px;padding:0 10px;border:none;border-radius:5px;cursor:pointer;background:transparent;color:var(--tx3);font-family:var(--ff);font-size:12px;font-weight:500;white-space:nowrap;transition:all .12s;flex-shrink:0;}
.tab:hover{background:var(--c100);color:var(--tx2);}
.tab.on{background:var(--blue-l);color:var(--blue);font-weight:600;}
.nav-r{display:flex;align-items:center;gap:6px;flex-shrink:0;margin-left:4px;}
.ts{font-size:10px;color:var(--tx3);}
@media(max-width:599px){.ts{display:none;}}
.btn-upd{height:28px;padding:0 10px;background:var(--blue);color:var(--wh);border:none;border-radius:5px;font-size:12px;font-weight:500;cursor:pointer;font-family:var(--ff);}
.btn-upd:disabled{opacity:.4;}
/* FILTER BAR */
.fbar{position:fixed;top:var(--nh);left:0;right:0;z-index:499;height:var(--fh);background:var(--wh);border-bottom:1px solid var(--bd);display:flex;align-items:center;padding:0 10px;gap:5px;overflow-x:auto;-webkit-overflow-scrolling:touch;}
.fbar::-webkit-scrollbar{display:none;}
.fi{height:28px;padding:0 8px;background:var(--wh);border:1px solid var(--bd);border-radius:5px;color:var(--tx2);font-family:var(--ff);font-size:12px;outline:none;flex-shrink:0;max-width:140px;}
.fi:focus{border-color:var(--blue);}
select.fi{cursor:pointer;}
input.fi{color:var(--tx);min-width:150px;}
input.fi::placeholder{color:var(--tx3);}
.fi-x{height:28px;padding:0 8px;background:transparent;border:1px solid var(--bd);border-radius:5px;color:var(--tx3);font-size:12px;cursor:pointer;flex-shrink:0;}
.fi-x:hover{color:var(--red);border-color:var(--red);}
.fcnt{font-size:11px;color:var(--tx3);white-space:nowrap;flex-shrink:0;padding-left:2px;}
/* BODY */
.pg{padding-top:calc(var(--nh)+var(--fh));min-height:100vh;}
.main{padding:12px;max-width:1600px;margin:0 auto;}
.view{display:none;}.view.on{display:block;animation:fi .14s ease;}
@keyframes fi{from{opacity:0;transform:translateY(3px)}to{opacity:1;transform:none}}
/* SECTION TITLE */
.stit{font-size:10px;font-weight:700;color:var(--tx3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:10px;display:flex;align-items:center;gap:8px;}
.stit::after{content:'';flex:1;height:1px;background:var(--bd);}
/* KPI STRIP */
.krow{display:grid;gap:8px;margin-bottom:12px;}
.k2{grid-template-columns:1fr 1fr;}.k3{grid-template-columns:1fr 1fr;}.k4{grid-template-columns:1fr 1fr;}.k5{grid-template-columns:1fr 1fr;}
@media(min-width:480px){.k3{grid-template-columns:repeat(3,1fr);}.k5{grid-template-columns:repeat(3,1fr);}}
@media(min-width:640px){.k4{grid-template-columns:repeat(4,1fr);}.k5{grid-template-columns:repeat(5,1fr);}}
@media(min-width:1024px){.krow{display:flex;gap:0;background:var(--bd);border:1px solid var(--bd);border-radius:var(--r2);overflow:hidden;box-shadow:var(--sh);}.k2,.k3,.k4,.k5{grid-template-columns:unset;}}
.kpi{background:var(--wh);padding:11px 14px;position:relative;overflow:hidden;border-radius:var(--r);border:1px solid var(--bd);}
@media(min-width:1024px){.kpi{flex:1;border:none;border-radius:0;}}
.kpi::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;}
.kpi.kr::before{background:var(--red);}.kpi.kb::before{background:var(--blue);}.kpi.kg::before{background:var(--grn);}.kpi.ka::before{background:var(--amb);}.kpi.kn::before{background:var(--c300);}
.klb{font-size:9.5px;font-weight:600;color:var(--tx3);text-transform:uppercase;letter-spacing:.05em;margin-bottom:3px;line-height:1.2;}
.kv{font-size:17px;font-weight:700;font-family:var(--fm);line-height:1;color:var(--c900);}
@media(min-width:1024px){.kv{font-size:19px;}}
.ks{font-size:9.5px;color:var(--tx3);margin-top:2px;line-height:1.3;}
.kpi.kr .kv{color:var(--red);}.kpi.kb .kv{color:var(--blue);}.kpi.kg .kv{color:var(--grn);}.kpi.ka .kv{color:var(--amb);}
/* SAVING HERO CARD */
.sav-hero{background:linear-gradient(135deg,var(--grn) 0%,#14532d 100%);border-radius:var(--r2);padding:20px 24px;color:#fff;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;box-shadow:var(--sh);}
.sav-hero-main .lbl{font-size:10.5px;font-weight:600;text-transform:uppercase;letter-spacing:.08em;opacity:.8;margin-bottom:4px;}
.sav-hero-main .val{font-size:32px;font-weight:800;font-family:var(--fm);line-height:1;}
.sav-hero-main .sub{font-size:12px;opacity:.75;margin-top:3px;}
.sav-hero-stats{display:flex;gap:20px;flex-wrap:wrap;}
.sav-stat{text-align:center;}
.sav-stat .sv{font-size:20px;font-weight:700;font-family:var(--fm);line-height:1;}
.sav-stat .sl{font-size:10px;opacity:.75;margin-top:2px;text-transform:uppercase;letter-spacing:.05em;}
/* ALERTS */
.alrows{display:flex;flex-direction:column;gap:5px;margin-bottom:12px;}
@media(min-width:640px){.alrows{flex-direction:row;flex-wrap:wrap;}}
.al{display:flex;align-items:flex-start;gap:6px;padding:6px 10px;font-size:12px;font-weight:500;border-radius:var(--r);border-left:3px solid;line-height:1.45;}
.al.ar{background:var(--red-l);border-color:var(--red);color:var(--red);}
.al.aa{background:var(--amb-l);border-color:var(--amb);color:var(--amb);}
.al.ag{background:var(--grn-l);border-color:var(--grn);color:var(--grn);}
.al.ab{background:var(--blue-l);border-color:var(--blue);color:var(--blue);}
.adot{width:6px;height:6px;border-radius:50%;background:currentColor;flex-shrink:0;margin-top:3px;}
.adot.bl{animation:blink 1.2s infinite;}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.1}}
/* INSIGHT STRIP */
.insights{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;}
.ins{background:var(--wh);border:1px solid var(--bd);border-radius:var(--r);padding:8px 12px;font-size:11.5px;color:var(--tx2);display:flex;align-items:center;gap:6px;line-height:1.4;box-shadow:var(--sh);}
.ins-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
/* GRID */
.grid{display:grid;gap:10px;margin-bottom:10px;}
.g1{grid-template-columns:1fr;}.g2{grid-template-columns:1fr;}.g3{grid-template-columns:1fr;}
@media(min-width:640px){.g2{grid-template-columns:1fr 1fr;}}
@media(min-width:768px){.g3{grid-template-columns:1fr 1fr 1fr;}}
@media(min-width:1024px){.g12{grid-template-columns:1fr 2fr;}.g21{grid-template-columns:2fr 1fr;}.g13{grid-template-columns:1fr 3fr;}}
/* PANEL */
.card{background:var(--wh);border:1px solid var(--bd);border-radius:var(--r2);box-shadow:var(--sh);overflow:hidden;}
.ch{padding:10px 12px 0;display:flex;align-items:center;justify-content:space-between;}
.ct{font-size:10.5px;font-weight:700;color:var(--tx2);text-transform:uppercase;letter-spacing:.04em;}
.cb{padding:10px 12px 12px;}.cb0{padding:0;}
/* CHARTS */
.cv{position:relative;}
.h130{height:130px;}.h160{height:160px;}.h185{height:185px;}.h210{height:210px;}.h250{height:250px;}.h280{height:280px;}
/* TABLES */
.tw{overflow:auto;-webkit-overflow-scrolling:touch;}
.mh200{max-height:200px;}.mh280{max-height:280px;}.mh360{max-height:360px;}.mh440{max-height:440px;}.mh520{max-height:520px;}
table{width:100%;border-collapse:collapse;font-size:11.5px;}
thead{position:sticky;top:0;z-index:4;}
th{background:var(--c50);color:var(--tx3);font-size:9.5px;font-weight:700;text-transform:uppercase;letter-spacing:.05em;padding:6px 10px;text-align:left;border-bottom:1px solid var(--c200);white-space:nowrap;}
td{padding:5px 10px;border-bottom:1px solid var(--c100);color:var(--tx);vertical-align:middle;}
tr:hover td{background:var(--blue-l);}
tr:last-child td{border-bottom:none;}
.mn{font-family:var(--fm);font-size:11px;}.tdr{text-align:right;}.te{max-width:180px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
/* TAGS */
.tag{display:inline-flex;align-items:center;padding:1px 5px;border-radius:3px;font-size:10px;font-weight:600;white-space:nowrap;line-height:1.5;}
.tg{background:var(--grn-l);color:var(--grn);}.tb{background:var(--blue-l);color:var(--blue);}
.tr2{background:var(--red-l);color:var(--red);}.ta{background:var(--amb-l);color:var(--amb);}.tn{background:var(--c100);color:var(--tx3);}
.abca{font-size:10px;font-weight:700;padding:1px 4px;border-radius:2px;background:var(--grn-l);color:var(--grn);}
.abcb{font-size:10px;font-weight:700;padding:1px 4px;border-radius:2px;background:var(--amb-l);color:var(--amb);}
.abcc{font-size:10px;font-weight:700;padding:1px 4px;border-radius:2px;background:var(--c100);color:var(--tx3);}
/* AGING */
.aok{color:var(--grn);font-family:var(--fm);font-size:11px;}.awa{color:var(--amb);font-family:var(--fm);font-size:11px;}.acr{color:var(--red);font-family:var(--fm);font-size:11px;}
/* STAT ROW */
.srow{display:flex;align-items:center;padding:4px 0;border-bottom:1px solid var(--c100);}
.srow:last-child{border-bottom:none;}
.slb{font-size:11.5px;color:var(--tx2);flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;padding-right:6px;}
.sbar{width:50px;height:3px;background:var(--c200);border-radius:2px;margin:0 5px;flex-shrink:0;}
.sfil{height:100%;border-radius:2px;}
.sval{font-family:var(--fm);font-size:11.5px;flex-shrink:0;}
/* MINI BAR */
.mb{display:flex;align-items:center;gap:4px;}.mbt{width:46px;height:3px;background:var(--c200);border-radius:2px;flex-shrink:0;}.mbf{height:100%;border-radius:2px;}
/* PROGRESS BAR (demanda status) */
.pbar-wrap{margin-bottom:8px;}
.pbar-label{display:flex;justify-content:space-between;font-size:11px;color:var(--tx2);margin-bottom:3px;}
.pbar-track{height:6px;background:var(--c200);border-radius:3px;overflow:hidden;}
.pbar-fill{height:100%;border-radius:3px;transition:width .4s ease;}
/* LOCAL FILTERS */
.lf{display:flex;align-items:center;gap:5px;padding:7px 12px;border-bottom:1px solid var(--c100);flex-wrap:wrap;}
.lf-cnt{font-size:10px;color:var(--tx3);white-space:nowrap;margin-left:auto;}
/* FOOTNOTE */
.fn{font-size:9.5px;color:var(--tx3);padding:4px 12px 8px;line-height:1.5;}
/* ABC LEGEND */
.abc-legend{display:flex;gap:12px;padding:6px 12px;border-top:1px solid var(--c100);flex-wrap:wrap;}
.abc-legend-item{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--tx2);}
.abc-dot{width:10px;height:10px;border-radius:2px;}
/* LOAD/ERROR */
.load{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:55vh;gap:12px;}
.spin{width:26px;height:26px;border:2px solid var(--c200);border-top-color:var(--blue);border-radius:50%;animation:sp .8s linear infinite;}
@keyframes sp{to{transform:rotate(360deg);}}
.ltx{color:var(--tx3);font-size:13px;}
.errw{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:55vh;gap:10px;padding:20px;text-align:center;}
.errt{font-size:14px;font-weight:700;color:var(--red);}.errm{color:var(--tx3);font-size:12px;max-width:400px;line-height:1.6;}
@media(max-width:479px){.main{padding:8px;}.kv{font-size:15px;}}
</style>
</head>
<body>
<nav class="nav">
  <div class="brand">
    <div class="bmark">DG</div>
    <div><div class="bname">Drogaria Globo</div><div class="bsub">Suprimentos</div></div>
  </div>
  <div class="tabs">
    <button class="tab on"  onclick="ir('exec',this)">Executivo</button>
    <button class="tab"     onclick="ir('garg',this)">Gargalos</button>
    <button class="tab"     onclick="ir('dem',this)">Demanda SC</button>
    <button class="tab"     onclick="ir('ocs',this)">OCs</button>
    <button class="tab"     onclick="ir('perf',this)">Performance</button>
    <button class="tab"     onclick="ir('fin',this)">Financeiro</button>
    <button class="tab"     onclick="ir('sav',this)">Saving</button>
    <button class="tab"     onclick="ir('cham',this)">Chamados MAN</button>
  </div>
  <div class="nav-r">
    <span class="ts" id="bTs"></span>
    <button class="btn-upd" id="btnR" onclick="init()">↺</button>
  </div>
</nav>
<div class="fbar" id="fbar"></div>
<div class="pg"><div class="main">

<!-- ══ EXECUTIVO ══ -->
<div class="view on" id="view-exec">
  <div class="stit">Visão Executiva</div>
  <div class="krow k4" id="kE"></div>
  <div class="alrows" id="aE"></div>
  <div class="grid g2" style="margin-bottom:10px">
    <div class="card"><div class="ch"><span class="ct">OCs por Status — Qtd e Valor</span></div><div class="cb"><div class="cv h185"><canvas id="cESt"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Distribuição por Comprador</span></div><div class="cb"><div class="cv h185"><canvas id="cECp"></canvas></div></div></div>
  </div>
  <div class="grid g3">
    <div class="card"><div class="ch"><span class="ct">Top 5 Fornecedores</span></div><div class="cb"><div class="cv h160"><canvas id="cEF5"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Status Gerencial</span></div><div class="cb" id="eStL" style="padding-top:6px"></div></div>
    <div class="card"><div class="ch"><span class="ct">Saving por Comprador</span></div><div class="cb" id="eSavL" style="padding-top:4px"></div></div>
  </div>
</div>

<!-- ══ GARGALOS ══ -->
<div class="view" id="view-garg">
  <div class="stit">Gargalos Operacionais</div>
  <div class="krow k4" id="kG"></div>
  <div class="alrows" id="aGarg"></div>
  <div class="grid g2">
    <div class="card">
      <div class="ch"><span class="ct">Pendente de Aprovação</span></div>
      <div class="fn">Valor Original · Dias corridos desde emissão</div>
      <div class="cb0"><div class="tw mh280"><table id="tNF"></table></div></div>
    </div>
    <div class="card">
      <div class="ch"><span class="ct">Backlog SC por Comprador</span></div>
      <div class="cb"><div class="cv h210"><canvas id="cGComp"></canvas></div></div>
    </div>
  </div>
  <div class="grid g2">
    <div class="card">
      <div class="ch"><span class="ct">Backlog SC por Centro de Custo</span></div>
      <div class="cb"><div class="cv h185"><canvas id="cGBf"></canvas></div></div>
    </div>
    <div class="card">
      <div class="ch"><span class="ct">Chamados sem SC — Encaminhados / Aguardando</span></div>
      <div class="cb0"><div class="tw mh220"><table id="tGcs"></table></div></div>
    </div>
  </div>
  <div class="card" style="margin-top:0">
    <div class="ch"><span class="ct">SC Serviços Não Cotadas — Aging</span></div>
    <div class="lf">
      <input class="fi" id="sBk" placeholder="Serviço ou CC..." oninput="rBkTbl()">
      <select class="fi" id="fBkAg" onchange="rBkTbl()">
        <option value="">Todos agings</option><option value="ok">Verde ≤3d</option>
        <option value="warn">Amarelo 4-15d</option><option value="crit">Vermelho +15d</option>
      </select>
      <span class="lf-cnt" id="cntBk"></span>
    </div>
    <div class="cb0"><div class="tw mh360"><table id="tBk"></table></div></div>
  </div>
</div>

<!-- ══ DEMANDA SC ══ -->
<div class="view" id="view-dem">
  <div class="stit">Demanda — Solicitações de Compra</div>
  <div class="krow k5" id="kD"></div>
  <div class="grid g3" style="margin-bottom:10px">
    <div class="card">
      <div class="ch"><span class="ct">Status das SCs</span></div>
      <div class="cb" id="dStatusBars" style="padding-top:8px"></div>
    </div>
    <div class="card"><div class="ch"><span class="ct">SC por Regional</span></div><div class="cb"><div class="cv h185"><canvas id="cDreg"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Tipo de Demanda</span></div><div class="cb"><div class="cv h185"><canvas id="cDtipo"></canvas></div></div></div>
  </div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Demanda por Setor Solicitante</span></div><div class="cb"><div class="cv h185"><canvas id="cDsetor"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Top Serviços / Produtos Solicitados</span></div><div class="cb"><div class="cv h185"><canvas id="cDitem"></canvas></div></div></div>
  </div>
  <div class="card">
    <div class="ch"><span class="ct">SCs — Detalhe</span></div>
    <div class="lf">
      <input class="fi" id="sDem" placeholder="Nº SC, descrição, CC..." oninput="rDemTbl()">
      <select class="fi" id="fDemTp" onchange="rDemTbl()"><option value="">Tipo</option><option value="Serviço">Serviço</option><option value="Produto">Produto</option></select>
      <select class="fi" id="fDemSit" onchange="rDemTbl()"><option value="">Status</option><option value="Não Cotada">Não Cotada</option><option value="Gerou O.C.">Gerou O.C.</option></select>
      <select class="fi" id="fDemReg" onchange="rDemTbl()"><option value="">Regional</option></select>
      <span class="lf-cnt" id="cntDem"></span>
    </div>
    <div class="cb0"><div class="tw mh440"><table id="tDem"></table></div></div>
  </div>
</div>

<!-- ══ OCs ══ -->
<div class="view" id="view-ocs">
  <div class="stit">Ordens de Compra — Indicadores e Detalhe</div>
  <div class="krow k4" id="kOC"></div>
  <div class="insights" id="insOC"></div>
  <div class="grid g3" style="margin-bottom:10px">
    <div class="card" style="grid-column:span 1"><div class="ch"><span class="ct">Análise por Comprador</span></div><div class="cb0"><div class="tw mh280"><table id="tOCcomp"></table></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Valor por Situação</span></div><div class="cb"><div class="cv h210"><canvas id="cOCsit"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Top 10 Fornecedores</span></div><div class="cb"><div class="cv h210"><canvas id="cOCforn"></canvas></div></div></div>
  </div>
  <div class="card">
    <div class="ch"><span class="ct">OCs — Detalhe</span></div>
    <div class="lf">
      <input class="fi" id="sOC" placeholder="FILIAL-OC, fornecedor..." oninput="rOCTbl()">
      <select class="fi" id="fOCSit" onchange="rOCTbl()"><option value="">Status</option><option value="Liquidado">Liquidado</option><option value="Aberto Total">Aberto Total</option><option value="Não Fechado">Não Fechado</option><option value="Cancelado">Cancelado</option></select>
      <select class="fi" id="fOCCp" onchange="rOCTbl()"><option value="">Comprador</option></select>
      <select class="fi" id="fOCReg" onchange="rOCTbl()"><option value="">Regional</option></select>
      <select class="fi" id="fOCTp" onchange="rOCTbl()"><option value="">Tipo</option><option value="Serviço">Serviço</option><option value="Produto">Produto</option><option value="Contrato">Contrato</option></select>
      <span class="lf-cnt" id="cntOC"></span>
    </div>
    <div class="cb0"><div class="tw mh520"><table id="tOC"></table></div></div>
  </div>
</div>

<!-- ══ PERFORMANCE ══ -->
<div class="view" id="view-perf">
  <div class="stit">Performance — Compradores</div>
  <div class="krow k4" id="kP"></div>
  <div class="grid g2">
    <div class="card">
      <div class="ch">
        <span class="ct">Ranking de Compradores</span>
        <select class="fi" id="fPSt" style="height:24px;font-size:10px" onchange="rPComp()">
          <option value="">Todos</option><option value="Suprimentos">Suprimentos</option><option value="Administrativo">Administrativo</option>
        </select>
      </div>
      <div class="cb0"><div class="tw mh440"><table id="tPcomp"></table></div></div>
      <div class="fn">Volume = valor total OCs · Saving Rate = SAVING ÷ Vlr. Inicial · Irreg. = OCs Não Fechado</div>
    </div>
    <div class="card">
      <div class="ch"><span class="ct">Volume por Comprador</span></div>
      <div class="cb"><div class="cv h210"><canvas id="cPvol"></canvas></div></div>
    </div>
  </div>
  <div class="grid g3">
    <div class="card"><div class="ch"><span class="ct">Saving por Comprador</span></div><div class="cb"><div class="cv h185"><canvas id="cPsav"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Saving Rate % (meta: 8%)</span></div><div class="cb"><div class="cv h185"><canvas id="cPrate"></canvas></div></div></div>
    <div class="card">
      <div class="ch">
        <span class="ct">Fornecedores — Curva ABC</span>
        <select class="fi" id="fPFabc" style="height:24px;font-size:10px" onchange="rPForn()">
          <option value="">Todos</option><option value="A">A</option><option value="B">B</option><option value="C">C</option>
        </select>
      </div>
      <div class="cb0"><div class="tw mh220"><table id="tPforn"></table></div></div>
    </div>
  </div>
</div>

<!-- ══ FINANCEIRO ══ -->
<div class="view" id="view-fin">
  <div class="stit">Controle Financeiro</div>
  <div class="krow k4" id="kFin"></div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Valor por Situação</span></div><div class="cb"><div class="cv h185"><canvas id="cFinB"></canvas></div></div></div>
    <div class="card">
      <div class="ch"><span class="ct">Curva ABC — Fornecedores por Concentração de Gasto</span></div>
      <div class="cb"><div class="cv h185"><canvas id="cFinAbc"></canvas></div></div>
      <div class="abc-legend">
        <div class="abc-legend-item"><div class="abc-dot" style="background:var(--grn)"></div>Classe A — 0 a 80% do gasto (poucos fornecedores, maior impacto)</div>
        <div class="abc-legend-item"><div class="abc-dot" style="background:var(--amb)"></div>Classe B — 80 a 95%</div>
        <div class="abc-legend-item"><div class="abc-dot" style="background:var(--c400)"></div>Classe C — 95 a 100% (muitos fornecedores, menor impacto)</div>
      </div>
    </div>
  </div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Top 15 Fornecedores — Curva ABC</span></div><div class="cb"><div class="cv h210"><canvas id="cFinForn"></canvas></div></div></div>
    <div class="card">
      <div class="ch"><span class="ct">Pendente de Aprovação — Detalhe</span></div>
      <div class="fn">"Comprometido" = Aberto Total (aprovadas, reservado). "Pendente" = Não Fechado (em aprovação). Ambos: Valor Original.</div>
      <div class="cb0"><div class="tw mh280"><table id="tFinNf"></table></div></div>
    </div>
  </div>
</div>

<!-- ══ SAVING ══ -->
<div class="view" id="view-sav">
  <div class="stit">Saving — Performance de Negociação</div>
  <div id="savHero"></div>
  <div class="grid g2">
    <div class="card">
      <div class="ch"><span class="ct">Por Comprador — Valor e Rate %</span></div>
      <div class="cb"><div class="cv h185"><canvas id="cSavC"></canvas></div></div>
      <div class="fn">Rate % = SAVING ÷ Valor Inicial × 100</div>
    </div>
    <div class="card"><div class="ch"><span class="ct">Por Setor Solicitante</span></div><div class="cb"><div class="cv h185"><canvas id="cSavS"></canvas></div></div></div>
  </div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Modo de Contratação</span></div><div class="cb"><div class="cv h150"><canvas id="cSavM"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Rate % por Comprador</span></div><div class="cb"><div class="cv h150"><canvas id="cSavR"></canvas></div></div></div>
  </div>
  <div class="card">
    <div class="ch"><span class="ct">Registros de Saving</span></div>
    <div class="lf">
      <input class="fi" id="sSav" placeholder="Descrição ou fornecedor..." oninput="rSavTbl()">
      <select class="fi" id="fSavC" onchange="rSavTbl()"><option value="">Comprador</option></select>
      <select class="fi" id="fSavM" onchange="rSavTbl()"><option value="">Modo</option><option value="CONTRATO">Contrato</option><option value="OC">OC Avulsa</option></select>
      <select class="fi" id="fSavSt" onchange="rSavTbl()"><option value="">Setor</option><option value="Suprimentos">Suprimentos</option><option value="Administrativo">Administrativo</option></select>
      <span class="lf-cnt" id="cntSav"></span>
    </div>
    <div class="cb0"><div class="tw mh380"><table id="tSav"></table></div></div>
  </div>
</div>

<!-- ══ CHAMADOS MAN ══ -->
<div class="view" id="view-cham">
  <div class="stit">Chamados MAN — Gestão Operacional e Recorrência</div>
  <div class="krow k4" id="kCh"></div>
  <div class="alrows" id="aCh"></div>
  <div class="grid g3">
    <div class="card"><div class="ch"><span class="ct">Por Status</span></div><div class="cb"><div class="cv h160"><canvas id="cChSt"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Aging dos Abertos</span></div><div class="cb"><div class="cv h160"><canvas id="cChAg"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Por Prioridade</span></div><div class="cb"><div class="cv h160"><canvas id="cChPr"></canvas></div></div></div>
  </div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Abertos por Mês</span></div><div class="cb"><div class="cv h185"><canvas id="cChMes"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Top Motivos</span></div><div class="cb"><div class="cv h185"><canvas id="cChMo"></canvas></div></div></div>
  </div>
  <!-- Recorrência incorporada -->
  <div class="stit" style="margin-top:4px">Recorrência e Reincidência</div>
  <div class="krow k2" id="kRec"></div>
  <div class="grid g2">
    <div class="card"><div class="ch"><span class="ct">Por UF (sem N/D)</span></div><div class="cb"><div class="cv h185"><canvas id="cRuf"></canvas></div></div></div>
    <div class="card"><div class="ch"><span class="ct">Top Reincidências — Loja × Motivo</span></div><div class="cb"><div class="cv h185"><canvas id="cRec"></canvas></div></div></div>
  </div>
  <div class="card" style="margin-bottom:10px">
    <div class="ch"><span class="ct">Ranking de Reincidência</span></div>
    <div class="cb0"><div class="tw mh280"><table id="tRec"></table></div></div>
    <div class="fn">≥2 mesma Loja+Motivo = Monitorar · ≥3 = Atenção · ≥5 = Crítico</div>
  </div>
  <!-- Tabela de chamados -->
  <div class="card">
    <div class="ch"><span class="ct">Chamados — Detalhe</span></div>
    <div class="lf">
      <input class="fi" id="sCh" placeholder="Protocolo, local ou motivo..." oninput="rChTbl()">
      <select class="fi" id="fChSt" onchange="rChTbl()"><option value="">Status</option></select>
      <select class="fi" id="fChPr" onchange="rChTbl()"><option value="">Prioridade</option></select>
      <select class="fi" id="fChTp" onchange="rChTbl()"><option value="">Tipo</option><option value="Corretivo">Corretivo</option><option value="Preventivo">Preventivo</option></select>
      <select class="fi" id="fChSC" onchange="rChTbl()"><option value="">Com/Sem SC</option><option value="sim">Com SC</option><option value="nao">Sem SC</option></select>
      <span class="lf-cnt" id="cntCh"></span>
    </div>
    <div class="cb0"><div class="tw mh440"><table id="tCh"></table></div></div>
  </div>
</div>

</div></div>
<script>
var SCRIPT_URL='COLE_SUA_URL_AQUI';
var D=null,CH={};
function fN(v){return Math.round(Number(v)||0).toLocaleString('pt-BR');}
function fR(v){return'R$\u00a0'+Math.round(Number(v)||0).toLocaleString('pt-BR');}
function fRd(v){return'R$\u00a0'+(Number(v)||0).toLocaleString('pt-BR',{minimumFractionDigits:2,maximumFractionDigits:2});}
function pct(a,b){return b?((a/b)*100).toFixed(1)+'%':'—';}
function sN(n){var p=(n||'').split(' ').filter(Boolean);return p.length?p[0]+(p.length>1?' '+p[p.length-1][0]+'.':''):n||'—';}
function $(id){return document.getElementById(id);}
function sh(id,h){var e=$(id);if(e)e.innerHTML=h;}
function tagSit(s){var m={'Liquidado':'tg','Aberto Total':'tb','Não Fechado':'ta','Cancelado':'tn','Não Cotada':'tr2','Gerou O.C.':'tg','CONTRATO':'tb','OC':'tn','Contrato':'tb','Serviço':'tb','Produto':'tg','Misto':'ta','Atendida':'tg'};return'<span class="tag '+(m[s]||'tn')+'">'+s+'</span>';}
function agH(d){if(d===null||d===undefined)return'<span class="aok">—</span>';return d<=3?'<span class="aok">'+fN(d)+'d</span>':d<=15?'<span class="awa">'+fN(d)+'d</span>':'<span class="acr">'+fN(d)+'d</span>';}
function prTag(p){var m={'Crítica':'tr2','Urgente':'tr2','Alta':'ta','Média':'tb','Normal':'tb','Baixa':'tg'};return'<span class="tag '+(m[p]||'tn')+'">'+p+'</span>';}
function kH(c,l,v,s){return'<div class="kpi '+c+'"><div class="klb">'+l+'</div><div class="kv">'+v+'</div><div class="ks">'+(s||'')+'</div></div>';}
Chart.defaults.color='#94a3b8';Chart.defaults.font.family="'Segoe UI',system-ui,sans-serif";Chart.defaults.font.size=11;
var GC='rgba(0,0,0,.05)';
var C={r:'#b91c1c',b:'#1e40af',g:'#166534',a:'#92400e',r2:'rgba(185,28,28,.6)',b2:'rgba(30,64,175,.6)',g2:'rgba(22,101,52,.6)',a2:'rgba(146,64,14,.6)',pal:['#1e40af','#b91c1c','#166534','#92400e','#6d28d9','#0e7490','#c2410c','#475569','#0f766e','#be185d']};
function mk(id,cfg){var el=$(id);if(!el)return null;if(CH[id]){CH[id].destroy();delete CH[id];}try{CH[id]=new Chart(el,cfg);}catch(e){}return CH[id]||null;}
var CUR='exec';
function ir(id,btn){CUR=id;document.querySelectorAll('.view').forEach(function(v){v.classList.remove('on');});document.querySelectorAll('.tab').forEach(function(b){b.classList.remove('on');});var v=$('view-'+id);if(v)v.classList.add('on');if(btn)btn.classList.add('on');showFbar(id);}
// ══ FILTER BAR POR ABA ══
var FBARS={
  exec:[{t:'sel',id:'gAno',ph:'Ano',src:'anos'},{t:'sel',id:'gMes',ph:'Mês',src:'meses'},{t:'sel',id:'gComp',ph:'Comprador',src:'comps'},{t:'sel',id:'gSetor',ph:'Setor',opts:['Suprimentos','Administrativo']},{t:'sel',id:'gReg',ph:'Regional',src:'regs'}],
  garg:[],
  dem:[{t:'sel',id:'gAno',ph:'Ano',src:'anos'},{t:'sel',id:'gMes',ph:'Mês',src:'meses'},{t:'sel',id:'gReg',ph:'Regional',src:'regs'}],
  ocs:[{t:'sel',id:'gAno',ph:'Ano',src:'anos'},{t:'sel',id:'gMes',ph:'Mês',src:'meses'},{t:'sel',id:'gComp',ph:'Comprador',src:'comps'},{t:'sel',id:'gSetor',ph:'Setor',opts:['Suprimentos','Administrativo']},{t:'sel',id:'gReg',ph:'Regional',src:'regs'},{t:'inp',id:'gTxt',ph:'Buscar...'}],
  perf:[{t:'sel',id:'gAno',ph:'Ano',src:'anos'},{t:'sel',id:'gMes',ph:'Mês',src:'meses'}],
  fin:[{t:'sel',id:'gAno',ph:'Ano',src:'anos'},{t:'sel',id:'gMes',ph:'Mês',src:'meses'},{t:'sel',id:'gReg',ph:'Regional',src:'regs'},{t:'sel',id:'gSit',ph:'Situação',opts:['Liquidado','Aberto Total','Não Fechado','Cancelado']}],
  sav:[{t:'sel',id:'gAno',ph:'Ano',src:'anos_sav'},{t:'sel',id:'gMes',ph:'Mês',src:'meses_sav'},{t:'sel',id:'gComp',ph:'Comprador',src:'comps_sav'},{t:'sel',id:'gSetor',ph:'Setor',opts:['Suprimentos','Administrativo']}],
  cham:[{t:'sel',id:'gAno',ph:'Ano',src:'anos_ch'},{t:'sel',id:'gUF',ph:'UF',src:'ufs'}],
};
var META={};
function showFbar(view){
  var fb=$('fbar');if(!fb)return;
  var defs=FBARS[view]||[];
  if(!defs.length){fb.innerHTML='<span style="font-size:11px;color:var(--tx3)">Filtros locais em cada seção</span>';return;}
  var html='';
  defs.forEach(function(d){
    if(d.t==='inp'){html+='<input class="fi" id="'+d.id+'" placeholder="'+d.ph+'" oninput="gApply()" style="min-width:150px">';}
    else{var arr=d.src?(META[d.src]||[]):(d.opts||[]);html+='<select class="fi" id="'+d.id+'" onchange="gApply()"><option value="">'+d.ph+'</option>'+arr.map(function(v){return'<option value="'+v+'">'+v+'</option>';}).join('')+'</select>';}
  });
  html+='<button class="fi-x" onclick="gClear()">✕</button><span class="fcnt" id="fcnt"></span>';
  fb.innerHTML=html;gApply();
}
function gGet(){var ids=['gAno','gMes','gComp','gSetor','gReg','gSit','gUF','gTxt'];var f={};ids.forEach(function(id){var e=$(id);if(e)f[id]=(e.value||'').trim();});return f;}
function gApply(){if(D)renderAll();}
function gClear(){['gAno','gMes','gComp','gSetor','gReg','gSit','gUF','gTxt'].forEach(function(id){var e=$(id);if(e)e.value='';});if(D)renderAll();}
function fOCs(){var f=gGet();return(D.ocs||[]).filter(function(o){return(!f.gAno||o.ano===f.gAno)&&(!f.gMes||o.mes===f.gMes)&&(!f.gComp||o.comprador.toLowerCase().startsWith(f.gComp.toLowerCase().split(' ')[0]))&&(!f.gSetor||o.setor===f.gSetor)&&(!f.gReg||o.regional===f.gReg)&&(!f.gSit||o.situacao===f.gSit)&&(!f.gTxt||(o.filialOC+' '+o.fornecedorNome+' '+o.comprador).toLowerCase().includes(f.gTxt.toLowerCase()));});}
function fSav(){var f=gGet();return(D.saving||[]).filter(function(s){return(!f.gAno||s.ano===f.gAno)&&(!f.gMes||s.mes===f.gMes)&&(!f.gSetor||s.setor===f.gSetor)&&(!f.gComp||s.comprador.toLowerCase().startsWith(f.gComp.toLowerCase().split(' ')[0]));});}
function fCham(){var f=gGet();return(D.chamados||[]).filter(function(c){return(!f.gAno||c.ano===f.gAno)&&(!f.gUF||c.uf===f.gUF);});}
function fDem(){var f=gGet();var all=[].concat((D.scServ||[]).map(function(s){return Object.assign({},s,{tipoSC:'Serviço'});}),(D.scProd||[]).map(function(s){return Object.assign({},s,{tipoSC:'Produto'});}));return all.filter(function(s){return(!f.gAno||s.ano===f.gAno)&&(!f.gMes||s.mes===f.gMes)&&(!f.gReg||s.regional===f.gReg);});}
// ══ INIT ══
function isGAS(){
  try{return typeof google!=='undefined'&&typeof google.script!=='undefined'&&typeof google.script.run!=='undefined';}
  catch(e){return false;}
}
function init(){
  var btn=$('btnR');if(btn){btn.disabled=true;btn.textContent='...';}
  var ve=$('view-exec');
  if(ve)ve.innerHTML='<div class="load"><div class="spin"></div><div class="ltx">Carregando dados...</div></div>';
  document.querySelectorAll('.view').forEach(function(v){v.classList.remove('on');});
  if(ve)ve.classList.add('on');
  function onOk(data){
    if(!data.ok){if(ve)ve.innerHTML='<div class="errw"><div class="errt">Erro</div><div class="errm">'+data.error+'</div></div>';if(btn){btn.disabled=false;btn.textContent='↺';}return;}
    D=data;restoreExec();buildMeta();showFbar(CUR);renderAll();
    sh('bTs',D.ts?new Date(D.ts).toLocaleString('pt-BR'):'');
    if(btn){btn.disabled=false;btn.textContent='↺';}
  }
  function onErr(msg){
    var diag='GAS detectado: '+isGAS()+' | URL: '+(typeof window!=='undefined'?window.location.href.substring(0,60):'?');
    if(ve)ve.innerHTML='<div class="errw"><div class="errt">Falha na conexão</div><div class="errm">'+msg+'</div><div style="font-size:10px;color:#94a3b8;margin-top:8px">'+diag+'</div></div>';
    if(btn){btn.disabled=false;btn.textContent='↺';}}
  // Dentro do Apps Script: usa google.script.run (sem CORS, sem fetch)
  if(isGAS()){
    google.script.run
      .withSuccessHandler(function(json){
        try{onOk(JSON.parse(json));}
        catch(ex){onErr('Erro ao interpretar dados: '+ex.message);}
      })
      .withFailureHandler(function(ex){onErr(ex.message||'Erro no servidor');})
      .getDadosJSON();
    return;
  }
  // Fora do Apps Script: requer SCRIPT_URL configurada
  if(!SCRIPT_URL||SCRIPT_URL==='COLE_SUA_URL_AQUI'){
    onErr('Configure SCRIPT_URL no início do script com a URL do Web App.');
    return;
  }
  fetch(SCRIPT_URL+'?action=dados&t='+Date.now())
    .then(function(r){if(!r.ok)throw new Error('HTTP '+r.status);return r.json();})
    .then(onOk)
    .catch(function(e){onErr('Erro de rede: '+e.message);});
}
function buildMeta(){
  var ocs=D.ocs||[];var ch=D.chamados||[];var sv=D.saving||[];
  META.anos=[...new Set(ocs.map(function(o){return o.ano;}).filter(Boolean))].sort().reverse();
  META.meses=[...new Set(ocs.map(function(o){return o.mes;}).filter(Boolean))].sort().reverse();
  META.comps=[...new Set(ocs.map(function(o){return o.comprador;}).filter(Boolean))].sort().map(sN);
  META.regs=[...new Set(ocs.map(function(o){return o.regional;}).filter(Boolean).filter(function(v){return v&&v!=='N/D';}))].sort();
  META.ufs=[...new Set(ch.map(function(c){return c.uf;}).filter(Boolean).filter(function(v){return v&&v!=='N/D';}))].sort();
  META.anos_ch=[...new Set(ch.map(function(c){return c.ano;}).filter(Boolean))].sort().reverse();
  META.anos_sav=[...new Set(sv.map(function(s){return s.ano;}).filter(Boolean))].sort().reverse();
  META.meses_sav=[...new Set(sv.map(function(s){return s.mes;}).filter(Boolean))].sort().reverse();
  META.comps_sav=[...new Set(sv.map(function(s){return s.comprador;}).filter(Boolean))].sort();
  // OC local filters
  var allComps=[...new Set(ocs.map(function(o){return o.comprador;}).filter(Boolean))].sort();
  var fOCCp=$('fOCCp');if(fOCCp)fOCCp.innerHTML='<option value="">Comprador</option>'+allComps.map(function(c){return'<option value="'+c+'">'+sN(c)+'</option>';}).join('');
  var allRegs=[...new Set(ocs.map(function(o){return o.regional;}).filter(Boolean).filter(function(v){return v&&v!=='N/D';}))].sort();
  var fOCReg=$('fOCReg');if(fOCReg)fOCReg.innerHTML='<option value="">Regional</option>'+allRegs.map(function(r){return'<option value="'+r+'">'+r+'</option>';}).join('');
  // Saving local
  var scs=[...new Set(sv.map(function(s){return s.comprador;}).filter(Boolean))].sort();
  var fSC=$('fSavC');if(fSC)fSC.innerHTML='<option value="">Comprador</option>'+scs.map(function(c){return'<option value="'+c+'">'+c+'</option>';}).join('');
  // Chamados local
  var chSts=[...new Set(ch.map(function(c){return c.status;}).filter(Boolean))].sort();
  var chPrs=[...new Set(ch.map(function(c){return c.prioridade;}).filter(Boolean))].sort();
  var fCSt=$('fChSt');if(fCSt)fCSt.innerHTML='<option value="">Status</option>'+chSts.map(function(s){return'<option value="'+s+'">'+s+'</option>';}).join('');
  var fCPr=$('fChPr');if(fCPr)fCPr.innerHTML='<option value="">Prioridade</option>'+chPrs.map(function(p){return'<option value="'+p+'">'+p+'</option>';}).join('');
  // Demanda regional
  var demRegs=[...new Set([].concat((D.scServ||[]).map(function(s){return s.regional;}),(D.scProd||[]).map(function(s){return s.regional;})).filter(function(v){return v&&v!=='N/D';}))].sort();
  var fDR=$('fDemReg');if(fDR)fDR.innerHTML='<option value="">Regional</option>'+demRegs.map(function(r){return'<option value="'+r+'">'+r+'</option>';}).join('');
}
function restoreExec(){
  sh('view-exec',
    '<div class="stit">Visão Executiva</div>'+
    '<div class="krow k4" id="kE"></div><div class="alrows" id="aE"></div>'+
    '<div class="grid g2" style="margin-bottom:10px">'+
      '<div class="card"><div class="ch"><span class="ct">OCs por Status</span></div><div class="cb"><div class="cv h185"><canvas id="cESt"></canvas></div></div></div>'+
      '<div class="card"><div class="ch"><span class="ct">Distribuição por Comprador</span></div><div class="cb"><div class="cv h185"><canvas id="cECp"></canvas></div></div></div>'+
    '</div>'+
    '<div class="grid g3">'+
      '<div class="card"><div class="ch"><span class="ct">Top 5 Fornecedores</span></div><div class="cb"><div class="cv h160"><canvas id="cEF5"></canvas></div></div></div>'+
      '<div class="card"><div class="ch"><span class="ct">Status Gerencial</span></div><div class="cb" id="eStL" style="padding-top:6px"></div></div>'+
      '<div class="card"><div class="ch"><span class="ct">Saving por Comprador</span></div><div class="cb" id="eSavL" style="padding-top:4px"></div></div>'+
    '</div>'
  );
}
function renderAll(){if(!D)return;rExec();rGarg();rDem();rOCs();rPerf();rFin();rSav();rCham();rChTbl();rSavTbl();}
// ══ EXECUTIVO ══
function rExec(){
  var ind=D.ind;var ocs=fOCs();
  var tv=ocs.reduce(function(s,o){return s+o.vlrOrig;},0);
  var tl=ocs.filter(function(o){return o.situacao==='Liquidado';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var ta=ocs.filter(function(o){return o.situacao==='Aberto Total';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var nNF=ocs.filter(function(o){return o.situacao==='Não Fechado';}).length;
  var vNF=ocs.filter(function(o){return o.situacao==='Não Fechado';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var txL=tv?Math.round(tl/tv*1000)/10:0;
  sh('kE',kH('kb','OCs',fN(ocs.length),[...new Set(ocs.map(function(o){return o.filial;}))].length+' filiais')+kH('kb','Valor Total',fR(tv),'')+kH('kg','Liquidado',fR(tl),txL+'%')+kH('ka','Comprometido',fR(ta),'Aberto Total')+kH('kr','Backlog Serv.',fN(ind.bkServCount),'sem cotação')+kH('ka','Pend. Aprovação',fN(nNF),fR(vNF))+kH('kg','Saving',fR(ind.totalSaving),ind.savingRate+'%')+kH('kr','Cham. Críticos',fN(ind.chamCrit),''));
  sh('fcnt',fN(ocs.length)+' OCs · '+fR(tv));
  var alts=[];
  var tc=ind.compradores&&ind.compradores[0];
  if(tc&&tv&&tc.valor/tv>0.5)alts.push({c:'ar',b:true,t:'⚡ '+sN(tc.nome)+': '+pct(tc.valor,tv)+' do valor total — concentração crítica'});
  if(ind.bkServCount>20)alts.push({c:'ar',b:true,t:fN(ind.bkServCount)+' SC de serviços sem cotação'});
  if(nNF>0)alts.push({c:'aa',b:false,t:fN(nNF)+' OCs pendentes de aprovação — '+fR(vNF)});
  if(ind.chamCrit>0)alts.push({c:'ar',b:true,t:fN(ind.chamCrit)+' chamados críticos/urgentes abertos'});
  if(ind.savingRate>=8)alts.push({c:'ag',b:false,t:'Saving rate '+ind.savingRate+'% — acima do benchmark 8%'});
  else if(ind.totalVI>0)alts.push({c:'aa',b:false,t:'Saving rate '+ind.savingRate+'% — abaixo do benchmark 8%'});
  sh('aE',alts.map(function(a){return'<div class="al '+a.c+'"><div class="adot'+(a.b?' bl':'')+'"></div>'+a.t+'</div>';}).join(''));
  var SC={'Liquidado':C.g,'Aberto Total':C.b,'Não Fechado':C.a,'Cancelado':'#94a3b8'};
  var sits=Object.keys(ind.porSituacao);
  mk('cESt',{type:'bar',data:{labels:sits,datasets:[{label:'Qtd',data:sits.map(function(k){return ind.porSituacao[k]||0;}),backgroundColor:sits.map(function(k){return SC[k]||'#94a3b8';}),borderRadius:3,yAxisID:'y'},{label:'Valor',data:sits.map(function(k){return ind.porSituacaoValor[k]||0;}),backgroundColor:sits.map(function(k){return(SC[k]||'#94a3b8')+'44';}),borderColor:sits.map(function(k){return SC[k]||'#94a3b8';}),borderWidth:1,borderRadius:3,yAxisID:'y2'}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC},title:{display:true,text:'Qtd'}},y2:{position:'right',grid:{display:false},ticks:{callback:function(v){return fR(v);}}}}}});
  var cE=(ind.compradores||[]).slice(0,6);
  mk('cECp',{type:'doughnut',data:{labels:cE.map(function(c){return sN(c.nome);}),datasets:[{data:cE.map(function(c){return c.valor;}),backgroundColor:C.pal,borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'52%',plugins:{legend:{position:'right',labels:{font:{size:10},padding:6}}}}});
  var f5=(ind.fornecedores||[]).slice(0,5);
  mk('cEF5',{type:'bar',data:{labels:f5.map(function(f){var n=f.nome||'';return n.length>22?n.slice(0,20)+'..':n;}),datasets:[{data:f5.map(function(f){return f.valor;}),backgroundColor:C.b2,borderColor:C.b,borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},y:{grid:{display:false}}}}});
  var tot=ocs.length||1;
  sh('eStL',sits.map(function(k){var v=ind.porSituacao[k]||0;return'<div class="srow"><span class="slb">'+tagSit(k)+'</span><div class="sbar"><div class="sfil" style="width:'+Math.round(v/tot*100)+'%;background:'+(SC[k]||'#94a3b8')+'"></div></div><span class="sval">'+fN(v)+'</span></div>';}).join(''));
  var sl=ind.savCompArr||[];var mx=sl.length?sl[0].saving:1;
  sh('eSavL',sl.map(function(s){return'<div class="srow"><span class="slb">'+s.nome+'</span><div class="sbar" style="width:46px"><div class="sfil" style="width:'+Math.round(s.saving/mx*100)+'%;background:'+C.g+'"></div></div><span class="sval" style="color:'+C.g+'">'+fR(s.saving)+'</span><span style="color:var(--tx3);font-size:9.5px;margin-left:3px">'+s.rate+'%</span></div>';}).join(''));
}
// ══ GARGALOS ══
function rGarg(){
  var ind=D.ind;
  sh('kG',kH('kr','Backlog Serv.',fN(ind.bkServCount),'SC sem cotação')+kH('ka','Aging Máx. SC',fN(ind.agMaxServ)+'d','')+kH('ka','Pend. Aprovação',fN(ind.nfCount),fR(ind.totalNF))+kH('kr','Cham. s/SC',fN(ind.chamSemSC),'aguard. orçamento'));
  var insights=[];
  var bkPorComp={};
  (D.scServ||[]).filter(function(s){return s.situacao==='Não Cotada';}).forEach(function(s){var k=s.solicitante||'N/D';bkPorComp[k]=(bkPorComp[k]||0)+1;});
  var topComp=Object.keys(bkPorComp).sort(function(a,b){return bkPorComp[b]-bkPorComp[a];}).slice(0,1)[0];
  if(topComp)insights.push({c:C.r,t:'Comprador com maior backlog: '+sN(topComp)+' ('+bkPorComp[topComp]+' SCs sem cotação)'});
  if(ind.agMaxServ>15)insights.push({c:C.r,t:'SC mais antiga há '+fN(ind.agMaxServ)+' dias sem cotação — risco de desabastecimento'});
  if(ind.nfCount>0)insights.push({c:C.a,t:fN(ind.nfCount)+' OCs aguardando aprovação — '+fR(ind.totalNF)+' comprometidos'});
  if(ind.chamSemSC>5)insights.push({c:C.a,t:fN(ind.chamSemSC)+' chamados abertos sem SC — demanda não capturada'});
  sh('aGarg',insights.map(function(i){return'<div class="al '+(i.c===C.r?'ar':'aa')+'"><div class="adot"></div>'+i.t+'</div>';}).join(''));
  var nf=ind.naoFechado||[];
  sh('tNF','<thead><tr><th>FILIAL-OC</th><th>Tipo</th><th>Comprador</th><th>Fornecedor</th><th class="tdr">Vlr. Original</th><th>Dias</th></tr></thead><tbody>'+nf.map(function(o){return'<tr><td class="mn" style="color:var(--amb)">'+o.filialOC+'</td><td>'+tagSit(o.tipo||'—')+'</td><td>'+sN(o.comprador)+'</td><td class="te">'+o.fornecedorNome+'</td><td class="mn tdr">'+fR(o.vlrOrig)+'</td><td>'+agH(o.diasAberto)+'</td></tr>';}).join('')+'</tbody>');
  // Backlog por comprador
  var bkC=Object.keys(bkPorComp).map(function(k){return{n:k,v:bkPorComp[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,8);
  mk('cGComp',{type:'bar',data:{labels:bkC.map(function(x){return sN(x.n);}),datasets:[{label:'SC não cotadas',data:bkC.map(function(x){return x.v;}),backgroundColor:C.r2,borderColor:C.r,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC}},x:{grid:{display:false}}}}});
  var bf=ind.bkPorCC||{};var ba=Object.keys(bf).filter(function(k){return k&&k!=='N/D';}).map(function(k){return{n:k,v:bf[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,10);
  mk('cGBf',{type:'bar',data:{labels:ba.map(function(x){return x.n.length>20?x.n.slice(0,18)+'..':x.n;}),datasets:[{data:ba.map(function(x){return x.v;}),backgroundColor:C.a2,borderColor:C.a,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC}},x:{grid:{display:false},ticks:{font:{size:9},maxRotation:30}}}}});
  var cg=ind.chamGarg||[];
  if(!cg.length){sh('tGcs','<tbody><tr><td colspan="6" style="text-align:center;color:var(--tx3);padding:14px;font-size:11px">✓ Nenhum chamado crítico sem SC</td></tr></tbody>');}
  else{sh('tGcs','<thead><tr><th>Protocolo</th><th>Local</th><th>UF</th><th>Motivo</th><th>Prioridade</th><th>Aging</th></tr></thead><tbody>'+cg.map(function(c){return'<tr><td class="mn" style="color:var(--red)">'+c.protocolo+'</td><td class="te">'+c.local+'</td><td>'+c.uf+'</td><td class="te">'+c.motivo+'</td><td>'+prTag(c.prioridade)+'</td><td>'+agH(c.aging)+'</td></tr>';}).join('')+'</tbody>');}
  rBkTbl();
}
function rBkTbl(){
  var sc=D.scServ||[];var bk=sc.filter(function(s){return s.situacao==='Não Cotada';});
  var q=(($('sBk')||{}).value||'').toLowerCase();var ag=(($('fBkAg')||{}).value||'');
  var rows=bk.filter(function(s){var a=s.aging||0;return(!ag||(ag==='ok'&&a<=3)||(ag==='warn'&&a>3&&a<=15)||(ag==='crit'&&a>15))&&(!q||(s.descricao||'').toLowerCase().includes(q)||(s.ccNome||'').toLowerCase().includes(q));}).sort(function(a,b){return(b.aging||0)-(a.aging||0);});
  sh('cntBk',fN(rows.length)+' SC');
  sh('tBk','<thead><tr><th>Solicitação</th><th>Regional</th><th>Centro de Custo</th><th>Descrição</th><th>Comprador</th><th>Data</th><th>Aging</th></tr></thead><tbody>'+rows.map(function(s){return'<tr><td class="mn">'+s.solicitacao+'</td><td>'+s.regional+'</td><td class="te">'+s.ccNome+'</td><td class="te" title="'+s.descricao+'">'+s.descricao+'</td><td>'+sN(s.solicitante)+'</td><td class="mn">'+s.data+'</td><td>'+agH(s.aging)+'</td></tr>';}).join('')+'</tbody>');
}
// ══ DEMANDA SC ══
function rDem(){
  var all=fDem();var serv=all.filter(function(s){return s.tipoSC==='Serviço';});var prod=all.filter(function(s){return s.tipoSC==='Produto';});
  var nc=all.filter(function(s){return s.situacao==='Não Cotada';}).length;
  var gc=all.filter(function(s){return s.situacao==='Gerou O.C.'||s.situacao==='Atendida';}).length;
  var tx=all.length?Math.round(gc/all.length*1000)/10:0;
  sh('kD',kH('kb','Total SC',fN(all.length),fN(serv.length)+' serv · '+fN(prod.length)+' prod')+kH('kg','Atendidas',fN(gc),tx+'% de conversão')+kH('kr','Não Cotadas',fN(nc),pct(nc,all.length))+kH('ka','Em Cotação',fN(all.filter(function(s){return s.situacao&&s.situacao.includes('Cotaç');}).length),'')+kH('kn','Itens SC',fN(all.length),'total de itens'));
  sh('fcnt',fN(all.length)+' SCs');
  // Status bars
  var statuses=['Não Cotada','Gerou O.C.','Atendida','Cancelada'];var statC={'Não Cotada':C.r,'Gerou O.C.':C.g,'Atendida':C.g,'Cancelada':'#94a3b8'};
  var html='';statuses.forEach(function(st){var n=all.filter(function(s){return s.situacao===st;}).length;if(n>0){var pctV=all.length?Math.round(n/all.length*100):0;html+='<div class="pbar-wrap"><div class="pbar-label"><span>'+tagSit(st)+'</span><span class="mn">'+fN(n)+' ('+pctV+'%)</span></div><div class="pbar-track"><div class="pbar-fill" style="width:'+pctV+'%;background:'+(statC[st]||'#94a3b8')+'"></div></div></div>';}});
  sh('dStatusBars',html);
  // SC por regional
  var regMap={};all.forEach(function(s){if(s.regional&&s.regional!=='N/D'){if(!regMap[s.regional])regMap[s.regional]={serv:0,prod:0};regMap[s.regional][s.tipoSC==='Serviço'?'serv':'prod']++;}});
  var regs=Object.keys(regMap);
  mk('cDreg',{type:'bar',data:{labels:regs,datasets:[{label:'Serviços',data:regs.map(function(r){return regMap[r].serv;}),backgroundColor:C.b2,borderColor:C.b,borderWidth:1,borderRadius:3},{label:'Produtos',data:regs.map(function(r){return regMap[r].prod;}),backgroundColor:C.g2,borderColor:C.g,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC}},x:{grid:{display:false}}}}});
  mk('cDtipo',{type:'doughnut',data:{labels:['Serviços','Produtos'],datasets:[{data:[serv.length,prod.length],backgroundColor:[C.b2,C.g2],borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'50%',plugins:{legend:{position:'right'}}}});
  // Por setor solicitante
  var setorMap={};all.forEach(function(s){var k=s.ccNome||s.cc||'N/D';if(k&&k!=='N/D')setorMap[k]=(setorMap[k]||0)+1;});
  var sa=Object.keys(setorMap).map(function(k){return{k:k,v:setorMap[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,8);
  mk('cDsetor',{type:'bar',data:{labels:sa.map(function(x){return x.k.length>20?x.k.slice(0,18)+'..':x.k;}),datasets:[{data:sa.map(function(x){return x.v;}),backgroundColor:C.a2,borderColor:C.a,borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC}},y:{grid:{display:false},ticks:{font:{size:9}}}}}});
  // Top itens
  var itemMap={};all.forEach(function(s){var k=s.descricao||s.servico||s.produto||'N/D';if(k&&k!=='N/D'&&k.length>2)itemMap[k]=(itemMap[k]||0)+1;});
  var ia=Object.keys(itemMap).map(function(k){return{k:k,v:itemMap[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,8);
  mk('cDitem',{type:'bar',data:{labels:ia.map(function(x){return x.k.length>26?x.k.slice(0,24)+'..':x.k;}),datasets:[{data:ia.map(function(x){return x.v;}),backgroundColor:C.b2,borderColor:C.b,borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC}},y:{grid:{display:false},ticks:{font:{size:9}}}}}});
  rDemTbl();
}
function rDemTbl(){
  var all=fDem();
  var q=(($('sDem')||{}).value||'').toLowerCase();var tp=(($('fDemTp')||{}).value||'');var sit=(($('fDemSit')||{}).value||'');var reg=(($('fDemReg')||{}).value||'');
  var rows=all.filter(function(s){return(!q||(s.solicitacao||'').includes(q)||(s.descricao||'').toLowerCase().includes(q)||(s.ccNome||'').toLowerCase().includes(q))&&(!tp||s.tipoSC===tp)&&(!sit||s.situacao===sit)&&(!reg||s.regional===reg);}).sort(function(a,b){return(b.aging||0)-(a.aging||0);});
  sh('cntDem',fN(rows.length)+' SCs');
  sh('tDem','<thead><tr><th>Nº SC</th><th>Tipo</th><th>Regional</th><th>CC / Setor</th><th>Descrição</th><th>Solicitante</th><th>Status</th><th>Data</th><th>Aging</th></tr></thead><tbody>'+rows.map(function(s){return'<tr><td class="mn" style="color:var(--blue)">'+s.solicitacao+'</td><td>'+tagSit(s.tipoSC)+'</td><td>'+s.regional+'</td><td class="te">'+s.ccNome+'</td><td class="te" title="'+s.descricao+'">'+s.descricao+'</td><td>'+sN(s.solicitante)+'</td><td>'+tagSit(s.situacao)+'</td><td class="mn">'+s.data+'</td><td>'+agH(s.aging)+'</td></tr>';}).join('')+'</tbody>');
}
// ══ OCs ══
function rOCs(){
  var ind=D.ind;var ocs=fOCs();
  var tv=ocs.reduce(function(s,o){return s+o.vlrOrig;},0);
  var tl=ocs.filter(function(o){return o.situacao==='Liquidado';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var ta=ocs.filter(function(o){return o.situacao==='Aberto Total';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var nNF=ocs.filter(function(o){return o.situacao==='Não Fechado';});
  var txL=tv?Math.round(tl/tv*1000)/10:0;
  sh('kOC',kH('kb','Total OCs',fN(ocs.length),fN([...new Set(ocs.map(function(o){return o.filial;}))].length)+' filiais')+kH('kb','Valor Total',fR(tv),'')+kH('kg','Liquidado',fR(tl),txL+'%')+kH('ka','Comprometido',fR(ta),'Aberto Total')+kH('ka','Pend. Aprovação',fN(nNF.length),fR(nNF.reduce(function(s,o){return s+o.vlrOrig;},0)))+kH('kn','Fornecedores',fN(ind.fornAtivos),'ativos'));
  // Insights
  var ins=[];
  var top=ind.compradores&&ind.compradores[0];
  if(top&&tv&&top.valor/tv>0.3)ins.push({c:C.b,t:'Maior volume: '+sN(top.nome)+' — '+fR(top.valor)+' ('+pct(top.valor,tv)+')'});
  var topForn=ind.fornecedores&&ind.fornecedores[0];
  if(topForn)ins.push({c:C.b,t:'Fornecedor #1: '+topForn.nome+' — '+fR(topForn.valor)+' (Classe '+topForn.abc+')'});
  if(nNF.length>0)ins.push({c:C.r,t:fN(nNF.length)+' OCs pendentes de aprovação · '+fR(nNF.reduce(function(s,o){return s+o.vlrOrig;},0))+' em risco'});
  var aSit=ind.fornecedores&&ind.fornecedores.filter(function(f){return f.abc==='A';}).length;
  if(aSit)ins.push({c:C.g,t:fN(aSit)+' fornecedores Classe A respondem por 80% do gasto total'});
  sh('insOC',ins.map(function(i){return'<div class="ins"><div class="ins-dot" style="background:'+i.c+'"></div>'+i.t+'</div>';}).join(''));
  // Análise por comprador
  var cm={};ocs.forEach(function(o){var k=o.comprador||'N/D';if(!cm[k])cm[k]={nome:k,setor:o.setor,qtd:0,valor:0,liq:0,nf:0};cm[k].qtd++;cm[k].valor+=o.vlrOrig;if(o.situacao==='Liquidado')cm[k].liq+=o.vlrOrig;if(o.situacao==='Não Fechado')cm[k].nf++;});
  var compList=Object.values(cm).sort(function(a,b){return b.valor-a.valor;});
  sh('tOCcomp','<thead><tr><th>Comprador</th><th>Setor</th><th class="tdr">R$ Total OC</th><th>Qtde OC</th><th>Liquidadas</th><th>Irreg.</th></tr></thead><tbody>'+compList.map(function(c){var txLc=c.valor?Math.round(c.liq/c.valor*1000)/10:0;return'<tr><td style="font-weight:600">'+sN(c.nome)+'</td><td><span class="tag '+(c.setor==='Suprimentos'?'tb':'tn')+'">'+c.setor+'</span></td><td class="mn tdr">'+fR(c.valor)+'</td><td class="mn">'+fN(c.qtd)+'</td><td class="mn" style="color:'+(txLc>=85?C.g:txLc>=60?C.a:C.r)+'">'+fN(c.liq)+' ('+txLc+'%)</td><td class="mn" style="color:'+(c.nf>0?C.a:'var(--tx3)')+'">'+fN(c.nf)+'</td></tr>';}).join('')+'</tbody>');
  // Valor por situação
  var SC={'Liquidado':C.g,'Aberto Total':C.b,'Não Fechado':C.a,'Cancelado':'#94a3b8'};var sits=Object.keys(SC);var sitV={};ocs.forEach(function(o){sitV[o.situacao]=(sitV[o.situacao]||0)+o.vlrOrig;});
  mk('cOCsit',{type:'bar',data:{labels:sits,datasets:[{data:sits.map(function(k){return sitV[k]||0;}),backgroundColor:sits.map(function(k){return SC[k]+'aa';}),borderColor:sits.map(function(k){return SC[k];}),borderWidth:1,borderRadius:4}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},x:{grid:{display:false}}}}});
  var f10=(ind.fornecedores||[]).slice(0,10);
  mk('cOCforn',{type:'bar',data:{labels:f10.map(function(f){var n=f.nome||'';return n.length>22?n.slice(0,20)+'..':n;}),datasets:[{data:f10.map(function(f){return f.valor;}),backgroundColor:f10.map(function(f){return f.abc==='A'?C.g2:f.abc==='B'?C.a2:'rgba(148,163,184,.5)';}),borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},y:{grid:{display:false},ticks:{font:{size:9}}}}}});
  rOCTbl();
}
function rOCTbl(){
  if(!D)return;
  var q=(($('sOC')||{}).value||'').toLowerCase();var sit=(($('fOCSit')||{}).value||'');var cp=(($('fOCCp')||{}).value||'');var reg=(($('fOCReg')||{}).value||'');var tp=(($('fOCTp')||{}).value||'');
  var f=gGet();
  var rows=(D.ocs||[]).filter(function(o){return(!f.gAno||o.ano===f.gAno)&&(!f.gMes||o.mes===f.gMes)&&(!f.gSetor||o.setor===f.gSetor)&&(!f.gReg||o.regional===f.gReg)&&(!f.gComp||o.comprador.toLowerCase().startsWith(f.gComp.toLowerCase().split(' ')[0]))&&(!q||(o.filialOC+' '+o.fornecedorNome+' '+o.comprador).toLowerCase().includes(q))&&(!sit||o.situacao===sit)&&(!cp||o.comprador===cp)&&(!reg||o.regional===reg)&&(!tp||o.tipo===tp);});
  var tv=rows.reduce(function(s,o){return s+o.vlrOrig;},0);
  sh('cntOC',fN(rows.length)+' OCs · '+fR(tv));
  sh('tOC','<thead><tr><th>FILIAL-OC</th><th>Regional</th><th>Situação</th><th>Tipo</th><th>Setor</th><th>Comprador</th><th>Fornecedor</th><th class="tdr">Vlr. Original</th><th>Emissão</th><th>Dias</th></tr></thead><tbody>'+rows.map(function(o){return'<tr><td class="mn" style="color:var(--blue);font-weight:600">'+o.filialOC+'</td><td>'+o.regional+'</td><td>'+tagSit(o.situacao)+'</td><td>'+tagSit(o.tipo||'—')+'</td><td><span class="tag '+(o.setor==='Suprimentos'?'tb':'tn')+'">'+o.setor+'</span></td><td>'+sN(o.comprador)+'</td><td class="te" title="'+o.fornecedorNome+'">'+o.fornecedorNome+'</td><td class="mn tdr">'+fR(o.vlrOrig)+'</td><td class="mn">'+o.emissao+'</td><td>'+agH(o.diasAberto)+'</td></tr>';}).join('')+'</tbody>');
}
// ══ PERFORMANCE ══
function rPerf(){
  var ind=D.ind;var ocs=fOCs();var tv=ocs.reduce(function(s,o){return s+o.vlrOrig;},0)||1;
  var ts=ind.totalSaving;var tvi=ind.totalVI;var sr=tvi?Math.round(ts/tvi*1000)/10:0;
  var topRate=ind.savCompArr&&ind.savCompArr.filter(function(s){return s.rate>=8;}).length;
  sh('kP',kH('kb','Compradores',fN(ind.compradores.length),'')+kH('kg','Saving Total',fR(ts),sr+'% rate')+kH(sr>=8?'kg':'ka','Rate Médio',sr+'%','meta: >8%')+kH('kb','Acima da Meta',fN(topRate),topRate+' compradores ≥8%'));
  rPComp();rPForn();
  var sl=ind.savCompArr||[];
  mk('cPvol',{type:'bar',data:{labels:(ind.compradores||[]).map(function(c){return sN(c.nome);}),datasets:[{label:'Valor OCs',data:(ind.compradores||[]).map(function(c){return c.valor;}),backgroundColor:C.b2,borderColor:C.b,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},x:{grid:{display:false}}}}});
  mk('cPsav',{type:'bar',data:{labels:sl.map(function(s){return s.nome;}),datasets:[{label:'Saving',data:sl.map(function(s){return s.saving;}),backgroundColor:C.g2,borderColor:C.g,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},x:{grid:{display:false}}}}});
  mk('cPrate',{type:'bar',data:{labels:sl.map(function(s){return s.nome;}),datasets:[{label:'Rate %',data:sl.map(function(s){return s.rate;}),backgroundColor:sl.map(function(s){return s.rate>=20?C.g2:s.rate>=8?C.a2:C.r2;}),borderRadius:3},{label:'Meta 8%',data:sl.map(function(){return 8;}),borderColor:C.b,borderDash:[4,4],type:'line',pointRadius:0,borderWidth:1.5}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return v+'%';}}},x:{grid:{display:false}}}}});
}
function rPComp(){
  var ind=D.ind;var comps=ind.compradores||[];var tv=ind.totalValor||1;
  var sf=(($('fPSt')||{}).value||'');var rows=sf?comps.filter(function(c){return c.setor===sf;}):comps;
  sh('tPcomp','<thead><tr><th>Comprador</th><th>Setor</th><th>OCs</th><th class="tdr">Volume</th><th>%</th><th>Irreg.</th><th class="tdr">Saving</th><th>Rate</th></tr></thead><tbody>'+rows.map(function(c){return'<tr><td style="font-weight:600">'+sN(c.nome)+'</td><td><span class="tag '+(c.setor==='Suprimentos'?'tb':'tn')+'">'+c.setor+'</span></td><td class="mn">'+fN(c.qtd)+'</td><td class="mn tdr">'+fR(c.valor)+'</td><td><div class="mb"><div class="mbt"><div class="mbf" style="width:'+Math.min(Math.round(c.valor/tv*100),100)+'%;background:'+C.b+'"></div></div>'+pct(c.valor,tv)+'</div></td><td class="mn" style="color:'+(c.irreg>0?C.a:'var(--tx3)')+'">'+fN(c.irreg)+'</td><td class="mn tdr" style="color:'+C.g+'">'+(c.saving?fR(c.saving):'—')+'</td><td class="mn" style="color:'+(c.savingRate&&c.savingRate>=8?C.g:C.a)+'">'+(c.savingRate!==null?c.savingRate+'%':'—')+'</td></tr>';}).join('')+'</tbody>');
}
function rPForn(){
  var forns=D.ind.fornecedores||[];var af=(($('fPFabc')||{}).value||'');var rows=af?forns.filter(function(f){return f.abc===af;}):forns;
  sh('tPforn','<thead><tr><th>#</th><th>Fornecedor</th><th>OCs</th><th class="tdr">Valor</th><th>Acum.</th><th>ABC</th></tr></thead><tbody>'+rows.slice(0,30).map(function(f,i){return'<tr><td class="mn" style="color:var(--tx3)">'+(i+1)+'</td><td class="te">'+f.nome+'</td><td class="mn">'+fN(f.qtd)+'</td><td class="mn tdr">'+fR(f.valor)+'</td><td class="mn">'+f.pctAcum+'%</td><td><span class="abc'+f.abc.toLowerCase()+'">'+f.abc+'</span></td></tr>';}).join('')+'</tbody>');
}
// ══ FINANCEIRO ══
function rFin(){
  var ind=D.ind;var ocs=fOCs();
  var tv=ocs.reduce(function(s,o){return s+o.vlrOrig;},0);
  var tl=ocs.filter(function(o){return o.situacao==='Liquidado';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var ta=ocs.filter(function(o){return o.situacao==='Aberto Total';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var tnf=ocs.filter(function(o){return o.situacao==='Não Fechado';}).reduce(function(s,o){return s+o.vlrOrig;},0);
  var txL=tv?Math.round(tl/tv*1000)/10:0;
  sh('kFin',kH('kg','Liquidado',fR(tl),txL+'%')+kH('kb','Comprometido',fR(ta),fN(ocs.filter(function(o){return o.situacao==='Aberto Total';}).length)+' OCs')+kH('ka','Pend. Aprovação',fR(tnf),fN(ocs.filter(function(o){return o.situacao==='Não Fechado';}).length)+' OCs')+kH('kg','Taxa Liquidação',txL+'%','meta >85%'));
  sh('fcnt',fN(ocs.length)+' OCs · '+fR(tv));
  var SC={'Liquidado':C.g,'Aberto Total':C.b,'Não Fechado':C.a,'Cancelado':'#94a3b8'};var sits=['Liquidado','Aberto Total','Não Fechado','Cancelado'];var sitV={};ocs.forEach(function(o){sitV[o.situacao]=(sitV[o.situacao]||0)+o.vlrOrig;});
  mk('cFinB',{type:'bar',data:{labels:sits,datasets:[{data:sits.map(function(k){return sitV[k]||0;}),backgroundColor:sits.map(function(k){return SC[k]+'aa';}),borderColor:sits.map(function(k){return SC[k];}),borderWidth:1,borderRadius:4}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},x:{grid:{display:false}}}}});
  // Curva ABC melhorada: gráfico de pizza com 3 grupos claros
  var forns=ind.fornecedores||[];
  var grpA=forns.filter(function(f){return f.abc==='A';});var grpB=forns.filter(function(f){return f.abc==='B';});var grpC=forns.filter(function(f){return f.abc==='C';});
  var vA=grpA.reduce(function(s,f){return s+f.valor;},0);var vB=grpB.reduce(function(s,f){return s+f.valor;},0);var vC=grpC.reduce(function(s,f){return s+f.valor;},0);
  mk('cFinAbc',{type:'doughnut',data:{labels:['Classe A — '+fN(grpA.length)+' fornecedores','Classe B — '+fN(grpB.length)+' fornecedores','Classe C — '+fN(grpC.length)+' fornecedores'],datasets:[{data:[vA,vB,vC],backgroundColor:[C.g2,C.a2,'rgba(148,163,184,.5)'],borderWidth:2,borderColor:'#fff',hoverOffset:6}]},options:{responsive:true,maintainAspectRatio:false,cutout:'55%',plugins:{legend:{position:'right',labels:{font:{size:11},padding:10}}}}});
  var f15=(ind.fornecedores||[]).slice(0,15);
  mk('cFinForn',{type:'bar',data:{labels:f15.map(function(f){var n=f.nome||'';return n.length>24?n.slice(0,22)+'..':n;}),datasets:[{data:f15.map(function(f){return f.valor;}),backgroundColor:f15.map(function(f){return f.abc==='A'?C.g2:f.abc==='B'?C.a2:'rgba(148,163,184,.45)';}),borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},y:{grid:{display:false},ticks:{font:{size:9}}}}}});
  var nf=ind.naoFechado||[];
  sh('tFinNf','<thead><tr><th>FILIAL-OC</th><th>Tipo</th><th>Comprador</th><th>Fornecedor</th><th class="tdr">Vlr. Original</th><th>Dias</th></tr></thead><tbody>'+nf.map(function(o){return'<tr><td class="mn" style="color:var(--amb)">'+o.filialOC+'</td><td>'+tagSit(o.tipo||'—')+'</td><td>'+sN(o.comprador)+'</td><td class="te">'+o.fornecedorNome+'</td><td class="mn tdr">'+fR(o.vlrOrig)+'</td><td>'+agH(o.diasAberto)+'</td></tr>';}).join('')+'</tbody>');
}
// ══ SAVING ══
function rSav(){
  var ind=D.ind;var sv=fSav();
  var ts=sv.reduce(function(s,x){return s+x.saving;},0);var tvi=sv.reduce(function(s,x){return s+x.vlrInicial;},0);var sr=tvi?Math.round(ts/tvi*1000)/10:0;
  var sl=ind.savCompArr||[];
  // Hero card
  sh('savHero','<div class="sav-hero"><div class="sav-hero-main"><div class="lbl">💰 Economia Gerada</div><div class="val">'+fR(ts)+'</div><div class="sub">'+fN(sv.length)+' negociações · Rate '+sr+'% '+( sr>=8?'✓ acima do benchmark 8%':'⚠ abaixo do benchmark 8%')+'</div></div><div class="sav-hero-stats"><div class="sav-stat"><div class="sv">'+fR(tvi)+'</div><div class="sl">Valor Inicial</div></div><div class="sav-stat"><div class="sv">'+sr+'%</div><div class="sl">Rate Médio</div></div><div class="sav-stat"><div class="sv">'+fN(sl.filter(function(s){return s.rate>=8;}).length)+'</div><div class="sl">Comprad. ≥8%</div></div></div></div>');
  sh('kSav','');sh('fcnt',fN(sv.length)+' registros · '+fR(ts)+' saving');
  mk('cSavC',{type:'bar',data:{labels:sl.map(function(s){return s.nome;}),datasets:[{label:'Saving',data:sl.map(function(s){return s.saving;}),backgroundColor:C.g2,borderColor:C.g,borderWidth:1,borderRadius:3,yAxisID:'y'},{label:'Rate %',data:sl.map(function(s){return s.rate;}),borderColor:C.b,type:'line',yAxisID:'y2',fill:false,tension:.3,pointRadius:3,borderWidth:1.5}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}},title:{display:true,text:'Saving'}},y2:{position:'right',grid:{display:false},ticks:{callback:function(v){return v+'%';}}}}}});
  var st=ind.savPorSetor||{};var sa=Object.keys(st).map(function(k){return{k:k,v:st[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,8);
  mk('cSavS',{type:'bar',data:{labels:sa.map(function(x){return x.k;}),datasets:[{data:sa.map(function(x){return x.v;}),backgroundColor:C.b2,borderColor:C.b,borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC},ticks:{callback:function(v){return fR(v);}}},y:{grid:{display:false}}}}});
  var md=ind.savPorModo||{};var mA=Object.keys(md);
  mk('cSavM',{type:'doughnut',data:{labels:mA.map(function(k){return k+' — '+fR(md[k]);}),datasets:[{data:mA.map(function(k){return md[k];}),backgroundColor:[C.g2,C.b2,C.a2],borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'50%',plugins:{legend:{position:'bottom',labels:{font:{size:10},padding:7}}}}});
  mk('cSavR',{type:'bar',data:{labels:sl.map(function(s){return s.nome;}),datasets:[{label:'Rate %',data:sl.map(function(s){return s.rate;}),backgroundColor:sl.map(function(s){return s.rate>=20?C.g2:s.rate>=8?C.a2:C.r2;}),borderRadius:3},{label:'Meta 8%',data:sl.map(function(){return 8;}),borderColor:C.b,borderDash:[4,4],type:'line',pointRadius:0,borderWidth:1.5}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC},ticks:{callback:function(v){return v+'%';}}},x:{grid:{display:false}}}}});
  rSavTbl();
}
function rSavTbl(){
  var sv=fSav();var q=(($('sSav')||{}).value||'').toLowerCase();var cp=(($('fSavC')||{}).value||'');var md=(($('fSavM')||{}).value||'');var st=(($('fSavSt')||{}).value||'');
  var rows=sv.filter(function(s){return(!q||(s.descricao||'').toLowerCase().includes(q)||(s.fornecedor||'').toLowerCase().includes(q))&&(!cp||s.comprador===cp)&&(!md||s.modo===md)&&(!st||s.setor===st);});
  sh('cntSav',fN(rows.length)+' registros');
  sh('tSav','<thead><tr><th>FILIAL-OC</th><th>Comprador</th><th>Setor</th><th>Fornecedor</th><th>Descrição</th><th class="tdr">Vlr. Inicial</th><th class="tdr">Saving</th><th>Rate</th><th>Modo</th></tr></thead><tbody>'+rows.map(function(s){var r=s.vlrInicial?Math.round(s.saving/s.vlrInicial*1000)/10:0;return'<tr><td class="mn">'+s.filialOC+'</td><td>'+s.comprador+'</td><td><span class="tag '+(s.setor==='Suprimentos'?'tb':'tn')+'">'+s.setor+'</span></td><td class="te">'+s.fornecedor+'</td><td class="te" title="'+s.descricao+'">'+s.descricao+'</td><td class="mn tdr">'+fRd(s.vlrInicial)+'</td><td class="mn tdr" style="color:'+C.g+';font-weight:600">'+fRd(s.saving)+'</td><td class="mn" style="color:'+(r>=8?C.g:C.a)+'">'+r+'%</td><td>'+tagSit(s.modo||'—')+'</td></tr>';}).join('')+'</tbody>');
}
// ══ CHAMADOS MAN (+ Recorrência incorporada) ══
function rCham(){
  var ind=D.ind;var ch=fCham();var ca=ch.filter(function(c){return c.aberto;});
  sh('kCh',kH('kb','Total',fN(ind.chamTotal),'')+kH('kr','Abertos',fN(ind.chamAbertos),'aguardando')+kH('kb','Em Aprovação',fN(ind.chamAprov),'')+kH('kg','Concluídos',fN(ind.chamConc),'')+kH('ka','Aging Médio',fN(ind.chamAgMed)+'d','')+kH('kr','Críticos',fN(ind.chamCrit),'')+kH('kb','Com SC',fN(ind.chamComSC),pct(ind.chamComSC,ind.chamTotal))+kH('kb','Preventivo',fN(ind.chamPrev),pct(ind.chamPrev,ind.chamTotal)));
  var alts=[];
  if(ind.chamCrit>0)alts.push({c:'ar',b:true,t:fN(ind.chamCrit)+' chamados críticos/urgentes abertos'});
  if(ind.chamSemSC>10)alts.push({c:'aa',b:false,t:fN(ind.chamSemSC)+' chamados abertos sem SC vinculada'});
  if(ind.chamAgMed>7)alts.push({c:'aa',b:false,t:'Aging médio '+fN(ind.chamAgMed)+'d — acima do ideal'});
  sh('aCh',alts.map(function(a){return'<div class="al '+a.c+'"><div class="adot'+(a.b?' bl':'')+'"></div>'+a.t+'</div>';}).join(''));
  if(!D.chamados||!D.chamados.length){['cChSt','cChAg','cChPr','cChMes','cChMo','cRuf','cRec'].forEach(function(id){var el=$(id);if(el&&el.parentNode)el.parentNode.innerHTML='<div style="padding:14px;text-align:center;color:var(--tx3);font-size:11px">Sem dados · verifique aba CHAMADOS MAN</div>';});sh('tCh','<tbody><tr><td colspan="9" style="text-align:center;color:var(--tx3);padding:16px">Nenhum chamado carregado</td></tr></tbody>');sh('cntCh','0');sh('tRec','');return;}
  var stC=function(s){var u=s.toUpperCase();if(u.includes('ENCAMINHADO')||u.includes('AGUARDANDO ORÇAMENTO')||u.includes('EM ANÁLISE'))return C.r;if(u.includes('APROVAÇÃO'))return C.a;if(u.includes('EXECUÇÃO'))return C.b;if(u.includes('ENCERRADO')||u.includes('CONCLUÍDO'))return C.g;return '#94a3b8';};
  var ss=ind.chamPorStatus||{};var ssK=Object.keys(ss);
  mk('cChSt',{type:'doughnut',data:{labels:ssK,datasets:[{data:ssK.map(function(k){return ss[k];}),backgroundColor:ssK.map(function(k){return stC(k)+'bb';}),borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'50%',plugins:{legend:{position:'right',labels:{font:{size:9}}}}}});
  var ab=ind.chamAgBuckets||{};var abK=Object.keys(ab);
  mk('cChAg',{type:'bar',data:{labels:abK,datasets:[{data:abK.map(function(k){return ab[k];}),backgroundColor:[C.g2,C.g2,C.a2,C.r2,C.r2],borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC}},x:{grid:{display:false}}}}});
  var pp=ind.chamPorPrior||{};var ppK=Object.keys(pp);var ppC={'Crítica':C.r,'Urgente':C.r,'Alta':C.a,'Média':C.b,'Normal':C.b,'Baixa':C.g};
  mk('cChPr',{type:'doughnut',data:{labels:ppK,datasets:[{data:ppK.map(function(k){return pp[k];}),backgroundColor:ppK.map(function(k){return(ppC[k]||'#94a3b8')+'bb';}),borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'50%',plugins:{legend:{position:'right',labels:{font:{size:9}}}}}});
  var cpm=ind.chamPorMes||{};var cpmK=Object.keys(cpm).sort();
  mk('cChMes',{type:'bar',data:{labels:cpmK,datasets:[{data:cpmK.map(function(k){return cpm[k];}),backgroundColor:C.r2,borderColor:C.r,borderWidth:1,borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:GC}},x:{grid:{display:false},ticks:{font:{size:9},maxRotation:30}}}}});
  var pm=ind.chamPorMotivo||{};var pma=Object.keys(pm).map(function(k){return{k:k,v:pm[k]};}).sort(function(a,b){return b.v-a.v;}).slice(0,8);
  mk('cChMo',{type:'bar',data:{labels:pma.map(function(x){return x.k.length>26?x.k.slice(0,24)+'..':x.k;}),datasets:[{data:pma.map(function(x){return x.v;}),backgroundColor:C.a2,borderColor:C.a,borderWidth:1,borderRadius:3}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{grid:{color:GC}},y:{grid:{display:false},ticks:{font:{size:9}}}}}});
  // Recorrência
  var rec=ind.recorrencia||[];var grave=rec.filter(function(r){return r.count>=3;}).length;
  sh('kRec',kH('kr','Reincidências',fN(rec.length),'Loja+Motivo 2+ ocorr.')+kH('kr','Grave (3+)',fN(grave),'')+kH('ka','Corretivo',fN(ind.chamCorr),pct(ind.chamCorr,ind.chamTotal))+kH('kg','Preventivo',fN(ind.chamPrev),pct(ind.chamPrev,ind.chamTotal)));
  var pu={};ch.forEach(function(c){if(c.uf&&c.uf!=='N/D')pu[c.uf]=(pu[c.uf]||0)+1;});
  var pua=Object.keys(pu).map(function(k){return{k:k,v:pu[k]};}).sort(function(a,b){return b.v-a.v;});
  mk('cRuf',{type:'doughnut',data:{labels:pua.map(function(x){return x.k+'  '+fN(x.v);}),datasets:[{data:pua.map(function(x){return x.v;}),backgroundColor:C.pal,borderWidth:1,borderColor:'#fff',hoverOffset:4}]},options:{responsive:true,maintainAspectRatio:false,cutout:'50%',plugins:{legend:{position:'right',labels:{font:{size:10}}}}}});
  var top15=rec.slice(0,15);
  mk('cRec',{type:'bar',data:{labels:top15.map(function(r){return(r.loja||'').slice(0,10)+'|'+(r.motivo||'').slice(0,10);}),datasets:[{label:'Concluídos',data:top15.map(function(r){return r.count-r.abertos;}),backgroundColor:C.g2,stack:'s',borderRadius:0},{label:'Abertos',data:top15.map(function(r){return r.abertos;}),backgroundColor:C.r2,stack:'s',borderRadius:3}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{position:'top',labels:{font:{size:10}}}},scales:{y:{grid:{color:GC},stacked:true},x:{grid:{display:false},stacked:true,ticks:{font:{size:8},maxRotation:35}}}}});
  sh('tRec','<thead><tr><th>#</th><th>Loja</th><th>UF</th><th>Motivo</th><th>Total</th><th>Abertos</th><th>Nível</th></tr></thead><tbody>'+rec.map(function(r,i){var nv=r.count>=5?['tr2','Crítico']:r.count>=3?['ta','Atenção']:['tb','Monitorar'];return'<tr><td class="mn" style="color:var(--tx3)">'+(i+1)+'</td><td style="font-weight:500" class="te">'+r.loja+'</td><td class="mn">'+r.uf+'</td><td class="te">'+r.motivo+'</td><td class="mn" style="font-weight:700;color:'+(r.count>=5?C.r:r.count>=3?C.a:C.b)+'">'+fN(r.count)+'×</td><td class="mn" style="color:'+(r.abertos>0?C.a:'var(--tx3)')+'">'+fN(r.abertos)+'</td><td><span class="tag '+nv[0]+'">'+nv[1]+'</span></td></tr>';}).join('')+'</tbody>');
  rChTbl();
}
function rChTbl(){
  var ch=D.chamados||[];var q=(($('sCh')||{}).value||'').toLowerCase();var fSt=(($('fChSt')||{}).value||'');var fPr=(($('fChPr')||{}).value||'');var fTp=(($('fChTp')||{}).value||'');var fSC=(($('fChSC')||{}).value||'');var f=gGet();
  var rows=ch.filter(function(c){return(!f.gAno||c.ano===f.gAno)&&(!f.gUF||c.uf===f.gUF)&&(!q||(c.protocolo||'').includes(q)||(c.local||'').toLowerCase().includes(q)||(c.motivo||'').toLowerCase().includes(q))&&(!fSt||c.status===fSt)&&(!fPr||c.prioridade===fPr)&&(!fTp||c.tipo===fTp)&&(!fSC||(fSC==='sim'&&c.sc&&c.sc!=='')||(fSC==='nao'&&(!c.sc||c.sc===''))  );}).sort(function(a,b){var po={'Crítica':0,'Urgente':0,'Alta':1,'Média':2,'Normal':2,'Baixa':3};var pa=po[a.prioridade]!==undefined?po[a.prioridade]:2,pb=po[b.prioridade]!==undefined?po[b.prioridade]:2;if(pa!==pb)return pa-pb;return(b.aging||0)-(a.aging||0);});
  sh('cntCh',fN(rows.length)+' chamados');
  sh('tCh','<thead><tr><th>Protocolo</th><th>Local</th><th>UF</th><th>Motivo</th><th>Tipo</th><th>Status</th><th>Prioridade</th><th>Aging</th><th>SC</th></tr></thead><tbody>'+rows.map(function(c){return'<tr><td class="mn" style="color:var(--blue);font-weight:600">'+c.protocolo+'</td><td class="te">'+c.local+'</td><td class="mn">'+c.uf+'</td><td class="te" title="'+c.motivo+'">'+c.motivo+'</td><td><span class="tag '+(c.tipo==='Preventivo'?'tb':'ta')+'">'+c.tipo+'</span></td><td><span class="tag tn" style="font-size:9px">'+c.status+'</span></td><td>'+prTag(c.prioridade)+'</td><td>'+agH(c.aging)+'</td><td class="mn" style="color:'+(c.sc?C.b:'var(--tx3)')+'">'+( c.sc||'—')+'</td></tr>';}).join('')+'</tbody>');
}
window.addEventListener('load',init);
</script>
</body>
</html>
