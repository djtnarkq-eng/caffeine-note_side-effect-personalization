<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>청소년 카페인 케어</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    :root {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      color: #064e3b;
      background: #ecfdf5;
    }
    * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
    body {
      margin: 0;
      padding: 0;
      background: radial-gradient(circle at top, #bbf7d0 0, #ecfdf5 45%, #f0fdf4 100%);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }
    .app {
      max-width: 1100px;
      margin: 0 auto;
      padding: 16px 16px 80px;
      width: 100%;
    }
    header {
      margin-top: 4px;
      margin-bottom: 10px;
      display:flex;
      align-items:flex-start;
      justify-content:flex-start;
      gap:16px;
    }
    .logo-row {
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .logo-circle {
      width: 40px;
      height: 40px;
      border-radius: 999px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #22c55e;
      color: #f0fdf4;
      font-weight: 700;
      font-size: 1.2rem;
      box-shadow: 0 10px 20px rgba(22,163,74,0.35);
    }
    header h1 {
      margin: 0;
      font-size: 1.35rem;
      letter-spacing: -0.02em;
      color:#064e3b;
    }
    header p {
      margin: 6px 0 0;
      font-size: 0.9rem;
      color: #047857;
    }

    .panel {
      background: rgba(255,255,255,0.96);
      border-radius: 16px;
      padding: 12px 14px;
      box-shadow: 0 10px 20px rgba(22,101,52,0.05);
      margin-bottom: 12px;
      border:1px solid #bbf7d0;
    }
    .panel-title {
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:8px;
      margin-bottom:6px;
    }
    .panel-title-left {
      display:flex;
      flex-direction:column;
      gap:2px;
    }
    .panel-title-left span:first-child {
      font-size:0.95rem;
      font-weight:600;
      color:#065f46;
    }
    .panel-title-left span:last-child {
      font-size:0.78rem;
      color:#047857;
    }

    .small { font-size:0.8rem; color:#065f46; }
    .row { display:flex; gap:8px; flex-wrap:wrap; align-items:flex-end; }
    .row > div { flex:1; min-width:140px; }

    
    :root { --ctl-h: 40px; }

    /* 입력칸/버튼 높이를 통일해서 '제품명 기반 자동 추정' 버튼 가운데 높이에 맞춰 정렬 */
    input[type="text"], input[type="number"], input[type="datetime-local"], select {
      min-height: var(--ctl-h);
      height: var(--ctl-h);
      line-height: calc(var(--ctl-h) - 2px);
    }
    .btn { min-height: var(--ctl-h); height: var(--ctl-h); padding-top: 0; padding-bottom: 0; display:inline-flex; align-items:center; justify-content:center; }

label { font-size:0.88rem; display:block; margin:6px 0 3px; color:#065f46; }
    input, select, textarea {
      width:100%;
      padding:6px 8px;
      border-radius:8px;
      border:1px solid #a7f3d0;
      font-size:0.9rem;
      font-family:inherit;
      box-sizing:border-box;
      background:#f0fdf4;
      color:#064e3b;
    }
    textarea { resize:vertical; min-height:60px; }
    input[type="file"] { padding:3px 0; }
    input:focus, select:focus, textarea:focus {
      outline:none;
      border-color:#22c55e;
      box-shadow:0 0 0 1px rgba(34,197,94,0.4);
      background:#ecfdf5;
    }

    .btn {
      padding:8px 12px;
      border-radius:999px;
      border:none;
      cursor:pointer;
      font-size:0.88rem;
      font-weight:600;
    }
    .btn-primary {
      background:#16a34a;
      color:#f0fdf4;
    }
    .btn-outline {
      background:#ecfdf5;
      color:#15803d;
      border:1px solid #22c55e;
    }
    .btn-ghost {
      background:transparent;
      color:#15803d;
      border:1px dashed #6ee7b7;
    }
    .btn:active { transform:translateY(1px) scale(0.98); }

    .top-layout { display:flex; flex-wrap:wrap; gap:12px; }
    .top-left { flex:0 0 260px; min-width:220px; }
    .top-right { flex:1; min-width:260px; }

    /* ===== 홈 화면: 컵 중앙 정렬 + 체중 상자 ===== */
    #view-home {
      margin-top: 10px;
      display:block;
    }
    .home-top-wrapper {
      position: relative;
      width: 100%;
      max-width: 760px;
      margin: 40px auto 16px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .cup-center-box {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
    }
    .weight-info-box {
      position: absolute;
      right: 0;
      top: -10px;
      width: 240px;
      padding: 12px 14px;
      background: rgba(255,255,255,0.95);
      border: 1px solid #bbf7d0;
      border-radius: 12px;
      font-size: 0.85rem;
      line-height: 1.38;
      color: #065f46;
      box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    }
    @media (max-width: 600px) {
      .home-top-wrapper {
        flex-direction: column;
      }
      .weight-info-box {
        position: static;
        width: 100%;
        margin-top: 16px;
      }
    }

    /* 컵 게이지 */
    .cup-shell {
      display:flex;
      justify-content:center;
      margin:6px 0 4px;
      transition:background 0.5s ease;
      cursor:pointer;
    }
    .cup-body {
      position:relative;
      width:150px;
      height:200px;
      clip-path: polygon(5% 4%, 95% 4%, 82% 100%, 18% 100%);
      border-radius:22px 22px 30px 30px;
      border:3px solid rgba(0,0,0,0.45);
      background:rgba(255,255,255,0.98);
      overflow:hidden;
      box-shadow:0 10px 18px rgba(21,128,61,0.18);
    }
    .cup-fill {
      position:absolute;
      left:0;
      bottom:0;
      width:100%;
      height:0%;
      background:linear-gradient(to top,#78350f,#d97757);
      transition:height 0.6s ease;
    }
    .cup-text {
      position:absolute;
      top:60%;
      left:50%;
      transform:translate(-50%,-50%);
      font-size:1rem;
      font-weight:600;
      color:#052e16;
      text-shadow:0 1px 2px rgba(255,255,255,0.9);
      white-space:nowrap;
    }
    .cup-mark {
      position:absolute;
      left:0;
      right:0;
      bottom:66.666%;
      height:2px;
      background:repeating-linear-gradient(
        to right,
        rgba(22,163,74,0.9) 0px,
        rgba(22,163,74,0.9) 6px,
        transparent 6px,
        transparent 10px
      );
      pointer-events:none;
    }
    /* 눈금선 왼쪽 말풍선 */
    .cup-mark-label {
      position:absolute;
      right:100%;
      bottom:calc(66.666% - 2px);
      margin-right:10px;
      font-size:0.72rem;
      color:#065f46;
      padding:4px 8px;
      border-radius:10px;
      background:rgba(236,253,245,0.98);
      box-shadow:0 0 0 1px rgba(16,185,129,0.45);
      white-space:nowrap;
    }
    .cup-mark-label::after {
      content:"";
      position:absolute;
      left:100%;
      top:50%;
      transform:translateY(-50%);
      border-width:6px;
      border-style:solid;
      border-color:transparent transparent transparent rgba(236,253,245,0.98);
    }

    .cup-shell.alert {
      background:radial-gradient(circle at center,rgba(248,113,113,0.28) 0, transparent 70%);
    }
    .cup-body.shake {
      animation:cupShake 0.4s ease-in-out infinite;
    }
    @keyframes cupShake {
      0% { transform:translateX(0) rotate(0); }
      20% { transform:translateX(-2px) rotate(-2deg); }
      40% { transform:translateX(2px) rotate(2deg); }
      60% { transform:translateX(-1.5px) rotate(-1.5deg); }
      80% { transform:translateX(1.5px) rotate(1.5deg); }
      100% { transform:translateX(0) rotate(0); }
    }

    .stat-row {
      display:flex;
      justify-content:space-between;
      font-size:0.9rem;
      margin:2px 0;
    }

    .stats-layout { display:flex; flex-wrap:wrap; gap:10px; }
    .stats-detail-block {
      margin-top: 8px;
      padding: 8px 10px;
      border-radius: 12px;
      border: 1px solid #bbf7d0;
      background: #f0fdf4;
    }
    .stats-detail-block h4 {
      margin: 0 0 4px;
      font-size: 0.9rem;
      color: #065f46;
    }
    .stats-chart-wrap { flex:1.6; min-width:260px; height:230px; }
    .stats-cal-wrap { flex:1; min-width:220px; }
    .calendar-grid {
      display:grid;
      grid-template-columns:repeat(7,minmax(0,1fr));
      gap:2px;
      margin-top:4px;
      font-size:0.78rem;
    }
    .calendar-day-header {
      text-align:center;
      font-weight:600;
      padding:2px 0;
      color:#047857;
    }
    .calendar-day {
      height:22px;
      border-radius:6px;
      text-align:center;
      line-height:22px;
      background:#e5f7ef;
      color:#064e3b;
    }
    .calendar-day.has-intake { font-weight:600; }
    .calendar-legend { margin-top:4px; font-size:0.75rem; color:#047857; }

    .effect-icon-row {
      display:flex;
      flex-wrap:wrap;
      gap:6px;
      margin:6px 0;
    }
    .effect-chip {
      display:inline-flex;
      align-items:center;
      gap:4px;
      padding:5px 8px;
      border-radius:999px;
      border:1px solid #a7f3d0;
      font-size:0.8rem;
      background:#ecfdf5;
      cursor:pointer;
      color:#065f46;
    }
    .effect-chip span:first-child { font-size:1.1rem; }
    .effect-chip.active {
      background:#fee2e2;
      border-color:#f97316;
      color:#b45309;
    }
.product-icon-row {
  display:flex;
  flex-wrap:wrap;
  gap:6px;
  margin:6px 0;
}
.product-shortcut-chip {
  display:inline-flex;
  align-items:center;
  gap:4px;
  padding:5px 8px;
  border-radius:999px;
  border:1px solid #a7f3d0;
  font-size:0.8rem;
  background:#ecfdf5;
  cursor:pointer;
  color:#065f46;
}
.product-shortcut-chip span:first-child {
  font-size:1.1rem;
}
.product-shortcut-chip.active {
  background:#dcfce7;
  border-color:#22c55e;
  color:#166534;
}
    .effect-tips {
      font-size:0.8rem;
      background:#fefce8;
      border-radius:8px;
      padding:6px 8px;
      margin-top:4px;
      border:1px solid #facc15;
      color:#854d0e;
    }
    .effect-list-item {
      display:flex;
      justify-content:space-between;
      gap:6px;
      padding:4px 0;
      border-bottom:1px dashed #d1fae5;
      font-size:0.8rem;
      color:#065f46;
    }

    .banner-cards {
      display:flex;
      flex-wrap:nowrap;
      gap:12px;
      margin-top:8px;
    }
    .banner-card {
      flex:1.3;
      min-width:260px;
      border-radius:12px;
      border:1px solid #6ee7b7;
      padding:8px;
      font-size:0.8rem;
      background:#ecfdf5;
    }
    .banner-card-title {
      font-size:0.85rem;
      font-weight:600;
      color:#047857;
      margin-bottom:4px;
    }

    .bottom-nav {
      position:fixed;
      left:0; right:0; bottom:0;
      padding:8px 12px 14px;
      background:rgba(240,253,250,0.96);
      backdrop-filter:blur(18px);
      border-top:1px solid rgba(110,231,183,0.9);
      display:flex;
      justify-content:center;
      z-index: 10;
    }
    .bottom-nav-inner {
      max-width:1100px;
      width:100%;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:8px;
    }
    .nav-pill {
      flex:1;
      display:flex;
      align-items:center;
      justify-content:center;
      gap:6px;
      border-radius:999px;
      padding:7px 10px;
      font-size:0.85rem;
      border:none;
      background:#166534;
      color:#ecfdf5;
      cursor:pointer;
    }
    .nav-dot {
      width:7px; height:7px;
      border-radius:999px;
      background:#22c55e;
      box-shadow:0 0 0 6px rgba(34,197,94,0.25);
    }
    @media (max-width: 720px) {
      .stats-layout { flex-direction:column; }
      .top-layout { flex-direction:column; }
      .banner-cards { flex-direction:column; }
    }

    /* 화면 뷰 토글 */
    #view-intake { margin-top:4px; display:none; }
    #view-extra { margin-top:4px; display:none; }

    /* 드래그 힌트 */
    .drag-hint {
      margin-top:10px;
      text-align:center;
      font-size:0.8rem;
      color:#047857;
      cursor: pointer;
    }
    .drag-handle {
      width:60px;
      height:4px;
      border-radius:999px;
      margin:4px auto 2px;
      background:rgba(22,163,74,0.5);
    }

    /* 플로팅 버튼 & 오버레이 */
    #fab-menu-button {
      position: fixed;
      bottom: 85px;
      right: 22px;
      width: 58px;
      height: 58px;
      border-radius: 50%;
      background: #22c55e;
      color: white;
      font-size: 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 6px 18px rgba(34,197,94,0.35);
      cursor: pointer;
      z-index: 999;
      transition: transform 0.2s ease;
    }
    #fab-menu-button:active {
      transform: scale(0.9);
    }
    #fab-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.35);
      backdrop-filter: blur(2px);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 998;
    }
    #fab-menu {
      background: #ffffff;
      border-radius: 16px;
      padding: 18px 16px;
      width: 220px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.25);
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    #fab-menu button {
      padding: 10px 12px;
      font-size: 0.9rem;
      background: #ecfdf5;
      border: 1px solid #6ee7b7;
      border-radius: 10px;
      color: #065f46;
      cursor: pointer;
    }
    #fab-menu button:active {
      background: #d1fae5;
    }

    /* 텍스트 가독성 공통 */
    .responsive-text-block {
      width: 100%;
      max-width: 480px;
      margin: 0 auto;
      padding: 8px 12px;
      line-height: 1.45;
      font-size: 0.9rem;
      word-break: keep-all;
      overflow-wrap: break-word;
      color: #065f46;
      text-align:center;
    }
    @media (min-width: 600px) {
      .responsive-text-block {
        max-width: 540px;
        font-size: 0.95rem;
        line-height: 1.55;
      }
    }
    @media (min-width: 900px) {
      .responsive-text-block {
        max-width: 620px;
        font-size: 1rem;
        line-height: 1.6;
      }
    }
  
    /* datalist 입력(제품/용량) 드롭다운 화살표를 select(mL)과 유사하게 보이도록 */
    .input-dd{ position:relative; display:block; }
    .input-dd input{ padding-right:38px !important; }
    .input-dd::before{
      content:"";
      position:absolute;
      right:6px;
      top:50%;
      transform:translateY(-50%);
      width:26px; height:26px;
      background:rgba(240,253,244,0.98);
      border-radius:8px;
      pointer-events:none;
    }
    .input-dd::after{
      content:"";
      position:absolute;
      right:14px;
      top:50%;
      transform:translateY(-35%);
      width:0; height:0;
      border-left:6px solid transparent;
      border-right:6px solid transparent;
      border-top:7px solid rgba(6,95,70,0.85);
      pointer-events:none;
    }


    /* ✅ datalist 기본 드롭다운 화살표(브라우저 기본 표시) 숨김: 커스텀 화살표만 보이게 */
    .input-dd input[list]::-webkit-calendar-picker-indicator{
      opacity:0;
      display:none;
      -webkit-appearance:none;
    }
    .input-dd input[list]{
      -webkit-appearance:none;
      appearance:none;
    }

/* 개인차 조절 활성 표시 */
.chip.active{ background:#16a34a; color:#fff; border-color:#16a34a; }
/* (추가) 개인차 조절 모달 */
.modal-backdrop{
  position: fixed; inset: 0; background: rgba(0,0,0,.35);
  display:flex; align-items:center; justify-content:center; z-index: 9999;
  padding: 16px;
}
.modal-panel{
  width: min(560px, 100%);
  background: rgba(255,255,255,.96);
  border: 1px solid rgba(6,78,59,.18);
  border-radius: 16px;
  box-shadow: 0 18px 60px rgba(0,0,0,.18);
  overflow:hidden;
}
.modal-head{ display:flex; align-items:flex-start; justify-content:space-between; gap:12px; padding:14px 14px 10px;}
.modal-title{ font-size:18px; font-weight:900; color:#064e3b;}
.modal-sub{ font-size:12px; opacity:.8; margin-top:2px; line-height:1.35;}
.modal-close{ border:none; background:transparent; font-size:18px; cursor:pointer; padding:4px 8px; opacity:.75;}
.modal-close:hover{ opacity:1;}
.modal-body{ padding: 6px 14px 12px; max-height: 55vh; overflow:auto;}
.slider-row{ display:flex; align-items:center; justify-content:space-between; gap:12px; padding:10px 0; border-bottom:1px dashed rgba(6,78,59,.18);}
.slider-row:last-child{ border-bottom:none;}
.slider-left{ min-width: 140px; }
.slider-name{ font-weight:800; }
.slider-desc{ font-size:11px; opacity:.75; margin-top:2px;}
.slider-right{ display:flex; align-items:center; gap:10px; flex:1;}
.slider-right input[type="range"]{ width:100%; }
.slider-val{ width:52px; text-align:right; font-variant-numeric: tabular-nums; font-weight:800; opacity:.9;}

.modal-actions{ display:flex; justify-content:flex-end; gap:10px; padding: 12px 14px 14px; border-top:1px solid rgba(6,78,59,.15);}
.btn-soft{
  border: 1px solid rgba(6,78,59,.25);
  background: rgba(187,247,208,.35);
  color:#064e3b;
  border-radius: 999px;
  padding: 10px 14px;
  cursor:pointer;
  font-weight:800;
}
.btn-primary{
  border: 1px solid rgba(6,78,59,.0);
  background: #22c55e;
  color: white;
  border-radius: 999px;
  padding: 10px 16px;
  cursor:pointer;
  font-weight:900;
}
.btn-primary:hover{ filter: brightness(0.98); }

/* (추가) 위험도 요약 박스: 오른쪽 상단에 자연스럽게 고정 */
.effects-right #risk-indicator-box{ position: sticky; top: 12px; margin-top: 0; }
#risk-indicator-box{font-size:13px!important;}
#risk-indicator-box .risk-title{font-size:14px!important;}
#risk-indicator-box .risk-score{font-size:13px!important;}
</style>
</head>
<body>
<div class="app">
  <header>
    <div class="logo-row">
      <div class="logo-circle">C</div>
      <div>
        <h1>청소년 카페인 케어</h1>
        <p>홈(컵) · 섭취 기록 · 추가 기능(통합+세부 화면)을 분리해서 사용해요.</p>
      </div>
    </div>
  </header>

  <!-- ===== 1. 홈 화면 ===== -->
  <div id="view-home">
    <section class="panel" style="background:transparent; box-shadow:none; border:none; padding:0;">
      <div class="home-top-wrapper">
        <!-- 가운데 컵 -->
        <div class="cup-center-box">
          <div class="cup-shell" id="cup-gauge" onclick="openIntake()">
            <div class="cup-body">
              <div class="cup-fill" id="cup-fill"></div>
              <div class="cup-mark"></div>
              <div class="cup-mark-label" id="cup-mark-label">일일 권장 섭취량</div>
              <div class="cup-text" id="cup-text">0 mg</div>
            </div>
          </div>
        </div>

        <!-- 오른쪽 상단 체중 입력 -->
        <div class="weight-info-box">
          <label for="weight-kg">체중 (선택 입력)</label>
          <input
            type="number"
            id="weight-kg"
            min="30"
            max="120"
            placeholder="예: 60"
          />
          <div class="small" style="margin-top:4px;">
            * 체중을 입력하면 권장 섭취량 눈금이 자동 계산됩니다.<br>
            (kg당 2.5 mg 기준)
          </div>
        </div>
      </div>

      <div class="drag-hint responsive-text-block" onclick="showExtraCombined()">
        <div class="drag-handle"></div>
        화면을 <b>위로 끌어올리거나 이 영역을 터치하면</b><br>
        통계 · 혈중 농도 · 부작용 · 정보/배너 등<br>
        <b>추가 기능 통합 화면</b>이 나타납니다.
      </div>
    </section>
  </div>

  <!-- ===== 2. 카페인 섭취 기록 화면 ===== -->
  <div id="view-intake">
    <button type="button" class="btn btn-outline" onclick="goHome()" style="margin-bottom:8px;">
      ⬅ 기본 화면으로
    </button>

    <section class="panel">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>카페인 섭취 기록</span>
          <span class="small">사진/제품명 자동 추정 + 오늘 요약</span>
        </div>
      </div>
      <div class="top-layout">
        <div class="top-right">
          <form id="intake-form">
            <label>제품 사진 첨부 (선택)</label>
            <input type="file" id="photo-input" accept="image/*" />
            <div class="small" id="photo-hint">
              * 파일명에 <b>coffee</b>, <b>energy</b>, <b>tea</b>, <b>cola</b>, <b>choco</b>, <b>snack</b> 등이 들어가면
              카페인 음료·식품의 양을 대략 추정합니다.
            </div>

            <div class="row">
              <div>
                <label>제품/음식 이름</label>
                <div class="row" style="align-items:flex-end;">
                  <div style="flex:2; min-width:160px;">
                    <div class="input-dd">
          <input type="text" id="product-name" list="kfd-caffeine-list" placeholder="예: 아메리카노, 에너지드링크, 초콜릿 쿠키" />
        </div>
                    <datalist id="kfd-caffeine-list"></datalist>

                  </div>
                  <div style="flex:1; min-width:110px;">

                    <button type="button" class="btn btn-ghost" id="guess-from-name-btn">제품명 기반 자동 추정</button>
                  </div>
                </div>
              </div>
              <div>
                <label>카페인 양 (mg)</label>
                <input type="number" id="caffeine-mg" min="0" step="1" placeholder="예: 80" required />
              </div>
            </div>

            <!-- ✅ [PRODUCT ICON UI] 자주 마시는 메뉴 아이콘 -->
            <div style="margin-top:6px;">
              <h3 style="margin:0 0 4px; font-size:0.9rem; color:#065f46;">자주 마시는 메뉴</h3>
              <div class="product-icon-row" id="product-shortcut-icons"></div>
              <div class="small" id="product-shortcut-hint" style="margin-top:4px;">
                아이콘을 누르면 <b>제품명 · 카페인 양 · 섭취량 메모</b>가 자동으로 채워집니다.
              </div>       
            </div>
            <!-- ✅ [PRODUCT ICON UI 끝] -->

          <div class="row">
  <div style="flex:1">
    <label>섭취량 메모</label>
    <input type="text" id="amount-note" placeholder="예: 1캔, 톨 사이즈 1잔, 쿠키 2개" />
    <!-- ✅ 섭취량 빠른 입력: 자연수 스크롤 + 직접 입력 -->
    <div class="amount-quick" style="margin-top:8px; display:flex; gap:8px; align-items:center; flex-wrap:wrap;">
      <div class="input-dd" style="flex:0 0 auto;">
        <input id="amount-qty"
       type="text"
       inputmode="numeric"
       pattern="[0-9]*"
       list="amount-qty-list"
       placeholder="예: 250"  style="width:120px;" aria-label="섭취량 숫자" />
      </div>
             
      <select id="amount-unit" aria-label="섭취량 단위" style="width:90px;">
        <option value="ml">mL</option>
        <option value="잔">잔</option>
        <option value="컵">컵</option>
      </select>
      <button id="amount-apply" type="button" class="btn" style="padding:8px 12px;">적용</button>
      <small style="opacity:.75;">(예: 125 mL, 2잔, 1컵)</small>
        </div>
<datalist id="amount-qty-list"></datalist>
  </div>

  <div style="flex:1">
    <label>섭취 시각</label>
    <input type="datetime-local" id="intake-time" required />
  </div>
</div>

            <div class="row">
              <div>
                <label>식전/식후/공복</label>
                <select id="meal-timing">
                  <option value="BEFORE">식전</option>
                  <option value="AFTER">식후</option>
                  <option value="EMPTY">공복</option>
                </select>
              </div>
              <div>
                <label>구분</label>
                <select id="category">
                  <option value="drink">카페인 음료</option>
                  <option value="food">카페인 식품(디저트/간식 등)</option>
                  <option value="medicine">약/건강보조식품</option>
                  <option value="other">기타</option>
                </select>
              </div>
            </div>

            <div style="margin-top:8px; display:flex; justify-content:flex-end; gap:8px;">
              <button type="button" class="btn btn-outline" id="now-btn">현재 시간으로</button>
              <button type="submit" class="btn btn-primary" id="submit-intake-btn">기록 저장</button>
              <button type="button" class="btn btn-ghost" id="edit-mode-btn">기록 수정</button>
            </div>

<div id="edit-tools" style="margin-top:6px; display:none;">
  <div class="small" style="margin-bottom:2px;">수정하거나 삭제할 기록을 선택한 뒤 버튼을 누르세요.</div>
  <div class="row" style="align-items:flex-end;">
    <div>
      <select id="edit-intake-select"></select>
    </div>
    <div style="flex:0 0 130px; min-width:115px;">
      <button type="button" class="btn btn-outline" id="load-intake-btn">선택 불러오기</button>
    </div>
    <!-- ✅ 추가: 선택 기록 삭제 버튼 -->
    <div style="flex:0 0 130px; min-width:115px;">
      <button type="button" class="btn btn-ghost" id="delete-intake-btn">선택 기록 삭제</button>
    </div>
  </div>
</div>

          </form>


          <div style="margin-top:8px;">
            <h3 style="margin:0 0 4px; font-size:0.95rem; color:#065f46;">오늘 섭취 요약</h3>
            <div id="today-summary">
              <div class="stat-row"><span>오늘 총 섭취량</span><span><b>0 mg</b></span></div>
              <div class="stat-row"><span>기록된 섭취 횟수</span><span>0회</span></div>
            </div>
            <div class="small" style="margin-top:4px;">
              * 이 시스템은 기록과 추세 확인용입니다. 건강 문제는 보호자·전문의와 상의하세요.
            </div>
          </div>
        </div>
      </div>
    </section>
<section class="panel" id="product-shortcut-panel">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>자주 마시는 메뉴 추가</span>
          <span class="small">
            카페인 섭취 기록에서 자주 사용하는 메뉴를 아이콘으로 저장해 두고,
            한 번에 불러올 수 있어요.
          </span>
        </div>
      </div>

      <div class="small" style="margin-bottom:6px;">
        위에서 보이는 <b>자주 마시는 메뉴 아이콘</b> 영역과 연결되어 있습니다.<br>
        이 박스에서 추가한 메뉴는, 카페인 섭취 기록 상단의 아이콘 목록에 자동으로 나타납니다.
      </div>

      <div class="row" id="product-shortcut-add-row" style="margin-top:2px; align-items:flex-end;">
        <div style="flex:2; min-width:120px;">
          <label style="margin:0 0 2px;">메뉴 이름</label>
          <input type="text" id="product-shortcut-name" placeholder="예: 편의점 캔커피" />
        </div>
        <div style="flex:1; min-width:90px;">
          <label style="margin:0 0 2px;">카페인 (mg)</label>
          <input type="number" id="product-shortcut-caffeine" min="0" step="1" placeholder="예: 80" />
        </div>
        <div style="flex:1; min-width:90px;">
          <label style="margin:0 0 2px;">용량/메모</label>
          <input type="text" id="product-shortcut-volume" placeholder="예: 355ml, 24oz" />
        </div>
        <div style="flex:0 0 70px; min-width:60px;">
          <label style="margin:0 0 2px;">아이콘</label>
          <input type="text" id="product-shortcut-icon" placeholder="예: ☕" maxlength="2" />
        </div>
        <div style="flex:0 0 80px; min-width:70px;">
          <button type="button" class="btn btn-ghost" id="product-shortcut-add-btn">추가</button>
        </div>
      </div>
    </section>
  </div>

  <!-- ===== 3. 추가 기능: 통합 + 세부 모드 ===== -->
  <div id="view-extra">
    <div style="display:flex; gap:8px; margin-bottom:8px;">
      <button type="button" class="btn btn-outline" onclick="goHome()">
        ⬅ 기본 화면으로
      </button>
      <button type="button" class="btn btn-ghost" id="extra-back-btn" onclick="setExtraMode(null)" style="display:none;">
        전체 보기
      </button>
    </div>

    <!-- 3-1 통계 -->
    <section class="panel" id="extra-section-stats">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>통계 · 또래 평균 · 월 캘린더</span>
          <span class="small">기간별 막대그래프 + 유사 체중/동일 나이 실선 비교</span>
        </div>
        <button type="button" class="btn btn-ghost" onclick="openStatsDetail()">전체 화면</button>
      </div>
      <div class="row">
        <div class="row" style="flex:1; align-items:flex-end;">
          <div style="flex:1; min-width:140px;">
            <label>기간 선택</label>
            <select id="period-select">
              <option value="day">오늘 (시간대별)</option>
              <option value="week">최근 7일 (일별)</option>
              <option value="month">이번 달 (일별)</option>
              <option value="year">올해 (월별)</option>
            </select>
          </div>
        </div>
      </div>

      <div class="stats-layout" style="margin-top:6px;">
        <div class="stats-chart-wrap">
          <canvas id="stats-chart"></canvas>
        </div>
        <div class="stats-cal-wrap">
          <div class="small"><b>월간 캘린더</b> (이번 달, 일별 섭취량 강도)</div>
          <div id="month-calendar" class="small"></div>
        </div>
      </div>
      <div id="stats-text" class="small" style="margin-top:6px;"></div>
 <!-- 📊 통계 전체 화면에서만 보이는 기간별 세부 그래프 영역 -->
  <div id="stats-detail-wrapper" style="display:none; margin-top:10px;">
    <div class="small" style="margin-bottom:6px;">
      오늘 · 최근 7일 · 이번 달 · 올해까지의 카페인 섭취량을
      <b>기간 순서대로 한 번에</b> 볼 수 있는 세부 그래프입니다.
    </div>

    <!-- 1) 오늘 (시간대별) -->
    <div class="stats-detail-block">
      <h4>오늘 (시간대별)</h4>
      <div style="height:180px; margin-bottom:6px;">
        <canvas id="stats-chart-day"></canvas>
      </div>
      <div class="small" id="stats-text-day"></div>
    </div>

    <!-- 2) 최근 7일 (일별) -->
    <div class="stats-detail-block">
      <h4>최근 7일 (일별)</h4>
      <div style="height:180px; margin-bottom:6px;">
        <canvas id="stats-chart-week"></canvas>
      </div>
      <div class="small" id="stats-text-week"></div>
    </div>

    <!-- 3) 이번 달 (일별) -->
    <div class="stats-detail-block">
      <h4>이번 달 (일별)</h4>
      <div style="height:180px; margin-bottom:6px;">
        <canvas id="stats-chart-month"></canvas>
      </div>
      <div class="small" id="stats-text-month"></div>
    </div>

    <!-- 4) 올해 (월별) -->
    <div class="stats-detail-block">
      <h4>올해 (월별)</h4>
      <div style="height:180px; margin-bottom:6px;">
        <canvas id="stats-chart-year"></canvas>
      </div>
      <div class="small" id="stats-text-year"></div>
    </div>
  </div>
</section>

    <!-- 3-2 혈중 카페인 -->
    <section class="panel" id="extra-section-blood">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>혈중 카페인 농도 · 수면 시간</span>
          <span class="small">반감기 모델 + 확대/축소 + 수면 시간 추천</span>
        </div>
        <button type="button" class="btn btn-ghost" onclick="openBloodDetail()">전체 화면</button>
      </div>
      <div class="row">
        <div>
          <label>평소 취침 시간</label>
          <input type="time" id="sleep-time" />
          <div class="small">* 취침 시간을 바꾸면, 해당 시점의 잔여 카페인과 수면 영향 안내가 표시됩니다.</div>
        </div>
        <div>
          <label>그래프 보기 범위</label>
          <select id="caffeine-range">
            <option value="morning">아침 (6~12시)</option>
            <option value="school">등교~하교 시간 (6~18시)</option>
            <option value="evening">저녁/밤 (18~24시)</option>
            <option value="full" selected>하루 전체 (0~24시)</option>
          </select>
          <div class="small">* 범위를 바꾸면 그래프를 확대·축소해서 추이를 자세히 볼 수 있어요.</div>
        </div>
      </div>

      <div style="margin-top:8px; height:230px;">
        <canvas id="caffeine-chart"></canvas>
      </div>
      <div id="sleep-info" style="margin-top:8px; font-size:0.9rem;"></div>
      <!-- 📈 혈중 카페인 세부 그래프 (전체 화면 모드에서만 표시) -->
      <div id="blood-detail-wrapper" style="display:none; margin-top:10px;">
        <div class="small" style="margin-bottom:6px;">
          위의 그래프는 <b>오늘 하루</b> 중 선택한 시간대만 보는 그래프이고,<br>
          아래부터는 <b>최근 1주일</b>과 <b>이번 달</b> 동안의
          <b>혈중 카페인 농도 추이</b>를 시간 순서대로 길게 보여주는 세부 그래프입니다.
        </div>

        <!-- 1) 최근 7일 전체 추이 -->
        <div class="stats-detail-block">
          <h4>최근 7일 혈중 카페인 농도 추이</h4>
          <div style="height:180px; margin-bottom:6px;">
            <canvas id="caffeine-chart-week"></canvas>
          </div>
          <div class="small" id="caffeine-text-week"></div>
        </div>

        <!-- 2) 이번 달 전체 추이 -->
        <div class="stats-detail-block">
          <h4>이번 달 혈중 카페인 농도 추이</h4>
          <div style="height:180px; margin-bottom:6px;">
            <canvas id="caffeine-chart-month"></canvas>
          </div>
          <div class="small" id="caffeine-text-month"></div>
        </div>
      </div>
    </section>

    <!-- 3-3 부작용 -->
    <section class="panel" id="extra-section-effects">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>부작용 기록 · 대처법 · 후기</span>
          <span class="small">자주 나타나는 증상은 아이콘으로 빠르게 선택</span>
        </div>
        <button type="button" class="btn btn-ghost" onclick="openEffectsDetail()">전체 화면</button>
      </div>

      <div class="row">
        <div style="flex:1; min-width:260px;">
          <h3 style="margin:0 0 4px; font-size:0.95rem; color:#065f46;">1) 주요 증상 선택</h3>
          <div class="effect-icon-row" id="effect-icons"></div>
          <div id="effect-tips" class="effect-tips" style="display:none;"></div>
    <div class="sensitivity-row" style="margin-top:10px; display:flex; gap:10px; align-items:center; flex-wrap:wrap;">
  <span style="font-size:12px; opacity:.8;">증상별 민감도를 슬라이더로 조절할 수 있어요.</span>
</div>


          <form id="side-effect-form" style="margin-top:8px;">
            <label>증상 메모 (선택)</label>
            <textarea id="side-effect-notes" placeholder="예: 심장이 두근거리고, 손이 약간 떨렸어요."></textarea>
            <label>발생 시각</label>
            <input type="datetime-local" id="side-effect-time" />
      <div style="margin-top:8px; display:flex; justify-content:flex-end; gap:10px;">
        <button type="button" class="btn btn-ghost" id="open-personal-modal">개인차 조절</button>
              <button type="submit" class="btn btn-primary">부작용 기록 저장</button>
            </div>
          </form>

<div style="margin-top:12px;">
<h3 style="margin:0 0 4px; font-size:0.95rem; color:#065f46;">2) 내 부작용 기록</h3>
<div id="side-effect-list" class="small">아직 기록이 없습니다.</div>

<!-- ✅ 추가: 내 카페인 위험도 요약 -->



</div>

        </div>

        <div style="flex:1; min-width:260px;">
      <div id="risk-indicator-box" style="margin:8px 0 12px; padding:12px; border-radius:14px; background:#fefce8; border:1px solid #facc15; display:none;">
        <div style="font-weight:800; color:#065f46; margin-bottom:6px;"><span class="risk-title">나의 부작용 위험도 점수 및 위험군</span></div>
        <div id="risk-indicator-content" style="font-size:0.92rem; line-height:1.35;"></div>
      </div>
<h3 style="margin:10px 0 4px; font-size:0.95rem; color:#065f46;">3) 다른 사람 후기</h3>

          <div style="display:flex; gap:6px;">
            <div style="flex:1; min-width:180px;">
              <h4 style="margin:4px 0; font-size:0.9rem; color:#065f46;">후기</h4>
              <div id="peer-stories" class="small"></div>
            </div>
            <div style="flex:1; min-width:180px;">
              <h4 style="margin:4px 0; font-size:0.9rem; color:#065f46;">해결 방법</h4>
              <div id="peer-solutions" class="small"></div>
            </div>
          </div>
        </div>
      </div>
  <!-- 4) 세부 화면(전체 화면 모드에서만) : 증상별 상세 모아보기 -->
  <div id="effects-detail-advanced"
       style="margin-top:10px; padding-top:8px; border-top:1px dashed #d1fae5; display:none;">
    <h3 style="margin:0 0 4px; font-size:0.95rem; color:#065f46;">
      📝 부작용 상세 기록 모아보기
    </h3>
    <div class="small" style="color:#047857; margin-bottom:4px;">
      ‘전체 화면’으로 들어왔을 때, 내가 기록한 부작용을 증상별로 모아 보고<br>
      각 증상에 맞는 <b>대처 방법</b>과 <b>다른 사람 후기</b>를 함께 확인할 수 있습니다.
    </div>
    <div id="effects-detail-body" class="small"></div>
  </div>

    </section>

    <!-- 3-4 배너/정보 -->
    <section class="panel" id="extra-section-banner">
      <div class="panel-title">
        <div class="panel-title-left">
          <span>카페인 정보 / 줄이기 캠페인</span>
          <span class="small">지식인 크롤링 결과(파일) 기반 인기 상품 + 캠페인</span>
        </div>
        <button type="button" class="btn btn-ghost" onclick="openBannerDetail()">전체 화면</button>
      </div>
      <div class="small">
        아래 표는 <code>popular_products.json</code> 파일(지식인 크롤링 전처리 결과)을 불러와서 구성합니다.
        파일이 없거나 읽기에 실패하면, 샘플 데이터를 대신 보여줍니다.
      </div>
      <div class="banner-cards">

        <!-- 좌측: 지식인 크롤링 -->
        <div class="banner-card" style="flex:1.6;">
          <div class="banner-card-title">📦 지식인 기반 유명 음료·식품 카페인</div>
          <div class="small">
            <label style="display:block; margin-bottom:4px;">키워드 입력 (선택)</label>
            <div class="row" style="align-items:flex-end;">
              <div style="flex:2; min-width:140px;">
                <input type="text" id="naver-keyword-input" placeholder="예: 에너지 드링크, 캔커피, 콜라" />
              </div>
              <div style="flex:1; min-width:120px;">
                <button type="button" class="btn btn-outline" id="naver-fetch-btn">
                  데이터 불러오기(지식인 기반)
                </button>
              </div>
            </div>
            <div class="small" id="naver-fetch-hint" style="margin-top:4px;">
              * 버튼을 누르면 같은 폴더의 <b>popular_products.json</b> 파일을 읽어와 목록을 보여줍니다.
              (파일이 없으면 샘플 데이터를 사용)
            </div>
          </div>
          <div class="small" style="margin-top:6px; max-height:220px; overflow:auto;">
            <table style="width:100%; border-collapse:collapse; font-size:0.78rem;">
              <thead>
                <tr>
                  <th style="text-align:left; padding:4px; border-bottom:1px solid #a7f3d0;">순위</th>
                  <th style="text-align:left; padding:4px; border-bottom:1px solid #a7f3d0;">상품명</th>
                  <th style="text-align:left; padding:4px; border-bottom:1px solid #a7f3d0;">유형</th>
                  <th style="text-align:right; padding:4px; border-bottom:1px solid #a7f3d0;">등장 빈도</th>
                  <th style="text-align:right; padding:4px; border-bottom:1px solid #a7f3d0;">예상 카페인(mg)</th>
                </tr>
              </thead>
              <tbody id="popular-products-body"></tbody>
            </table>
          </div>
        </div>

        <!-- 우측: 카페인 줄이기 캠페인 -->
        <div class="banner-card">
          <div class="banner-card-title">🌱 카페인 줄이기 캠페인/방법</div>
          <ul class="small">
            <li>오후 4시 이후 카페인 대신 물·무카페인 티 마시기</li>
            <li>일일 최대 섭취량을 정해두고 앱에서 초과 시 알림 받기</li>
            <li>친구들과 “노카페인 챌린지” 주간 운영하기</li>
          </ul>
          <div class="small" style="margin-top:4px;">
            학교·보건소·지자체에서 진행하는 <b>카페인 줄이기 캠페인</b> 사이트를 연결하는 버튼을 둘 수 있습니다.
          </div>
        </div>
      </div>
    </section>
  </div>
</div>

<!-- 플로팅 버튼 -->
<div id="fab-menu-button">＋</div>
<div id="fab-overlay">
  <div id="fab-menu">
    <button onclick="openIntake()">📒 카페인 기록</button>
    <button onclick="openStatsDetail()">📊 그래프/통계(세부)</button>
    <button onclick="showExtraCombined()">📚 추가 기능 전체</button>
    <button onclick="showHome()">🏠 기본 화면</button>
  </div>
</div>

<!-- 하단 고정 버튼 -->
<nav class="bottom-nav">
  <div class="bottom-nav-inner">
    <button class="nav-pill" onclick="openIntake()">
      <div class="nav-dot"></div>
      <span>오늘 카페인 섭취, 바로 기록하기</span>
    </button>
  </div>
</nav>

<script>
  const HALF_LIFE_HOURS = 5;
  const DEFAULT_WEIGHT_KG = 60;
  let userProfile = { weightKg: DEFAULT_WEIGHT_KG };
  let RECOMMENDED_MG = Math.round(DEFAULT_WEIGHT_KG * 2.5);
  let MAX_MG = RECOMMENDED_MG * 1.5;

  let intakes = [];
  let sideEffects = [];
  let currentEditId = null;
  let extraDetailMode = null;
  let userProductShortcuts = [];

  const POPULAR_PRODUCTS_SAMPLE = [
    { rank:1, name:"몬스터 에너지", category:"샘플", count:120, caffeineMg:100 },
    { rank:2, name:"레드불", category:"샘플", count:95, caffeineMg:80 },
    { rank:3, name:"핫식스", category:"샘플", count:80, caffeineMg:60 },
    { rank:4, name:"조지아 에메랄드 마운틴", category:"샘플", count:50, caffeineMg:120 },
    { rank:5, name:"코카콜라", category:"샘플", count:45, caffeineMg:25 }
  ];

  // 지식인/표준 정보를 모아두는 간단한 상품 DB
// 지식인/표준 정보를 모아두는 간단한 상품 DB (이마트24 기준 RTD + 에너지드링크)
const PRODUCT_DB = [
  /* =======================
   *  에너지 드링크 (이마트24)
   * ======================= */
  {
    keyWords: ["몬스터", "몬스터에너지", "몬스터 에너지", "monster", "monster energy"],
    brand: "몬스터",
    store: "이마트24",
    name: "몬스터 에너지 355ml",
    caffeineMg: 100,
    volumeMl: 355,
    category: "에너지 드링크"
  },
  {
    keyWords: ["핫식스", "핫식스더킹", "핫식스 더킹", "hot6", "hot six", "the king"],
    brand: "핫식스",
    store: "이마트24",
    name: "핫식스 더킹 355ml",
    caffeineMg: 100,
    volumeMl: 355,
    category: "에너지 드링크"
  },
  {
    keyWords: ["핫식스", "핫식스더킹", "핫식스 더킹", "hot6", "hot six", "the king"],
    brand: "핫식스",
    store: "이마트24",
    name: "핫식스 더킹 500ml",
    caffeineMg: 140,
    volumeMl: 500,
    category: "에너지 드링크"
  },
  {
    keyWords: ["레드불", "red bull", "redbull"],
    brand: "레드불",
    store: "이마트24",
    name: "레드불 250ml",
    caffeineMg: 62.5,
    volumeMl: 250,
    category: "에너지 드링크"
  },

  /* =======================
   *  스타벅스 RTD (캔/보틀)
   * ======================= */
  {
    keyWords: ["스타벅스", "더블샷바닐라", "더블샷 바닐라", "더블샷", "바닐라 더블샷"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 더블샷 바닐라 200ml(캔/보틀)",
    caffeineMg: 140,
    volumeMl: 200,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "더블샷바닐라", "더블샷 바닐라", "더블샷", "바닐라 더블샷"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 더블샷 바닐라 275ml(캔/보틀)",
    caffeineMg: 193,
    volumeMl: 275,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "더블샷에스프레소크림", "더블샷 에스프레소 크림", "더블샷크림"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 더블샷 에스프레소 크림 200ml",
    caffeineMg: 103,
    volumeMl: 200,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "더블샷에스프레소크림", "더블샷 에스프레소 크림", "더블샷크림"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 더블샷 에스프레소 크림 275ml",
    caffeineMg: 142,
    volumeMl: 275,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "더블샷돌체", "더블샷 돌체", "돌체 더블샷"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 더블샷 돌체 275ml",
    caffeineMg: 193,
    volumeMl: 275,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "파이크플레이스로스트블랙", "파이크 플레이스 로스트 블랙", "파이크플레이스", "파이크 플레이스"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 파이크 플레이스 로스트 블랙 200ml",
    caffeineMg: 107,
    volumeMl: 200,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "파이크플레이스로스트블랙", "파이크 플레이스 로스트 블랙", "파이크플레이스", "파이크 플레이스"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 파이크 플레이스 로스트 블랙 275ml",
    caffeineMg: 147,
    volumeMl: 275,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "카페베로나블랙", "카페 베로나 블랙", "베로나"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 카페 베로나 블랙 275ml",
    caffeineMg: 151,
    volumeMl: 275,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "오리지날", "오리지널", "starbucks original"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 오리지날 281ml",
    caffeineMg: 102,
    volumeMl: 281,
    category: "RTD 커피(캔/보틀)"
  },
  {
    keyWords: ["스타벅스", "모카", "스타벅스 모카"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 모카 281ml",
    caffeineMg: 82,
    volumeMl: 281,
    category: "RTD 커피(캔/보틀)"
  },

  /* =======================
   *  스타벅스 컵 제품
   * ======================= */
  {
    keyWords: ["스타벅스", "바닐라", "컵바닐라", "스타벅스 컵 바닐라"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 바닐라 200ml(컵)",
    caffeineMg: 92,
    volumeMl: 200,
    category: "컵 커피"
  },
  {
    keyWords: ["스타벅스", "카페라떼", "카페 라떼", "라떼", "컵라떼"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 카페라떼 200ml(컵)",
    caffeineMg: 92,
    volumeMl: 200,
    category: "컵 커피"
  },
  {
    keyWords: ["스타벅스", "카페라떼", "카페 라떼", "라떼", "컵라떼"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 카페라떼 320ml(컵)",
    caffeineMg: 147,
    volumeMl: 320,
    category: "컵 커피"
  },
  {
    keyWords: ["스타벅스", "카페모카", "카페 모카", "모카", "컵모카"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 카페모카 320ml(컵)",
    caffeineMg: 147,
    volumeMl: 320,
    category: "컵 커피"
  },

  /* =======================
   *  스타벅스 PET/펫
   * ======================= */
  {
    keyWords: ["스타벅스", "밀크티", "스타벅스 밀크티"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 밀크티 325ml(PET)",
    caffeineMg: 116,
    volumeMl: 325,
    category: "티/밀크티"
  },
  {
    keyWords: ["스타벅스", "셀렉트바닐라라떼", "셀렉트 바닐라 라떼"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 셀렉트 바닐라 라떼 300ml(PET)",
    caffeineMg: 133,
    volumeMl: 300,
    category: "RTD 커피(PET)"
  },
  {
    keyWords: ["스타벅스", "셀렉트카페라떼", "셀렉트 카페 라떼"],
    brand: "스타벅스",
    store: "이마트24",
    name: "스타벅스 셀렉트 카페 라떼 300ml(PET)",
    caffeineMg: 133,
    volumeMl: 300,
    category: "RTD 커피(PET)"
  },

  /* =======================
   *  매일 바리스타 (컵)
   * ======================= */
  {
    keyWords: ["매일", "바리스타", "에스프레소라떼", "에스프레소 라떼"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 에스프레소 라떼 250ml(컵)",
    caffeineMg: 110,
    volumeMl: 250,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "로어슈거에스프레소라떼", "로어슈거 에스프레소 라떼", "로슈거"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 로어슈거 에스프레소 라떼 250ml(컵)",
    caffeineMg: 115,
    volumeMl: 250,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "모카프레소", "모카 프레소"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 모카프레소 250ml(컵)",
    caffeineMg: 95,
    volumeMl: 250,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "카라멜딥프레소", "카라멜 딥프레소"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 카라멜 딥프레소 250ml(컵)",
    caffeineMg: 100,
    volumeMl: 250,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "스모키로스티드라떼", "스모키 로스티드 라떼"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 스모키 로스티드 라떼 250ml(컵)",
    caffeineMg: 113,
    volumeMl: 250,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "마다가스카르바닐라빈라떼", "마다가스카르 바닐라빈 라떼", "바닐라빈 라떼"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 마다가스카르 바닐라빈 라떼 325ml(컵)",
    caffeineMg: 105,
    volumeMl: 325,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "벨지엄쇼콜라모카", "벨지엄 쇼콜라 모카"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 벨지엄 쇼콜라 모카 325ml(컵)",
    caffeineMg: 125,
    volumeMl: 325,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "돌체라떼", "돌체 라떼"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 돌체 라떼 325ml(컵)",
    caffeineMg: 130,
    volumeMl: 325,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "시그니처드립라떼", "시그니처 드립 라떼"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 시그니처 드립 라떼 325ml(컵)",
    caffeineMg: 160,
    volumeMl: 325,
    category: "컵 커피"
  },
  {
    keyWords: ["매일", "바리스타", "콜드브루블랙", "콜드 브루 블랙", "콜드브루"],
    brand: "매일 바리스타",
    store: "이마트24",
    name: "바리스타 콜드브루 블랙 325ml(컵)",
    caffeineMg: 165,
    volumeMl: 325,
    category: "콜드브루/블랙"
  }
];

// ===== [SYLLABLE_MATCH_UTIL] 상품명 음절(글자) 단위 매칭 유틸 =====
function normalizeKorText(text) {
  return (text || '')
    .toLowerCase()
    .replace(/\s+/g, '')               // 공백 제거
    .replace(/[^0-9가-힣a-z]/g, '');    // 한글/숫자/영문 외 제거
}

// baseStr: DB에 있는 상품명이나 키워드
// ocrText: OCR로 추출된 전체 텍스트
// 반환값: 0~1 (1이면 baseStr의 모든 글자가 ocrText에 등장)
function syllableMatchScore(baseStr, ocrText) {
  const base = normalizeKorText(baseStr);
  const txt  = normalizeKorText(ocrText);
  if (!base || !txt) return 0;

  let matched = 0;
  for (const ch of base) {
    if (txt.includes(ch)) matched++;
  }
  return matched / base.length;
}

// OCR 텍스트와 가장 잘 맞는 상품(DB)을 찾는 함수
function findProductBySyllables(ocrText) {
  let bestProduct = null;
  let bestScore = 0;

  for (const p of PRODUCT_DB) {
    const candidates = [p.name, ...(p.keyWords || [])];

    for (const cand of candidates) {
      const score = syllableMatchScore(cand, ocrText);

      // 1. 모든 글자가 포함된 "완전매칭"이면 바로 채택
      if (score === 1 && normalizeKorText(cand).length > 0) {
        return p;
      }

      // 2. 완전매칭은 아니지만 꽤 높은 유사도(예: 0.7 이상)를 가진 경우
      if (score > bestScore && score >= 0.7) {
        bestScore = score;
        bestProduct = p;
      }
    }
  }

  return bestProduct;  // 없으면 null
}

const KFD_CAFFEINE_DB = [{"name":"커피_더블에스프레소","caffeineMg":395.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소","caffeineMg":346.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 마키아또 (Solo)","caffeineMg":340.91,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 콘 파나 (Solo)","caffeineMg":340.91,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 (Solo)","caffeineMg":340.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소","caffeineMg":340.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소","caffeineMg":339.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 마끼아또","caffeineMg":291.43,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에소프레소 핫(HOT) (싱글)","caffeineMg":248.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소","caffeineMg":244.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에소프레소 핫(HOT) (더블)","caffeineMg":242.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 핫(HOT) (더블)","caffeineMg":234.48,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 핫(HOT) (싱글)","caffeineMg":234.48,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_제주 말차 할리치노","caffeineMg":194.0,"basis":"354mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_더치 라떼","caffeineMg":167.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치아메리카노","caffeineMg":167.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"제주 말차 라떼 핫(HOT) L","caffeineMg":159.0,"basis":"473mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_콜드브루 모카 할리치노","caffeineMg":137.0,"basis":"354mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_시그니처 더 블랙 콜드 브루 보틀","caffeineMg":136.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_제주 말차 라떼 아이스(ICED)","caffeineMg":129.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_제주 말차 라떼 핫(HOT)","caffeineMg":129.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼","caffeineMg":124.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛아메리카노","caffeineMg":124.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 마끼아또","caffeineMg":122.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 1리터","caffeineMg":122.18,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 피에노","caffeineMg":121.95,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 커피 아이스(ICED)","caffeineMg":118.57,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 시트러스","caffeineMg":111.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소","caffeineMg":109.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼","caffeineMg":104.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노","caffeineMg":104.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또","caffeineMg":104.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼","caffeineMg":104.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카","caffeineMg":104.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_원조커피 핫(HOT)","caffeineMg":104.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 콘파냐","caffeineMg":97.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_콜드브루 할리치노","caffeineMg":91.0,"basis":"354mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_사케라또 비안코 오버 아이스(ICED) (Tall)","caffeineMg":88.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헥사메리카노 핫(HOT)","caffeineMg":84.24,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_라벤더 블론드 스타벅스 더블 샷","caffeineMg":82.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":81.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":81.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":79.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_빽’s 카페 라떼 핫(HOT)","caffeineMg":79.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아포가토","caffeineMg":78.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리치노 아이스(ICED)","caffeineMg":77.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루라떼 아이스(ICED)","caffeineMg":76.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루라떼 핫(HOT)","caffeineMg":76.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":76.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 핫(HOT)","caffeineMg":75.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 카페 라떼 핫(HOT)","caffeineMg":75.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_큐브 아이스(ICED)","caffeineMg":74.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT)","caffeineMg":74.59,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":74.18,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아포카토","caffeineMg":73.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 플랫 화이트 (Tall)","caffeineMg":73.24,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_오늘의 커피 (Tall)","caffeineMg":73.24,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":72.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 카푸치노 N2","caffeineMg":72.86,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 블랙 N2","caffeineMg":72.86,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 스타벅스 더블 샷","caffeineMg":72.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_커피 스타벅스 더블 샷","caffeineMg":72.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 스타벅스 더블 샷","caffeineMg":72.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아포가토 (R)","caffeineMg":71.54,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리치노 라떼 아이스(ICED)","caffeineMg":70.44,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED) (L)","caffeineMg":69.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블돌체 라떼 핫(HOT) (L)","caffeineMg":69.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_나이트로 콜드 브루 (Tall)","caffeineMg":69.01,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_자바 초코렛 칩 스노우","caffeineMg":68.99,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 (L)","caffeineMg":68.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 핫(HOT)","caffeineMg":67.71,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":67.71,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_럼 샷 코르타도 (Short)","caffeineMg":67.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 카페 라떼 핫(HOT) (J)","caffeineMg":67.02,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스크림_아포가토","caffeineMg":66.67,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"라떼_제주 말차 카페 라떼 핫(HOT)","caffeineMg":66.07,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED)","caffeineMg":66.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":65.94,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_프리미엄 블렌드 아메리카노 아이스(ICED)","caffeineMg":65.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_프리미엄 블렌드 아메리카노 핫(HOT)","caffeineMg":65.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":65.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트모카 핫(HOT)","caffeineMg":65.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_나이트로 바닐라 크림 (Tall)","caffeineMg":65.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헥사메리카노 아이스(ICED)","caffeineMg":64.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 (R)","caffeineMg":64.71,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 아이스(ICED)","caffeineMg":63.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 핫(HOT)","caffeineMg":63.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_과테말라 누에보 오리엔테","caffeineMg":63.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브라질 만티게이라 BSCA","caffeineMg":63.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에티오피아 게라","caffeineMg":63.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_케냐 니에리","caffeineMg":63.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_청자다방커피","caffeineMg":63.47,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_쿠키&크림 스노우","caffeineMg":62.9,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_원조커피 아이스(ICED) 빽사이즈","caffeineMg":62.84,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트모카 핫(HOT)","caffeineMg":62.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 카페 라떼 핫(HOT)","caffeineMg":62.77,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_원조커피 아이스(ICED)","caffeineMg":62.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블돌체 라떼 아이스(ICED) (L)","caffeineMg":62.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아포가토","caffeineMg":62.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 (L)","caffeineMg":61.11,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼","caffeineMg":61.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_롱블랫 핫(HOT) (Short)","caffeineMg":60.34,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바나나 달달 커피 핫(HOT)","caffeineMg":60.3,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_앗메리카노 핫(HOT)","caffeineMg":59.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 빈 라떼 아이스(ICED) (Tall)","caffeineMg":59.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 빈 라떼 핫(HOT) (Tall)","caffeineMg":59.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_사케라또 아포가토 (Tall)","caffeineMg":59.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_클래식 아포가토 (Tall)","caffeineMg":59.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_그린티 스노우","caffeineMg":58.15,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_허니큐브 아이스(ICED) (R)","caffeineMg":58.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_녹차 샷 라떼 핫(HOT)","caffeineMg":56.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m D 아이스(ICED) (M)","caffeineMg":55.84,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더벤티사이즈 카페 라떼 아이스(ICED)","caffeineMg":55.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_달달연유 라떼 핫(HOT)","caffeineMg":55.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":55.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":55.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 (R)","caffeineMg":55.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 핫(HOT)","caffeineMg":54.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블돌체 라떼 핫(HOT) (R)","caffeineMg":54.71,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_그린티도피오 라떼 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_그린티도피오 라떼 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카 프라페","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 라떼 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 라떼 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜 프라페","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카라멜모카 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_코코프레소","caffeineMg":54.65,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_피넛 라떼 아이스(ICED)","caffeineMg":54.47,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":53.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_벨벳 다크 모카 나이트로 (Tall)","caffeineMg":53.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드 브루 몰트 (Tall)","caffeineMg":53.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드 브루 플로트 (Tall)","caffeineMg":53.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_그린티 아이스샷","caffeineMg":53.25,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":53.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_큐브 라떼 아이스(ICED)","caffeineMg":53.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜커피 프라페 (L)","caffeineMg":52.85,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_모카 카페 라떼 핫(HOT) (J)","caffeineMg":52.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 핫(HOT) (J)","caffeineMg":52.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_원조빽스치노","caffeineMg":52.32,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_싱글오리진 스페셜티","caffeineMg":52.14,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 카페 라떼 핫(HOT) (J)","caffeineMg":52.01,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":52.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 핫(HOT) (L)","caffeineMg":51.93,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":51.83,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":51.83,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (R)","caffeineMg":51.83,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (R)","caffeineMg":51.83,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민우롱 밀크티 핫(HOT)","caffeineMg":51.39,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_로얄 밀크티 라떼 아이스(ICED)","caffeineMg":51.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_로얄 밀크티 라떼 핫(HOT)","caffeineMg":51.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_더벤티사이즈 아메리카노 아이스(ICED)","caffeineMg":50.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_제주 말차 카페 라떼 아이스(ICED)","caffeineMg":50.74,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":50.63,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜커피 프라페 (Max)","caffeineMg":50.59,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":50.23,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_약과 크림커피 아이스(ICED)","caffeineMg":49.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_약과 크림커피 핫(HOT)","caffeineMg":49.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_빽’s 카페 라떼 아이스(ICED) 빽사이즈","caffeineMg":49.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_앗메리카노 아이스(ICED) 빽사이즈","caffeineMg":49.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (J)","caffeineMg":49.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_허니큐브 아이스(ICED) (L)","caffeineMg":49.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카칩커피 프라페 (L)","caffeineMg":49.26,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_카라멜커피 프라페 (R)","caffeineMg":48.79,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_바닐라카페 라떼 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스페니쉬연유카페 라떼 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리키토 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아이스크림카페 라떼 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑임자카페 라떼 아이스(ICED) (Max)","caffeineMg":48.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 콜드브루 아이스(ICED)","caffeineMg":48.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스크림_바닐라아포가토","caffeineMg":48.43,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"커피_롱블랫 아이스(ICED) (Short)","caffeineMg":48.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_숏카페 라떼 아이스(ICED) (Short)","caffeineMg":48.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_숏카페 라떼 핫(HOT) (Short)","caffeineMg":48.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바나나 달달 커피 아이스(ICED)","caffeineMg":48.26,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_베트남 연유 커피 아이스(ICED)","caffeineMg":48.26,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_코코넛 더치","caffeineMg":48.17,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_데일리오트코코넛 라떼 핫(HOT) (L)","caffeineMg":48.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_블론드 바닐라 더블 샷 마키아또 아이스(ICED) (Tall)","caffeineMg":47.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_블론드 바닐라 더블 샷 마키아또 핫(HOT) (Tall)","caffeineMg":47.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED) (L)","caffeineMg":47.78,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블샷 바닐라 딜라이트 아이스(ICED)","caffeineMg":47.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블샷 바닐라 딜라이트 핫(HOT)","caffeineMg":47.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_버터스카치폼 에스프레소 블렌디드","caffeineMg":47.65,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_데일리오트코코넛 라떼 아이스(ICED) (Max)","caffeineMg":47.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED) (Max)","caffeineMg":47.21,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED) (Max)","caffeineMg":47.21,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_토피넛 샷 라떼 핫(HOT)","caffeineMg":47.06,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카칩커피 프라페 (Max)","caffeineMg":47.04,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_콜드브루","caffeineMg":46.99,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브루잉 케냐AA","caffeineMg":46.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블돌체 라떼 아이스(ICED) (R)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트카페모카 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT) (L)","caffeineMg":46.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":46.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":46.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":46.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 시다모","caffeineMg":46.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 아이스(ICED)","caffeineMg":45.87,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브루잉 콜롬비아","caffeineMg":45.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라카페 라떼 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라카페 라떼 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스페니쉬연유카페 라떼 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스페니쉬연유카페 라떼 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아이스크림카페 라떼 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑임자카페 라떼 아이스(ICED) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑임자카페 라떼 핫(HOT) (L)","caffeineMg":45.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카칩커피 프라페 (R)","caffeineMg":45.41,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_녹차 샷 라떼 아이스(ICED)","caffeineMg":45.11,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":45.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":44.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 다크리카노 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 다크리카노 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라다크리카노 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라다크리카노 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라딥 라떼 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라딥 라떼 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_에스프레소 쉐이크","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_연유 라떼 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 라떼 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_오트카페 라떼 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_오트카페 라떼 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 다크리카노 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 다크리카노 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 딥 라떼 아이스(ICED)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 딥 라떼 핫(HOT)","caffeineMg":44.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브루잉 블랙와인","caffeineMg":44.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (J)","caffeineMg":44.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"기타차_레몬&오렌지홍차티 핫(HOT)","caffeineMg":44.06,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":44.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED)","caffeineMg":43.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT)","caffeineMg":43.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브루잉 블라썸","caffeineMg":43.83,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시그니처아메리카노 핫(HOT)","caffeineMg":43.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_버터스카치폼 아인슈페너 핫(HOT)","caffeineMg":43.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":43.41,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바나리카노 아이스(ICED)","caffeineMg":43.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 아이스(ICED) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 핫(HOT) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 아이스(ICED) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 핫(HOT) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 아이스(ICED) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 핫(HOT) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (L)","caffeineMg":43.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_퐁당치노 원조커피","caffeineMg":43.07,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아인슈페너 아이스(ICED)","caffeineMg":43.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_바닐라 크럼블 아이스크림 라떼 아이스(ICED)","caffeineMg":43.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_그린 밀크티 핫(HOT)","caffeineMg":42.93,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_카페 연유다 아이스(ICED)","caffeineMg":42.93,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_원조빽스치노 소프트","caffeineMg":42.75,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_싱글오리진 동티모르","caffeineMg":42.63,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 케냐 AA","caffeineMg":42.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 아이스(ICED)","caffeineMg":42.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":42.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":42.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 카페 라떼 아이스(ICED)","caffeineMg":42.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드 브루 (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 크림 콜드 브루 (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스타벅스 돌체 라떼 아이스(ICED) (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스타벅스 돌체 라떼 핫(HOT) (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 아메리카노 아이스(ICED) (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 아메리카노 핫(HOT) (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드 브루 (Tall)","caffeineMg":42.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시나몬 카페 라떼 핫(HOT)","caffeineMg":42.11,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":42.06,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED) (R)","caffeineMg":42.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_녹차 프라페","caffeineMg":42.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_콜드브루 딜라이트 아이스(ICED)","caffeineMg":41.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":41.81,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_브루잉 아리차","caffeineMg":41.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_녹차 빽스치노","caffeineMg":41.6,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아이스크림 바닐라 라떼 아이스(ICED)","caffeineMg":41.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아이스크림 카페모카 아이스(ICED)","caffeineMg":41.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_블랙티 핫(HOT) (L)","caffeineMg":41.55,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_하동 호지 밀크티 핫(HOT) (L)","caffeineMg":41.55,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_돌체 콜드 브루 라떼 아이스(ICED)","caffeineMg":41.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m B 아이스(ICED) (M)","caffeineMg":41.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_데일리오트코코넛 라떼 핫(HOT) (R)","caffeineMg":41.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 아이스(ICED) (L)","caffeineMg":41.44,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_하동 호지 밀크티 핫(HOT) (J)","caffeineMg":41.44,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_모카 프라페 (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_민트카페모카 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_바닐라 프라페 (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜 프라페 (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED) (L)","caffeineMg":41.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":41.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_샥 라떼 아이스(ICED)","caffeineMg":41.1,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트모카 아이스(ICED)","caffeineMg":40.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":40.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트모카 아이스(ICED)","caffeineMg":40.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_밀크카라멜마키아또 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시나몬 라떼 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 라떼 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_제로슈가 스위트 아메리카노 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_피스타치오 카페 라떼 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_허니아메리카노 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛아메리카노 핫(HOT)","caffeineMg":40.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_데일리오트코코넛 라떼 아이스(ICED) (L)","caffeineMg":40.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 예가체프","caffeineMg":40.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (XL)","caffeineMg":40.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (L)","caffeineMg":40.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라카페 라떼 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라카페 라떼 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스페니쉬연유카페 라떼 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아이스크림카페 라떼 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑임자카페 라떼 핫(HOT) (R)","caffeineMg":40.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":40.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"우롱차_우롱티 핫(HOT) (L)","caffeineMg":39.61,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"라떼_제주말차 라떼 핫(HOT) (L)","caffeineMg":39.55,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민우롱 밀크티 아이스(ICED)","caffeineMg":39.53,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_달달연유 라떼 아이스(ICED)","caffeineMg":39.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":39.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_커피 아이스(ICED) (Tall)","caffeineMg":39.44,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":39.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":39.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 핫(HOT) (R)","caffeineMg":39.15,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 말차 밀크티 핫(HOT) (L)","caffeineMg":39.07,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_그린 밀크티 아이스(ICED)","caffeineMg":38.84,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_플랫화이트 핫(HOT)","caffeineMg":38.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED)","caffeineMg":38.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 핫(HOT) (L)","caffeineMg":38.69,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_싱글오리진 콜롬비아","caffeineMg":38.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (XL)","caffeineMg":38.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (L)","caffeineMg":38.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 아이스(ICED) (R)","caffeineMg":38.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 핫(HOT) (R)","caffeineMg":38.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 아이스(ICED) (R)","caffeineMg":38.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 핫(HOT) (R)","caffeineMg":38.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_버터스카치폼 아인슈페너 아이스(ICED)","caffeineMg":38.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT)","caffeineMg":38.05,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 커피 핫(HOT)","caffeineMg":38.05,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT)","caffeineMg":37.99,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_제주말차 라떼 핫(HOT) (XL)","caffeineMg":37.95,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_빽’s 카페 라떼 아이스(ICED)","caffeineMg":37.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_앗메리카노 아이스(ICED)","caffeineMg":37.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마키아또 아이스(ICED)","caffeineMg":37.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":37.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 아이스(ICED)","caffeineMg":37.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED)","caffeineMg":37.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 커피 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아몬드 라떼 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 모카 핫(HOT)","caffeineMg":37.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_토피넛 샷 라떼 아이스(ICED)","caffeineMg":37.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_니트로커피","caffeineMg":37.44,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드 브루 아메리카노 아이스(ICED)","caffeineMg":37.42,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":37.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":37.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":37.06,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_어른커피","caffeineMg":36.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루오리지널 핫(HOT)","caffeineMg":36.72,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED)","caffeineMg":36.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 핫(HOT)","caffeineMg":36.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_더블 에스프레소 칩 프라푸치노 (Tall)","caffeineMg":36.62,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아이스크림 카페 라떼 아이스(ICED)","caffeineMg":36.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":36.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":36.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_그린티 카페 라떼 아이스(ICED)","caffeineMg":36.06,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_그린티 카페 라떼 핫(HOT)","caffeineMg":36.06,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마키아또 아이스(ICED)","caffeineMg":35.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마키아또 핫(HOT)","caffeineMg":35.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":35.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":35.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":35.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":35.79,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":35.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":35.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 아이스(ICED) (R)","caffeineMg":35.51,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티+펄 핫(HOT) (L)","caffeineMg":35.51,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_헤이즐넛아메리카노 핫(HOT)","caffeineMg":35.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티 핫(HOT)","caffeineMg":35.47,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_콜드 브루 라떼 아이스(ICED)","caffeineMg":35.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_하동 호지 밀크티 아이스(ICED) (J)","caffeineMg":35.33,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_데일리오트코코넛 라떼 아이스(ICED) (R)","caffeineMg":35.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 빈 라떼 핫(HOT)","caffeineMg":35.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_하동 호지 밀크티 아이스(ICED) (L)","caffeineMg":35.31,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_꼰대 라떼 핫(HOT)","caffeineMg":35.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_바닐라라떼 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_바닐라라떼 핫(HOT)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체라떼 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 라떼 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페라떼 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페라떼 핫(HOT)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛라떼 아이스(ICED)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛라떼 핫(HOT)","caffeineMg":35.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 핫(HOT) (J)","caffeineMg":35.1,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_돌체 카페 라떼 핫(HOT) (L)","caffeineMg":35.02,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_티라미수 라떼 핫(HOT)","caffeineMg":35.01,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":34.97,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m D 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m D 핫(HOT) (L)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED) (L)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT) (L)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m D 핫(HOT) (L)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m D 아이스(ICED) (M)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m D 핫(HOT) (L)","caffeineMg":34.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT)","caffeineMg":34.62,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":34.55,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스페니쉬연유카페 라떼 아이스(ICED) (R)","caffeineMg":34.54,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_커피밀크쉐이크 (R)","caffeineMg":34.54,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_흑임자카페 라떼 아이스(ICED) (R)","caffeineMg":34.54,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 스페셜티 아이스(ICED)","caffeineMg":34.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 핫(HOT) (L)","caffeineMg":34.3,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"커피_민트카페모카 핫(HOT)","caffeineMg":34.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":34.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":34.08,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_녹차 빽스치노 소프트","caffeineMg":33.99,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_돌체 카페 라떼 아이스(ICED) (J)","caffeineMg":33.95,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_에스프레소 프라푸치노 (Tall)","caffeineMg":33.8,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_클래식 밀크티 핫(HOT)","caffeineMg":33.8,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"아이스티_아이스티 샷추가 (L)","caffeineMg":33.79,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"커피_꿀아메리카노 핫(HOT)","caffeineMg":33.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":33.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_모카 카페 라떼 아이스(ICED) (J)","caffeineMg":33.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 아이스(ICED) (J)","caffeineMg":33.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀아메리카노 아이스(ICED)","caffeineMg":33.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시그니처아메리카노 아이스(ICED)","caffeineMg":33.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트카페모카 아이스(ICED)","caffeineMg":33.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_플랫화이트 아이스(ICED)","caffeineMg":33.21,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라아메리카노 핫(HOT)","caffeineMg":33.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_티라미수 라떼 아이스(ICED)","caffeineMg":33.16,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 카페 라떼 아이스(ICED) (J)","caffeineMg":33.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"복숭아홍차_복숭아 얼그레이 아이스(ICED)","caffeineMg":33.0,"basis":"354mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"복숭아홍차_복숭아 얼그레이 핫(HOT)","caffeineMg":33.0,"basis":"354mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 아이스(ICED) (L)","caffeineMg":32.98,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_빅포즈 아메리카노","caffeineMg":32.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT) (L)","caffeineMg":32.86,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_연유 라떼 핫(HOT)","caffeineMg":32.86,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 말차 밀크티 핫(HOT) (XL)","caffeineMg":32.61,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":32.54,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루","caffeineMg":32.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼","caffeineMg":32.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 연유","caffeineMg":32.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 흑당","caffeineMg":32.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시나몬 카페 라떼 아이스(ICED)","caffeineMg":32.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 모카 핫(HOT)","caffeineMg":32.22,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":32.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":32.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":32.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":32.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m D 아이스(ICED) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m D 아이스(ICED) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m D 아이스(ICED) (L)","caffeineMg":31.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치 블랙 에티오피아 예가체프","caffeineMg":31.72,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치 블랙 케냐AA","caffeineMg":31.72,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 카페 라떼 아이스(ICED) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 카페 라떼 핫(HOT) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트 초콜렛 모카 아이스(ICED) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트 초콜렛 모카 핫(HOT) (EX)","caffeineMg":31.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 카페 라떼 핫(HOT) (L)","caffeineMg":31.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_오리엔탈 라떼 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT)","caffeineMg":31.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼야또 핫(HOT)","caffeineMg":31.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 콜드브루","caffeineMg":31.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼","caffeineMg":31.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아메리카노","caffeineMg":31.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아인슈페너","caffeineMg":31.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 크림넛","caffeineMg":31.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 다크퍼플 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 마일드 그린 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (K(코끼리))","caffeineMg":31.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_프리미엄 블렌드 딥 라떼 아이스(ICED)","caffeineMg":31.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_프리미엄 블렌드 딥 라떼 핫(HOT)","caffeineMg":31.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_밀크카라멜마키아또 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_시나몬 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_제로슈가 스위트 아메리카노 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_크리미 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_피스타치오 카페 라떼 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_허니아메리카노 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛아메리카노 아이스(ICED)","caffeineMg":31.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"탄산음료_쿨 라임 피지오 (Tall)","caffeineMg":30.99,"basis":"100mL","major":"음료 및 차류","rep":"탄산음료","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (J)","caffeineMg":30.57,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_달고나 카페 라떼","caffeineMg":30.54,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED)","caffeineMg":30.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 커피 아이스(ICED)","caffeineMg":30.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 시다모 아이스(ICED)","caffeineMg":30.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_블랙티 핫(HOT) (J)","caffeineMg":30.44,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_모카 카페 라떼 핫(HOT) (L)","caffeineMg":30.43,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (EX)","caffeineMg":30.34,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (EX)","caffeineMg":30.34,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":30.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":30.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_메가리카노 아이스(ICED)","caffeineMg":30.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 라떼 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀 커피 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아몬드 라떼 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 모카 아이스(ICED)","caffeineMg":30.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 콜드브루 (EX)","caffeineMg":29.91,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 (EX)","caffeineMg":29.91,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아메리카노 (EX)","caffeineMg":29.91,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라빈 라떼 핫(HOT)","caffeineMg":29.73,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체콜드브루 아이스(ICED)","caffeineMg":29.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":29.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED)","caffeineMg":29.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_제주 말차 블렌디드","caffeineMg":29.62,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_라벤더 카페 브레베 아이스(ICED) (Tall)","caffeineMg":29.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_라벤더 카페 브레베 핫(HOT) (Tall)","caffeineMg":29.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_스파클링 시트러스 에스프레소 (Tall)","caffeineMg":29.58,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED)","caffeineMg":29.18,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT) (XL)","caffeineMg":29.13,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED) (L)","caffeineMg":28.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT) (L)","caffeineMg":28.75,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (L)","caffeineMg":28.74,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (J)","caffeineMg":28.42,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"빙수_티라미수케이크 빙수","caffeineMg":28.36,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":28.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_솔티카라멜크림 라떼 아이스(ICED) (S)","caffeineMg":28.21,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_자바 칩 프라푸치노 (Tall)","caffeineMg":28.17,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":28.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 동티모르 아이스(ICED)","caffeineMg":28.12,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_싱글오리진 케냐AA 아이스(ICED)","caffeineMg":28.09,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 핫(HOT)","caffeineMg":28.05,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 아이스(ICED) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 핫(HOT) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (EX)","caffeineMg":28.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛아메리카노 아이스(ICED)","caffeineMg":27.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루","caffeineMg":27.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_티라미수 라떼","caffeineMg":27.63,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":27.48,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아몬드 크림 콜드브루","caffeineMg":27.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트카페모카 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_에스프레소 (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 핫(HOT) (R)","caffeineMg":27.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED)","caffeineMg":27.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT)","caffeineMg":27.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_토피넛 라떼 핫(HOT)","caffeineMg":27.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치 썬셋","caffeineMg":27.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치 오션","caffeineMg":27.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트모카 아이스(ICED)","caffeineMg":27.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_민트모카 핫(HOT)","caffeineMg":27.19,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 빈 라떼 아이스(ICED)","caffeineMg":27.12,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"우롱차_우롱티 핫(HOT) (J)","caffeineMg":27.06,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"커피_싱글오리진 예가체프 아이스(ICED)","caffeineMg":26.78,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 모카 아이스(ICED) (Tall)","caffeineMg":26.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 모카 핫(HOT) (Tall)","caffeineMg":26.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꼰대 라떼 아이스(ICED)","caffeineMg":26.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m B 아이스(ICED) (L)","caffeineMg":26.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m B 아이스(ICED) (L)","caffeineMg":26.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m B 아이스(ICED) (L)","caffeineMg":26.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루오리지널 아이스(ICED)","caffeineMg":26.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_블랙티 아이스(ICED) (L)","caffeineMg":26.43,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"라떼_잉글리쉬 브렉퍼스트 라떼 핫(HOT)","caffeineMg":26.43,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_커피 밀크쉐이크","caffeineMg":26.4,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":26.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":26.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_콜드브루 커피 프라페","caffeineMg":26.4,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (L)","caffeineMg":26.33,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":26.3,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_리스트레또 딜라이트 아이스(ICED)","caffeineMg":26.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_리스트레또 딜라이트 핫(HOT)","caffeineMg":26.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 아이스(ICED)","caffeineMg":26.14,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":26.14,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_클래식 밀크티 아이스(ICED)","caffeineMg":26.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m B 아이스(ICED) (M)","caffeineMg":25.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m B 핫(HOT) (L)","caffeineMg":25.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m B 핫(HOT) (L)","caffeineMg":25.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m B 아이스(ICED) (M)","caffeineMg":25.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m B 핫(HOT) (L)","caffeineMg":25.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (L)","caffeineMg":25.89,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"자몽홍차_오렌지자몽블랙티 핫(HOT)","caffeineMg":25.71,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"커피_싱글오리진 콜롬비아 아이스(ICED)","caffeineMg":25.46,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_제주말차 라떼 아이스(ICED) (XL)","caffeineMg":25.45,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 아이스(ICED) (R)","caffeineMg":25.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더블 모카 라떼 핫(HOT) (R)","caffeineMg":25.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카 프라푸치노 (Tall)","caffeineMg":25.35,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (R)","caffeineMg":25.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT) (R)","caffeineMg":25.35,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":25.33,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"우롱차_우롱티 아이스(ICED) (L)","caffeineMg":25.16,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT) (L)","caffeineMg":25.12,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"녹차_해남 녹차 아이스(ICED)","caffeineMg":25.0,"basis":"354mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_해남 녹차 핫(HOT)","caffeineMg":25.0,"basis":"354mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티+펄 핫(HOT) (J)","caffeineMg":24.95,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT) (J)","caffeineMg":24.95,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 핫(HOT) (J)","caffeineMg":24.95,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"커피_아인슈페너 아이스(ICED)","caffeineMg":24.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 핫(HOT)","caffeineMg":24.88,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":24.87,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":24.87,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"코코아_핫초코 핫(HOT)","caffeineMg":24.81,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"커피_카페 모카 아이스(ICED)","caffeineMg":24.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_제주말차 프라페 (L)","caffeineMg":24.74,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 말차 밀크티 아이스(ICED) (XL)","caffeineMg":24.47,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED) (L)","caffeineMg":24.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 핫(HOT) (L)","caffeineMg":24.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼야또 아이스(ICED)","caffeineMg":24.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜 프라푸치노 (Tall)","caffeineMg":23.94,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_화이트 초콜릿 모카 프라푸치노 (Tall)","caffeineMg":23.94,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스티_아이스티 샷추가 (XL)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"커피_오리엔탈 라떼 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED)","caffeineMg":23.89,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_에스프레소 프라페","caffeineMg":23.7,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_제주말차 프라페 (Max)","caffeineMg":23.69,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":23.64,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 핫(HOT) (L)","caffeineMg":23.43,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_레몬아메리카노 아이스(ICED)","caffeineMg":23.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라빈 라떼 아이스(ICED)","caffeineMg":23.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 아이스(ICED)","caffeineMg":23.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED)","caffeineMg":23.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":23.27,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_모카 프라페 (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_민트카페모카 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_바닐라 프라페 (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼그레이 리저브 핫(HOT)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"스무디_카라멜 프라페 (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 라떼 아이스(ICED) (R)","caffeineMg":23.25,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_더블 토피넛 위드샷 아이스(ICED)","caffeineMg":23.19,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_더블 토피넛 위드샷 핫(HOT)","caffeineMg":23.19,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_제주말차 라떼 아이스(ICED) (L)","caffeineMg":23.13,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_돌체 크러쉬 위드 샷","caffeineMg":23.04,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_모카 플랫치노","caffeineMg":23.04,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_화이트 초코 아이스(ICED)","caffeineMg":23.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_화이트 초코 핫(HOT)","caffeineMg":23.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":22.99,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (XL)","caffeineMg":22.96,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티+펄 아이스(ICED) (L)","caffeineMg":22.62,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_바닐라딜라이트 아이스(ICED)","caffeineMg":22.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라딜라이트 핫(HOT)","caffeineMg":22.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_커피 드로잉 말차 프라푸치노 (Tall)","caffeineMg":22.54,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED) (L)","caffeineMg":22.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 핫(HOT) (L)","caffeineMg":22.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라빈 라떼 아이스(ICED)","caffeineMg":22.48,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":22.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 아이스(ICED) (J)","caffeineMg":22.27,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"스무디_제주말차 프라페 (R)","caffeineMg":22.22,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_아이스버블 밀크티 아이스(ICED) (L)","caffeineMg":22.2,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_제주 비자림 콜드 브루 (Grande)","caffeineMg":22.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_카라멜 플랫치노","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 아이스(ICED)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼야또 핫(HOT)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_커피 플랫치노","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_화이트 초콜렛 모카 아이스(ICED)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트 초콜렛 모카 핫(HOT)","caffeineMg":22.03,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 카페 라떼 아이스(ICED)","caffeineMg":21.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_연유 카페 라떼 핫(HOT)","caffeineMg":21.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_자이언트 아메리카노 아이스(ICED)","caffeineMg":21.95,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":21.93,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 아이스(ICED) (L)","caffeineMg":21.78,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 리저브 아이스(ICED)","caffeineMg":21.63,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"코코아_아이스초코 아이스(ICED)","caffeineMg":21.6,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED) (L)","caffeineMg":21.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티 아이스(ICED)","caffeineMg":21.28,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_바닐라빈 라떼 핫(HOT)","caffeineMg":21.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":21.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 핫(HOT)","caffeineMg":21.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT)","caffeineMg":21.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마키아또 아이스(ICED) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마키아또 핫(HOT) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트 초콜릿 모카 아이스(ICED) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_화이트 초콜릿 모카 핫(HOT) (Tall)","caffeineMg":21.13,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아몬드 비엔나 커피","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_헤이즐넛 라떼 핫(HOT)","caffeineMg":21.04,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_달콤 구름 라떼","caffeineMg":20.96,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_카라멜 아이스샷","caffeineMg":20.96,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_코코넛 아이스샷","caffeineMg":20.96,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_커피 프라페","caffeineMg":20.86,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"케이크_떠먹는 티라미수 케이크","caffeineMg":20.69,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"레몬홍차_레몬얼그레이티 핫(HOT)","caffeineMg":20.57,"basis":"100mL","major":"음료 및 차류","rep":"레몬홍차","source":"식품의약품안전처"},{"name":"커피_달고나 아인슈페너 아이스(ICED)","caffeineMg":20.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_달고나 크림커피 아이스(ICED)","caffeineMg":20.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라아메리카노 아이스(ICED)","caffeineMg":20.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"우롱차_피치우롱 핫(HOT)","caffeineMg":20.0,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"라떼_로얄 밀크티 라떼 아이스(ICED)","caffeineMg":19.98,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_흑당콜드브루 (EX)","caffeineMg":19.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 말차 밀크티 아이스(ICED) (L)","caffeineMg":19.85,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_바닐라크림 콜드브루 아이스(ICED)","caffeineMg":19.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼 그레이티 핫(HOT) (Tall)","caffeineMg":19.72,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬 브렉퍼스트티 핫(HOT) (Tall)","caffeineMg":19.72,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"자몽홍차_자몽 허니 블랙티 핫(HOT) (Tall)","caffeineMg":19.72,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"라떼_차이티 라떼 아이스(ICED) (Tall)","caffeineMg":19.72,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_차이티 라떼 핫(HOT) (Tall)","caffeineMg":19.72,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_돌체 카페 라떼 아이스(ICED) (L)","caffeineMg":19.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 라떼 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 마끼아또 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카푸치노 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_헤이즐넛 라떼 아이스(ICED)","caffeineMg":19.52,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_시그니처콜드브루 아이스(ICED)","caffeineMg":19.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":19.37,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_아메리카노 핫(HOT)","caffeineMg":19.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_블랙티 아이스(ICED) (J)","caffeineMg":19.35,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (J)","caffeineMg":19.24,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_카라멜 아이스 블렌디드 (R)","caffeineMg":19.15,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 아이스(ICED) (R)","caffeineMg":19.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜마끼아또 핫(HOT) (R)","caffeineMg":19.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑당 아인슈페너 아이스(ICED)","caffeineMg":19.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑당 아인슈페너 핫(HOT)","caffeineMg":19.15,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_그린티 아이스(ICED) (R)","caffeineMg":19.1,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (L)","caffeineMg":19.08,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_카페 코코다","caffeineMg":19.05,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_키위 스무디","caffeineMg":19.04,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초콜릿 블렌디드","caffeineMg":19.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_하동녹차 프라페","caffeineMg":18.87,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_제주 첫물 차광 녹차 라떼 핫(HOT)","caffeineMg":18.82,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_차이 라떼 아이스(ICED)","caffeineMg":18.82,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_차이 라떼 핫(HOT)","caffeineMg":18.82,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_청포도 그린티+알로에 (J)","caffeineMg":18.74,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"커피_블랙펄 카페 라떼 아이스(ICED)","caffeineMg":18.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":18.67,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_믹스커피 아이스(ICED)","caffeineMg":18.61,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_믹스커피 핫(HOT)","caffeineMg":18.61,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_제주 그린티 스무디","caffeineMg":18.6,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_청포도 그린티+알로에 (L)","caffeineMg":18.6,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"우롱차_피치우롱 아이스(ICED)","caffeineMg":18.6,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (L)","caffeineMg":18.56,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"아이스티_아이스티샷추가 아샷추 빽사이즈","caffeineMg":18.56,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"홍차_블랙티 핫(HOT)","caffeineMg":18.49,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"라떼_얼그레이 밀크티 라떼 아이스(ICED)","caffeineMg":18.31,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_얼그레이 밀크티 라떼 핫(HOT)","caffeineMg":18.31,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_콜드 브루 오트 라떼 (Tall)","caffeineMg":18.31,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페","caffeineMg":18.26,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_모카 카페 라떼 아이스(ICED) (L)","caffeineMg":18.18,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 카페 라떼 아이스(ICED) (L)","caffeineMg":18.18,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_흑당버블그린티 라떼 아이스(ICED)","caffeineMg":18.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_로얄 밀크티 라떼 핫(HOT)","caffeineMg":17.97,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_아이스버블 밀크티 아이스(ICED) (R)","caffeineMg":17.87,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_피치우롱스위티 핫(HOT)","caffeineMg":17.81,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (XL)","caffeineMg":17.68,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_흑당 카페라떼 아이스(ICED)","caffeineMg":17.6,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_브라운샷버블 라떼 아이스(ICED)","caffeineMg":17.45,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_더벤티사이즈 믹스커피 아이스(ICED)","caffeineMg":17.44,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_카라멜 카페 라떼 아이스(ICED) (L)","caffeineMg":17.34,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"우롱차_우롱티 아이스(ICED) (J)","caffeineMg":17.2,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"밀크티/버블티_돌체 블랙 밀크티 핫(HOT) (Tall)","caffeineMg":16.9,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_제주 유기농 말차로 만든 라떼 아이스(ICED) (Tall)","caffeineMg":16.9,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_제주 유기농 말차로 만든 라떼 핫(HOT) (Tall)","caffeineMg":16.9,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_제주 유기농 말차로 만든 크림 프라푸치노 (Tall)","caffeineMg":16.9,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_카페 라떼 아이스(ICED) (L)","caffeineMg":16.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED) (XL)","caffeineMg":16.44,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_레몬허니블랙티 핫(HOT)","caffeineMg":16.41,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"자몽홍차_자몽허니블랙티 핫(HOT)","caffeineMg":16.41,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"스무디_그린티 프라페","caffeineMg":16.34,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_달고나 콜드브루 라떼 핫(HOT)","caffeineMg":16.34,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED) (J)","caffeineMg":16.28,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED) (L)","caffeineMg":16.28,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"사과차_애플 그린티 핫(HOT)","caffeineMg":16.24,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"라떼_제주 첫물 차광 녹차 라떼 아이스(ICED)","caffeineMg":16.07,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티+펄 아이스(ICED) (J)","caffeineMg":15.98,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m D 핫(HOT) (M)","caffeineMg":15.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 아이스(ICED) (M)","caffeineMg":15.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 라떼 핫(HOT) (M)","caffeineMg":15.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m D 핫(HOT) (M)","caffeineMg":15.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑당커피 아이스(ICED) (M)","caffeineMg":15.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_브라운샷버블 라떼 핫(HOT)","caffeineMg":15.86,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_초코바른 제주 그린 스무디","caffeineMg":15.86,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 아이스(ICED) (J)","caffeineMg":15.82,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"아이스크림_로얄밀크티파르페 아이스(ICED) (Short)","caffeineMg":15.79,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"스무디_녹차 바나치노","caffeineMg":15.77,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_돌체 블랙 밀크티 핫(HOT)","caffeineMg":15.75,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_하동녹차 라떼 아이스(ICED)","caffeineMg":15.72,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_버블흑당콜드브루","caffeineMg":15.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 화이트 비엔나","caffeineMg":15.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_흑당콜드브루","caffeineMg":15.7,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬브렉퍼스트 아이스(ICED) (L)","caffeineMg":15.64,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":15.57,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED)","caffeineMg":15.57,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스티_아이스티샷추가 아샷추","caffeineMg":15.5,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"커피_티라미수 번버거 + 아메리카노 SET","caffeineMg":15.2,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_그린티 프라페 (R)","caffeineMg":15.15,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_그린티 프라페 (L)","caffeineMg":15.13,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티 핫(HOT) (J)","caffeineMg":15.01,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티+펄 핫(HOT) (J)","caffeineMg":15.01,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"자몽홍차_오렌지자몽블랙티 아이스(ICED)","caffeineMg":15.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티 핫(HOT) (L)","caffeineMg":14.98,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티+펄 핫(HOT) (L)","caffeineMg":14.98,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_쿠키&크림 번버거 + 아메리카노 SET","caffeineMg":14.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":14.94,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_레몬&오렌지홍차티 아이스(ICED)","caffeineMg":14.91,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 얼 그레이 밀크티 핫(HOT) (Grande)","caffeineMg":14.8,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"허브차_크림얼그레이티 핫(HOT)","caffeineMg":14.74,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT)","caffeineMg":14.57,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_더치라떼 아이스(ICED)","caffeineMg":14.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더치커피 핫(HOT)","caffeineMg":14.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아인슈페너 아이스(ICED)","caffeineMg":14.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":14.29,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_하동녹차 라떼 핫(HOT)","caffeineMg":14.29,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 핫(HOT) (L)","caffeineMg":14.25,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 핫(HOT) (J)","caffeineMg":14.16,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED) (L)","caffeineMg":14.14,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_초코스모어 쿠키","caffeineMg":14.14,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED)","caffeineMg":14.12,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 핫(HOT)","caffeineMg":14.12,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"홍차_얼 그레이티 아이스(ICED) (Tall)","caffeineMg":14.08,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 핫(HOT)","caffeineMg":13.95,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED)","caffeineMg":13.74,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT)","caffeineMg":13.74,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_아쌈티 핫(HOT)","caffeineMg":13.66,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 아이스(ICED) (L)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 핫(HOT) (L)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED) (M)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 핫(HOT) (M)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아이스(ICED) (M)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 핫(HOT) (M)","caffeineMg":13.53,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_바닐라 크림콜드브루 아이스(ICED)","caffeineMg":13.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 크림콜드브루 아이스(ICED)","caffeineMg":13.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_꿀메리카노 I’m B 핫(HOT) (M)","caffeineMg":13.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m B 핫(HOT) (M)","caffeineMg":13.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_아메리카노 I’m D 핫(HOT) (M)","caffeineMg":13.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_제주유기농녹차 아이스(ICED) (L)","caffeineMg":13.32,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"커피_헤이즐넛 아메리카노 I’m B 핫(HOT) (M)","caffeineMg":13.32,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":13.25,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬브렉퍼스트 핫(HOT) (L)","caffeineMg":13.11,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"녹차_하동 녹차 아이스(ICED)","caffeineMg":13.11,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_하동 녹차 핫(HOT)","caffeineMg":13.11,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"커피_달고나 콜드브루 라떼 아이스(ICED)","caffeineMg":13.08,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED) (EX)","caffeineMg":12.92,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT) (EX)","caffeineMg":12.92,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 아이스(ICED)","caffeineMg":12.69,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 핫(HOT)","caffeineMg":12.69,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄밀크 버블티","caffeineMg":12.69,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_자몽 얼그레이티 아이스(ICED)","caffeineMg":12.68,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_레몬허니블랙티 아이스(ICED)","caffeineMg":12.62,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"자몽홍차_자몽허니블랙티 아이스(ICED)","caffeineMg":12.62,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED) (Max)","caffeineMg":12.52,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED) (L)","caffeineMg":12.47,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 핫(HOT) (L)","caffeineMg":12.47,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (L)","caffeineMg":12.47,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_아이스버블 밀크티 라떼 아이스(ICED) (L)","caffeineMg":12.47,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (J)","caffeineMg":12.44,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT)","caffeineMg":12.42,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 핫(HOT) (R)","caffeineMg":12.39,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_달고나카페 라떼 핫(HOT) (R)","caffeineMg":12.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 핫(HOT) (L)","caffeineMg":12.34,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":12.3,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_청포도 그린티 (J)","caffeineMg":12.29,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"케이크_떠먹는 커피쿠키 케이크","caffeineMg":12.28,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED)","caffeineMg":12.28,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_골든펄 돌체 밀크티","caffeineMg":12.26,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_청포도 그린티 (L)","caffeineMg":12.26,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"라떼_제주 말차 라떼 핫(HOT)","caffeineMg":12.09,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"레몬홍차_레몬얼그레이티 아이스(ICED)","caffeineMg":12.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬홍차","source":"식품의약품안전처"},{"name":"허브차_크림얼그레이티 아이스(ICED)","caffeineMg":12.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙펄 밀크티 아이스(ICED)","caffeineMg":11.98,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_피치우롱스위티 아이스(ICED)","caffeineMg":11.97,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_바닐라 탐앤치노","caffeineMg":11.95,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_믹스커피 아이스(ICED)","caffeineMg":11.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"케이크_티라미수 케이크","caffeineMg":11.86,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED) (L)","caffeineMg":11.84,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED) (M)","caffeineMg":11.84,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT) (M)","caffeineMg":11.84,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"복숭아홍차_피치얼그레이 아이스(ICED)","caffeineMg":11.84,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"복숭아홍차_피치얼그레이 핫(HOT)","caffeineMg":11.84,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_아몬드 밀크티 핫(HOT)","caffeineMg":11.63,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 핫(HOT) (L)","caffeineMg":11.42,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 핫(HOT) (XL)","caffeineMg":11.41,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 핫(HOT) (L)","caffeineMg":11.36,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_자몽 블랙 프룻티","caffeineMg":11.33,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT)","caffeineMg":11.29,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬 브렉퍼스트티 아이스(ICED) (Tall)","caffeineMg":11.27,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"녹차_그린티 핫(HOT) (R)","caffeineMg":11.24,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_제주유기농녹차 핫(HOT) (L)","caffeineMg":11.21,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 아이스(ICED)","caffeineMg":11.17,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"우롱차_우롱티 아이스(ICED)","caffeineMg":11.17,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"녹차_녹차 아이스(ICED)","caffeineMg":11.06,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_녹차 핫(HOT)","caffeineMg":11.05,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 얼 그레이 밀크티 아이스(ICED) (Grande)","caffeineMg":10.99,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 핫(HOT) (XL)","caffeineMg":10.93,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"자몽홍차_꿀 자몽 블랙티","caffeineMg":10.92,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 핫(HOT) (L)","caffeineMg":10.87,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_믹스커피 핫(HOT)","caffeineMg":10.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_초콜릿 칩 플랫치노","caffeineMg":10.8,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 핫(HOT) (J)","caffeineMg":10.78,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_민트 초콜릿 칩 플랫치노","caffeineMg":10.7,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED) (R)","caffeineMg":10.63,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"레몬홍차_레몬 얼그레이티 핫(HOT)","caffeineMg":10.63,"basis":"100mL","major":"음료 및 차류","rep":"레몬홍차","source":"식품의약품안전처"},{"name":"라떼_아이스버블 밀크티 라떼 아이스(ICED) (R)","caffeineMg":10.63,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타음료_인크레드불 화이트 아이스(ICED)","caffeineMg":10.58,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"자몽홍차_허니자몽블랙티 핫(HOT)","caffeineMg":10.41,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":10.4,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":10.4,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_녹차 플랫치노","caffeineMg":10.4,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티 아이스(ICED) (L)","caffeineMg":10.36,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티+펄 아이스(ICED) (L)","caffeineMg":10.36,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티 아이스(ICED) (J)","caffeineMg":10.29,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_제주 그린 밀크티+펄 아이스(ICED) (J)","caffeineMg":10.29,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT) (L)","caffeineMg":10.15,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_카페모카 아이스(ICED)","caffeineMg":10.14,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED) (L)","caffeineMg":10.1,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"자몽홍차_허니자몽블랙티 아이스(ICED)","caffeineMg":9.99,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"라떼_딸기 그린티 라떼","caffeineMg":9.88,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_돌체 블랙 밀크티 아이스(ICED) (Tall)","caffeineMg":9.86,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_망고 패션 프루트 블렌디드 (Tall)","caffeineMg":9.86,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"홍차_블랙티 아이스(ICED)","caffeineMg":9.61,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT)","caffeineMg":9.51,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"홍차_얼그레이티 아이스(ICED)","caffeineMg":9.49,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":9.46,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT)","caffeineMg":9.37,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"복숭아홍차_복숭아 얼그레이 아이스(ICED)","caffeineMg":9.32,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"복숭아홍차_복숭아 얼그레이 핫(HOT)","caffeineMg":9.32,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_아몬드 밀크티 아이스(ICED)","caffeineMg":9.31,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_달고나카페 라떼 핫(HOT) (L)","caffeineMg":9.3,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 아이스(ICED) (L)","caffeineMg":9.3,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_제주 말차 라떼 아이스(ICED)","caffeineMg":9.28,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"아이스티_복숭아아이스티 아이스(ICED)","caffeineMg":9.25,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 아이스(ICED) (J)","caffeineMg":9.22,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_카페모카 핫(HOT)","caffeineMg":9.22,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED)","caffeineMg":9.14,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 아이스(ICED) (M)","caffeineMg":8.99,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 핫(HOT) (M)","caffeineMg":8.99,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 핫(HOT) (R)","caffeineMg":8.91,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_제주 그린티 브리즈 (Grande)","caffeineMg":8.88,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"라떼_메가초코 라떼 핫(HOT)","caffeineMg":8.76,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"사과차_애플민트티 아이스(ICED) (R)","caffeineMg":8.7,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"커피_달고나카페 라떼 아이스(ICED) (L)","caffeineMg":8.67,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"허브차_민트 아이스(ICED) (L)","caffeineMg":8.67,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 아이스(ICED) (L)","caffeineMg":8.67,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 아이스(ICED) (J)","caffeineMg":8.6,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜릿 밀크티 핫(HOT)","caffeineMg":8.57,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"아이스티_달콤아이스티","caffeineMg":8.5,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_그릭요거트&밀크티 크러쉬","caffeineMg":8.46,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_딸기 아사이 레모네이드 스타벅스 리프레셔 (Tall)","caffeineMg":8.45,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티 아이스(ICED) (EX)","caffeineMg":8.45,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티 핫(HOT) (EX)","caffeineMg":8.45,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"탄산음료_블랙티 레모네이드 피지오 (Tall)","caffeineMg":8.45,"basis":"100mL","major":"음료 및 차류","rep":"탄산음료","source":"식품의약품안전처"},{"name":"자몽홍차_자몽 허니 블랙티 아이스(ICED) (Tall)","caffeineMg":8.45,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_버터스카치폼 밀크티 아이스(ICED)","caffeineMg":8.42,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_치즈 폼 밀크티 아이스(ICED)","caffeineMg":8.38,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_달고나카페 라떼 아이스(ICED) (R)","caffeineMg":8.21,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"사과차_애플민트티 핫(HOT) (R)","caffeineMg":8.17,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"코코아_초코 아이스(ICED)","caffeineMg":8.17,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"녹차_녹차 핫(HOT)","caffeineMg":8.12,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"라떼_초코 아이스(ICED)","caffeineMg":8.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 핫(HOT)","caffeineMg":8.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_달고나카페 라떼 아이스(ICED) (Max)","caffeineMg":7.95,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜릿 밀크티 아이스(ICED)","caffeineMg":7.95,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_말차스모어 쿠키","caffeineMg":7.89,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED)","caffeineMg":7.85,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_말차초코칩 프라페","caffeineMg":7.78,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 아이스(ICED)","caffeineMg":7.75,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"마카롱_메가초코 마카롱","caffeineMg":7.6,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_그린티 라떼 아이스(ICED) (R)","caffeineMg":7.58,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_메가초코 라떼 아이스(ICED)","caffeineMg":7.53,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티","caffeineMg":7.53,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_진저 밀크티","caffeineMg":7.53,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"코코아_초코 핫(HOT)","caffeineMg":7.5,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED)","caffeineMg":7.5,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_달고나커피 아이스(ICED)","caffeineMg":7.48,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"허브차_민트 핫(HOT) (L)","caffeineMg":7.4,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED) (L)","caffeineMg":7.4,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT) (L)","caffeineMg":7.4,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"스무디_골든펄 돌체 밀크티 스무디","caffeineMg":7.19,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 핫(HOT)","caffeineMg":7.18,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 핫(HOT)","caffeineMg":7.05,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티 아이스(ICED)","caffeineMg":6.99,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_진저 밀크티 아이스(ICED)","caffeineMg":6.99,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_제주 한라봉 블랙티 아이스(ICED)","caffeineMg":6.97,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"커피_달고나커피 핫(HOT)","caffeineMg":6.8,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 아이스(ICED)","caffeineMg":6.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 아인슈페너 아이스(ICED)","caffeineMg":6.76,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"우롱차_우롱티 핫(HOT)","caffeineMg":6.62,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 아이스(ICED)","caffeineMg":6.6,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼 핫(HOT)","caffeineMg":6.6,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"홍차_아쌈티 아이스(ICED)","caffeineMg":6.55,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"녹차_프레시그린티 아이스(ICED)","caffeineMg":6.52,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_프레시그린티 핫(HOT)","caffeineMg":6.52,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"코코아_화이트초코 아이스(ICED)","caffeineMg":6.5,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"코코아_화이트초코 핫(HOT)","caffeineMg":6.5,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 아이스(ICED) (XL)","caffeineMg":6.41,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_쑥단팥스모어 쿠키","caffeineMg":6.37,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"커피_디카페인 아인슈페너 아이스(ICED)","caffeineMg":6.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아인슈페너 핫(HOT)","caffeineMg":6.28,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 아이스(ICED) (XL)","caffeineMg":6.17,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_자몽 그린티 (L)","caffeineMg":6.13,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티 핫(HOT) (J)","caffeineMg":6.13,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티 핫(HOT) (L)","caffeineMg":6.04,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_자몽 그린티 (J)","caffeineMg":5.99,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"커피_디카페인 카페모카 아이스(ICED)","caffeineMg":5.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페모카 핫(HOT)","caffeineMg":5.92,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페","caffeineMg":5.92,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초당옥수수 팝핑 스무디","caffeineMg":5.92,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초콜렛 쿠키&크림 스무디","caffeineMg":5.92,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_리얼초코 프라페","caffeineMg":5.89,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_아쌈 버블티","caffeineMg":5.88,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_발로나 민트 초코 프라페","caffeineMg":5.79,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라 딜라이트 아이스(ICED)","caffeineMg":5.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라 딜라이트 핫(HOT)","caffeineMg":5.65,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_유스베리티 아이스(ICED) (Tall)","caffeineMg":5.63,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_유스베리티 핫(HOT) (Tall)","caffeineMg":5.63,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"빙수_그린티 초코 쿨빙수","caffeineMg":5.56,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"밀크티/버블티_자스민 그린 밀크티 아이스(ICED) (L)","caffeineMg":5.52,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_더벤티사이즈 디카페인 아메리카노 아이스(ICED)","caffeineMg":5.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_더벤티사이즈 디카페인 카페 라떼 아이스(ICED)","caffeineMg":5.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페","caffeineMg":5.41,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED)","caffeineMg":5.38,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"밀크티/버블티_우롱 밀크티 아이스(ICED) (L)","caffeineMg":5.31,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타음료_레드 파워 스매셔 (Grande)","caffeineMg":5.29,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"라떼_흑당 밀크티 라떼 아이스(ICED)","caffeineMg":5.18,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"크로플_티라미수크림 크로플","caffeineMg":5.17,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"라떼_민트초콜릿 아이스(ICED)","caffeineMg":5.16,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초콜릿 핫(HOT)","caffeineMg":5.16,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_스트로베리 프룻티","caffeineMg":5.11,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_핑크 리치 프룻티","caffeineMg":5.11,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_초코 밀크티 핫(HOT) (XL)","caffeineMg":5.08,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_딸기 듬뿍 밀크티","caffeineMg":5.07,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초당옥수수 밀크티+펄","caffeineMg":5.07,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티+펄 핫(HOT) (J)","caffeineMg":5.07,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티+펄 핫(HOT) (L)","caffeineMg":5.07,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_로얄 밀크티 아이스(ICED)","caffeineMg":4.99,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_돌체 블랙 밀크티 아이스(ICED)","caffeineMg":4.98,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초코 밀크티 핫(HOT) (L)","caffeineMg":4.95,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_스트로베리초콜릿 프라페 (L)","caffeineMg":4.86,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_초코 리얼 라떼 핫(HOT) (L)","caffeineMg":4.77,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_코코초코 프라페","caffeineMg":4.74,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"사과차_애플 그린티 아이스(ICED)","caffeineMg":4.71,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"라떼_민트 초콜릿 핫(HOT)","caffeineMg":4.68,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_납작복숭아 타르트 크러쉬","caffeineMg":4.65,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_리얼 초코 핫(HOT)","caffeineMg":4.61,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_더블 토피넛 라떼 아이스(ICED)","caffeineMg":4.59,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_더블 토피넛 라떼 핫(HOT)","caffeineMg":4.59,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"우롱차_우롱티 아이스(ICED)","caffeineMg":4.59,"basis":"100mL","major":"음료 및 차류","rep":"우롱차","source":"식품의약품안전처"},{"name":"스무디_토피넛 플랫치노","caffeineMg":4.59,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_스트로베리초콜릿 프라페 (Max)","caffeineMg":4.57,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_초코바나나 주스","caffeineMg":4.57,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"라떼_토피 넛 라떼 아이스(ICED)","caffeineMg":4.53,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피 넛 라떼 핫(HOT)","caffeineMg":4.53,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 아이스(ICED)","caffeineMg":4.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아인슈페너 아이스(ICED)","caffeineMg":4.51,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_제주 유기 녹차 아이스(ICED) (Tall)","caffeineMg":4.51,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"녹차_제주 유기 녹차 핫(HOT) (Tall)","caffeineMg":4.51,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"스무디_코코넛커피 쉐이크","caffeineMg":4.47,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_납작복숭아 쥬얼리 밀크티","caffeineMg":4.44,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_딸기 쿠키 스무디","caffeineMg":4.44,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초코바른 피스타치오 스무디","caffeineMg":4.44,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라딥라떼 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라딥라떼 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_디카페인 에스프레소 쉐이크","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 연유 라떼 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 연유 라떼 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 오트카페 라떼 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 오트카페 라떼 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카라멜마끼야또 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카라멜마끼야또 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛딥라떼 아이스(ICED)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛딥라떼 핫(HOT)","caffeineMg":4.4,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_스트로베리초콜릿 프라페 (R)","caffeineMg":4.35,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트 초코칩 블렌디드","caffeineMg":4.34,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트 초콜릿 아이스(ICED)","caffeineMg":4.34,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티+펄 아이스(ICED) (J)","caffeineMg":4.3,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"아이스티_레몬 아이스티 (EX)","caffeineMg":4.27,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_양지감로","caffeineMg":4.27,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_그릭요거트&망고 밀크티 크러쉬","caffeineMg":4.23,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"코코아_시그니처 초콜릿 아이스(ICED) (Tall)","caffeineMg":4.23,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"코코아_시그니처 초콜릿 핫(HOT) (Tall)","caffeineMg":4.23,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"기타차_유스베리 로즈티 브리즈 핫(HOT) (Grande)","caffeineMg":4.23,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티+펄 아이스(ICED)) (L)","caffeineMg":4.23,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_토피 넛 라떼 아이스(ICED) (EX)","caffeineMg":4.13,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피 넛 라떼 핫(HOT) (EX)","caffeineMg":4.13,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"아이스크림_초콜릿파르페 아이스(ICED) (Short)","caffeineMg":4.08,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"녹차_녹차 아이스(ICED)","caffeineMg":4.03,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"기타차_골든펄 망고 패션프룻 그린티","caffeineMg":4.02,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_리얼 딸기 쥬얼리 밀크티","caffeineMg":4.02,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜렛 밀크티 핫(HOT) (J)","caffeineMg":4.02,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티 아이스(ICED) (L)","caffeineMg":4.02,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_피스타치오 밀크티 아이스(ICED) (J)","caffeineMg":3.99,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_오레오초코 라떼 아이스(ICED)","caffeineMg":3.96,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_치즈&애플망고 블렌디드","caffeineMg":3.96,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_버터스카치 라떼 아이스(ICED)","caffeineMg":3.9,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_초콜릿 라떼 핫(HOT)","caffeineMg":3.9,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜렛 밀크티 핫(HOT) (L)","caffeineMg":3.86,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"탄산음료_체리콕콕 아이스(ICED)","caffeineMg":3.83,"basis":"100mL","major":"음료 및 차류","rep":"탄산음료","source":"식품의약품안전처"},{"name":"라떼_초코 리얼 라떼 핫(HOT) (XL)","caffeineMg":3.81,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"녹차_자스민 그린티 아이스(ICED)","caffeineMg":3.73,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"스무디_초코 블렌디드","caffeineMg":3.72,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 연유 콜드브루 (EX)","caffeineMg":3.61,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 (EX)","caffeineMg":3.61,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아메리카노 (EX)","caffeineMg":3.61,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_딸기 초코 라떼","caffeineMg":3.61,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초콜릿 라떼 아이스(ICED)","caffeineMg":3.61,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_그릭요거트&딸기 밀크티 크러쉬","caffeineMg":3.59,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_납작복숭아 블루밍 크러쉬","caffeineMg":3.59,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_리얼 초코 아이스(ICED)","caffeineMg":3.55,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_화이트 템플티 아이스(ICED)","caffeineMg":3.55,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_화이트 템플티 핫(HOT)","caffeineMg":3.55,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"아이스티_달콤아이스티 아이스(ICED) 빽사이즈","caffeineMg":3.37,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT)","caffeineMg":3.37,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"에이드_체리콕","caffeineMg":3.37,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티","caffeineMg":3.36,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_청포도 아이스티","caffeineMg":3.36,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_레몬 아이스티","caffeineMg":3.35,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_치즈&스트로베리 블렌디드","caffeineMg":3.32,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_치즈&핑크리치 블렌디드","caffeineMg":3.32,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티 (EX)","caffeineMg":3.28,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_민트 프라페","caffeineMg":3.21,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_초코 리얼 라떼 아이스(ICED) (XL)","caffeineMg":3.21,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_초코바른 초코 스무디","caffeineMg":3.17,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트크림초코 라떼 핫(HOT)","caffeineMg":3.15,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_초코 밀크티 아이스(ICED) (XL)","caffeineMg":3.15,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"기타차_인디안 차이티 아이스(ICED)","caffeineMg":3.09,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_인디안 차이티 핫(HOT)","caffeineMg":3.09,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페","caffeineMg":3.08,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_커피 프라페","caffeineMg":3.08,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED)","caffeineMg":3.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT)","caffeineMg":3.0,"basis":"354mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_민트 초코칩 할리치노","caffeineMg":3.0,"basis":"354mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_헤이즐넛 초코칩 할리치노","caffeineMg":3.0,"basis":"354mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_초코 리얼 라떼 아이스(ICED) (L)","caffeineMg":2.92,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_토피넛초코칩 프라페","caffeineMg":2.88,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초콜릿 크림 칩 프라푸치노 (Tall)","caffeineMg":2.82,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트크림초코 라떼 아이스(ICED)","caffeineMg":2.79,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_딸기 쥬얼리 밀크티 아이스(ICED)","caffeineMg":2.75,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티","caffeineMg":2.66,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜렛 밀크티 아이스(ICED) (J)","caffeineMg":2.61,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_초코 밀크티 아이스(ICED) (L)","caffeineMg":2.58,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_초코 프라페","caffeineMg":2.58,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_디카페인 아샷추 아이스티","caffeineMg":2.54,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"기타차_유스베리 로즈티 브리즈 아이스(ICED) (Grande)","caffeineMg":2.54,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"밀크티/버블티_초콜렛 밀크티 아이스(ICED) (L)","caffeineMg":2.54,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루","caffeineMg":2.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼","caffeineMg":2.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 연유","caffeineMg":2.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 흑당","caffeineMg":2.5,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"복숭아홍차_피치얼그레이티 아이스(ICED)","caffeineMg":2.47,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"자몽홍차_허니자몽블랙티 아이스(ICED)","caffeineMg":2.47,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"허브차_허브티 아이스(ICED)","caffeineMg":2.47,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"라떼_초콜릿 아이스(ICED) (EX)","caffeineMg":2.44,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초콜릿 핫(HOT) (EX)","caffeineMg":2.44,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 니트로 커피","caffeineMg":2.42,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_초코밀크 쉐이크 (R)","caffeineMg":2.42,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_흑당버블 밀크티 라떼 아이스(ICED)","caffeineMg":2.42,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED)","caffeineMg":2.37,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT)","caffeineMg":2.37,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_초코 쉐이크","caffeineMg":2.37,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 라떼 핫(HOT)","caffeineMg":2.37,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"코코아_핫초코 아이스(ICED)","caffeineMg":2.26,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"코코아_핫초코 핫(HOT)","caffeineMg":2.26,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"복숭아홍차_피치얼그레이티 핫(HOT)","caffeineMg":2.25,"basis":"100mL","major":"음료 및 차류","rep":"복숭아홍차","source":"식품의약품안전처"},{"name":"자몽홍차_허니자몽블랙티 핫(HOT)","caffeineMg":2.25,"basis":"100mL","major":"음료 및 차류","rep":"자몽홍차","source":"식품의약품안전처"},{"name":"허브차_허브티 핫(HOT)","caffeineMg":2.25,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"라떼_헤이즐넛자바칩 라떼 아이스(ICED)","caffeineMg":2.25,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_헤이즐넛자바칩 라떼 핫(HOT)","caffeineMg":2.25,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED)","caffeineMg":2.22,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_콜드브루디카페인 핫(HOT)","caffeineMg":2.22,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 연유 콜드브루","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아메리카노","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아인슈페너","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 크림넛","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 티라미수","caffeineMg":2.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"기타차_제주 키위 오션 그린티 (Grande)","caffeineMg":2.11,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_청포도 스무디","caffeineMg":2.11,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_폼폼 유스베리티 (Grande)","caffeineMg":2.11,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_초코허니퐁 크러쉬","caffeineMg":2.1,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_초콜릿 아이스(ICED)","caffeineMg":2.07,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초콜릿 핫(HOT)","caffeineMg":2.07,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 아메리카노 아이스(ICED)","caffeineMg":1.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아메리카노 핫(HOT)","caffeineMg":1.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 아이스(ICED)","caffeineMg":1.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 핫(HOT)","caffeineMg":1.98,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_민트초코 프라페","caffeineMg":1.97,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_싱글오리진 디카페인","caffeineMg":1.96,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"홍차_얼그레이 핫(HOT)","caffeineMg":1.86,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"스무디_쿠키크런치 빽스치노","caffeineMg":1.75,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 쥬얼리 요구르트 크러쉬","caffeineMg":1.69,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_토피넛 라떼 아이스(ICED)","caffeineMg":1.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_토피넛 라떼 핫(HOT)","caffeineMg":1.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 라떼 아이스(ICED)","caffeineMg":1.68,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_피스타치오 빽스치노","caffeineMg":1.6,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초코 바나나 프라페","caffeineMg":1.59,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬 브랙퍼스트 아이스(ICED)","caffeineMg":1.58,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"홍차_잉글리쉬 브랙퍼스트 핫(HOT)","caffeineMg":1.58,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"커피_디카페인라떼 아이스(ICED)","caffeineMg":1.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인라떼 핫(HOT)","caffeineMg":1.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인커피 아이스(ICED)","caffeineMg":1.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인커피 핫(HOT)","caffeineMg":1.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 화이트비엔나","caffeineMg":1.52,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루디카페인 아이스(ICED)","caffeineMg":1.47,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_쿠키크런치 빽스치노 소프트","caffeineMg":1.47,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 버블 흑당 콜드브루","caffeineMg":1.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 흑당 콜드브루","caffeineMg":1.45,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 버블 흑당 콜드브루 (EX)","caffeineMg":1.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 흑당 콜드브루 (EX)","caffeineMg":1.38,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_피스타치오 빽스치노 소프트","caffeineMg":1.31,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_싱글오리진 디카페인 아이스(ICED)","caffeineMg":1.29,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스티_아이스티","caffeineMg":1.2,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_딸기 초코칩 프라페","caffeineMg":1.18,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_리얼초코 프라페","caffeineMg":1.18,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코칩 프라페","caffeineMg":1.18,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_자이언트 아이스티","caffeineMg":1.13,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED)","caffeineMg":1.1,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_민트초코 프라페 (L)","caffeineMg":1.06,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코 프라페 (Max)","caffeineMg":1.02,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_아메리카노 아이스(ICED)","caffeineMg":1.0,"basis":"360mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT)","caffeineMg":1.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_민트초코 프라페 (R)","caffeineMg":0.97,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠키 프라페","caffeineMg":0.93,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_딥초코버블 라떼 아이스(ICED)","caffeineMg":0.91,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_리얼초코 라떼 아이스(ICED)","caffeineMg":0.91,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛 라떼 핫(HOT)","caffeineMg":0.87,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛 커피 핫(HOT)","caffeineMg":0.87,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED)","caffeineMg":0.85,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT)","caffeineMg":0.85,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_딥초코버블 라떼 핫(HOT)","caffeineMg":0.83,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_리얼초코 라떼 핫(HOT)","caffeineMg":0.83,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 바나나 달달 커피 핫(HOT)","caffeineMg":0.82,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_버터스카치 라떼 핫(HOT)","caffeineMg":0.78,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛 라떼 아이스(ICED)","caffeineMg":0.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛 커피 아이스(ICED)","caffeineMg":0.69,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 바나나 달달 커피 아이스(ICED)","caffeineMg":0.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 베트남 연유 커피 아이스(ICED)","caffeineMg":0.66,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티","caffeineMg":0.63,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_딸기쿠키 프라페","caffeineMg":0.61,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 핫(HOT)","caffeineMg":0.59,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아인슈페너 아이스(ICED)","caffeineMg":0.56,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 꿀 라떼 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 꿀 커피 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라 라떼 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아메리카노 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아몬드 라떼 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 모카 핫(HOT)","caffeineMg":0.49,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_디카페인 바닐라 크럼블 아이스크림 라떼 아이스(ICED)","caffeineMg":0.48,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_디카페인 돌체 콜드브루 라떼 아이스(ICED)","caffeineMg":0.47,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 아이스(ICED)","caffeineMg":0.47,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 달고나 콜드브루 라떼 핫(HOT)","caffeineMg":0.44,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"녹차_그린티 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"녹차","source":"식품의약품안전처"},{"name":"커피_디카페인 꿀 라떼 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 꿀 커피 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라 라떼 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아메리카노 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 아몬드 라떼 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 라떼 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 카페 모카 아이스(ICED)","caffeineMg":0.39,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 달고나 콜드브루 라떼 아이스(ICED)","caffeineMg":0.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아이스(ICED)","caffeineMg":0.36,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"라떼_민트초코 아이스(ICED)","caffeineMg":0.28,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 핫(HOT)","caffeineMg":0.28,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코바나나 라떼 아이스(ICED)","caffeineMg":0.28,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코바나나 라떼 핫(HOT)","caffeineMg":0.28,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_초코쿠키 쉐이크","caffeineMg":0.24,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 핫(HOT)","caffeineMg":0.19,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"커피_디카페인 바닐라 크림콜드브루 아이스(ICED)","caffeineMg":0.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 라떼 아이스(ICED)","caffeineMg":0.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 콜드브루 아이스(ICED)","caffeineMg":0.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_디카페인 헤이즐넛 크림콜드브루 아이스(ICED)","caffeineMg":0.17,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이 밀크티 아이스(ICED)","caffeineMg":0.14,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_얼그레이버블티 아이스(ICED)","caffeineMg":0.12,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"빙수_22오리지널 팥빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"아이스티_NEW복숭아아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"허니브레드_갈릭 치즈 브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_고구마 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"유자차_고흥 유자 레몬 캐모마일티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_고흥유자차 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_고흥유자차 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"라떼_곡물 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_곡물 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_골드 고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_골드 고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"과ㆍ채주스_골드키위 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"라떼_곶감 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_곶감 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"요구르트(호상)_그릭요거 망고놀라","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(호상)","source":"식품의약품안전처"},{"name":"허브차_그린루이보스 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_그린루이보스 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"스무디_그린티 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_그린티 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_기운내라임 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"기타차_깔라만시","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"에이드_깔라만시 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_깔라만시 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_깔라만시 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"라떼_꿀 딸기 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_꿀 망고 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_꿀 복숭아 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_꿀 자몽 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"자몽차_꿀 자몽티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_꿀 자몽티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"스무디_꿀배 쿨러시","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_꿀복숭아 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"호떡_꿀호떡","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"호떡","source":"식품의약품안전처"},{"name":"아이스크림_노말한소프트 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"라떼_녹차 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타음료_논알콜 하이볼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"과ㆍ채주스_놀라운망고","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_놀라운청포도","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_놀라운패션후르츠","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"마카롱_누텔라 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"크로플_누텔라크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"크림빵_단팥크림빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"라떼_단호박 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"샌드위치_단호박 크림치즈 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"라떼_달고나 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_달고나 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_달고나 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_달고나 버블 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"와플_달고나 아이스크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"스무디_달달녹차프라푸치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"케이크_당근당근 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"쌍화차_대추쌍화차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"쌍화차","source":"식품의약품안전처"},{"name":"쌍화차_대추쌍화차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"쌍화차","source":"식품의약품안전처"},{"name":"대추차_대추차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"대추차","source":"식품의약품안전처"},{"name":"대추차_대추차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"대추차","source":"식품의약품안전처"},{"name":"대추차_대추차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"대추차","source":"식품의약품안전처"},{"name":"대추차_대추차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"대추차","source":"식품의약품안전처"},{"name":"라떼_더블 초콜릿 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_더블 초콜릿 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_더블 초콜릿 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_더블 초콜릿 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"케이크_더블치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"케이크_데블스 초코 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"라떼_도넛파티 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 디카페인 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 디카페인 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 디카페인 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_돌체 콜드브루 라떼 디카페인 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"마카롱_돼지바 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"마카롱_돼지바 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_딸기 듬뿍 라떼 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_딸기 듬뿍 라떼 (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_딸기 딜라이트 요거트 블렌디드 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_딸기 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_딸기 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_딸기 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"마카롱_딸기 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 바나나 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_딸기 빽스치노 소프트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 쉐이크 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_딸기 아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"에이드_딸기 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_딸기 에이드 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_딸기 요거트 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 요거트 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기 유자 소르베","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기 주스 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_딸기 치즈 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기돼지쉑","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기바나나 빽스치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기바나나 빽스치노 소프트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_딸기바나나 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_딸기바나나요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_딸기버블 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_딸기스노우 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"빙수_딸기시리얼빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"빙수_딸기시리얼컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"기타차_딸기오렌지바나나 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_딸기오렌지바나나 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_딸기요거 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_딸기요거트 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"마카롱_딸기요거트 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_딸기요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기요거트 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기요거트 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_딸기차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_딸기차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_딸기차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_딸기차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"빙수_딸기치즈 눈꽃빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"스무디_딸기크림쿠키 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기크림프라푸치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_딸기티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_딸기티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_딸기퐁 크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"빙수_딸기피치 요거놀라 1인빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"스무디_딸기피치 요거스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_딸기한라봉 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"와플_땅콩딸기생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"케이크_떠먹는 유자 티라미수 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"케이크_떠먹는 쿠키앤크림 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"케이크_떠먹는 티라미수 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"스무디_라이스 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타음료_라임 모히또","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"마카롱_라즈베리 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_레드자몽 쿨러시","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_레모 네이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"케이크_레몬 마스카포네 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"레몬차_레몬 스윗플럼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"아이스티_레몬 아이스티 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_레몬 아이스티 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (EX)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_레몬 에이드 (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"유자차_레몬 유자티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_레몬 유자티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"에이드_레몬딸기 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"허브차_레몬밤","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"아이스티_레몬아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"기타차_레몬진저 캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_레몬진저 캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"레몬차_레몬차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"레몬차_레몬티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"레몬차","source":"식품의약품안전처"},{"name":"기타차_레몬페퍼민트티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_레몬페퍼민트티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"에이드_로즈 갤럭시 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"아이스티_로즈 오로라 아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"핫도그_롤핫도그","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"핫도그","source":"식품의약품안전처"},{"name":"기타차_루이보스 바닐라티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_루이보스 바닐라티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"허브차_루이보스 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_루이보스 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_루이보스오렌지 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_루이보스오렌지 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"과ㆍ채주스_리얼 수박 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_리얼 수박 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"라떼_리얼군고구마 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"과ㆍ채주스_리얼수박 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"케이크_마스카포네 티라미수 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"라떼_마스카포네치즈 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"케이크_마스카포네티라미수","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"마카롱_마약옥수수 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_마카다미아 쿠키","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_마카롱꼬끄","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"라떼_마카롱파티 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"마카롱_말차 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_말차 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_말차 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_말차 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_말차 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"빙수_망고 눈꽃빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"라떼_망고 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_망고 바나나 블렌디드 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 바나나 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"빙수_망고 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"스무디_망고 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고 아이스 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스크림_망고 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"스무디_망고 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"요구르트(액상)_망고 요구르트+화이트펄 (J)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"요구르트(액상)_망고 요구르트+화이트펄 (L)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스 (J)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_망고 주스 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_망고 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고바나나요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_망고요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"요구르트(액상)_망고요구르트 (J)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"요구르트(액상)_망고요구르트 (L)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"빙수_망고파인 컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"빙수_망고패션 요거놀라 1인빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"기타차_매실차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_매실차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_매실차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_매실차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"에이드_메가 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"마테차_메리베리마테 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"마테차","source":"식품의약품안전처"},{"name":"마테차_메리베리마테 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"마테차","source":"식품의약품안전처"},{"name":"마테차_메리베리마테 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"마테차","source":"식품의약품안전처"},{"name":"마테차_메리베리마테 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"마테차","source":"식품의약품안전처"},{"name":"허니브레드_메이플 넛 브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"와플_메이플 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"샌드위치_멜팅치즈 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"롤빵_목장의아침우유롤","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"롤빵","source":"식품의약품안전처"},{"name":"아이스크림_몬스터 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"케이크_몽쉘 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"오미자차_문경오미자차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"오미자차","source":"식품의약품안전처"},{"name":"미숫가루_미숫가루","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"미숫가루","source":"식품의약품안전처"},{"name":"라떼_미숫가루 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_미숫가루 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타음료_미초 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"에이드_미초(석류) 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"밀크티/버블티_민트 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_민트 밀크티 아이스(ICED) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_민트 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_민트 밀크티 핫(HOT) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"허브차_민트 블렌드티 아이스(ICED) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_민트 블렌드티 핫(HOT) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"스무디_민트 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트 초콜릿 칩 블렌디드 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트초코 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_민트초코 빽스치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코 빽스치노 소프트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초코프라푸치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초콜릿칩 프라페 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_민트초콜릿칩 프라페 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_민트쿠키 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_민트쿠키 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_민트쿠키 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_밀싹 케일 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_밀크 쉐이크 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"빙수_밀크 팥빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"밀크티/버블티_밀크티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_밀크티 버블 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"과ㆍ채주스_바나나 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"마카롱_바나나누텔라 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_바나나퐁 크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_바나나프로틴쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_바닐라 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"마카롱_바닐라 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_바닐라 크림 프라푸치노 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_배 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_배꿀 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"뱅쇼_뱅쇼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"뱅쇼","source":"식품의약품안전처"},{"name":"라떼_버블흑당 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"빙수_베리 컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"피자_베이컨 포테이토 스퀘어 피자","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"피자","source":"식품의약품안전처"},{"name":"스무디_복숭아 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_복숭아 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_복숭아 아이스티 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_복숭아 애플망고 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_복숭아 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_복숭아 에이드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_복숭아 요거스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_복숭아아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_복숭아아이스티 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_복숭아아이스티 (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"또띠아_불고기 브리또","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"또띠아","source":"식품의약품안전처"},{"name":"샌드위치_불고기 파니니","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_브라우니 쿠키","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"밀크티/버블티_브라운 슈가 쥬얼리 밀크티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_브라운 슈가 쥬얼리 밀크티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_브라운 슈가 쥬얼리 치즈폼 스무디 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_브라운슈가버블 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_브라운슈가버블 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_블랙 밀크티 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_블랙펄 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"에이드_블루레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_블루레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_블루레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_블루레몬 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"머핀_블루베리 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"머핀_블루베리 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"베이글_블루베리 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_블루베리 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_블루베리 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"빙수_블루베리 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"스무디_블루베리 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스크림_블루베리 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"스무디_블루베리 요거스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"요구르트(액상)_블루베리 요거트 병음료","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"스무디_블루베리 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리 요거트 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"케이크_블루베리 크림치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"스무디_블루베리요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리요거트 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_블루베리요거트 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"빙수_블루베리케이크 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"에이드_블루파인 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"과ㆍ채주스_비트 사과 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"마카롱_뽀또치즈 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"마카롱_뽀또치즈 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"대추차_사과 대추차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"대추차","source":"식품의약품안전처"},{"name":"와플_사과생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"와플_사과생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"유자차_사과유자차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_사과유자차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"사과차_사과차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"사과차_사과차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"사과차_사과차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"사과차_사과차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"샌드위치_사라다빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"마카롱_산딸기 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_생강 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"생강차_생강차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"생강차","source":"식품의약품안전처"},{"name":"과ㆍ채주스_생과일 수박 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_생과일 토마토 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_생딸기 그래놀라 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_생딸기 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"와플_생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"카스텔라_생크림 카스테라","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"카스텔라","source":"식품의약품안전처"},{"name":"카스텔라_생크림 카스테라","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"카스텔라","source":"식품의약품안전처"},{"name":"에이드_샤인 망고 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"아이스티_샤인 매실 아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"스무디_샤인 머스캣 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_샤인머스캣 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_샤인머스캣 티플레저","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"에이드_샤인코코 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"허브차_샤인히비스커스 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_샤인히비스커스 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"에이드_샹그리아 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_샹그리아 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"기타차_샹그리아 프루티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_샹그리아 프루티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"사과차_석류 애플라임","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"사과차_석류 애플라임 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"기타차_석류 오리지널 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"사과차_석류애플라임 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"사과차","source":"식품의약품안전처"},{"name":"라떼_설향 딸기 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_성주참외꿀 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"또띠아_소고기 브리또","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"또띠아","source":"식품의약품안전처"},{"name":"버터빵_소금빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"버터빵","source":"식품의약품안전처"},{"name":"소세지빵_소세지빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"소세지빵","source":"식품의약품안전처"},{"name":"마카롱_솔티카라멜 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"과ㆍ채주스_수박 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_수박머스캣 소다","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_수박파인 펀치","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"케이크_수플레 치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"크림빵_슈크림 콩빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"스무디_슈크림허니퐁 크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_슈파티 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_스노우코코 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_스노우코코 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_스노우코코 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_스노우코코 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"크림빵_스노우쿠키슈","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"허브차_스위트후르츠 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_스위트후르츠 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"기타음료_스타벅스 슬래머 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"라떼_스트로베리 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_스트로베리 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_스트로베리 요거트 블렌디드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_스트로베리 요거트 블렌디드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_스트로베리치즈홀릭","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"우유_스팀 우유 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"우유","source":"식품의약품안전처"},{"name":"에이드_스파클링 고흥유자 레몬 캐모마일","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_스파클링 망고","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_스파클링 망고 캐모마일","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_스파클링 베리","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_스파클링 제주 레몬 스웨디쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"허브차_스프링캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_스프링캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"크림빵_아이스슈","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"와플_아이스크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"크로플_아이스크림 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"와플_아이스크림 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"크로플_아이스크림 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"호떡_아이스크림 호떡","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"호떡","source":"식품의약품안전처"},{"name":"아이스티_아이스티 복숭아 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_아이스티 복숭아 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"크림빵_아이스허니와앙슈","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"스무디_애플망고 샹그리아 소르베","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_애플망고 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스티_애플망고 아이스티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"빙수_애플망고케이크 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"스무디_애플망고크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"버터빵_약과 버터바","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"버터빵","source":"식품의약품안전처"},{"name":"라떼_약과 오트라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_약과 오트라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_약과 카라멜 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"크로플_약과 크림 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"베이글_어니언 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_어니언 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_어니언 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"홍차_얼그레이","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"마카롱_얼그레이 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"홍차_얼그레이 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"홍차","source":"식품의약품안전처"},{"name":"샌드위치_에그 베이컨 과카몰리 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"기타차_엘더베리 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_엘더베리 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"마카롱_연유 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_연유딸기쉑","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_연유망고쉑","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"크림빵_연유크림브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"라떼_영암 고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_영암 고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"빙수_옛날팥빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"라떼_오곡 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_오곡 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"미숫가루_오곡 미숫가루","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"미숫가루","source":"식품의약품안전처"},{"name":"과ㆍ채주스_오곡바나나 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"마카롱_오레오 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"마카롱_오레오 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_오레오 쉐이크 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"와플_오레오생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"빙수_오레오초코 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"번_오리지널 핫 번","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"번","source":"식품의약품안전처"},{"name":"케이크_오리지널티라미수","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"스무디_오리진 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_오미자 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"과ㆍ채주스_완전딸기 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_완전망고 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_요거트 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_요거트 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_요거트 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_우도땅콩 바나나 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_우리 고구마 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_우리 고구마 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"우유_우유 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"우유","source":"식품의약품안전처"},{"name":"마카롱_월드콘 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_유니콘 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_유니콘매직 에이드 블루","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_유니콘매직 에이드 핑크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"마카롱_유니콘프라페 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"유자차_유자 민트티 아이스(ICED) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자 민트티 핫(HOT) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"생강차_유자 생강차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"생강차","source":"식품의약품안전처"},{"name":"에이드_유자 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"기타차_유자 엘더베리 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_유자 엘더베리 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"유자차_유자 캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자 캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"탄산음료_유자 패션 피지오 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"탄산음료","source":"식품의약품안전처"},{"name":"유자차_유자 피나콜라다","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자 피나콜라다 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자 피나콜라다 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자레몬티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자레몬티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"유자차_유자티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"유자차","source":"식품의약품안전처"},{"name":"라떼_이곡 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_이곡 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"케이크_이디야 티라미수 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"마카롱_인절미 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"빙수_인절미 빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"아이스크림_인절미 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"머핀_잉글리쉬 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"아이스티_자두 아이스티 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"아이스티_자두 아이스티 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"아이스티","source":"식품의약품안전처"},{"name":"에이드_자두 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_자두크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"자몽차_자몽 네이블 오렌지 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽 네이블 오렌지 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽 네이블오렌지","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"기타음료_자몽 모히또","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"스무디_자몽 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_자몽 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드 (EX)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_자몽 에이드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_자몽 요거트 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_자몽 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_자몽 주스 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"스무디_자몽 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_자몽라임 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"요구르트(액상)_자몽요구르트 (J)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"요구르트(액상)_자몽요구르트 (L)","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"자몽차_자몽차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_자몽티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"기타차_자몽히비스커스티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_자몽히비스커스티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_자바칩 프라페 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_자바칩프라푸치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_작설차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_장수 오미자 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_제주 그린 한라봉 모히또 블렌디드 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_제주 까망 라떼 아이스(ICED) (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_제주 까망 라떼 핫(HOT) (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_제주 까망 크림 프라푸치노 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_제주 레몬 망고 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"미숫가루_제주 보리개역 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"미숫가루","source":"식품의약품안전처"},{"name":"미숫가루_제주 보리개역 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"미숫가루","source":"식품의약품안전처"},{"name":"스무디_제주 쑥떡 크림 프라푸치노 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_제주 쑥쑥 라떼 핫(HOT) (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_제주 한라봉 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_제주 한라봉 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"샌드위치_제주당근에그마요 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"기타차_제주당근오렌지티플레저 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"귤차_제주청귤 블라썸 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_제주청귤 오리지널 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_제주청귤차","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"스무디_죠리퐁 프라페 밀크카라멜","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_죠리퐁 프라페 플레인","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_짱구 초코 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"에이드_청귤 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청귤 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청귤 에이드 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"귤차_청귤블랙티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤블랙티 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤블랙티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤블랙티 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤차 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤차 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤차 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"귤차_청귤차 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"귤차","source":"식품의약품안전처"},{"name":"에이드_청자스페셜","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"기타음료_청포도 모히또","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"스무디_청포도 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_청포도 아이스 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스크림_청포도 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드 (EX)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_청포도 에이드 (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"스무디_청포도 쿨러시","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_청포도블라썸","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"기타음료_청포도플라워 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타음료","source":"식품의약품안전처"},{"name":"와플_체다치즈 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"기타차_체리석류 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_체리석류 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"에이드_체리콕 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"라떼_초코 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_초코 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"아이스크림_초코 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"케이크_초코 티라미수 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"스무디_초코돼지쉑","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_초코라떼 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"케이크_초코무스 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"스무디_초코바나나 빽스치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초코바나나 빽스치노 소프트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"머핀_초코범벅","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"스무디_초코빽스치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초코빽스치노 소프트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"와플_초코생크림 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"머핀_초코칩 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"머핀_초코칩 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"스무디_초코칩 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초코칩 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_초코칩 쿠키","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"스무디_초코프로틴쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_초콜릿 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_초콜릿 아이스 블렌디드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_초콜릿 아이스 블렌디드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"비스킷/쿠키/크래커_초콜릿칩 쿠키","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"비스킷/쿠키/크래커","source":"식품의약품안전처"},{"name":"기타빵_춘천 감자빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"기타빵","source":"식품의약품안전처"},{"name":"츄러스_츄러스 바바리안 크림","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"츄러스","source":"식품의약품안전처"},{"name":"요구르트(액상)_치아씨드 요거트 병음료","caffeineMg":0.0,"basis":"100mL","major":"유제품류 및 빙과류","rep":"요구르트(액상)","source":"식품의약품안전처"},{"name":"머핀_치즈 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"베이글_치즈 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"케이크_치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"라떼_치즈군고구마 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"크림빵_치즈크림빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"또띠아_치킨 브리또","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"또띠아","source":"식품의약품안전처"},{"name":"허브차_카모마일 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_카모마일 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_카모마일 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_카모마일 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"크로플_카야치즈 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"샌드위치_카야치즈토스트","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_카야토스트","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"라떼_카카오 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_카카오 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"기타차_카페오르조","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"허브차_캐모마일","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 블렌드티 아이스(ICED) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 블렌드티 핫(HOT) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_캐모마일 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"기타차_캐모마일리치티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_캐모마일리치티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"허브차_캐모마일티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"번_커피콩빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"번","source":"식품의약품안전처"},{"name":"빙수_컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"에이드_코코 에이드 청포도","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"밀크티/버블티_코코넛 버블티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"샌드위치_콘참치샌드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 디카페인 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 디카페인 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 디카페인 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 디카페인 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"커피_콜드브루 라떼 디카페인 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"커피","source":"식품의약품안전처"},{"name":"스무디_쿠앤크 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠앤크 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠앤크 스무디 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠앤크프라푸치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스크림_쿠키 아이스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"스무디_쿠키 프라페","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠키&크림 프라페 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_쿠키&크림 프라페 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_쿠키앤크림 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_쿠키크림 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_쿠키크림 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_쿠키크림 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_쿠키크림 라떼 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"마카롱_쿠키프라페 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"허브차_쿨 허벌티 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_쿨 허벌티 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"샌드위치_크로크무슈","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_크로크무슈","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"크로와상_크루아상","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로와상","source":"식품의약품안전처"},{"name":"크림빵_크림소금빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"머핀_크림치즈 머핀","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"머핀","source":"식품의약품안전처"},{"name":"와플_크림치즈 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"베이글_크림치즈 프레즐","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"빙수_클래식 컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"과ㆍ채주스_키위 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_키위 주스 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 아이스(ICED) (J)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 아이스(ICED) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 핫(HOT) (J)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티 핫(HOT) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티+펄 아이스(ICED) (J)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티+펄 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티+펄 핫(HOT) (J)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 밀크티+펄 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_타로 버블티","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"스무디_타로 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"과ㆍ채주스_토마토 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_토마토 주스 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_토피넛 라떼 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"마카롱_토피넛크런치 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"스무디_트위스트 피치 요거트 블렌디드 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"케이크_티라미수","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"과ㆍ채주스_파이팅 청귤 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_파인 자몽 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"빙수_팥인절미 1인빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"빙수_팥인절미 눈꽃빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"탄산음료_패션 탱고티 레모네이드 피지오 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"탄산음료","source":"식품의약품안전처"},{"name":"스무디_퍼플 사워 블렌디드 (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"허브차_페어진저 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페어진저 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"샌드위치_페퍼로니 피자 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"허브차_페퍼민트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_페퍼민트 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"기타차_폼폼 민트티 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"스무디_퐁당치노 미숫가루","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_퐁당치노 바닐라","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"아이스크림_퐁스크림","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"아이스크림","source":"식품의약품안전처"},{"name":"스무디_퐁크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_퐁크러쉬 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"허브차_퓨어페퍼민트 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_퓨어페퍼민트 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"프레즐_프레즐","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"프레즐","source":"식품의약품안전처"},{"name":"스무디_프로틴 그릭요거트 아이스 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_프로틴 초콜릿 아이스 블렌디드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"코코아_플러피 판다 초콜릿 아이스(ICED) (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"코코아_플러피 판다 핫 초콜릿 핫(HOT) (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"코코아","source":"식품의약품안전처"},{"name":"스무디_플레인 그릭요거트 아이스 블렌디드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"베이글_플레인 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_플레인 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_플레인 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"베이글_플레인 베이글","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"베이글","source":"식품의약품안전처"},{"name":"와플_플레인 와플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"스무디_플레인 요거스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인 요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인 요거트 플랫치노","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"와플_플레인 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"와플","source":"식품의약품안전처"},{"name":"크로플_플레인 크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"스무디_플레인요거트","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인요거트 스무디","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인요거트 스무디 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인요거트 스무디 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"크로플_플레인크로플","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크로플","source":"식품의약품안전처"},{"name":"스무디_플레인퐁 크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"스무디_플레인허니퐁 크러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"기타차_피치망고 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_피치망고 (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"케이크_필라델피아 치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"케이크_필라델피아치즈 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"마카롱_핑크딸기 마카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"에이드_핑크리치 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_핑크리치 에이드 (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_한라 자몽 에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_한라봉 에이드 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"에이드_한라봉 에이드 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"과ㆍ채주스_한라봉 주스 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"과ㆍ채주스_한라봉주스 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"기타차_한라봉차 (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"기타차_한라봉차 (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"기타차","source":"식품의약품안전처"},{"name":"케이크_한라봉홍차 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"과ㆍ채주스_한방에 쭉 감당 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"번_핫 치즈번","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"번","source":"식품의약품안전처"},{"name":"핫도그_핫도그","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"핫도그","source":"식품의약품안전처"},{"name":"또띠아_핫치킨 브리또","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"또띠아","source":"식품의약품안전처"},{"name":"샌드위치_햄&에그 로메인 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_햄앤치즈 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_햄앤치즈샌드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_햄에그 파니니","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"샌드위치_햄치즈 샌드위치","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"샌드위치","source":"식품의약품안전처"},{"name":"과ㆍ채주스_햇사과 주스 병음료","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"피자_허니 고르곤졸라 스퀘어 피자","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"피자","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 밀크티 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_허니 밀크티 핫(HOT) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"허니브레드_허니 카라멜 브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"허니브레드_허니브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"허니브레드_허니브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"허니브레드_허니브레드볼","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"허니브레드_허니초코브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"허니브레드_허니카라멜브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"허니브레드","source":"식품의약품안전처"},{"name":"케이크_헤이즐넛초콜릿 케이크","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"케이크","source":"식품의약품안전처"},{"name":"페이스트리_현무암돌빵","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"페이스트리","source":"식품의약품안전처"},{"name":"스무디_현미 밀크 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"라떼_호두 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"과ㆍ채주스_홍시 주스","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"과ㆍ채주스","source":"식품의약품안전처"},{"name":"자몽차_홍자몽차 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"자몽차_홍자몽차 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"자몽차","source":"식품의약품안전처"},{"name":"뱅쇼_화이트 뱅쇼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"뱅쇼","source":"식품의약품안전처"},{"name":"라떼_화이트 초콜릿 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_화이트 초콜릿 아이스(ICED) (EX)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_화이트 초콜릿 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_화이트 초콜릿 핫(HOT) (EX)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_화이트 타이거 프라푸치노 (Grande)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"마카롱_황치즈 뚱카롱","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"마카롱","source":"식품의약품안전처"},{"name":"라떼_흑당 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_흑당 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_흑당 라떼 핫(HOT)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"밀크티/버블티_흑당 밀크티 아이스(ICED) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_흑당 밀크티 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_흑당 밀크티 아이스(ICED) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_흑당 밀크티 핫(HOT) (L)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"밀크티/버블티_흑당 밀크티 핫(HOT) (XL)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"밀크티/버블티","source":"식품의약품안전처"},{"name":"라떼_흑당 버블 라떼 아이스(ICED) (M)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_흑당고구마 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_흑당버블 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"라떼_흑당버블 라떼 아이스(ICED)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"크림빵_흑당크림브레드","caffeineMg":0.0,"basis":"100g","major":"빵 및 과자류","rep":"크림빵","source":"식품의약품안전처"},{"name":"빙수_흑임자 컵빙수","caffeineMg":0.0,"basis":"100g","major":"유제품류 및 빙과류","rep":"빙수","source":"식품의약품안전처"},{"name":"라떼_흑호 라떼","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"라떼","source":"식품의약품안전처"},{"name":"스무디_흰둥이 바닐라 밀크 쉐이크","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"},{"name":"에이드_히비스엘더에이드","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"에이드","source":"식품의약품안전처"},{"name":"허브차_히비스커스 블렌드티 아이스(ICED) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_히비스커스 블렌드티 핫(HOT) (Tall)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_히비스커스 아이스(ICED) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"허브차_히비스커스 핫(HOT) (R)","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"허브차","source":"식품의약품안전처"},{"name":"스무디_히비스커스펀치슬러쉬","caffeineMg":0.0,"basis":"100mL","major":"음료 및 차류","rep":"스무디","source":"식품의약품안전처"}];

// ------------------------------
// ✅ 식약처(foodsafetykorea) 카페인 DB 자동 입력 (엑셀 기반 내장)
// - #product-name 입력창에서 2글자 이상 입력 시 자동 추천(최대 25개)
// - 항목을 선택하면 #caffeine-mg 자동 채움 + 기준량을 섭취량 메모에 힌트로 추가
// ------------------------------
const KFD_NAME_TO_ITEM = new Map(KFD_CAFFEINE_DB.map(x => [x.name, x]));

// 간단 카테고리 매핑(원하면 나중에 더 정교화 가능)
function kfdGuessCategory(item){
  const major = (item?.major || '') + ' ' + (item?.rep || '');
  if (/음료|차류|커피|에너지|탄산|주스|우유/.test(major)) return 'drink';
  if (/과자|초콜릿|디저트|빵|아이스크림|젤리|캔디|식품/.test(major)) return 'food';
  return 'other';
}

function kfdUpdateDatalist(query){
  const dl = document.getElementById('kfd-caffeine-list');
  if (!dl) return;
  dl.innerHTML = '';
  const q = (query || '').trim();
  if (q.length < 1) return;

  // 포함 검색 + 상위 N개
  const lower = q.toLowerCase();
  const hits = [];
  for (const it of KFD_CAFFEINE_DB){
    // name에 영어가 섞인 경우 대비
    if ((it.name || '').toLowerCase().includes(lower)){
      hits.push(it);
      if (hits.length >= 25) break;
    }
  }

  // datalist option: value는 name(선택 시 input에 그대로 들어감)
  
  // ✅ 입력값이 DB의 단일 항목과 정확히 일치하면(더 추천할 것이 없으면) 리스트를 닫기 위해 비워둠
  if (hits.length === 1){
    const only = hits[0];
    if ((only.name || '').toLowerCase() === lower){
      return; // dl은 이미 비워져 있음
    }
  }

for (const it of hits){
    const opt = document.createElement('option');
    opt.value = it.name;
    opt.label = `${it.caffeineMg}mg / ${it.basis}`;
    dl.appendChild(opt);
  }
}

function kfdApplySelected(productName){
  const item = KFD_NAME_TO_ITEM.get(productName);
  if (!item) return false;

  setKfdSelectedItemAndRecalc(item);

  
  // ✅ DB 선택 시: 제품명 입력칸을 DB의 "전체 이름"으로 고정 + 저장용 메타데이터 부여
  const pnEl = document.getElementById('product-name');
  if (pnEl && item){
    pnEl.value = item.name || pnEl.value;
    pnEl.dataset.kfdSelectedId = String(item.id || '');
    pnEl.dataset.kfdSelectedName = String(item.name || '');
    // ✅ 선택 완료 처리: 추천 리스트 닫기 + 입력(타이핑) 상태 종료
    pnEl.dataset.kfdLocked = '1';
    // datalist(추천 옵션) 비우기 → 같은 값으로 추천이 다시 뜨는 현상 방지
    const dl = document.getElementById('kfd-caffeine-list');
    if (dl) dl.innerHTML = '';
    // 포커스 해제(드롭다운 닫힘)
    setTimeout(() => { try { pnEl.blur(); } catch(e){} }, 0);
  }
const cafInput = document.getElementById('caffeine-mg');
  const amountNote = document.getElementById('amount-note');
  const categorySel = document.getElementById('category');

  // 카페인 자동 입력 (기준량 대비 mg)
  if (cafInput) cafInput.value = Math.round(Number(item.caffeineMg) || 0);

  // 섭취량 메모 힌트(비어있거나, 자동추정 힌트가 없을 때만)
  if (amountNote){
    const hint = `기준량: ${item.basis}`;
    if (!amountNote.value) amountNote.value = hint;
    else if (!amountNote.value.includes('기준량:')) amountNote.value = `${amountNote.value} · ${hint}`;
  }

  // 카테고리 추정
  if (categorySel){
    const guessed = kfdGuessCategory(item);
    if (guessed) categorySel.value = guessed;
  }

  // 작은 안내(있으면)
  const pHint = document.getElementById('photo-hint');
  if (pHint){
    pHint.innerHTML = `* 식약처 DB 선택됨: <b>${item.name}</b> (카페인 <b>${item.caffeineMg}mg</b> / ${item.basis})`;
  }

  return true;
}

/* ================================
   ✅ KFD 매칭 기반 "섭취량 변경 시 카페인 자동 재계산"
   - KFD에서 선택된 item을 기억
   - amount-note에서 mL/g를 읽어 item.basis 대비 비율로 caffeine-mg 자동 갱신
================================== */

// 현재 KFD에서 "선택 적용"된 항목을 기억
let KFD_SELECTED_ITEM = null;

/** "100mL", "355ml", "60 g", "1회 제공량 100mL" 같은 문자열에서 {qty, unit} 뽑기 */
function parseQtyUnit(str) {
  if (!str) return null;
  const s = String(str).trim();
  // mL/ml/L/g/잔/컵 지원
if (/^\d+(\.\d+)?$/.test(s)) {
  return { qty: parseFloat(s), unit: 'ml' };
}
  const m = s.match(/([0-9]+(?:\.[0-9]+)?)\s*(m?l|ml|l|g|잔|컵)/i);
  if (!m) return null;

  const qty = parseFloat(m[1]);
  let unit = String(m[2]).toLowerCase();

  if (!Number.isFinite(qty)) return null;
  if (unit === 'l') return { qty: qty * 1000, unit: 'ml' }; // L -> mL
  if (unit === 'ml' || unit === 'm?l') return { qty, unit: 'ml' };
  if (unit === 'g') return { qty, unit: 'g' };
  if (unit === '잔') return { qty, unit: '잔' };
  if (unit === '컵') return { qty, unit: '컵' };
  return { qty, unit };
}

/** amount-note에서 사용자가 적은 mL/g를 최대한 찾아냄 (여러 개면 "마지막 값" 우선) */
function extractUserQtyUnitFromAmountNote(note) {
  if (!note) return null;
  // '125mL', '200 ml', '2잔', '1컵', '0.5L', '100g' 등을 파싱
  return parseQtyUnit(String(note).trim());
}

/** KFD_SELECTED_ITEM + amount-note 기반으로 caffeine-mg를 자동 갱신 */
function recalcCaffeineFromKfdAmount() {
  if (!KFD_SELECTED_ITEM) return;

  const cafInput = document.getElementById('caffeine-mg');
  const amountEl = document.getElementById('amount-note');
  // ✅ 빠른 입력(자연수 스크롤 + 직접입력) → amount-note 반영
  const qtyEl = document.getElementById('amount-qty');
  const unitEl = document.getElementById('amount-unit');
  const applyBtn = document.getElementById('amount-apply');

  const applyQuickAmount = () => {
    if (!amountEl) return;
    const q = qtyEl ? parseFloat(qtyEl.value) : NaN;
    const u = unitEl ? unitEl.value : 'ml';
    if (!Number.isFinite(q) || q <= 0) return;

    if (u === 'ml') amountEl.value = `${Math.round(q)}mL`;
    else amountEl.value = `${q}${u}`; // 잔/컵

    recalcCaffeineFromKfdAmount();
  };

  if (applyBtn) applyBtn.addEventListener('click', applyQuickAmount);
  if (qtyEl) qtyEl.addEventListener('input', applyQuickAmount);
  if (unitEl) unitEl.addEventListener('change', applyQuickAmount);

  if (!cafInput) return;

  const baseMg = Number(KFD_SELECTED_ITEM.caffeineMg) || 0;

  // 1) 기준량(basis) 파싱: basis 우선, 없으면 volumeML/volumeMl 같은 숫자 필드 활용
  let basisParsed = parseQtyUnit(KFD_SELECTED_ITEM.basis);

  if (!basisParsed || !basisParsed.qty || !basisParsed.unit) {
    const fb = KFD_SELECTED_ITEM.volumeML ?? KFD_SELECTED_ITEM.volumeMl ?? KFD_SELECTED_ITEM.volMl ?? KFD_SELECTED_ITEM.volML ?? null;
    const n = (typeof fb === 'number') ? fb : (fb != null ? parseFloat(String(fb).replace(/[^0-9.]/g,'')) : NaN);
    if (Number.isFinite(n) && n > 0) {
      basisParsed = { qty: n, unit: 'ml' };
    }
  }

  // 기준량을 끝까지 못 얻으면: DB 값 유지 (곱셈 폭주 방지)
  if (!basisParsed || !basisParsed.qty || !basisParsed.unit) {
    cafInput.value = Math.round(baseMg);
    return;
  }

  // 2) 사용자 입력 파싱
  const userParsed = extractUserQtyUnitFromAmountNote(amountEl ? amountEl.value : '');

  // 사용자가 단위를 안 썼으면: DB 값 유지
  if (!userParsed || !userParsed.qty || !userParsed.unit) {
    cafInput.value = Math.round(baseMg);
    return;
  }

  // 3) 잔/컵은 '배수'로 처리 (1잔/1컵 = DB의 1회 제공량 기준)
  if (userParsed.unit === '잔' || userParsed.unit === '컵') {
    const mult = userParsed.qty;
    cafInput.value = Math.round(baseMg * mult);
    return;
  }

  // 4) mL/g는 기준량 대비 비례 계산
  if (userParsed.unit !== basisParsed.unit) {
    cafInput.value = Math.round(baseMg); // 단위 불일치면 안전하게 유지
    return;
  }

  const ratio = userParsed.qty / basisParsed.qty;
  const newMg = baseMg * ratio;
  cafInput.value = Math.round(newMg);
}

/** 외부에서 KFD_SELECTED_ITEM을 세팅하고 즉시 재계산까지 실행 */
function setKfdSelectedItemAndRecalc(item) {
  KFD_SELECTED_ITEM = item || null;
  recalcCaffeineFromKfdAmount();
}

// amount-note가 바뀔 때마다 자동 재계산 이벤트 연결
document.addEventListener('DOMContentLoaded', () => {
  const amountEl = document.getElementById('amount-note');
  if (!amountEl) return;

  // 입력 중/입력 완료 둘 다 대응
  amountEl.addEventListener('input', () => recalcCaffeineFromKfdAmount());
  amountEl.addEventListener('change', () => recalcCaffeineFromKfdAmount());
});


// 이벤트 연결

  // ✅ [KFD 자동재계산] amount-note 변경 시 (선택된 KFD 항목 기준) 카페인 자동 수정
  // - 기존 코드가 어떤 화면(추가/수정)에서 amount-note를 만들더라도 동작하도록 "이벤트 위임" 방식으로 한 번만 연결합니다.
  document.addEventListener('input', (ev) => {
    const el = ev.target;
    if (!el) return;
    if (el.classList && el.classList.contains('amount-note')) {
      try { recalcCaffeineFromKfdAmount(el); } catch (e) {}
    }
  }, true);

  document.addEventListener('change', (ev) => {
    const el = ev.target;
    if (!el) return;
    if (el.classList && el.classList.contains('amount-note')) {
      try { recalcCaffeineFromKfdAmount(el); } catch (e) {}
    }
  }, true);
document.addEventListener('DOMContentLoaded', () => {
  const pn = document.getElementById('product-name');
  if (!pn) return;
 const qtyList = document.getElementById('amount-qty-list');
  if (qtyList) {
    qtyList.innerHTML = '';
    for (let n = 1; n <= 300; n += 1) {
      const opt = document.createElement('option');
      opt.value = String(n);
      qtyList.appendChild(opt);
    }
  }

  // ✅ (추가) 섭취량 숫자 드롭다운을 다시 열 때 "선택된 숫자 기준으로 필터링"되지 않도록,
  //    포커스/클릭 시 현재 값을 잠시 비워 전체(1~300) 자연수가 항상 보이게 강제합니다.
  //    - 선택 없이 빠져나오면 이전 값 복원
  const qtyInput = document.getElementById('amount-qty');
  if (qtyInput) {
    const stashPrev = () => { qtyInput.dataset.prevQty = qtyInput.value || ''; };
    const clearForAll = () => {
      // 이미 비어있으면 그대로
      if (qtyInput.value !== '') {
        stashPrev();
        // datalist 후보가 "현재 입력값"으로 필터링되는 것을 방지
        qtyInput.value = '';
        // 일부 브라우저는 value 변경 후 렌더 지연이 있어 다음 틱에서 한 번 더 비움
        setTimeout(() => { if (document.activeElement === qtyInput) qtyInput.value = ''; }, 0);
      }
    };

    // 클릭/터치로 열 때
    qtyInput.addEventListener('pointerdown', () => { clearForAll(); }, { passive: true });
    // 키보드 탭 등으로 포커스될 때도 동일 처리
    qtyInput.addEventListener('focus', () => { clearForAll(); });

    // 선택 없이 벗어나면 이전 값 복원
    qtyInput.addEventListener('blur', () => {
      const prev = qtyInput.dataset.prevQty || '';
      if (qtyInput.value === '' && prev) qtyInput.value = prev;
      delete qtyInput.dataset.prevQty;
    });
  }

  // 입력 중 추천 업데이트
  let t = null;
  pn.addEventListener('input', (e) => {
    // ✅ DB 추천에서 하나를 '선택 완료'한 직후엔 다시 추천이 뜨지 않게 잠금
    //    (단, 사용자가 값을 수정하기 시작하면 잠금 해제)
    if (pn.dataset.kfdLocked === '1') {
      const lockedName = String(pn.dataset.kfdSelectedName || '');
      const cur = String(e.target.value || '');
      if (lockedName && cur === lockedName) return; // 그대로면 추천 업데이트 중지
      // 사용자가 수정 시작 → 잠금 해제
      delete pn.dataset.kfdLocked;
      delete pn.dataset.kfdSelectedId;
      delete pn.dataset.kfdSelectedName;
    }
    const v = e.target.value || '';
    clearTimeout(t);
    t = setTimeout(() => kfdUpdateDatalist(v), 120);
  });

  // ✅ 세 번째 항목(용량 스크롤)처럼: 다시 사용할 때도 추천이 항상 재생성되도록 focus에서도 갱신
  pn.addEventListener('focus', () => {
    const v = (pn.value || '').trim();
    kfdUpdateDatalist(v);
  });

  // ✅ 입력창을 벗어나면 추천 리스트 비우기(남아있는 목록 방지)
  pn.addEventListener('blur', () => {
    const dl = document.getElementById('kfd-caffeine-list');
    if (!dl) return;
    // 클릭 선택 직후 blur가 먼저 오면 change가 못 잡힐 수 있어 약간 지연
    setTimeout(() => { dl.innerHTML = ''; }, 120);
  });

  
  // ✅ 사용자가 직접 타이핑을 시작하면(=DB 선택 상태 해제) 저장용 KFD 메타데이터 초기화
  pn.addEventListener('input', () => {
    // DB에서 선택 완료(locked) 상태면 메타데이터 유지
    if (pn.dataset.kfdLocked === '1') return;
    pn.dataset.kfdSelectedId = '';
    pn.dataset.kfdSelectedName = '';
  }, { once:false });
// datalist에서 선택되면 자동 적용
  pn.addEventListener('change', (e) => {
    const v = (e.target.value || '').trim();
    kfdApplySelected(v);
  });
});

const PRODUCT_SHORTCUT_DEFS = [
  {
    id: 'starbucks_ame_tall',
    icon: '☕',
    label: '스타벅스 아메리카노 톨',
    caffeineMg: 150,
    volume: '355ml (톨)',
    defaultAmountNote: '1잔'
  },
  {
    id: 'paiks_iced_tea',
    icon: '🧊',
    label: '빽다방 아이스티',
    caffeineMg: 21,
    volume: '24oz',
    defaultAmountNote: '1잔'
  },
  {
    id: 'monster_355',
    icon: '⚡',
    label: '몬스터 에너지 355ml',
    caffeineMg: 100,
    volume: '355ml',
    defaultAmountNote: '1캔'
  }
];

const EFFECT_DEFS = [
  { id:'palpitation', icon:'💓', label:'심장 두근거림', tip:'일시적으로 카페인 섭취를 중단하고, 깊게 숨을 쉬며 휴식을 취하세요. 증상이 계속되면 보호자·의사와 상의해야 합니다.' },
  { id:'insomnia', icon:'🌙', label:'불면증', tip:'늦은 오후 이후 카페인 섭취를 피하고, 취침 1시간 전에는 스마트폰·밝은 화면을 줄이는 것이 좋습니다.' },
  { id:'anxiety', icon:'😰', label:'초조/불안', tip:'물을 충분히 마시고, 짧은 산책·스트레칭으로 몸을 풀어 주세요. 불안이 심하면 상담 선생님·전문의와 상의하세요.' },
  { id:'headache', icon:'🤕', label:'두통', tip:'물을 마시고, 조용하고 어두운 곳에서 잠깐 눈을 감고 쉬는 것이 도움이 될 수 있습니다. 일상에 지장을 줄 정도라면 병원 진료가 필요합니다.' },
  { id:'stomach', icon:'🤢', label:'속쓰림/메스꺼움', tip:'공복 카페인을 피하고, 가볍게 식사를 한 뒤 따뜻한 물을 조금씩 마시세요. 구토·복통이 심하면 보호자에게 바로 알리세요.' },
  { id:'tremor', icon:'🤲', label:'손발 떨림', tip:'손이나 발이 떨릴 때는 카페인 섭취를 중단하고, 물을 마시며 편한 자세로 휴식을 취하세요. 떨림이 오래 가거나 심하면 보호자·의사와 상의해야 합니다.' },
  { id:'etc', icon:'❓', label:'기타', tip:'자신이 느낀 증상을 자세히 적어 두면 의사·보호자가 상태를 파악하는 데 도움이 됩니다.' }
];

// ===== 개인차(민감도) 반영 =====
let EFFECT_SENS_MULT = Number(localStorage.getItem('EFFECT_SENS_MULT') || '1.0');
if (!Number.isFinite(EFFECT_SENS_MULT)) EFFECT_SENS_MULT = 1.0;
EFFECT_SENS_MULT = Math.min(1.5, Math.max(0.5, EFFECT_SENS_MULT));

function setEffectSensitivity(mult){
  const v = Number(mult);
  if (!Number.isFinite(v)) return;
  EFFECT_SENS_MULT = Math.min(1.5, Math.max(0.5, v));
  localStorage.setItem('EFFECT_SENS_MULT', String(EFFECT_SENS_MULT));
  updateSensitivityUI();
  try { renderUserEffectRiskSummary(); } catch(e) {}
}

function updateSensitivityUI(){
  const label = document.getElementById('sens-label');
  if (!label) return;
  let txt = '보통';
  if (EFFECT_SENS_MULT <= 0.9) txt = '둔감';
  else if (EFFECT_SENS_MULT >= 1.1) txt = '민감';
  label.textContent = `(${txt})`;
  // 버튼 active 처리
  const sec = document.getElementById('extra-section-effects');
  if (!sec) return;
  sec.querySelectorAll('[data-sens]').forEach(btn=>{
    const b = Number(btn.getAttribute('data-sens'));
    btn.classList.toggle('active', Math.abs(b - EFFECT_SENS_MULT) < 0.05);
  });
}

document.addEventListener('click', (ev)=>{
  const btn = ev.target && ev.target.closest && ev.target.closest('[data-sens]');
  if (!btn) return;
  ev.preventDefault();
  setEffectSensitivity(btn.getAttribute('data-sens'));
}, true);

document.addEventListener('DOMContentLoaded', ()=>{ updateSensitivityUI(); });



  const PEER_STORIES = [
    {
      id: 'palpitation',
      icon: '💓',
      label: '심장 두근거림',
      story: '고3 학생 / 에너지 드링크 2캔(약 300mg)을 빠르게 마신 뒤 심장이 빨리 뛰고 불안감을 느낌.',
      solution: '이후 오후 4시 이후에는 카페인을 마시지 않고, 하루 1잔만 천천히 마시는 습관으로 바꾸자 증상이 거의 사라짐.'
    },
    {
      id: 'insomnia',
      icon: '🌙',
      label: '불면증',
      story: '중3 학생 / 시험 기간마다 캔커피와 콜라를 함께 마시다가 새벽 3시까지 잠이 오지 않는 날이 계속됨.',
      solution: '수면일기를 쓰며 카페인 음료는 오후 2시 이전까지만 마시고, 저녁에는 물·우유로 바꾸자 11~12시 사이에 잠들 수 있게 됨.'
    },
    {
      id: 'stomach',
      icon: '🤢',
      label: '속쓰림',
      story: '고1 학생 / 아침을 거르고 라떼만 마셨다가 속이 메스껍고 쓰린 느낌이 반복됨.',
      solution: '“공복에 카페인 금지” 원칙을 세우고, 빵·바나나 등을 먼저 먹은 뒤 라떼를 마시자 속이 훨씬 편안해짐.'
    }
  ];

// ===== 부작용 가중치 기반 '카페인 위험도 점수' 계산 =====
// 설문 분석에서 도출한 가중치를 effectId 기준으로 매핑
const EFFECT_WEIGHTS = {
  palpitation: 0.83,  // 심장 두근거림
  insomnia:    1.00,  // 불면증
  headache:    0.33,  // 두통
  stomach:     0.33,  // 속쓰림/메스꺼움
  anxiety:     0.17,  // 초조/불안
  tremor:      0.08,  // 손발 떨림
  etc:         0.08   // 기타(경미한 증상)
};// (추가) 증상별 개인차(민감도) 배수 저장/로드
const EFFECT_PERSONAL_KEY = 'EFFECT_PERSONAL_MULT_V1';
function loadEffectPersonalMult(){
  try{
    const raw = localStorage.getItem(EFFECT_PERSONAL_KEY);
    const obj = raw ? JSON.parse(raw) : {};
    return (obj && typeof obj === 'object') ? obj : {};
  }catch(_){ return {}; }
}
function saveEffectPersonalMult(map){
  try{ localStorage.setItem(EFFECT_PERSONAL_KEY, JSON.stringify(map||{})); }catch(_){}
}
let EFFECT_PERSONAL_MULT = loadEffectPersonalMult();
function clamp(n, a, b){ return Math.max(a, Math.min(b, n)); }
function getPersonalMult(effectId){
  const v = Number(EFFECT_PERSONAL_MULT?.[effectId]);
  return clamp(Number.isFinite(v) ? v : 1, 0.5, 2.0);
}


// 개인차/민감도까지 반영했을 때의 "최대 점수"(정규화 기준)
// - 개인차 슬라이더는 증상별 배수로 가중치에 곱해짐
// - 민감도(EFFECT_SENS_MULT)는 전체 점수에 공통으로 곱해짐
function computeMaxEffectScore(){
  const keys = Object.keys(EFFECT_WEIGHTS);
  let sum = 0;
  for (const k of keys){
    const w = Number(EFFECT_WEIGHTS[k]) || 0;
    sum += w * (Number(getPersonalMult?.(k)) || 1);
  }
  return sum * (Number(window.EFFECT_SENS_MULT) || 1);
}

// sideEffects 배열(내 기록 전체)을 기준으로
// "어떤 증상을 한 번이라도 겪었는지"를 모아서 점수 계산
function computeUserEffectScore() {
  if (!sideEffects || sideEffects.length === 0) return 0;

  // effectId별로 한 번이라도 나타났으면 1로 처리 (중복 기록으로 점수 폭증 방지)
  const used = new Set();
  sideEffects.forEach(s => {
    if (s.effectId && EFFECT_WEIGHTS[s.effectId] !== undefined) used.add(s.effectId);
  });

  let score = 0;
  used.forEach(id => {
    const w = Number(EFFECT_WEIGHTS[id] || 0);
    const pm = Number(getPersonalMult(id) || 1); // 증상별 개인차(슬라이더) 반영
    score += (w * pm);
  });

  // 전체 민감도(공통 배수) 반영
  const sens = Number(EFFECT_SENS_MULT) || 1;
  return score * sens;
}

// 0~100점 환산 + 위험군(저/중/고) + "상위 몇 % 느낌" 텍스트 생성
function buildRiskIndicatorText() {
  const rawScore = computeUserEffectScore();
  if (rawScore <= 0) {
    return {
      visible: false,
      html: '지금까지 기록된 부작용이 없어서, 카페인 민감도 위험도는 매우 낮은 상태입니다.'
    };
  }

  const maxScore = Math.max(1e-6, computeMaxEffectScore());
  // 0~100점 정규화(개인차/민감도 포함). 100을 넘지 않도록 클램프.
  const normalized = Math.max(0, Math.min(100, (rawScore / maxScore) * 100));

  let level = '저위험';
  let percentText = '하위 50% 이상(상대적으로 안전한 편)';
  let emoji = '🟢';

  if (normalized >= 60 && normalized < 80) {
    level = '중위험';
    percentText = '대략 상위 30~40% 구간이라 꽤 민감한 편입니다.';
    emoji = '🟠';
  } else if (normalized >= 80) {
    level = '고위험';
    percentText = '대략 상위 20% 안에 들어가는 수준이라, 카페인에 상당히 민감한 편입니다.';
    emoji = '🔴';
  }

  // “상위 몇 %니깐 조심하셈” 느낌으로 메시지 구성
  const html = `
    <b>${emoji} 나의 부작용 위험도 점수 및 위험군</b><br>
    · <span class="risk-score">부작용 점수: </span><b>${normalized.toFixed(1)}점 / 100점</b> (${level})<br>
    · ${percentText}<br><br>
    최근에 기록한 부작용(두근거림, 불면, 두통, 속쓰림, 불안 등)을 기준으로 계산한 값이에요.<br>
    늦은 저녁·시험 기간에는 카페인 섭취량과 시간대를 조금 더 조심해서 조절해 보는 걸 추천합니다.
  `;

  return {
    visible: true,
    html
  };
}

// DOM에 실제로 뿌려주는 함수
function renderRiskIndicator() {
  const box = document.getElementById('risk-indicator-box');
  if (!box) return;

  const { visible, html } = buildRiskIndicatorText();
  if (!visible) {
    box.style.display = 'none';
    box.innerHTML = '';
    return;
  }

  box.style.display = 'block';
  box.innerHTML = html;
}



  function isSameDay(d1, d2) {
    return d1.getFullYear() === d2.getFullYear() &&
           d1.getMonth() === d2.getMonth() &&
           d1.getDate() === d2.getDate();
  }
  function formatDateTimeLocal(date) {
    const pad = n => String(n).padStart(2,'0');
    return `${date.getFullYear()}-${pad(date.getMonth()+1)}-${pad(date.getDate())}T${pad(date.getHours())}:${pad(date.getMinutes())}`;
  }
  function formatDateTimeView(date) {
    const pad = n => String(n).padStart(2,'0');
    return `${date.getFullYear()}-${pad(date.getMonth()+1)}-${pad(date.getDate())} ${pad(date.getHours())}:${pad(date.getMinutes())}`;
  }

  function loadData() {
    try {
      intakes = JSON.parse(localStorage.getItem('intakes') || '[]');
      sideEffects = JSON.parse(localStorage.getItem('sideEffects') || '[]');
const storedShortcuts = JSON.parse(localStorage.getItem('userProductShortcuts') || '[]');
      if (Array.isArray(storedShortcuts)) {
        userProductShortcuts = storedShortcuts;
      } else {
        userProductShortcuts = [];
      }

      const storedProfile = JSON.parse(localStorage.getItem('userProfile') || '{}');
      if (storedProfile && typeof storedProfile.weightKg === 'number' && storedProfile.weightKg > 0) {
        userProfile.weightKg = storedProfile.weightKg;
      }
    } catch (e) {
      intakes = [];
      sideEffects = [];
    }
    updateRecommendedFromProfile();
  }
  function saveData() {
    localStorage.setItem('intakes', JSON.stringify(intakes));
    localStorage.setItem('sideEffects', JSON.stringify(sideEffects));
  }
function saveUserProductShortcuts() {
  localStorage.setItem('userProductShortcuts', JSON.stringify(userProductShortcuts));
}
  function saveUserProfile() {
    localStorage.setItem('userProfile', JSON.stringify(userProfile));
  }
  function updateRecommendedFromProfile() {
    const w = userProfile.weightKg || DEFAULT_WEIGHT_KG;
    RECOMMENDED_MG = Math.round(w * 2.5);
    MAX_MG = RECOMMENDED_MG * 1.5;
    const wtInput = document.getElementById('weight-kg');
    if (wtInput) wtInput.value = w;
    const label = document.getElementById('cup-mark-label');
    if (label) label.textContent = `일일 권장 섭취량 (약 ${RECOMMENDED_MG} mg)`;
  }

  function updateEditSelect() {
    const sel = document.getElementById('edit-intake-select');
    if (!sel) return;
    const items = intakes.slice().sort((a,b)=>new Date(b.takenAt) - new Date(a.takenAt));
    if (!items.length) {
      sel.innerHTML = '<option value="">수정할 기록이 없습니다.</option>';
      return;
    }
    const pad = n => String(n).padStart(2,'0');
    sel.innerHTML = items.map(i => {
      const d = new Date(i.takenAt);
      const label = `[${pad(d.getMonth()+1)}/${pad(d.getDate())} ${pad(d.getHours())}:${pad(d.getMinutes())}] ${i.productName} (${i.caffeineMg}mg)`;
      return `<option value="${i.id}">${label}</option>`;
    }).join('');
  }

  function updateTodaySummary() {
    const today = new Date();
    let total = 0;
    let count = 0;
    intakes.forEach(i => {
      const d = new Date(i.takenAt);
      if (isSameDay(d, today)) {
        total += i.caffeineMg;
        count++;
      }
    });

    const summaryDiv = document.getElementById('today-summary');
    if (summaryDiv) {
      summaryDiv.innerHTML = `
        <div class="stat-row"><span>오늘 총 섭취량</span><span><b>${total.toFixed(0)} mg</b></span></div>
        <div class="stat-row"><span>기록된 섭취 횟수</span><span>${count}회</span></div>
      `;
    }

    const cupFill = document.getElementById('cup-fill');
    const cupText = document.getElementById('cup-text');
    const cupShell = document.getElementById('cup-gauge');
    const cupBody = document.querySelector('.cup-body');
    if (cupFill && cupText) {
      let percent = MAX_MG > 0 ? (total / MAX_MG) * 100 : 0;
      if (percent > 100) percent = 100;
      if (percent < 0) percent = 0;
      cupFill.style.height = `${percent}%`;
      cupText.textContent = `${total.toFixed(0)} mg`;

      if (cupShell && total > RECOMMENDED_MG && !window._cupAlertShown) {
        window._cupAlertShown = true;
        const showOnce = () => {
          cupShell.classList.add('alert');
          if (cupBody) cupBody.classList.add('shake');
          setTimeout(() => {
            cupShell.classList.remove('alert');
            if (cupBody) cupBody.classList.remove('shake');
          }, 2000);
        };
        showOnce();
        setTimeout(showOnce, 2500);
      }
    }
  }

  // ===== OCR 함수 (all_ocr 수정.html에서 가져와 통합) =====
  async function runOCR(file) {
    const apiKey = "K87918974988957";  // ★ 실제 사용할 때는 본인 키로 교체

   const formData = new FormData();
  formData.append("apikey", apiKey);
  formData.append("language", "kor");          // 한글 OCR
  formData.append("isOverlayRequired", "false");
  formData.append("OCREngine", "2");           // ★★ 핵심: 엔진2 사용 설정 ★★
  formData.append("file", file);

  const response = await fetch("https://api.ocr.space/parse/image", {
    method: "POST",
    body: formData,
  });

  const result = await response.json();
  if (result.ParsedResults && result.ParsedResults.length > 0) {
    return result.ParsedResults[0].ParsedText;
  }
  return "";
}
// [OCR 함수 끝 - 엔진2 사용 버전]


  function guessFromFilename(name) {
    // 파일명 전체를 소문자로
    name = name.toLowerCase();

    // 1) 먼저 PRODUCT_DB에서 정확히 아는 상품인지 확인
    const dbHit = PRODUCT_DB.find(p =>
      p.keyWords.some(k => name.includes(k.toLowerCase()))
    );
    if (dbHit) {
      return {
        mg: dbHit.caffeineMg,
        label: `${dbHit.name} (${dbHit.volumeMl}ml, 약 ${dbHit.caffeineMg}mg)`
      };
    }

    // 2) DB에 없으면 기존 규칙 사용
    if (name.includes('coffee') || name.includes('cafe') || name.includes('latte') || name.includes('americano')) {
      return { mg: 80, label: '커피(추정)' };
    }
    if (name.includes('energy')) {
      return { mg: 120, label: '에너지 드링크(추정)' };
    }
    if (name.includes('tea') || name.includes('green')) {
      return { mg: 40, label: '차/티(추정)' };
    }
    if (name.includes('cola') || name.includes('coke')) {
      return { mg: 30, label: '콜라/탄산음료(추정)' };
    }
    if (name.includes('choco') || name.includes('chocolate')) {
      return { mg: 30, label: '초콜릿/디저트(추정)' };
    }
    if (name.includes('snack') || name.includes('cookie') || name.includes('cake')) {
      return { mg: 20, label: '간식/과자(추정)' };
    }
    return null;
  }

function guessFromProductName(text) {
  const name = (text || '').toLowerCase();
  if (!name) return null;

  // 0) ✅ 식약처(DB) 카페인 데이터가 있으면, 먼저 그 값을 우선 적용
  // - "제품명 기반 자동 추정" 버튼에서도 DB 카페인 정보를 자동 입력
  try{
    const raw = String(text || '').trim();
    if (raw.length >= 2 && typeof kfdApplySelected === 'function' && typeof KFD_CAFFEINE_DB !== 'undefined'){
      // 정확 일치 우선
      let pick = (typeof KFD_NAME_TO_ITEM !== 'undefined' && KFD_NAME_TO_ITEM instanceof Map) ? (KFD_NAME_TO_ITEM.get(raw) || null) : null;

      // 부분 일치(가장 먼저 매칭되는 항목)
      if (!pick){
        const lower = raw.toLowerCase();
        for (const it of KFD_CAFFEINE_DB){
          const nm = String(it?.name || '').toLowerCase();
          if (nm.includes(lower)){
            pick = it; break;
          }
        }
      }

      if (pick && pick.name){
        // 전체 제품명으로 고정 + KFD 로직 적용(카페인 자동 입력/기준량 힌트/비례계산 준비)
        const pnEl = document.getElementById('product-name');
        if (pnEl) pnEl.value = pick.name;
        kfdApplySelected(pick.name);
        return { mg: pick.caffeineMg, label: `${pick.name} (${pick.caffeineMg}mg / ${pick.basis})` };
      }
    }
  }catch(e){}


  // 1) 먼저 OCR와 동일한 음절 매칭으로 DB 검색
  const dbHit = findProductBySyllables(text);
  if (dbHit) {
    return {
      mg: dbHit.caffeineMg,
      label: `${dbHit.name} (${dbHit.volumeMl}ml, 약 ${dbHit.caffeineMg}mg)`
    };
  }

  // 2) PRODUCT_DB 키워드에 직접 포함되는지 확인
  const dbDirect = PRODUCT_DB.find(p =>
    p.keyWords.some(k => name.includes(k.toLowerCase()))
  );
  if (dbDirect) {
    return {
      mg: dbDirect.caffeineMg,
      label: `${dbDirect.name} (${dbDirect.volumeMl}ml, 약 ${dbDirect.caffeineMg}mg)`
    };
  }

  // 3) DB에 없으면 기존 규칙 사용
  if (name.includes('아메리카노') || name.includes('americano')) {
    return { mg: 100, label: '아메리카노(추정)' };
  }
  if (name.includes('에스프레소') || name.includes('espresso')) {
    return { mg: 80, label: '에스프레소(추정)' };
  }
  if (name.includes('라떼') || name.includes('latte')) {
    return { mg: 75, label: '라떼/우유커피(추정)' };
  }
  if (name.includes('콜라') || name.includes('cola') || name.includes('coke')) {
    return { mg: 30, label: '콜라/탄산음료(추정)' };
  }
  if (name.includes('에너지') || name.includes('몬스터') || name.includes('레드불') || name.includes('energy')) {
    return { mg: 120, label: '에너지 드링크(추정)' };
  }
  if (name.includes('티') || name.includes('tea') || name.includes('녹차') || name.includes('그린티')) {
    return { mg: 40, label: '차/티(추정)' };
  }
  if (name.includes('초콜릿') || name.includes('초코') || name.includes('choco') || name.includes('chocolate')) {
    return { mg: 30, label: '초콜릿/디저트(추정)' };
  }
  if (name.includes('쿠키') || name.includes('cookie') || name.includes('케이크') || name.includes('cake')) {
    return { mg: 20, label: '간식/과자(추정)' };
  }

  return null;
}

  // ---- 지식인 JSON + 샘플 필터링 & 렌더링 ----
  function filterPopularProducts(keyword) {
    const kw = (keyword || '').trim().toLowerCase();
    if (!kw) return POPULAR_PRODUCTS_SAMPLE;
    return POPULAR_PRODUCTS_SAMPLE.filter(p =>
      p.name.toLowerCase().includes(kw) ||
      (p.category || '').toLowerCase().includes(kw)
    );
  }

  function renderPopularProducts(list) {
    const tbody = document.getElementById('popular-products-body');
    if (!tbody) return;
    if (!list.length) {
      tbody.innerHTML = '<tr><td colspan="5" style="padding:4px;">검색 결과가 없습니다. 키워드를 바꾸거나 비워서 다시 시도해 보세요.</td></tr>';
      return;
    }
    tbody.innerHTML = list.map(item => `
      <tr>
        <td style="padding:4px; border-bottom:1px solid #d1fae5;">${item.rank ?? ''}</td>
        <td style="padding:4px; border-bottom:1px solid #d1fae5;">${item.name}</td>
        <td style="padding:4px; border-bottom:1px solid #d1fae5;">${item.category ?? ''}</td>
        <td style="padding:4px; border-bottom:1px solid #d1fae5; text-align:right;">${item.count ?? ''}</td>
        <td style="padding:4px; border-bottom:1px solid #d1fae5; text-align:right;">${item.caffeineMg ?? '-'}</td>
      </tr>
    `).join('');
  }

  // popular_products.json(지식인 크롤링 결과)을 읽어오는 함수
  async function loadPopularProducts(keyword) {
    try {
      const res = await fetch('popular_products.json'); // 같은 폴더에 위치
      if (!res.ok) throw new Error('HTTP ' + res.status);
      const all = await res.json(); // [{rank,name,category,count,caffeineMg}, ...]
      const kw = (keyword || '').trim();
      if (!kw) return all;
      return all.filter(p =>
        (p.name && p.name.includes(kw)) ||
        (p.category && p.category.includes(kw))
      );
    } catch (err) {
      console.error('popular_products.json 로드 실패, 샘플로 대체합니다.', err);
      return filterPopularProducts(keyword);
    }
  }

document.addEventListener('change', function(e) {
  // ★ 파일 선택 시: 파일명이 아니라 OCR 결과 텍스트를 기준으로 제품명/카페인 추정
  if (e.target.id === 'photo-input') {
    const file = e.target.files[0];
    if (!file) return;

    const caffeineInput = document.getElementById('caffeine-mg');
    const productInput  = document.getElementById('product-name');
    const hint          = document.getElementById('photo-hint');

    if (hint) {
      hint.textContent = '이미지에서 라벨 텍스트를 분석하는 중입니다...';
    }

    // 1) OCR 실행 → 텍스트 기반으로 제품명 / 카페인 양 추정
    runOCR(file).then(text => {
      const rawText = (text || '').trim();

      if (!rawText) {
        // OCR 자체가 실패한 경우: 마지막 수단으로만 파일명 사용
        const fileGuess = guessFromFilename(file.name || '');
        if (fileGuess && caffeineInput && !caffeineInput.value) {
          caffeineInput.value = fileGuess.mg;
        }
        if (productInput && !productInput.value && fileGuess) {
          productInput.value = fileGuess.label;
        }
        if (hint) {
          hint.innerHTML = 'OCR로 라벨 텍스트를 읽지 못했습니다. ' +
                           (fileGuess
                             ? `파일명을 기준으로 <b>${fileGuess.label}</b>로 추정하여 약 <b>${fileGuess.mg}</b> mg로 입력했습니다. 실제와 다를 수 있습니다.`
                             : '제품명 또는 카페인 양을 직접 입력해 주세요.');
        }
        return;
      }

      // 2) OCR 텍스트에서 제품명 후보(첫 번째 의미 있는 줄) 뽑기
      const lines = rawText.split('\n').map(l => l.trim()).filter(l => l.length > 0);
      const firstLine = lines[0] || rawText;
      if (productInput && !productInput.value) {
        productInput.value = firstLine;
      }

      // 3) OCR 텍스트에서 "숫자 + mg" 형식 직접 추출 (예: 100mg)
      let mgFromLabel = null;
      const mgMatch = rawText.match(/(\d+)\s*mg/i);
      if (mgMatch) {
        mgFromLabel = parseInt(mgMatch[1], 10);
      }

      // 4) OCR 전체 텍스트를 상품 DB와 음절 단위로 대조
      let dbProduct = findProductBySyllables(rawText);   // ★ [SYLLABLE_MATCH_UTIL] 사용
      let guess = null;

      if (dbProduct) {
        // DB에 있는 상품과 음절 매칭이 된 경우
        guess = {
          mg: dbProduct.caffeineMg,
          label: `${dbProduct.name} (${dbProduct.volumeMl}ml, 약 ${dbProduct.caffeineMg}mg)`
        };

        // 제품명 칸을 DB 상품명으로 보정
        if (productInput && !productInput.value) {
          productInput.value = dbProduct.name;
        }
      } else if (!mgFromLabel) {
        // DB에서도 못 찾고, mg 숫자도 없을 때 → 기존 제품명 기반 추정 사용
        guess = guessFromProductName(firstLine || rawText);
      }

      // 5) 카페인 입력칸 채우기 (이미 직접 입력한 값이 없을 때만 자동 입력)
      if (caffeineInput && !caffeineInput.value) {
        if (mgFromLabel) {
          caffeineInput.value = mgFromLabel;
        } else if (guess) {
          caffeineInput.value = guess.mg;
        }
      }

      // 6) 안내문 구성
      if (hint) {
        let msg = 'OCR로 라벨 텍스트를 인식했습니다.';
        if (firstLine) {
          msg += ` (예: "<b>${firstLine}</b>")`;
        }
        if (mgFromLabel) {
          msg += ` 라벨에서 <b>${mgFromLabel}mg</b> 문구를 찾아 카페인 양을 자동 입력했습니다.`;
        } else if (dbProduct && guess) {
          msg += ` 인식된 텍스트와 상품 DB를 음절 단위로 대조하여 <b>${guess.label}</b>로 판단하고, 약 <b>${guess.mg}</b> mg로 자동 입력했습니다.`;
        } else if (guess) {
          msg += ` 라벨에 나타난 제품명을 바탕으로 <b>${guess.label}</b>로 추정하여 약 <b>${guess.mg}</b> mg로 자동 입력했습니다.`;
        } else {
          msg += ' 다만 카페인 양/종류를 정확히 찾지 못해, 제품명 또는 카페인 양은 직접 확인해 주세요.';
        }
        hint.innerHTML = msg;
      }

    }).catch(err => {
      console.error('OCR 에러:', err);
      const caffeineInput = document.getElementById('caffeine-mg');
      const productInput  = document.getElementById('product-name');
      const hint          = document.getElementById('photo-hint');

      // OCR도 실패하면 마지막으로만 파일명 추정 사용
      const fileGuess = guessFromFilename(file.name || '');
      if (fileGuess && caffeineInput && !caffeineInput.value) {
        caffeineInput.value = fileGuess.mg;
      }
      if (productInput && !productInput.value && fileGuess) {
        productInput.value = fileGuess.label;
      }
      if (hint) {
        hint.innerHTML =
          '이미지 분석 중 오류가 발생했습니다. ' +
          (fileGuess
            ? `파일명을 기준으로 <b>${fileGuess.label}</b>로 추정하여 약 <b>${fileGuess.mg}</b> mg로 입력했습니다. 실제와 다를 수 있습니다.`
            : '제품명 또는 카페인 양을 직접 입력해 주세요.');
      }
    });

    return; // 이하 다른 change 핸들러로 내려가지 않도록 여기서 종료
  }

  // ★ 나머지 change 핸들러들은 기존 코드 그대로 유지
  if (e.target.id === 'period-select') {
    updateStats();
  }
  if (e.target.id === 'sleep-time' || e.target.id === 'caffeine-range') {
    updateCaffeineGraph();
  }
  if (e.target.id === 'weight-kg') {
    const val = parseFloat(e.target.value || '0');
    if (!isNaN(val) && val > 0) {
      userProfile.weightKg = val;
      updateRecommendedFromProfile();
      saveUserProfile();
      updateTodaySummary();
      updateStats();
      updateCaffeineGraph();
    }
  }
});

  document.addEventListener('click', function(e) {
    if (e.target.id === 'now-btn') {
      const input = document.getElementById('intake-time');
      if (input) input.value = formatDateTimeLocal(new Date());
      return;
    }
    if (e.target.id === 'guess-from-name-btn') {
      const nameInput = document.getElementById('product-name');
      const caffeineInput = document.getElementById('caffeine-mg');
      const hint = document.getElementById('photo-hint');
      const text = nameInput ? nameInput.value.trim() : '';
      if (!text) {
        alert('먼저 제품/음식 이름을 입력해 주세요.');
        return;
      }
      const guessed = guessFromProductName(text);
      if (!guessed) {
        alert('해당 제품명에서는 카페인 양을 추정하기 어렵습니다. 직접 입력해 주세요.');
        return;
      }
      if (caffeineInput.value) {
        if (!confirm('이미 입력된 카페인 양이 있습니다. 제품명 기준 추정값으로 덮어쓸까요?')) return;
      }
      caffeineInput.value = guessed.mg;
      if (hint) {
        hint.innerHTML = `제품명을 바탕으로 <b>${guessed.label}</b>로 인식하여 약 <b>${guessed.mg}</b> mg로 자동 입력했습니다. 실제 상품과는 차이가 있을 수 있습니다.`;
      }
      return;
    }
    if (e.target.id === 'edit-mode-btn') {
      const box = document.getElementById('edit-tools');
      if (!box) return;
      const visible = box.style.display !== 'none';
      box.style.display = visible ? 'none' : 'block';
      if (!visible) updateEditSelect();
      return;
    }
    // ✅ 자주 마시는 메뉴 아이콘 - 사용자 정의 추가
    if (e.target.id === 'product-shortcut-add-btn') {
      const nameInput   = document.getElementById('product-shortcut-name');
      const cafInput    = document.getElementById('product-shortcut-caffeine');
      const volInput    = document.getElementById('product-shortcut-volume');
      const iconInput   = document.getElementById('product-shortcut-icon');

      const name = nameInput ? nameInput.value.trim() : '';
      const mg   = cafInput ? parseFloat(cafInput.value || '0') : 0;
      const vol  = volInput ? volInput.value.trim() : '';
      const icon = iconInput ? iconInput.value.trim() : '';

      if (!name || isNaN(mg) || mg <= 0) {
        alert('메뉴 이름과 카페인 양(mg)을 올바르게 입력해 주세요.');
        return;
      }

      userProductShortcuts.push({
        id: 'user_' + Date.now(),
        icon: icon || '⭐',
        label: name,
        caffeineMg: mg,
        volume: vol,
        defaultAmountNote: '1잔'
      });
      saveUserProductShortcuts();
      renderProductShortcuts();

      if (nameInput) nameInput.value = '';
      if (cafInput) cafInput.value = '';
      if (volInput) volInput.value = '';
      if (iconInput) iconInput.value = '';

      alert('자주 마시는 메뉴 아이콘이 추가되었습니다.');
      return;
    }
    // ✅ 자주 마시는 메뉴 아이콘 선택 시, 기록 폼 자동 채우기
    const pChip = e.target.closest && e.target.closest('.product-shortcut-chip');
    if (pChip) {
      const all = getAllProductShortcuts();
      const def = all.find(p => p.id === pChip.dataset.id);
      if (!def) return;

      const nameInput   = document.getElementById('product-name');
      const cafInput    = document.getElementById('caffeine-mg');
      const amountInput = document.getElementById('amount-note');
      const catSelect   = document.getElementById('category');
      const hint        = document.getElementById('product-shortcut-hint');

      if (nameInput)   nameInput.value   = def.label;
      if (cafInput)    cafInput.value    = def.caffeineMg;
      if (amountInput) amountInput.value = def.defaultAmountNote || '1잔';
      if (catSelect)   catSelect.value   = 'drink';

      if (hint) {
        hint.innerHTML =
          `선택한 아이콘을 <b>${def.label}</b> (${def.volume || ''}, 약 ${def.caffeineMg}mg)로 인식하여 ` +
          `<b>제품명 · 카페인 양 · 섭취량 메모</b>에 값을 채웠습니다. 필요하면 직접 수정해 주세요.`;
      }

      // 시각 입력이 비어 있으면 현재 시간으로
      const intakeTime = document.getElementById('intake-time');
      if (intakeTime && !intakeTime.value) {
        intakeTime.value = formatDateTimeLocal(new Date());
      }

      return;
    }


    if (e.target.id === 'load-intake-btn') {
      const sel = document.getElementById('edit-intake-select');
      if (!sel || !sel.value) {
        alert('수정할 기록이 없습니다.');
        return;
      }
      const id = sel.value;
      const intake = intakes.find(i => String(i.id) === id);
      if (!intake) {
        alert('선택한 기록을 찾을 수 없습니다.');
        return;
      }
      document.getElementById('product-name').value = intake.productName || '';
      document.getElementById('amount-note').value = intake.amountNote || '';
      document.getElementById('caffeine-mg').value = intake.caffeineMg;
      document.getElementById('intake-time').value = formatDateTimeLocal(new Date(intake.takenAt));
      document.getElementById('meal-timing').value = intake.mealTiming || 'AFTER';
      document.getElementById('category').value = intake.category || 'drink';
      currentEditId = intake.id;
      const submitBtn = document.getElementById('submit-intake-btn');
      if (submitBtn) submitBtn.textContent = '수정 내용 저장';
      const cupText = document.getElementById('today-cup-text');
      if (cupText) cupText.textContent = '선택한 기록을 수정한 뒤 “수정 내용 저장”을 누르면 반영됩니다.';
      return;
    }
    // ✅ 선택한 섭취 기록 삭제
    if (e.target.id === 'delete-intake-btn') {
      const sel = document.getElementById('edit-intake-select');
      if (!sel || !sel.value) {
        alert('삭제할 기록이 없습니다.');
        return;
      }

      const id = sel.value;
      const idx = intakes.findIndex(i => String(i.id) === id);

      if (idx === -1) {
        alert('선택한 기록을 찾을 수 없습니다.');
        return;
      }

      if (!confirm('정말 이 기록을 삭제할까요? 삭제 후에는 되돌릴 수 없습니다.')) {
        return;
      }

      const deleted = intakes.splice(idx, 1)[0];

      // 만약 방금 삭제한 것이 현재 수정 중이던 기록이면, 수정 상태 초기화
      if (currentEditId !== null && String(currentEditId) === String(deleted.id)) {
        currentEditId = null;
        const submitBtn = document.getElementById('submit-intake-btn');
        if (submitBtn) submitBtn.textContent = '기록 저장';
        const form = document.getElementById('intake-form');
        if (form) form.reset();
        const intakeTime = document.getElementById('intake-time');
        if (intakeTime) intakeTime.value = formatDateTimeLocal(new Date());
      }

      // 저장 + 화면 갱신
      saveData();
      updateTodaySummary();
      updateStats();
      updateCaffeineGraph();
      updateEditSelect();   // 드롭다운 목록 갱신
      renderStatsDetail();  // 세부 그래프도 사용 중이면 갱신
      renderBloodDetail();  // 혈중 농도 세부 그래프 갱신

      alert('선택한 섭취 기록이 삭제되었습니다.');
      return;
    }

    if (e.target.closest && e.target.closest('.drag-hint')) {
      showExtraCombined();
      return;
    }

    const chip = e.target.closest && e.target.closest('.effect-chip');
    if (chip) {
      document.querySelectorAll('.effect-chip').forEach(c=>c.classList.remove('active'));
      chip.classList.add('active');
      const def = EFFECT_DEFS.find(d=>d.id===chip.dataset.id);
      const tipsDiv = document.getElementById('effect-tips');
      if (def && tipsDiv) {
        tipsDiv.style.display = 'block';
        tipsDiv.textContent = def.tip + ' (심하거나 반복되면 반드시 보호자·전문가에게 알려야 합니다.)';
      }
      return;
    }

    // 지식인 기반 popular_products.json 로드 버튼
    if (e.target.id === 'naver-fetch-btn') {
      const input = document.getElementById('naver-keyword-input');
      const hint = document.getElementById('naver-fetch-hint');
      const keyword = input ? input.value : '';

      loadPopularProducts(keyword)
        .then(list => {
          renderPopularProducts(list);
          if (hint) {
            hint.textContent =
              'popular_products.json(지식인 크롤링 결과)을 기준으로 정리한 목록입니다. ' +
              '파일이 없었거나 오류가 있으면 샘플 데이터를 사용했을 수 있습니다.';
          }
        })
        .catch(err => {
          console.error(err);
          renderPopularProducts(filterPopularProducts(keyword));
          if (hint) {
            hint.textContent = '데이터 불러오는 중 오류가 발생하여 샘플 데이터를 대신 표시합니다.';
          }
        });
      return;
    }
  });
    
// ===== 폼 제출 공통 처리 (카페인 섭취 기록 + 부작용 기록) =====

document.addEventListener('submit', function(e) {
  if (e.target.id === 'intake-form') {
    e.preventDefault();

    const caffeinePerUnit = parseFloat(
      document.getElementById('caffeine-mg').value || '0'
    );
    if (isNaN(caffeinePerUnit) || caffeinePerUnit <= 0) {
      alert('카페인 양을 올바르게 입력해주세요.');
      return;
    }

    const productName = document.getElementById('product-name').value.trim() || '미지정';
    const amountNoteRaw = document.getElementById('amount-note').value || '';
    const amountNote = amountNoteRaw.trim();

// ✅ [FIX] amount-note가 "용량(ml/g/oz/L)"이면 곱하지 않도록 count 계산을 안전하게 처리
function parseIntakeCountFromAmountNote(note) {
  const s = (note || '').trim().toLowerCase();
  if (!s) return 1;

  // (1) 용량/중량 표기면 "횟수"로 해석하지 않음
  // 예: 125ml, 355 ml, 0.5l, 60g, 24oz
  if (/(ml|mℓ|oz|l|g|그램)\b/.test(s)) return 1;

  // (2) 잔/컵은 "횟수"로 해석 (예: 2잔, 1.5컵)
  // (3) 단위 없는 숫자도 횟수로 해석 (예: 2, 1.5)
  const m = s.match(/(\d+(?:[.]\d+)?)/);
  if (!m) return 1;

  const v = parseFloat(m[1].replace(',', '.'));
  if (!Number.isFinite(v) || v <= 0) return 1;
  return v;
}

// ... 기존 코드 흐름 유지 ...
const count = parseIntakeCountFromAmountNote(amountNote);
const caffeineMg = caffeinePerUnit * count;

    const timeStr = document.getElementById('intake-time').value;
    if (!timeStr) {
      alert('섭취 시각을 입력해주세요.');
      return;
    }
    const mealTiming = document.getElementById('meal-timing').value;
    const category = document.getElementById('category').value;
    const takenAtIso = new Date(timeStr).toISOString();

    const submitBtn = document.getElementById('submit-intake-btn');
    const cupText  = document.getElementById('today-cup-text');
    const isEdit   = currentEditId !== null;

    if (!isEdit) {
      intakes.push({
        id: Date.now(),
        productName,
        amountNote,
        caffeineMg,
        takenAt: takenAtIso,
        mealTiming,
        category
      });
    } else {
      const idx = intakes.findIndex(i => i.id === currentEditId);
      if (idx !== -1) {
        intakes[idx].productName = productName;
        intakes[idx].amountNote  = amountNote;
        intakes[idx].caffeineMg  = caffeineMg;
        intakes[idx].takenAt     = takenAtIso;
        intakes[idx].mealTiming  = mealTiming;
        intakes[idx].category    = category;
      }
      currentEditId = null;
      if (submitBtn) submitBtn.textContent = '기록 저장';
      if (cupText) {
        cupText.textContent =
          '컵 이미지를 누르거나 아래 버튼을 누르면 섭취 기록 화면으로 이동합니다.';
      }
    }

    saveData();
    updateTodaySummary();
    updateStats();
    updateCaffeineGraph();
    updateEditSelect();
    renderStatsDetail();
    renderBloodDetail();
    e.target.reset();

    if (isEdit) {
      alert('선택한 기록이 수정되었습니다.');
    } else {
      alert('카페인 섭취 기록이 저장되었습니다.');
    }

    showHome();
    return;
  }
});

  // 📊 통계 메인 / 세부 차트
  let statsChart = null;
  let statsDetailCharts = {};

  // 기간별 라벨/데이터/텍스트 + 또래 평균(동일 나이) 계산
  function getStatsData(period) {
    const now = new Date();
    let labels = [];
    let data = [];
    let explain = '';
    let extra = '';

    if (period === 'day') {
      // 오늘: 시간대별
      labels = Array.from({ length: 24 }, (_, i) => `${i}시`);
      data = new Array(24).fill(0);
      intakes.forEach(i => {
        const d = new Date(i.takenAt);
        if (isSameDay(d, now)) data[d.getHours()] += i.caffeineMg;
      });
      explain = '오늘 시간대별 카페인 섭취량입니다.';
    } else if (period === 'week') {
      // 최근 7일: 일별
      const days = [];
      for (let i = 6; i >= 0; i--) {
        const d = new Date(now);
        d.setDate(now.getDate() - i);
        days.push(d);
      }
      labels = days.map(d => `${d.getMonth() + 1}/${d.getDate()}`);
      data = new Array(7).fill(0);
      intakes.forEach(i => {
        const d = new Date(i.takenAt);
        days.forEach((day, idx) => {
          if (isSameDay(d, day)) data[idx] += i.caffeineMg;
        });
      });
      explain = '최근 7일 동안의 일별 총 섭취량입니다.';
      const totalWeek = data.reduce((a, b) => a + b, 0);
      extra = ` / 하루 평균: <b>${(totalWeek / 7).toFixed(1)} mg</b>`;
    } else if (period === 'month') {
      // 이번 달: 날짜별
      const y = now.getFullYear();
      const m = now.getMonth();
      const lastDay = new Date(y, m + 1, 0).getDate();
      labels = Array.from({ length: lastDay }, (_, i) => `${m + 1}/${i + 1}`);
      data = new Array(lastDay).fill(0);
      intakes.forEach(i => {
        const d = new Date(i.takenAt);
        if (d.getFullYear() === y && d.getMonth() === m) {
          data[d.getDate() - 1] += i.caffeineMg;
        }
      });
      explain = '이번 달 동안의 날짜별 총 섭취량입니다.';
      const totalMonth = data.reduce((a, b) => a + b, 0);
      const daysInMonth = labels.length || 1;
      extra = ` / 하루 평균: <b>${(totalMonth / daysInMonth).toFixed(1)} mg</b>`;
    } else {
      // 올해: 월별
      labels = ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월'];
      data = new Array(12).fill(0);
      const y = now.getFullYear();
      intakes.forEach(i => {
        const d = new Date(i.takenAt);
        if (d.getFullYear() === y) data[d.getMonth()] += i.caffeineMg;
      });
      explain = '올해 월별 총 섭취량입니다.';
    }

    const total = data.reduce((a, b) => a + b, 0);
    const avg = data.length ? total / data.length : 0;
    const { ageData } = buildPeerDataPair(period, labels);  // 동일 나이 평균만 사용

    return { now, labels, data, explain, extra, total, avg, ageData };
  }

  // 또래(동일 나이) 평균 시계열 만들기
  function buildPeerDataPair(period, labels) {
    // 26명 데이터 (총 mg / 시간대)
    const peerRaw = [
      {mg:200, times:["16:00-18:00"]},
      {mg:200, times:["16:00-18:00"]},
      {mg:0,   times:[]},
      {mg:200, times:["20:00-22:00"]},
      {mg:200, times:["8:00-10:00","10:00-12:00","12:00-14:00","14:00-16:00","20:00-22:00","22:00-24:00"]},
      {mg:600, times:["12:00-14:00","22:00-24:00"]},
      {mg:200, times:["8:00-10:00","20:00-22:00"]},
      {mg:0,   times:["20:00-22:00","22:00-24:00"]},
      {mg:200, times:["14:00-16:00"]},
      {mg:0,   times:[]},
      {mg:1000, times:["12:00-14:00","20:00-22:00","22:00-24:00"]},
      {mg:200, times:["10:00-12:00","12:00-14:00","14:00-16:00"]},
      {mg:0,   times:[]},
      {mg:200, times:["14:00-16:00","16:00-18:00"]},
      {mg:200, times:["12:00-14:00"]},
      {mg:0,   times:["10:00-12:00"]},
      {mg:200, times:["20:00-22:00"]},
      {mg:0,   times:[]},
      {mg:200, times:["20:00-22:00","22:00-24:00"]},
      {mg:0,   times:[]},
      {mg:0,   times:[]},
      {mg:200, times:["12:00-14:00"]},
      {mg:200, times:["20:00-22:00"]},
      {mg:0,   times:[]},
      {mg:200, times:["18:00-20:00"]},
      {mg:1000, times:["8:00-10:00","12:00-14:00","16:00-18:00","20:00-22:00","22:00-24:00"]}
    ];

    // 시간대별 mg 평균 계산 (0~23시)
    const hourAvg = new Array(24).fill(0);
    const hourCnt = new Array(24).fill(0);

    peerRaw.forEach(p =>{
      p.times.forEach(t => {
        const [s,e] = t.split("-");
        const sh = parseInt(s.split(":")[0]);
        const eh = parseInt(e.split(":")[0]);
        const eachMg = p.mg / p.times.length; // 시간블록별 분배

        for (let h = sh; h < eh; h++){
          hourAvg[h] += eachMg;
          hourCnt[h] += 1;
        }
      });
    });

    for (let h=0; h<24; h++){
      if(hourCnt[h]>0) hourAvg[h] = hourAvg[h] / hourCnt[h];
    }

    // period별 라벨에 맞춰 평균 출력 (지금은 시간대 label에서만 사용)
    const ageData = labels.map(label=>{
      if(label.includes("시")){
        const h = parseInt(label.replace("시",""));
        return hourAvg[h] || 0;
      }
      return 0;
    });

    return { ageData };
  }

  // 📊 메인 통계 패널 업데이트
  function updateStats() {
    const select = document.getElementById('period-select');
    if (!select) return;

    const period = select.value;
    const {
      now,
      labels,
      data,
      explain,
      extra,
      total,
      avg,
      ageData
    } = getStatsData(period);

    const textDiv = document.getElementById('stats-text');
    if (textDiv) {
      textDiv.innerHTML =
        `총 섭취량: <b>${total.toFixed(0)} mg</b>, 평균: <b>${avg.toFixed(1)} mg</b>${extra}` +
        `<br>${explain}` +
        `<br>연한 녹색 막대는 <b>나의 섭취량</b>, 점선 회색 실선은 <b>동일 나이 평균</b>의 값입니다.`;
    }

    const canvas = document.getElementById('stats-chart');
    if (canvas) {
      const ctx = canvas.getContext('2d');
      if (!statsChart) {
        statsChart = new Chart(ctx, {
          type: 'bar',
          data: {
            labels,
            datasets: [
              {
                type: 'line',
                label: '동일 나이 평균',
                data: ageData,
                tension: 0.3,
                borderColor: 'rgba(156,163,175,0.95)',
                backgroundColor: 'rgba(156,163,175,0.03)',
                borderWidth: 2,
                borderDash: [2, 3],
                pointRadius: 0,
                order: 1
              },
              {
                type: 'bar',
                label: '내 섭취량 (mg)',
                data,
                backgroundColor: 'rgba(34,197,94,0.45)',
                borderColor: 'rgba(22,163,74,0.95)',
                borderWidth: 1,
                order: 2
              }
            ]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: { y: { beginAtZero: true } }
          }
        });
      } else {
        statsChart.data.labels = labels;
        statsChart.data.datasets[0].data = ageData;
        statsChart.data.datasets[1].data = data;
        statsChart.update();
      }

      // 월간 캘린더는 month일 때만 데이터 전달
      renderMonthCalendar(now, period === 'month' ? data : []);
    }
  }

  // 📊 통계 전체 화면(세부 모드)에서 4개 기간 그래프 렌더링
  function renderStatsDetail() {
    const wrapper = document.getElementById('stats-detail-wrapper');
    if (!wrapper || wrapper.style.display === 'none') return;

    const configs = [
      { period: 'day',   canvasId: 'stats-chart-day',   textId: 'stats-text-day' },
      { period: 'week',  canvasId: 'stats-chart-week',  textId: 'stats-text-week' },
      { period: 'month', canvasId: 'stats-chart-month', textId: 'stats-text-month' },
      { period: 'year',  canvasId: 'stats-chart-year',  textId: 'stats-text-year' }
    ];

    configs.forEach(cfg => {
      const canvas = document.getElementById(cfg.canvasId);
      const textDiv = document.getElementById(cfg.textId);
      if (!canvas || !textDiv) return;

      const {
        labels,
        data,
        explain,
        extra,
        total,
        avg,
        ageData
      } = getStatsData(cfg.period);

      textDiv.innerHTML =
        `총 섭취량: <b>${total.toFixed(0)} mg</b>, 평균: <b>${avg.toFixed(1)} mg</b>${extra}` +
        `<br>${explain}`;

      const ctx = canvas.getContext('2d');

      if (!statsDetailCharts[cfg.period]) {
        // 최초 생성
        statsDetailCharts[cfg.period] = new Chart(ctx, {
          type: 'bar',
          data: {
            labels,
            datasets: [
              {
                type: 'line',
                label: '동일 나이 평균',
                data: ageData,
                tension: 0.3,
                borderColor: 'rgba(156,163,175,0.95)',
                backgroundColor: 'rgba(156,163,175,0.03)',
                borderWidth: 2,
                borderDash: [6, 4],
                pointRadius: 0,
                order: 1
              },
              {
                type: 'bar',
                label: '내 섭취량 (mg)',
                data,
                backgroundColor: 'rgba(34,197,94,0.45)',
                borderColor: 'rgba(22,163,74,0.95)',
                borderWidth: 1,
                order: 2
              }
            ]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: { y: { beginAtZero: true } },
            plugins: {
              legend: { display: false } // 세부 화면에서는 범례 감추기
            }
          }
        });
      } else {
        // 이미 있는 차트 업데이트
        const chart = statsDetailCharts[cfg.period];
        chart.data.labels = labels;
        chart.data.datasets[0].data = ageData;
        chart.data.datasets[1].data = data;
        chart.update();
      }
    });
  }

  // 📊 월간 캘린더 + 날짜 클릭 시 하루 그래프 표시
  function renderMonthCalendar(now, dataForMonth) {
    const cal = document.getElementById('month-calendar');
    if (!cal) return;

    const y = now.getFullYear();
    const m = now.getMonth();
    const lastDay = new Date(y, m + 1, 0).getDate();
    const firstWeekday = new Date(y, m, 1).getDay();
    const weekdays = ['일','월','화','수','목','금','토'];

    // 월별 섭취 데이터 준비
    let data = dataForMonth;
    if (!Array.isArray(data) || data.length !== lastDay) {
      data = new Array(lastDay).fill(0);
      intakes.forEach(i => {
        const d = new Date(i.takenAt);
        if (d.getFullYear() === y && d.getMonth() === m) {
          data[d.getDate() - 1] += i.caffeineMg;
        }
      });
    }
    const maxVal = data.length ? Math.max(...data) : 0;

    // 캘린더 HTML 생성
    let html = '<div class="calendar-grid">';
    weekdays.forEach(w => {
      html += `<div class="calendar-day-header">${w}</div>`;
    });

    // 1일 시작 전 빈 칸
    for (let i = 0; i < firstWeekday; i++) {
      html += '<div class="calendar-day"></div>';
    }

    // 날짜 칸
    for (let day = 1; day <= lastDay; day++) {
      const idx = day - 1;
      const val = data[idx] || 0;

      let bg = '#e5f7ef';
      if (maxVal > 0 && val > 0) {
        const ratio = val / maxVal;
        const light = 90 - Math.round(35 * ratio); // 값이 클수록 더 진하게
        bg = `hsl(140,60%,${light}%)`;
      }
      const has = val > 0;

      // data-day + cursor:pointer 추가 (클릭 가능 표시)
      html += `<div class="calendar-day${has ? ' has-intake' : ''}"
                   data-day="${day}"
                   style="background:${bg}; cursor:pointer;">
                 ${day}
               </div>`;
    }

    html += '</div><div class="calendar-legend">숫자와 색이 진할수록 해당 날짜의 카페인 섭취량이 많습니다.</div>';
    cal.innerHTML = html;

    // 📅 날짜 클릭 시 해당 날짜의 하루 카페인 섭취 그래프 표시
    const dayCells = cal.querySelectorAll('.calendar-day[data-day]');
    dayCells.forEach(cell => {
      cell.addEventListener('click', () => {
        const day = parseInt(cell.getAttribute('data-day'), 10);
        renderDailyStatsForDate(y, m, day);
      });
    });
  }

  // 📊 선택한 날짜의 하루(0~23시) 카페인 섭취량 그래프
  function renderDailyStatsForDate(year, monthIndex, day) {
    const labels = Array.from({ length: 24 }, (_, i) => `${i}시`);
    const data   = new Array(24).fill(0);

    // 해당 날짜의 기록을 시간대별로 합산
    intakes.forEach(i => {
      const d = new Date(i.takenAt);
      if (
        d.getFullYear() === year &&
        d.getMonth() === monthIndex &&
        d.getDate() === day
      ) {
        data[d.getHours()] += i.caffeineMg;
      }
    });

    const total = data.reduce((a, b) => a + b, 0);
    const avg   = data.length ? total / data.length : 0;

    // 텍스트 영역 업데이트
    const textDiv = document.getElementById('stats-text');
    if (textDiv) {
      const mm = String(monthIndex + 1).padStart(2, '0');
      const dd = String(day).padStart(2, '0');
      textDiv.innerHTML =
        `선택한 날짜: <b>${year}-${mm}-${dd}</b>` +
        `<br>총 섭취량: <b>${total.toFixed(0)} mg</b>, 시간대 평균: <b>${avg.toFixed(1)} mg</b>` +
        `<br>막대를 통해 어느 시간대에 많이 섭취했는지 확인해 보세요.`;
    }

    const canvas = document.getElementById('stats-chart');
    if (!canvas) return;
    const ctx = canvas.getContext('2d');

    // 통계용 메인 차트 재사용 (없으면 새로 생성)
    if (!statsChart) {
      statsChart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels,
          datasets: [
            {
              label: '시간대별 섭취량 (mg)',
              data,
              backgroundColor: 'rgba(34,197,94,0.45)',
              borderColor: 'rgba(22,163,74,0.95)',
              borderWidth: 1
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: { y: { beginAtZero: true } }
        }
      });
      return;
    }

    // 기존 statsChart 데이터만 교체
    statsChart.data.labels = labels;
    const ds = statsChart.data.datasets;

    if (ds.length >= 2) {
      // 0: 동일 나이 평균, 1: 내 섭취량 막대
      ds[0].data = new Array(24).fill(null); // 라인 숨기기
      ds[1].label = '시간대별 섭취량 (mg)';
      ds[1].data  = data;
    } else if (ds.length >= 1) {
      ds[0].label = '시간대별 섭취량 (mg)';
      ds[0].data  = data;
    }

    statsChart.update();
  }

  // 🔽 아래 세 줄은 원래 있던 값 유지 (혈중 농도 그래프용)
  let caffeineChart = null;
  let caffeineWeekChart  = null;
  let caffeineMonthChart = null;

  function caffeineLevelAt(time) {
    let total = 0;
    intakes.forEach(i=>{
      const takenAt = new Date(i.takenAt);
      const diffHours = (time - takenAt)/(1000*60*60);
      if (diffHours >= 0) {
        total += i.caffeineMg * Math.pow(0.5, diffHours / HALF_LIFE_HOURS);
      }
    });
    return total;
  }
 function buildCaffeineSeries(rangeType) {
    const now = new Date();

    let start, end;
    const stepHours = 1; // 1시간 간격

    if (rangeType === 'week') {
      // 오늘 포함 최근 7일: (6일 전 0시) ~ (오늘 다음날 0시)
      const today0 = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 0, 0, 0);
      start = new Date(today0);
      start.setDate(today0.getDate() - 6);

      end = new Date(today0);
      end.setDate(today0.getDate() + 1); // 다음날 0시까지
    } else {
      // 이번 달 1일 0시 ~ 다음 달 1일 0시
      const y = now.getFullYear();
      const m = now.getMonth();
      start = new Date(y, m, 1, 0, 0, 0);
      end   = new Date(y, m + 1, 1, 0, 0, 0);
    }

    const labels = [];
    const data   = [];

    const t = new Date(start);
    while (t < end) {
      labels.push(
        `${t.getMonth() + 1}/${t.getDate()} ${String(t.getHours()).padStart(2, '0')}시`
      );
      data.push(caffeineLevelAt(t));
      t.setHours(t.getHours() + stepHours);
    }

    return { labels, data };
  }
  // 📈 혈중 카페인 세부 화면 (최근 7일 / 이번 달 추이)
  function renderBloodDetail() {
    const wrapper = document.getElementById('blood-detail-wrapper');
    if (!wrapper || wrapper.style.display === 'none') return;

    // ---------- 1) 최근 7일 ----------
    const weekCanvas = document.getElementById('caffeine-chart-week');
    const weekText   = document.getElementById('caffeine-text-week');

    if (weekCanvas && weekText) {
      const { labels, data } = buildCaffeineSeries('week');

      const total = data.reduce((a, b) => a + b, 0);
      const avg   = data.length ? total / data.length : 0;

      weekText.innerHTML =
        `최근 7일 동안 1시간 간격으로 계산한 <b>혈중 카페인 농도 추이</b>입니다.` +
        `<br>전체 구간 평균: <b>${avg.toFixed(1)}</b> (상대값 기준)`;

      const ctxW = weekCanvas.getContext('2d');
      if (!caffeineWeekChart) {
        caffeineWeekChart = new Chart(ctxW, {
          type: 'line',
          data: {
            labels,
            datasets: [{
              label: '혈중 카페인 농도 (상대값)',
              data,
              tension: 0.3,
              fill: false
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: { y: { beginAtZero: true } }
          }
        });
      } else {
        caffeineWeekChart.data.labels = labels;
        caffeineWeekChart.data.datasets[0].data = data;
        caffeineWeekChart.update();
      }
    }

    // ---------- 2) 이번 달 ----------
    const monthCanvas = document.getElementById('caffeine-chart-month');
    const monthText   = document.getElementById('caffeine-text-month');

    if (monthCanvas && monthText) {
      const { labels, data } = buildCaffeineSeries('month');

      const total = data.reduce((a, b) => a + b, 0);
      const avg   = data.length ? total / data.length : 0;

      monthText.innerHTML =
        `이번 달 1일 0시부터 현재까지 1시간 간격으로 계산한 <b>혈중 카페인 농도 추이</b>입니다.` +
        `<br>전체 구간 평균: <b>${avg.toFixed(1)}</b> (상대값 기준)`;

      const ctxM = monthCanvas.getContext('2d');
      if (!caffeineMonthChart) {
        caffeineMonthChart = new Chart(ctxM, {
          type: 'line',
          data: {
            labels,
            datasets: [{
              label: '혈중 카페인 농도 (상대값)',
              data,
              tension: 0.3,
              fill: false
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: { y: { beginAtZero: true } }
          }
        });
      } else {
        caffeineMonthChart.data.labels = labels;
        caffeineMonthChart.data.datasets[0].data = data;
        caffeineMonthChart.update();
      }
    }
  }

  function updateCaffeineGraph() {
    const canvas = document.getElementById('caffeine-chart');
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    const now = new Date();
    const start = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 0,0,0);

    const rangeSel = document.getElementById('caffeine-range');
    const range = rangeSel ? rangeSel.value : 'full';
    let startHour = 0;
    let endHour = 24;
    if (range === 'school') { startHour = 6; endHour = 18; }
    else if (range === 'evening') { startHour = 18; endHour = 24; }
    else if (range === 'morning') { startHour = 6; endHour = 12; }

    const labels = [];
    const data = [];
    for (let h=startHour; h<endHour; h++) {
      const t = new Date(start);
      t.setHours(h);
      labels.push(`${h}시`);
      data.push(caffeineLevelAt(t));
    }

    let maxDay = 0;
    for (let h=0; h<24; h++) {
      const t = new Date(start);
      t.setHours(h);
      maxDay = Math.max(maxDay, caffeineLevelAt(t));
    }
    if (maxDay < 1) maxDay = 1;

    if (!caffeineChart) {
      caffeineChart = new Chart(ctx,{
        type:'line',
        data:{ labels, datasets:[{ label:'추정 혈중 카페인 (상대값)', data, tension:0.3, fill:false }] },
        options:{ responsive:true, maintainAspectRatio:false, scales:{ y:{ beginAtZero:true } } }
      });
    } else {
      caffeineChart.data.labels = labels;
      caffeineChart.data.datasets[0].data = data;
      caffeineChart.update();
    }

    const sleepInput = document.getElementById('sleep-time');
    let sleepTime = new Date(start);
    if (sleepInput && sleepInput.value) {
      const [hh,mm] = sleepInput.value.split(':').map(Number);
      sleepTime.setHours(hh, mm || 0, 0, 0);
    } else {
      sleepTime.setHours(23,0,0,0);
    }
    const levelAtSleep = caffeineLevelAt(sleepTime);
    const ratio = (levelAtSleep / maxDay) * 100;

    const threshold = maxDay * 0.25;
    let recommendedTime = null;
    for (let mins = 0; mins <= 24*60; mins += 30) {
      const t = new Date(start.getTime() + mins*60000);
      const lvl = caffeineLevelAt(t);
      if (lvl <= threshold) {
        recommendedTime = t;
        break;
      }
    }

    const sleepInfo = document.getElementById('sleep-info');
    if (!sleepInfo) return;

    let msg = `선택한 취침 시각(${sleepTime.getHours()}시 기준)의 추정 잔여 카페인: <b>${levelAtSleep.toFixed(1)}</b> (오늘 최대치 대비 약 ${ratio.toFixed(0)}%)`;
    if (ratio > 60) {
      msg += ' — 이때 자면 <b>카페인 농도가 상당히 높은 상태</b>에서 자게 될 수 있어요.';
    } else if (ratio > 30) {
      msg += ' — 다소 높은 편이라, 잠이 얕아지거나 잠드는 데 시간이 걸릴 수 있습니다.';
    } else {
      msg += ' — 수면에 큰 영향을 줄 가능성은 상대적으로 낮은 편입니다. (개인차 존재)';
    }

    if (recommendedTime) {
      msg += `<br>카페인 농도가 상대적으로 안정되는 시점(최대치의 약 25% 이하로 떨어지는 시간)은 <b>${recommendedTime.getHours()}시 ${String(recommendedTime.getMinutes()).padStart(2,'0')}분</b> 전후입니다.`;
      msg += ' 그 부근에 잠자리에 드는 것이 더 편안한 수면에 도움이 될 수 있어요.';
    } else {
      msg += '<br>오늘 섭취량이 많아, 하루 동안 카페인 농도가 충분히 떨어지지 않을 수 있습니다.';
    }

    sleepInfo.innerHTML = msg;
  }

  function renderEffectIcons() {
    const container = document.getElementById('effect-icons');
    if (!container) return;
    container.innerHTML = EFFECT_DEFS.map(e =>
      `<button type="button" class="effect-chip" data-id="${e.id}" data-label="${e.label}">
        <span>${e.icon}</span><span>${e.label}</span>
      </button>`
    ).join('');
  }
 function getAllProductShortcuts() {
    return [...PRODUCT_SHORTCUT_DEFS, ...userProductShortcuts];
  }

  function renderProductShortcuts() {
    const container = document.getElementById('product-shortcut-icons');
    if (!container) return;

    const all = getAllProductShortcuts();
    if (!all.length) {
      container.innerHTML = '<span class="small">등록된 메뉴가 없습니다.</span>';
      return;
    }

    container.innerHTML = all.map(p => `
      <button type="button"
              class="product-shortcut-chip"
              data-id="${p.id}">
        <span>${p.icon || '☕'}</span>
        <span>${p.label}</span>
      </button>
    `).join('');
  }

  function renderSideEffectList() {
    const container = document.getElementById('side-effect-list');
    if (!container) return;
    if (!sideEffects.length) {
      container.textContent = '아직 기록이 없습니다.';
      return;
    }
    const items = sideEffects.slice().sort((a,b)=> new Date(b.occurredAt)-new Date(a.occurredAt)).slice(0,3);
    container.innerHTML = items.map(s=>{
      const d = new Date(s.occurredAt);
      return `<div class="effect-list-item">
        <span>${formatDateTimeView(d)}</span>
        <span>${s.effectLabel}${s.notes ? ' - ' + s.notes : ''}</span>
      </div>`;
    }).join('');
  renderRiskIndicator();
  }

  function renderPeerStories() {
    const storyBox = document.getElementById('peer-stories');
    const solutionBox = document.getElementById('peer-solutions');
    if (!storyBox || !solutionBox) return;

    // 왼쪽: 후기(상황)
    storyBox.innerHTML = PEER_STORIES.map(s =>
      `<div style="margin-bottom:6px;">
         ${s.icon} <b>${s.label}</b><br>
         ${s.story}
       </div>`
    ).join('');

    // 오른쪽: 해결 방법
    solutionBox.innerHTML = PEER_STORIES.map(s =>
      `<div style="margin-bottom:6px;">
         <b>${s.label}</b>일 때<br>
         ${s.solution}
       </div>`
    ).join('');
  }

function renderEffectDetailView(show) {
  const box  = document.getElementById('effects-detail-advanced');
  const body = document.getElementById('effects-detail-body');
  if (!box || !body) return;

  if (!show) {
    box.style.display = 'none';
    return;
  }
  box.style.display = 'block';

  if (!sideEffects.length) {
    body.textContent =
      '아직 저장된 부작용 기록이 없습니다. 증상 아이콘을 선택하고, 부작용 기록을 저장해 보세요.';
    return;
  }

  // 증상별 그룹화
  const grouped = {};
  sideEffects.forEach(s => {
    const key = s.effectId || 'etc';
    if (!grouped[key]) grouped[key] = [];
    grouped[key].push(s);
  });

  const cards = Object.keys(grouped).map(effectId => {
    const list = grouped[effectId].slice().sort(
      (a,b) => new Date(b.occurredAt) - new Date(a.occurredAt)
    );
    const def  = EFFECT_DEFS.find(d => d.id === effectId);
    const peer = PEER_STORIES.find(p => p.id === effectId);

    const label = def ? def.label : (list[0].effectLabel || '기타');
    const icon  = def ? def.icon : '❓';

    const itemsHtml = list.map(s => {
      const d = new Date(s.occurredAt);
      return `
        <div style="padding:4px 0; border-bottom:1px dashed #d1fae5;">
          <div style="font-weight:600;">${formatDateTimeView(d)}</div>
          <div>${s.notes ? s.notes : '(메모 없음)'}</div>
        </div>
      `;
    }).join('');

    let helperHtml = '';
    if (def) {
      helperHtml += `<b>[기본 대처 방법]</b><br>${def.tip}`;
    }
    if (peer) {
      helperHtml += `<br><br><b>[다른 학생 후기/해결 방법]</b><br>${peer.story}<br>${peer.solution}`;
    }
    if (!helperHtml) {
      helperHtml = '이 증상에 대한 기본 대처 방법과 후기는 아직 준비 중입니다.';
    }

    return `
      <div style="border-radius:10px; border:1px solid #a7f3d0; padding:8px; margin-top:8px; background:#ecfdf5;">
        <div style="font-weight:700; margin-bottom:4px; color:#065f46;">
          ${icon} ${label} (총 ${list.length}회)
        </div>
        <div style="margin-bottom:6px;">
          ${helperHtml}
        </div>
        <div style="max-height:160px; overflow:auto; background:#f0fdf4; border-radius:8px; padding:6px;">
          ${itemsHtml}
        </div>
      </div>
    `;
  });

  body.innerHTML = cards.join('');
}

// [B2] 부작용 이벤트/저장 로직 (이 블록 전체를 그대로 추가)

// 어떤 아이콘을 선택했는지 저장
let selectedEffectId = null;
let selectedEffectLabel = "";

// 부작용 아이콘 클릭 이벤트 바인딩
function bindEffectIconEvents() {
  const container = document.getElementById('effect-icons');
  const tipBox = document.getElementById('effect-tips');
  if (!container) return;

  container.addEventListener('click', (e) => {
    const btn = e.target.closest('.effect-chip');
    if (!btn) return;

    // 모든 아이콘 비활성화 → 클릭한 아이콘만 활성화
    document.querySelectorAll('.effect-chip').forEach(el => {
      el.classList.remove('active');
    });
    btn.classList.add('active');

    selectedEffectId = btn.dataset.id;
    selectedEffectLabel = btn.dataset.label;

    const def = EFFECT_DEFS.find(d => d.id === selectedEffectId);
    if (def && tipBox) {
      tipBox.style.display = 'block';
      tipBox.textContent = def.tip;
    }
  });
}

// 부작용 폼 제출(저장) 처리
function handleSideEffectSubmit(e) {
  e.preventDefault();

  if (!selectedEffectId) {
    alert('먼저 증상 아이콘을 하나 선택해 주세요.');
    return;
  }

  const notesEl = document.getElementById('side-effect-notes');
  const timeEl  = document.getElementById('side-effect-time');

  const notes = notesEl ? notesEl.value.trim() : '';
  // 시간이 비어 있으면 지금 시각으로
  const occurredAt = (timeEl && timeEl.value)
    ? timeEl.value
    : formatDateTimeLocal(new Date());

  const entry = {
    id: Date.now(),
    effectId: selectedEffectId,
    effectLabel: selectedEffectLabel,
    notes,
    occurredAt
  };

  sideEffects.push(entry);

  // 오른쪽 "내 부작용 기록" 업데이트
  renderSideEffectList();

  // 전체 화면 모드일 땐 상세 모아보기도 즉시 갱신
  if (extraDetailMode === 'effects') {
    renderEffectDetailView(true);
  } else {
    renderEffectDetailView(false);
  }

  // 폼 정리
  if (notesEl) notesEl.value = '';
  if (timeEl && !timeEl.value) {
    timeEl.value = occurredAt;
  }

  alert('부작용 기록이 저장되었습니다.');
}

// [B3] setExtraMode 보완 버전 (기존 함수 전체 교체)
function setExtraMode(mode) {
  extraDetailMode = mode; // null or 'stats'|'blood'|'effects'|'banner'

  const ids = {
    stats: 'extra-section-stats',
    blood: 'extra-section-blood',
    effects: 'extra-section-effects',
    banner: 'extra-section-banner'
  };

  const allSections = Object.values(ids).map(id => document.getElementById(id));
  const backBtn = document.getElementById('extra-back-btn');

  if (!mode) {
    // 통합 보기: 네 개 패널 모두 보이기
    allSections.forEach(sec => { if (sec) sec.style.display = 'block'; });
    if (backBtn) backBtn.style.display = 'none';

    // 통합 화면에서는 "부작용 상세 모아보기"는 접어두기
    renderEffectDetailView(false);
  } else {
    // 특정 모드만 전체 화면
    allSections.forEach(sec => { if (sec) sec.style.display = 'none'; });
    const target = document.getElementById(ids[mode]);
    if (target) target.style.display = 'block';
    if (backBtn) backBtn.style.display = 'inline-block';

    // 부작용 모드일 때만 '상세 모아보기' 열기
    if (mode === 'effects') {
      renderEffectDetailView(true);
    } else {
      renderEffectDetailView(false);
    }
  }
    // 📊 통계 세부 모드일 때만 기간별 세부 그래프 표시
    const statsDetail = document.getElementById('stats-detail-wrapper');
    if (statsDetail) {
      if (mode === 'stats') {
        statsDetail.style.display = 'block';
        renderStatsDetail();
      } else {
        statsDetail.style.display = 'none';
      }
    }

    // 📈 혈중 카페인 세부 모드일 때만 1주/1달 추이 그래프 표시
    const bloodDetail = document.getElementById('blood-detail-wrapper');
    if (bloodDetail) {
      if (mode === 'blood') {
        bloodDetail.style.display = 'block';
        renderBloodDetail();
      } else {
        bloodDetail.style.display = 'none';
      }
    }

    window.scrollTo({ top: 0, behavior: 'smooth' });
}

  function showHome() {
    document.getElementById('view-home').style.display = 'block';
    document.getElementById('view-intake').style.display = 'none';
    document.getElementById('view-extra').style.display = 'none';
    setExtraMode(null);
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }

  function goHome() {
    showHome();
  }

  function showExtraCombined() {
    document.getElementById('view-home').style.display = 'none';
    document.getElementById('view-intake').style.display = 'none';
    document.getElementById('view-extra').style.display = 'block';
    setExtraMode(null);
  }

  function openStatsDetail() {
    document.getElementById('view-home').style.display = 'none';
    document.getElementById('view-intake').style.display = 'none';
    document.getElementById('view-extra').style.display = 'block';
    setExtraMode('stats');
  }

  function openBloodDetail() {
    document.getElementById('view-home').style.display = 'none';
    document.getElementById('view-intake').style.display = 'none';
    document.getElementById('view-extra').style.display = 'block';
    setExtraMode('blood');
  }

// [B4] 부작용 전체 화면 진입 함수 (기존 함수 전체 교체)
function openEffectsDetail() {
  const home  = document.getElementById('view-home');
  const intake = document.getElementById('view-intake');
  const extra = document.getElementById('view-extra');

  if (home)   home.style.display = 'none';
  if (intake) intake.style.display = 'none';
  if (extra)  extra.style.display = 'block';

  // 부작용 패널만 전체 화면 + 상세 모아보기 ON
  setExtraMode('effects');

  renderEffectDetailView(true);
}

  function openBannerDetail() {
    document.getElementById('view-home').style.display = 'none';
    document.getElementById('view-intake').style.display = 'none';
    document.getElementById('view-extra').style.display = 'block';
    setExtraMode('banner');
  }

  function openIntake() {
    document.getElementById('view-home').style.display = 'none';
    document.getElementById('view-intake').style.display = 'block';
    document.getElementById('view-extra').style.display = 'none';
    setExtraMode(null);
    const form = document.getElementById('intake-form');
    if (form) {
      setTimeout(() => {
        window.scrollTo({
          top: form.getBoundingClientRect().top + window.scrollY - 60,
          behavior: 'smooth'
        });
      }, 50);
    }
  }

  document.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      goHome();
    }
  });

  // === 드래그/휠 제스처: 홈 ↔ 추가 기능 ===
  let dragStartY = null;
  let dragStartView = null;
  const DRAG_THRESHOLD = 120;

  function currentView() {
    const home = document.getElementById('view-home');
    const intake = document.getElementById('view-intake');
    const extra = document.getElementById('view-extra');
    if (intake && intake.style.display === 'block') return 'intake';
    if (extra && extra.style.display === 'block') return 'extra';
    if (home && home.style.display === 'block') return 'home';
    return 'home';
  }

  function handleTouchStart(e) {
    if (e.touches.length !== 1) return;
    dragStartY = e.touches[0].clientY;
    dragStartView = currentView();
  }
  function handleTouchMove(e) {
    if (dragStartY === null) return;
    const y = e.touches[0].clientY;
    const dy = y - dragStartY;

    if (dragStartView === 'home' && dy < -DRAG_THRESHOLD) {
      showExtraCombined();
      dragStartY = null;
      dragStartView = null;
    }
    if (dragStartView === 'extra' && dy > DRAG_THRESHOLD) {
      if (window.scrollY <= 10) {
        showHome();
        dragStartY = null;
        dragStartView = null;
      }
    }
  }
  function handleTouchEnd() {
    dragStartY = null;
    dragStartView = null;
  }

  document.addEventListener('touchstart', handleTouchStart, { passive: true });
  document.addEventListener('touchmove', handleTouchMove, { passive: true });
  document.addEventListener('touchend', handleTouchEnd, { passive: true });
  document.addEventListener('touchcancel', handleTouchEnd, { passive: true });

  let mouseDown = false;
  let mouseStartY = null;
  let mouseStartView = null;

  function handleMouseDown(e) {
    mouseDown = true;
    mouseStartY = e.clientY;
    mouseStartView = currentView();
  }
  function handleMouseMove(e) {
    if (!mouseDown || mouseStartY === null) return;
    const dy = e.clientY - mouseStartY;

    if (mouseStartView === 'home' && dy < -DRAG_THRESHOLD) {
      showExtraCombined();
      mouseDown = false;
      mouseStartY = null;
      mouseStartView = null;
    }
    if (mouseStartView === 'extra' && dy > DRAG_THRESHOLD) {
      if (window.scrollY <= 10) {
        showHome();
        mouseDown = false;
        mouseStartY = null;
        mouseStartView = null;
      }
    }
  }
  function handleMouseUp() {
    mouseDown = false;
    mouseStartY = null;
    mouseStartView = null;
  }

  document.addEventListener('mousedown', handleMouseDown);
  document.addEventListener('mousemove', handleMouseMove);
  document.addEventListener('mouseup', handleMouseUp);

  function handleWheel(e) {
    const view = currentView();
    const dy = e.deltaY;
    if (view === 'intake') return;

    if (view === 'home' && dy > 0) {
      const nearBottom =
        window.scrollY + window.innerHeight >= document.body.scrollHeight - 40;
      if (nearBottom) {
        showExtraCombined();
      }
      return;
    }

    if (view === 'extra' && dy < 0) {
      if (window.scrollY <= 10) {
        showHome();
      }
      return;
    }
  }

  document.addEventListener('wheel', handleWheel, { passive: true });

  function renderMonthCalendarInit() {
    const now = new Date();
    renderMonthCalendar(now, []);
  }

function init() {
  const todayLabel = document.getElementById('today-date-label');
  const now = new Date();
  if (todayLabel) {
    todayLabel.textContent = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}-${String(now.getDate()).padStart(2,'0')}`;
  }

  loadData();

  const intakeTime = document.getElementById('intake-time');
  if (intakeTime) intakeTime.value = formatDateTimeLocal(new Date());
  const seTime = document.getElementById('side-effect-time');
  if (seTime) seTime.value = formatDateTimeLocal(new Date());

  const sleepInput = document.getElementById('sleep-time');
  if (sleepInput) sleepInput.value = '23:00';

  // ✅ 부작용 아이콘/후기/리스트/상세 초기화
  renderEffectIcons();
  renderPeerStories();
  renderSideEffectList();
  renderEffectDetailView(false);   // 처음에는 상세 모아보기 접기
  renderProductShortcuts();

  // ✅ 부작용 폼 이벤트 연결
  const seForm = document.getElementById('side-effect-form');
  if (seForm) {
    seForm.addEventListener('submit', handleSideEffectSubmit);
  }
  bindEffectIconEvents();

  // (추가) 개인차 조절(증상별 슬라이더) 모달
  function initPersonalEffectModal(){
    const openBtn = document.getElementById('open-personal-modal');
    const modal = document.getElementById('effect-personal-modal');
    const closeBtn = document.getElementById('close-personal-modal');
    const body = document.getElementById('personal-sliders');
    const btnSave = document.getElementById('personal-save');
    const btnReset = document.getElementById('personal-reset');

    if (!openBtn || !modal || !body) return;

    function renderSliders(){
      body.innerHTML = '';
      EFFECT_DEFS.forEach(def => {
        const id = def.id;
        if (!id) return;
        // '기타'는 과도하게 일반적이라 제외(원하면 주석 해제)
        if (id === 'etc') return;

        const row = document.createElement('div');
        row.className = 'slider-row';

        const left = document.createElement('div');
        left.className = 'slider-left';
        left.innerHTML = `
          <div class="slider-name">${def.icon || ''} ${def.label || id}</div>
          <div class="slider-desc">기본 1.0 · 현재 <b>${getPersonalMult(id).toFixed(1)}</b></div>
        `;

        const right = document.createElement('div');
        right.className = 'slider-right';

        const range = document.createElement('input');
        range.type = 'range';
        range.min = '0.5';
        range.max = '2.0';
        range.step = '0.1';
        range.value = String(getPersonalMult(id));

        const val = document.createElement('div');
        val.className = 'slider-val';
        val.textContent = Number(range.value).toFixed(1);

        range.addEventListener('input', () => {
          val.textContent = Number(range.value).toFixed(1);
          // 왼쪽 설명도 즉시 반영
          const desc = left.querySelector('.slider-desc');
          if (desc) desc.innerHTML = `기본 1.0 · 현재 <b>${Number(range.value).toFixed(1)}</b>`;
        });

        range.addEventListener('change', () => {
          const v = clamp(Number(range.value), 0.5, 2.0);
          EFFECT_PERSONAL_MULT[id] = v;
          saveEffectPersonalMult(EFFECT_PERSONAL_MULT);
          renderRiskIndicator?.();
        });

        right.appendChild(range);
        right.appendChild(val);

        row.appendChild(left);
        row.appendChild(right);
        body.appendChild(row);
      });
    }

    function open(){
      renderSliders();
      modal.style.display = 'flex';
      document.body.style.overflow = 'hidden';
    }
    function close(){
      modal.style.display = 'none';
      document.body.style.overflow = '';
      // 입력 완료(타이핑 대기 해제) 느낌을 위해 포커스 제거
      openBtn.blur?.();
    }

    openBtn.addEventListener('click', open);
    closeBtn?.addEventListener('click', close);
    modal.addEventListener('mousedown', (e) => {
      if (e.target === modal) close();
    });

    btnReset?.addEventListener('click', () => {
      EFFECT_PERSONAL_MULT = {};
      saveEffectPersonalMult(EFFECT_PERSONAL_MULT);
      renderSliders();
      renderRiskIndicator?.();
    });

    btnSave?.addEventListener('click', () => {
      saveEffectPersonalMult(EFFECT_PERSONAL_MULT);
      renderRiskIndicator?.();
      close();
    });
  }
document.addEventListener('DOMContentLoaded', initPersonalEffectModal);
;

  // 기존 통계/그래프/달력 초기화
  updateTodaySummary();
  renderMonthCalendarInit();
  updateStats();
  updateCaffeineGraph();
  updateEditSelect();
  renderBloodDetail();

  // 초기에는 샘플로 테이블 채워두기
  renderPopularProducts(POPULAR_PRODUCTS_SAMPLE);

  showHome();
}

  init();

  // 플로팅 버튼/오버레이
  const fabButton = document.getElementById('fab-menu-button');
  const fabOverlay = document.getElementById('fab-overlay');

  if (fabButton && fabOverlay) {
    fabButton.addEventListener('click', () => {
      fabOverlay.style.display = 'flex';
    });

    fabOverlay.addEventListener('click', (e) => {
      if (e.target === fabOverlay) {
        fabOverlay.style.display = 'none';
      }
    });

    document.querySelectorAll('#fab-menu button').forEach(btn => {
      btn.addEventListener('click', () => {
        fabOverlay.style.display = 'none';
      });
    });
  }
</script>
<!-- 개인차 조절 모달 -->
<div id="effect-personal-modal" class="modal-backdrop" style="display:none;">
  <div class="modal-panel" role="dialog" aria-modal="true" aria-labelledby="personal-modal-title">
    <div class="modal-head">
      <div>
        <div id="personal-modal-title" class="modal-title">개인차 조절</div>
        <div class="modal-sub">각 증상의 민감도를 0.5(덜 민감) ~ 2.0(더 민감) 범위에서 조절하세요.</div>
      </div>
      <button type="button" id="close-personal-modal" class="modal-close" aria-label="닫기">✕</button>
    </div>

    <div id="personal-sliders" class="modal-body"></div>

    <div class="modal-actions">
      <button type="button" id="personal-reset" class="btn-soft">초기화</button>
      <button type="button" id="personal-save" class="btn-primary">저장</button>
    </div>
  </div>
</div>
</body>
</html>
