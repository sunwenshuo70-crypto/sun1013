<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
<title>数字健康医疗 · 产业安全 | 디지털 헬스케어 · 산업 보안</title>
<!-- 使用稳定的 html2pdf 库实现 PDF 导出 -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<script>
  window.addEventListener('load', function() {
    if (typeof html2pdf === 'undefined') {
      var fallback = document.createElement('script');
      fallback.src = 'https://unpkg.com/html2pdf.js@0.10.1/dist/html2pdf.bundle.min.js';
      document.head.appendChild(fallback);
    }
  });
</script>
<link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&family=Noto+Sans+KR:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :root {
    --bg-dark: #0A0F1F;
    --bg-card: #111827;
    --accent-cyan: #00E0FF;
    --accent-green: #00FFAA;
    --accent-orange: #FF6B4A;
    --text-white: #F0F4FF;
    --text-dim: #8B9DC3;
    --border-glow: rgba(0,224,255,0.2);
  }

  body {
    background: var(--bg-dark);
    color: var(--text-white);
    font-family: 'Inter', 'Noto Sans KR', sans-serif;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* 语言切换显示控制 */
  .lang-zh { display: block; }
  .lang-ko { display: none; }
  body.lang-ko .lang-zh { display: none; }
  body.lang-ko .lang-ko { display: block; }

  /* 通用容器 */
  .container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 1.5rem;
  }

  /* 头部区域 */
  .hero {
    padding: 80px 0 60px;
    position: relative;
    border-bottom: 1px solid var(--border-glow);
  }
  .hero::before {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    width: 500px;
    height: 500px;
    background: radial-gradient(circle, rgba(0,224,255,0.08) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero-tag {
    display: inline-block;
    font-size: 0.75rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent-cyan);
    border: 1px solid rgba(0,224,255,0.3);
    padding: 0.3rem 1rem;
    border-radius: 40px;
    margin-bottom: 1.5rem;
    background: rgba(0,224,255,0.05);
  }
  h1 {
    font-size: clamp(2.2rem, 6vw, 4rem);
    font-weight: 800;
    line-height: 1.2;
    letter-spacing: -0.02em;
  }
  .gradient-text {
    background: linear-gradient(135deg, #FFFFFF, var(--accent-cyan), var(--accent-green));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
  }
  .hero-sub {
    font-size: 1rem;
    color: var(--text-dim);
    max-width: 600px;
    margin: 1.5rem 0 2rem;
  }

  /* 按钮组 (右侧悬浮) */
  .floating-actions {
    position: fixed;
    bottom: 30px;
    right: 30px;
    z-index: 1000;
    display: flex;
    flex-direction: column;
    gap: 12px;
  }
  .lang-switch {
    display: flex;
    gap: 8px;
    background: rgba(17,24,39,0.85);
    backdrop-filter: blur(8px);
    padding: 6px;
    border-radius: 50px;
    border: 1px solid var(--border-glow);
  }
  .lang-btn {
    background: transparent;
    border: none;
    padding: 6px 18px;
    border-radius: 40px;
    font-size: 0.8rem;
    font-weight: 600;
    cursor: pointer;
    color: var(--text-dim);
    transition: 0.2s;
    font-family: inherit;
  }
  .lang-btn.active {
    background: var(--accent-cyan);
    color: #0A0F1F;
    box-shadow: 0 0 12px rgba(0,224,255,0.4);
  }
  .pdf-download-btn {
    background: linear-gradient(135deg, #0F2B5E, #0A1A3A);
    border: 1px solid var(--accent-cyan);
    border-radius: 48px;
    padding: 12px 24px;
    font-size: 0.85rem;
    font-weight: 700;
    color: var(--accent-cyan);
    display: flex;
    align-items: center;
    gap: 10px;
    cursor: pointer;
    transition: 0.2s;
    backdrop-filter: blur(8px);
    font-family: inherit;
    white-space: nowrap;
  }
  .pdf-download-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 20px rgba(0,224,255,0.3);
    background: linear-gradient(135deg, #1A3F7A, #0F2B5E);
  }

  /* 卡片通用 */
  section {
    padding: 70px 0;
    border-bottom: 1px solid rgba(0,224,255,0.1);
  }
  .section-label {
    font-size: 0.7rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent-green);
    margin-bottom: 1rem;
  }
  h2 {
    font-size: clamp(1.6rem, 4vw, 2.5rem);
    font-weight: 700;
    margin-bottom: 2rem;
  }
  .grid-2col {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.8rem;
  }
  .feature-card, .tech-card {
    background: var(--bg-card);
    border: 1px solid var(--border-glow);
    border-radius: 24px;
    padding: 1.8rem;
    transition: all 0.3s;
  }
  .feature-card:hover {
    border-color: var(--accent-cyan);
    transform: translateY(-4px);
  }
  .feature-icon {
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  .feature-card h3 {
    font-size: 1.3rem;
    margin-bottom: 0.8rem;
  }
  .feature-card p {
    color: var(--text-dim);
    font-size: 0.9rem;
  }

  /* 设计与开发方法区块 */
  .dev-method {
    background: linear-gradient(135deg, rgba(0,224,255,0.05), rgba(0,255,170,0.02));
    border-radius: 32px;
    padding: 2rem;
    margin-top: 1rem;
  }
  .tech-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    margin: 1.5rem 0;
  }
  .tech-badge {
    background: rgba(0,224,255,0.1);
    border: 1px solid rgba(0,224,255,0.3);
    padding: 0.4rem 1rem;
    border-radius: 40px;
    font-size: 0.8rem;
    font-weight: 500;
  }
  .timeline-item {
    border-left: 2px solid var(--accent-cyan);
    padding-left: 1.5rem;
    margin-bottom: 2rem;
  }
  .timeline-item h4 {
    font-size: 1.1rem;
    margin-bottom: 0.4rem;
  }
  .timeline-date {
    font-size: 0.7rem;
    color: var(--accent-cyan);
    margin-bottom: 0.5rem;
  }

  /* 数值指标 */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }
  .stat-item {
    background: var(--bg-card);
    border-radius: 20px;
    padding: 1.5rem;
    text-align: center;
    border: 1px solid var(--border-glow);
  }
  .stat-number {
    font-size: 2.2rem;
    font-weight: 800;
    background: linear-gradient(135deg, var(--accent-cyan), var(--accent-green));
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
  }

  footer {
    text-align: center;
    padding: 2rem 0;
    color: var(--text-dim);
    font-size: 0.8rem;
    border-top: 1px solid rgba(0,224,255,0.1);
  }

  /* PDF 导出隐藏辅助 */
  .pdf-export-area {
    background: white;
    padding: 2rem;
    max-width: 1100px;
    font-family: 'Inter', 'Noto Sans KR', sans-serif;
  }
  @media (max-width: 768px) {
    .container { padding: 0 1rem; }
    .hero { padding: 50px 0; }
    section { padding: 50px 0; }
    .floating-actions { bottom: 20px; right: 16px; }
    .pdf-download-btn span { font-size: 12px; }
  }
</style>
</head>
<body>
<div class="floating-actions">
  <div class="lang-switch">
    <button class="lang-btn active" id="btnZh" onclick="setLanguage('zh')">中文</button>
    <button class="lang-btn" id="btnKo" onclick="setLanguage('ko')">한국어</button>
  </div>
  <button class="pdf-download-btn" id="pdfBtn">
    <span>📄</span> <span class="lang-zh">韩文版 PDF 报告</span><span class="lang-ko">한국어 PDF 보고서</span>
  </button>
</div>

<main>
  <div class="container">
    <!-- HERO -->
    <div class="hero">
      <div class="hero-tag">
        <span class="lang-zh">DIGITAL HEALTH · INDUSTRY SAFETY</span>
        <span class="lang-ko">디지털 헬스 · 산업 안전</span>
      </div>
      <h1>
        <span class="lang-zh">数字健康医疗<br><span class="gradient-text">产业安全体系</span></span>
        <span class="lang-ko">디지털 헬스케어<br><span class="gradient-text">산업 보안 프레임워크</span></span>
      </h1>
      <p class="hero-sub">
        <span class="lang-zh">构建面向未来的医疗数据安全与产业防护网络，保障患者隐私、医疗机构数据完整性及全球互联安全标准。</span>
        <span class="lang-ko">미래 지향적 의료 데이터 보안 및 산업 보호 네트워크를 구축하여 환자 프라이버시, 의료기관 데이터 무결성, 글로벌 상호 연결 보안 기준을 보장합니다.</span>
      </p>
    </div>

    <!-- 1. 平台概览 / 주요 개요 -->
    <section>
      <div class="section-label">
        <span class="lang-zh">01 — 产业安全核心价值</span>
        <span class="lang-ko">01 — 산업 보안 핵심 가치</span>
      </div>
      <h2>
        <span class="lang-zh">为何医疗产业安全至关重要</span>
        <span class="lang-ko">의료 산업 보안이 왜 중요한가</span>
      </h2>
      <div class="grid-2col">
        <div class="feature-card"><div class="feature-icon">🛡️</div><h3><span class="lang-zh">患者数据保护</span><span class="lang-ko">환자 데이터 보호</span></h3><p><span class="lang-zh">医疗数据属最高敏感级信息。完善的安全体系确保隐私合规，符合HIPAA、GDPR及国内法规。</span><span class="lang-ko">의료 데이터는 가장 민감한 정보입니다. 완벽한 보안 체계로 프라이버시를 보호하고 HIPAA, GDPR 등 규정을 준수합니다.</span></p></div>
        <div class="feature-card"><div class="feature-icon">🏥</div><h3><span class="lang-zh">医疗机构合规</span><span class="lang-ko">의료기관 규정 준수</span></h3><p><span class="lang-zh">帮助医院、诊所满足国际信息安全标准，降低合规风险，建立患者信任。</span><span class="lang-ko">병원과 클리닉이 국제 정보보안 기준을 충족하도록 지원하여 규정 준수 리스크를 낮추고 환자 신뢰를 구축합니다.</span></p></div>
        <div class="feature-card"><div class="feature-icon">⚡</div><h3><span class="lang-zh">实时威胁检测</span><span class="lang-ko">실시간 위협 탐지</span></h3><p><span class="lang-zh">AI 驱动7x24监控，毫秒级响应潜在安全事件，保障医疗服务连续性。</span><span class="lang-ko">AI 기반 7x24시간 모니터링, 밀리초 단위 대응으로 의료 서비스 연속성을 보장합니다.</span></p></div>
        <div class="feature-card"><div class="feature-icon">🔗</div><h3><span class="lang-zh">跨机构安全互联</span><span class="lang-ko">기관 간 안전 연계</span></h3><p><span class="lang-zh">保证数据安全前提下，实现医院、保险、药企及监管机构间的安全数据共享。</span><span class="lang-ko">데이터 보안을 유지하면서 병원, 보험사, 제약사 및 규제 기관 간 안전한 데이터 공유를 실현합니다.</span></p></div>
      </div>
    </section>

    <!-- 2. 网站主要功能介绍 (包含6项核心功能) -->
    <section>
      <div class="section-label">
        <span class="lang-zh">02 — 平台核心功能</span>
        <span class="lang-ko">02 — 플랫폼 핵심 기능</span>
      </div>
      <h2>
        <span class="lang-zh">数字健康安全防护矩阵</span>
        <span class="lang-ko">디지털 헬스 보안 방어 매트릭스</span>
      </h2>
      <div class="grid-2col">
        <div class="feature-card"><h3>🔐 <span class="lang-zh">零信任架构(ZTA)</span><span class="lang-ko">제로 트러스트 아키텍처</span></h3><p><span class="lang-zh">动态身份验证、MFA多因素认证、行为生物识别，永不信任始终验证。</span><span class="lang-ko">동적 인증, 다중 인증(MFA), 행동 생체인식, 절대 신뢰하지 않고 항상 검증합니다.</span></p></div>
        <div class="feature-card"><h3>🤖 <span class="lang-zh">医疗AI安全分析</span><span class="lang-ko">의료 AI 보안 분석</span></h3><p><span class="lang-zh">深度学习模型识别异常访问模式，自动生成安全事件报告与整改建议。</span><span class="lang-ko">딥러닝 모델로 비정상 접근 패턴 탐지, 보안 보고서 및 개선 권고 자동 생성.</span></p></div>
        <div class="feature-card"><h3>🔒 <span class="lang-zh">端到端加密传输</span><span class="lang-ko">종단 간 암호화</span></h3><p><span class="lang-zh">TLS 1.3 + AES-256，确保医疗数据传输与存储的机密性与完整性。</span><span class="lang-ko">TLS 1.3 및 AES-256으로 의료 데이터 전송 및 저장 기밀성·무결성 보장.</span></p></div>
        <div class="feature-card"><h3>⛓️ <span class="lang-zh">区块链审计日志</span><span class="lang-ko">블록체인 감사 로그</span></h3><p><span class="lang-zh">不可篡改的审计追踪，满足监管检查与合规要求。</span><span class="lang-ko">변조 불가능 감사 추적, 규제 감사 및 규정 준수 충족.</span></p></div>
        <div class="feature-card"><h3>📋 <span class="lang-zh">自动合规扫描引擎</span><span class="lang-ko">자동 규정 준수 스캔</span></h3><p><span class="lang-zh">持续对照HIPAA、GDPR、HL7 FHIR等标准，自动标记不合规项并修复。</span><span class="lang-ko">HIPAA, GDPR, HL7 FHIR 등 기준과 실시간 비교, 미준수 항목 자동 표시 및 수정.</span></p></div>
        <div class="feature-card"><h3>🔄 <span class="lang-zh">灾难恢复与业务连续性</span><span class="lang-ko">재해 복구 및 업무 연속성</span></h3><p><span class="lang-zh">多活数据中心架构，RTO<4h / RPO<1h，极端情况持续运营。</span><span class="lang-ko">다중 활성 데이터센터, RTO<4시간·RPO<1시간, 극한 상황에서도 지속 운영.</span></p></div>
      </div>
    </section>

    <!-- 3. 网站设计与开发方法 (必须包含部分) -->
    <section>
      <div class="section-label">
        <span class="lang-zh">03 — 设计与开发方法</span>
        <span class="lang-ko">03 — 설계 및 개발 방법론</span>
      </div>
      <h2>
        <span class="lang-zh">现代化安全架构与技术实现</span>
        <span class="lang-ko">최신 보안 아키텍처 및 기술 구현</span>
      </h2>
      <div class="dev-method">
        <p style="margin-bottom:1rem;"><strong><span class="lang-zh">开发理念</span><span class="lang-ko">개발 철학</span>:</strong> <span class="lang-zh">采用 DevSecOps + 微服务架构，将安全性嵌入SDLC全生命周期。前端使用React18+TypeScript构建动态仪表板，后端基于Python FastAPI与Node.js网关，容器化部署于K8s集群，实现弹性扩展与高可用。</span><span class="lang-ko">DevSecOps + 마이크로서비스 아키텍처를 채택하여 보안을 SDLC 전체에 내재화. 프론트엔드는 React18+TypeScript, 백엔드는 Python FastAPI 및 Node.js 게이트웨이, 컨테이너화 및 K8s 클러스터 배포.</span></p>
        <div class="tech-stack">
          <span class="tech-badge">React 18</span><span class="tech-badge">TypeScript</span><span class="tech-badge">Python FastAPI</span><span class="tech-badge">Node.js</span><span class="tech-badge">Kubernetes</span><span class="tech-badge">Docker</span><span class="tech-badge">OWASP</span><span class="tech-badge">NIST CSF</span>
        </div>
        <div class="timeline-item"><div class="timeline-date">PHASE 01</div><h4><span class="lang-zh">安全需求与威胁建模</span><span class="lang-ko">보안 요구사항 및 위협 모델링</span></h4><p><span class="lang-zh">STRIDE方法识别欺骗、篡改、信息泄露等六大威胁，制定针对性防护策略。</span><span class="lang-ko">STRIDE 방법으로 스푸핑, 변조, 정보 유출 등 6대 위협 식별 및 맞춤형 방어 전략 수립.</span></p></div>
        <div class="timeline-item"><div class="timeline-date">PHASE 02</div><h4><span class="lang-zh">零信任安全架构设计</span><span class="lang-ko">제로 트러스트 보안 설계</span></h4><p><span class="lang-zh">网络隔离、身份管理、数据保护、安全监控四大安全域纵深防御体系。</span><span class="lang-ko">네트워크 격리, 신원 관리, 데이터 보호, 보안 모니터링의 심층 방어 체계.</span></p></div>
        <div class="timeline-item"><div class="timeline-date">PHASE 03</div><h4><span class="lang-zh">DevSecOps CI/CD 集成</span><span class="lang-ko">DevSecOps CI/CD 통합</span></h4><p><span class="lang-zh">SAST静态扫描、DAST动态测试、依赖漏洞扫描集成至流水线，安全左移。</span><span class="lang-ko">SAST 정적 스캔, DAST 동적 테스트, 취약점 스캔을 파이프라인에 통합.</span></p></div>
        <div class="timeline-item"><div class="timeline-date">PHASE 04</div><h4><span class="lang-zh">持续渗透测试与审计</span><span class="lang-ko">지속적 침투 테스트 및 감사</span></h4><p><span class="lang-zh">季度第三方渗透测试 + 自动化漏洞扫描，闭环管理安全漏洞。</span><span class="lang-ko">분기별 제3자 침투 테스트 및 자동화 취약점 스캔으로 보안 취약점 폐쇄 루프 관리.</span></p></div>
      </div>
    </section>

    <!-- 4. 预期效果与应用价值 -->
    <section>
      <div class="section-label">
        <span class="lang-zh">04 — 预期效果与应用价值</span>
        <span class="lang-ko">04 — 기대 효과 및 적용 가치</span>
      </div>
      <h2>
        <span class="lang-zh">赋能医疗产业安全升级</span>
        <span class="lang-ko">의료 산업 보안 혁신을 위한 가치</span>
      </h2>
      <div class="grid-2col">
        <div class="feature-card"><h3>📈 <span class="lang-zh">安全事件减少</span><span class="lang-ko">보안 사건 감소</span></h3><p><span class="lang-zh">AI实时威胁检测降低数据泄露风险达87%，提升应急响应效率70%以上。</span><span class="lang-ko">AI 실시간 위협 탐지로 데이터 유출 위험 87% 감소, 대응 효율 70% 이상 향상.</span></p></div>
        <div class="feature-card"><h3>💰 <span class="lang-zh">合规成本优化</span><span class="lang-ko">규정 준수 비용 최적화</span></h3><p><span class="lang-zh">自动化合规引擎减少人工审计工作量65%，快速通过ISO 27001等认证。</span><span class="lang-ko">자동 규정 준수 엔진으로 감사 작업량 65% 절감, ISO 27001 인증 신속 획득.</span></p></div>
        <div class="feature-card"><h3>🏆 <span class="lang-zh">患者信任提升</span><span class="lang-ko">환자 신뢰 향상</span></h3><p><span class="lang-zh">完善的安全体系增强患者对医疗机构的信任，提升品牌声誉。</span><span class="lang-ko">견고한 보안 체계는 환자의 의료기관 신뢰를 강화하고 브랜드 평판을 높입니다.</span></p></div>
        <div class="feature-card"><h3>🌍 <span class="lang-zh">全球化安全互操作</span><span class="lang-ko">글로벌 보안 상호운용성</span></h3><p><span class="lang-zh">支持跨国际医疗数据合规流动，促进全球医疗协作网络建设。</span><span class="lang-ko">국제 의료 데이터의 합법적 흐름을 지원하고 글로벌 의료 협력 네트워크 구축을 촉진합니다.</span></p></div>
      </div>
      <div class="stats-grid">
        <div class="stat-item"><div class="stat-number">99.97%</div><div class="lang-zh">系统可用性</div><div class="lang-ko">시스템 가용성</div></div>
        <div class="stat-item"><div class="stat-number">256-bit</div><div class="lang-zh">加密标准</div><div class="lang-ko">암호화 표준</div></div>
        <div class="stat-item"><div class="stat-number">&lt;50ms</div><div class="lang-zh">威胁响应</div><div class="lang-ko">위협 대응 시간</div></div>
        <div class="stat-item"><div class="stat-number">ISO 27K</div><div class="lang-zh">合规认证</div><div class="lang-ko">규정 준수 인증</div></div>
      </div>
    </section>

    <!-- 5. 其他相关证明 / 기타 증빙 -->
    <section>
      <div class="section-label">
        <span class="lang-zh">05 — 其他相关证明</span>
        <span class="lang-ko">05 — 기타 관련 증빙</span>
      </div>
      <h2>
        <span class="lang-zh">权威认证与安全保障</span>
        <span class="lang-ko">공인 인증 및 보안 보증</span>
      </h2>
      <div class="grid-2col">
        <div class="feature-card"><h3>✅ <span class="lang-zh">国际安全标准</span><span class="lang-ko">국제 보안 표준</span></h3><p><span class="lang-zh">符合ISO 27001:2022、HIPAA、GDPR、PIPL，通过第三方权威机构审计。</span><span class="lang-ko">ISO 27001:2022, HIPAA, GDPR, PIPL 충족, 제3자 기관 감사 통과.</span></p></div>
        <div class="feature-card"><h3>🔬 <span class="lang-zh">渗透测试报告</span><span class="lang-ko">침투 테스트 보고서</span></h3><p><span class="lang-zh">年度渗透测试由知名安全团队执行，未发现严重漏洞，系统高韧度。</span><span class="lang-ko">연례 침투 테스트에서 심각한 취약점 발견되지 않음, 시스템 높은 탄력성 확인.</span></p></div>
        <div class="feature-card"><h3>📜 <span class="lang-zh">区块链证据存证</span><span class="lang-ko">블록체인 증거 보존</span></h3><p><span class="lang-zh">所有关键操作日志上链，司法级不可否认性，满足电子数据取证要求。</span><span class="lang-ko">모든 중요 작업 로그가 블록체인에 저장되어 법적 부인 방지 및 전자 증거 요구사항 충족.</span></p></div>
        <div class="feature-card"><h3>🌐 <span class="lang-zh">全球访问可用性</span><span class="lang-ko">글로벌 접근 가능성</span></h3><p><span class="lang-zh">多CDN加速 + 备用架构，确保任何地域无差别访问，无封锁风险。</span><span class="lang-ko">멀티 CDN 가속 + 이중화 아키텍처로 전 세계 어디서나 차단 없이 접근 가능.</span></p></div>
      </div>
    </section>
  </div>
  <footer>
    <span class="lang-zh">© 2025 数字健康医疗 · 产业安全融合平台 | 数据安全 · 可信互联</span>
    <span class="lang-ko">© 2025 디지털 헬스케어 · 산업 보안 융합 플랫폼 | 데이터 보안 · 신뢰할 수 있는 연결</span>
  </footer>
</main>

<script>
  // 语言切换
  function setLanguage(lang) {
    document.body.classList.remove('lang-zh', 'lang-ko');
    document.body.classList.add(lang === 'zh' ? 'lang-zh' : 'lang-ko');
    document.getElementById('btnZh').classList.toggle('active', lang === 'zh');
    document.getElementById('btnKo').classList.toggle('active', lang === 'ko');
  }
  window.setLanguage = setLanguage;

  // ------------------- 韩文版 PDF 导出 -------------------
  // 构建一个临时容器，包含所有需要导出的韩文内容 (确保 PDF 中包含：设计开发方法、主要功能、预期效果、其他证明)
  async function generateKoreanPDF() {
    const btn = document.getElementById('pdfBtn');
    const originalText = btn.innerHTML;
    btn.disabled = true;
    btn.innerHTML = '<span>⏳</span> <span class="lang-ko">생성중...</span><span class="lang-zh">生成中...</span>';

    // 获取当前韩文内容（强制抓取韩语文本块）
    // 因为页面中所有含有 class="lang-ko" 的内容即韩文，但我们需要保证结构完整。
    // 克隆主要区域，并提取所有韩文内容块，同时保留结构和样式用于PDF。
    const mainClone = document.querySelector('main').cloneNode(true);
    // 移除所有中文内容，只保留韩文显示
    const allChinese = mainClone.querySelectorAll('.lang-zh');
    allChinese.forEach(el => el.remove());
    // 为PDF添加完整头部和脚注
    const pdfHeader = document.createElement('div');
    pdfHeader.style.borderBottom = '2px solid #00E0FF';
    pdfHeader.style.marginBottom = '20px';
    pdfHeader.style.paddingBottom = '10px';
    pdfHeader.innerHTML = '<h1 style="color:#0A0F1F;">디지털 헬스케어 & 산업 보안 기술 보고서</h1><p style="color:#2c3e50;">생성일: ' + new Date().toLocaleDateString('ko-KR') + ' | 버전 1.0</p><p style="font-size:12px;">본 보고서는 웹사이트 설계·개발 방법, 주요 기능, 기대 효과 및 적용 가치, 기타 증빙을 포함합니다.</p>';
    
    const pdfFooter = document.createElement('div');
    pdfFooter.style.marginTop = '30px';
    pdfFooter.style.borderTop = '1px solid #ccc';
    pdfFooter.style.paddingTop = '15px';
    pdfFooter.style.fontSize = '10px';
    pdfFooter.style.textAlign = 'center';
    pdfFooter.innerHTML = '© 2025 디지털 헬스-산업안전 통합 보고서 | 모든 정보는 진실하게 기술됨 | 글로벌 접근 보장';

    const wrapper = document.createElement('div');
    wrapper.style.background = 'white';
    wrapper.style.padding = '2rem';
    wrapper.style.maxWidth = '1100px';
    wrapper.style.margin = '0 auto';
    wrapper.style.fontFamily = "'Inter', 'Noto Sans KR', sans-serif";
    wrapper.style.color = '#1e2a3e';
    wrapper.appendChild(pdfHeader);
    wrapper.appendChild(mainClone);
    wrapper.appendChild(pdfFooter);
    
    document.body.appendChild(wrapper);
    const opt = {
      margin: [0.5, 0.5, 0.5, 0.5],
      filename: '디지털헬스_산업안전_기술보고서.pdf',
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 2, letterRendering: true, logging: false },
      jsPDF: { unit: 'in', format: 'a4', orientation: 'portrait' }
    };
    try {
      if (typeof html2pdf !== 'undefined') {
        await html2pdf().set(opt).from(wrapper).save();
      } else {
        alert('PDF 라이브러리가 로드되지 않았습니다. 잠시 후 다시 시도하세요.');
      }
    } catch (err) {
      console.error(err);
      alert('PDF 생성 중 오류가 발생했습니다.');
    } finally {
      document.body.removeChild(wrapper);
      btn.disabled = false;
      btn.innerHTML = originalText;
    }
  }

  document.getElementById('pdfBtn').addEventListener('click', generateKoreanPDF);
</script>
</body>
</html>
