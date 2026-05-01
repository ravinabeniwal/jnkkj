<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EduCore — Student Management System</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,300&family=Fraunces:opsz,wght@9..144,300;9..144,400;9..144,600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #f7f5f0;
    --surface: #ffffff;
    --surface2: #f0ede6;
    --border: rgba(60,52,40,0.1);
    --border-med: rgba(60,52,40,0.18);
    --text: #1a1612;
    --text-muted: #7a6f62;
    --text-hint: #a89e92;
    --accent: #2d5a3d;
    --accent-light: #e8f0eb;
    --accent2: #b85c2a;
    --accent2-light: #faf0ea;
    --blue: #1e4a8c;
    --blue-light: #e8eff9;
    --amber: #9a6b0a;
    --amber-light: #fdf5e0;
    --sidebar-w: 240px;
    --radius: 12px;
    --radius-sm: 8px;
    --shadow: 0 1px 3px rgba(0,0,0,0.06), 0 4px 16px rgba(0,0,0,0.04);
  }

  [data-theme="dark"] {
    --bg: #111410;
    --surface: #1c1f18;
    --surface2: #252820;
    --border: rgba(255,255,255,0.08);
    --border-med: rgba(255,255,255,0.14);
    --text: #ede8df;
    --text-muted: #8a8278;
    --text-hint: #5a544e;
    --accent: #4a8f62;
    --accent-light: #162318;
    --accent2: #d4724a;
    --accent2-light: #1e1208;
    --blue: #4a7cc9;
    --blue-light: #0e1a2e;
    --amber: #c9932a;
    --amber-light: #1e1500;
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    overflow: hidden;
    font-size: 14px;
    line-height: 1.6;
    transition: background 0.3s, color 0.3s;
  }

  /* SIDEBAR */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--surface);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    height: 100vh;
    position: fixed;
    left: 0; top: 0;
    z-index: 100;
    transition: transform 0.3s ease;
  }

  .sidebar-logo {
    padding: 24px 20px 20px;
    border-bottom: 1px solid var(--border);
  }
  .logo-mark {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .logo-icon {
    width: 36px; height: 36px;
    background: var(--accent);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
  }
  .logo-icon svg { width: 20px; height: 20px; }
  .logo-text {
    font-family: 'Fraunces', serif;
    font-size: 18px;
    font-weight: 600;
    color: var(--text);
    letter-spacing: -0.3px;
  }
  .logo-text span { color: var(--accent); }

  .nav-section { padding: 12px 12px 0; }
  .nav-label {
    font-size: 11px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--text-hint);
    padding: 8px 8px 6px;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 9px 10px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    color: var(--text-muted);
    font-size: 13.5px;
    font-weight: 400;
    transition: all 0.15s;
    margin-bottom: 2px;
    user-select: none;
  }
  .nav-item:hover { background: var(--surface2); color: var(--text); }
  .nav-item.active {
    background: var(--accent-light);
    color: var(--accent);
    font-weight: 500;
  }
  .nav-item svg { width: 16px; height: 16px; opacity: 0.8; flex-shrink: 0; }
  .nav-item.active svg { opacity: 1; }
  .nav-badge {
    margin-left: auto;
    background: var(--accent2);
    color: white;
    font-size: 10px;
    font-weight: 600;
    padding: 1px 6px;
    border-radius: 20px;
  }

  .sidebar-footer {
    margin-top: auto;
    padding: 16px 12px;
    border-top: 1px solid var(--border);
  }
  .user-chip {
    display: flex; align-items: center; gap: 10px;
    padding: 8px;
    border-radius: var(--radius-sm);
    cursor: pointer;
  }
  .user-chip:hover { background: var(--surface2); }
  .avatar {
    width: 32px; height: 32px;
    border-radius: 50%;
    background: var(--accent);
    display: flex; align-items: center; justify-content: center;
    font-size: 12px; font-weight: 600; color: white;
    flex-shrink: 0;
  }
  .user-name { font-size: 13px; font-weight: 500; }
  .user-role { font-size: 11px; color: var(--text-muted); }

  /* MAIN */
  .main {
    margin-left: var(--sidebar-w);
    flex: 1;
    height: 100vh;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
  }

  /* TOPBAR */
  .topbar {
    background: var(--surface);
    border-bottom: 1px solid var(--border);
    padding: 0 28px;
    height: 60px;
    display: flex;
    align-items: center;
    gap: 16px;
    position: sticky;
    top: 0;
    z-index: 50;
  }
  .page-title {
    font-family: 'Fraunces', serif;
    font-size: 20px;
    font-weight: 400;
    color: var(--text);
    flex: 1;
  }
  .search-bar {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 24px;
    padding: 7px 14px;
    width: 240px;
    transition: all 0.2s;
  }
  .search-bar:focus-within {
    border-color: var(--accent);
    width: 280px;
  }
  .search-bar svg { width: 14px; height: 14px; color: var(--text-muted); flex-shrink: 0; }
  .search-bar input {
    border: none; background: transparent;
    font-family: inherit; font-size: 13px;
    color: var(--text); outline: none; flex: 1;
  }
  .search-bar input::placeholder { color: var(--text-hint); }

  .icon-btn {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: var(--surface2);
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer;
    transition: all 0.15s;
    flex-shrink: 0;
  }
  .icon-btn:hover { background: var(--border); transform: scale(1.05); }
  .icon-btn svg { width: 16px; height: 16px; }
  .notif-dot {
    width: 8px; height: 8px;
    background: var(--accent2);
    border-radius: 50%;
    position: absolute;
    top: 6px; right: 6px;
    border: 2px solid var(--surface);
  }
  .rel { position: relative; }

  /* CONTENT */
  .content {
    padding: 28px;
    flex: 1;
  }

  /* PANELS */
  .panel { display: none; }
  .panel.active { display: block; }

  /* STATS GRID */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 24px;
  }
  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
    cursor: default;
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .stat-card:hover { transform: translateY(-2px); box-shadow: var(--shadow); }
  .stat-top { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 12px; }
  .stat-icon {
    width: 40px; height: 40px;
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
  }
  .stat-icon svg { width: 18px; height: 18px; }
  .stat-icon.green { background: var(--accent-light); color: var(--accent); }
  .stat-icon.orange { background: var(--accent2-light); color: var(--accent2); }
  .stat-icon.blue { background: var(--blue-light); color: var(--blue); }
  .stat-icon.amber { background: var(--amber-light); color: var(--amber); }
  .stat-delta {
    font-size: 11px;
    padding: 3px 8px;
    border-radius: 20px;
    font-weight: 500;
  }
  .stat-delta.up { background: var(--accent-light); color: var(--accent); }
  .stat-delta.down { background: #fff0f0; color: #c0392b; }
  [data-theme="dark"] .stat-delta.down { background: #1e0a0a; color: #e07070; }
  .stat-value {
    font-family: 'Fraunces', serif;
    font-size: 30px;
    font-weight: 400;
    line-height: 1;
    color: var(--text);
    margin-bottom: 4px;
  }
  .stat-label { font-size: 12.5px; color: var(--text-muted); }

  /* GRID 2-COL */
  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px; }
  .grid-3-1 { display: grid; grid-template-columns: 2fr 1fr; gap: 20px; margin-bottom: 20px; }

  /* CARD */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
  }
  .card-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 18px; }
  .card-title { font-size: 14px; font-weight: 500; color: var(--text); }
  .card-action { font-size: 12px; color: var(--accent); cursor: pointer; font-weight: 500; }
  .card-action:hover { text-decoration: underline; }

  /* CHART AREA */
  .chart-wrap { position: relative; height: 180px; }

  /* ATTENDANCE BAR CHART */
  .bar-chart { display: flex; align-items: flex-end; gap: 8px; height: 140px; padding-top: 10px; }
  .bar-col { display: flex; flex-direction: column; align-items: center; gap: 6px; flex: 1; }
  .bar {
    width: 100%;
    background: var(--accent-light);
    border-radius: 4px 4px 0 0;
    transition: background 0.2s;
    cursor: pointer;
    position: relative;
    min-height: 4px;
  }
  .bar:hover { background: var(--accent); }
  .bar.highlight { background: var(--accent); }
  .bar-label { font-size: 10.5px; color: var(--text-hint); }
  .bar-val { font-size: 10px; color: var(--text-muted); font-weight: 500; }

  /* DONUT CHART (CSS) */
  .donut-wrap { display: flex; align-items: center; gap: 24px; }
  .donut {
    width: 100px; height: 100px;
    border-radius: 50%;
    background: conic-gradient(
      var(--accent) 0% 78%,
      var(--accent2) 78% 90%,
      var(--blue) 90% 97%,
      var(--border) 97% 100%
    );
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .donut-hole {
    width: 64px; height: 64px;
    background: var(--surface);
    border-radius: 50%;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
  }
  .donut-pct { font-size: 16px; font-weight: 600; color: var(--text); }
  .donut-sub { font-size: 9px; color: var(--text-muted); }
  .legend { display: flex; flex-direction: column; gap: 8px; }
  .legend-item { display: flex; align-items: center; gap: 8px; font-size: 12.5px; color: var(--text-muted); }
  .legend-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }

  /* RECENT STUDENTS TABLE */
  .table-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; }
  th {
    text-align: left;
    font-size: 11px;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-hint);
    padding: 0 12px 12px;
    border-bottom: 1px solid var(--border);
  }
  td {
    padding: 12px;
    font-size: 13.5px;
    color: var(--text);
    border-bottom: 1px solid var(--border);
    vertical-align: middle;
  }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: var(--surface2); }
  .student-cell { display: flex; align-items: center; gap: 10px; }
  .stu-avatar {
    width: 30px; height: 30px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 11px; font-weight: 600; color: white;
    flex-shrink: 0;
  }

  /* BADGES */
  .badge {
    display: inline-flex; align-items: center;
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 11.5px;
    font-weight: 500;
  }
  .badge-green { background: var(--accent-light); color: var(--accent); }
  .badge-amber { background: var(--amber-light); color: var(--amber); }
  .badge-red { background: #fff0f0; color: #c0392b; }
  [data-theme="dark"] .badge-red { background: #1e0a0a; color: #e07070; }
  .badge-blue { background: var(--blue-light); color: var(--blue); }
  .badge-gray { background: var(--surface2); color: var(--text-muted); }

  /* PROGRESS */
  .progress-wrap { display: flex; align-items: center; gap: 10px; }
  .progress-bar { flex: 1; height: 6px; background: var(--surface2); border-radius: 3px; overflow: hidden; }
  .progress-fill { height: 100%; border-radius: 3px; }
  .progress-val { font-size: 12px; color: var(--text-muted); min-width: 36px; text-align: right; }

  /* ANNOUNCEMENTS */
  .announce-item { padding: 14px 0; border-bottom: 1px solid var(--border); }
  .announce-item:last-child { border-bottom: none; }
  .announce-top { display: flex; align-items: flex-start; gap: 12px; }
  .announce-icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .announce-icon svg { width: 14px; height: 14px; }
  .announce-title { font-size: 13.5px; font-weight: 500; margin-bottom: 2px; }
  .announce-meta { font-size: 12px; color: var(--text-muted); }

  /* BUTTONS */
  .btn {
    display: inline-flex; align-items: center; gap: 6px;
    padding: 8px 16px;
    border-radius: var(--radius-sm);
    font-family: inherit;
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.15s;
    border: none;
  }
  .btn svg { width: 14px; height: 14px; }
  .btn-primary { background: var(--accent); color: white; }
  .btn-primary:hover { background: #244d35; transform: translateY(-1px); }
  .btn-secondary { background: var(--surface2); color: var(--text); border: 1px solid var(--border); }
  .btn-secondary:hover { background: var(--border); }
  .btn-sm { padding: 5px 12px; font-size: 12px; }

  /* STUDENTS PAGE */
  .filters-row { display: flex; align-items: center; gap: 10px; margin-bottom: 18px; flex-wrap: wrap; }
  .filter-chip {
    padding: 5px 14px;
    border-radius: 20px;
    border: 1px solid var(--border);
    background: var(--surface);
    font-size: 12.5px;
    cursor: pointer;
    color: var(--text-muted);
    transition: all 0.15s;
  }
  .filter-chip:hover, .filter-chip.active { background: var(--accent-light); color: var(--accent); border-color: var(--accent); }
  select.filter-select {
    padding: 5px 12px;
    border-radius: var(--radius-sm);
    border: 1px solid var(--border);
    background: var(--surface);
    font-family: inherit;
    font-size: 12.5px;
    color: var(--text);
    outline: none;
    cursor: pointer;
  }

  /* GRID STUDENTS */
  .students-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 16px; margin-bottom: 24px; }
  .stu-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 20px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
  }
  .stu-card:hover { transform: translateY(-3px); box-shadow: var(--shadow); border-color: var(--accent); }
  .stu-card-avatar {
    width: 52px; height: 52px;
    border-radius: 50%;
    margin: 0 auto 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px; font-weight: 600; color: white;
  }
  .stu-card-name { font-size: 14px; font-weight: 500; margin-bottom: 2px; }
  .stu-card-id { font-size: 12px; color: var(--text-muted); margin-bottom: 10px; }
  .stu-card-stats { display: flex; justify-content: center; gap: 16px; }
  .stu-stat { font-size: 11px; color: var(--text-muted); text-align: center; }
  .stu-stat strong { display: block; font-size: 13px; font-weight: 600; color: var(--text); }

  /* ATTENDANCE PAGE */
  .att-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 8px; margin-bottom: 20px; }
  .att-day-header { text-align: center; font-size: 11px; font-weight: 600; text-transform: uppercase; color: var(--text-hint); padding: 8px 0; }
  .att-cell {
    aspect-ratio: 1;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.15s;
    border: 1px solid var(--border);
    background: var(--surface);
  }
  .att-cell.present { background: var(--accent-light); color: var(--accent); border-color: var(--accent); font-weight: 600; }
  .att-cell.absent { background: #fff0f0; color: #c0392b; border-color: #e0a0a0; font-weight: 600; }
  [data-theme="dark"] .att-cell.absent { background: #1e0a0a; color: #e07070; border-color: #5a2020; }
  .att-cell.today { box-shadow: 0 0 0 2px var(--accent); }
  .att-cell.empty { background: transparent; border-color: transparent; cursor: default; }

  /* PERFORMANCE PAGE */
  .grades-table td:first-child { font-weight: 500; }
  .grade-bar-wrap { display: flex; align-items: center; gap: 8px; }
  .grade-fill { height: 8px; border-radius: 4px; }

  /* MODAL */
  .modal-backdrop {
    position: fixed; inset: 0;
    background: rgba(0,0,0,0.4);
    z-index: 200;
    display: flex; align-items: center; justify-content: center;
    opacity: 0; pointer-events: none;
    transition: opacity 0.2s;
  }
  .modal-backdrop.open { opacity: 1; pointer-events: all; }
  .modal {
    background: var(--surface);
    border-radius: 16px;
    padding: 28px;
    width: 480px;
    max-width: 90vw;
    transform: translateY(12px) scale(0.98);
    transition: transform 0.25s;
    border: 1px solid var(--border);
  }
  .modal-backdrop.open .modal { transform: translateY(0) scale(1); }
  .modal-title { font-family: 'Fraunces', serif; font-size: 20px; margin-bottom: 20px; color: var(--text); }
  .form-group { margin-bottom: 16px; }
  .form-label { font-size: 12px; font-weight: 500; color: var(--text-muted); margin-bottom: 6px; display: block; }
  .form-input {
    width: 100%; padding: 9px 12px;
    border: 1px solid var(--border-med);
    border-radius: var(--radius-sm);
    background: var(--surface2);
    font-family: inherit; font-size: 13.5px;
    color: var(--text); outline: none;
    transition: border-color 0.15s;
  }
  .form-input:focus { border-color: var(--accent); }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .modal-actions { display: flex; gap: 10px; justify-content: flex-end; margin-top: 20px; }

  /* NOTIFICATIONS */
  .notif-dropdown {
    position: absolute; top: 50px; right: 0;
    width: 320px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    box-shadow: 0 8px 32px rgba(0,0,0,0.12);
    z-index: 300;
    display: none;
  }
  .notif-dropdown.open { display: block; }
  .notif-head { padding: 14px 16px; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; }
  .notif-head span { font-weight: 500; font-size: 14px; }
  .notif-item { padding: 12px 16px; border-bottom: 1px solid var(--border); cursor: pointer; }
  .notif-item:last-child { border-bottom: none; }
  .notif-item:hover { background: var(--surface2); }
  .notif-item p { font-size: 13px; color: var(--text); margin-bottom: 2px; }
  .notif-item span { font-size: 11px; color: var(--text-muted); }
  .notif-item.unread { border-left: 3px solid var(--accent); }

  /* THEME TOGGLE */
  .theme-toggle-wrap {
    display: flex; align-items: center; gap: 6px;
    font-size: 12px; color: var(--text-muted);
  }
  .toggle-switch {
    width: 34px; height: 18px;
    background: var(--border-med);
    border-radius: 9px;
    position: relative;
    cursor: pointer;
    transition: background 0.2s;
  }
  .toggle-switch.on { background: var(--accent); }
  .toggle-knob {
    width: 14px; height: 14px;
    background: white;
    border-radius: 50%;
    position: absolute;
    top: 2px; left: 2px;
    transition: left 0.2s;
    box-shadow: 0 1px 3px rgba(0,0,0,0.2);
  }
  .toggle-switch.on .toggle-knob { left: 18px; }

  /* RESPONSIVE */
  @media (max-width: 1100px) {
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
    .grid-2 { grid-template-columns: 1fr; }
    .grid-3-1 { grid-template-columns: 1fr; }
  }
  @media (max-width: 768px) {
    :root { --sidebar-w: 0px; }
    .sidebar { transform: translateX(-240px); }
    .sidebar.open { transform: translateX(0); --sidebar-w: 240px; }
    .stats-grid { grid-template-columns: 1fr 1fr; }
    .search-bar { width: 160px; }
    .content { padding: 16px; }
  }

  /* MINI LINE CHART (SVG) */
  .sparkline { width: 100%; height: 60px; }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border-med); border-radius: 3px; }

  /* ANIMATION */
  @keyframes slideIn { from { opacity:0; transform: translateY(8px); } to { opacity:1; transform: translateY(0); } }
  .panel.active { animation: slideIn 0.25s ease; }
  @keyframes countUp { from { opacity:0; transform: scale(0.8); } to { opacity:1; transform: scale(1); } }
  .stat-value { animation: countUp 0.4s ease; }
</style>
</head>
<body>

<!-- SIDEBAR -->
<aside class="sidebar" id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-mark">
      <div class="logo-icon">
        <svg fill="none" viewBox="0 0 24 24" stroke="white" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 14l9-5-9-5-9 5 9 5z"/>
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z"/>
        </svg>
      </div>
      <span class="logo-text">Edu<span>Core</span></span>
    </div>
  </div>

  <div class="nav-section">
    <div class="nav-label">Main</div>
    <div class="nav-item active" onclick="navigate('dashboard', this)">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Dashboard
    </div>
    <div class="nav-item" onclick="navigate('students', this)">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0"/></svg>
      Students
      <span class="nav-badge">1,284</span>
    </div>
    <div class="nav-item" onclick="navigate('attendance', this)">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>
      Attendance
    </div>
    <div class="nav-item" onclick="navigate('performance', this)">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/></svg>
      Performance
    </div>
  </div>

  <div class="nav-section">
    <div class="nav-label">Management</div>
    <div class="nav-item" onclick="navigate('communication', this)">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/></svg>
      Communication
      <span class="nav-badge">3</span>
    </div>
    <div class="nav-item">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/><circle cx="12" cy="12" r="3"/></svg>
      Settings
    </div>
  </div>

  <div class="sidebar-footer">
    <div class="theme-toggle-wrap" style="padding: 0 8px 12px;">
      <svg width="14" height="14" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="5"/><path stroke-linecap="round" d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/></svg>
      <span style="flex:1; font-size:12px; color:var(--text-muted);">Dark mode</span>
      <div class="toggle-switch" id="themeToggle" onclick="toggleTheme()"><div class="toggle-knob"></div></div>
    </div>
    <div class="user-chip">
      <div class="avatar">AD</div>
      <div>
        <div class="user-name">Admin User</div>
        <div class="user-role">Administrator</div>
      </div>
    </div>
  </div>
</aside>

<!-- MAIN -->
<main class="main">
  <!-- TOPBAR -->
  <header class="topbar">
    <h1 class="page-title" id="pageTitle">Dashboard</h1>
    <div class="search-bar">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path stroke-linecap="round" d="m21 21-4.35-4.35"/></svg>
      <input placeholder="Search students, classes..." id="globalSearch">
    </div>
    <div class="rel">
      <div class="icon-btn" onclick="toggleNotif()">
        <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path stroke-linecap="round" stroke-linejoin="round" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"/></svg>
        <div class="notif-dot"></div>
      </div>
      <div class="notif-dropdown" id="notifDropdown">
        <div class="notif-head"><span>Notifications</span><span style="font-size:12px; color:var(--accent); cursor:pointer;">Mark all read</span></div>
        <div class="notif-item unread"><p>Exam results uploaded for Grade 10</p><span>2 minutes ago</span></div>
        <div class="notif-item unread"><p>3 students marked absent today</p><span>1 hour ago</span></div>
        <div class="notif-item unread"><p>New announcement from Principal</p><span>3 hours ago</span></div>
        <div class="notif-item"><p>Report cards generated for Term 2</p><span>Yesterday</span></div>
      </div>
    </div>
    <button class="btn btn-primary" onclick="openModal()">
      <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/></svg>
      Add Student
    </button>
  </header>

  <!-- CONTENT -->
  <div class="content">

    <!-- DASHBOARD PANEL -->
    <div class="panel active" id="panel-dashboard">
      <!-- STATS -->
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon green">
              <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0"/></svg>
            </div>
            <span class="stat-delta up">+4.2%</span>
          </div>
          <div class="stat-value">1,284</div>
          <div class="stat-label">Total Students</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon blue">
              <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/></svg>
            </div>
            <span class="stat-delta up">+1.8%</span>
          </div>
          <div class="stat-value">91.4%</div>
          <div class="stat-label">Avg Attendance</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon amber">
              <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"/></svg>
            </div>
            <span class="stat-delta up">+2.3%</span>
          </div>
          <div class="stat-value">78.6</div>
          <div class="stat-label">Avg Score</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon orange">
              <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M12 14l9-5-9-5-9 5 9 5z"/><path d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z"/></svg>
            </div>
            <span class="stat-delta down">-2</span>
          </div>
          <div class="stat-value">42</div>
          <div class="stat-label">Active Classes</div>
        </div>
      </div>

      <div class="grid-3-1">
        <!-- ATTENDANCE CHART -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">Weekly Attendance — May 2025</span>
            <span class="card-action" onclick="navigate('attendance', document.querySelector('[onclick*=attendance]'))">View all</span>
          </div>
          <div class="bar-chart" id="attChart">
            <!-- JS fills this -->
          </div>
          <div style="display:flex; justify-content:space-between; margin-top:10px; padding: 0 4px;">
            <span style="font-size:11px; color:var(--text-hint);">Mon</span>
            <span style="font-size:11px; color:var(--text-hint);">Tue</span>
            <span style="font-size:11px; color:var(--text-hint);">Wed</span>
            <span style="font-size:11px; color:var(--text-hint);">Thu</span>
            <span style="font-size:11px; color:var(--text-hint);">Fri</span>
          </div>
        </div>

        <!-- GRADE DIST -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">Grade Distribution</span>
          </div>
          <div class="donut-wrap">
            <div class="donut">
              <div class="donut-hole">
                <span class="donut-pct">78%</span>
                <span class="donut-sub">Pass rate</span>
              </div>
            </div>
            <div class="legend">
              <div class="legend-item"><div class="legend-dot" style="background:var(--accent)"></div>Excellent (A)</div>
              <div class="legend-item"><div class="legend-dot" style="background:var(--accent2)"></div>Good (B)</div>
              <div class="legend-item"><div class="legend-dot" style="background:var(--blue)"></div>Average (C)</div>
              <div class="legend-item"><div class="legend-dot" style="background:var(--border-med)"></div>Needs Work</div>
            </div>
          </div>
        </div>
      </div>

      <div class="grid-2">
        <!-- RECENT STUDENTS -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">Recent Students</span>
            <span class="card-action" onclick="navigate('students', document.querySelector('[onclick*=students]'))">See all</span>
          </div>
          <div class="table-wrap">
            <table>
              <thead>
                <tr><th>Student</th><th>Grade</th><th>Attendance</th><th>Status</th></tr>
              </thead>
              <tbody id="dashStudentRows"></tbody>
            </table>
          </div>
        </div>

        <!-- ANNOUNCEMENTS -->
        <div class="card">
          <div class="card-header">
            <span class="card-title">Announcements</span>
            <span class="card-action" onclick="navigate('communication', document.querySelector('[onclick*=communication]'))">Post new</span>
          </div>
          <div class="announce-item">
            <div class="announce-top">
              <div class="announce-icon" style="background:var(--accent-light)">
                <svg fill="none" viewBox="0 0 24 24" stroke="var(--accent)" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z"/></svg>
              </div>
              <div>
                <div class="announce-title">Mid-term exams scheduled</div>
                <div class="announce-meta">Principal's Office · May 10, 2025</div>
              </div>
            </div>
          </div>
          <div class="announce-item">
            <div class="announce-top">
              <div class="announce-icon" style="background:var(--amber-light)">
                <svg fill="none" viewBox="0 0 24 24" stroke="var(--amber)" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>
              </div>
              <div>
                <div class="announce-title">Library closure — maintenance</div>
                <div class="announce-meta">Facilities · May 8, 2025</div>
              </div>
            </div>
          </div>
          <div class="announce-item">
            <div class="announce-top">
              <div class="announce-icon" style="background:var(--blue-light)">
                <svg fill="none" viewBox="0 0 24 24" stroke="var(--blue)" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4"/></svg>
              </div>
              <div>
                <div class="announce-title">Term 2 report cards ready</div>
                <div class="announce-meta">Academic Office · May 5, 2025</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- TOP PERFORMERS -->
      <div class="card">
        <div class="card-header">
          <span class="card-title">Subject Performance Overview</span>
          <span class="card-action">Export CSV</span>
        </div>
        <div id="subjectBars"></div>
      </div>
    </div>

    <!-- STUDENTS PANEL -->
    <div class="panel" id="panel-students">
      <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:20px;">
        <div>
          <h2 style="font-family:'Fraunces',serif; font-size:22px; font-weight:400; margin-bottom:4px;">Student Directory</h2>
          <p style="font-size:13px; color:var(--text-muted);">1,284 enrolled students across all grades</p>
        </div>
        <div style="display:flex; gap:8px;">
          <button class="btn btn-secondary btn-sm">
            <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"/></svg>
            Export
          </button>
          <button class="btn btn-primary btn-sm" onclick="openModal()">
            <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" d="M12 4v16m8-8H4"/></svg>
            Add Student
          </button>
        </div>
      </div>
      <div class="filters-row">
        <div class="filter-chip active">All</div>
        <div class="filter-chip">Grade 9</div>
        <div class="filter-chip">Grade 10</div>
        <div class="filter-chip">Grade 11</div>
        <div class="filter-chip">Grade 12</div>
        <select class="filter-select">
          <option>Sort: Name A–Z</option>
          <option>Sort: Grade</option>
          <option>Sort: Attendance</option>
          <option>Sort: Score</option>
        </select>
      </div>
      <div class="students-grid" id="studentsGrid"></div>
    </div>

    <!-- ATTENDANCE PANEL -->
    <div class="panel" id="panel-attendance">
      <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:20px;">
        <div>
          <h2 style="font-family:'Fraunces',serif; font-size:22px; font-weight:400; margin-bottom:4px;">Attendance Tracker</h2>
          <p style="font-size:13px; color:var(--text-muted);">May 2025 — Click a date to mark attendance</p>
        </div>
        <div style="display:flex; gap:8px;">
          <button class="btn btn-secondary btn-sm">← April</button>
          <button class="btn btn-secondary btn-sm">June →</button>
        </div>
      </div>
      <div class="grid-2" style="margin-bottom:20px;">
        <div class="card">
          <div class="card-header"><span class="card-title">May 2025 Calendar</span></div>
          <div style="display:grid; grid-template-columns:repeat(7,1fr); gap:4px; margin-bottom:8px;">
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">S</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">M</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">T</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">W</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">T</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">F</div>
            <div style="text-align:center;font-size:11px;color:var(--text-hint);padding:4px;">S</div>
          </div>
          <div id="calGrid" style="display:grid; grid-template-columns:repeat(7,1fr); gap:4px;"></div>
          <div style="display:flex; gap:12px; margin-top:14px; flex-wrap:wrap;">
            <div style="display:flex;align-items:center;gap:6px;font-size:12px;color:var(--text-muted)"><div style="width:10px;height:10px;border-radius:2px;background:var(--accent-light);border:1px solid var(--accent)"></div>Present</div>
            <div style="display:flex;align-items:center;gap:6px;font-size:12px;color:var(--text-muted)"><div style="width:10px;height:10px;border-radius:2px;background:#fff0f0;border:1px solid #e0a0a0"></div>Absent</div>
            <div style="display:flex;align-items:center;gap:6px;font-size:12px;color:var(--text-muted)"><div style="width:10px;height:10px;border-radius:2px;background:var(--surface2);border:1px solid var(--border)"></div>Weekend</div>
          </div>
        </div>
        <div class="card">
          <div class="card-header"><span class="card-title">Monthly Summary</span></div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px;">
            <div style="background:var(--surface2);padding:14px;border-radius:var(--radius-sm);text-align:center;">
              <div style="font-family:'Fraunces',serif;font-size:28px;font-weight:400;color:var(--accent)">91.4%</div>
              <div style="font-size:12px;color:var(--text-muted)">Avg Attendance</div>
            </div>
            <div style="background:var(--surface2);padding:14px;border-radius:var(--radius-sm);text-align:center;">
              <div style="font-family:'Fraunces',serif;font-size:28px;font-weight:400;color:var(--accent2)">87</div>
              <div style="font-size:12px;color:var(--text-muted)">Absent Today</div>
            </div>
          </div>
          <div id="attStudentList"></div>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><span class="card-title">Class-wise Attendance</span><span class="card-action">Generate Report</span></div>
        <table>
          <thead><tr><th>Class</th><th>Total Students</th><th>Present</th><th>Absent</th><th>Rate</th><th>Status</th></tr></thead>
          <tbody id="classAttTable"></tbody>
        </table>
      </div>
    </div>

    <!-- PERFORMANCE PANEL -->
    <div class="panel" id="panel-performance">
      <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:20px;">
        <div>
          <h2 style="font-family:'Fraunces',serif; font-size:22px; font-weight:400; margin-bottom:4px;">Academic Performance</h2>
          <p style="font-size:13px; color:var(--text-muted);">Term 2 · May 2025</p>
        </div>
        <div style="display:flex; gap:8px;">
          <select class="filter-select">
            <option>All Grades</option>
            <option>Grade 9</option>
            <option>Grade 10</option>
            <option>Grade 11</option>
            <option>Grade 12</option>
          </select>
          <button class="btn btn-primary btn-sm">
            <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/></svg>
            Report Card
          </button>
        </div>
      </div>
      <div class="stats-grid" style="grid-template-columns:repeat(4,1fr);">
        <div class="stat-card">
          <div class="stat-top"><div class="stat-icon green"><svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/></svg></div><span class="stat-delta up">+3%</span></div>
          <div class="stat-value">78.6</div><div class="stat-label">Class Average</div>
        </div>
        <div class="stat-card">
          <div class="stat-top"><div class="stat-icon amber"><svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"/></svg></div><span class="stat-delta up">+5</span></div>
          <div class="stat-value">247</div><div class="stat-label">A-grade Students</div>
        </div>
        <div class="stat-card">
          <div class="stat-top"><div class="stat-icon blue"><svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"/></svg></div><span class="stat-delta up">+2.4</span></div>
          <div class="stat-value">94.2</div><div class="stat-label">Top Score</div>
        </div>
        <div class="stat-card">
          <div class="stat-top"><div class="stat-icon orange"><svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.8"><path d="M12 9v2m0 4h.01M5.07 19H19a2 2 0 001.75-2.97L13.75 5a2 2 0 00-3.5 0L3.25 16.03A2 2 0 005.07 19z"/></svg></div><span class="stat-delta down">-2</span></div>
          <div class="stat-value">38</div><div class="stat-label">At Risk</div>
        </div>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-header"><span class="card-title">Subject-wise Averages</span></div>
          <div id="perfSubjectBars"></div>
        </div>
        <div class="card">
          <div class="card-header"><span class="card-title">Top 5 Performers</span></div>
          <div id="topPerformers"></div>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><span class="card-title">Grade Distribution</span></div>
        <table class="grades-table">
          <thead><tr><th>Student</th><th>Math</th><th>Science</th><th>English</th><th>History</th><th>Overall</th><th>Grade</th></tr></thead>
          <tbody id="gradesTableBody"></tbody>
        </table>
      </div>
    </div>

    <!-- COMMUNICATION PANEL -->
    <div class="panel" id="panel-communication">
      <div style="display:flex; align-items:center; justify-content:space-between; margin-bottom:20px;">
        <div>
          <h2 style="font-family:'Fraunces',serif; font-size:22px; font-weight:400; margin-bottom:4px;">Communication Hub</h2>
          <p style="font-size:13px; color:var(--text-muted);">Announcements and messages</p>
        </div>
        <button class="btn btn-primary btn-sm" onclick="openAnnounceModal()">
          <svg fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" d="M12 4v16m8-8H4"/></svg>
          New Announcement
        </button>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-header"><span class="card-title">Recent Announcements</span></div>
          <div id="announceList"></div>
        </div>
        <div class="card">
          <div class="card-header"><span class="card-title">Quick Message</span></div>
          <div class="form-group"><label class="form-label">To</label><input class="form-input" placeholder="Search student or class..."></div>
          <div class="form-group"><label class="form-label">Message</label><textarea class="form-input" rows="4" placeholder="Type your message..."></textarea></div>
          <div style="display:flex; gap:8px; margin-top:8px;">
            <button class="btn btn-primary" style="flex:1;">Send Message</button>
          </div>
        </div>
      </div>
    </div>

  </div>
</main>

<!-- ADD STUDENT MODAL -->
<div class="modal-backdrop" id="modalBackdrop" onclick="closeModal(event)">
  <div class="modal" onclick="event.stopPropagation()">
    <div class="modal-title">Add New Student</div>
    <div class="form-row">
      <div class="form-group"><label class="form-label">First Name</label><input class="form-input" placeholder="e.g. Sarah" id="fName"></div>
      <div class="form-group"><label class="form-label">Last Name</label><input class="form-input" placeholder="e.g. Johnson" id="lName"></div>
    </div>
    <div class="form-row">
      <div class="form-group"><label class="form-label">Grade</label>
        <select class="form-input" id="grade">
          <option>Grade 9</option><option>Grade 10</option><option>Grade 11</option><option>Grade 12</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Date of Birth</label><input type="date" class="form-input" id="dob"></div>
    </div>
    <div class="form-group"><label class="form-label">Email</label><input class="form-input" placeholder="student@school.edu" id="email"></div>
    <div class="form-group"><label class="form-label">Parent/Guardian Contact</label><input class="form-input" placeholder="+1 (555) 000-0000" id="phone"></div>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Cancel</button>
      <button class="btn btn-primary" onclick="addStudent()">Add Student</button>
    </div>
  </div>
</div>

<!-- ANNOUNCE MODAL -->
<div class="modal-backdrop" id="announceBackdrop" onclick="closeAnnounceModal(event)">
  <div class="modal" onclick="event.stopPropagation()">
    <div class="modal-title">New Announcement</div>
    <div class="form-group"><label class="form-label">Title</label><input class="form-input" placeholder="Announcement title..." id="aTitle"></div>
    <div class="form-group"><label class="form-label">Content</label><textarea class="form-input" rows="4" placeholder="Write your announcement..." id="aContent"></textarea></div>
    <div class="form-row">
      <div class="form-group"><label class="form-label">Audience</label>
        <select class="form-input"><option>All Students</option><option>Grade 9</option><option>Grade 10</option><option>Grade 11</option><option>Grade 12</option></select>
      </div>
      <div class="form-group"><label class="form-label">Priority</label>
        <select class="form-input"><option>Normal</option><option>Important</option><option>Urgent</option></select>
      </div>
    </div>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeAnnounceModal()">Cancel</button>
      <button class="btn btn-primary" onclick="postAnnouncement()">Post Announcement</button>
    </div>
  </div>
</div>

<script>
const COLORS = ['#2d5a3d','#b85c2a','#1e4a8c','#9a6b0a','#6b3fa0','#1e6b8a','#8a3f1e','#3f6b1e'];

const students = [
  { name:'Aiden Clark', id:'STU-2401', grade:'Grade 10', attendance:96, score:88, status:'Active' },
  { name:'Priya Sharma', id:'STU-2402', grade:'Grade 11', attendance:92, score:94, status:'Active' },
  { name:'Marcus Webb', id:'STU-2403', grade:'Grade 9', attendance:78, score:72, status:'At Risk' },
  { name:'Zara Ahmed', id:'STU-2404', grade:'Grade 12', attendance:99, score:96, status:'Active' },
  { name:'Liam Torres', id:'STU-2405', grade:'Grade 10', attendance:85, score:79, status:'Active' },
  { name:'Chloe Bennett', id:'STU-2406', grade:'Grade 11', attendance:91, score:85, status:'Active' },
  { name:'Noah Kim', id:'STU-2407', grade:'Grade 9', attendance:74, score:68, status:'At Risk' },
  { name:'Amara Johnson', id:'STU-2408', grade:'Grade 12', attendance:97, score:91, status:'Active' },
  { name:'Ethan Patel', id:'STU-2409', grade:'Grade 10', attendance:88, score:83, status:'Active' },
  { name:'Sofia Rivera', id:'STU-2410', grade:'Grade 11', attendance:93, score:89, status:'Active' },
];

const subjects = [
  { name:'Mathematics', avg:76, color:'#2d5a3d' },
  { name:'Science', avg:81, color:'#1e4a8c' },
  { name:'English', avg:85, color:'#b85c2a' },
  { name:'History', avg:72, color:'#9a6b0a' },
  { name:'Computer Science', avg:88, color:'#6b3fa0' },
  { name:'Physical Education', avg:94, color:'#1e6b8a' },
];

const announces = [
  { title:'Mid-term exams scheduled for May 20–24', from:'Principal\'s Office', date:'May 10', type:'info', icon: 'M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z' },
  { title:'Library will be closed May 8–9 for maintenance', from:'Facilities', date:'May 8', type:'warn', icon: 'M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z' },
  { title:'Term 2 report cards are now available online', from:'Academic Office', date:'May 5', type:'success', icon: 'M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4' },
  { title:'Science fair registrations open until May 15', from:'Science Dept.', date:'May 3', type:'info', icon: 'M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z' },
];

function getInitials(name) { return name.split(' ').map(n=>n[0]).join('').slice(0,2); }
function scoreColor(s) { return s>=90?'#2d5a3d':s>=75?'#9a6b0a':s>=60?'#1e4a8c':'#b85c2a'; }
function statusBadge(s) {
  if(s==='Active') return `<span class="badge badge-green">${s}</span>`;
  if(s==='At Risk') return `<span class="badge badge-amber">${s}</span>`;
  return `<span class="badge badge-gray">${s}</span>`;
}

function renderDashboardStudents() {
  const tbody = document.getElementById('dashStudentRows');
  tbody.innerHTML = students.slice(0,6).map(s=>`
    <tr>
      <td><div class="student-cell"><div class="stu-avatar" style="background:${COLORS[s.id.slice(-1)%COLORS.length]}">${getInitials(s.name)}</div>${s.name}</div></td>
      <td><span class="badge badge-gray">${s.grade}</span></td>
      <td><div class="progress-wrap"><div class="progress-bar"><div class="progress-fill" style="width:${s.attendance}%;background:${s.attendance>85?'#2d5a3d':'#9a6b0a'}"></div></div><span class="progress-val">${s.attendance}%</span></div></td>
      <td>${statusBadge(s.status)}</td>
    </tr>`).join('');
}

function renderStudentsGrid() {
  const grid = document.getElementById('studentsGrid');
  grid.innerHTML = students.map(s=>`
    <div class="stu-card">
      <div class="stu-card-avatar" style="background:${COLORS[s.id.slice(-1)%COLORS.length]}">${getInitials(s.name)}</div>
      <div class="stu-card-name">${s.name}</div>
      <div class="stu-card-id">${s.id} · ${s.grade}</div>
      <div style="margin-bottom:10px;">${statusBadge(s.status)}</div>
      <div class="stu-card-stats">
        <div class="stu-stat"><strong>${s.attendance}%</strong>Attend.</div>
        <div class="stu-stat"><strong>${s.score}</strong>Score</div>
      </div>
    </div>`).join('');
}

function renderAttendanceCalendar() {
  const grid = document.getElementById('calGrid');
  const data = [null,null,null,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31];
  const absent = [3,9,14,22];
  const weekend = d => { if(!d) return false; const dow = (d+2)%7; return dow===0||dow===6; };
  grid.innerHTML = data.map(d=>{
    if(!d) return `<div></div>`;
    const isAbsent = absent.includes(d);
    const isWeekend = weekend(d);
    const isToday = d===1;
    let cls = 'att-cell';
    if(isWeekend) cls+=' empty';
    else if(isAbsent) cls+=' absent';
    else if(d<10) cls+=' present';
    if(isToday) cls+=' today';
    return `<div class="${cls}" title="${isAbsent?'Absent':isWeekend?'Weekend':'Present'}">${d}</div>`;
  }).join('');

  const attList = document.getElementById('attStudentList');
  attList.innerHTML = `<div style="font-size:12px;color:var(--text-muted);margin-bottom:10px;">Students absent today</div>` +
    students.filter((_,i)=>i%3===0).slice(0,4).map(s=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-bottom:1px solid var(--border);">
      <div class="stu-avatar" style="background:${COLORS[s.id.slice(-1)%COLORS.length]};width:28px;height:28px;font-size:10px;">${getInitials(s.name)}</div>
      <div><div style="font-size:13px;font-weight:500">${s.name}</div><div style="font-size:11px;color:var(--text-muted)">${s.grade}</div></div>
      <span class="badge badge-red" style="margin-left:auto">Absent</span>
    </div>`).join('');

  const classTable = document.getElementById('classAttTable');
  const classes = [
    {name:'Grade 9A',total:32,present:30},{name:'Grade 9B',total:30,present:27},
    {name:'Grade 10A',total:34,present:32},{name:'Grade 10B',total:33,present:33},
    {name:'Grade 11A',total:31,present:29},{name:'Grade 12A',total:28,present:26},
  ];
  classTable.innerHTML = classes.map(c=>{
    const rate = Math.round(c.present/c.total*100);
    return `<tr>
      <td style="font-weight:500">${c.name}</td>
      <td>${c.total}</td>
      <td style="color:var(--accent)">${c.present}</td>
      <td style="color:#c0392b">${c.total-c.present}</td>
      <td><div class="progress-wrap"><div class="progress-bar"><div class="progress-fill" style="width:${rate}%;background:${rate>90?'#2d5a3d':rate>80?'#9a6b0a':'#b85c2a'}"></div></div><span class="progress-val">${rate}%</span></div></td>
      <td>${rate>90?'<span class="badge badge-green">Excellent</span>':rate>80?'<span class="badge badge-amber">Good</span>':'<span class="badge badge-red">Poor</span>'}</td>
    </tr>`;
  }).join('');
}

function renderSubjectBars(containerId) {
  const el = document.getElementById(containerId);
  el.innerHTML = subjects.map(s=>`
    <div style="margin-bottom:14px;">
      <div style="display:flex;justify-content:space-between;margin-bottom:6px;">
        <span style="font-size:13px;color:var(--text)">${s.name}</span>
        <span style="font-size:13px;font-weight:500;color:var(--text)">${s.avg}/100</span>
      </div>
      <div class="progress-bar" style="height:8px;"><div class="progress-fill" style="width:${s.avg}%;background:${s.color};transition:width 0.6s ease;"></div></div>
    </div>`).join('');
}

function renderAttChart() {
  const data = [92,88,95,91,87];
  const max = 100;
  const container = document.getElementById('attChart');
  container.innerHTML = data.map((v,i)=>`
    <div class="bar-col">
      <div class="bar ${i===2?'highlight':''}" style="height:${(v/max)*120}px;" title="${v}% attendance"></div>
    </div>`).join('');
}

function renderPerformance() {
  const tbody = document.getElementById('gradesTableBody');
  tbody.innerHTML = students.map(s=>{
    const scores = [Math.round(s.score+Math.random()*10-5), Math.round(s.score+Math.random()*8-4), Math.round(s.score+Math.random()*12-6), Math.round(s.score+Math.random()*15-7)].map(x=>Math.max(40,Math.min(100,x)));
    const overall = Math.round(scores.reduce((a,b)=>a+b,0)/4);
    const grade = overall>=90?'A+':overall>=80?'A':overall>=70?'B':overall>=60?'C':'D';
    const gc = overall>=80?'badge-green':overall>=70?'badge-blue':overall>=60?'badge-amber':'badge-red';
    return `<tr>
      <td><div class="student-cell"><div class="stu-avatar" style="background:${COLORS[s.id.slice(-1)%COLORS.length]};width:28px;height:28px;font-size:10px">${getInitials(s.name)}</div>${s.name}</div></td>
      ${scores.map(sc=>`<td>${sc}</td>`).join('')}
      <td style="font-weight:600">${overall}</td>
      <td><span class="badge ${gc}">${grade}</span></td>
    </tr>`;
  }).join('');

  const top = document.getElementById('topPerformers');
  const sorted = [...students].sort((a,b)=>b.score-a.score).slice(0,5);
  top.innerHTML = sorted.map((s,i)=>`
    <div style="display:flex;align-items:center;gap:12px;padding:10px 0;border-bottom:1px solid var(--border);">
      <div style="width:22px;height:22px;border-radius:50%;background:${i===0?'#9a6b0a':'var(--surface2)'};color:${i===0?'white':'var(--text-muted)'};display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:600;flex-shrink:0;">${i+1}</div>
      <div class="stu-avatar" style="background:${COLORS[s.id.slice(-1)%COLORS.length]};width:30px;height:30px;font-size:11px;flex-shrink:0">${getInitials(s.name)}</div>
      <div style="flex:1"><div style="font-size:13px;font-weight:500">${s.name}</div><div style="font-size:11px;color:var(--text-muted)">${s.grade}</div></div>
      <span style="font-size:14px;font-weight:600;color:var(--accent)">${s.score}</span>
    </div>`).join('');
}

function renderAnnouncements() {
  const el = document.getElementById('announceList');
  const colors = { info:'var(--blue-light)', warn:'var(--amber-light)', success:'var(--accent-light)' };
  const strokes = { info:'var(--blue)', warn:'var(--amber)', success:'var(--accent)' };
  el.innerHTML = announces.map(a=>`
    <div class="announce-item">
      <div class="announce-top">
        <div class="announce-icon" style="background:${colors[a.type]}">
          <svg fill="none" viewBox="0 0 24 24" stroke="${strokes[a.type]}" stroke-width="1.8" width="14" height="14"><path stroke-linecap="round" stroke-linejoin="round" d="${a.icon}"/></svg>
        </div>
        <div>
          <div class="announce-title">${a.title}</div>
          <div class="announce-meta">${a.from} · ${a.date}, 2025</div>
        </div>
      </div>
    </div>`).join('');
}

function navigate(page, el) {
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  if(el) el.classList.add('active');
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.getElementById('panel-'+page).classList.add('active');
  const titles = { dashboard:'Dashboard', students:'Students', attendance:'Attendance', performance:'Academic Performance', communication:'Communication' };
  document.getElementById('pageTitle').textContent = titles[page]||page;
  if(page==='students') renderStudentsGrid();
  if(page==='attendance') renderAttendanceCalendar();
  if(page==='performance') { renderPerformance(); renderSubjectBars('perfSubjectBars'); }
  if(page==='communication') renderAnnouncements();
}

function openModal() { document.getElementById('modalBackdrop').classList.add('open'); }
function closeModal(e) { if(!e||e.target===document.getElementById('modalBackdrop')) document.getElementById('modalBackdrop').classList.remove('open'); }
function openAnnounceModal() { document.getElementById('announceBackdrop').classList.add('open'); }
function closeAnnounceModal(e) { if(!e||e.target===document.getElementById('announceBackdrop')) document.getElementById('announceBackdrop').classList.remove('open'); }

function addStudent() {
  const fn = document.getElementById('fName').value;
  const ln = document.getElementById('lName').value;
  if(!fn||!ln) { alert('Please enter first and last name.'); return; }
  const grade = document.getElementById('grade').value;
  const newStu = { name: fn+' '+ln, id:'STU-'+Math.floor(2400+Math.random()*500), grade, attendance: Math.round(75+Math.random()*25), score: Math.round(65+Math.random()*30), status:'Active' };
  students.unshift(newStu);
  closeModal();
  document.getElementById('fName').value=''; document.getElementById('lName').value=''; document.getElementById('email').value=''; document.getElementById('phone').value='';
  renderDashboardStudents();
}

function postAnnouncement() {
  const title = document.getElementById('aTitle').value;
  if(!title) { alert('Please enter a title.'); return; }
  announces.unshift({ title, from:'Admin', date:'Today', type:'info', icon:'M11 5.882V19.24a1.76 1.76 0 01-3.417.592l-2.147-6.15M18 13a3 3 0 100-6M5.436 13.683A4.001 4.001 0 017 6h1.832c4.1 0 7.625-1.234 9.168-3v14c-1.543-1.766-5.067-3-9.168-3H7a3.988 3.988 0 01-1.564-.317z' });
  closeAnnounceModal();
  document.getElementById('aTitle').value=''; document.getElementById('aContent').value='';
  renderAnnouncements();
}

function toggleNotif() {
  document.getElementById('notifDropdown').classList.toggle('open');
}
document.addEventListener('click', function(e) {
  if(!e.target.closest('.rel')) document.getElementById('notifDropdown').classList.remove('open');
});

function toggleTheme() {
  const toggle = document.getElementById('themeToggle');
  const isDark = toggle.classList.toggle('on');
  document.documentElement.dataset.theme = isDark ? 'dark' : '';
}

// Chip filters
document.querySelectorAll('.filter-chip').forEach(chip=>{
  chip.addEventListener('click', function() {
    this.closest('.filters-row').querySelectorAll('.filter-chip').forEach(c=>c.classList.remove('active'));
    this.classList.add('active');
  });
});

// Init
renderDashboardStudents();
renderAttChart();
renderSubjectBars('subjectBars');
</script>
</body>
</html>
