# financial-bmw-v7
<!doctype html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>파이낸셜 | BMW 운용리스 견적 v7</title>
  <meta name="theme-color" content="#111111" />
  <style>
    :root{
      --bg:#f6f6f6; --card:#ffffff; --text:#111; --muted:#666; --line:#e6e6e6;
      --radius:16px;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;
      background:var(--bg); color:var(--text);}
    .wrap{max-width:980px;margin:0 auto;padding:16px 14px 40px}
    .badges{display:flex;gap:8px;flex-wrap:wrap;margin:10px 0 12px}
    .badge{padding:6px 10px;border-radius:999px;font-size:12px}
    .badge.dark{background:#111;color:#fff}
    .badge.outline{border:1px solid #ddd;background:#fff;color:#111}
    h1{margin:0;font-size:22px;letter-spacing:-.02em}
    .sub{margin:6px 0 14px;color:var(--muted);font-size:13px;line-height:1.35}
    .grid{display:grid;gap:12px}
    @media(min-width:900px){.grid.cols-2{grid-template-columns:1fr 1fr}}
    @media(min-width:900px){.grid.cols-3{grid-template-columns:2fr 1fr}}
    .card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:14px}
    .card h2{margin:0 0 10px;font-size:15px}
    .row{display:flex;justify-content:space-between;gap:12px;margin:8px 0}
    .row .l{color:var(--muted);font-size:13px}
    .row .r{font-size:13px}
    .row .r strong{font-size:13px}
    .hr{height:1px;background:var(--line);margin:10px 0}
    label{display:block;font-size:12px;font-weight:700;margin-bottom:6px}
    .hint{font-weight:400;color:var(--muted);margin-left:6px}
    input,select,button,textarea{width:100%;font-size:14px}
    input,select{padding:10px 12px;border-radius:14px;border:1px solid var(--line);background:#fff}
    input[disabled]{background:#f0f0f0}
    .btn{border:0;border-radius:14px;padding:12px 12px;font-weight:700;cursor:pointer}
    .btn.primary{background:#111;color:#fff}
    .btn.outline{background:#fff;border:1px solid #ddd}
    .btnrow{display:flex;gap:8px}
    .btnrow > *{flex:1}
    .small{font-size:12px;color:var(--muted);line-height:1.35}
    .tabs{display:flex;gap:8px;margin:14px 0 12px}
    .tab{flex:1;padding:10px;border-radius:14px;border:1px solid #ddd;background:#fff;font-weight:700}
    .tab.active{background:#111;color:#fff;border-color:#111}
    .hide{display:none}
    textarea{min-height:240px;resize:vertical;padding:12px;border-radius:14px;border:1px solid var(--line)}
    .pillgroup{display:flex;flex-wrap:wrap;gap:8px}
    .pill{padding:10px 12px;border-radius:999px;border:1px solid #ddd;background:#fff;font-weight:700;cursor:pointer}
    .pill.active{background:#111;color:#fff;border-color:#111}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="badges">
      <span class="badge dark">파이낸셜</span>
      <span class="badge outline">운용리스</span>
      <span class="badge outline">v7</span>
      <span class="badge outline">웹페이지</span>
    </div>
    <h1>BMW 운용리스 견적·비용처리 계산기</h1>
    <div class="sub">
      월 납입료는 <b>VAT 없음(숫자만 입력)</b> · 차량가격-할인=최종구입가격 · 기타비용 합산 · 법인/개인 절세 동시 비교
    </div>

    <div class="tabs">
      <button class="tab active" data-tab="quote">견적서</button>
      <button class="tab" data-tab="input">입력</button>
      <button class="tab" data-tab="tax">절세</button>
    </div>

    <!-- ===== 견적서 탭 ===== -->
    <section id="tab-quote">
      <div class="grid cols-3">
        <div class="card">
          <h2>견적서 1페이지(요약)</h2>

          <div class="card" style="margin-top:12px">
            <h2>차량 정보</h2>
            <div class="row"><div class="l">모델</div><div class="r"><strong id="q-model"></strong></div></div>
          </div>

          <div class="card" style="margin-top:12px">
            <h2>가격 정보</h2>
            <div class="row"><div class="l">차량가격</div><div class="r" id="q-carPrice"></div></div>
            <div class="row"><div class="l">할인금액</div><div class="r" id="q-discount"></div></div>
            <div class="hr"></div>
            <div class="row"><div class="l">최종구입가격</div><div class="r"><strong id="q-final"></strong></div></div>
          </div>

          <div class="card" style="margin-top:12px">
            <h2>기타비용</h2>
            <div class="row"><div class="l">취득세</div><div class="r" id="q-acq"></div></div>
            <div class="row"><div class="l">공채구매비용</div><div class="r" id="q-bond"></div></div>
            <div class="row"><div class="l">탁송료</div><div class="r" id="q-delivery"></div></div>
            <div class="row"><div class="l">기타등록비용</div><div class="r" id="q-reg"></div></div>
            <div class="hr"></div>
            <div class="row"><div class="l">총 기타비용</div><div class="r"><strong id="q-etc"></strong></div></div>
          </div>

          <div class="card" style="margin-top:12px;background:#f3f3f3">
            <div class="row"><div class="l">총 구매비용</div><div class="r"><strong id="q-totalPurchase"></strong></div></div>
          </div>

          <div class="card" style="margin-top:12px">
            <h2>운용리스 조건</h2>
            <div class="row"><div class="l">계약기간</div><div class="r" id="q-term"></div></div>
            <div class="row"><div class="l">보증금</div><div class="r" id="q-deposit"></div></div>
            <div class="row"><div class="l">월 납입료</div><div class="r"><strong id="q-monthly"></strong></div></div>
          </div>

          <div style="margin-top:12px" class="btnrow">
            <button class="btn primary" id="btn-copy">1페이지 요약 복사</button>
            <button class="btn outline" id="btn-download">TXT 저장</button>
          </div>
          <div class="small" style="margin-top:10px">
            ※ 본 계산은 상담 편의용 시뮬레이션이며 실제 세무 처리는 업종/차량구분/업무사용비율 등에 따라 달라질 수 있습니다.
          </div>
        </div>

        <div class="card">
          <h2>빠른 설정</h2>

          <div class="row" style="align-items:center">
            <div class="l"><strong>프리셋 사용</strong><div class="small">켜면 주요 값이 잠김</div></div>
            <div class="r">
              <input type="checkbox" id="usePreset" style="width:auto;transform:scale(1.2)" checked />
            </div>
          </div>

          <label>프리셋 모델</label>
          <select id="presetSelect"></select>

          <div class="btnrow" style="margin-top:10px">
            <button class="btn primary" id="btn-applyPreset">프리셋 적용</button>
            <button class="btn outline" id="btn-direct">직접입력</button>
          </div>

          <div class="hr"></div>

          <label>할인금액(원) <span class="hint">옵션가 대신 할인</span></label>
          <input id="discount" inputmode="numeric" placeholder="0" />

          <label style="margin-top:10px">월 납입료(원) <span class="hint">VAT 없음 · 숫자만</span></label>
          <input id="monthlyPayment" inputmode="numeric" placeholder="0" />

          <div class="hr"></div>

          <label>법인세율(%)</label>
          <select id="corpRate"></select>

          <label style="margin-top:10px">소득세율(%) <span class="hint">개인사업자 체감세율</span></label>
          <select id="incomeRate"></select>
        </div>
      </div>
    </section>

    <!-- ===== 입력 탭 ===== -->
    <section id="tab-input" class="hide">
      <div class="grid cols-2">
        <div class="card">
          <h2>가격/기타비용 입력</h2>

          <label>모델</label>
          <input id="model" placeholder="예: BMW 520i" />

          <div class="grid cols-2" style="margin-top:10px">
            <div>
              <label>차량가격(원)</label>
              <input id="carPrice" inputmode="numeric" placeholder="0" />
            </div>
            <div>
              <label>할인금액(원)</label>
              <input id="discount2" inputmode="numeric" placeholder="0" />
            </div>
          </div>

          <div class="hr"></div>
          <div class="row"><div class="l">최종구입가격</div><div class="r"><strong id="i-final"></strong></div></div>

          <div class="hr"></div>
          <div class="grid cols-2">
            <div>
              <label>취득세(원)</label>
              <input id="acquisitionTax" inputmode="numeric" placeholder="0" />
            </div>
            <div>
              <label>공채구매비용(원)</label>
              <input id="bondCost" inputmode="numeric" placeholder="0" />
            </div>
            <div>
              <label>탁송료(원)</label>
              <input id="deliveryFee" inputmode="numeric" placeholder="0" />
            </div>
            <div>
              <label>기타등록비용(원)</label>
              <input id="otherRegFee" inputmode="numeric" placeholder="0" />
            </div>
          </div>

          <div class="hr"></div>
          <div class="row"><div class="l">총 기타비용</div><div class="r"><strong id="i-etc"></strong></div></div>
          <div class="row"><div class="l">총 구매비용</div><div class="r"><strong id="i-totalPurchase"></strong></div></div>
        </div>

        <div class="card">
          <h2>운용리스 조건</h2>

          <label>계약기간(개월)</label>
          <select id="termMonths">
            <option value="36">36</option>
            <option value="48">48</option>
            <option value="60">60</option>
          </select>

          <label style="margin-top:10px">보증금(%)</label>
          <input id="depositPct" inputmode="numeric" placeholder="0~100" />

          <label style="margin-top:10px">월 납입료(원) <span class="hint">VAT 없음</span></label>
          <input id="monthlyPayment2" inputmode="numeric" placeholder="0" />

          <div class="hr"></div>
          <div class="row"><div class="l">보증금 금액</div><div class="r"><strong id="i-depositAmt"></strong></div></div>

          <div class="hr"></div>
          <div class="small">
            · 월 납입료는 “공급가액(세금표기 없음)” 기준으로 입력합니다.<br/>
            · 프리셋 사용 시 주요 값이 잠깁니다.
          </div>
        </div>
      </div>
    </section>

    <!-- ===== 절세 탭 ===== -->
    <section id="tab-tax" class="hide">
      <div class="grid cols-2">
        <div class="card">
          <h2>비용처리/세율 입력</h2>

          <label>연간 기타연관비용(원) <span class="hint">보험/정비 등</span></label>
          <input id="annualOtherCost" inputmode="numeric" placeholder="0" />

          <label style="margin-top:10px">비용처리 인정 한도(원)</label>
          <input id="recognizedLimit" inputmode="numeric" placeholder="15000000" />

          <div class="hr"></div>
          <div class="row"><div class="l">연간 관련비용</div><div class="r"><strong id="t-annualRelated"></strong></div></div>
          <div class="row"><div class="l">인정금액</div><div class="r"><strong id="t-recognized"></strong></div></div>

          <div class="hr"></div>
          <label>법인세율(%)</label>
          <div class="pillgroup" id="corpPills"></div>

          <label style="margin-top:10px">소득세율(%) <span class="hint">개인 체감세율</span></label>
          <div class="pillgroup" id="incomePills"></div>
        </div>

        <div class="card">
          <h2>절세 비교 결과</h2>

          <div class="row"><div class="l">법인(연 절세)</div><div class="r"><strong id="t-corpSaving"></strong></div></div>
          <div class="row"><div class="l">법인(월 절세)</div><div class="r" id="t-corpMonthlySaving"></div></div>
          <div class="row"><div class="l">법인(월 체감비용)</div><div class="r"><strong id="t-corpEff"></strong></div></div>

          <div class="hr"></div>

          <div class="row"><div class="l">개인(연 절세)</div><div class="r"><strong id="t-incomeSaving"></strong></div></div>
          <div class="row"><div class="l">개인(월 절세)</div><div class="r" id="t-incomeMonthlySaving"></div></div>
          <div class="row"><div class="l">개인(월 체감비용)</div><div class="r"><strong id="t-incomeEff"></strong></div></div>

          <div class="hr"></div>
          <label>고객 1페이지 텍스트</label>
          <textarea id="summaryText" readonly></textarea>
        </div>
      </div>
    </section>
  </div>

<script>
  // ===== Data =====
  const PRESETS = [
    { model: "BMW 520i", carPrice: 74300000, termMonths: 60, depositPct: 0, monthlyPayment: 1128910 },
    { model: "BMW 530i", carPrice: 90000000, termMonths: 48, depositPct: 20, monthlyPayment: 1350000 },
    { model: "BMW X3 20d", carPrice: 85000000, termMonths: 48, depositPct: 20, monthlyPayment: 1400000 },
    { model: "BMW X5 30d", carPrice: 120000000, termMonths: 60, depositPct: 20, monthlyPayment: 2000000 },
  ];
  const CORP_TAX_RATES = [10, 20, 22, 25];
  const INCOME_TAX_RATES = [6, 15, 24, 35, 38, 40, 42, 45];

  // ===== Utils =====
  const toNumber = (v) => {
    const n = Number(String(v ?? "").replace(/,/g, ""));
    return Number.isFinite(n) ? n : 0;
  };
  const clampPct = (v) => Math.max(0, Math.min(100, Number.isFinite(v) ? v : 0));
  const won = (n) => `${Math.round(n).toLocaleString("ko-KR")}원`;
  const pct = (n) => `${Math.round(n)}%`;

  // ===== Compute (v7 rules) =====
  function compute(s){
    const carPrice = Math.max(0, toNumber(s.carPrice));
    const discount = Math.max(0, toNumber(s.discount));
    const finalPurchasePrice = Math.max(0, carPrice - discount);

    const depositPctVal = clampPct(toNumber(s.depositPct));
    const depositAmount = (finalPurchasePrice * depositPctVal) / 100;

    const etcTotal =
      Math.max(0, toNumber(s.acquisitionTax)) +
      Math.max(0, toNumber(s.bondCost)) +
      Math.max(0, toNumber(s.deliveryFee)) +
      Math.max(0, toNumber(s.otherRegFee));
    const totalPurchaseCost = finalPurchasePrice + etcTotal;

    const monthlyPayment = Math.max(0, toNumber(s.monthlyPayment)); // VAT 없음
    const annualLease = monthlyPayment * 12;
    const annualRelatedCost = annualLease + Math.max(0, toNumber(s.annualOtherCost));

    const recognizedLimit = Math.max(0, toNumber(s.recognizedLimit));
    const recognized = Math.min(annualRelatedCost, recognizedLimit);

    const corpRate = clampPct(toNumber(s.corpRate));
    const incomeRate = clampPct(toNumber(s.incomeRate));

    const corpSaving = (recognized * corpRate) / 100;
    const incomeSaving = (recognized * incomeRate) / 100;

    const corpMonthlySaving = corpSaving / 12;
    const incomeMonthlySaving = incomeSaving / 12;

    return {
      finalPurchasePrice, depositAmount, etcTotal, totalPurchaseCost,
      annualRelatedCost, recognized,
      corpSaving, incomeSaving,
      corpMonthlySaving, incomeMonthlySaving,
      corpMonthlyEffective: monthlyPayment - corpMonthlySaving,
      incomeMonthlyEffective: monthlyPayment - incomeMonthlySaving
    };
  }

  // ===== State (localStorage) =====
  const KEY = "financial_bmw_v7_state";
  const defaultState = {
    usePreset: true,
    presetIndex: 0,
    model: PRESETS[0].model,
    carPrice: PRESETS[0].carPrice,
    discount: 0,
    termMonths: PRESETS[0].termMonths,
    depositPct: PRESETS[0].depositPct,
    monthlyPayment: PRESETS[0].monthlyPayment,
    acquisitionTax: 0,
    bondCost: 0,
    deliveryFee: 0,
    otherRegFee: 0,
    annualOtherCost: 0,
    recognizedLimit: 15000000,
    corpRate: 22,
    incomeRate: 33
  };

  let state = (() => {
    try {
      const saved = JSON.parse(localStorage.getItem(KEY) || "null");
      return saved ? { ...defaultState, ...saved } : { ...defaultState };
    } catch {
      return { ...defaultState };
    }
  })();

  function save(){ localStorage.setItem(KEY, JSON.stringify(state)); }

  // ===== DOM =====
  const $ = (id) => document.getElementById(id);

  // Tabs
  document.querySelectorAll(".tab").forEach(btn => {
    btn.addEventListener("click", () => {
      document.querySelectorAll(".tab").forEach(b => b.classList.remove("active"));
      btn.classList.add("active");
      const tab = btn.dataset.tab;
      $("tab-quote").classList.toggle("hide", tab !== "quote");
      $("tab-input").classList.toggle("hide", tab !== "input");
      $("tab-tax").classList.toggle("hide", tab !== "tax");
    });
  });

  // Populate selects
  function initSelectors(){
    const presetSel = $("presetSelect");
    presetSel.innerHTML = PRESETS.map((p, i) => `<option value="${i}">${p.model}</option>`).join("");
    presetSel.value = String(state.presetIndex);

    const corpSel = $("corpRate");
    corpSel.innerHTML = CORP_TAX_RATES.map(r => `<option value="${r}">${r}%</option>`).join("");
    corpSel.value = String(state.corpRate);

    const incomeSel = $("incomeRate");
    incomeSel.innerHTML = INCOME_TAX_RATES.map(r => `<option value="${r}">${r}%</option>`).join("");
    incomeSel.value = String(state.incomeRate);
  }

  // Pills
  function renderPills(){
    const corpWrap = $("corpPills");
    corpWrap.innerHTML = "";
    CORP_TAX_RATES.forEach(r => {
      const b = document.createElement("button");
      b.className = "pill" + (Number(state.corpRate) === r ? " active" : "");
      b.textContent = r + "%";
      b.onclick = () => { state.corpRate = r; save(); syncAll(); };
      corpWrap.appendChild(b);
    });

    const incomeWrap = $("incomePills");
    incomeWrap.innerHTML = "";
    INCOME_TAX_RATES.forEach(r => {
      const b = document.createElement("button");
      b.className = "pill" + (Number(state.incomeRate) === r ? " active" : "");
      b.textContent = r + "%";
      b.onclick = () => { state.incomeRate = r; save(); syncAll(); };
      incomeWrap.appendChild(b);
    });
  }

  function applyPreset(index){
    const p = PRESETS[index];
    state.presetIndex = index;
    state.model = p.model;
    state.carPrice = p.carPrice;
    state.termMonths = p.termMonths;
    state.depositPct = p.depositPct;
    state.monthlyPayment = p.monthlyPayment;
  }

  function lockByPreset(){
    const locked = !!state.usePreset;
    $("model").disabled = locked;
    $("carPrice").disabled = locked;
    $("depositPct").disabled = locked;
    $("monthlyPayment").disabled = locked;
    $("monthlyPayment2").disabled = locked;
    $("monthlyPayment").disabled = locked;
    // quick card monthlyPayment input too
    $("monthlyPayment").disabled = locked;
  }

  // Build summary text
  function buildSummary(r){
    const lines = [];
    lines.push("BMW 운용리스 견적 요약(1페이지)");
    lines.push("----------------------------------------------");
    lines.push("[차량 정보]");
    lines.push("모델: " + state.model);
    lines.push("");
    lines.push("[가격 정보]");
    lines.push("차량가격: " + won(state.carPrice));
    lines.push("할인금액: " + won(state.discount));
    lines.push("최종구입가격: " + won(r.finalPurchasePrice));
    lines.push("");
    lines.push("[기타비용]");
    lines.push("취득세: " + won(state.acquisitionTax));
    lines.push("공채구매비용: " + won(state.bondCost));
    lines.push("탁송료: " + won(state.deliveryFee));
    lines.push("기타등록비용: " + won(state.otherRegFee));
    lines.push("총 기타비용: " + won(r.etcTotal));
    lines.push("");
    lines.push("총 구매비용: " + won(r.totalPurchaseCost));
    lines.push("");
    lines.push("[운용리스 조건]");
    lines.push("계약기간: " + state.termMonths + "개월");
    lines.push("보증금: " + pct(state.depositPct) + " / " + won(r.depositAmount));
    lines.push("월 납입료: " + won(state.monthlyPayment) + " (VAT 없음)");
    lines.push("");
    lines.push("[비용처리·절세(법인/개인 동시 비교)]");
    lines.push("연간 관련비용: " + won(r.annualRelatedCost) + " (월납입료×12 + 연간기타비용)");
    lines.push("비용처리 인정금액: " + won(r.recognized) + " (한도 " + won(state.recognizedLimit) + ")");
    lines.push("법인(" + pct(state.corpRate) + "): 연 절세 " + won(r.corpSaving) + " / 월 체감 " + won(r.corpMonthlyEffective));
    lines.push("개인(" + pct(state.incomeRate) + "): 연 절세 " + won(r.incomeSaving) + " / 월 체감 " + won(r.incomeMonthlyEffective));
    lines.push("");
    lines.push("※ 본 계산은 상담 편의용 시뮬레이션입니다.");
    return lines.join("\\n");
  }

  // Sync inputs -> state
  function bindInputs(){
    // Quote quick
    $("usePreset").checked = !!state.usePreset;
    $("presetSelect").value = String(state.presetIndex);
    $("discount").value = String(state.discount);
    $("monthlyPayment").value = String(state.monthlyPayment);
    $("corpRate").value = String(state.corpRate);
    $("incomeRate").value = String(state.incomeRate);

    // Input tab
    $("model").value = state.model;
    $("carPrice").value = String(state.carPrice);
    $("discount2").value = String(state.discount);
    $("termMonths").value = String(state.termMonths);
    $("depositPct").value = String(state.depositPct);
    $("monthlyPayment2").value = String(state.monthlyPayment);

    $("acquisitionTax").value = String(state.acquisitionTax);
    $("bondCost").value = String(state.bondCost);
    $("deliveryFee").value = String(state.deliveryFee);
    $("otherRegFee").value = String(state.otherRegFee);

    // Tax tab
    $("annualOtherCost").value = String(state.annualOtherCost);
    $("recognizedLimit").value = String(state.recognizedLimit);
  }

  // Render outputs
  function render(){
    const r = compute(state);

    // Quote view
    $("q-model").textContent = state.model;
    $("q-carPrice").textContent = won(state.carPrice);
    $("q-discount").textContent = won(state.discount);
    $("q-final").textContent = won(r.finalPurchasePrice);

    $("q-acq").textContent = won(state.acquisitionTax);
    $("q-bond").textContent = won(state.bondCost);
    $("q-delivery").textContent = won(state.deliveryFee);
    $("q-reg").textContent = won(state.otherRegFee);
    $("q-etc").textContent = won(r.etcTotal);

    $("q-totalPurchase").textContent = won(r.totalPurchaseCost);

    $("q-term").textContent = state.termMonths + "개월";
    $("q-deposit").textContent = pct(state.depositPct) + " / " + won(r.depositAmount);
    $("q-monthly").textContent = won(state.monthlyPayment) + " (VAT 없음)";

    // Input view
    $("i-final").textContent = won(r.finalPurchasePrice);
    $("i-etc").textContent = won(r.etcTotal);
    $("i-totalPurchase").textContent = won(r.totalPurchaseCost);
    $("i-depositAmt").textContent = won(r.depositAmount);

    // Tax view
    $("t-annualRelated").textContent = won(r.annualRelatedCost);
    $("t-recognized").textContent = won(r.recognized);

    $("t-corpSaving").textContent = won(r.corpSaving);
    $("t-corpMonthlySaving").textContent = won(r.corpMonthlySaving);
    $("t-corpEff").textContent = won(r.corpMonthlyEffective);

    $("t-incomeSaving").textContent = won(r.incomeSaving);
    $("t-incomeMonthlySaving").textContent = won(r.incomeMonthlySaving);
    $("t-incomeEff").textContent = won(r.incomeMonthlyEffective);

    $("summaryText").value = buildSummary(r);
  }

  function syncAll(){
    lockByPreset();
    initSelectors();
    renderPills();
    bindInputs();
    render();
  }

  // Event wiring
  function wire(){
    // preset usage
    $("usePreset").addEventListener("change", (e) => {
      state.usePreset = e.target.checked;
      save(); syncAll();
    });
    $("presetSelect").addEventListener("change", (e) => {
      state.presetIndex = toNumber(e.target.value);
      save(); syncAll();
    });
    $("btn-applyPreset").addEventListener("click", () => {
      applyPreset(state.presetIndex);
      save(); syncAll();
    });
    $("btn-direct").addEventListener("click", () => {
      state.usePreset = false;
      save(); syncAll();
    });

    // quick inputs
    $("discount").addEventListener("input", (e) => { state.discount = toNumber(e.target.value); $("discount2").value = String(state.discount); save(); render(); });
    $("monthlyPayment").addEventListener("input", (e) => { state.monthlyPayment = toNumber(e.target.value); $("monthlyPayment2").value = String(state.monthlyPayment); save(); render(); });
    $("corpRate").addEventListener("change", (e) => { state.corpRate = toNumber(e.target.value); save(); syncAll(); });
    $("incomeRate").addEventListener("change", (e) => { state.incomeRate = toNumber(e.target.value); save(); syncAll(); });

    // input tab
    $("model").addEventListener("input", (e) => { state.model = e.target.value; save(); render(); });
    $("carPrice").addEventListener("input", (e) => { state.carPrice = toNumber(e.target.value); save(); render(); });
    $("discount2").addEventListener("input", (e) => { state.discount = toNumber(e.target.value); $("discount").value = String(state.discount); save(); render(); });

    $("termMonths").addEventListener("change", (e) => { state.termMonths = toNumber(e.target.value); save(); render(); });
    $("depositPct").addEventListener("input", (e) => { state.depositPct = toNumber(e.target.value); save(); render(); });
    $("monthlyPayment2").addEventListener("input", (e) => { state.monthlyPayment = toNumber(e.target.value); $("monthlyPayment").value = String(state.monthlyPayment); save(); render(); });

    $("acquisitionTax").addEventListener("input", (e) => { state.acquisitionTax = toNumber(e.target.value); save(); render(); });
    $("bondCost").addEventListener("input", (e) => { state.bondCost = toNumber(e.target.value); save(); render(); });
    $("deliveryFee").addEventListener("input", (e) => { state.deliveryFee = toNumber(e.target.value); save(); render(); });
    $("otherRegFee").addEventListener("input", (e) => { state.otherRegFee = toNumber(e.target.value); save(); render(); });

    // tax tab
    $("annualOtherCost").addEventListener("input", (e) => { state.annualOtherCost = toNumber(e.target.value); save(); render(); });
    $("recognizedLimit").addEventListener("input", (e) => { state.recognizedLimit = toNumber(e.target.value); save(); render(); });

    // copy / download
    $("btn-copy").addEventListener("click", async () => {
      const text = $("summaryText").value;
      try {
        await navigator.clipboard.writeText(text);
        alert("복사 완료! (클립보드)");
      } catch {
        // iOS Safari에서 권한 문제 있을 수 있음
        $("summaryText").focus();
        $("summaryText").select();
        alert("복사가 막혀있어요. 텍스트가 선택됐으니 수동 복사해주세요.");
      }
    });

    $("btn-download").addEventListener("click", () => {
      const text = $("summaryText").value;
      const blob = new Blob([text], { type: "text/plain;charset=utf-8" });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = `BMW_운용리스_요약_${state.model}.txt`;
      a.click();
      URL.revokeObjectURL(url);
    });
  }

  // init
  initSelectors();
  wire();
  syncAll();
</script>
</body>
</html>
