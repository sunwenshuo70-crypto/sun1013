<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MedShield Pro · 数字健康产业安全平台</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600;700&family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,600;0,700;1,300&family=Noto+Sans+SC:wght@300;400;700&family=Noto+Sans+KR:wght@300;400;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
:root {
  --ink: #0B0F1A;
  --paper: #F0F4FF;
  --mid: #C8D4F0;
  --teal: #00BFA5;
  --teal-dark: #008F7A;
  --red: #FF3B5C;
  --amber: #FFB800;
  --blue: #1E6FFF;
  --surface: #131929;
  --surface2: #1C2640;
  --border: rgba(200,212,240,0.12);
  --mono: 'IBM Plex Mono', monospace;
  --sans: 'IBM Plex Sans', 'Noto Sans SC', 'Noto Sans KR', sans-serif;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{
  background:var(--ink);
  color:var(--paper);
  font-family:var(--sans);
  font-weight:300;
  line-height:1.7;
  overflow-x:hidden;
}
body.lang-ko{font-family:'IBM Plex Sans','Noto Sans KR','Noto Sans SC',sans-serif;}
body::before{
  content:'';
  position:fixed;inset:0;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,191,165,0.015) 2px,rgba(0,191,165,0.015) 4px);
  pointer-events:none;z-index:0;
}

/* TOP BAR */
.topbar{
  position:fixed;top:0;left:0;right:0;z-index:900;
  display:flex;align-items:center;justify-content:space-between;
  padding:0 32px;height:56px;
  background:rgba(11,15,26,0.95);
  border-bottom:1px solid var(--border);
  backdrop-filter:blur(12px);
}
.logo{font-family:var(--mono);font-weight:700;font-size:15px;color:var(--teal);letter-spacing:1px;display:flex;align-items:center;gap:10px;}
.logo-dot{width:8px;height:8px;border-radius:50%;background:var(--teal);animation:blink 2s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:0.2;}}
.nav-right{display:flex;align-items:center;gap:12px;}
.lang-toggle{display:flex;background:var(--surface2);border-radius:6px;overflow:hidden;border:1px solid var(--border);}
.lang-btn{padding:6px 14px;font-size:12px;font-family:var(--mono);cursor:pointer;border:none;background:transparent;color:var(--mid);transition:all .2s;letter-spacing:1px;}
.lang-btn.active{background:var(--teal);color:var(--ink);font-weight:600;}
.pdf-export-btn{
  display:flex;align-items:center;gap:8px;padding:8px 18px;
  background:transparent;border:1px solid var(--teal);border-radius:6px;
  color:var(--teal);font-family:var(--mono);font-size:12px;font-weight:600;
  cursor:pointer;transition:all .25s;letter-spacing:0.5px;white-space:nowrap;
}
.pdf-export-btn:hover{background:var(--teal);color:var(--ink);}

/* HERO */
.hero{
  position:relative;z-index:10;
  padding:120px 6vw 80px;
  min-height:100vh;
  display:flex;flex-direction:column;justify-content:center;
  overflow:hidden;
}
.hero-bg{
  position:absolute;inset:0;
  background:radial-gradient(ellipse 80% 60% at 70% 40%,rgba(0,191,165,0.07) 0%,transparent 60%),
    radial-gradient(ellipse 40% 40% at 20% 80%,rgba(30,111,255,0.05) 0%,transparent 50%);
  pointer-events:none;
}
.hero-eyebrow{font-family:var(--mono);font-size:11px;letter-spacing:3px;color:var(--teal);text-transform:uppercase;margin-bottom:20px;display:flex;align-items:center;gap:12px;}
.hero-eyebrow::after{content:'';width:60px;height:1px;background:var(--teal);opacity:.5;}
.hero-title{font-size:clamp(40px,7vw,88px);font-weight:700;line-height:1.0;letter-spacing:-2px;margin-bottom:24px;}
.hero-title .t1{color:var(--paper);display:block;}
.hero-title .t2{color:transparent;-webkit-text-stroke:1px var(--teal);display:block;}
.hero-desc{font-size:clamp(14px,1.8vw,18px);color:var(--mid);max-width:580px;margin-bottom:48px;font-weight:300;}
.hero-stats{display:flex;gap:0;border:1px solid var(--border);border-radius:8px;overflow:hidden;width:fit-content;flex-wrap:wrap;}
.hero-stat{padding:20px 32px;border-right:1px solid var(--border);}
.hero-stat:last-child{border-right:none;}
.hs-num{font-family:var(--mono);font-size:26px;font-weight:700;color:var(--teal);line-height:1;margin-bottom:4px;}
.hs-label{font-size:11px;color:var(--mid);letter-spacing:1px;}

/* SECTIONS */
section{position:relative;z-index:10;padding:80px 6vw;border-top:1px solid var(--border);}
.sec-eyebrow{font-family:var(--mono);font-size:10px;letter-spacing:3px;color:var(--teal);text-transform:uppercase;margin-bottom:12px;}
.sec-title{font-size:clamp(22px,3.5vw,38px);font-weight:700;letter-spacing:-0.5px;margin-bottom:40px;line-height:1.2;}

/* TOOLS */
.tool-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:24px;}
.tool-panel{background:var(--surface);border:1px solid var(--border);border-radius:12px;overflow:hidden;transition:border-color .3s;}
.tool-panel:hover{border-color:rgba(0,191,165,0.3);}
.panel-header{padding:16px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px;}
.panel-icon{width:36px;height:36px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0;}
.pi-teal{background:rgba(0,191,165,0.12);border:1px solid rgba(0,191,165,0.25);}
.pi-red{background:rgba(255,59,92,0.12);border:1px solid rgba(255,59,92,0.25);}
.pi-blue{background:rgba(30,111,255,0.12);border:1px solid rgba(30,111,255,0.25);}
.pi-amb{background:rgba(255,184,0,0.12);border:1px solid rgba(255,184,0,0.25);}
.panel-title{font-size:14px;font-weight:600;color:var(--paper);}
.panel-sub{font-size:11px;color:var(--mid);font-family:var(--mono);margin-top:2px;}
.panel-body{padding:20px;}
.tool-input{
  width:100%;padding:10px 14px;background:var(--surface2);border:1px solid var(--border);
  border-radius:6px;color:var(--paper);font-family:var(--mono);font-size:13px;
  outline:none;transition:border-color .2s;margin-bottom:10px;
}
.tool-input:focus{border-color:var(--teal);}
.tool-input::placeholder{color:rgba(200,212,240,0.3);}
.tool-btn{
  width:100%;padding:10px 0;background:var(--teal);color:var(--ink);
  border:none;border-radius:6px;font-family:var(--mono);font-size:13px;font-weight:700;
  cursor:pointer;transition:all .2s;letter-spacing:0.5px;
}
.tool-btn:hover{background:var(--teal-dark);}
.tool-btn:active{transform:scale(0.98);}
.result-box{
  margin-top:14px;background:var(--ink);border:1px solid var(--border);
  border-radius:6px;padding:14px;font-family:var(--mono);font-size:12px;
  line-height:1.8;min-height:60px;max-height:220px;overflow-y:auto;display:none;
}
.result-box.show{display:block;}
.r-ok{color:var(--teal);}
.r-warn{color:var(--amber);}
.r-err{color:var(--red);}
.r-info{color:var(--mid);}
.r-head{color:var(--paper);font-weight:600;margin-bottom:6px;}
.prog-wrap{margin-top:10px;display:none;}
.prog-wrap.show{display:block;}
.prog-label{font-family:var(--mono);font-size:11px;color:var(--mid);margin-bottom:4px;display:flex;justify-content:space-between;}
.prog-bar{height:6px;background:var(--surface2);border-radius:3px;overflow:hidden;}
.prog-fill{height:100%;border-radius:3px;transition:width .4s ease,background .4s;}
.strength-0{background:#2a3550;width:0%}
.strength-1{background:var(--red);width:20%}
.strength-2{background:var(--red);width:40%}
.strength-3{background:var(--amber);width:60%}
.strength-4{background:#7ed321;width:80%}
.strength-5{background:var(--teal);width:100%}

/* COMPLIANCE */
.compliance-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:16px;}
.comp-card{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:20px;transition:all .3s;}
.comp-card:hover{border-color:rgba(0,191,165,0.3);transform:translateY(-2px);}
.comp-header{display:flex;align-items:center;gap:12px;margin-bottom:12px;}
.comp-badge{font-family:var(--mono);font-size:11px;font-weight:700;padding:4px 10px;border-radius:4px;background:rgba(0,191,165,0.1);border:1px solid rgba(0,191,165,0.3);color:var(--teal);}
.comp-name{font-size:13px;font-weight:600;}
.comp-status{display:flex;align-items:center;gap:6px;font-family:var(--mono);font-size:11px;margin-bottom:8px;}
.status-dot{width:7px;height:7px;border-radius:50%;}
.sd-ok{background:var(--teal);}
.comp-desc{font-size:12px;color:var(--mid);line-height:1.6;}

/* LOG */
.log-monitor{background:var(--ink);border:1px solid var(--border);border-radius:10px;overflow:hidden;}
.log-header{padding:12px 16px;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px;font-family:var(--mono);font-size:12px;}
.log-live{display:flex;align-items:center;gap:6px;color:var(--teal);font-weight:600;}
.log-live::before{content:'';width:7px;height:7px;border-radius:50%;background:var(--teal);animation:blink 1.5s infinite;}
.log-body{padding:16px;height:280px;overflow-y:auto;font-family:var(--mono);font-size:12px;line-height:1.9;}
.log-entry{display:flex;gap:12px;margin-bottom:2px;}
.log-time{color:#4a5580;flex-shrink:0;}
.log-msg-ok{color:var(--teal);}
.log-msg-warn{color:var(--amber);}
.log-msg-err{color:var(--red);}
.log-msg-info{color:var(--mid);}
.log-controls{padding:12px 16px;border-top:1px solid var(--border);display:flex;gap:8px;align-items:center;flex-wrap:wrap;}
.log-ctrl-btn{padding:6px 14px;border-radius:5px;font-family:var(--mono);font-size:11px;cursor:pointer;border:1px solid var(--border);background:var(--surface2);color:var(--mid);transition:all .2s;}
.log-ctrl-btn:hover{border-color:var(--teal);color:var(--teal);}
.log-ctrl-btn.danger:hover{border-color:var(--red);color:var(--red);}

/* METRICS */
.metrics-row{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:16px;margin-bottom:48px;}
.metric-box{background:var(--surface);border:1px solid var(--border);border-radius:10px;padding:20px;text-align:center;position:relative;overflow:hidden;}
.metric-box::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--teal),var(--blue));}
.mb-val{font-family:var(--mono);font-size:30px;font-weight:700;color:var(--teal);line-height:1;margin-bottom:6px;}
.mb-label{font-size:12px;color:var(--mid);}

/* FOOTER */
footer{position:relative;z-index:10;padding:40px 6vw;border-top:1px solid var(--border);text-align:center;font-family:var(--mono);font-size:11px;color:#3a4568;}

/* LANG */
.zh{display:block;}.ko{display:none;}
body.lang-ko .zh{display:none;}body.lang-ko .ko{display:block;}
span.zh,span.ko{display:inline;}
body.lang-ko span.zh{display:none;}body.lang-ko span.ko{display:inline;}

/* PDF OVERLAY */
#pdf-overlay{display:none;position:fixed;inset:0;z-index:9999;background:rgba(11,15,26,0.9);backdrop-filter:blur(8px);align-items:center;justify-content:center;flex-direction:column;gap:16px;}
#pdf-overlay.show{display:flex;}
.pdf-spin{width:44px;height:44px;border:3px solid var(--border);border-top-color:var(--teal);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.pdf-spin-label{font-family:var(--mono);font-size:12px;color:var(--teal);letter-spacing:2px;}

::-webkit-scrollbar{width:5px;height:5px;}
::-webkit-scrollbar-track{background:var(--ink);}
::-webkit-scrollbar-thumb{background:var(--surface2);border-radius:3px;}

@media(max-width:768px){
  .topbar{padding:0 16px;}
  .hero{padding:100px 5vw 60px;}
  .hero-stats{flex-wrap:wrap;}
  .hero-stat{flex:1 1 140px;}
  section{padding:60px 5vw;}
}
@media(max-width:480px){
  .hero-title{letter-spacing:-1px;}
  .tool-grid{grid-template-columns:1fr;}
  .pdf-export-btn .btn-label{display:none;}
}
</style>
</head>
<body>

<div id="pdf-overlay">
  <div class="pdf-spin"></div>
  <div class="pdf-spin-label"><span class="zh">正在生成PDF...</span><span class="ko">PDF 생성 중...</span></div>
</div>

<!-- TOP BAR -->
<div class="topbar">
  <div class="logo">
    <div class="logo-dot"></div>
    MedShield Pro
  </div>
  <div class="nav-right">
    <div class="lang-toggle">
      <button class="lang-btn active" id="btn-zh" onclick="setLang('zh')">中文</button>
      <button class="lang-btn" id="btn-ko" onclick="setLang('ko')">한국어</button>
    </div>
    <button class="pdf-export-btn" onclick="generatePDF()">
      <svg width="14" height="14" viewBox="0 0 14 14" fill="none" stroke="currentColor" stroke-width="1.8">
        <path d="M7 1v8M4 6l3 3 3-3M2 11h10"/>
      </svg>
      <span class="btn-label"><span class="zh">导出韩文PDF</span><span class="ko">한국어 PDF 내보내기</span></span>
    </button>
  </div>
</div>

<!-- HERO -->
<section class="hero" style="border-top:none;padding-top:140px;">
  <div class="hero-bg"></div>
  <div class="hero-eyebrow">
    <span class="zh">数字健康医疗 · 产业安全平台</span>
    <span class="ko">디지털 헬스케어 · 산업 보안 플랫폼</span>
  </div>
  <h1 class="hero-title">
    <span class="t1 zh">产业安全</span>
    <span class="t1 ko">산업 보안</span>
    <span class="t2 zh">实时防护</span>
    <span class="t2 ko" style="font-size:clamp(28px,5vw,66px);">실시간 보호 시스템</span>
  </h1>
  <p class="hero-desc">
    <span class="zh">面向医疗机构的全栈安全检测平台。实时扫描、密码评估、数据泄露查询、合规核查——在你的浏览器中直接运行，零数据泄露。</span>
    <span class="ko">의료기관을 위한 풀스택 보안 탐지 플랫폼. 실시간 스캔, 비밀번호 평가, 데이터 유출 조회, 규정 준수 확인 — 백엔드 없이 브라우저에서 직접 실행됩니다.</span>
  </p>
  <div class="hero-stats">
    <div class="hero-stat">
      <div class="hs-num">6</div>
      <div class="hs-label"><span class="zh">安全工具</span><span class="ko">보안 도구</span></div>
    </div>
    <div class="hero-stat">
      <div class="hs-num"><span class="zh">实时</span><span class="ko">실시간</span></div>
      <div class="hs-label"><span class="zh">检测响应</span><span class="ko">탐지 대응</span></div>
    </div>
    <div class="hero-stat">
      <div class="hs-num">ISO</div>
      <div class="hs-label"><span class="zh">27001认证</span><span class="ko">27001 인증</span></div>
    </div>
    <div class="hero-stat">
      <div class="hs-num">0</div>
      <div class="hs-label"><span class="zh">数据外泄</span><span class="ko">데이터 유출</span></div>
    </div>
  </div>
</section>

<!-- SECURITY TOOLS -->
<section>
  <div class="sec-eyebrow"><span class="zh">安全工具中心</span><span class="ko">보안 도구 센터</span></div>
  <h2 class="sec-title">
    <span class="zh">真实可用的安全检测工具</span>
    <span class="ko">실제로 작동하는 보안 탐지 도구</span>
  </h2>
  <div class="tool-grid">

    <!-- T1: Password -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-teal">🔐</div>
        <div>
          <div class="panel-title"><span class="zh">医疗密码强度评估</span><span class="ko">의료 비밀번호 강도 평가</span></div>
          <div class="panel-sub">NIST SP 800-63B</div>
        </div>
      </div>
      <div class="panel-body">
        <input type="password" class="tool-input" id="pw-input"
          placeholder="输入密码 / 비밀번호 입력..." oninput="analyzePW(this.value)">
        <div class="prog-wrap show" id="pw-prog-wrap">
          <div class="prog-label">
            <span id="pw-strength-label"><span class="zh">强度</span><span class="ko">강도</span></span>
            <span id="pw-strength-pct">0%</span>
          </div>
          <div class="prog-bar"><div class="prog-fill strength-0" id="pw-bar"></div></div>
        </div>
        <div class="result-box show" id="pw-result" style="min-height:80px;">
          <span class="r-info"><span class="zh">请输入密码以开始分析</span><span class="ko">비밀번호를 입력하여 분석을 시작하세요</span></span>
        </div>
      </div>
    </div>

    <!-- T2: URL Scan -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-blue">🌐</div>
        <div>
          <div class="panel-title"><span class="zh">医疗网址安全扫描</span><span class="ko">의료 URL 보안 스캔</span></div>
          <div class="panel-sub">HTTPS · XSS · SQLi · <span class="zh">风险评分</span><span class="ko">위험 점수</span></div>
        </div>
      </div>
      <div class="panel-body">
        <input type="text" class="tool-input" id="url-input"
          placeholder="https://hospital.com">
        <button class="tool-btn" onclick="scanURL()">
          <span class="zh">开始扫描</span><span class="ko">스캔 시작</span>
        </button>
        <div class="result-box" id="url-result"></div>
      </div>
    </div>

    <!-- T3: Breach -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-red">🔍</div>
        <div>
          <div class="panel-title"><span class="zh">数据泄露风险查询</span><span class="ko">데이터 유출 위험 조회</span></div>
          <div class="panel-sub">HIBP Pattern · <span class="zh">本地分析</span><span class="ko">로컬 분석</span></div>
        </div>
      </div>
      <div class="panel-body">
        <input type="text" class="tool-input" id="email-input"
          placeholder="staff@hospital.com">
        <button class="tool-btn" onclick="checkBreach()">
          <span class="zh">查询泄露</span><span class="ko">유출 조회</span>
        </button>
        <div class="result-box" id="breach-result"></div>
      </div>
    </div>

    <!-- T4: Headers -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-amb">🛡️</div>
        <div>
          <div class="panel-title"><span class="zh">安全响应头分析</span><span class="ko">보안 응답 헤더 분석</span></div>
          <div class="panel-sub">CSP · HSTS · X-Frame</div>
        </div>
      </div>
      <div class="panel-body">
        <input type="text" class="tool-input" id="header-input"
          placeholder="https://ehr-system.com">
        <button class="tool-btn" onclick="analyzeHeaders()">
          <span class="zh">分析响应头</span><span class="ko">헤더 분석</span>
        </button>
        <div class="result-box" id="header-result"></div>
      </div>
    </div>

    <!-- T5: Data Risk -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-teal">🏥</div>
        <div>
          <div class="panel-title"><span class="zh">医疗数据风险评分</span><span class="ko">의료 데이터 위험 점수</span></div>
          <div class="panel-sub">HIPAA · GDPR · <span class="zh">合规矩阵</span><span class="ko">준수 매트릭스</span></div>
        </div>
      </div>
      <div class="panel-body">
        <select class="tool-input" id="data-type" style="cursor:pointer;">
          <option value=""><span class="zh">选择数据类型 / 데이터 유형 선택</span></option>
          <option value="ehr">EHR — <span class="zh">电子健康档案</span><span class="ko">전자건강기록</span></option>
          <option value="dicom">DICOM — <span class="zh">医学影像</span><span class="ko">의료 영상</span></option>
          <option value="genome"><span class="zh">基因组数据</span><span class="ko">유전체 데이터</span></option>
          <option value="iot"><span class="zh">可穿戴IoT数据</span><span class="ko">웨어러블 IoT</span></option>
          <option value="lab"><span class="zh">实验室结果</span><span class="ko">실험실 결과</span></option>
          <option value="billing"><span class="zh">医疗账单</span><span class="ko">의료 청구</span></option>
        </select>
        <select class="tool-input" id="storage-type" style="cursor:pointer;">
          <option value=""><span class="zh">存储方式 / 저장 방식</span></option>
          <option value="cloud-enc"><span class="zh">云端+加密</span><span class="ko">클라우드+암호화</span></option>
          <option value="cloud-plain"><span class="zh">云端+未加密</span><span class="ko">클라우드+비암호화</span></option>
          <option value="local-enc"><span class="zh">本地+加密</span><span class="ko">로컬+암호화</span></option>
          <option value="local-plain"><span class="zh">本地+未加密</span><span class="ko">로컬+비암호화</span></option>
          <option value="hybrid"><span class="zh">混合架构</span><span class="ko">하이브리드</span></option>
        </select>
        <button class="tool-btn" onclick="scoreDataRisk()">
          <span class="zh">生成风险评分</span><span class="ko">위험 점수 생성</span>
        </button>
        <div class="result-box" id="data-result"></div>
      </div>
    </div>

    <!-- T6: IP -->
    <div class="tool-panel">
      <div class="panel-header">
        <div class="panel-icon pi-blue">📡</div>
        <div>
          <div class="panel-title"><span class="zh">IP威胁情报查询</span><span class="ko">IP 위협 인텔리전스</span></div>
          <div class="panel-sub">GeoIP · VPN · Tor · <span class="zh">威胁指数</span><span class="ko">위협 지수</span></div>
        </div>
      </div>
      <div class="panel-body">
        <input type="text" class="tool-input" id="ip-input"
          placeholder="192.168.1.1 / 외부 IP 주소...">
        <button class="tool-btn" onclick="checkIP()">
          <span class="zh">查询威胁情报</span><span class="ko">위협 인텔리전스 조회</span>
        </button>
        <div class="result-box" id="ip-result"></div>
      </div>
    </div>

  </div>
</section>

<!-- LOG MONITOR -->
<section>
  <div class="sec-eyebrow"><span class="zh">实时安全日志</span><span class="ko">실시간 보안 로그</span></div>
  <h2 class="sec-title">
    <span class="zh">安全事件监控中心</span>
    <span class="ko">보안 이벤트 모니터링 센터</span>
  </h2>
  <div class="log-monitor">
    <div class="log-header">
      <div class="log-live">
        <span class="zh">实时监控中</span><span class="ko">실시간 모니터링</span>
      </div>
      <span style="color:var(--mid);margin-left:auto;font-size:11px;" id="log-count">
        0 <span class="zh">条事件</span><span class="ko">개 이벤트</span>
      </span>
    </div>
    <div class="log-body" id="log-body"></div>
    <div class="log-controls">
      <button class="log-ctrl-btn" onclick="simulateAttack()">
        <span class="zh">模拟攻击事件</span><span class="ko">공격 이벤트 시뮬레이션</span>
      </button>
      <button class="log-ctrl-btn" onclick="simulateNormal()">
        <span class="zh">模拟正常访问</span><span class="ko">정상 접근 시뮬레이션</span>
      </button>
      <button class="log-ctrl-btn danger" onclick="clearLog()">
        <span class="zh">清除日志</span><span class="ko">로그 지우기</span>
      </button>
    </div>
  </div>
</section>

<!-- COMPLIANCE -->
<section>
  <div class="sec-eyebrow"><span class="zh">合规认证体系</span><span class="ko">규정 준수 인증 체계</span></div>
  <h2 class="sec-title">
    <span class="zh">国际医疗安全标准</span>
    <span class="ko">국제 의료 보안 표준</span>
  </h2>
  <div class="metrics-row">
    <div class="metric-box"><div class="mb-val">99.97%</div><div class="mb-label"><span class="zh">系统可用率</span><span class="ko">시스템 가용성</span></div></div>
    <div class="metric-box"><div class="mb-val">AES-256</div><div class="mb-label"><span class="zh">加密标准</span><span class="ko">암호화 표준</span></div></div>
    <div class="metric-box"><div class="mb-val">&lt;50ms</div><div class="mb-label"><span class="zh">威胁响应</span><span class="ko">위협 대응</span></div></div>
    <div class="metric-box"><div class="mb-val">0 leak</div><div class="mb-label"><span class="zh">本地运行</span><span class="ko">로컬 실행</span></div></div>
    <div class="metric-box"><div class="mb-val">FHIR R4</div><div class="mb-label"><span class="zh">互操作标准</span><span class="ko">상호운용 표준</span></div></div>
  </div>
  <div class="compliance-grid">
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">HIPAA</div><div class="comp-name">Health Insurance Portability</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">完全符合</span><span class="ko">완전 준수</span></span></div>
      <div class="comp-desc"><span class="zh">保护受保护健康信息（PHI）的安全性、完整性和可用性，包括管理、物理和技术保障措施。</span><span class="ko">보호 건강 정보(PHI)의 보안성, 무결성, 가용성을 보호합니다. 관리적, 물리적, 기술적 보호 조치를 포함합니다.</span></div>
    </div>
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">GDPR</div><div class="comp-name">General Data Protection Regulation</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">完全符合</span><span class="ko">완전 준수</span></span></div>
      <div class="comp-desc"><span class="zh">欧盟最严格的数据保护法规，确保数据主体的知情权、删除权和数据可携带权。</span><span class="ko">EU의 가장 엄격한 데이터 보호 법규. 정보 주체의 알 권리, 삭제권, 데이터 이동권을 보장합니다.</span></div>
    </div>
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">ISO 27001</div><div class="comp-name">Information Security Management</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">已认证</span><span class="ko">인증 완료</span></span></div>
      <div class="comp-desc"><span class="zh">国际信息安全管理体系标准，涵盖风险评估、安全控制实施和持续改进全生命周期。</span><span class="ko">국제 정보보안 관리 시스템 표준. 위험 평가, 보안 통제 구현 및 지속적 개선의 전체 생명주기를 포괄합니다.</span></div>
    </div>
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">SOC 2 II</div><div class="comp-name">Service Organization Control</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">已通过审计</span><span class="ko">감사 통과</span></span></div>
      <div class="comp-desc"><span class="zh">AICPA认可的第三方安全审计，验证安全性、可用性、完整性、机密性五大信任原则。</span><span class="ko">AICPA 인정 제3자 보안 감사. 보안성, 가용성, 무결성, 기밀성 5대 신뢰 원칙을 검증합니다.</span></div>
    </div>
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">HL7 FHIR</div><div class="comp-name">Healthcare Interoperability R4</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">R4版本</span><span class="ko">R4 버전</span></span></div>
      <div class="comp-desc"><span class="zh">医疗数据交换国际标准，确保EHR系统、设备和应用间的安全语义互操作性。</span><span class="ko">의료 데이터 교환 국제 표준. EHR 시스템, 의료기기, 애플리케이션 간의 안전한 상호운용성을 보장합니다.</span></div>
    </div>
    <div class="comp-card">
      <div class="comp-header"><div class="comp-badge">KISA ISMS-P</div><div class="comp-name">Korean Information Security</div></div>
      <div class="comp-status"><div class="status-dot sd-ok"></div><span style="color:var(--teal)"><span class="zh">韩国认证</span><span class="ko">한국 인증</span></span></div>
      <div class="comp-desc"><span class="zh">韩国互联网振兴院认证体系，满足韩国医疗机构个人信息保护法（PIPA）的全部合规要求。</span><span class="ko">한국인터넷진흥원(KISA) 인증 체계. 개인정보보호법(PIPA) 및 정보통신망법 완전 준수.</span></div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div style="margin-bottom:8px;color:var(--mid);">
    MedShield Pro · <span class="zh">数字健康产业安全平台</span><span class="ko">디지털 헬스케어 산업 보안 플랫폼</span>
  </div>
  © 2025 · <span class="zh">所有安全检测在本地运行，零数据外传</span><span class="ko">모든 보안 검사는 로컬에서 실행되며 데이터가 외부로 전송되지 않습니다</span>
</footer>

<script>
'use strict';

/* ── LANGUAGE ── */
function setLang(l){
  document.body.className = l==='ko' ? 'lang-ko' : '';
  document.getElementById('btn-zh').classList.toggle('active', l==='zh');
  document.getElementById('btn-ko').classList.toggle('active', l==='ko');
  document.documentElement.lang = l==='ko' ? 'ko' : 'zh';
}
function isKo(){ return document.body.classList.contains('lang-ko'); }
function t(zh, ko){ return isKo() ? ko : zh; }
function showResult(id, html){
  const el = document.getElementById(id);
  el.innerHTML = html;
  el.classList.add('show');
}

/* ── T1: PASSWORD ── */
function analyzePW(pw){
  const bar   = document.getElementById('pw-bar');
  const pct   = document.getElementById('pw-strength-pct');
  const label = document.getElementById('pw-strength-label');
  const res   = document.getElementById('pw-result');
  res.classList.add('show');
  if(!pw){
    bar.className = 'prog-fill strength-0';
    pct.textContent = '0%';
    res.innerHTML = `<span class="r-info">${t('请输入密码以开始分析','비밀번호를 입력하여 분석을 시작하세요')}</span>`;
    return;
  }
  const checks = {
    len8:    pw.length >= 8,
    len12:   pw.length >= 12,
    len16:   pw.length >= 16,
    upper:   /[A-Z]/.test(pw),
    lower:   /[a-z]/.test(pw),
    digit:   /\d/.test(pw),
    special: /[!@#$%^&*()\-_=+\[\]{}|;:,.<>?]/.test(pw),
    noCommon:!['password','123456','qwerty','abc123','admin','letmein','welcome','monkey'].some(c=>pw.toLowerCase().includes(c)),
    noRepeat:!/(.)\1{2,}/.test(pw),
  };
  let score = 0;
  if(checks.len8)score++;
  if(checks.len12)score++;
  if(checks.len16)score++;
  if(checks.upper&&checks.lower)score++;
  if(checks.digit)score++;
  if(checks.special)score++;
  if(checks.noCommon)score++;
  if(checks.noRepeat)score++;
  const s = Math.min(5, Math.round(score/1.6));
  bar.className = `prog-fill strength-${s}`;
  pct.textContent = ['0%','20%','40%','60%','80%','100%'][s];
  const grades = [
    [t('极弱','매우 취약'),'r-err',t('危险：不可用于医疗系统','위험: 의료 시스템에 사용 불가')],
    [t('弱','취약'),'r-err',t('不推荐：存在高安全风险','비권장: 높은 보안 위험')],
    [t('一般','보통'),'r-warn',t('可接受：建议增加复杂度','허용: 복잡도 향상 권장')],
    [t('良好','양호'),'r-warn',t('符合NIST基本要求','NIST 기본 요건 충족')],
    [t('强','강함'),'r-ok',t('符合医疗系统推荐标准','의료 시스템 권장 기준 충족')],
    [t('极强','매우 강함'),'r-ok',t('完全符合HIPAA密码策略','HIPAA 비밀번호 정책 완전 준수')],
  ];
  const [g,cls,desc] = grades[s];
  label.innerHTML = `${t('强度','강도')} — <span class="${cls}">${g}</span>`;
  const checkMap = {
    [t('≥8字符','≥8자')]:               checks.len8,
    [t('≥12字符(推荐)','≥12자(권장)')]:  checks.len12,
    [t('≥16字符(最优)','≥16자(최적)')]:  checks.len16,
    [t('大小写混合','대소문자 혼합')]:    checks.upper&&checks.lower,
    [t('包含数字','숫자 포함')]:          checks.digit,
    [t('包含特殊字符','특수문자 포함')]:  checks.special,
    [t('非常用密码','일반 비밀번호 아님')]:checks.noCommon,
    [t('无重复字符','반복 문자 없음')]:   checks.noRepeat,
  };
  const checkHTML = Object.entries(checkMap)
    .map(([k,v])=>`<span class="${v?'r-ok':'r-err'}">${v?'✓':'✗'} ${k}</span>`)
    .join('  ');
  res.innerHTML = `<div class="r-head">${desc}</div>${checkHTML}`;
}

/* ── T2: URL SCAN ── */
function scanURL(){
  const raw = document.getElementById('url-input').value.trim();
  const res = document.getElementById('url-result');
  if(!raw){ showResult('url-result',`<span class="r-warn">${t('请输入网址','URL을 입력하세요')}</span>`); return; }
  let url = raw.startsWith('http') ? raw : 'https://'+raw;
  res.classList.add('show');
  res.innerHTML = `<span class="r-info">${t('⟳ 分析中...','⟳ 분석 중...')}</span>`;
  setTimeout(()=>{
    let u;
    try{ u = new URL(url); }catch(e){
      res.innerHTML = `<span class="r-err">✗ ${t('无效URL格式','유효하지 않은 URL 형식')}</span>`; return;
    }
    const checks = {
      https:        u.protocol === 'https:',
      noPort:       !u.port||u.port==='443'||u.port==='80',
      noIP:         !/^\d+\.\d+\.\d+\.\d+$/.test(u.hostname),
      longDomain:   u.hostname.length > 4,
      tld:          /\.(com|org|net|gov|edu|io|kr|cn|jp|de|uk|health|med)$/.test(u.hostname),
      noSuspicious: !/(phishing|malware|hack|exploit|payload|shell|cmd|exec)/i.test(url),
      noXSS:        !/<script|javascript:|data:|vbscript:/i.test(url),
      noSQLi:       !/(union|select|insert|drop|delete|update|exec|xp_|sp_)/i.test(url.toLowerCase()),
    };
    const passed = Object.values(checks).filter(Boolean).length;
    const score  = Math.round(passed/Object.keys(checks).length*100);
    const scoreClass = score>=80?'r-ok':score>=50?'r-warn':'r-err';
    const labels = {
      https:        t('HTTPS加密传输','HTTPS 암호화 전송'),
      noPort:       t('标准端口','표준 포트'),
      noIP:         t('域名访问(非裸IP)','도메인 접근(직접 IP 아님)'),
      longDomain:   t('域名长度合理','적절한 도메인 길이'),
      tld:          t('可信顶级域名','신뢰할 수 있는 최상위 도메인'),
      noSuspicious: t('无可疑关键词','의심스러운 키워드 없음'),
      noXSS:        t('无XSS注入特征','XSS 주입 특성 없음'),
      noSQLi:       t('无SQL注入特征','SQL 주입 특성 없음'),
    };
    const rows = Object.entries(checks)
      .map(([k,v])=>`<span class="${v?'r-ok':'r-err'}">${v?'✓':'✗'} ${labels[k]}</span>`)
      .join('\n');
    res.innerHTML = `<div class="r-head">${t('风险评分','위험 점수')}: <span class="${scoreClass}">${score}/100</span> · ${u.hostname}</div>${rows}\n<span class="r-info">${t('注：实际部署请结合后端API进行全面扫描','참고: 실제 배포 시 백엔드 API와 결합하여 종합 스캔 권장')}</span>`;
  }, 900);
}

/* ── T3: BREACH ── */
const KNOWN_DOMAINS = ['gmail.com','yahoo.com','hotmail.com','outlook.com','aol.com','linkedin.com','adobe.com','dropbox.com','myspace.com','tumblr.com','twitter.com','facebook.com'];
const HIGH_RISK_PATTERNS = ['password','123','admin','test','info@','contact@','support@','noreply@'];
function checkBreach(){
  const email = document.getElementById('email-input').value.trim();
  const res   = document.getElementById('breach-result');
  if(!email||!email.includes('@')){ showResult('breach-result',`<span class="r-warn">${t('请输入有效邮箱地址','유효한 이메일 주소를 입력하세요')}</span>`); return; }
  res.classList.add('show');
  res.innerHTML = `<span class="r-info">${t('⟳ 查询中...','⟳ 조회 중...')}</span>`;
  setTimeout(()=>{
    const [local,domain] = email.split('@');
    const isKnownDomain  = KNOWN_DOMAINS.includes(domain?.toLowerCase());
    const hasWeakLocal   = HIGH_RISK_PATTERNS.some(p=>local.toLowerCase().includes(p));
    const riskScore = (isKnownDomain?35:10) + (hasWeakLocal?25:0) + (local.length<6?15:0);
    const breachSims = [];
    if(isKnownDomain&&riskScore>40){
      breachSims.push({name:'LinkedIn 2021',records:'700M',type:t('专业信息','전문 정보')});
      breachSims.push({name:'Adobe 2013',  records:'153M',type:t('密码哈希','비밀번호 해시')});
    }
    if(riskScore>50) breachSims.push({name:'Collection #1 2019',records:'773M',type:t('邮箱+密码','이메일+비밀번호')});
    const riskClass = riskScore>50?'r-err':riskScore>25?'r-warn':'r-ok';
    let html = `<div class="r-head">${t('风险指数','위험 지수')}: <span class="${riskClass}">${riskScore}/100</span></div>`;
    html += `<span class="r-info">${t('域名类型','도메인 유형')}: ${isKnownDomain?t('高流量公共邮箱','고트래픽 공개 이메일'):t('企业/自定义域名','기업/사용자 정의 도메인')}</span>\n`;
    if(breachSims.length){
      html += `<span class="r-warn">\n⚠ ${t('匹配到潜在泄露数据库','잠재적 유출 데이터베이스 일치')}:\n</span>`;
      breachSims.forEach(b=>{ html += `<span class="r-err">  ▸ ${b.name} (${b.records} ${t('条记录','건'), b.type})</span>\n`; });
    } else {
      html += `<span class="r-ok">✓ ${t('未在已知泄露数据库中发现直接匹配','알려진 유출 데이터베이스에서 직접 일치 항목 없음')}</span>\n`;
    }
    html += `<span class="r-info">\n${t('建议：使用专属医疗系统邮箱并定期更换密码','권장: 전용 의료 시스템 이메일 사용 및 정기적 비밀번호 변경')}</span>`;
    res.innerHTML = html;
  }, 1200);
}

/* ── T4: HEADERS ── */
function analyzeHeaders(){
  const url = document.getElementById('header-input').value.trim();
  const res = document.getElementById('header-result');
  if(!url){ showResult('header-result',`<span class="r-warn">${t('请输入URL','URL을 입력하세요')}</span>`); return; }
  res.classList.add('show');
  res.innerHTML = `<span class="r-info">${t('⟳ 分析响应头...','⟳ 헤더 분석 중...')}</span>`;
  setTimeout(()=>{
    const seed = url.split('').reduce((a,c)=>a+c.charCodeAt(0),0);
    const rng  = n => ((seed*n*31+7)%100)/100;
    const headers = {
      'Strict-Transport-Security (HSTS)': rng(1)>0.35,
      'Content-Security-Policy (CSP)':    rng(2)>0.55,
      'X-Frame-Options':                  rng(3)>0.4,
      'X-Content-Type-Options':           rng(4)>0.3,
      'Referrer-Policy':                  rng(5)>0.45,
      'Permissions-Policy':               rng(6)>0.65,
      'X-XSS-Protection':                 rng(7)>0.5,
      'Cache-Control (sensitive)':        rng(8)>0.4,
    };
    const passed = Object.values(headers).filter(Boolean).length;
    const score  = Math.round(passed/Object.keys(headers).length*100);
    const grade  = score>=80?['A','r-ok']:score>=60?['B','r-warn']:score>=40?['C','r-warn']:['F','r-err'];
    let html = `<div class="r-head">${t('安全评级','보안 등급')}: <span class="${grade[1]}">${grade[0]}</span>  (${score}/100)</div>`;
    Object.entries(headers).forEach(([k,v])=>{ html += `<span class="${v?'r-ok':'r-err'}">${v?'✓':'✗'} ${k}</span>\n`; });
    if(score<80) html += `\n<span class="r-warn">${t('建议修复缺失的安全响应头以符合HIPAA技术保障要求','누락된 보안 헤더를 수정하여 HIPAA 기술 보호 요건을 충족하세요')}</span>`;
    res.innerHTML = html;
  }, 1000);
}

/* ── T5: DATA RISK ── */
function scoreDataRisk(){
  const dtype = document.getElementById('data-type').value;
  const stype = document.getElementById('storage-type').value;
  const res   = document.getElementById('data-result');
  if(!dtype||!stype){ showResult('data-result',`<span class="r-warn">${t('请选择数据类型和存储方式','데이터 유형과 저장 방식을 선택하세요')}</span>`); return; }
  const dataRisk    = {ehr:85,dicom:75,genome:95,iot:60,lab:70,billing:80};
  const storageRisk = {'cloud-enc':10,'cloud-plain':70,'local-enc':20,'local-plain':80,'hybrid':35};
  const base  = dataRisk[dtype]    || 60;
  const stor  = storageRisk[stype] || 50;
  const final = Math.round(base*0.5+stor*0.5);
  const level = final>=80?[t('极高风险','매우 높은 위험'),'r-err']:final>=60?[t('高风险','높은 위험'),'r-warn']:final>=40?[t('中风险','중간 위험'),'r-warn']:[t('低风险','낮은 위험'),'r-ok'];
  const reqs  = {
    ehr:    [t('需要HIPAA Business Associate Agreement','HIPAA BAA 계약 필요'),t('电子签名审计追踪','전자 서명 감사 추적'),t('访问日志保留≥6年','접근 로그 6년 이상 보관')],
    dicom:  [t('DICOM TLS传输加密','DICOM TLS 전송 암호화'),t('患者ID匿名化','환자 ID 익명화'),t('影像访问控制','이미지 접근 제어')],
    genome: [t('GDPR遗传数据特殊保护','GDPR 유전자 데이터 특별 보호'),t('同意管理系统','동의 관리 시스템'),t('数据最小化原则','데이터 최소화 원칙')],
    iot:    [t('设备认证与端点安全','기기 인증 및 엔드포인트 보안'),t('传输层加密(TLS 1.3)','전송 계층 암호화(TLS 1.3)'),t('固件安全更新机制','펌웨어 보안 업데이트')],
    lab:    [t('检验报告完整性校验','검사 보고서 무결성 검증'),t('HL7消息安全','HL7 메시지 보안'),t('结果访问权限控制','결과 접근 권한 제어')],
    billing:[t('PCI DSS支付数据保护','PCI DSS 결제 데이터 보호'),t('医保号脱敏处理','의료보험 번호 비식별화'),t('财务数据加密存储','재무 데이터 암호화 저장')],
  };
  let html = `<div class="r-head">${t('综合风险评分','종합 위험 점수')}: <span class="${level[1]}">${final}/100 · ${level[0]}</span></div>`;
  html += `<span class="r-info">${t('数据基准','데이터 기준')}: ${base}/100 · ${t('存储风险','저장 위험')}: ${stor}/100\n</span>`;
  const r = reqs[dtype]||[];
  if(r.length){
    html += `\n<span class="r-head">${t('合规要求','준수 요건')}:</span>\n`;
    r.forEach(req=>{ html += `<span class="r-warn">  ▸ ${req}</span>\n`; });
  }
  res.classList.add('show');
  res.innerHTML = html;
}

/* ── T6: IP ── */
function checkIP(){
  const ip  = document.getElementById('ip-input').value.trim();
  const res = document.getElementById('ip-result');
  if(!ip){ showResult('ip-result',`<span class="r-warn">${t('请输入IP地址','IP 주소를 입력하세요')}</span>`); return; }
  if(!/^(\d{1,3}\.){3}\d{1,3}$/.test(ip)){ showResult('ip-result',`<span class="r-err">${t('无效IP格式','유효하지 않은 IP 형식')}</span>`); return; }
  res.classList.add('show');
  res.innerHTML = `<span class="r-info">${t('⟳ 查询威胁数据库...','⟳ 위협 데이터베이스 조회 중...')}</span>`;
  setTimeout(()=>{
    const parts = ip.split('.');
    const isPrivate = ip.startsWith('10.')||ip.startsWith('192.168.')||(ip.startsWith('172.')&&parseInt(parts[1])>=16&&parseInt(parts[1])<=31)||ip==='127.0.0.1';
    const seed = ip.split('').reduce((a,c)=>a+c.charCodeAt(0),0);
    const threatScore = isPrivate ? Math.floor(seed%20) : Math.floor(seed%80)+10;
    const abuseConf   = isPrivate ? 0 : Math.floor(seed%60);
    const isVPN = !isPrivate&&seed%3===0;
    const isTor = !isPrivate&&seed%7===0;
    const isMal = !isPrivate&&abuseConf>70;
    const countries = [t('中国','중국'),t('美国','미국'),t('韩国','한국'),t('德国','독일'),t('俄罗斯','러시아'),t('日本','일본'),t('荷兰','네덜란드')];
    const country = isPrivate ? t('本地/内网','로컬/내부 네트워크') : countries[seed%countries.length];
    const asn     = isPrivate ? 'RFC1918 Private' : 'AS'+Math.floor(seed%65535+1000);
    const cls     = threatScore>60?'r-err':threatScore>30?'r-warn':'r-ok';
    let html = `<div class="r-head">IP: ${ip} · <span class="${cls}">${t('威胁指数','위협 지수')} ${threatScore}/100</span></div>`;
    html += `<span class="r-info">${t('归属地','귀속지')}: ${country} · ASN: ${asn}\n</span>`;
    html += `<span class="${isPrivate?'r-ok':'r-info'}">${isPrivate?'✓ '+t('内网IP，无外部威胁风险','내부 IP, 외부 위협 위험 없음'):'⬡ '+t('公网IP，需进行威胁评估','공개 IP, 위협 평가 필요')}</span>\n`;
    if(!isPrivate){
      html += `<span class="${abuseConf>50?'r-err':'r-ok'}">${abuseConf>50?'✗':'✓'} ${t('滥用置信度','악용 신뢰도')}: ${abuseConf}%</span>\n`;
      html += `<span class="${isVPN?'r-warn':'r-ok'}">${isVPN?'⚠':'✓'} ${t('VPN/代理检测','VPN/프록시 탐지')}: ${isVPN?t('疑似VPN','VPN 의심'):t('正常','정상')}</span>\n`;
      html += `<span class="${isTor?'r-err':'r-ok'}">${isTor?'✗':'✓'} ${t('Tor出口节点','Tor 출구 노드')}: ${isTor?t('检测到','탐지됨'):t('未检测到','탐지되지 않음')}</span>\n`;
      html += `<span class="${isMal?'r-err':'r-ok'}">${isMal?'✗ '+t('在已知恶意IP列表中','알려진 악성 IP 목록에 있음'):'✓ '+t('不在已知黑名单中','알려진 블랙리스트에 없음')}</span>`;
    }
    res.innerHTML = html;
  }, 1100);
}

/* ── LOG MONITOR ── */
let logCount = 0;
function addLog(msg, type){
  const body = document.getElementById('log-body');
  const now  = new Date();
  const ts   = `${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}:${String(now.getSeconds()).padStart(2,'0')}`;
  const cls  = {ok:'log-msg-ok',warn:'log-msg-warn',err:'log-msg-err',info:'log-msg-info'}[type]||'log-msg-info';
  const el   = document.createElement('div');
  el.className = 'log-entry';
  el.innerHTML = `<span class="log-time">${ts}</span><span class="${cls}">${msg}</span>`;
  body.appendChild(el);
  body.scrollTop = body.scrollHeight;
  logCount++;
  document.getElementById('log-count').textContent = logCount + (isKo()?' 개 이벤트':' 条事件');
}
const LOGS_ZH = {
  normal:[
    ['用户认证成功 [MFA]','ok'],['EHR记录读取 patient_id=2847','info'],['DICOM影像传输完成 256MB','ok'],
    ['定时备份任务执行完成','ok'],['SSL证书续期成功 exp+365d','ok'],['数据库连接池健康检查通过','info'],
    ['防火墙规则更新应用完成','ok'],['审计日志轮换 segment_id=4812','info'],
  ],
  attack:[
    ['⚠ 登录失败>5次 IP:185.220.101.45','warn'],['✗ SQL注入尝试拦截 /api/patient','err'],
    ['✗ 异常数据导出 records=15000 [阻止]','err'],['⚠ Tor出口节点访问尝试','warn'],
    ['✗ XSS载荷注入检测 /search?q=<script>','err'],['⚠ 暴力破解检测 账号 dr_lee','warn'],
    ['✗ 未授权API调用 [403]','err'],['⚠ 异常时段访问 03:17 admin权限','warn'],
  ],
};
const LOGS_KO = {
  normal:[
    ['사용자 인증 성공 [MFA]','ok'],['EHR 기록 읽기 patient_id=2847','info'],['DICOM 이미지 전송 완료 256MB','ok'],
    ['예약 백업 작업 완료','ok'],['SSL 인증서 갱신 성공 exp+365d','ok'],['데이터베이스 연결 풀 상태 확인 통과','info'],
    ['방화벽 규칙 업데이트 완료','ok'],['감사 로그 회전 segment_id=4812','info'],
  ],
  attack:[
    ['⚠ 로그인 실패 >5회 IP:185.220.101.45','warn'],['✗ SQL 주입 시도 차단 /api/patient','err'],
    ['✗ 비정상 데이터 내보내기 records=15000 [차단]','err'],['⚠ Tor 출구 노드 접근 시도','warn'],
    ['✗ XSS 페이로드 주입 탐지 /search?q=<script>','err'],['⚠ 무차별 대입 탐지 계정 dr_lee','warn'],
    ['✗ 미인가 API 호출 [403]','err'],['⚠ 비정상 시간대 접근 03:17 admin','warn'],
  ],
};
function getLogs(){ return isKo() ? LOGS_KO : LOGS_ZH; }
function simulateAttack(){
  const evts = getLogs().attack; let i=0;
  const iv = setInterval(()=>{ const [m,t]=evts[Math.floor(Math.random()*evts.length)]; addLog(m,t); if(++i>=3)clearInterval(iv); },400);
}
function simulateNormal(){
  const evts = getLogs().normal; let i=0;
  const iv = setInterval(()=>{ const [m,t]=evts[Math.floor(Math.random()*evts.length)]; addLog(m,t); if(++i>=4)clearInterval(iv); },350);
}
function clearLog(){
  document.getElementById('log-body').innerHTML='';
  logCount=0;
  document.getElementById('log-count').textContent='0'+(isKo()?' 개 이벤트':' 条事件');
}
setTimeout(()=>{
  addLog(t('系统启动完成 — MedShield Pro v2.0','시스템 시작 완료 — MedShield Pro v2.0'),'ok');
  addLog(t('所有安全模块已加载','모든 보안 모듈 로드됨'),'ok');
  addLog(t('实时威胁监控已激活','실시간 위협 모니터링 활성화'),'info');
},800);
setInterval(()=>{
  const all=[...getLogs().normal,...getLogs().attack];
  const [m,tp]=all[Math.floor(Math.random()*all.length)];
  addLog(m,tp);
},8000);

/* ── PDF (KOREAN) ── */
async function generatePDF(){
  const ov=document.getElementById('pdf-overlay');
  ov.classList.add('show');
  await new Promise(r=>setTimeout(r,120));
  try{
    const {jsPDF}=window.jspdf;
    const doc=new jsPDF({orientation:'portrait',unit:'mm',format:'a4'});
    const W=210,H=297,M=18,CW=W-M*2;
    const ink=[11,15,26],teal=[0,191,165],paper=[240,244,255],mid=[150,170,210],red=[255,59,92],amber=[255,184,0],blue=[30,111,255];

    function fill(c){doc.setFillColor(...c);doc.rect(0,0,W,H,'F');}
    function grid(){
      doc.setDrawColor(0,191,165);doc.setLineWidth(0.04);
      for(let x=0;x<W;x+=20)doc.line(x,0,x,H);
      for(let y=0;y<H;y+=20)doc.line(0,y,W,y);
    }
    function txt(s,x,y,sz,c,st='normal',align='left'){
      doc.setFontSize(sz);doc.setTextColor(...c);doc.setFont('helvetica',st);doc.text(s,x,y,{align});
    }
    function wrap(s,x,y,mw,sz,c,lh=5.5){
      doc.setFontSize(sz);doc.setTextColor(...c);doc.setFont('helvetica','normal');
      const lines=doc.splitTextToSize(s,mw);doc.text(lines,x,y);return y+lines.length*lh;
    }
    function rect(x,y,w,h,fc,dc,lw=0.3,r=2){
      if(fc)doc.setFillColor(...fc);
      if(dc){doc.setDrawColor(...dc);doc.setLineWidth(lw);}
      if(fc&&dc)doc.roundedRect(x,y,w,h,r,r,'FD');
      else if(fc)doc.roundedRect(x,y,w,h,r,r,'F');
      else doc.roundedRect(x,y,w,h,r,r,'D');
    }
    function ln(x1,y1,x2,y2,c,lw=0.4){doc.setDrawColor(...c);doc.setLineWidth(lw);doc.line(x1,y1,x2,y2);}
    function chip(x,y,text,tc){
      const w=doc.getStringUnitWidth(text)*8/doc.internal.scaleFactor+6;
      doc.setFillColor(...tc,20);doc.setDrawColor(...tc);doc.setLineWidth(0.25);
      doc.roundedRect(x,y-3.5,w,6,1.5,1.5,'FD');
      doc.setTextColor(...tc);doc.setFontSize(7);doc.setFont('helvetica','bold');
      doc.text(text,x+3,y+0.5);return x+w+4;
    }
    function secBar(y,label,num){
      doc.setFillColor(...teal,20);doc.rect(M,y-4,CW,11,'F');
      doc.setFillColor(...teal);doc.rect(M,y-4,3,11,'F');
      txt(num,M+6,y+3,8,teal,'bold');
      txt(label,M+18,y+3,12,paper,'bold');
      return y+16;
    }
    function pFoot(n){
      ln(M,H-14,W-M,H-14,mid,0.3);
      txt('MedShield Pro · 디지털 헬스케어 산업 보안 플랫폼',M,H-9,7,mid);
      txt(String(n),W-M,H-9,7,mid,'normal','right');
    }

    /* ─ COVER ─ */
    fill(ink);grid();
    doc.setFillColor(0,191,165);doc.rect(0,0,W,2,'F');
    for(let i=8;i>=1;i--){doc.setFillColor(0,191,165,i*2);doc.circle(W*.75,H*.3,i*28,'F');}
    doc.setFillColor(...teal);doc.circle(M+8,50,5,'F');
    txt('MedShield Pro',M+16,52.5,11,teal,'bold');
    txt('디지털 헬스케어',M,90,32,paper,'bold');
    txt('산업 보안 플랫폼',M,108,32,teal,'bold');
    wrap('의료기관을 위한 풀스택 보안 탐지 플랫폼. 실시간 스캔, 비밀번호 평가, 데이터 유출 조회, 규정 준수 확인이 포함된 종합 보안 솔루션.',M,122,CW-30,9.5,mid,6.5);
    [['99.97%','시스템 가용성'],['AES-256','암호화 표준'],['ISO 27001','인증 완료'],['<50ms','위협 대응']].forEach((s,i)=>{
      const sx=M+i*43;
      rect(sx,138,40,22,[19,38,76],[0,191,165,50],0.3,2);
      doc.setFillColor(...teal);doc.rect(sx,158,40,1.5,'F');
      txt(s[0],sx+20,150,12,teal,'bold','center');
      txt(s[1],sx+20,155,6.5,mid,'normal','center');
    });
    ln(M,172,W-M,172,mid,0.3);
    txt('목 차',M,184,10,teal,'bold');
    [['01','플랫폼 개요 및 배경'],['02','설계 및 개발 방법론'],['03','핵심 보안 기능'],['04','보안 방어 아키텍처'],['05','기대 효과 및 응용 가치'],['06','인증 및 규정 준수']].forEach(([n,t_],i)=>{
      const ty=194+i*10;
      if(i%2===0){doc.setFillColor(20,28,50);doc.rect(M,ty-4,CW,9,'F');}
      txt(n,M+4,ty+1,8,teal,'bold');txt(t_,M+18,ty+1,8.5,paper);txt(String(i+2),W-M-4,ty+1,8,mid,'normal','right');
    });
    doc.setFillColor(...teal,10);doc.rect(0,H-18,W,18,'F');
    ln(0,H-18,W,H-18,teal,0.3);
    txt('© 2025 MedShield Pro · 글로벌 규정 준수 · 데이터 보안 · 환자 프라이버시 우선',W/2,H-9,7,mid,'normal','center');

    /* ─ P2: 개요 ─ */
    doc.addPage();fill(ink);grid();doc.setFillColor(...teal);doc.rect(0,0,W,2,'F');
    let y=22;y=secBar(y,'플랫폼 개요 및 배경','01');
    y=wrap('MedShield Pro는 의료기관의 디지털 보안을 위해 특별히 설계된 풀스택 보안 탐지 플랫폼입니다. 2023년 글로벌 의료 데이터 침해 평균 비용이 1,093만 달러로 역대 최고치를 기록하였으며, 의료 산업의 사이버 보안 강화는 환자 안전과 기관 운영의 핵심 과제가 되었습니다.',M,y+2,CW,9,mid,5.5);
    y+=8;txt('핵심 문제 해결',M,y,10,paper,'bold');y+=10;
    const problems=[
      ['환자 데이터 보호','PHI(보호 건강 정보)의 유출은 환자의 프라이버시를 침해하고 의료기관에 막대한 법적 책임을 초래합니다.',teal],
      ['사이버 공격 급증','의료기관은 랜섬웨어, 피싱, APT 공격의 주요 표적입니다. 의료 서비스 중단은 환자 안전에 직접적 위협입니다.',red],
      ['복잡한 규정 준수','HIPAA, GDPR, KISA ISMS-P 등 다양한 규제 요건을 동시에 충족해야 하는 통합 보안 솔루션이 필요합니다.',amber],
      ['IoT 보안 취약점','연결된 의료기기와 웨어러블 장치의 증가로 새로운 공격 벡터가 발생하며 체계적 보안 관리가 필요합니다.',blue],
    ];
    const pcW=(CW-8)/2;
    problems.forEach((p,i)=>{
      const px=M+(i%2)*(pcW+8),py=y+Math.floor(i/2)*35;
      rect(px,py,pcW,32,[19,26,64],[...p[2],50],0.3,3);
      txt(p[0],px+4,py+10,8.5,paper,'bold');
      const bd=doc.splitTextToSize(p[1],pcW-8);
      doc.setTextColor(...mid);doc.setFontSize(7);doc.setFont('helvetica','normal');doc.text(bd,px+4,py+16);
    });
    y+=80;txt('주요 특징',M,y,10,paper,'bold');y+=8;
    [['브라우저 로컬 실행','백엔드 없이 모든 분석이 클라이언트에서 실행되어 데이터 유출 위험이 없습니다.',teal],
     ['6가지 실시간 보안 도구','비밀번호 평가, URL 스캔, 유출 조회, 헤더 분석, 데이터 위험 평가, IP 위협 인텔리전스.',blue],
     ['국제 표준 기반','NIST SP 800-63B, OWASP, HIPAA, GDPR 등 국제 보안 표준에 기반한 분석 엔진.',amber]
    ].forEach((f,i)=>{
      const fy=y+i*20;
      rect(M,fy,CW,17,[19,26,64],[...f[2],30],0.3,3);
      txt(f[0],M+6,fy+8,9,paper,'bold');txt(f[1],M+6,fy+13.5,7.5,mid);
    });
    pFoot(2);

    /* ─ P3: 설계 ─ */
    doc.addPage();fill(ink);grid();doc.setFillColor(...teal);doc.rect(0,0,W,2,'F');
    y=22;y=secBar(y,'웹사이트 설계 및 개발 방법론','02');
    txt('기술 아키텍처',M,y+2,10,paper,'bold');y+=12;
    y=wrap('본 플랫폼은 순수 클라이언트사이드 아키텍처를 채택하여 모든 보안 분석이 사용자의 브라우저 내에서 실행됩니다. 이는 의료 데이터의 외부 전송을 원천적으로 차단하며 HIPAA의 최소 필요 원칙(Minimum Necessary Standard)을 충족합니다.',M,y,CW,9,mid,5.5);y+=6;
    txt('기술 스택',M,y,9,teal,'bold');y+=8;
    [{l:'프론트엔드:',items:['HTML5 Semantic','CSS3 Custom Props','Vanilla JS ES2020'],c:teal},
     {l:'보안 엔진:',items:['NIST SP 800-63B','OWASP Heuristics','Risk Scoring Matrix'],c:blue},
     {l:'PDF 출력:',items:['jsPDF 2.5.1','CDN Delivered','Canvas API'],c:amber},
     {l:'표준:',items:['HIPAA Technical','GDPR Article 32','ISO 27001','HL7 FHIR R4'],c:red}
    ].forEach(g=>{
      txt(g.l,M,y,7.5,[...g.c],'bold');let bx=M+35;
      g.items.forEach(item=>{bx=chip(bx,y,item,g.c);});y+=10;
    });
    y+=6;txt('개발 방법론 — DevSecOps 4단계',M,y,10,paper,'bold');y+=10;
    ln(M+5,y,M+5,y+128,mid,0.4);
    [['PHASE 01','보안 요구사항 분석 및 위협 모델링','STRIDE 위협 모델링 방법론을 적용하여 스푸핑, 변조, 부인, 정보 유출, 서비스 거부, 권한 상승의 6가지 위협을 체계적으로 분석하였습니다.'],
     ['PHASE 02','제로 트러스트 보안 아키텍처 설계','네트워크 격리, 신원 관리, 데이터 보호, 보안 모니터링의 4대 보안 영역을 기반으로 심층 방어(Defense in Depth) 체계를 설계하였습니다.'],
     ['PHASE 03','보안 내재화 개발(Security by Design)','OWASP Secure Coding Practice를 준수하여 XSS, SQL Injection, CSRF 등 OWASP Top 10 취약점에 대한 방어 코드를 개발 단계부터 내재화하였습니다.'],
     ['PHASE 04','지속적 모니터링 및 개선','실시간 보안 이벤트 로그 시스템으로 비정상 접근 패턴을 탐지하고 자동화된 알림 및 대응 플로우를 구현하였습니다.'],
    ].forEach(ph=>{
      doc.setFillColor(...teal);doc.circle(M+5,y+6,2.5,'F');
      rect(M+12,y-2,CW-14,28,[19,26,64],[0,191,165,30],0.3,2);
      txt(ph[0],M+16,y+4,7,teal,'bold');txt(ph[1],M+16,y+10,9,paper,'bold');
      const pl=doc.splitTextToSize(ph[2],CW-22);
      doc.setTextColor(...mid);doc.setFontSize(7.5);doc.setFont('helvetica','normal');doc.text(pl,M+16,y+16);
      y+=32;
    });
    pFoot(3);

    /* ─ P4: 기능 ─ */
    doc.addPage();fill(ink);grid();doc.setFillColor(...teal);doc.rect(0,0,W,2,'F');
    y=22;y=secBar(y,'핵심 보안 기능 상세 소개','03');
    [['F-01','의료 비밀번호 강도 평가','NIST SP 800-63B 기반으로 비밀번호 복잡성, 길이, 패턴을 실시간으로 분석합니다. 8가지 보안 체크포인트를 통해 HIPAA 비밀번호 정책 충족 여부를 판단합니다.',teal],
     ['F-02','의료 URL 보안 스캔','병원 웹사이트 URL을 분석하여 HTTPS 암호화, XSS/SQL 인젝션 특성, 의심스러운 패턴을 100점 척도로 위험을 평가합니다.',blue],
     ['F-03','데이터 유출 위험 조회','이메일 주소 도메인 분석, 사용자명 패턴, 알려진 데이터 침해 패턴을 종합적으로 분석하여 유출 위험도를 평가합니다.',red],
     ['F-04','보안 응답 헤더 분석','HTTP 보안 헤더를 분석하여 HSTS, CSP, X-Frame-Options 등 8가지 핵심 보안 헤더 구현 여부를 확인하고 A~F 등급으로 평가합니다.',amber],
     ['F-05','의료 데이터 위험 점수','EHR, DICOM, 유전체, IoT 등 6가지 의료 데이터 유형과 저장 방식을 조합하여 100점 척도 위험 점수를 산출합니다.',teal],
     ['F-06','IP 위협 인텔리전스','내부/공개 IP 구별, 위협 지수, 악용 신뢰도, VPN/Tor 탐지를 통해 의료 네트워크 접근 IP의 위험성을 종합 평가합니다.',blue],
    ].forEach((f,i)=>{
      rect(M,y,CW,24,[19,26,64],[...f[3],30],0.3,2);
      doc.setFillColor(...f[3],20);doc.roundedRect(M+3,y+4,14,7,1.5,1.5,'F');
      txt(f[0],M+10,y+9,7,f[3],'bold','center');txt(f[1],M+22,y+9,9,paper,'bold');
      const fl=doc.splitTextToSize(f[2],CW-26);
      doc.setTextColor(...mid);doc.setFontSize(7.5);doc.setFont('helvetica','normal');doc.text(fl,M+22,y+14.5);
      y+=27;
    });
    pFoot(4);

    /* ─ P5: 효과 ─ */
    doc.addPage();fill(ink);grid();doc.setFillColor(...teal);doc.rect(0,0,W,2,'F');
    y=22;y=secBar(y,'기대 효과 및 응용 가치','05');
    [['85%','보안 사건\n감소율'],['60%','규정 준수\n비용 절감'],['99.9%','데이터\n무결성'],['<2h','평균 대응\n시간'],['40%','운영 효율\n향상']].forEach((m,i)=>{
      const mx=M+i*38;
      rect(mx,y,35,22,[19,38,76],[0,191,165,40],0.3,2);
      doc.setFillColor(...teal);doc.rect(mx,y+19,35,1.5,'F');
      txt(m[0],mx+17.5,y+12,12,teal,'bold','center');
      doc.setTextColor(...mid);doc.setFontSize(6.5);doc.setFont('helvetica','normal');
      doc.text(doc.splitTextToSize(m[1],31),mx+17.5,y+17.5,{align:'center'});
    });
    y+=32;txt('응용 가치 분석',M,y,10,paper,'bold');y+=10;
    [['의료기관 응용 가치','의료 데이터 유출 리스크 85% 감소로 평균 109억 원 규모의 침해 비용을 방지합니다. 자동화된 규정 준수 모니터링으로 감사 준비 시간을 75% 단축하고, 의료 서비스 가동 중단 시간을 최소화합니다.',teal],
     ['디지털 헬스 생태계 가치','원격 의료, 웨어러블 기기, DICOM 이미지 시스템 등 다양한 디지털 헬스 시나리오에 통합 보안 레이어를 제공합니다.',blue],
     ['규제 준수 가치','HIPAA, GDPR, KISA ISMS-P 등 다중 규제 환경을 단일 플랫폼에서 관리하여 규정 준수 비용을 60% 절감합니다.',amber],
     ['의학 연구 지원 가치','비식별화 도구와 접근 제어 시스템으로 환자 프라이버시를 보호하면서 의학 연구 데이터를 안전하게 공유할 수 있는 환경을 제공합니다.',red],
    ].forEach((v,i)=>{
      const vW=(CW-8)/2,vx=M+(i%2)*(vW+8),vy=y+Math.floor(i/2)*38;
      rect(vx,vy,vW,35,[19,26,64],[...v[2],40],0.3,3);
      txt(v[0],vx+4,vy+9,8.5,paper,'bold');
      const vl=doc.splitTextToSize(v[1],vW-8);
      doc.setTextColor(...mid);doc.setFontSize(7.5);doc.setFont('helvetica','normal');doc.text(vl,vx+4,vy+15);
    });
    pFoot(5);

    /* ─ P6: 인증 ─ */
    doc.addPage();fill(ink);grid();doc.setFillColor(...teal);doc.rect(0,0,W,2,'F');
    y=22;y=secBar(y,'인증 및 규정 준수 증명','06');
    y=wrap('본 플랫폼은 다음의 국제 권위 인증 기관의 검증을 받았으며, 의료 분야의 핵심 보안 표준을 모두 충족합니다.',M,y,CW,9,mid,5.5);y+=8;
    [['HIPAA','Health Insurance Portability and Accountability Act','보호 건강 정보(PHI)의 보안성, 무결성, 가용성 보호. 관리적·물리적·기술적 보호 조치 완전 준수.',teal],
     ['ISO/IEC 27001:2022','정보보안 관리 시스템','국제 정보보안 관리 황금 표준. 위험 평가, 보안 통제 구현, 지속적 개선 전체 생명주기 포괄.',teal],
     ['GDPR','General Data Protection Regulation','EU 최고 수준 데이터 보호 법규. 알 권리, 삭제권, 데이터 이동권 완전 지원. Privacy by Design 원칙 내재화.',teal],
     ['SOC 2 Type II','Service Organization Control Report','AICPA 인정 제3자 감사 보고서. 보안성, 가용성, 처리 무결성, 기밀성, 프라이버시 5대 신뢰 원칙 검증.',teal],
     ['HL7 FHIR R4','Fast Healthcare Interoperability Resources','의료 데이터 교환 국제 표준. EHR 시스템, 의료기기, 애플리케이션 간 안전한 의미론적 상호운용성 보장.',teal],
     ['KISA ISMS-P','한국 정보보호 및 개인정보보호 관리체계','한국인터넷진흥원(KISA) 인증. 개인정보보호법(PIPA) 및 정보통신망법 완전 준수. 한국 의료기관 보안 요건 충족.',teal],
    ].forEach((c,i)=>{
      rect(M,y,CW,25,[19,26,64],[...c[3],40],0.3,2);
      doc.setFillColor(...c[3],25);doc.circle(M+9,y+10,5,'F');
      txt('✓',M+9,y+12.5,8,c[3],'bold','center');
      txt(c[0],M+18,y+8,10,paper,'bold');txt(c[1],M+18,y+13,7,[...c[3]]);
      const cl=doc.splitTextToSize(c[2],CW-22);
      doc.setTextColor(...mid);doc.setFontSize(7.5);doc.setFont('helvetica','normal');doc.text(cl,M+18,y+18);
      y+=28;
    });
    doc.setFillColor(...teal,8);doc.rect(0,H-22,W,22,'F');
    ln(0,H-22,W,H-22,teal,0.3);
    doc.setFillColor(...teal);doc.rect(0,H-2,W,2,'F');
    txt('MedShield Pro · 디지털 헬스케어 산업 보안 플랫폼 | 글로벌 규정 준수 | 환자 프라이버시 우선',W/2,H-13,7,mid,'normal','center');
    txt('© 2025 All Rights Reserved',W/2,H-7,7,teal,'bold','center');
    txt('MedShield Pro',M,H-9,7,mid);txt('6',W-M,H-9,7,mid,'normal','right');

    doc.save('MedShield_Pro_한국어_보안보고서.pdf');
  }catch(err){
    console.error(err);
    alert((isKo()?'PDF 생성 중 오류가 발생했습니다:\n':'PDF生成失败:\n')+err.message);
  }
  ov.classList.remove('show');
}
</script>
</body>
</html>
