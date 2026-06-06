[index.html](https://github.com/user-attachments/files/28660051/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Dispatcher Hub</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #f5f5f0;
    --surface: #ffffff;
    --surface2: #f0efea;
    --border: rgba(0,0,0,0.1);
    --border-mid: rgba(0,0,0,0.18);
    --text: #1a1a1a;
    --text-muted: #666;
    --text-hint: #999;
    --accent: #1a1a2e;
    --accent-light: #eeeef8;
    --accent-text: #534AB7;
    --radius: 10px;
    --radius-lg: 14px;
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #111110;
      --surface: #1c1c1a;
      --surface2: #242422;
      --border: rgba(255,255,255,0.08);
      --border-mid: rgba(255,255,255,0.14);
      --text: #f0efe8;
      --text-muted: #aaa;
      --text-hint: #666;
      --accent: #2e2e50;
      --accent-light: #1e1e38;
      --accent-text: #a49ef5;
    }
  }

  body {
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
  }

  /* SIDEBAR */
  .layout { display: flex; min-height: 100vh; }

  .sidebar {
    width: 220px;
    min-width: 220px;
    background: var(--accent);
    display: flex;
    flex-direction: column;
    padding: 1.5rem 0;
    position: sticky;
    top: 0;
    height: 100vh;
    overflow-y: auto;
  }

  .sidebar-logo {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 0 1.2rem 1.5rem;
    border-bottom: 0.5px solid rgba(255,255,255,0.1);
    margin-bottom: 1rem;
  }

  .logo-icon {
    width: 34px; height: 34px;
    background: rgba(255,255,255,0.15);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
  }
  .logo-icon i { font-size: 18px; color: #fff; }

  .logo-text { color: #fff; font-size: 15px; font-weight: 600; line-height: 1.2; }
  .logo-sub { color: rgba(255,255,255,0.5); font-size: 11px; margin-top: 1px; }

  .nav-section { margin-bottom: 0.25rem; }
  .nav-label {
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.35);
    padding: 0.75rem 1.2rem 0.25rem;
  }

  .nav-item {
    display: flex;
    align-items: center;
    gap: 9px;
    padding: 8px 1.2rem;
    color: rgba(255,255,255,0.65);
    font-size: 13.5px;
    cursor: pointer;
    border: none;
    background: none;
    width: 100%;
    text-align: left;
    border-radius: 0;
    transition: background 0.12s, color 0.12s;
    position: relative;
  }
  .nav-item i { font-size: 16px; flex-shrink: 0; }
  .nav-item:hover { background: rgba(255,255,255,0.07); color: rgba(255,255,255,0.9); }
  .nav-item.active {
    background: rgba(255,255,255,0.12);
    color: #fff;
    font-weight: 500;
  }
  .nav-item.active::before {
    content: '';
    position: absolute;
    left: 0; top: 4px; bottom: 4px;
    width: 3px;
    background: #a49ef5;
    border-radius: 0 2px 2px 0;
  }

  .nav-sub {
    padding-left: 2.8rem;
    font-size: 13px;
    color: rgba(255,255,255,0.5);
    display: none;
  }
  .nav-sub.open { display: block; }
  .nav-sub-item {
    display: block;
    padding: 5px 1.2rem 5px 0;
    cursor: pointer;
    color: rgba(255,255,255,0.5);
    font-size: 12.5px;
    border: none;
    background: none;
    width: 100%;
    text-align: left;
    transition: color 0.12s;
  }
  .nav-sub-item:hover { color: rgba(255,255,255,0.85); }
  .nav-sub-item.active { color: #a49ef5; font-weight: 500; }

  /* MAIN */
  .main {
    flex: 1;
    padding: 2rem 2.5rem;
    max-width: 900px;
  }

  .section { display: none; }
  .section.active { display: block; }

  .page-header { margin-bottom: 1.5rem; }
  .page-header h1 { font-size: 22px; font-weight: 600; color: var(--text); }
  .page-header p { font-size: 14px; color: var(--text-muted); margin-top: 4px; }

  /* CARDS GRID */
  .cards { display: grid; grid-template-columns: repeat(auto-fill, minmax(170px, 1fr)); gap: 12px; }

  .card {
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 1.1rem 1.1rem 1rem;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    gap: 8px;
    text-decoration: none;
    transition: border-color 0.14s, box-shadow 0.14s, transform 0.12s;
  }
  .card:hover {
    border-color: var(--border-mid);
    box-shadow: 0 2px 12px rgba(0,0,0,0.07);
    transform: translateY(-1px);
  }

  .card-icon {
    width: 38px; height: 38px;
    border-radius: 9px;
    display: flex; align-items: center; justify-content: center;
    font-size: 19px;
    flex-shrink: 0;
  }
  .ci-blue   { background: #E6F1FB; color: #185FA5; }
  .ci-teal   { background: #E1F5EE; color: #0F6E56; }
  .ci-amber  { background: #FAEEDA; color: #854F0B; }
  .ci-coral  { background: #FAECE7; color: #993C1D; }
  .ci-purple { background: #EEEDFE; color: #534AB7; }
  .ci-green  { background: #EAF3DE; color: #3B6D11; }
  .ci-gray   { background: var(--surface2); color: var(--text-muted); }
  .ci-pink   { background: #FBEAF0; color: #993556; }

  @media (prefers-color-scheme: dark) {
    .ci-blue   { background: #0c3256; color: #85B7EB; }
    .ci-teal   { background: #043430; color: #5DCAA5; }
    .ci-amber  { background: #412402; color: #EF9F27; }
    .ci-coral  { background: #4A1B0C; color: #F0997B; }
    .ci-purple { background: #26215C; color: #AFA9EC; }
    .ci-green  { background: #173404; color: #97C459; }
    .ci-pink   { background: #4B1528; color: #ED93B1; }
  }

  .card-name { font-size: 13.5px; font-weight: 500; color: var(--text); line-height: 1.3; }
  .card-desc { font-size: 12px; color: var(--text-muted); line-height: 1.5; }

  .card-tag {
    font-size: 11px;
    padding: 2px 8px;
    border-radius: 20px;
    align-self: flex-start;
    margin-top: 2px;
    font-weight: 500;
  }
  .tag-link   { background: #E6F1FB; color: #185FA5; }
  .tag-doc    { background: #FAEEDA; color: #854F0B; }
  .tag-tool   { background: #E1F5EE; color: #0F6E56; }
  .tag-form   { background: #EEEDFE; color: #534AB7; }
  .tag-secure { background: var(--surface2); color: var(--text-muted); }
  .tag-train  { background: #EAF3DE; color: #3B6D11; }
  .tag-folder { background: #FBEAF0; color: #993556; }
  .tag-contract { background: #FAECE7; color: #993C1D; }
  .tag-memo   { background: #FAEEDA; color: #854F0B; }

  @media (prefers-color-scheme: dark) {
    .tag-link   { background: #0c3256; color: #85B7EB; }
    .tag-doc    { background: #412402; color: #EF9F27; }
    .tag-tool   { background: #043430; color: #5DCAA5; }
    .tag-form   { background: #26215C; color: #AFA9EC; }
    .tag-train  { background: #173404; color: #97C459; }
    .tag-folder { background: #4B1528; color: #ED93B1; }
    .tag-contract { background: #4A1B0C; color: #F0997B; }
    .tag-memo   { background: #412402; color: #EF9F27; }
  }

  .group-label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.07em;
    text-transform: uppercase;
    color: var(--text-hint);
    margin: 1.5rem 0 0.6rem;
  }
  .group-label:first-child { margin-top: 0; }

  /* WELCOME */
  .welcome-hero {
    background: var(--accent);
    border-radius: var(--radius-lg);
    padding: 2rem;
    color: #fff;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }
  .welcome-hero .hi { font-size: 20px; font-weight: 600; }
  .welcome-hero .sub { font-size: 13px; color: rgba(255,255,255,0.6); margin-top: 4px; line-height: 1.5; }
  .welcome-icon { font-size: 44px; opacity: 0.7; }

  .quick-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 10px; }

  /* RESPONSIVE */
  @media (max-width: 680px) {
    .sidebar { display: none; }
    .main { padding: 1rem 1rem; }
    .mobile-nav {
      display: flex;
      overflow-x: auto;
      gap: 6px;
      padding: 0.75rem 1rem;
      background: var(--surface);
      border-bottom: 0.5px solid var(--border);
      -webkit-overflow-scrolling: touch;
    }
    .mobile-nav-btn {
      flex-shrink: 0;
      font-size: 12px;
      padding: 5px 12px;
      border: 0.5px solid var(--border-mid);
      border-radius: 20px;
      background: none;
      color: var(--text-muted);
      cursor: pointer;
    }
    .mobile-nav-btn.active { background: var(--accent); color: #fff; border-color: var(--accent); }
  }
  @media (min-width: 681px) {
    .mobile-nav { display: none; }
  }
</style>
</head>
<body>

<div class="layout">

  <!-- SIDEBAR -->
  <nav class="sidebar" aria-label="Main navigation">
    <div class="sidebar-logo">
      <div class="logo-icon"><i class="ti ti-key" aria-hidden="true"></i></div>
      <div>
        <div class="logo-text">Dispatcher Hub</div>
        <div class="logo-sub">Internal portal</div>
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Overview</div>
      <button class="nav-item active" onclick="showSection('home', this)">
        <i class="ti ti-home" aria-hidden="true"></i> Home
      </button>
    </div>

    <div class="nav-section">
      <div class="nav-label">Workspace</div>
      <button class="nav-item" onclick="toggleSub('schedule-sub', this, 'schedule')">
        <i class="ti ti-calendar" aria-hidden="true"></i> Schedule
      </button>
      <div class="nav-sub" id="schedule-sub">
        <button class="nav-sub-item" onclick="showSection('timesheet')">Timesheet</button>
        <button class="nav-sub-item" onclick="showSection('schedule2026')">2026 Schedule</button>
      </div>

      <button class="nav-item" onclick="toggleSub('tools-sub', this, 'tools')">
        <i class="ti ti-tool" aria-hidden="true"></i> Tools
      </button>
      <div class="nav-sub" id="tools-sub">
        <button class="nav-sub-item" onclick="showSection('logins')">Logins</button>
        <button class="nav-sub-item" onclick="showSection('dialpad')">Dialpad</button>
        <button class="nav-sub-item" onclick="showSection('uleadz')">uLeadz</button>
        <button class="nav-sub-item" onclick="showSection('workiz')">Workiz</button>
        <button class="nav-sub-item" onclick="showSection('pricing')">Pricing</button>
        <button class="nav-sub-item" onclick="showSection('taskguide')">Task Guide</button>
        <button class="nav-sub-item" onclick="showSection('checklist')">Checklist</button>
      </div>

      <button class="nav-item" onclick="showSection('reports', this)">
        <i class="ti ti-chart-bar" aria-hidden="true"></i> Reports
      </button>
    </div>

    <div class="nav-section">
      <div class="nav-label">Knowledge</div>
      <button class="nav-item" onclick="toggleSub('learning-sub', this, 'learning')">
        <i class="ti ti-school" aria-hidden="true"></i> Learning Hub
      </button>
      <div class="nav-sub" id="learning-sub">
        <button class="nav-sub-item" onclick="showSection('onboarding-learn')">Onboarding</button>
        <button class="nav-sub-item" onclick="showSection('garage-door')">Garage Door</button>
        <button class="nav-sub-item" onclick="showSection('chimney')">Chimney</button>
        <button class="nav-sub-item" onclick="showSection('key-types')">Key Types</button>
      </div>

      <button class="nav-item" onclick="toggleSub('sop-sub', this, 'sop')">
        <i class="ti ti-file-text" aria-hidden="true"></i> SOPs
      </button>
      <div class="nav-sub" id="sop-sub">
        <button class="nav-sub-item" onclick="showSection('onboarding-contract')">Onboarding Contract</button>
        <button class="nav-sub-item" onclick="showSection('memos')">Memos</button>
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Performance</div>
      <button class="nav-item" onclick="toggleSub('eval-sub', this, 'eval')">
        <i class="ti ti-star" aria-hidden="true"></i> Call Evaluation
      </button>
      <div class="nav-sub" id="eval-sub">
        <button class="nav-sub-item" onclick="showSection('dispatchers-folder')">Dispatchers Folder</button>
      </div>
    </div>
  </nav>

  <!-- MOBILE NAV -->
  <div class="mobile-nav">
    <button class="mobile-nav-btn active" onclick="showSection('home',this)">Home</button>
    <button class="mobile-nav-btn" onclick="showSection('schedule',this)">Schedule</button>
    <button class="mobile-nav-btn" onclick="showSection('tools',this)">Tools</button>
    <button class="mobile-nav-btn" onclick="showSection('reports',this)">Reports</button>
    <button class="mobile-nav-btn" onclick="showSection('learning',this)">Learning</button>
    <button class="mobile-nav-btn" onclick="showSection('sop',this)">SOPs</button>
    <button class="mobile-nav-btn" onclick="showSection('eval',this)">Evaluation</button>
  </div>

  <!-- MAIN CONTENT -->
  <main class="main">

    <!-- HOME -->
    <div id="home" class="section active">
      <div class="welcome-hero">
        <div class="welcome-icon" aria-hidden="true">🗝️</div>
        <div>
          <div class="hi">Welcome, Dispatcher</div>
          <div class="sub">Your central hub for tools, schedules, training, and resources.<br>Everything you need — in one place.</div>
        </div>
      </div>
      <div class="page-header">
        <h1>Quick Access</h1>
        <p>Most-used tools and links</p>
      </div>
      <div class="quick-grid">
        <div class="card" onclick="showSection('timesheet')">
          <div class="card-icon ci-blue"><i class="ti ti-clock" aria-hidden="true"></i></div>
          <div class="card-name">Timesheet</div>
          <span class="card-tag tag-form">Form</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-blue"><i class="ti ti-phone" aria-hidden="true"></i></div>
          <div class="card-name">Dialpad</div>
          <span class="card-tag tag-link">Link</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-teal"><i class="ti ti-users" aria-hidden="true"></i></div>
          <div class="card-name">uLeadz</div>
          <span class="card-tag tag-link">Link</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-green"><i class="ti ti-settings" aria-hidden="true"></i></div>
          <div class="card-name">Workiz</div>
          <span class="card-tag tag-link">Link</span>
        </div>
        <div class="card" onclick="showSection('pricing')">
          <div class="card-icon ci-amber"><i class="ti ti-currency-dollar" aria-hidden="true"></i></div>
          <div class="card-name">Pricing</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
        <div class="card" onclick="showSection('checklist')">
          <div class="card-icon ci-coral"><i class="ti ti-checkbox" aria-hidden="true"></i></div>
          <div class="card-name">Checklist</div>
          <span class="card-tag tag-form">Form</span>
        </div>
      </div>
    </div>

    <!-- SCHEDULE OVERVIEW -->
    <div id="schedule" class="section">
      <div class="page-header">
        <h1>Dispatcher's Schedule</h1>
        <p>Timesheets and annual schedule tracker</p>
      </div>
      <div class="cards">
        <div class="card" onclick="showSection('timesheet')">
          <div class="card-icon ci-blue"><i class="ti ti-clock" aria-hidden="true"></i></div>
          <div class="card-name">Timesheet</div>
          <div class="card-desc">Log and review daily hours worked</div>
          <span class="card-tag tag-form">Form</span>
        </div>
        <div class="card" onclick="showSection('schedule2026')">
          <div class="card-icon ci-teal"><i class="ti ti-calendar-event" aria-hidden="true"></i></div>
          <div class="card-name">2026 Schedule</div>
          <div class="card-desc">Full year dispatcher schedule</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
      </div>
    </div>

    <!-- TIMESHEET -->
    <div id="timesheet" class="section">
      <div class="page-header">
        <h1>Timesheet</h1>
        <p>Log your hours below — add link to Google Sheets or timesheet tool here</p>
      </div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-blue"><i class="ti ti-external-link" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Open Timesheet</div>
        <div class="card-desc">Click to open the timesheet in Google Sheets or your timekeeping platform.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none">
          <i class="ti ti-external-link" style="font-size:14px"></i> Open Timesheet
        </a>
      </div>
    </div>

    <!-- 2026 SCHEDULE -->
    <div id="schedule2026" class="section">
      <div class="page-header">
        <h1>2026 Schedule</h1>
        <p>Annual dispatcher schedule — replace link below with actual doc</p>
      </div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-teal"><i class="ti ti-calendar-event" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">View 2026 Schedule</div>
        <div class="card-desc">Opens the full year schedule document for all dispatchers.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none">
          <i class="ti ti-external-link" style="font-size:14px"></i> Open Schedule
        </a>
      </div>
    </div>

    <!-- TOOLS OVERVIEW -->
    <div id="tools" class="section">
      <div class="page-header">
        <h1>Tools</h1>
        <p>Quick access to all platforms, apps, and guides</p>
      </div>
      <div class="group-label">Platforms &amp; Links</div>
      <div class="cards">
        <div class="card" onclick="showSection('logins')">
          <div class="card-icon ci-gray"><i class="ti ti-lock" aria-hidden="true"></i></div>
          <div class="card-name">Logins</div>
          <div class="card-desc">Credentials and account access</div>
          <span class="card-tag tag-secure">Secured</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-blue"><i class="ti ti-phone" aria-hidden="true"></i></div>
          <div class="card-name">Dialpad</div>
          <div class="card-desc">Open the Dialpad phone platform</div>
          <span class="card-tag tag-link">Link</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-teal"><i class="ti ti-users" aria-hidden="true"></i></div>
          <div class="card-name">uLeadz</div>
          <div class="card-desc">Lead management platform</div>
          <span class="card-tag tag-link">Link</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-green"><i class="ti ti-settings" aria-hidden="true"></i></div>
          <div class="card-name">Workiz</div>
          <div class="card-desc">Job and dispatch management</div>
          <span class="card-tag tag-link">Link</span>
        </div>
      </div>
      <div class="group-label">Guides &amp; References</div>
      <div class="cards">
        <div class="card" onclick="showSection('pricing')">
          <div class="card-icon ci-amber"><i class="ti ti-currency-dollar" aria-hidden="true"></i></div>
          <div class="card-name">Pricing</div>
          <div class="card-desc">Service pricing reference sheet</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
        <div class="card" onclick="showSection('taskguide')">
          <div class="card-icon ci-purple"><i class="ti ti-list" aria-hidden="true"></i></div>
          <div class="card-name">Task Guide</div>
          <div class="card-desc">Step-by-step task instructions</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
        <div class="card" onclick="showSection('checklist')">
          <div class="card-icon ci-coral"><i class="ti ti-checkbox" aria-hidden="true"></i></div>
          <div class="card-name">Checklist</div>
          <div class="card-desc">Daily and shift checklists</div>
          <span class="card-tag tag-form">Form</span>
        </div>
      </div>
    </div>

    <!-- TOOL DETAIL PAGES (logins, dialpad, uleadz, workiz, pricing, taskguide, checklist) -->
    <div id="logins" class="section">
      <div class="page-header"><h1>Logins</h1><p>Account credentials and platform access</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-gray"><i class="ti ti-lock" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Login Sheet</div>
        <div class="card-desc">Add your secured credentials document link here (e.g. private Google Doc or password manager).</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Logins</a>
      </div>
    </div>

    <div id="dialpad" class="section">
      <div class="page-header"><h1>Dialpad</h1><p>Phone and communication platform</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-blue"><i class="ti ti-phone" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Open Dialpad</div>
        <div class="card-desc">Click to launch Dialpad in a new tab.</div>
        <a href="https://dialpad.com" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Dialpad</a>
      </div>
    </div>

    <div id="uleadz" class="section">
      <div class="page-header"><h1>uLeadz</h1><p>Lead management platform</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-teal"><i class="ti ti-users" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Open uLeadz</div>
        <div class="card-desc">Click to launch uLeadz in a new tab.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open uLeadz</a>
      </div>
    </div>

    <div id="workiz" class="section">
      <div class="page-header"><h1>Workiz</h1><p>Job and dispatch management</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-green"><i class="ti ti-settings" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Open Workiz</div>
        <div class="card-desc">Click to launch Workiz in a new tab.</div>
        <a href="https://app.workiz.com" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Workiz</a>
      </div>
    </div>

    <div id="pricing" class="section">
      <div class="page-header"><h1>Pricing</h1><p>Service pricing reference</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-amber"><i class="ti ti-currency-dollar" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Pricing Sheet</div>
        <div class="card-desc">Open the pricing document — replace link with your Google Sheet or PDF.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Pricing</a>
      </div>
    </div>

    <div id="taskguide" class="section">
      <div class="page-header"><h1>Task Guide</h1><p>Step-by-step task instructions</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-purple"><i class="ti ti-list" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Task Guide</div>
        <div class="card-desc">Open the task guide document — replace link with your Google Doc or PDF.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Task Guide</a>
      </div>
    </div>

    <div id="checklist" class="section">
      <div class="page-header"><h1>Checklist</h1><p>Daily and shift checklists</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-coral"><i class="ti ti-checkbox" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Shift Checklist</div>
        <div class="card-desc">Open the checklist — replace link with your Google Form or checklist doc.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Checklist</a>
      </div>
    </div>

    <!-- REPORTS -->
    <div id="reports" class="section">
      <div class="page-header"><h1>Reports</h1><p>Performance data, metrics, and summaries</p></div>
      <div class="cards">
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-blue"><i class="ti ti-chart-line" aria-hidden="true"></i></div>
          <div class="card-name">Daily Report</div>
          <div class="card-desc">Today's job and call summary</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-teal"><i class="ti ti-chart-bar" aria-hidden="true"></i></div>
          <div class="card-name">Weekly Summary</div>
          <div class="card-desc">Week-over-week performance</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
        <div class="card" onclick="window.open('#','_blank')">
          <div class="card-icon ci-amber"><i class="ti ti-file-analytics" aria-hidden="true"></i></div>
          <div class="card-name">Monthly Report</div>
          <div class="card-desc">Full monthly metrics overview</div>
          <span class="card-tag tag-doc">Doc</span>
        </div>
      </div>
    </div>

    <!-- LEARNING HUB -->
    <div id="learning" class="section">
      <div class="page-header"><h1>Learning Hub</h1><p>Training materials and product knowledge</p></div>
      <div class="group-label">Getting started</div>
      <div class="cards">
        <div class="card" onclick="showSection('onboarding-learn')">
          <div class="card-icon ci-teal"><i class="ti ti-school" aria-hidden="true"></i></div>
          <div class="card-name">Onboarding</div>
          <div class="card-desc">New dispatcher training modules</div>
          <span class="card-tag tag-train">Training</span>
        </div>
      </div>
      <div class="group-label">Service knowledge</div>
      <div class="cards">
        <div class="card" onclick="showSection('garage-door')">
          <div class="card-icon ci-amber"><i class="ti ti-building" aria-hidden="true"></i></div>
          <div class="card-name">Garage Door</div>
          <div class="card-desc">Types, repairs, and services</div>
          <span class="card-tag tag-doc">Guide</span>
        </div>
        <div class="card" onclick="showSection('chimney')">
          <div class="card-icon ci-coral"><i class="ti ti-flame" aria-hidden="true"></i></div>
          <div class="card-name">Chimney</div>
          <div class="card-desc">Chimney service knowledge base</div>
          <span class="card-tag tag-doc">Guide</span>
        </div>
        <div class="card" onclick="showSection('key-types')">
          <div class="card-icon ci-purple"><i class="ti ti-key" aria-hidden="true"></i></div>
          <div class="card-name">Key Types</div>
          <div class="card-desc">Key identification and services</div>
          <span class="card-tag tag-doc">Guide</span>
        </div>
      </div>
    </div>

    <!-- LEARNING DETAIL PAGES -->
    <div id="onboarding-learn" class="section">
      <div class="page-header"><h1>Onboarding</h1><p>New dispatcher training modules</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-teal"><i class="ti ti-school" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Onboarding Materials</div>
        <div class="card-desc">Replace this link with your onboarding Google Doc, Slides, or training video.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Onboarding</a>
      </div>
    </div>

    <div id="garage-door" class="section">
      <div class="page-header"><h1>Garage Door</h1><p>Types, repairs, and services guide</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-amber"><i class="ti ti-building" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Garage Door Guide</div>
        <div class="card-desc">Replace this link with your garage door knowledge base document.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Guide</a>
      </div>
    </div>

    <div id="chimney" class="section">
      <div class="page-header"><h1>Chimney</h1><p>Chimney service knowledge base</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-coral"><i class="ti ti-flame" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Chimney Guide</div>
        <div class="card-desc">Replace this link with your chimney knowledge base document.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Guide</a>
      </div>
    </div>

    <div id="key-types" class="section">
      <div class="page-header"><h1>Key Types</h1><p>Key identification and services</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-purple"><i class="ti ti-key" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Key Types Guide</div>
        <div class="card-desc">Replace this link with your key types reference document.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Guide</a>
      </div>
    </div>

    <!-- SOPs -->
    <div id="sop" class="section">
      <div class="page-header"><h1>SOPs</h1><p>Standard operating procedures and official documents</p></div>
      <div class="group-label">Procedures</div>
      <div class="cards">
        <div class="card" onclick="showSection('onboarding-contract')">
          <div class="card-icon ci-blue"><i class="ti ti-file-check" aria-hidden="true"></i></div>
          <div class="card-name">Onboarding Contract</div>
          <div class="card-desc">New hire agreement and terms</div>
          <span class="card-tag tag-contract">Contract</span>
        </div>
      </div>
      <div class="group-label">Communications</div>
      <div class="cards">
        <div class="card" onclick="showSection('memos')">
          <div class="card-icon ci-amber"><i class="ti ti-news" aria-hidden="true"></i></div>
          <div class="card-name">Memos</div>
          <div class="card-desc">Company announcements and updates</div>
          <span class="card-tag tag-memo">Memo</span>
        </div>
      </div>
    </div>

    <div id="onboarding-contract" class="section">
      <div class="page-header"><h1>Onboarding Contract</h1><p>New hire agreement and terms</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-blue"><i class="ti ti-file-check" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">View Contract</div>
        <div class="card-desc">Replace this link with your onboarding contract document (Google Doc or PDF).</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Contract</a>
      </div>
    </div>

    <div id="memos" class="section">
      <div class="page-header"><h1>Memos</h1><p>Company announcements and updates</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-amber"><i class="ti ti-news" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Company Memos</div>
        <div class="card-desc">Replace this link with your memos folder (Google Drive, Notion, etc.).</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Memos</a>
      </div>
    </div>

    <!-- EVALUATION -->
    <div id="eval" class="section">
      <div class="page-header"><h1>Call Evaluation</h1><p>Performance reviews and individual scorecards</p></div>
      <div class="cards">
        <div class="card" onclick="showSection('dispatchers-folder')">
          <div class="card-icon ci-pink"><i class="ti ti-folder-open" aria-hidden="true"></i></div>
          <div class="card-name">Dispatchers Folder</div>
          <div class="card-desc">Individual call evaluation records for each dispatcher</div>
          <span class="card-tag tag-folder">Folder</span>
        </div>
      </div>
    </div>

    <div id="dispatchers-folder" class="section">
      <div class="page-header"><h1>Dispatchers Folder</h1><p>Individual call evaluation records</p></div>
      <div class="card" style="max-width:500px;padding:2rem;align-items:flex-start;gap:12px">
        <div class="card-icon ci-pink"><i class="ti ti-folder-open" aria-hidden="true"></i></div>
        <div class="card-name" style="font-size:15px">Evaluation Folder</div>
        <div class="card-desc">Replace this link with your Google Drive folder containing individual dispatcher evaluation files.</div>
        <a href="#" target="_blank" style="display:inline-flex;align-items:center;gap:6px;margin-top:4px;font-size:13px;padding:7px 16px;background:var(--accent);color:#fff;border-radius:8px;text-decoration:none"><i class="ti ti-external-link" style="font-size:14px"></i> Open Folder</a>
      </div>
    </div>

  </main>
</div>

<script>
const navItems = document.querySelectorAll('.nav-item');

function clearActiveNav() {
  navItems.forEach(b => b.classList.remove('active'));
}

function showSection(id, triggerBtn) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  const target = document.getElementById(id);
  if (target) target.classList.add('active');
  if (triggerBtn) {
    clearActiveNav();
    triggerBtn.classList.add('active');
  }
  document.querySelectorAll('.nav-sub-item').forEach(s => {
    s.classList.toggle('active', s.getAttribute('onclick') && s.getAttribute('onclick').includes("'"+id+"'"));
  });
}

function toggleSub(subId, btn, sectionId) {
  clearActiveNav();
  btn.classList.add('active');
  const sub = document.getElementById(subId);
  const isOpen = sub.classList.contains('open');
  document.querySelectorAll('.nav-sub').forEach(s => s.classList.remove('open'));
  if (!isOpen) sub.classList.add('open');
  showSection(sectionId);
}
</script>

</body>
</html>
