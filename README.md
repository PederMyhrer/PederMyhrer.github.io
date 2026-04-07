<!DOCTYPE html>
<!-- spareoversikt build 2 -->
<html lang="no">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spareoversikt</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;1,9..144,300&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --bg: #F5F2EB; --surface: #FFFEF9; --surface2: #EEE9DE; --border: #D4CCBA;
  --text: #1A1812; --text2: #6B6354; --text3: #9E9487;
  --green: #2D5A1B; --green-bg: #E8F0E3; --green-light: #f0f6ec;
  --red: #7A2020; --red-bg: #F5E8E8;
  --amber: #7A4E10; --amber-bg: #F5EBD8;
  --blue: #1a3f6b; --blue-bg: #e6eef8;
  --purple: #3d2060; --purple-bg: #ede8f5;
  --accent: #2D5A1B;
  --mono: 'DM Mono', monospace; --serif: 'Fraunces', Georgia, serif;
}
body { background: var(--bg); color: var(--text); font-family: var(--mono); min-height: 100vh; padding: 2rem 2rem 4rem; }
.wrap { max-width: 1400px; margin: 0 auto; }
header { margin-bottom: 2rem; }
header h1 { font-family: var(--serif); font-size: 2.2rem; font-weight: 300; font-style: italic; line-height: 1.1; }
header p { font-size: 0.75rem; color: var(--text3); margin-top: 0.4rem; letter-spacing: 0.06em; text-transform: uppercase; }

/* TABS */
.tabs { display: flex; gap: 0; border-bottom: 1px solid var(--border); margin-bottom: 2rem; }
.tab-btn { font-family: var(--mono); font-size: 0.75rem; letter-spacing: 0.06em; text-transform: uppercase; color: var(--text3); background: none; border: none; border-bottom: 2px solid transparent; padding: 0.6rem 1.2rem 0.55rem; cursor: pointer; transition: color 0.15s, border-color 0.15s; margin-bottom: -1px; }
.tab-btn:hover { color: var(--text2); }
.tab-btn.active { color: var(--text); border-bottom-color: var(--accent); }
.tab-content { display: none; }
.tab-content.active { display: block; }

/* SHARED PANEL */
.grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
@media (max-width: 620px) { .grid { grid-template-columns: 1fr; } }
.panel { background: var(--surface); border: 1px solid var(--border); border-radius: 4px; padding: 1.25rem; }
.panel-title { font-size: 0.65rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text3); margin-bottom: 1rem; }
.input-row { display: flex; justify-content: space-between; align-items: center; padding: 0.45rem 0; border-bottom: 1px solid var(--surface2); gap: 8px; }
.input-row:last-child { border-bottom: none; }
.input-label { font-size: 0.78rem; color: var(--text2); flex: 1; }
.input-label small { display: block; font-size: 0.65rem; color: var(--text3); margin-top: 1px; }
.input-wrap { position: relative; }
.input-wrap span { position: absolute; right: 7px; top: 50%; transform: translateY(-50%); font-size: 0.7rem; color: var(--text3); pointer-events: none; }
input[type="text"] {
  background: var(--surface2); border: 1px solid var(--border); border-radius: 3px;
  color: var(--text); font-family: var(--mono); font-size: 0.8rem;
  padding: 0.3rem 2rem 0.3rem 0.5rem; width: 120px; text-align: right; transition: border-color 0.15s;
}
input[type="text"]:focus { outline: 2px solid var(--accent); outline-offset: 1px; border-color: var(--accent); }
input[type="text"].error { border-color: var(--red); }
.toggle-row { display: flex; justify-content: space-between; align-items: center; padding: 0.45rem 0; border-bottom: 1px solid var(--surface2); }
.toggle-row:last-child { border-bottom: none; }
.toggle { position: relative; width: 36px; height: 20px; flex-shrink: 0; }
.toggle input { opacity: 0; width: 0; height: 0; }
.toggle-slider { position: absolute; inset: 0; background: var(--surface2); border: 1px solid var(--border); border-radius: 20px; cursor: pointer; transition: 0.2s; }
.toggle-slider::before { content: ''; position: absolute; width: 14px; height: 14px; background: var(--text3); border-radius: 50%; top: 2px; left: 2px; transition: 0.2s; }
.toggle input:checked + .toggle-slider { background: var(--green-bg); border-color: var(--green); }
.toggle input:checked + .toggle-slider::before { background: var(--green); transform: translateX(16px); }

/* SUMMARY CARDS */
.summary-grid { display: grid; grid-template-columns: repeat(3, minmax(0,1fr)); gap: 10px; margin-bottom: 0.5rem; }
.sum-card { background: var(--surface); border: 1px solid var(--border); border-radius: 4px; padding: 0.9rem; }
.sum-label { font-size: 0.62rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text3); margin-bottom: 0.3rem; }
.sum-val { font-size: 1.05rem; font-weight: 500; }
.section-head { font-size: 0.65rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text3); margin-bottom: 0.75rem; margin-top: 1.75rem; }

/* ACCOUNT TOTAL */
.account-total-row { display: flex; justify-content: space-between; align-items: flex-start; padding: 0.6rem 0 0.1rem; margin-top: 0.35rem; border-top: 1px solid var(--border); }
.account-total-label { font-size: 0.72rem; font-weight: 500; color: var(--text2); padding-top: 2px; }
.account-total-right { text-align: right; }
.account-total-val { font-size: 0.9rem; font-weight: 500; }
.account-total-val.match { color: var(--green); }
.match-hint { font-size: 0.62rem; margin-top: 2px; }
.match-hint.ok { color: var(--green); }
.match-hint.bad { color: var(--red); }

/* TIMELINE */
.timeline { margin-top: 0.5rem; }
.tl-month { background: var(--surface); border: 1px solid var(--border); border-radius: 4px; margin-bottom: 0.6rem; overflow: hidden; }
.tl-month-header { display: flex; justify-content: space-between; align-items: center; padding: 0.7rem 1rem; cursor: pointer; user-select: none; transition: background 0.12s; }
.tl-month-header:hover { background: var(--surface2); }
.tl-month-name { font-size: 0.8rem; font-weight: 500; letter-spacing: 0.04em; }
.tl-month-right { display: flex; align-items: center; gap: 0.75rem; flex-wrap: wrap; justify-content: flex-end; }
.tl-month-total { font-size: 0.88rem; font-weight: 500; }
.tl-badge { font-size: 0.6rem; padding: 2px 7px; border-radius: 2px; letter-spacing: 0.05em; text-transform: uppercase; }
.badge-warn { background: var(--amber-bg); color: var(--amber); }
.badge-ok { background: var(--green-bg); color: var(--green); }
.badge-blue { background: var(--blue-bg); color: var(--blue); }
.badge-purple { background: var(--purple-bg); color: var(--purple); }
.chevron { font-size: 0.6rem; color: var(--text3); transition: transform 0.2s; display: inline-block; }
.tl-month.open > .tl-month-header .chevron { transform: rotate(180deg); }
.tl-month-body { display: none; padding: 0.7rem 1rem; border-top: 1px solid var(--surface2); }
.tl-month.open .tl-month-body { display: block; }
.tl-row { display: flex; justify-content: space-between; align-items: center; padding: 0.32rem 0; border-bottom: 1px solid var(--surface2); font-size: 0.75rem; gap: 8px; }
.tl-row:last-child { border-bottom: none; }
.tl-row-label { color: var(--text2); }
.tl-row-val { font-weight: 500; white-space: nowrap; }
.pos { color: var(--green); } .neg { color: var(--red); } .neut { color: var(--text); }
.tl-total { display: flex; justify-content: space-between; padding: 0.45rem 0 0; font-size: 0.8rem; font-weight: 500; border-top: 1px solid var(--border); margin-top: 0.3rem; }
.tl-note { font-size: 0.67rem; color: var(--text3); margin-top: 0.5rem; padding: 0.38rem 0.6rem; background: var(--surface2); border-radius: 3px; }
.tl-unlocked { font-size: 0.67rem; margin-top: 0.5rem; padding: 0.38rem 0.6rem; border-radius: 3px; }
.tl-unlocked.type-buffer { background: var(--blue-bg); color: var(--blue); }
.tl-unlocked.type-wish { background: var(--green-light); color: var(--green); }
.bar-wrap { height: 3px; background: var(--surface2); border-radius: 2px; margin-top: 0.65rem; overflow: hidden; }
.bar-fill { height: 3px; border-radius: 2px; background: var(--accent); transition: width 0.35s; }

/* QUEUE TAB */
.queue-area { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; margin-bottom: 1.5rem; }
@media (max-width: 620px) { .queue-area { grid-template-columns: 1fr; } }
.queue-list { display: flex; flex-direction: column; gap: 0.5rem; }
.queue-item {
  background: var(--surface); border: 1px solid var(--border); border-radius: 4px;
  padding: 0.7rem 0.85rem; display: flex; align-items: center; gap: 8px;
  cursor: grab; user-select: none; transition: box-shadow 0.15s, opacity 0.15s;
}
.queue-item:active { cursor: grabbing; }
.queue-item.dragging { opacity: 0.4; }
.queue-item.drag-over { box-shadow: 0 -2px 0 var(--accent); }
.qi-handle { color: var(--text3); font-size: 0.75rem; flex-shrink: 0; cursor: grab; }
.qi-type { font-size: 0.58rem; padding: 2px 6px; border-radius: 2px; letter-spacing: 0.05em; text-transform: uppercase; flex-shrink: 0; }
.qi-type.buffer { background: var(--blue-bg); color: var(--blue); }
.qi-type.wish { background: var(--green-light); color: var(--green); }
.qi-name { font-size: 0.78rem; color: var(--text); flex: 1; min-width: 0; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.qi-amount { font-size: 0.78rem; font-weight: 500; color: var(--text2); white-space: nowrap; }
.qi-delete { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.85rem; padding: 0 2px; line-height: 1; flex-shrink: 0; }
.qi-delete:hover { color: var(--red); }
.qi-num { font-size: 0.65rem; color: var(--text3); min-width: 14px; text-align: right; flex-shrink: 0; }
  .qi-planned { font-size: 0.6rem; padding: 2px 7px; border-radius: 2px; background: #EDE8F5; color: #3d2060; letter-spacing: 0.04em; flex-shrink: 0; white-space: nowrap; }

.add-form { background: var(--surface); border: 1px solid var(--border); border-radius: 4px; padding: 1rem; }
.add-form-title { font-size: 0.65rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--text3); margin-bottom: 0.85rem; }
.form-row { display: flex; flex-direction: column; gap: 4px; margin-bottom: 0.75rem; }
.form-label { font-size: 0.7rem; color: var(--text2); }
.form-input {
  background: var(--surface2); border: 1px solid var(--border); border-radius: 3px;
  color: var(--text); font-family: var(--mono); font-size: 0.8rem;
  padding: 0.35rem 0.6rem; width: 100%; transition: border-color 0.15s;
}
.form-input:focus { outline: 2px solid var(--accent); outline-offset: 1px; border-color: var(--accent); }
.type-select { display: flex; gap: 0.5rem; margin-bottom: 0.75rem; }
.type-btn { flex: 1; font-family: var(--mono); font-size: 0.7rem; padding: 0.35rem; border-radius: 3px; border: 1px solid var(--border); background: var(--surface2); color: var(--text2); cursor: pointer; transition: all 0.15s; }
.type-btn.active-wish { background: var(--green-light); border-color: var(--green); color: var(--green); }
.type-btn.active-buffer { background: var(--blue-bg); border-color: var(--blue); color: var(--blue); }
.add-btn { width: 100%; font-family: var(--mono); font-size: 0.72rem; letter-spacing: 0.05em; text-transform: uppercase; padding: 0.45rem; border-radius: 3px; border: 1px solid var(--border); background: var(--surface2); color: var(--text2); cursor: pointer; transition: all 0.15s; }
.add-btn:hover { background: var(--green-bg); border-color: var(--green); color: var(--green); }

.queue-total-row { display: flex; justify-content: space-between; align-items: center; padding: 0.5rem 0 0; border-top: 1px solid var(--border); margin-top: 0.5rem; font-size: 0.78rem; }
.empty-hint { font-size: 0.72rem; color: var(--text3); text-align: center; padding: 1.5rem 0; }

footer { font-size: 0.65rem; color: var(--text3); text-align: center; margin-top: 3rem; letter-spacing: 0.05em; }
  .idea-cat-badge { font-size: 0.58rem; padding: 2px 7px; border-radius: 2px; font-weight: 500; letter-spacing: 0.05em; text-transform: uppercase; flex-shrink: 0; cursor: pointer; border: none; font-family: var(--mono); }
  .idea-cat-maha   { background: #FCEBEB; color: #A32D2D; }
  .idea-cat-trenger { background: #FAEEDA; color: #633806; }
  .idea-cat-onsker { background: #EAF3DE; color: #27500A; }
  .idea-cat-ide    { background: #EEE9DE; color: #5F5E5A; }
  .idea-card {
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: 4px;
    padding: 0.6rem 0.9rem;
    margin-bottom: 0.4rem;
    display: flex;
    align-items: flex-start;
    gap: 10px;
    transition: background 0.1s;
  }
  .idea-card:hover { background: var(--surface2); }
  .idea-card-handle { color: var(--text3); font-size: 0.75rem; cursor: grab; padding-top: 2px; flex-shrink: 0; }
  .idea-card-num { font-size: 0.62rem; color: var(--text3); min-width: 14px; flex-shrink: 0; padding-top: 3px; }
  .idea-card-body { flex: 1; min-width: 0; }
  .idea-card-title { display: flex; align-items: center; gap: 7px; flex-wrap: wrap; }
  .idea-card-name { font-size: 0.78rem; font-weight: 500; color: var(--text); flex: 1; min-width: 0; }
  .idea-card-price { font-size: 0.73rem; font-weight: 500; color: var(--green); white-space: nowrap; flex-shrink: 0; }
  .idea-card-link { font-size: 0.68rem; color: var(--blue); text-decoration: none; white-space: nowrap; flex-shrink: 0; border-bottom: 1px solid rgba(26,63,107,0.25); }
  .idea-card-link:hover { border-bottom-color: var(--blue); }
  .idea-card-note { font-size: 0.7rem; color: var(--text3); line-height: 1.5; margin-top: 3px; white-space: pre-wrap; }
  .idea-card-actions { display: flex; gap: 4px; flex-shrink: 0; align-items: center; }
  .idea-card-btn { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.75rem; padding: 2px 4px; line-height: 1; border-radius: 2px; }
  .idea-card-btn:hover { background: var(--surface2); color: var(--text); }
  .idea-card-delete { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.95rem; line-height: 1; padding: 2px 4px; border-radius: 2px; }
  .idea-card-delete:hover { color: var(--red); }
  .idea-cat-popover-wrap { position: relative; flex-shrink: 0; }
  .idea-cat-drop { display: none; position: absolute; top: calc(100% + 4px); left: 0; z-index: 100; background: var(--surface); border: 1px solid var(--border); border-radius: 4px; padding: 5px; min-width: 90px; box-shadow: 0 4px 12px rgba(0,0,0,0.08); }
  .idea-cat-drop button { margin-bottom: 2px; }
  .idea-cat-drop button:last-child { margin-bottom: 0; }
  .active-maha    { opacity: 1 !important; box-shadow: inset 0 0 0 1.5px #A32D2D; }
  .active-trenger { opacity: 1 !important; box-shadow: inset 0 0 0 1.5px #7A4E10; }
  .active-onsker  { opacity: 1 !important; box-shadow: inset 0 0 0 1.5px #2D5A1B; }
  .active-ide     { opacity: 1 !important; box-shadow: inset 0 0 0 1.5px #5F5E5A; }
  .prepurchase-card { background: var(--surface); border: 0.5px solid var(--border); border-radius: 4px; padding: 0.6rem 0.9rem; margin-bottom: 0.4rem; display: flex; align-items: center; gap: 10px; }
  .prepurchase-card:hover { background: var(--surface2); }
  .pp-name { font-size: 0.78rem; font-weight: 500; color: var(--text); flex: 1; }
  .pp-amount { font-size: 0.78rem; font-weight: 500; color: var(--red); white-space: nowrap; }
  .pp-date { font-size: 0.68rem; color: var(--text3); white-space: nowrap; }
  .pp-delete { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.95rem; padding: 2px 4px; }
  .pp-delete:hover { color: var(--red); }
  .pp-debt-bar { height: 4px; background: var(--surface2); border-radius: 2px; overflow: hidden; margin-top: 4px; }
  .pp-debt-fill { height: 4px; border-radius: 2px; background: var(--red); transition: width 0.4s; }

  /* ── BUDSJETT ── */
  .bud-table { border-collapse: collapse; min-width: 100%; font-size: 0.75rem; }
  .bud-table th, .bud-table td { padding: 0.35rem 0.4rem; white-space: nowrap; }
  .bud-table th { font-size: 0.62rem; letter-spacing: 0.06em; text-transform: uppercase; color: var(--text3); font-weight: 400; border-bottom: 1px solid var(--border); text-align: right; }
  .bud-table th:first-child { text-align: left; min-width: 220px; width: 220px; }
  .bud-table td:first-child { min-width: 220px; width: 220px; }
  .bud-table td { border-bottom: 0.5px solid var(--surface2); color: var(--text2); text-align: right; font-size: 0.68rem; }
  .bud-table td:first-child { text-align: left; color: var(--text2); }
  .bud-cat-header td { background: var(--surface2); font-size: 0.65rem; font-weight: 500; letter-spacing: 0.07em; text-transform: uppercase; color: var(--text2); padding: 0.5rem 0.6rem; border-bottom: 1px solid var(--border); }
  .bud-cat-total td { background: transparent; font-weight: 400; font-size: 0.68rem; color: var(--text3); border-top: 0.5px solid var(--surface2); border-bottom: 0.5px solid var(--surface2); }
  .bud-cat-total td:first-child { color: var(--text3); }
  .bud-zero-total td { font-weight: 500; font-size: 0.82rem; background: var(--surface); border-top: 2px solid var(--border); border-bottom: 2px solid var(--border); }
  /* Sticky "Til fordeling" header row */
  .bud-sticky-row th { position: sticky; top: 0; z-index: 10; background: var(--bg); border-bottom: 1px solid var(--border); font-size: 0.68rem; font-weight: 400; color: var(--text2); padding: 0.35rem 0.4rem; }
  .bud-sticky-row th:first-child { text-align: left; }
  .bud-sticky-row th.pos { color: var(--green); }
  .bud-sticky-row th.neg { color: var(--red); }
  .bud-cell-input { background: transparent; border: none; border-bottom: 1px solid transparent; color: var(--text2); font-family: var(--mono); font-size: 0.68rem; text-align: right; width: 70px; padding: 1px 2px; border-radius: 2px; }
  .bud-cell-input:focus { outline: none; border-bottom-color: var(--accent); background: var(--surface2); }
  .bud-name-input { background: transparent; border: none; color: var(--text2); font-family: var(--mono); font-size: 0.75rem; width: 100%; padding: 1px 2px; border-radius: 2px; }
  .bud-name-input:focus { outline: none; background: var(--surface2); color: var(--text); }
  .bud-add-btn { background: none; border: 1px dashed var(--border); border-radius: 3px; color: var(--text3); font-family: var(--mono); font-size: 0.68rem; padding: 3px 10px; cursor: pointer; margin-top: 4px; }
  .bud-add-btn:hover { border-color: var(--accent); color: var(--accent); }
  .bud-del-btn { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.8rem; padding: 0 3px; opacity: 0; transition: opacity 0.15s; }
  .bud-edit-mode tr:hover .bud-del-btn { opacity: 1; }
  .bud-del-btn:hover { color: var(--red); }
  .bud-drag-handle { color: var(--text3); font-size: 0.75rem; cursor: grab; padding: 0 3px; opacity: 0; transition: opacity 0.15s; }
  .bud-edit-mode tr:hover .bud-drag-handle { opacity: 1; }
  .bud-drag-handle:active { cursor: grabbing; }
  .bud-edit-btn { font-family: var(--mono); font-size: 0.6rem; letter-spacing: 0.05em; text-transform: uppercase; background: none; border: 1px solid var(--border); border-radius: 3px; color: var(--text3); padding: 2px 8px; cursor: pointer; transition: all 0.15s; }
  .bud-edit-btn:hover { border-color: var(--accent); color: var(--accent); }
  .bud-edit-btn.active { background: var(--green-bg); border-color: var(--green); color: var(--green); }
  tr.bud-dragging { opacity: 0.4; }
  tr.bud-drag-over { box-shadow: 0 -2px 0 var(--accent); }
  .bud-fill-btn { background: none; border: none; color: var(--text3); cursor: pointer; font-size: 0.65rem; padding: 0 4px; letter-spacing: 0.03em; border-radius: 2px; }
  .bud-fill-btn:hover { background: var(--surface2); color: var(--accent); }
  .pos { color: var(--green); } .neg { color: var(--red); }
  .zero-bar { display: flex; gap: 10px; flex-wrap: wrap; }
  .zero-card { background: var(--surface); border: 0.5px solid var(--border); border-radius: 4px; padding: 0.65rem 0.9rem; flex: 1; min-width: 120px; }
  .zero-card-label { font-size: 0.6rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text3); margin-bottom: 3px; }
  .zero-card-val { font-size: 1rem; font-weight: 500; }
  .zero-card.highlight { border-color: var(--accent); }
</style>
</head>
<body>
<div class="wrap">

  <!-- GitHub sync bar -->
  <div id="gh-bar" style="display:flex;align-items:center;gap:10px;margin-bottom:1.5rem;padding:0.6rem 0.9rem;background:var(--surface);border:0.5px solid var(--border);border-radius:4px;font-size:0.72rem;">
    <span style="color:var(--text3);flex-shrink:0;">GitHub token</span>
    <input id="gh-token-input" type="password" placeholder="Lim inn Personal Access Token..." style="flex:1;background:var(--surface2);border:1px solid var(--border);border-radius:3px;font-family:var(--mono);font-size:0.72rem;padding:0.25rem 0.5rem;color:var(--text);">
    <button onclick="ghSaveToken()" style="font-family:var(--mono);font-size:0.68rem;background:none;border:1px solid var(--border);border-radius:3px;padding:3px 10px;cursor:pointer;color:var(--text2);">Lagre</button>
    <span id="gh-status" style="color:var(--text3);white-space:nowrap;"></span>
    <button onclick="ghPush()" id="gh-push-btn" style="font-family:var(--mono);font-size:0.68rem;background:none;border:1px solid var(--border);border-radius:3px;padding:3px 10px;cursor:pointer;color:var(--text2);display:none;">↑ Lagre til GitHub</button>
    <button onclick="ghPull()" id="gh-pull-btn" style="font-family:var(--mono);font-size:0.68rem;background:none;border:1px solid var(--border);border-radius:3px;padding:3px 10px;cursor:pointer;color:var(--text2);display:none;">↓ Hent fra GitHub</button>
  </div>

  <header>
    <h1>Spareoversikt</h1>
    <p>Interaktiv fremskrivning — oppdater forutsetninger under</p>
  </header>

  <div class="tabs">
    <button class="tab-btn active" onclick="switchTab('oversikt')">Oversikt</button>
    <button class="tab-btn" onclick="switchTab('kø')">Prioriteringskø</button>
    <button class="tab-btn" onclick="switchTab('idéer')">Idéer</button>
    <button class="tab-btn" onclick="switchTab('budsjett')">Budsjett</button>
  </div>

  <!-- TAB 1: OVERSIKT -->
  <div id="tab-oversikt" class="tab-content active">
    <div class="grid">
      <div class="panel">
        <p class="panel-title">Kontoer per i dag</p>
        <div class="input-row"><div class="input-label">BSU 1</div><div class="input-wrap"><input type="text" id="bsu1" value="147 948"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">BSU 2</div><div class="input-wrap"><input type="text" id="bsu2" value="125 605"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">BSU Ekstra 1</div><div class="input-wrap"><input type="text" id="bsux1" value="80 632"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">BSU Ekstra 2</div><div class="input-wrap"><input type="text" id="bsux2" value="139 957"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">Sparekonto</div><div class="input-wrap"><input type="text" id="spare" value="10 000"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">Bryllupskonto<small>øremerket, ikke til bolig</small></div><div class="input-wrap"><input type="text" id="bryllup" value="89 428"><span>kr</span></div></div>
        <div class="account-total-row">
          <span class="account-total-label">Sum kontoer</span>
          <div class="account-total-right">
            <div class="account-total-val" id="account-sum">—</div>
            <div class="match-hint" id="match-hint"></div>
          </div>
        </div>
      </div>

      <div class="panel">
        <p class="panel-title">Sparing per måned</p>
        <div class="input-row"><div class="input-label">April</div><div class="input-wrap"><input type="text" id="apr" value="24 770"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">Mai<small>kommer inn etter kjøp</small></div><div class="input-wrap"><input type="text" id="mai" value="19 300"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">Juni</div><div class="input-wrap"><input type="text" id="jun" value="75 500"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">Juli</div><div class="input-wrap"><input type="text" id="jul" value="45 223"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">August</div><div class="input-wrap"><input type="text" id="aug" value="47 609"><span>kr</span></div></div>
        <div class="input-row"><div class="input-label">September og videre<small>snitt månedlig</small></div><div class="input-wrap"><input type="text" id="snitt" value="18 773"><span>kr</span></div></div>
        <div style="margin-top:1.25rem; border-top:1px solid var(--surface2); padding-top:1rem;">
          <p class="panel-title">Innstillinger</p>
          <div class="toggle-row">
            <span class="input-label">Fyll bryllupskonto i juni</span>
            <label class="toggle"><input type="checkbox" id="refillJun" checked><span class="toggle-slider"></span></label>
          </div>
          <div class="input-row" style="border-bottom:none; margin-top:0.1rem;">
            <div class="input-label">Egenkapital til megler</div>
            <div class="input-wrap"><input type="text" id="egenkap" value="560 000"><span>kr</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="section-head">Oppsummering</div>
    <div class="summary-grid">
      <div class="sum-card"><div class="sum-label">Lån fra bryllupskonto</div><div class="sum-val" id="s-loan">—</div></div>
      <div class="sum-card"><div class="sum-label">Bryllupskonto full igjen</div><div class="sum-val" id="s-refill">—</div></div>
      <div class="sum-card"><div class="sum-label">Fritt etter august</div><div class="sum-val pos" id="s-aug">—</div></div>
    </div>

  </div>

  <!-- TAB 2: PRIORITERINGSKØ -->
  <div id="tab-kø" class="tab-content">
    <div class="queue-area">
      <div>
        <div class="panel" style="margin-bottom:1rem;">
          <p class="panel-title">Legg til</p>
          <div class="type-select">
            <button class="type-btn active-wish" id="type-wish-btn" onclick="setType('wish')">Ønskeliste</button>
            <button class="type-btn" id="type-buffer-btn" onclick="setType('buffer')">Buffer</button>
          </div>
          <div class="form-row">
            <label class="form-label">Navn</label>
            <input type="text" class="form-input" id="q-name" placeholder="f.eks. Sofa, Bufferkonto..." style="width:100%; padding-right:0.6rem;">
          </div>
          <div class="form-row">
            <label class="form-label">Beløp</label>
            <div class="input-wrap" style="width:100%;">
              <input type="text" class="form-input" id="q-amount" placeholder="0" style="width:100%; padding-right:2rem;">
              <span>kr</span>
            </div>
          </div>
          <div class="form-row">
            <label class="form-label">Planlagt måned <span style="color:var(--text3);font-weight:400;">(valgfritt)</span></label>
            <select class="form-input" id="q-month" style="width:100%;padding-right:0.6rem;">
              <option value="">— Ingen, første mulig —</option>
              <option value="Mai-2026">Mai 2026</option>
              <option value="Juni-2026">Juni 2026</option>
              <option value="Juli-2026">Juli 2026</option>
              <option value="August-2026">August 2026</option>
              <option value="September-2026">September 2026</option>
              <option value="Oktober-2026">Oktober 2026</option>
              <option value="November-2026">November 2026</option>
              <option value="Desember-2026">Desember 2026</option>
              <option value="Januar-2027">Januar 2027</option>
              <option value="Februar-2027">Februar 2027</option>
              <option value="Mars-2027">Mars 2027</option>
              <option value="April-2027">April 2027</option>
              <option value="Mai-2027">Mai 2027</option>
              <option value="Juni-2027">Juni 2027</option>
              <option value="Juli-2027">Juli 2027</option>
              <option value="August-2027">August 2027</option>
              <option value="September-2027">September 2027</option>
              <option value="Oktober-2027">Oktober 2027</option>
              <option value="November-2027">November 2027</option>
              <option value="Desember-2027">Desember 2027</option>
              <option value="Januar-2028">Januar 2028</option>
              <option value="Februar-2028">Februar 2028</option>
              <option value="Mars-2028">Mars 2028</option>
              <option value="April-2028">April 2028</option>
              <option value="Mai-2028">Mai 2028</option>
              <option value="Juni-2028">Juni 2028</option>
              <option value="Juli-2028">Juli 2028</option>
              <option value="August-2028">August 2028</option>
              <option value="September-2028">September 2028</option>
              <option value="Oktober-2028">Oktober 2028</option>
              <option value="November-2028">November 2028</option>
              <option value="Desember-2028">Desember 2028</option>
            </select>
          </div>
          <button class="add-btn" onclick="addQueueItem()">+ Legg til i kø</button>
        </div>

        <div>
          <p class="panel-title" style="margin-bottom:0.75rem;">Buffere</p>
          <div id="qt-buffer-list" style="margin-bottom:1rem;"><div style="font-size:0.72rem;color:var(--text3);">Ingen buffere lagt til</div></div>

          <p class="panel-title" style="margin-bottom:0.75rem;">Ønskeliste</p>
          <div style="display:flex;justify-content:space-between;font-size:0.8rem;margin-bottom:1rem;">
            <span style="color:var(--text2);">Totalt</span>
            <span style="font-weight:500;color:var(--green);" id="qt-wish">0 kr</span>
          </div>
        </div>
      </div>

      <div class="panel">
        <p class="panel-title">Prioritert rekkefølge <span style="font-weight:400; color:var(--text3);">— dra for å endre</span></p>
        <div class="queue-list" id="queue-list">
          <div class="empty-hint" id="queue-empty">Ingen elementer lagt til ennå</div>
        </div>
      </div>
    </div>

    <div class="section-head">Kapitalutvikling</div>

    <!-- KPI CARDS -->
    <div style="display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:10px;margin-bottom:1.25rem;" id="kpi-grid">
      <div class="sum-card">
        <div class="sum-label" id="kpi-cash-label">Cash fritt ved årsslutt</div>
        <div class="sum-val pos" id="kpi-cash">—</div>
      </div>
      <div class="sum-card">
        <div class="sum-label" id="kpi-total-label">Totalt inkl. buffere ved årsslutt</div>
        <div class="sum-val" id="kpi-total">—</div>
      </div>
      <div class="sum-card">
        <div class="sum-label">Buffere (mål)</div>
        <div class="sum-val" style="color:var(--blue);" id="kpi-buf">—</div>
      </div>
    </div>

    <!-- CHART -->
    <div class="panel" style="margin-bottom:1.5rem;">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:1rem;flex-wrap:wrap;gap:0.75rem;">
        <div style="display:flex;gap:1.25rem;font-size:0.72rem;flex-wrap:wrap;align-items:center;">
          <span style="display:flex;align-items:center;gap:6px;"><span style="width:10px;height:3px;background:#2D5A1B;display:inline-block;border-radius:2px;"></span><span style="color:var(--text2);">Cash fritt</span></span>
          <span style="display:flex;align-items:center;gap:6px;"><span style="width:10px;height:3px;background:#1a3f6b;display:inline-block;border-radius:2px;"></span><span style="color:var(--text2);">Totalt inkl. buffere</span></span>
          <span style="display:flex;align-items:center;gap:6px;"><span style="width:8px;height:8px;background:#2D5A1B22;border:1px solid #2D5A1B55;display:inline-block;border-radius:1px;"></span><span style="color:var(--text2);">Sparing inn</span></span>
          <span style="display:flex;align-items:center;gap:6px;"><span style="width:8px;height:8px;background:rgba(26,63,107,0.15);border:1px solid rgba(26,63,107,0.4);display:inline-block;border-radius:1px;"></span><span style="color:var(--text2);">Til buffere</span></span>
          <span style="display:flex;align-items:center;gap:6px;"><span style="width:8px;height:8px;background:rgba(122,32,32,0.18);border:1px solid rgba(122,32,32,0.45);display:inline-block;border-radius:1px;"></span><span style="color:var(--text2);">Til ønskeliste</span></span>
        </div>
        <select id="chart-year-filter" onchange="updateCapitalChart()" style="font-family:var(--mono);font-size:0.72rem;background:var(--surface2);border:1px solid var(--border);border-radius:3px;color:var(--text);padding:0.25rem 0.5rem;cursor:pointer;">
          <option value="all">Alle år</option>
          <option value="2026" selected>2026</option>
          <option value="2027">2027</option>
          <option value="2028">2028</option>
        </select>
      </div>
      <div style="position:relative;width:100%;height:220px;">
        <canvas id="capital-chart"></canvas>
      </div>
    </div>

    <div class="section-head">Når har jeg råd?</div>
    <div class="timeline" id="queue-timeline"></div>
  </div>


  <!-- TAB 3: IDÉER -->
  <div id="tab-idéer" class="tab-content">
    <div class="panel" style="margin-bottom:1.5rem;">
      <p class="panel-title">Ny idé</p>
      <div style="display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:1rem;margin-bottom:0.85rem;">
        <button class="type-btn idea-cat-maha" id="icat-maha" onclick="setIdeaCat('maha')">Må ha</button>
        <button class="type-btn idea-cat-trenger" id="icat-trenger" onclick="setIdeaCat('trenger')">Trenger</button>
        <button class="type-btn idea-cat-onsker active-onsker" id="icat-onsker" onclick="setIdeaCat('onsker')">Ønsker</button>
        <button class="type-btn idea-cat-ide" id="icat-ide" onclick="setIdeaCat('ide')">Idé</button>
      </div>
      <div style="display:grid;grid-template-columns:2fr 1fr 1fr;gap:0.75rem;align-items:start;">
        <div class="form-row" style="margin:0;">
          <label class="form-label">Navn</label>
          <input type="text" class="form-input" id="idea-name" placeholder="f.eks. IKEA hylle..." style="width:100%;padding-right:0.6rem;">
        </div>
        <div class="form-row" style="margin:0;">
          <label class="form-label">Pris (valgfritt)</label>
          <div class="input-wrap" style="width:100%;">
            <input type="text" class="form-input" id="idea-price" placeholder="—" style="width:100%;padding-right:2rem;">
            <span>kr</span>
          </div>
        </div>
        <div class="form-row" style="margin:0;">
          <label class="form-label">Lenke (valgfritt)</label>
          <input type="text" class="form-input" id="idea-url" placeholder="https://..." style="width:100%;padding-right:0.6rem;">
        </div>
      </div>
      <div class="form-row" style="margin-top:0.75rem;margin-bottom:0.85rem;">
        <label class="form-label">Notat (valgfritt)</label>
        <textarea class="form-input" id="idea-note" placeholder="Tanker, spørsmål..." rows="2" style="width:100%;padding-right:0.6rem;resize:vertical;line-height:1.5;"></textarea>
      </div>
      <button class="add-btn" onclick="addIdea()">+ Legg til</button>
    </div>

    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:0.75rem;">
      <div class="section-head" style="margin:0;">Idéliste</div>
      <div style="display:flex;gap:5px;flex-wrap:wrap;">
        <button onclick="filterIdeas('all')" id="ifilter-all" class="type-btn idea-cat-ide" style="font-size:0.62rem;padding:2px 9px;">Alle</button>
        <button onclick="filterIdeas('maha')" id="ifilter-maha" class="type-btn idea-cat-maha" style="font-size:0.62rem;padding:2px 9px;">Må ha</button>
        <button onclick="filterIdeas('trenger')" id="ifilter-trenger" class="type-btn idea-cat-trenger" style="font-size:0.62rem;padding:2px 9px;">Trenger</button>
        <button onclick="filterIdeas('onsker')" id="ifilter-onsker" class="type-btn idea-cat-onsker" style="font-size:0.62rem;padding:2px 9px;">Ønsker</button>
        <button onclick="filterIdeas('ide')" id="ifilter-ide" class="type-btn idea-cat-ide" style="font-size:0.62rem;padding:2px 9px;">Idé</button>
      </div>
    </div>
    <div id="idea-list"></div>
  </div>



  <!-- TAB 4: BUDSJETT -->
  <div id="tab-budsjett" class="tab-content">

    <!-- Controls bar -->
    <div style="display:flex;align-items:center;gap:1rem;flex-wrap:wrap;margin-bottom:1.5rem;">
      <select id="bud-year" class="form-input" style="width:auto;padding-right:1rem;" onchange="renderBudget()">
        <option value="2026">2026</option>
        <option value="2027">2027</option>
      </select>
      <div style="display:flex;gap:4px;flex-wrap:wrap;" id="bud-month-filters"></div>
      <button id="bud-edit-btn" class="bud-edit-btn" onclick="budToggleEdit()">Rediger</button>
    </div>

    <!-- Zero-budget summary bar -->
    <div id="bud-zero-bar" style="margin-bottom:1.5rem;"></div>

    <!-- Budget table -->
    <div style="overflow-x:visible;">
      <table id="bud-table" class="bud-table">
        <thead id="bud-thead"></thead>
        <tbody id="bud-tbody"></tbody>
      </table>
    </div>

  </div>

  <footer>Alle tall i NOK &nbsp;·&nbsp; Oppdateres automatisk</footer>
</div>

<script>
// ── UTILS ──
function nbFmt(n) { return Math.round(n).toLocaleString('nb-NO') + '\u00a0kr'; }
function signed(n) { const a = Math.abs(Math.round(n)); return (n >= 0 ? '+\u202f' : '\u2212\u202f') + a.toLocaleString('nb-NO') + '\u00a0kr'; }
function parseVal(id) { const raw = document.getElementById(id).value.replace(/[\s\u00a0\u202f]/g,'').replace(/kr/gi,'').replace(/,/,'.'); const n = parseFloat(raw); return isNaN(n) ? 0 : n; }
function parseRaw(str) { const raw = str.replace(/[\s\u00a0\u202f]/g,'').replace(/kr/gi,'').replace(/,/,'.'); const n = parseFloat(raw); return isNaN(n) ? 0 : n; }
function formatField(el) { const raw = el.value.replace(/[\s\u00a0\u202f]/g,'').replace(/kr/gi,'').replace(/,/,'.'); const n = parseFloat(raw); if (!isNaN(n)) { el.value = Math.round(n).toLocaleString('nb-NO'); el.classList.remove('error'); } else { el.classList.add('error'); } }

// ── TAB SWITCHING ──
function switchTab(name) {
  document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  const tabs = ['oversikt','kø','idéer','budsjett']; const idx = tabs.indexOf(name);
  document.querySelectorAll('.tab-btn')[idx].classList.add('active');
  if (name === 'kø') { renderQueueTimeline(); if (window.Chart) updateCapitalChart(); }
  if (name === 'budsjett') renderBudget();
}

// ── IDÉER ──
let ideas = [];
let ideaCat = 'onsker';
let ideaFilter = 'all';

const CAT_META = {
  maha:    { label: 'Må ha',   cls: 'idea-cat-maha' },
  trenger: { label: 'Trenger', cls: 'idea-cat-trenger' },
  onsker:  { label: 'Ønsker',  cls: 'idea-cat-onsker' },
  ide:     { label: 'Idé',    cls: 'idea-cat-ide' },
};

function setIdeaCat(cat) {
  ideaCat = cat;
  Object.keys(CAT_META).forEach(k => {
    const btn = document.getElementById('icat-' + k);
    if (!btn) return;
    btn.className = 'type-btn ' + CAT_META[k].cls + (k === cat ? ' active-' + k : '');
  });
}

function filterIdeas(cat) {
  ideaFilter = cat;
  document.querySelectorAll('[id^="ifilter-"]').forEach(b => {
    const k = b.id.replace('ifilter-', '');
    b.style.opacity = (cat === 'all' || cat === k) ? '1' : '0.45';
  });
  renderIdeas();
}

function addIdea() {
  const nameEl  = document.getElementById('idea-name');
  const priceEl = document.getElementById('idea-price');
  const urlEl   = document.getElementById('idea-url');
  const noteEl  = document.getElementById('idea-note');
  const name = nameEl.value.trim();
  if (!name) { nameEl.focus(); return; }
  ideas.push({ id: Date.now(), cat: ideaCat, name, price: parseRaw(priceEl.value)||0, url: urlEl.value.trim(), note: noteEl.value.trim() });
  nameEl.value = ''; priceEl.value = ''; urlEl.value = ''; noteEl.value = '';
  nameEl.focus();
  saveState();
  renderIdeas();
}

function removeIdea(id) {
  ideas = ideas.filter(i => i.id !== id);
  saveState();
  renderIdeas();
}

function moveIdea(id, dir) {
  const idx = ideas.findIndex(i => i.id === id);
  const swap = idx + dir;
  if (swap < 0 || swap >= ideas.length) return;
  [ideas[idx], ideas[swap]] = [ideas[swap], ideas[idx]];
  saveState();
  renderIdeas();
}

function setIdeaCardCat(id, cat) {
  const idea = ideas.find(i => i.id === id);
  if (idea) { idea.cat = cat; saveState(); renderIdeas(); }
}

function toggleCatDrop(dropId) {
  const drop = document.getElementById(dropId);
  if (!drop) return;
  const isOpen = drop.style.display === 'block';
  // Close all other dropdowns first
  document.querySelectorAll('.idea-cat-drop').forEach(d => d.style.display = 'none');
  drop.style.display = isOpen ? 'none' : 'block';
}

// Close dropdowns on outside click
document.addEventListener('click', e => {
  if (!e.target.closest('.idea-cat-popover-wrap')) {
    document.querySelectorAll('.idea-cat-drop').forEach(d => d.style.display = 'none');
  }
});

let ideaDragSrc = null;

function renderIdeas() {
  const list = document.getElementById('idea-list');
  list.innerHTML = '';
  const filtered = ideaFilter === 'all' ? ideas : ideas.filter(i => i.cat === ideaFilter);
  if (filtered.length === 0) {
    list.innerHTML = '<div class="empty-hint">' + (ideas.length === 0 ? 'Ingen idéer lagt til ennå' : 'Ingen i denne kategorien') + '</div>';
    return;
  }
  filtered.forEach((idea, idx) => {
    const card = document.createElement('div');
    card.className = 'idea-card';
    card.draggable = true;
    card.dataset.id = idea.id;
    const meta = CAT_META[idea.cat] || CAT_META.ide;
    let href = idea.url ? (idea.url.startsWith('http') ? idea.url : 'https://' + idea.url) : '';
    let domain = href ? href.replace(/^https?:\/\/(www\.)?/, '').split('/')[0] : '';

    const dropId = 'icat-drop-' + idea.id;
    const catOpts = Object.entries(CAT_META).filter(([k]) => k !== idea.cat).map(([k, m]) =>
      `<button onclick="setIdeaCardCat(${idea.id},'${k}')" class="idea-cat-badge ${m.cls}" style="display:block;width:100%;text-align:left;margin-bottom:3px;">${m.label}</button>`
    ).join('');

    card.innerHTML = `
      <span class="idea-card-handle">⠿</span>
      <span class="idea-card-num">${idx+1}</span>
      <div class="idea-card-body">
        <div class="idea-card-title">
          <div class="idea-cat-popover-wrap">
            <button class="idea-cat-badge ${meta.cls}" onclick="toggleCatDrop('${dropId}')">${meta.label} ▾</button>
            <div class="idea-cat-drop" id="${dropId}">${catOpts}</div>
          </div>
          <span class="idea-card-name">${idea.name.replace(/</g,'&lt;')}</span>
          ${idea.price > 0 ? `<span class="idea-card-price">${nbFmt(idea.price)}</span>` : ''}
          ${href ? `<a href="${href}" target="_blank" class="idea-card-link">${domain} ↗</a>` : ''}
        </div>
        ${idea.note ? `<div class="idea-card-note">${idea.note.replace(/</g,'&lt;')}</div>` : ''}
      </div>
      <div class="idea-card-actions">
        <button class="idea-card-btn" onclick="moveIdea(${idea.id},-1)" title="Opp">▲</button>
        <button class="idea-card-btn" onclick="moveIdea(${idea.id},1)" title="Ned">▼</button>
        <button class="idea-card-delete" onclick="removeIdea(${idea.id})" title="Fjern">×</button>
      </div>`;

    card.addEventListener('dragstart', e => { ideaDragSrc = card; card.style.opacity = '0.4'; e.dataTransfer.effectAllowed = 'move'; });
    card.addEventListener('dragend', () => { card.style.opacity = '1'; document.querySelectorAll('.idea-card').forEach(c => c.style.boxShadow = ''); });
    card.addEventListener('dragover', e => { e.preventDefault(); card.style.boxShadow = '0 -2px 0 var(--accent)'; });
    card.addEventListener('dragleave', () => { card.style.boxShadow = ''; });
    card.addEventListener('drop', e => {
      e.preventDefault(); card.style.boxShadow = '';
      if (!ideaDragSrc || ideaDragSrc === card) return;
      const srcId = parseInt(ideaDragSrc.dataset.id);
      const dstId = parseInt(card.dataset.id);
      const si = ideas.findIndex(x => x.id === srcId);
      const di = ideas.findIndex(x => x.id === dstId);
      const [moved] = ideas.splice(si, 1);
      ideas.splice(di, 0, moved);
      saveState(); renderIdeas();
    });

    list.appendChild(card);
  });
}

// Enter key flow
document.getElementById('idea-name').addEventListener('keydown', e => { if (e.key==='Enter') { e.preventDefault(); document.getElementById('idea-price').focus(); } });
document.getElementById('idea-price').addEventListener('keydown', e => { if (e.key==='Enter') { e.preventDefault(); document.getElementById('idea-url').focus(); } });
document.getElementById('idea-url').addEventListener('keydown', e => { if (e.key==='Enter') { e.preventDefault(); document.getElementById('idea-note').focus(); } });
document.getElementById('idea-price').addEventListener('blur', () => {
  const el = document.getElementById('idea-price');
  const n = parseRaw(el.value);
  if (n > 0) el.value = Math.round(n).toLocaleString('nb-NO');
});

// ── SHARED MONTH BUILDER ──
function buildMonths() {
  const bsu1=parseVal('bsu1'), bsu2=parseVal('bsu2'), bsux1=parseVal('bsux1'), bsux2=parseVal('bsux2');
  const spare=parseVal('spare'), bryllup=parseVal('bryllup');
  const apr=parseVal('apr'), mai=parseVal('mai'), jun=parseVal('jun');
  const jul=parseVal('jul'), aug=parseVal('aug'), snitt=parseVal('snitt');
  const egenkap=parseVal('egenkap');
  const refillJun=document.getElementById('refillJun').checked;
  const total = bsu1+bsu2+bsux1+bsux2+spare+bryllup;
  const freeToday = total - bryllup;
  const atPayment = freeToday + apr;
  const loanFromBryllup = Math.max(0, egenkap - atPayment);
  const brylAfterKjop = bryllup - loanFromBryllup;
  let free = Math.max(0, atPayment - egenkap);
  let brylSaldo = brylAfterKjop;
  const months = [];

  // Known months 2026
  const known2026 = [
    { name:'Mai',      year:2026, savings:mai,   special:'kjøpsmåned' },
    { name:'Juni',     year:2026, savings:jun,   refill:true },
    { name:'Juli',     year:2026, savings:jul },
    { name:'August',   year:2026, savings:aug },
    { name:'September',year:2026, savings:snitt },
    { name:'Oktober',  year:2026, savings:snitt },
    { name:'November', year:2026, savings:snitt },
    { name:'Desember', year:2026, savings:snitt },
  ];

  // 2027 and 2028 all use snitt
  const futureMonthNames = ['Januar','Februar','Mars','April','Mai','Juni','Juli','August','September','Oktober','November','Desember'];
  [2027, 2028].forEach(yr => {
    futureMonthNames.forEach(mn => {
      known2026.push({ name: mn, year: yr, savings: snitt });
    });
  });

  known2026.forEach((m, idx) => {
    const prevFree = free;
    let refillAmt = 0;
    if (m.refill && refillJun && loanFromBryllup > 0) {
      refillAmt = Math.min(loanFromBryllup, free + m.savings);
    }
    free = free + m.savings - refillAmt;
    brylSaldo += refillAmt;
    months.push({
      name: m.name, year: m.year, free, brylSaldo,
      savings: m.savings, refillAmt, prevFree,
      special: m.special || null,
      loanFromBryllup: idx === 0 ? loanFromBryllup : 0,
    });
  });

  return { months, loanFromBryllup, bryllup, atPayment, egenkap, freeToday, total, refillJun };
}

// ── OVERSIKT TAB ──
function calc() {
  const bsu1=parseVal('bsu1'), bsu2=parseVal('bsu2'), bsux1=parseVal('bsux1'), bsux2=parseVal('bsux2');
  const spare=parseVal('spare'), bryllup=parseVal('bryllup');

  const total = bsu1+bsu2+bsux1+bsux2+spare+bryllup;
  const sumEl = document.getElementById('account-sum');
  const hintEl = document.getElementById('match-hint');
  sumEl.textContent = nbFmt(total);
  sumEl.className = 'account-total-val';
  hintEl.textContent = '';
  hintEl.className = 'match-hint';

  const { months, loanFromBryllup, bryllup: brylTarget, atPayment, egenkap } = buildMonths();

  const augMonth = months.find(m => m.name === 'August' && m.year === 2026);
  const augFree = augMonth ? augMonth.free : (months[months.length-1].free);

  const lEl = document.getElementById('s-loan');
  if (lEl) { lEl.textContent = loanFromBryllup>0 ? nbFmt(loanFromBryllup) : '0 kr'; lEl.className = 'sum-val '+(loanFromBryllup>0?'neg':'pos'); }
  const rm = months.find(m => Math.round(m.brylSaldo) >= Math.round(brylTarget));
  const sRefill = document.getElementById('s-refill');
  if (sRefill) sRefill.textContent = rm ? rm.name+' '+rm.year : (loanFromBryllup===0 ? 'Ikke nødvendig' : 'Etter 2028');
  const sAug = document.getElementById('s-aug');
  if (sAug) sAug.textContent = nbFmt(augFree);

  const tl = document.getElementById('timeline');
  if (!tl) return;
  tl.innerHTML = '';

  // Simulate buffers per month
  const buffers_calc = queueItems.filter(it => it.type === 'buffer');
  let bufFilled_calc = buffers_calc.map(b => ({ ...b, filled: 0 }));

  // Group months by year
  const byYear = {};
  months.forEach(m => {
    if (!byYear[m.year]) byYear[m.year] = [];
    let remaining = m.free;
    let allocBuf = 0;
    bufFilled_calc = bufFilled_calc.map(b => {
      const needed = b.amount - b.filled;
      if (needed<=0||remaining<=0) return b;
      const fill = Math.min(needed, remaining);
      remaining -= fill; allocBuf += fill;
      return {...b, filled: b.filled+fill};
    });
    const bfSnapshot = bufFilled_calc.map(b=>({...b}));
    byYear[m.year].push({ ...m, allocBuf, bfSnapshot, freeAfterBuf: m.free - allocBuf });
  });

  Object.entries(byYear).forEach(([year, yMonths]) => {
    const yrFreeEnd = yMonths[yMonths.length-1].freeAfterBuf;
    const yrTotalEnd = yMonths[yMonths.length-1].free;
    const yrSavings = yMonths.reduce((s,m2)=>s+m2.savings,0);
    const maxFreeYear = Math.max(...yMonths.map(m2=>m2.freeAfterBuf),1);

    const yrDiv = document.createElement('div');
    yrDiv.className = 'tl-month';
    yrDiv.style.marginBottom = '0.6rem';

    const monthsHtml = yMonths.map(m => {
      const rowsArr = [];
      if (m.loanFromBryllup > 0) rowsArr.push({ label:'Lån fra bryllupskonto', val:-m.loanFromBryllup, cls:'neg' });
      rowsArr.push({ label:'Sparing inn', val:m.savings, cls:'pos' });
      if (m.refillAmt > 0) rowsArr.push({ label:'Tilbake til bryllupskonto', val:-m.refillAmt, cls:'neg' });
      if (m.allocBuf > 0) rowsArr.push({ label:'Satt av til buffere', val:-m.allocBuf, cls:'neg' });
      const rowsHtml = rowsArr.map(r => `<div class="tl-row"><span class="tl-row-label">${r.label}</span><span class="tl-row-val ${r.cls}">${signed(r.val)}</span></div>`).join('');

      const bufRows = m.bfSnapshot.length ? m.bfSnapshot.map(b => {
        const pctFill = b.amount>0 ? Math.min(100,Math.round((b.filled/b.amount)*100)) : 0;
        const isFull = b.filled >= b.amount;
        return `<div style="margin-top:5px;">
          <div style="display:flex;justify-content:space-between;font-size:0.68rem;margin-bottom:2px;">
            <span style="color:var(--text2);">${b.name}</span>
            <span style="color:${isFull?'var(--blue)':'var(--text3)'};">${nbFmt(Math.min(b.filled,b.amount))} / ${nbFmt(b.amount)}${isFull?' ✓':''}</span>
          </div>
          <div style="height:3px;background:var(--surface2);border-radius:2px;overflow:hidden;">
            <div style="height:3px;background:var(--blue);border-radius:2px;width:${pctFill}%;"></div>
          </div>
        </div>`;
      }).join('') : '';

      const pct = Math.max(0, Math.round((m.freeAfterBuf / maxFreeYear) * 100));
      const specialBadge = m.special ? `<span class="tl-badge badge-warn">${m.special}</span>` : '';
      const brylNote = m.brylSaldo < brylTarget
        ? `<div class="tl-note">Bryllupskonto: ${nbFmt(m.brylSaldo)} (mangler ${nbFmt(brylTarget-m.brylSaldo)})</div>`
        : (m.refillAmt>0 ? `<div class="tl-note" style="color:var(--green);">Bryllupskonto full igjen ✓</div>` : '');

      return `<div class="tl-month" style="margin:0 0 4px 0;border-radius:3px;">
        <div class="tl-month-header" style="padding:0.5rem 0.75rem;">
          <span class="tl-month-name" style="font-size:0.75rem;">${m.name}</span>
          <div class="tl-month-right">
            ${specialBadge}
            <span style="font-size:0.8rem;font-weight:500;" class="${m.freeAfterBuf>=0?'pos':'neg'}">${nbFmt(m.freeAfterBuf)}</span>
            <span class="chevron">▼</span>
          </div>
        </div>
        <div class="tl-month-body" style="padding:0.5rem 0.75rem;">
          <div class="tl-row"><span class="tl-row-label">Fra forrige</span><span class="tl-row-val neut">${nbFmt(m.prevFree)}</span></div>
          ${rowsHtml}
          <div class="tl-total"><span>Fritt etter buffere</span><span class="${m.freeAfterBuf>=0?'pos':'neg'}">${nbFmt(m.freeAfterBuf)}</span></div>
          <div style="display:flex;justify-content:space-between;font-size:0.72rem;margin-top:3px;"><span style="color:var(--text2);">Totalt inkl. buffere</span><span style="color:var(--text2);">${nbFmt(m.free)}</span></div>
          ${bufRows ? `<div style="border-top:1px solid var(--surface2);margin-top:0.4rem;padding-top:0.4rem;">${bufRows}</div>` : ''}
          ${brylNote}
          <div class="bar-wrap"><div class="bar-fill" style="width:${pct}%"></div></div>
        </div>
      </div>`;
    }).join('');

    yrDiv.innerHTML = `
      <div class="tl-month-header">
        <span class="tl-month-name">${year}</span>
        <div class="tl-month-right">
          <span style="font-size:0.72rem;color:var(--text3);">inn ${nbFmt(yrSavings)}</span>
          <span class="tl-month-total pos">${nbFmt(yrFreeEnd)}</span>
          <span class="chevron">▼</span>
        </div>
      </div>
      <div class="tl-month-body" style="padding:0.5rem 0.75rem;">
        <div style="display:flex;justify-content:space-between;font-size:0.72rem;margin-bottom:8px;padding-bottom:6px;border-bottom:1px solid var(--surface2);">
          <span style="color:var(--text2);">Totalt inkl. buffere ved årsslutt</span>
          <span style="font-weight:500;color:var(--text2);">${nbFmt(yrTotalEnd)}</span>
        </div>
        ${monthsHtml}
      </div>`;

    if (parseInt(year) === 2026) yrDiv.classList.add('open');

    const yrChev1 = yrDiv.querySelector(':scope > .tl-month-header .chevron');
    if (yrChev1) yrChev1.style.transform = yrDiv.classList.contains('open') ? 'rotate(180deg)' : '';
    yrDiv.querySelector('.tl-month-header').addEventListener('click', () => {
      const isOpen = yrDiv.classList.toggle('open');
      const c = yrDiv.querySelector(':scope > .tl-month-header .chevron');
      if (c) c.style.transform = isOpen ? 'rotate(180deg)' : '';
    });
    yrDiv.querySelectorAll('.tl-month-body > .tl-month').forEach(mDiv => {
      const body = mDiv.querySelector('.tl-month-body');
      const chev = mDiv.querySelector(':scope > .tl-month-header .chevron');
      if (body) body.style.display = 'none';
      if (chev) chev.style.transform = '';
      mDiv.querySelector('.tl-month-header').addEventListener('click', () => {
        const b = mDiv.querySelector('.tl-month-body');
        const c = mDiv.querySelector(':scope > .tl-month-header .chevron');
        const isOpen = mDiv.classList.toggle('open');
        if (b) b.style.display = isOpen ? 'block' : 'none';
        if (c) c.style.transform = isOpen ? 'rotate(180deg)' : '';
      });
    });

    tl.appendChild(yrDiv);
  });
}

// ── QUEUE STATE ──
let queueItems = [];
let dragSrc = null;
let newItemType = 'wish';

function setType(t) {
  newItemType = t;
  document.getElementById('type-wish-btn').className = 'type-btn' + (t==='wish'?' active-wish':'');
  document.getElementById('type-buffer-btn').className = 'type-btn' + (t==='buffer'?' active-buffer':'');
}

function addQueueItem() {
  const nameEl = document.getElementById('q-name');
  const amtEl = document.getElementById('q-amount');
  const monthEl = document.getElementById('q-month');
  const name = nameEl.value.trim();
  const amount = parseRaw(amtEl.value);
  if (!name || amount <= 0) { if (!name) nameEl.focus(); else amtEl.focus(); return; }
  const plannedMonth = monthEl ? monthEl.value : '';
  queueItems.push({ id: Date.now(), type: newItemType, name, amount, plannedMonth });
  nameEl.value = '';
  amtEl.value = '';
  if (monthEl) monthEl.value = '';
  nameEl.focus();
  saveState();
  renderQueue();
  renderQueueTimeline();
}

function removeItem(id) {
  const numId = Number(id);
  queueItems = queueItems.filter(i => i.id !== numId);
  saveState();
  renderQueue();
  renderQueueTimeline();
}

function renderQueue() {
  const list = document.getElementById('queue-list');
  // Remove only queue-item elements, preserve the empty-hint node
  list.querySelectorAll('.queue-item').forEach(el => el.remove());
  const emptyHint = list.querySelector('.empty-hint');
  if (queueItems.length === 0) {
    if (emptyHint) emptyHint.style.display = 'block';
  } else {
    if (emptyHint) emptyHint.style.display = 'none';
    queueItems.forEach((item, idx) => {
      const div = document.createElement('div');
      div.className = 'queue-item';
      div.draggable = true;
      div.dataset.id = item.id;
      const pmBadge = item.plannedMonth ? `<span class="qi-planned">${item.plannedMonth.replace('-', ' ')}</span>` : '';
      div.innerHTML = `<span class="qi-num">${idx+1}</span><span class="qi-handle">⠿</span><span class="qi-type ${item.type}">${item.type==='wish'?'Ønske':'Buffer'}</span><span class="qi-name" title="${item.name}">${item.name}</span>${pmBadge}<span class="qi-amount">${nbFmt(item.amount)}</span><button class="qi-delete" onclick="removeItem(${item.id})" title="Fjern">×</button>`;
      div.addEventListener('dragstart', e => { dragSrc = div; div.classList.add('dragging'); e.dataTransfer.effectAllowed='move'; });
      div.addEventListener('dragend', () => { dragSrc = null; div.classList.remove('dragging'); document.querySelectorAll('.queue-item').forEach(d=>d.classList.remove('drag-over')); });
      div.addEventListener('dragover', e => { e.preventDefault(); e.dataTransfer.dropEffect='move'; div.classList.add('drag-over'); });
      div.addEventListener('dragleave', () => div.classList.remove('drag-over'));
      div.addEventListener('drop', e => {
        e.preventDefault(); div.classList.remove('drag-over');
        if (dragSrc && dragSrc !== div) {
          const srcId = parseInt(dragSrc.dataset.id);
          const dstId = parseInt(div.dataset.id);
          const si = queueItems.findIndex(x=>x.id===srcId);
          const di = queueItems.findIndex(x=>x.id===dstId);
          const [moved] = queueItems.splice(si,1);
          queueItems.splice(di,0,moved);
          saveState(); renderQueue(); renderQueueTimeline();
        }
      });
      list.appendChild(div);
    });
  }
  // totals
  const wishTotal = queueItems.filter(i=>i.type==='wish').reduce((s,i)=>s+i.amount,0);
  const buffers = queueItems.filter(i=>i.type==='buffer');
  const bufTotal = buffers.reduce((s,i)=>s+i.amount,0);
  document.getElementById('qt-wish').textContent = nbFmt(wishTotal);

  // Buffer list panel
  const bufListEl = document.getElementById('qt-buffer-list');
  if (buffers.length === 0) {
    bufListEl.innerHTML = '<div style="font-size:0.72rem;color:var(--text3);">Ingen buffere lagt til</div>';
  } else {
    bufListEl.innerHTML = buffers.map(it =>
      `<div style="display:flex;justify-content:space-between;align-items:center;font-size:0.78rem;padding:5px 0;border-bottom:1px solid var(--surface2);">
        <span style="color:var(--text2);">${it.name}</span>
        <span style="font-weight:500;color:var(--blue);">${nbFmt(it.amount)}</span>
      </div>`
    ).join('') + `<div style="display:flex;justify-content:space-between;font-size:0.78rem;padding:5px 0;font-weight:500;">
      <span style="color:var(--text2);">Totalt</span>
      <span style="color:var(--blue);">${nbFmt(bufTotal)}</span>
    </div>`;
  }

  // Compute per-month cash after buffers for KPI + chart
  updateCapitalChart();
}

let capitalChart = null;

// Shared simulation: computes per-month capital accounting for buffers + wish purchases.
// Returns array of month objects with consistent numbers used by both chart and timelines.
// Parse "Månednavn-Årstall" key into {name, year}
function parsePlannedMonth(pm) {
  if (!pm) return null;
  const [name, year] = pm.split('-');
  return { name, year: parseInt(year) };
}

function simulateMonths() {
  const { months } = buildMonths();
  const buffers = queueItems.filter(i=>i.type==='buffer');
  const wishes  = queueItems.filter(i=>i.type==='wish');

  let bufFilled      = buffers.map(b=>({...b, filled:0}));
  let wishSpentTotal = 0;
  let unlockedWish   = new Set();

  // Track planned-month warnings: itemId -> { canAfford, shortfall }
  const plannedWarnings = {};

  return months.map(m => {
    // Step 1: fill buffers
    // Buffers with a plannedMonth only start filling from that month onwards
    let simBuf = m.free;
    let allocBuf = 0;
    bufFilled = bufFilled.map(b => {
      const pm = parsePlannedMonth(b.plannedMonth);
      // If buffer has a planned month, don't fill before that month
      if (pm) {
        const monthIdx = months.findIndex(x => x.name === m.name && x.year === m.year);
        const targetIdx = months.findIndex(x => x.name === pm.name && x.year === pm.year);
        if (monthIdx < targetIdx) return b; // not yet
      }
      const needed = b.amount - b.filled;
      if (needed <= 0 || simBuf <= 0) return b;
      const fill = Math.min(needed, simBuf);
      simBuf -= fill;
      allocBuf += fill;
      return {...b, filled: b.filled + fill};
    });
    const totalBufFilled = bufFilled.reduce((s,b) => s + b.filled, 0);

    // Step 2: available for wishes after buffers and past spending
    const afterBufAndPastWish = m.free - totalBufFilled - wishSpentTotal;

    // Step 3: unlock wishes — respect plannedMonth
    let allocWishThisMonth = 0;
    let simWish = afterBufAndPastWish;
    for (const w of wishes) {
      if (unlockedWish.has(w.id)) continue;
      const pm = parsePlannedMonth(w.plannedMonth);
      if (pm) {
        // Check if this is the planned month
        const isPlannedMonth = (m.name === pm.name && m.year === pm.year);
        const monthIdx = months.findIndex(x => x.name === m.name && x.year === m.year);
        const targetIdx = months.findIndex(x => x.name === pm.name && x.year === pm.year);
        if (monthIdx < targetIdx) continue; // too early, skip
        if (isPlannedMonth) {
          // Planned month arrived — can we afford it?
          if (simWish >= w.amount) {
            unlockedWish.add(w.id);
            simWish -= w.amount;
            allocWishThisMonth += w.amount;
            wishSpentTotal += w.amount;
          } else {
            // Can't afford — record warning
            plannedWarnings[w.id] = { name: w.name, shortfall: w.amount - simWish, month: m.name + ' ' + m.year };
          }
          continue; // planned item only triggers on its month, don't cascade
        }
        // Past the planned month and still not unlocked (e.g. couldn't afford) — try now
        if (monthIdx > targetIdx && !plannedWarnings[w.id]) {
          if (simWish >= w.amount) {
            unlockedWish.add(w.id);
            simWish -= w.amount;
            allocWishThisMonth += w.amount;
            wishSpentTotal += w.amount;
          }
          continue;
        }
      } else {
        // No planned month: unlock as soon as affordable in queue order
        if (simWish >= w.amount) {
          unlockedWish.add(w.id);
          simWish -= w.amount;
          allocWishThisMonth += w.amount;
          wishSpentTotal += w.amount;
        } else break;
      }
    }

    const cashFritt    = m.free - totalBufFilled - wishSpentTotal;
    const totalInklBuf = cashFritt + totalBufFilled;
    const trueAvailable = m.free - totalBufFilled - (wishSpentTotal - allocWishThisMonth);

    const yearStr    = String(m.year).slice(2);
    const label      = m.name.slice(0,3) + " '" + yearStr;
    const shortLabel = m.name.slice(0,3);

    // Collect any planned-month warnings active this month
    const activeWarnings = Object.values(plannedWarnings).filter(w => w.month === m.name + ' ' + m.year);

    return {
      label, shortLabel,
      year: m.year, name: m.name,
      trueAvailable,
      total: totalInklBuf,
      cashFritt,
      allocBuf,
      allocWish: allocWishThisMonth,
      savings: m.savings || 0,
      bufSnapshot: bufFilled.map(b=>({...b})),
      wishSpentTotal,
      plannedWarnings: activeWarnings,
    };
  });
}

function computeMonthlyCapital() {
  return simulateMonths();
}

function updateCapitalChart() {
  const data = computeMonthlyCapital();
  const buffers = queueItems.filter(i=>i.type==='buffer');
  const bufTotal = buffers.reduce((s,i)=>s+i.amount,0);

  const yearFilter = document.getElementById('chart-year-filter');
  const selectedYear = yearFilter ? yearFilter.value : '2026';
  const singleYear = selectedYear !== 'all';

  const filtered = singleYear
    ? data.filter(d => d.year === parseInt(selectedYear))
    : data;

  // KPI: show end of selected year (or end of 2026 if all)
  const kpiYear = singleYear ? parseInt(selectedYear) : 2026;
  const kpiData = data.filter(d => d.year === kpiYear);
  const kpiEnd = kpiData[kpiData.length-1];
  if (kpiEnd) {
    const yearLabel = kpiYear;
    document.getElementById('kpi-cash-label').textContent = 'Cash fritt ved slutten av ' + yearLabel;
    document.getElementById('kpi-total-label').textContent = 'Totalt inkl. buffere ved slutten av ' + yearLabel;
    document.getElementById('kpi-cash').textContent = nbFmt(Math.max(0, kpiEnd.cashFritt));
    document.getElementById('kpi-total').textContent = nbFmt(kpiEnd.total);
    document.getElementById('kpi-buf').textContent = nbFmt(bufTotal);
  }

  // Update year filter select options dynamically (keep in sync)
  const sel = document.getElementById('chart-year-filter');
  if (sel) {
    Array.from(sel.options).forEach(o => {
      o.selected = o.value === selectedYear;
    });
  }

  if (!window.Chart) return;
  const ctx = document.getElementById('capital-chart');
  if (!ctx) return;
  if (capitalChart) { capitalChart.destroy(); capitalChart = null; }

  // Use short labels (Jan, Feb...) for single year, full labels for all years
  const labels = filtered.map(d => singleYear ? d.shortLabel : d.label);

  capitalChart = new window.Chart(ctx, {
    data: {
      labels,
      datasets: [
        {
          type: 'bar', label: 'Sparing inn',
          data: filtered.map(d=>d.savings),
          backgroundColor: 'rgba(45,90,27,0.12)', borderColor: 'rgba(45,90,27,0.35)',
          borderWidth: 1, borderRadius: 2, order: 5
        },
        {
          type: 'bar', label: 'Til buffere',
          data: filtered.map(d=>d.allocBuf),
          backgroundColor: 'rgba(26,63,107,0.15)', borderColor: 'rgba(26,63,107,0.4)',
          borderWidth: 1, borderRadius: 2, order: 4
        },
        {
          type: 'bar', label: 'Til \u00f8nskeliste',
          data: filtered.map(d=>d.allocWish),
          backgroundColor: 'rgba(122,32,32,0.18)', borderColor: 'rgba(122,32,32,0.45)',
          borderWidth: 1, borderRadius: 2, order: 3
        },
        {
          type: 'line', label: 'Totalt inkl. buffere',
          data: filtered.map(d=>d.total),
          borderColor: '#1a3f6b', borderWidth: 2,
          pointRadius: 2, pointBackgroundColor: '#1a3f6b',
          tension: 0.3, fill: false, order: 1
        },
        {
          type: 'line', label: 'Cash fritt',
          data: filtered.map(d=>Math.max(0, d.cashFritt)),
          borderColor: '#2D5A1B', borderWidth: 2,
          pointRadius: 2, pointBackgroundColor: '#2D5A1B',
          tension: 0.3, fill: false, order: 0
        },
      ]
    },
    options: {
      responsive: true, maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: {
          mode: 'index', intersect: false,
          callbacks: {
            label: c => ' ' + c.dataset.label + ': ' + Math.round(c.parsed.y).toLocaleString('nb-NO') + '\u00a0kr'
          }
        }
      },
      scales: {
        x: {
          ticks: {
            font: { family: 'DM Mono, monospace', size: 11 },
            color: '#9E9487',
            maxRotation: 0,
            autoSkip: false,
            callback: function(val, index) {
              if (singleYear) return filtered[index].shortLabel;
              // All years: show Jan and Jul only (every 6 months)
              const m = filtered[index];
              if (m.shortLabel === 'Jan' || m.shortLabel === 'Jul') return m.shortLabel + ' ' + m.year;
              return '';
            }
          },
          grid: { color: 'rgba(0,0,0,0.04)' }
        },
        y: {
          ticks: {
            font: { family: 'DM Mono, monospace', size: 11 },
            color: '#9E9487',
            callback: v => Math.round(v/1000) + 'k'
          },
          grid: { color: 'rgba(0,0,0,0.06)' }
        }
      }
    }
  });
}

function renderQueueTimeline() {
  const tl = document.getElementById('queue-timeline');
  tl.innerHTML = '';
  if (queueItems.length === 0) {
    tl.innerHTML = '<div class="empty-hint">Legg til elementer i k\u00f8en for \u00e5 se n\u00e5r du har r\u00e5d</div>';
    return;
  }

  const simMonths = simulateMonths();
  const unlockedIds = new Set();

  const byYear = {};
  simMonths.forEach(m => {
    if (!byYear[m.year]) byYear[m.year] = [];
    byYear[m.year].push(m);
  });

  Object.entries(byYear).forEach(([year, yMonths]) => {
    let anyUnlockedInYear = false;

    const monthDivs = yMonths.map(m => {
      // Derive which wish items unlocked this month
      const unlockedThisMonth = [];
      let wishBudget = m.allocWish;
      for (const item of queueItems) {
        if (item.type !== 'wish') continue;
        if (unlockedIds.has(item.id)) continue;
        if (wishBudget >= item.amount) {
          unlockedThisMonth.push(item);
          unlockedIds.add(item.id);
          wishBudget -= item.amount;
        } else break;
      }
      // Buffers completing this month
      const buffersUnlocked = [];
      m.bufSnapshot.forEach(b => {
        const key = 'buf_' + b.id;
        if (b.filled >= b.amount && !unlockedIds.has(key)) {
          buffersUnlocked.push(b);
          unlockedIds.add(key);
        }
      });

      if (unlockedThisMonth.length || buffersUnlocked.length) anyUnlockedInYear = true;

      const stillLocked = queueItems.filter(i => i.type==='wish' && !unlockedIds.has(i.id));
      const nextItem = stillLocked[0];
      const allDone = queueItems.every(i => unlockedIds.has(i.id) || unlockedIds.has('buf_'+i.id));

      const badges = [
        ...buffersUnlocked.map(b => `<span class="tl-badge badge-blue">${b.name}</span>`),
        ...unlockedThisMonth.map(i => `<span class="tl-badge badge-ok">${i.name}</span>`)
      ].join('');

      const unlockedHtml = [
        ...buffersUnlocked.map(b => `<div class="tl-unlocked type-buffer">\u2713 Buffer full: <strong>${b.name}</strong> (${nbFmt(b.amount)})</div>`),
        ...unlockedThisMonth.map(i => `<div class="tl-unlocked type-wish">\u2713 Har r\u00e5d til: <strong>${i.name}</strong> (${nbFmt(i.amount)})</div>`)
      ].join('');

      const nextHint = nextItem
        ? `<div class="tl-note">Neste: <strong>${nextItem.name}</strong> \u2014 ${nbFmt(nextItem.amount)} (mangler ${nbFmt(Math.max(0, nextItem.amount - m.trueAvailable))})</div>`
        : (allDone ? `<div class="tl-note" style="color:var(--green);">Hele k\u00f8en er finansiert \u2713</div>` : '');

      // Planned month warnings for this month
      const warningHtml = (m.plannedWarnings||[]).map(w =>
        `<div style="font-size:0.68rem;background:#FCEBEB;color:#A32D2D;border-radius:3px;padding:5px 8px;margin-top:4px;">
          \u26a0 <strong>${w.name}</strong> er planlagt denne m\u00e5neden, men du mangler ${nbFmt(w.shortfall)}
        </div>`
      ).join('');

      // Planned badge on month header if something is planned here
      const plannedBadge = (m.plannedWarnings||[]).length > 0
        ? `<span class="tl-badge" style="background:#FCEBEB;color:#A32D2D;">planlagt</span>`
        : '';

      return `<div class="tl-month" style="margin:0 0 4px 0;border-radius:3px;">
        <div class="tl-month-header" style="padding:0.5rem 0.75rem;">
          <span class="tl-month-name" style="font-size:0.75rem;">${m.name}</span>
          <div class="tl-month-right">
            ${plannedBadge}
            ${badges}
            <span class="tl-month-total ${m.cashFritt>=0?'pos':'neg'}" style="font-size:0.8rem;">${nbFmt(m.cashFritt)}</span>
            <span class="chevron">\u25bc</span>
          </div>
        </div>
        <div class="tl-month-body" style="padding:0.5rem 0.75rem;">
          <div class="tl-row"><span class="tl-row-label">Tilgjengelig kapital</span><span class="tl-row-val neut">${nbFmt(m.trueAvailable)}</span></div>
          ${m.allocWish>0?`<div class="tl-row"><span class="tl-row-label">\u00d8nskeliste kj\u00f8p</span><span class="tl-row-val neg">${signed(-m.allocWish)}</span></div>`:''}
          ${m.allocBuf>0?`<div class="tl-row"><span class="tl-row-label">Til buffere</span><span class="tl-row-val neg">${signed(-m.allocBuf)}</span></div>`:''}
          <div class="tl-total"><span>Cash fritt</span><span class="${m.cashFritt>=0?'pos':'neg'}">${nbFmt(m.cashFritt)}</span></div>
          <div style="display:flex;justify-content:space-between;font-size:0.72rem;margin-top:3px;"><span style="color:var(--text2);">Totalt inkl. buffere</span><span style="color:var(--text2);">${nbFmt(m.total)}</span></div>
          ${unlockedHtml}
          ${warningHtml}
          ${nextHint}
        </div>
      </div>`;
    }).join('');

    const lastM = yMonths[yMonths.length-1];
    const yrDiv = document.createElement('div');
    yrDiv.className = 'tl-month' + (anyUnlockedInYear || parseInt(year)===2026 ? ' open' : '');
    yrDiv.style.marginBottom = '0.6rem';
    yrDiv.innerHTML = `
      <div class="tl-month-header">
        <span class="tl-month-name">${year}</span>
        <div class="tl-month-right">
          <span class="tl-month-total pos">${nbFmt(lastM.cashFritt)}</span>
          <span class="chevron">\u25bc</span>
        </div>
      </div>
      <div class="tl-month-body" style="padding:0.5rem 0.75rem;">${monthDivs}</div>`;

    const yrChev = yrDiv.querySelector(':scope > .tl-month-header .chevron');
    yrDiv.querySelector('.tl-month-header').addEventListener('click', () => {
      const isOpen = yrDiv.classList.toggle('open');
      if (yrChev) yrChev.style.transform = isOpen ? 'rotate(180deg)' : '';
    });
    // Sync year chevron with initial open state
    if (yrDiv.classList.contains('open') && yrChev) yrChev.style.transform = 'rotate(180deg)';

    yrDiv.querySelectorAll('.tl-month-body > .tl-month').forEach(mDiv => {
      const body = mDiv.querySelector('.tl-month-body');
      const chev = mDiv.querySelector(':scope > .tl-month-header .chevron');
      if (body) body.style.display = 'none';
      if (chev) chev.style.transform = '';
      mDiv.querySelector('.tl-month-header').addEventListener('click', () => {
        const b = mDiv.querySelector('.tl-month-body');
        const c = mDiv.querySelector(':scope > .tl-month-header .chevron');
        const isOpen = mDiv.classList.toggle('open');
        if (b) b.style.display = isOpen ? 'block' : 'none';
        if (c) c.style.transform = isOpen ? 'rotate(180deg)' : '';
      });
    });

    tl.appendChild(yrDiv);
  });
}
// ── ENTER KEY on add form ──
document.getElementById('q-name').addEventListener('keydown', e => { if (e.key==='Enter') { e.preventDefault(); document.getElementById('q-amount').focus(); } });
document.getElementById('q-amount').addEventListener('keydown', e => { if (e.key==='Enter') { e.preventDefault(); addQueueItem(); } });

// ── WIRE UP INPUTS ──
document.querySelectorAll('#tab-oversikt input[type="text"]').forEach(el => {
  el.addEventListener('blur', () => { formatField(el); saveState(); calc(); renderQueueTimeline(); });
  el.addEventListener('input', () => { saveState(); calc(); renderQueueTimeline(); });
});
document.getElementById('refillJun').addEventListener('change', () => { saveState(); calc(); renderQueueTimeline(); });

// also format the queue amount field on blur
document.getElementById('q-amount').addEventListener('blur', () => {
  const el = document.getElementById('q-amount');
  const raw = el.value.replace(/[\s\u00a0\u202f]/g,'').replace(/kr/gi,'').replace(/,/,'.');
  const n = parseFloat(raw);
  if (!isNaN(n) && n > 0) el.value = Math.round(n).toLocaleString('nb-NO');
});


// ── BUDSJETT ──
const BUD_MONTHS = ['Januar','Februar','Mars','April','Mai','Juni','Juli','August','September','Oktober','November','Desember'];
const BUD_CATS = [
  { id: 'inntekter', label: 'Inntekter',    sign: 1  },
  { id: 'kostnader', label: 'Kostnader',    sign: -1 },
  { id: 'sinking',   label: 'Sinking Funds',sign: -1 },
  { id: 'gjeld',     label: 'Gjeld',        sign: -1 },
  { id: 'sparing',   label: 'Sparing',      sign: -1 },
];

// budgetData[year][catId] = [ { id, name, amounts:[12 numbers] }, ... ]
let budgetData = {};
let budEditMode = false;

function budToggleEdit() {
  budEditMode = !budEditMode;
  const table = document.getElementById('bud-table');
  const btn = document.getElementById('bud-edit-btn');
  if (table) table.classList.toggle('bud-edit-mode', budEditMode);
  if (btn) { btn.textContent = budEditMode ? 'Ferdig' : 'Rediger'; btn.classList.toggle('active', budEditMode); }
}
let budVisibleMonths = [0,1,2,3,4,5,6,7,8,9,10,11]; // all by default

function budGetYear() { return parseInt(document.getElementById('bud-year').value) || 2026; }

const BUD_DEFAULTS = {
  inntekter: [
    'Norges Bank','Nydalen DPS','AHUS','Moertune','Lånekassen I','Lånekassen II',
    'Utleie av garasje','Rentefradrag','Renteinntekter','Annen inntekt'
  ],
  kostnader: [
    'Husleie / boliglån','Felleskostnader','Innboforsikring','Strøm','Dagligvarer',
    'Treningssenter','Transport','Forsikring','Mobilabonnement',
    'Macrofactor / Lifesum','ChatGPT','Disney+','Claude','Life360','Netflix','Apple storage'
  ],
  sinking: [
    'Supplements','Julegaver','Bursdager','Personlig Viktoria','Personlig Peder',
    'Skincare','Interiør','Ferie 2026','Fun','Wedding'
  ],
  gjeld: ['Student loan I','Student loan II'],
  sparing: ['BSU P','BSU V','BSU Extra P','BSU Extra V','Emergency Fund'],
};

function budMakeRow(name) {
  return { id: Date.now() + Math.random(), name, amounts: Array(12).fill(0) };
}

function budEnsureYear(year) {
  if (!budgetData[year]) {
    budgetData[year] = {};
    BUD_CATS.forEach(c => {
      const defaults = BUD_DEFAULTS[c.id] || [];
      budgetData[year][c.id] = defaults.map(name => budMakeRow(name));
    });
  }
}

function budAddRow(catId) {
  const year = budGetYear();
  budEnsureYear(year);
  budgetData[year][catId].push({ id: Date.now(), name: '', amounts: Array(12).fill(0) });
  saveState();
  renderBudget();
}

function budRemoveRow(catId, rowId) {
  const year = budGetYear();
  budgetData[year][catId] = budgetData[year][catId].filter(r => r.id !== rowId);
  saveState();
  renderBudget();
}

function budSetName(catId, rowId, val) {
  const year = budGetYear();
  const row = budgetData[year][catId].find(r => r.id === rowId);
  if (row) { row.name = val; saveState(); }
}

function budSetAmount(catId, rowId, mIdx, val) {
  const year = budGetYear();
  const row = budgetData[year][catId].find(r => r.id === rowId);
  if (row) { row.amounts[mIdx] = parseRaw(val) || 0; saveState(); renderBudgetTotals(); }
}

function budToggleFill(rowId) {
  // Close all other fill popovers first
  document.querySelectorAll('[id^="fill-pop-"]').forEach(el => {
    if (el.id !== 'fill-pop-' + rowId) el.style.display = 'none';
  });
  const pop = document.getElementById('fill-pop-' + rowId);
  if (!pop) return;
  const isOpen = pop.style.display === 'flex';
  pop.style.display = isOpen ? 'none' : 'flex';
  if (!isOpen) {
    setTimeout(() => { const inp = document.getElementById('fill-input-' + rowId); if (inp) inp.focus(); }, 50);
  }
}

// Close fill popovers on outside click
document.addEventListener('click', e => {
  if (!e.target.closest('[id^="fill-pop-"]') && !e.target.matches('.bud-fill-btn')) {
    document.querySelectorAll('[id^="fill-pop-"]').forEach(el => el.style.display = 'none');
  }
});

function budFillRow(catId, rowId) {
  const year = budGetYear();
  const row = budgetData[year][catId].find(r => r.id === rowId);
  if (!row) return;
  // Find the fill input for this row
  const fillInput = document.getElementById('fill-input-' + rowId);
  if (!fillInput) return;
  const n = parseRaw(fillInput.value);
  if (isNaN(n) || n < 0) return;
  row.amounts = Array(12).fill(n);
  fillInput.value = '';
  saveState();
  renderBudget();
}

function budCalcCatTotals(year, catId) {
  budEnsureYear(year);
  const rows = budgetData[year][catId];
  const monthly = Array(12).fill(0);
  rows.forEach(r => r.amounts.forEach((a, i) => monthly[i] += a));
  return { monthly, annual: monthly.reduce((s,v)=>s+v,0) };
}

function renderBudgetMonthFilters() {
  const container = document.getElementById('bud-month-filters');
  if (!container) return;
  container.innerHTML = '';
  BUD_MONTHS.forEach((name, i) => {
    const btn = document.createElement('button');
    const short = name.slice(0,3);
    const active = budVisibleMonths.includes(i);
    btn.className = 'type-btn';
    btn.style.cssText = `font-size:0.6rem;padding:2px 8px;background:${active?'rgba(45,90,27,0.12)':'transparent'};border-color:${active?'rgba(45,90,27,0.4)':'var(--border)'};color:${active?'var(--green)':'var(--text3)'};`;
    btn.textContent = short;
    btn.addEventListener('click', () => {
      if (budVisibleMonths.includes(i)) {
        if (budVisibleMonths.length > 1) budVisibleMonths = budVisibleMonths.filter(m => m !== i);
      } else {
        budVisibleMonths = [...budVisibleMonths, i].sort((a,b)=>a-b);
      }
      renderBudget();
    });
    container.appendChild(btn);
  });
}

function renderBudgetTotals() {
  // Just re-render totals without rebuilding full table
  // Easier to just call renderBudget — it's fast enough
  renderBudget();
}

function renderBudget() {
  const year = budGetYear();
  budEnsureYear(year);
  renderBudgetMonthFilters();

  const thead = document.getElementById('bud-thead');
  const tbody = document.getElementById('bud-tbody');
  if (!thead || !tbody) return;

  const visMon = budVisibleMonths;

  // ── PRE-CALCULATE totals for sticky row ──
  // (needs to run before rendering so sticky row is accurate)
  const _innt = budCalcCatTotals(year, 'inntekter');
  const _kost = budCalcCatTotals(year, 'kostnader');
  const _sink = budCalcCatTotals(year, 'sinking');
  const _gjeld = budCalcCatTotals(year, 'gjeld');
  const _spar = budCalcCatTotals(year, 'sparing');
  const _leftMon = Array(12).fill(0).map((_,i) =>
    _innt.monthly[i] - _kost.monthly[i] - _sink.monthly[i] - _gjeld.monthly[i] - _spar.monthly[i]);
  const _leftYear = _leftMon.reduce((s,v)=>s+v,0);

  // ── HEADER ──
  // Apply edit mode class
  const tbl = document.getElementById('bud-table');
  if (tbl) tbl.classList.toggle('bud-edit-mode', budEditMode);

  thead.innerHTML = '';

  // Row 1: Sticky "Til fordeling"
  const stickyRow = document.createElement('tr');
  stickyRow.className = 'bud-sticky-row';
  const thSName = document.createElement('th');
  thSName.textContent = 'Til fordeling';
  stickyRow.appendChild(thSName);
  visMon.forEach(i => {
    const th = document.createElement('th');
    const v = _leftMon[i];
    th.textContent = v !== 0 ? Math.round(v).toLocaleString('nb-NO') : '';
    th.className = v > 0 ? 'pos' : v < 0 ? 'neg' : '';
    stickyRow.appendChild(th);
  });
  const thSYear = document.createElement('th');
  thSYear.textContent = Math.round(_leftYear).toLocaleString('nb-NO');
  thSYear.className = _leftYear >= 0 ? 'pos' : 'neg';
  stickyRow.appendChild(thSYear);
  thead.appendChild(stickyRow);

  // Row 2: Month labels
  const hRow = document.createElement('tr');
  const thName = document.createElement('th');
  thName.textContent = '';
  thName.style.textAlign = 'left';
  hRow.appendChild(thName);
  visMon.forEach(i => {
    const th = document.createElement('th');
    th.textContent = BUD_MONTHS[i].slice(0,3);
    hRow.appendChild(th);
  });
  const thYear = document.createElement('th');
  thYear.textContent = 'År';
  thYear.style.color = 'var(--text2)';
  hRow.appendChild(thYear);
  thead.appendChild(hRow);

  tbody.innerHTML = '';

  // ── CATEGORIES ──
  const catAnnuals = {};
  const catMonthly = {};

  BUD_CATS.forEach(cat => {
    const rows = budgetData[year][cat.id] || [];

    // Category header row
    const catRow = document.createElement('tr');
    catRow.className = 'bud-cat-header';
    const catTd = document.createElement('td');
    catTd.colSpan = visMon.length + 2;
    catTd.innerHTML = `<span>${cat.label}</span>`;
    catRow.appendChild(catTd);
    tbody.appendChild(catRow);

    // Data rows
    rows.forEach(row => {
      const tr = document.createElement('tr');

      // Name cell
      const tdName = document.createElement('td');
      tdName.style.display = 'flex';
      tdName.style.alignItems = 'center';
      tdName.style.gap = '4px';
      tdName.innerHTML = `
        <span class="bud-drag-handle" title="Dra for å flytte">⠿</span>
        <input class="bud-name-input" value="${row.name.replace(/"/g,'&quot;')}" placeholder="Navn..." onchange="budSetName('${cat.id}',${row.id},this.value)" style="flex:1;">
        <span style="position:relative;display:inline-block;">
          <button class="bud-fill-btn" onclick="budToggleFill(${row.id})" title="Fyll alle måneder">⊞</button>
          <span id="fill-pop-${row.id}" style="display:none;position:absolute;left:0;top:calc(100% + 4px);z-index:50;background:var(--surface);border:1px solid var(--border);border-radius:4px;padding:5px 6px;display:none;align-items:center;gap:4px;box-shadow:0 4px 12px rgba(0,0,0,0.1);white-space:nowrap;">
            <input id="fill-input-${row.id}" class="bud-cell-input" style="width:70px;border-bottom-color:var(--border);" placeholder="beløp" onkeydown="if(event.key==='Enter'){budFillRow('${cat.id}',${row.id});}">
            <button class="bud-fill-btn" style="color:var(--green);" onclick="budFillRow('${cat.id}',${row.id})">Fyll →</button>
          </span>
        </span>
        <button class="bud-del-btn" onclick="budRemoveRow('${cat.id}',${row.id})" title="Fjern">×</button>`;
      tr.appendChild(tdName);

      // Drag and drop for row reordering
      tr.draggable = false; // only draggable in edit mode
      tr.dataset.catId = cat.id;
      tr.dataset.rowId = row.id;
      const handle = tdName.querySelector('.bud-drag-handle');
      if (handle) {
        handle.addEventListener('mousedown', () => { if (budEditMode) tr.draggable = true; });
        handle.addEventListener('mouseup', () => { tr.draggable = false; });
      }
      tr.addEventListener('dragstart', e => { if (!budEditMode) { e.preventDefault(); return; } tr.classList.add('bud-dragging'); e.dataTransfer.effectAllowed = 'move'; e.dataTransfer.setData('text/plain', cat.id + '|' + row.id); });
      tr.addEventListener('dragend', () => { tr.classList.remove('bud-dragging'); tr.draggable = false; document.querySelectorAll('.bud-drag-over').forEach(el => el.classList.remove('bud-drag-over')); });
      tr.addEventListener('dragover', e => { e.preventDefault(); tr.classList.add('bud-drag-over'); });
      tr.addEventListener('dragleave', () => tr.classList.remove('bud-drag-over'));
      tr.addEventListener('drop', e => {
        e.preventDefault(); tr.classList.remove('bud-drag-over');
        const [srcCat, srcIdStr] = (e.dataTransfer.getData('text/plain')||'').split('|');
        const srcId = parseFloat(srcIdStr);
        if (srcCat !== cat.id || isNaN(srcId) || srcId === row.id) return;
        const yr = budGetYear();
        const arr = budgetData[yr][cat.id];
        const si = arr.findIndex(r => r.id === srcId);
        const di = arr.findIndex(r => r.id === row.id);
        if (si < 0 || di < 0) return;
        const [moved] = arr.splice(si, 1);
        arr.splice(di, 0, moved);
        saveState(); renderBudget();
      });

      // Month cells
      visMon.forEach(mIdx => {
        const td = document.createElement('td');
        const val = row.amounts[mIdx];
        td.innerHTML = `<input class="bud-cell-input" value="${val > 0 ? Math.round(val).toLocaleString('nb-NO') : ''}" placeholder=""
          onchange="budSetAmount('${cat.id}',${row.id},${mIdx},this.value)"
          onblur="if(this.value){const n=parseRaw(this.value);if(!isNaN(n)&&n>0)this.value=Math.round(n).toLocaleString('nb-NO');else this.value='';}">`;
        tr.appendChild(td);
      });

      // Annual sum cell
      const tdYear = document.createElement('td');
      const rowAnnual = row.amounts.reduce((s,a)=>s+a,0);
      tdYear.textContent = rowAnnual > 0 ? Math.round(rowAnnual).toLocaleString('nb-NO') : '—';
      tdYear.style.color = 'var(--text3)';
      tr.appendChild(tdYear);

      tbody.appendChild(tr);
    });

    // Add row button
    const addRow = document.createElement('tr');
    const addTd = document.createElement('td');
    addTd.colSpan = visMon.length + 2;
    addTd.innerHTML = `<button class="bud-add-btn" onclick="budAddRow('${cat.id}')">+ Legg til rad</button>`;
    addRow.appendChild(addTd);
    tbody.appendChild(addRow);

    // Category total row
    const totals = budCalcCatTotals(year, cat.id);
    catAnnuals[cat.id] = totals.annual;
    catMonthly[cat.id] = totals.monthly;

    const totalRow = document.createElement('tr');
    totalRow.className = 'bud-cat-total';
    const tdTotName = document.createElement('td');
    tdTotName.textContent = 'Sum ' + cat.label.toLowerCase();
    totalRow.appendChild(tdTotName);
    visMon.forEach(mIdx => {
      const td = document.createElement('td');
      const v = totals.monthly[mIdx];
      td.textContent = v > 0 ? Math.round(v).toLocaleString('nb-NO') : '—';
      totalRow.appendChild(td);
    });
    const tdTotYear = document.createElement('td');
    tdTotYear.textContent = totals.annual > 0 ? Math.round(totals.annual).toLocaleString('nb-NO') : '—';
    tdTotYear.style.fontWeight = '500';
    totalRow.appendChild(tdTotYear);
    tbody.appendChild(totalRow);

    // Spacer
    const spacer = document.createElement('tr');
    spacer.innerHTML = `<td colspan="${visMon.length+2}" style="height:8px;background:var(--bg);border:none;"></td>`;
    tbody.appendChild(spacer);
  });

  // ── ZERO BAR (summary cards above table) ──
  const annualLeft = _leftYear;
  const zeroBar = document.getElementById('bud-zero-bar');
  if (zeroBar) {
    const cards = [
      { label: 'Inntekter', val: catAnnuals['inntekter']||0 },
      { label: 'Kostnader', val: catAnnuals['kostnader']||0 },
      { label: 'Sinking funds', val: catAnnuals['sinking']||0 },
      { label: 'Gjeld', val: catAnnuals['gjeld']||0 },
      { label: 'Sparing', val: catAnnuals['sparing']||0 },
    ];
    zeroBar.innerHTML = `<div class="zero-bar">
      <div class="zero-card highlight">
        <div class="zero-card-label">Til fordeling ${year}</div>
        <div class="zero-card-val ${annualLeft>=0?'pos':'neg'}">${Math.round(annualLeft).toLocaleString('nb-NO')} kr</div>
      </div>
      ${cards.map(c=>`
      <div class="zero-card">
        <div class="zero-card-label">${c.label} ${year}</div>
        <div class="zero-card-val" style="color:var(--text2);font-size:0.85rem;">${Math.round(c.val).toLocaleString('nb-NO')} kr</div>
      </div>`).join('')}
    </div>`;
  }
}

// ── STORAGE (localStorage + GitHub) ──
const LS_KEY   = 'spareoversikt_v2';
const GH_OWNER = 'PederMyhrer';
const GH_REPO  = 'PederMyhrer.github.io';
const GH_FILE  = 'data.json';
const GH_TOKEN_KEY = 'gh_token_spareoversikt';

function ghGetToken() { try { return localStorage.getItem(GH_TOKEN_KEY) || ''; } catch(e) { return ''; } }

function ghSaveToken() {
  const val = document.getElementById('gh-token-input').value.trim();
  if (!val) return;
  try { localStorage.setItem(GH_TOKEN_KEY, val); } catch(e) {}
  document.getElementById('gh-token-input').value = '';
  ghInitBar();
  ghPull();
}

function ghInitBar() {
  const token = ghGetToken();
  const pushBtn = document.getElementById('gh-push-btn');
  const pullBtn = document.getElementById('gh-pull-btn');
  const status  = document.getElementById('gh-status');
  const input   = document.getElementById('gh-token-input');
  if (token) {
    if (pushBtn) pushBtn.style.display = 'inline-block';
    if (pullBtn) pullBtn.style.display = 'inline-block';
    if (status)  status.textContent = '✓ Token lagret';
    if (input)   input.placeholder = 'Token er lagret — lim inn nytt for å bytte';
  } else {
    if (pushBtn) pushBtn.style.display = 'none';
    if (pullBtn) pullBtn.style.display = 'none';
    if (status)  status.textContent = 'Ingen token — data lagres kun lokalt';
  }
}

function getState() {
  const inputs = {};
  ['bsu1','bsu2','bsux1','bsux2','spare','bryllup','apr','mai','jun','jul','aug','snitt','egenkap'].forEach(id => {
    const el = document.getElementById(id);
    if (el) inputs[id] = el.value;
  });
  const refill = document.getElementById('refillJun');
  return {
    inputs,
    refillJun: refill ? refill.checked : true,
    queueItems,
    ideas,
    budgetData,
  };
}

function applyState(state) {
  if (!state) return;
  if (state.inputs) {
    Object.entries(state.inputs).forEach(([id, val]) => {
      const el = document.getElementById(id);
      if (el) el.value = val;
    });
  }
  const refill = document.getElementById('refillJun');
  if (refill && state.refillJun !== undefined) refill.checked = state.refillJun;
  if (Array.isArray(state.queueItems)) queueItems = state.queueItems;
  if (Array.isArray(state.ideas)) ideas = state.ideas;
  if (state.budgetData && typeof state.budgetData === 'object') {
    budgetData = state.budgetData;
    Object.keys(budgetData).forEach(year => {
      BUD_CATS.forEach(c => {
        if (!budgetData[year][c.id]) budgetData[year][c.id] = [];
        if (budgetData[year][c.id].length === 0 && BUD_DEFAULTS[c.id]) {
          budgetData[year][c.id] = BUD_DEFAULTS[c.id].map(name => budMakeRow(name));
        }
      });
    });
  }
}

function saveState() {
  const state = getState();
  try { localStorage.setItem(LS_KEY, JSON.stringify(state)); } catch(e) {}
}

function loadState() {
  let state;
  try { state = JSON.parse(localStorage.getItem(LS_KEY)); } catch(e) {}
  applyState(state);
}

// ── GITHUB SYNC ──
let ghFileSha = null;

async function ghPull() {
  const token = ghGetToken();
  if (!token) return;
  const status = document.getElementById('gh-status');
  if (status) status.textContent = '⏳ Henter...';
  try {
    const res = await fetch(
      `https://api.github.com/repos/${GH_OWNER}/${GH_REPO}/contents/${GH_FILE}`,
      { headers: { Authorization: 'token ' + token, Accept: 'application/vnd.github.v3+json' } }
    );
    if (res.status === 404) {
      // File doesn't exist yet — that's fine, use local state
      if (status) status.textContent = 'ℹ Ingen skydata ennå — lagre for å opprette';
      return;
    }
    if (!res.ok) throw new Error('HTTP ' + res.status);
    const json = await res.json();
    ghFileSha = json.sha;
    const data = JSON.parse(atob(json.content.replace(/\n/g, '')));
    applyState(data);
    saveState(); // sync to localStorage too
    // Re-render everything
    calc(); renderQueue(); renderIdeas(); if (document.getElementById('tab-budsjett').classList.contains('active')) renderBudget();
    if (status) status.textContent = '✓ Hentet ' + new Date().toLocaleTimeString('nb-NO', {hour:'2-digit',minute:'2-digit'});
  } catch(e) {
    if (status) status.textContent = '⚠ Feil: ' + e.message;
  }
}

async function ghPush() {
  const token = ghGetToken();
  if (!token) return;
  const status = document.getElementById('gh-status');
  if (status) status.textContent = '⏳ Lagrer...';
  try {
    const state = getState();
    const encoded = btoa(unescape(encodeURIComponent(JSON.stringify(state, null, 2))));
    const body = { message: 'Oppdater data', content: encoded };
    if (ghFileSha) body.sha = ghFileSha;
    const res = await fetch(
      `https://api.github.com/repos/${GH_OWNER}/${GH_REPO}/contents/${GH_FILE}`,
      { method: 'PUT', headers: { Authorization: 'token ' + token, Accept: 'application/vnd.github.v3+json', 'Content-Type': 'application/json' }, body: JSON.stringify(body) }
    );
    if (!res.ok) throw new Error('HTTP ' + res.status);
    const json = await res.json();
    ghFileSha = json.content.sha;
    saveState();
    if (status) status.textContent = '✓ Lagret ' + new Date().toLocaleTimeString('nb-NO', {hour:'2-digit',minute:'2-digit'});
  } catch(e) {
    if (status) status.textContent = '⚠ Feil: ' + e.message;
  }
}

// Load state, then init
loadState();
ghInitBar();
calc();
renderQueue();
renderIdeas();
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js" onload="updateCapitalChart()"></script>
</body>
</html>
