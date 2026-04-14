# nwm-tracker
NWM Transformation Tracker
[influence_digital_project_tracker.html](https://github.com/user-attachments/files/26720387/influence_digital_project_tracker.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Influence Digital Project Tracker — Amgueddfa Cymru</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fontsource/ibm-plex-sans@5/index.css"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --red:    #DA1E28;
    --red-lt: #FFF1F1;
    --red-dk: #A2191F;
    --green:  #198038;
    --green-lt: #DEFBE6;
    --blue:   #0043CE;
    --blue-lt: #EDF5FF;
    --blue-md: #4589FF;
    --black:  #161616;
    --grey1:  #393939;
    --grey2:  #6F6F6F;
    --grey3:  #E0E0E0;
    --grey4:  #F4F4F4;
    --white:  #FFFFFF;
    --amber:  #F1C21B;
    --amber-lt: #FFF8E1;
    --font: 'IBM Plex Sans', 'Arial', sans-serif;
    --radius: 4px;
  }

  body {
    font-family: var(--font);
    background: var(--white);
    color: var(--black);
    font-size: 13px;
    line-height: 1.5;
  }

  /* ── HEADER ── */
  .header {
    background: var(--black);
    color: var(--white);
    padding: 0;
    display: flex;
    align-items: stretch;
    border-bottom: 3px solid var(--red);
  }
  .header-brand {
    background: var(--red);
    padding: 14px 24px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    min-width: 220px;
  }
  .header-brand .logo-top {
    font-size: 11px;
    font-weight: 400;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.75);
  }
  .header-brand .logo-main {
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 0.01em;
    color: var(--white);
    line-height: 1.2;
  }
  .header-meta {
    padding: 14px 24px;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .header-client { display: flex; flex-direction: column; gap: 2px; }
  .header-client .label {
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--grey2);
  }
  .header-client .name {
    font-size: 18px;
    font-weight: 600;
    color: var(--white);
  }
  .header-client .sub {
    font-size: 12px;
    color: var(--grey2);
  }
  .header-right {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 4px;
  }
  .header-right .date-label {
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--grey2);
  }
  .header-right [contenteditable] {
    font-size: 13px;
    color: var(--white);
    background: transparent;
    border: none;
    outline: none;
    text-align: right;
    font-family: var(--font);
  }

  /* ── NAV TABS ── */
  .nav {
    background: var(--grey4);
    border-bottom: 1px solid var(--grey3);
    display: flex;
    overflow-x: auto;
    padding: 0 24px;
  }
  .nav-tab {
    padding: 10px 20px;
    font-size: 12px;
    font-weight: 500;
    color: var(--grey2);
    cursor: pointer;
    border-bottom: 3px solid transparent;
    white-space: nowrap;
    user-select: none;
    transition: color 0.15s;
  }
  .nav-tab:hover { color: var(--black); }
  .nav-tab.active {
    color: var(--black);
    border-bottom-color: var(--blue);
    font-weight: 600;
  }

  /* ── SECTION WRAPPER ── */
  .section { display: none; padding: 28px 24px 48px; }
  .section.active { display: block; }

  .section-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 2px solid var(--black);
  }
  .section-title { font-size: 18px; font-weight: 600; }
  .section-sub { font-size: 12px; color: var(--grey2); margin-top: 3px; }
  .section-badge {
    font-size: 10px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    padding: 4px 10px;
    border-radius: 2px;
    background: var(--blue);
    color: var(--white);
  }

  /* ── TABLES ── */
  table { width: 100%; border-collapse: collapse; font-size: 12px; }
  thead th {
    background: var(--black);
    color: var(--white);
    padding: 8px 12px;
    text-align: left;
    font-weight: 500;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    white-space: nowrap;
  }
  tbody tr { border-bottom: 1px solid var(--grey3); }
  tbody tr:hover { background: var(--grey4); }
  tbody td {
    padding: 8px 12px;
    vertical-align: middle;
    color: var(--black);
  }
  [contenteditable] {
    outline: none;
    min-width: 60px;
    cursor: text;
    display: inline-block;
    width: 100%;
  }
  [contenteditable]:focus {
    background: var(--blue-lt);
    border-radius: 2px;
    outline: 2px solid var(--blue);
    outline-offset: -1px;
  }
  [contenteditable]:empty::before {
    content: attr(placeholder);
    color: #AAAAAA;
    font-style: italic;
    pointer-events: none;
  }

  /* ── STATUS BADGES ── */
  .badge {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 2px;
    font-size: 10px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    cursor: pointer;
    user-select: none;
    white-space: nowrap;
  }
  .badge-complete  { background: var(--green-lt);  color: var(--green); }
  .badge-progress  { background: var(--blue-lt);   color: var(--blue);  }
  .badge-pending   { background: var(--grey4);     color: var(--grey2); }
  .badge-risk      { background: var(--red-lt);    color: var(--red);   }
  .badge-review    { background: var(--amber-lt);  color: #8A6800;     }

  /* ── PHASE TAGS ── */
  .phase-a { display:inline-block; padding:2px 7px; background:var(--red);   color:#fff; border-radius:2px; font-size:10px; font-weight:600; }
  .phase-b { display:inline-block; padding:2px 7px; background:#6929C4;      color:#fff; border-radius:2px; font-size:10px; font-weight:600; }
  .phase-c { display:inline-block; padding:2px 7px; background:var(--green); color:#fff; border-radius:2px; font-size:10px; font-weight:600; }
  .phase-d { display:inline-block; padding:2px 7px; background:var(--black); color:#fff; border-radius:2px; font-size:10px; font-weight:600; }

  /* ── PROGRESS BAR ── */
  .progress-wrap { background: var(--grey3); border-radius: 2px; height: 6px; width: 100%; min-width: 80px; }
  .progress-fill { height: 6px; border-radius: 2px; background: var(--blue); }

  /* ── SCORE CHIP ── */
  .score {
    width: 32px; height: 32px;
    border-radius: 50%;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 700;
    cursor: pointer;
  }
  .score-high  { background: var(--green-lt); color: var(--green); border: 2px solid var(--green); }
  .score-mid   { background: var(--amber-lt); color: #8A6800;     border: 2px solid var(--amber); }
  .score-low   { background: var(--red-lt);   color: var(--red);   border: 2px solid var(--red);  }

  /* ── CARDS ── */
  .card-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; margin-bottom: 24px; }
  .card {
    border: 1px solid var(--grey3);
    border-radius: var(--radius);
    overflow: hidden;
  }
  .card-header {
    padding: 10px 14px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
  }
  .card-body { padding: 12px 14px; }
  .card-row {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    padding: 6px 0;
    border-bottom: 1px solid var(--grey3);
    gap: 12px;
    font-size: 12px;
  }
  .card-row:last-child { border-bottom: none; }
  .card-row-label { color: var(--grey2); font-size: 11px; min-width: 100px; flex-shrink: 0; }
  .card-row-value [contenteditable] { text-align: right; font-size: 12px; }

  /* ── HORIZON TIERS ── */
  .horizon { margin-bottom: 28px; border-radius: var(--radius); overflow: hidden; border: 1px solid var(--grey3); }
  .horizon-header {
    padding: 12px 18px;
    display: flex;
    align-items: center;
    gap: 14px;
  }
  .horizon-number {
    width: 28px; height: 28px;
    border-radius: 50%;
    background: var(--white);
    display: flex; align-items: center; justify-content: center;
    font-size: 13px; font-weight: 700;
    flex-shrink: 0;
  }
  .horizon-title { font-size: 15px; font-weight: 600; }
  .horizon-sub   { font-size: 11px; opacity: 0.8; margin-top: 1px; }
  .horizon-body  { background: var(--white); padding: 0; }
  .horizon-row {
    display: grid;
    grid-template-columns: 28px 2fr 1.5fr 1fr 1fr 120px;
    gap: 0;
    border-bottom: 1px solid var(--grey3);
    align-items: center;
    font-size: 12px;
  }
  .horizon-row:last-child { border-bottom: none; }
  .horizon-row > * { padding: 9px 12px; }
  .horizon-row-num { color: var(--grey2); font-size: 11px; text-align: center; }
  .horizon-thead {
    display: grid;
    grid-template-columns: 28px 2fr 1.5fr 1fr 1fr 120px;
    background: var(--grey4);
    border-bottom: 1px solid var(--grey3);
    font-size: 10px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--grey2);
  }
  .horizon-thead > * { padding: 7px 12px; }

  /* ── INSIGHTS GRID ── */
  .insight-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; margin-bottom: 24px; }
  .stage-col { border: 1px solid var(--grey3); border-radius: var(--radius); overflow: hidden; }
  .stage-header {
    padding: 8px 12px;
    font-size: 11px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--white);
  }
  .stage-before { background: var(--red); }
  .stage-during { background: var(--blue); }
  .stage-after  { background: var(--green); }
  .stage-body { padding: 10px 12px; }
  .stage-channel { margin-bottom: 10px; }
  .stage-channel-name {
    font-size: 11px; font-weight: 600; color: var(--black);
    margin-bottom: 4px; display: flex; align-items: center; justify-content: space-between;
  }
  .stage-channel-finding {
    font-size: 11px; color: var(--grey1); line-height: 1.45;
  }

  /* ── METHODOLOGY BOX ── */
  .method-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 24px; }
  .method-box {
    border: 1px solid var(--grey3);
    border-radius: var(--radius);
    padding: 14px 16px;
    background: var(--grey4);
  }
  .method-box h4 { font-size: 12px; font-weight: 600; margin-bottom: 8px; border-bottom: 1px solid var(--grey3); padding-bottom: 6px; }
  .method-box ul { padding-left: 16px; }
  .method-box li { font-size: 11px; color: var(--grey1); margin-bottom: 4px; line-height: 1.4; }

  /* ── SUMMARY STATS ── */
  .stat-row { display: flex; gap: 12px; margin-bottom: 24px; }
  .stat-card {
    flex: 1;
    border-radius: var(--radius);
    padding: 14px 16px;
    border: 1px solid var(--grey3);
    text-align: center;
  }
  .stat-card .stat-value { font-size: 28px; font-weight: 700; line-height: 1; margin-bottom: 4px; }
  .stat-card .stat-label { font-size: 10px; text-transform: uppercase; letter-spacing: 0.08em; color: var(--grey2); }

  /* ── UTILITY ── */
  .subsection-title {
    font-size: 13px; font-weight: 600; margin: 24px 0 10px;
    padding-bottom: 6px; border-bottom: 1px solid var(--grey3);
    display: flex; align-items: center; gap: 8px;
  }
  .tag {
    font-size: 10px; padding: 2px 6px; border-radius: 2px;
    background: var(--blue-lt); color: var(--blue); font-weight: 600;
  }
  .add-row-btn {
    display: inline-flex; align-items: center; gap: 6px;
    margin-top: 10px; padding: 6px 12px;
    font-size: 11px; font-weight: 600;
    border: 1px dashed var(--grey3);
    border-radius: var(--radius);
    cursor: pointer; color: var(--grey2);
    background: transparent;
    font-family: var(--font);
    transition: all 0.15s;
  }
  .add-row-btn:hover { border-color: var(--blue); color: var(--blue); background: var(--blue-lt); }

  .divider { border: none; border-top: 1px solid var(--grey3); margin: 20px 0; }
  .footnote { font-size: 10px; color: var(--grey2); font-style: italic; margin-top: 8px; }

  @media print {
    .nav { display: none; }
    .section { display: block !important; page-break-after: always; }
    .add-row-btn { display: none; }
  }
</style>
</head>
<body>

<!-- ══════════════ HEADER ══════════════ -->
<header class="header">
  <div class="header-brand">
    <span class="logo-top">Influence Digital</span>
    <span class="logo-main">Project Tracker</span>
  </div>
  <div class="header-meta">
    <div class="header-client">
      <span class="label">Client</span>
      <span class="name">Amgueddfa Cymru</span>
      <span class="sub">Digital Experience Review · May – August 2025</span>
    </div>
    <div class="header-right">
      <span class="date-label">Last updated</span>
      <span contenteditable="true" placeholder="DD Month YYYY">05 May 2025</span>
      <span style="font-size:10px;color:var(--grey2);margin-top:4px;">Version <span contenteditable="true">1.0</span></span>
    </div>
  </div>
</header>

<!-- ══════════════ NAV ══════════════ -->
<nav class="nav">
  <div class="nav-tab active" onclick="switchTab(0)">01 · Milestones</div>
  <div class="nav-tab" onclick="switchTab(1)">02 · Status Panel</div>
  <div class="nav-tab" onclick="switchTab(2)">03 · Audit Insights</div>
  <div class="nav-tab" onclick="switchTab(3)">04 · Transformation Roadmap</div>
</nav>

<!-- ══════════════════════════════════════
     SECTION 1 — MILESTONES LOG
══════════════════════════════════════ -->
<section class="section active" id="s0">
  <div class="section-header">
    <div>
      <div class="section-title">Project Milestones Log</div>
      <div class="section-sub">Completed and in-progress deliverables across all four phases</div>
    </div>
    <span class="section-badge">Live Tracking</span>
  </div>

  <!-- Summary stats -->
  <div class="stat-row">
    <div class="stat-card" style="border-left:4px solid var(--green)">
      <div class="stat-value" style="color:var(--green)" id="count-complete">0</div>
      <div class="stat-label">Completed</div>
    </div>
    <div class="stat-card" style="border-left:4px solid var(--blue)">
      <div class="stat-value" style="color:var(--blue)" id="count-progress">0</div>
      <div class="stat-label">In Progress</div>
    </div>
    <div class="stat-card" style="border-left:4px solid var(--grey2)">
      <div class="stat-value" style="color:var(--grey2)" id="count-pending">0</div>
      <div class="stat-label">Pending</div>
    </div>
    <div class="stat-card" style="border-left:4px solid var(--red)">
      <div class="stat-value" style="color:var(--red)" id="count-risk">0</div>
      <div class="stat-label">At Risk</div>
    </div>
  </div>

  <table id="milestones-table">
    <thead>
      <tr>
        <th style="width:70px">Phase</th>
        <th>Milestone / Activity</th>
        <th style="width:90px">Owner</th>
        <th style="width:100px">Due Date</th>
        <th style="width:110px">Status</th>
        <th>Notes</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="phase-a">A</span></td>
        <td><span contenteditable="true">Project kick-off meeting</span></td>
        <td><span contenteditable="true" placeholder="Owner">All</span></td>
        <td><span contenteditable="true" placeholder="Date">5 May 2025</span></td>
        <td><span class="badge badge-complete" onclick="cycleStatus(this)">Complete</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Agenda agreed. Stakeholder list confirmed.</span></td>
      </tr>
      <tr>
        <td><span class="phase-a">A</span></td>
        <td><span contenteditable="true">Data intake — analytics, CRM, audience research</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">12 May 2025</span></td>
        <td><span class="badge badge-complete" onclick="cycleStatus(this)">Complete</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">GA4, social dashboards and CRM data received.</span></td>
      </tr>
      <tr>
        <td><span class="phase-a">A</span></td>
        <td><span contenteditable="true">Review of Marketing Framework, Business Plan &amp; DDaT strategy</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">16 May 2025</span></td>
        <td><span class="badge badge-progress" onclick="cycleStatus(this)">In Progress</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Documents received. Review underway.</span></td>
      </tr>
      <tr>
        <td><span class="phase-a">A</span></td>
        <td><span contenteditable="true">Internal stakeholder interviews — all teams &amp; functions</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID + AA</span></td>
        <td><span contenteditable="true" placeholder="Date">30 May 2025</span></td>
        <td><span class="badge badge-progress" onclick="cycleStatus(this)">In Progress</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">7 of 12 interviews complete. Scheduling W4–5.</span></td>
      </tr>
      <tr>
        <td><span class="phase-a">A</span></td>
        <td><span contenteditable="true">Staff digital skills survey distributed across all 7 sites</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">30 May 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Survey drafted. AC to circulate.</span></td>
      </tr>
      <tr>
        <td><span class="phase-b">B</span></td>
        <td><span contenteditable="true">On-site visitor intercepts — priority museum sites</span></td>
        <td><span contenteditable="true" placeholder="Owner">AA + ID</span></td>
        <td><span contenteditable="true" placeholder="Date">27 Jun 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Dates to be confirmed with AC operations team.</span></td>
      </tr>
      <tr>
        <td><span class="phase-b">B</span></td>
        <td><span contenteditable="true">Non-visitor focus groups — working Welsh families, young people</span></td>
        <td><span contenteditable="true" placeholder="Owner">AA</span></td>
        <td><span contenteditable="true" placeholder="Date">27 Jun 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Recruitment underway via AA panel.</span></td>
      </tr>
      <tr>
        <td><span class="phase-b">B</span></td>
        <td><span contenteditable="true">Site visits — all 7 museums (depth calibrated per site)</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">11 Jul 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes...">Schedule in progress. NSM requires hard hat access.</span></td>
      </tr>
      <tr>
        <td><span class="phase-b">B</span></td>
        <td><span contenteditable="true">Digital channel audit — website, social, email/CRM, on-site tech</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">11 Jul 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-b">B</span></td>
        <td><span contenteditable="true">Sector &amp; experience economy benchmarking (4 lenses)</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID + AA</span></td>
        <td><span contenteditable="true" placeholder="Date">18 Jul 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-c">C</span></td>
        <td><span contenteditable="true">Gap analysis &amp; Dimensions Framework synthesis</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID + RB</span></td>
        <td><span contenteditable="true" placeholder="Date">1 Aug 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-c">C</span></td>
        <td><span contenteditable="true">Three-horizon roadmap — Brilliant Basics / Build / Bold</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID + RB</span></td>
        <td><span contenteditable="true" placeholder="Date">8 Aug 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-c">C</span></td>
        <td><span contenteditable="true">Draft report issued to Amgueddfa Cymru</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID</span></td>
        <td><span contenteditable="true" placeholder="Date">15 Aug 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-d">D</span></td>
        <td><span contenteditable="true">Client review &amp; bilingual QA</span></td>
        <td><span contenteditable="true" placeholder="Owner">AC + ID</span></td>
        <td><span contenteditable="true" placeholder="Date">22 Aug 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
      <tr>
        <td><span class="phase-d">D</span></td>
        <td><span contenteditable="true">Final stakeholder presentation — Senior Executive team</span></td>
        <td><span contenteditable="true" placeholder="Owner">ID + RB</span></td>
        <td><span contenteditable="true" placeholder="Date">29 Aug 2025</span></td>
        <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
        <td><span contenteditable="true" placeholder="Add notes..."></span></td>
      </tr>
    </tbody>
  </table>
  <button class="add-row-btn" onclick="addMilestoneRow()">+ Add milestone</button>
  <p class="footnote">Click any status badge to cycle through: Complete → In Progress → Pending → At Risk → Review → Complete</p>
</section>

<!-- ══════════════════════════════════════
     SECTION 2 — STATUS PANEL
══════════════════════════════════════ -->
<section class="section" id="s1">
  <div class="section-header">
    <div>
      <div class="section-title">Audit Component Status Panel</div>
      <div class="section-sub">Real-time status across all digital audit workstreams</div>
    </div>
    <span class="section-badge">Workstream View</span>
  </div>

  <div class="card-grid">

    <!-- Website -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        Website &amp; Digital Presence
        <span class="badge badge-progress" onclick="cycleStatus(this)">In Progress</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">ID</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">UX, SEO, content architecture, accessibility</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:35%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">35% complete</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding...">Site functions as noticeboard. Conversion pathways unclear.</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-risk" onclick="cycleStatus(this)">At Risk</span>
        </div>
      </div>
    </div>

    <!-- Social Media -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        Social Media
        <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">ID</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">Instagram, Facebook, X, TikTok (dormant), YouTube</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:10%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">10% complete</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding...">TikTok account exists but inactive. No cross-platform strategy.</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-review" onclick="cycleStatus(this)">Review</span>
        </div>
      </div>
    </div>

    <!-- Email / CRM -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        Email / CRM
        <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">ID</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">List health, journey logic, segmentation, campaign performance</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:0%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">Not started</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding..."></span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
        </div>
      </div>
    </div>

    <!-- On-Site Digital -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        On-Site Digital Experience
        <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">ID + RB</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">Wayfinding, interactives, immersive tech across 7 sites</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:0%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">Not started</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding..."></span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
        </div>
      </div>
    </div>

    <!-- Content & Workflows -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        Content &amp; Workflows
        <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">ID</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">Production, governance, approval flows, channel distribution</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:0%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">Not started</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding..."></span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
        </div>
      </div>
    </div>

    <!-- Skills & Compliance -->
    <div class="card">
      <div class="card-header" style="background:var(--black);color:var(--white);">
        Skills, Compliance &amp; Technology
        <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
      </div>
      <div class="card-body">
        <div class="card-row">
          <span class="card-row-label">Lead</span>
          <span contenteditable="true" placeholder="Name">RB + ID</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Scope</span>
          <span contenteditable="true" placeholder="Scope detail">Capability gaps, GDPR, Welsh Language, accessibility, cyber</span>
        </div>
        <div class="card-row">
          <span class="card-row-label">Progress</span>
          <div style="flex:1">
            <div class="progress-wrap"><div class="progress-fill" style="width:0%"></div></div>
            <div style="font-size:10px;color:var(--grey2);margin-top:3px">Not started</div>
          </div>
        </div>
        <div class="card-row">
          <span class="card-row-label">Key finding</span>
          <span contenteditable="true" placeholder="Add finding..."></span>
        </div>
        <div class="card-row">
          <span class="card-row-label">RAG</span>
          <span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span>
        </div>
      </div>
    </div>

  </div>
  <p class="footnote">ID = Influence Digital · AA = Audience Agency · RB = Transformation Specialist · AC = Amgueddfa Cymru</p>
</section>

<!-- ══════════════════════════════════════
     SECTION 3 — AUDIT INSIGHTS
══════════════════════════════════════ -->
<section class="section" id="s2">
  <div class="section-header">
    <div>
      <div class="section-title">Audit Insights</div>
      <div class="section-sub">Methodology, synthesised data findings, and channel scoring mapped to Before / During / After</div>
    </div>
    <span class="section-badge">Analytical Layer</span>
  </div>

  <!-- Methodology -->
  <div class="subsection-title">Methodology <span class="tag">Dimensions Framework</span></div>
  <div class="method-grid">
    <div class="method-box">
      <h4>Research approach</h4>
      <ul>
        <li contenteditable="true">Structured stakeholder interviews — 1:1 and small group across all functions</li>
        <li contenteditable="true">Staff digital skills survey — all 7 sites</li>
        <li contenteditable="true">On-site visitor intercepts — peak and quieter periods</li>
        <li contenteditable="true">Non-visitor focus groups — working Welsh families, young people</li>
        <li contenteditable="true">Associate Content Producer (ACP) panel — youth voice</li>
        <li contenteditable="true">Sector benchmarking across 4 lenses</li>
      </ul>
    </div>
    <div class="method-box">
      <h4>Diagnostic dimensions (applied holistically)</h4>
      <ul>
        <li contenteditable="true"><strong>a. Audience focus</strong> — who we reach, relevance, engagement</li>
        <li contenteditable="true"><strong>b. Content</strong> — quality, governance, workflow, distribution</li>
        <li contenteditable="true"><strong>c. Technology</strong> — infrastructure, platforms, integration</li>
        <li contenteditable="true"><strong>d. Data</strong> — analytics maturity, insight quality, GDPR</li>
        <li contenteditable="true"><strong>e. Skills &amp; leadership</strong> — capability, culture, change readiness</li>
      </ul>
    </div>
  </div>

  <!-- Synthesised Findings -->
  <div class="subsection-title">Synthesised data findings</div>
  <table>
    <thead>
      <tr>
        <th>Dimension</th>
        <th>Headline finding</th>
        <th>Evidence source</th>
        <th style="width:90px">Priority</th>
        <th style="width:90px">Score /10</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Audience focus</strong></td>
        <td><span contenteditable="true" placeholder="Finding...">Two-thirds of Wales not engaged. Current audience skews older, ABC1, Cardiff-centric.</span></td>
        <td><span contenteditable="true" placeholder="Source">Profiling data, stakeholder interviews</span></td>
        <td><span class="badge badge-risk">High</span></td>
        <td><span class="score score-low" contenteditable="true">3</span></td>
      </tr>
      <tr>
        <td><strong>Content</strong></td>
        <td><span contenteditable="true" placeholder="Finding...">Rich collections exist but no coherent content pipeline. Governance absent. Siloed production.</span></td>
        <td><span contenteditable="true" placeholder="Source">Stakeholder interviews, workflow review</span></td>
        <td><span class="badge badge-risk">High</span></td>
        <td><span class="score score-low" contenteditable="true">3</span></td>
      </tr>
      <tr>
        <td><strong>Technology</strong></td>
        <td><span contenteditable="true" placeholder="Finding...">Website functions as noticeboard. No integrated CRM journey. On-site digital piecemeal.</span></td>
        <td><span contenteditable="true" placeholder="Source">Website audit, interviews</span></td>
        <td><span class="badge badge-risk">High</span></td>
        <td><span class="score score-low" contenteditable="true">4</span></td>
      </tr>
      <tr>
        <td><strong>Data</strong></td>
        <td><span contenteditable="true" placeholder="Finding...">GA4 in place but inconsistently applied. No single source of truth. Limited insight culture.</span></td>
        <td><span contenteditable="true" placeholder="Source">Analytics review, interviews</span></td>
        <td><span class="badge badge-review">Medium</span></td>
        <td><span class="score score-mid" contenteditable="true">5</span></td>
      </tr>
      <tr>
        <td><strong>Skills &amp; leadership</strong></td>
        <td><span contenteditable="true" placeholder="Finding...">Digital understood as 'website only'. Significant skills gap. Fear of change noted across teams.</span></td>
        <td><span contenteditable="true" placeholder="Source">Survey, interviews</span></td>
        <td><span class="badge badge-risk">High</span></td>
        <td><span class="score score-low" contenteditable="true">3</span></td>
      </tr>
    </tbody>
  </table>

  <!-- Channel Scoring — Before / During / After -->
  <div class="subsection-title" style="margin-top:28px">Channel-by-channel scoring <span class="tag">Before / During / After</span></div>
  <p style="font-size:11px;color:var(--grey2);margin-bottom:14px">Scores out of 10. Click score to edit. Findings are editable per cell.</p>

  <div class="insight-grid">
    <div class="stage-col">
      <div class="stage-header stage-before">Before — Discovery &amp; Planning</div>
      <div class="stage-body">
        <div class="stage-channel">
          <div class="stage-channel-name">Search &amp; SEO <span class="score score-mid" contenteditable="true">5</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Organic presence limited. Individual museum sites poorly indexed. No unified SEO strategy.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Social media <span class="score score-low" contenteditable="true">3</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Inconsistent posting frequency. No audience-first content strategy. TikTok dormant.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Website (entry) <span class="score score-low" contenteditable="true">4</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Homepage does not inspire visit intent. No clear value proposition above the fold.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Email / CRM <span class="score score-mid" contenteditable="true">5</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Newsletter exists but not journey-mapped. No segmentation or pre-visit nurture flow.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Welsh language <span class="score score-mid" contenteditable="true">6</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Bilingual provision exists but inconsistently applied across platforms.</div>
        </div>
      </div>
    </div>

    <div class="stage-col">
      <div class="stage-header stage-during">During — On-Site Experience</div>
      <div class="stage-body">
        <div class="stage-channel">
          <div class="stage-channel-name">Wayfinding &amp; signage <span class="score score-mid" contenteditable="true">5</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Physical wayfinding present but digital extensions limited. No QR journey mapping.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Interactive tech <span class="score score-low" contenteditable="true">4</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Piecemeal adoption across sites. Exists without audience brief. Maintenance issues noted.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Content in space <span class="score score-mid" contenteditable="true">6</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Living museums (St Fagans, Big Pit) score well. City-centre sites more static.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">UGC / shareable moments <span class="score score-low" contenteditable="true">3</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Very few designed-for-sharing moments across sites. No selfie/UGC hooks.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Accessibility <span class="score score-mid" contenteditable="true">6</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Physical accessibility generally good. Digital WCAG compliance patchy across sites.</div>
        </div>
      </div>
    </div>

    <div class="stage-col">
      <div class="stage-header stage-after">After — Engagement &amp; Advocacy</div>
      <div class="stage-body">
        <div class="stage-channel">
          <div class="stage-channel-name">Post-visit email <span class="score score-low" contenteditable="true">2</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">No structured post-visit email journey exists. Most visitors not captured into CRM.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Social sharing <span class="score score-low" contenteditable="true">3</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">No mechanism to encourage post-visit sharing. NPS score of 84 not being leveraged.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Digital collections access <span class="score score-low" contenteditable="true">4</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">Collections online but not surfaced as post-visit discovery or continuing journey.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Website (return) <span class="score score-low" contenteditable="true">3</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">No returning audience journey. Site does not differentiate new vs returning visitors.</div>
        </div>
        <hr class="divider"/>
        <div class="stage-channel">
          <div class="stage-channel-name">Data capture <span class="score score-low" contenteditable="true">3</span></div>
          <div class="stage-channel-finding" contenteditable="true" placeholder="Finding...">GDPR-compliant but low consent rates. Minimal CRM growth from site visits.</div>
        </div>
      </div>
    </div>
  </div>
  <p class="footnote">Scores are indicative at this stage and will be refined following completion of Phase B audit activities.</p>
</section>

<!-- ══════════════════════════════════════
     SECTION 4 — TRANSFORMATION ROADMAP
══════════════════════════════════════ -->
<section class="section" id="s3">
  <div class="section-header">
    <div>
      <div class="section-title">Transformation Roadmap</div>
      <div class="section-sub">Three-horizon structure: Brilliant Basics · Build · Bold</div>
    </div>
    <span class="section-badge">Strategic Output</span>
  </div>

  <!-- HORIZON 1 -->
  <div class="horizon">
    <div class="horizon-header" style="background:var(--red);">
      <div class="horizon-number" style="color:var(--red);">1</div>
      <div>
        <div class="horizon-title" style="color:var(--white);">Brilliant Basics</div>
        <div class="horizon-sub" style="color:rgba(255,255,255,0.8);">Non-negotiable foundations · Months 1–6 post-delivery</div>
      </div>
    </div>
    <div class="horizon-thead">
      <div>#</div>
      <div>Recommendation</div>
      <div>Rationale</div>
      <div>Owner</div>
      <div>Effort</div>
      <div>Priority</div>
    </div>
    <div class="horizon-body">
      <div class="horizon-row">
        <div class="horizon-row-num">1</div>
        <div contenteditable="true">Establish a shared digital definition and language across the organisation</div>
        <div contenteditable="true" style="color:var(--grey1);">Staff understand 'digital' as website only. A shared framework unlocks everything else.</div>
        <div contenteditable="true" placeholder="Owner">AC Internal</div>
        <div contenteditable="true" placeholder="Effort">Low</div>
        <div><span class="badge badge-risk">Critical</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">2</div>
        <div contenteditable="true">Implement consistent GA4 tracking and analytics baseline across all sites</div>
        <div contenteditable="true" style="color:var(--grey1);">No single source of truth. Data-driven decisions impossible without a reliable baseline.</div>
        <div contenteditable="true" placeholder="Owner">ID + ICT</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-risk">Critical</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">3</div>
        <div contenteditable="true">Audit and remediate WCAG 2.1 AA accessibility compliance across all digital touchpoints</div>
        <div contenteditable="true" style="color:var(--grey1);">Legal obligation and audience inclusion imperative. Must precede further digital investment.</div>
        <div contenteditable="true" placeholder="Owner">ID + Digital</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-risk">Critical</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">4</div>
        <div contenteditable="true">Establish a content governance framework and clear production workflow</div>
        <div contenteditable="true" style="color:var(--grey1);">Content is lifeblood but not flowing. Process clarity enables all storytelling ambitions.</div>
        <div contenteditable="true" placeholder="Owner">Marketing + ID</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-review">High</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">5</div>
        <div contenteditable="true">Develop and roll out a digital skills training programme across all sites</div>
        <div contenteditable="true" style="color:var(--grey1);">Skills gap identified at every level. Capability must grow in parallel with any platform work.</div>
        <div contenteditable="true" placeholder="Owner">RB + HR</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-review">High</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">6</div>
        <div contenteditable="true" placeholder="Add recommendation..."></div>
        <div contenteditable="true" placeholder="Add rationale..."></div>
        <div contenteditable="true" placeholder="Owner"></div>
        <div contenteditable="true" placeholder="Effort"></div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></div>
      </div>
    </div>
  </div>

  <!-- HORIZON 2 -->
  <div class="horizon">
    <div class="horizon-header" style="background:var(--blue);">
      <div class="horizon-number" style="color:var(--blue);">2</div>
      <div>
        <div class="horizon-title" style="color:var(--white);">Build</div>
        <div class="horizon-sub" style="color:rgba(255,255,255,0.8);">Audience-led growth · Months 6–18 post-delivery</div>
      </div>
    </div>
    <div class="horizon-thead">
      <div>#</div>
      <div>Recommendation</div>
      <div>Rationale</div>
      <div>Owner</div>
      <div>Effort</div>
      <div>Priority</div>
    </div>
    <div class="horizon-body">
      <div class="horizon-row">
        <div class="horizon-row-num">1</div>
        <div contenteditable="true">Redesign website as audience-first experience — the eighth site</div>
        <div contenteditable="true" style="color:var(--grey1);">Current site is a noticeboard. Needs to function as a digital museum and conversion engine.</div>
        <div contenteditable="true" placeholder="Owner">ID + Digital</div>
        <div contenteditable="true" placeholder="Effort">High</div>
        <div><span class="badge badge-review">High</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">2</div>
        <div contenteditable="true">Build audience-segmented email journeys and CRM integration</div>
        <div contenteditable="true" style="color:var(--grey1);">Pre- and post-visit communications are the lowest-hanging fruit for re-engagement.</div>
        <div contenteditable="true" placeholder="Owner">Marketing + ID</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-review">High</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">3</div>
        <div contenteditable="true">Activate social channels with audience-led, platform-native content strategy</div>
        <div contenteditable="true" style="color:var(--grey1);">Audiences are on TikTok and Instagram. Presence without strategy is not enough.</div>
        <div contenteditable="true" placeholder="Owner">Marketing + ID</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-review">High</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">4</div>
        <div contenteditable="true">On-site digital experience uplift — shareable moments and UGC hooks at priority sites</div>
        <div contenteditable="true" style="color:var(--grey1);">NPS of 84 not being converted to advocacy. Designed moments create social reach at no media cost.</div>
        <div contenteditable="true" placeholder="Owner">ID + Visitor Exp</div>
        <div contenteditable="true" placeholder="Effort">Medium</div>
        <div><span class="badge badge-review">Medium</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">5</div>
        <div contenteditable="true" placeholder="Add recommendation..."></div>
        <div contenteditable="true" placeholder="Add rationale..."></div>
        <div contenteditable="true" placeholder="Owner"></div>
        <div contenteditable="true" placeholder="Effort"></div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></div>
      </div>
    </div>
  </div>

  <!-- HORIZON 3 -->
  <div class="horizon">
    <div class="horizon-header" style="background:var(--black);">
      <div class="horizon-number" style="color:var(--black);">3</div>
      <div>
        <div class="horizon-title" style="color:var(--white);">Bold</div>
        <div class="horizon-sub" style="color:rgba(255,255,255,0.6);">Ambitious &amp; future-facing · 18 months+ post-delivery</div>
      </div>
    </div>
    <div class="horizon-thead">
      <div>#</div>
      <div>Recommendation</div>
      <div>Rationale</div>
      <div>Owner</div>
      <div>Effort</div>
      <div>Priority</div>
    </div>
    <div class="horizon-body">
      <div class="horizon-row">
        <div class="horizon-row-num">1</div>
        <div contenteditable="true">AI-powered personalisation across website, email and on-site content layers</div>
        <div contenteditable="true" style="color:var(--grey1);">Once data foundations are in place, personalisation unlocks relevance at scale for all audience segments.</div>
        <div contenteditable="true" placeholder="Owner">ID + RB + Digital</div>
        <div contenteditable="true" placeholder="Effort">High</div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Future</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">2</div>
        <div contenteditable="true">Immersive on-site digital experiences — AI-enabled interactives and collections discovery</div>
        <div contenteditable="true" style="color:var(--grey1);">Technology now affordable. Art of the possible mapped per site. NSM as first mover pilot.</div>
        <div contenteditable="true" placeholder="Owner">ID + Sites</div>
        <div contenteditable="true" placeholder="Effort">High</div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Future</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">3</div>
        <div contenteditable="true">Predictive analytics and data-driven programme planning</div>
        <div contenteditable="true" style="color:var(--grey1);">Mature data estate enables forward-looking decisions on exhibitions, campaigns and investment priorities.</div>
        <div contenteditable="true" placeholder="Owner">RB + Digital</div>
        <div contenteditable="true" placeholder="Effort">High</div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Future</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">4</div>
        <div contenteditable="true">Sector-leading bilingual digital experience — Cymraeg-first design standard</div>
        <div contenteditable="true" style="color:var(--grey1);">Position AC as the global benchmark for bilingual digital museum experience. Unique in the world.</div>
        <div contenteditable="true" placeholder="Owner">AC + ID</div>
        <div contenteditable="true" placeholder="Effort">High</div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Future</span></div>
      </div>
      <div class="horizon-row">
        <div class="horizon-row-num">5</div>
        <div contenteditable="true" placeholder="Add recommendation..."></div>
        <div contenteditable="true" placeholder="Add rationale..."></div>
        <div contenteditable="true" placeholder="Owner"></div>
        <div contenteditable="true" placeholder="Effort"></div>
        <div><span class="badge badge-pending" onclick="cycleStatus(this)">Future</span></div>
      </div>
    </div>
  </div>

  <p class="footnote">Roadmap is indicative at this stage and will be refined, prioritised, and costed as part of Phase C synthesis. All recommendations subject to compliance review including Welsh Language Standards, GDPR, accessibility and cyber security.</p>
</section>

<script>
  const tabs = document.querySelectorAll('.nav-tab');
  const sections = document.querySelectorAll('.section');

  function switchTab(i) {
    tabs.forEach((t,j) => t.classList.toggle('active', j===i));
    sections.forEach((s,j) => s.classList.toggle('active', j===i));
    updateCounts();
  }

  const statusCycle = ['Complete','In Progress','Pending','At Risk','Review'];
  const statusClasses = {
    'Complete':'badge-complete',
    'In Progress':'badge-progress',
    'Pending':'badge-pending',
    'At Risk':'badge-risk',
    'Review':'badge-review'
  };

  function cycleStatus(el) {
    const cur = el.textContent.trim();
    const idx = statusCycle.indexOf(cur);
    const next = statusCycle[(idx + 1) % statusCycle.length];
    el.textContent = next;
    Object.values(statusClasses).forEach(c => el.classList.remove(c));
    el.classList.add(statusClasses[next]);
    updateCounts();
  }

  function updateCounts() {
    const table = document.querySelector('#milestones-table');
    if (!table) return;
    const badges = table.querySelectorAll('tbody .badge');
    let c=0,p=0,pe=0,r=0;
    badges.forEach(b => {
      const t = b.textContent.trim();
      if (t==='Complete') c++;
      else if (t==='In Progress') p++;
      else if (t==='At Risk') r++;
      else pe++;
    });
    document.getElementById('count-complete').textContent = c;
    document.getElementById('count-progress').textContent = p;
    document.getElementById('count-pending').textContent = pe;
    document.getElementById('count-risk').textContent = r;
  }

  function addMilestoneRow() {
    const tbody = document.querySelector('#milestones-table tbody');
    const row = document.createElement('tr');
    row.innerHTML = `
      <td><span class="phase-a">A</span></td>
      <td><span contenteditable="true" placeholder="Add milestone..."></span></td>
      <td><span contenteditable="true" placeholder="Owner"></span></td>
      <td><span contenteditable="true" placeholder="Date"></span></td>
      <td><span class="badge badge-pending" onclick="cycleStatus(this)">Pending</span></td>
      <td><span contenteditable="true" placeholder="Notes..."></span></td>`;
    tbody.appendChild(row);
    updateCounts();
  }

  updateCounts();
</script>
</body>
</html>
