# Gully_cricket_score_clac
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GullyScore Pro - Live Local Sync Edition</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --accent: #10b981;
            --accent-glow: rgba(16, 185, 129, 0.4);
            --danger: #ef4444;
            --danger-glow: rgba(239, 68, 68, 0.4);
            --warning: #f59e0b;
            --warning-glow: rgba(245, 158, 11, 0.4);
            --info: #3b82f6;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: "Plus Jakarta Sans", -apple-system, BlinkMacSystemFont, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 20px;
            display: flex;
            justify-content: center;
            min-height: 100vh;
        }

        .container {
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 16px;
        }

        header h1 {
            color: var(--accent);
            font-size: 2.2rem;
            font-weight: 800;
            letter-spacing: -1px;
        }

        header p {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 4px;
        }

        nav {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            background-color: var(--card-bg);
            padding: 6px;
            border-radius: 12px;
            margin-bottom: 16px;
        }

        nav button {
            background: transparent;
            border: none;
            color: var(--text-muted);
            padding: 10px;
            font-weight: 600;
            font-size: 0.85rem;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        nav button.active {
            background-color: var(--accent);
            color: #fff;
            box-shadow: 0 0 12px var(--accent-glow);
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 16px;
            padding: 20px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
            margin-bottom: 16px;
        }

        .hidden { display: none !important; }

        .form-group {
            margin-bottom: 14px;
        }

        .form-group label {
            display: block;
            margin-bottom: 6px;
            font-size: 0.9rem;
            color: var(--text-muted);
            font-weight: 600;
        }

        input, select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #334155;
            background-color: #0f172a;
            color: #fff;
            font-size: 1rem;
        }

        .btn {
            width: 100%;
            padding: 14px;
            background-color: var(--accent);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .btn:hover {
            background-color: #059669;
            box-shadow: 0 0 15px var(--accent-glow);
        }

        .team-grid-layout {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
            margin-bottom: 20px;
        }

        @media (max-width: 480px) {
            .team-grid-layout { grid-template-columns: 1fr; }
        }

        .team-squad-column {
            background-color: #0f172a;
            padding: 16px;
            border-radius: 12px;
            border: 1px solid #334155;
        }

        .player-entry-row {
            display: flex;
            gap: 6px;
            margin-bottom: 8px;
        }

        .player-entry-row input { padding: 8px 10px; font-size: 0.9rem; }

        .btn-remove-player {
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 6px;
            padding: 8px 12px;
            cursor: pointer;
        }

        .btn-add-player {
            background-color: #334155;
            color: var(--text-main);
            border: none;
            border-radius: 6px;
            padding: 8px 12px;
            font-size: 0.85rem;
            cursor: pointer;
            width: 100%;
            margin-top: 8px;
        }

        .share-widget { display: flex; gap: 8px; margin-bottom: 14px; }
        .btn-share { background-color: var(--info); cursor: pointer; border: none; border-radius: 8px; color: white; font-weight: 700; }

        .batsmen-box {
            background-color: #0f172a;
            border-radius: 10px;
            padding: 14px;
            margin-bottom: 16px;
            border: 1px solid #334155;
        }

        .batsman-row { display: flex; justify-content: space-between; padding: 8px 0; color: var(--text-muted); }
        .batsman-row.on-strike { color: var(--text-main); font-weight: 700; border-left: 3px solid var(--accent); padding-left: 6px; }
        .batsman-stats { font-variant-numeric: tabular-nums; font-weight: 700; color: var(--text-main); }

        .score-display { text-align: center; margin: 10px 0; }
        .main-score { font-size: 3.8rem; font-weight: 800; }
        .overs-display { font-size: 1.2rem; color: var(--text-muted); }

        .target-box {
            background: rgba(245, 158, 11, 0.1);
            border: 1px solid var(--warning);
            color: var(--warning);
            padding: 10px;
            border-radius: 8px;
            text-align: center;
            font-weight: 700;
            margin-bottom: 14px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 16px;
            text-align: center;
            background: #0f172a;
            padding: 12px;
            border-radius: 8px;
        }

        .keypad { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-bottom: 14px; }
        .key {
            padding: 16px 0; font-size: 1.2rem; font-weight: 700; background-color: #334155;
            color: white; border: none; border-radius: 8px; cursor: pointer; transition: all 0.2s;
        }
        .key.wicket { background-color: var(--danger); }
        .key.extra { background-color: #475569; font-size: 0.95rem; }

        .action-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 12px; }
        .btn-undo { background-color: #475569; }
        .btn-warn { background-color: var(--warning); color: black; }
        .btn-exit { background-color: #475569; opacity: 0.75; }
        .btn-exit:hover { background-color: var(--danger); opacity: 1; }

        .balls-row { display: flex; gap: 6px; overflow-x: auto; padding: 8px 0; }
        .ball-dot {
            min-width: 36px; height: 36px; border-radius: 50%; background: #334155;
            display: flex; align-items: center; justify-content: center; font-size: 0.85rem; font-weight: 700;
        }
        .ball-dot.wkt { background: var(--danger); }
        .ball-dot.boundary { background: var(--accent); }
        .ball-dot.ext { background: var(--warning); color: #000; }

        .spectator-badge {
            background-color: var(--danger);
            color: white;
            text-align: center;
            padding: 8px;
            border-radius: 8px;
            font-weight: 700;
            font-size: 0.9rem;
            margin-bottom: 14px;
            letter-spacing: 0.5px;
        }

        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.85); display: flex; align-items: center; justify-content: center; padding: 20px; z-index: 100;
        }
        .modal-content { background: var(--card-bg); border-radius: 16px; padding: 24px; width: 100%; max-width: 400px; border: 1px solid #334155; }

        .over-alert-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.95);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            z-index: 200; opacity: 0; pointer-events: none;
            transition: opacity 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .over-alert-overlay.show { opacity: 1; pointer-events: auto; }
        .over-alert-title {
            font-size: 2.5rem; font-weight: 800; color: var(--warning);
            letter-spacing: 2px; transform: scale(0.7);
            transition: transform 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        .over-alert-overlay.show .over-alert-title { transform: scale(1); }
        .over-alert-subtitle { font-size: 1.2rem; color: var(--text-muted); margin-top: 8px; }
    </style>
</head>
<body>

<div id="over-alert-screen" class="over-alert-overlay">
    <div class="over-alert-title" id="over-alert-title-text">OVER COMPLETED</div>
    <div class="over-alert-subtitle" id="over-alert-stats-text">0 Runs • 0 Wickets</div>
</div>

<div class="container">
    <header>
        <h1>GullyScore Pro 🏏</h1>
        <p>Advanced Live Grid Scoring Matrix</p>
    </header>

    <nav>
        <button id="nav-dash" class="active" onclick="switchTab('dashboard')">Dashboard</button>
        <button id="nav-match" onclick="switchTab('match')">Match Room</button>
        <button id="nav-spec" onclick="switchTab('spectate')">Spectate</button>
    </nav>

    <!-- DASHBOARD VIEW -->
    <div id="dashboard-view" class="card">
        <h3>Live Broadcast Dashboard</h3>
        <p style="color: var(--text-muted); margin-top:8px; font-size:0.95rem; margin-bottom:16px;">Initiate an active room match to stream analytics.</p>
        <button class="btn" onclick="switchTab('match')">Go to Match Setup ➔</button>
    </div>

    <!-- SPECTATE VIEW -->
    <div id="spectate-view" class="card hidden">
        <h3>Live Spectator Room</h3>
        <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 10px;">Enter the Room Code generated by the scorer (e.g., GULLY-1234):</p>
        <input type="text" id="spectate-input-url" placeholder="Enter Room Code here..." style="margin-bottom: 14px;">
        <button class="btn btn-share" style="width:100%; padding:14px;" onclick="syncSpectatorStream()">Sync Spectate Stream</button>
    </div>

    <!-- SETUP SCREEN -->
    <div id="setup-screen" class="card hidden">
        <h3 style="margin-bottom: 16px;">Team Grid Profiles</h3>
        
        <div class="team-grid-layout">
            <div class="team-squad-column">
                <div class="form-group">
                    <label>Team 1 Name</label>
                    <input type="text" id="team1-name" value="Titans">
                </div>
                <label style="font-size:0.85rem; color:var(--text-muted); font-weight:700; display:block; margin-bottom:6px;">Player Roster</label>
                <div id="t1-players-container"></div>
                <button class="btn-add-player" onclick="addPlayerRow('t1', '')">+ Add Batter</button>
            </div>

            <div class="team-squad-column">
                <div class="form-group">
                    <label>Team 2 Name</label>
                    <input type="text" id="team2-name" value="Knights">
                </div>
                <label style="font-size:0.85rem; color:var(--text-muted); font-weight:700; display:block; margin-bottom:6px;">Player Roster</label>
                <div id="t2-players-container"></div>
                <button class="btn-add-player" onclick="addPlayerRow('t2', '')">+ Add Batter</button>
            </div>
        </div>

        <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px; margin-bottom: 16px;">
            <div class="form-group">
                <label>Overs</label>
                <input type="number" id="match-overs" value="2">
            </div>
            <div class="form-group">
                <label>Max Wickets</label>
                <input type="number" id="match-wickets" value="3">
            </div>
        </div>
        <button class="btn" onclick="startMatch()">Lock Squads & Start Match ➔</button>
    </div>

    <!-- SCORER SCREEN -->
    <div id="scorer-screen" class="card hidden">
        <div id="spectator-view-badge" class="spectator-badge hidden">👁️ SPECTATOR VIEW ONLY (AUTO-REFRESHING)</div>

        <div class="share-widget" id="share-widget-container">
            <input type="text" id="broadcast-link-url" readonly style="font-size:0.85rem; color:var(--text-muted);">
            <button class="btn btn-share" style="width:auto; white-space:nowrap; padding: 0 14px;" onclick="copyShareLink()">Copy Code 📋</button>
        </div>

        <div class="match-info">
            <span id="display-teams"></span> | <span id="display-innings"></span>
        </div>

        <div id="target-container" class="target-box hidden">
            Target: <span id="target-score">0</span> (Req: <span id="req-rr">0.00</span> rpo)
        </div>

        <div class="score-display">
            <div class="main-score"><span id="runs">0</span> / <span id="wickets">0</span></div>
            <div class="overs-display">Overs: <span id="overs">0.0</span> / <span id="max-overs">5</span></div>
        </div>

        <div class="batsmen-box">
            <div id="striker-row" class="batsman-row on-strike">
                <span><span id="striker-name">-</span> *</span>
                <span class="batsman-stats" id="striker-stats">0 (0)</span>
            </div>
            <div id="nonstriker-row" class="batsman-row">
                <span><span id="nonstriker-name">-</span></span>
                <span class="batsman-stats" id="nonstriker-stats">0 (0)</span>
            </div>
        </div>

        <div class="stats-grid">
            <div>
                <div style="font-size:0.8rem; color:var(--text-muted)">CRR</div>
                <div style="font-size:1.1rem; font-weight:700" id="crr">0.00</div>
            </div>
            <div>
                <div style="font-size:0.8rem; color:var(--text-muted)" id="status-label">Extras</div>
                <div style="font-size:1.1rem; font-weight:700" id="extras-disp">0</div>
            </div>
        </div>

        <div id="scorer-input-keypad" class="keypad">
            <button class="key" onclick="addRuns(0)">0</button>
            <button class="key" onclick="addRuns(1)">1</button>
            <button class="key" onclick="addRuns(2)">2</button>
            <button class="key" onclick="addRuns(3)">3</button>
            <button class="key" onclick="addRuns(4)">4</button>
            <button class="key" onclick="addRuns(6)">6</button>
            <button class="key extra" onclick="addExtra('WD')">WD</button>
            <button class="key extra" onclick="addExtra('NB')">NB</button>
            <button class="key extra" onclick="addExtra('LB')">LB</button>
            <button class="key extra" onclick="addExtra('B')">B</button>
            <button class="key wicket" style="grid-column: span 4;" onclick="triggerWicketWorkflow()">WICKET / DISMISSAL</button>
        </div>

        <div id="scorer-action-row" class="action-row">
            <button class="btn btn-undo" onclick="undoLastBall()">Undo ↩</button>
            <button class="btn btn-warn" id="next-inning-btn" onclick="switchInnings()">End Innings ➔</button>
        </div>

        <button class="btn btn-exit" style="margin-top: 4px;" onclick="exitMatchRoom()">Exit Match Room ✖</button>

        <div style="margin-top:16px;">
            <div style="font-size:0.9rem; color:var(--text-muted); font-weight:600;">This Over:</div>
            <div class="balls-row" id="this-over-balls"></div>
        </div>
    </div>
</div>

<div id="wicket-modal" class="modal hidden">
    <div class="modal-content">
        <h3 style="margin-bottom:12px;">Wicket Process Engine</h3>
        <div class="form-group">
            <label>Type of Wicket</label>
            <select id="wkt-nature-select">
                <option value="standard">Bowled/Caught/LBW</option>
                <option value="runout_striker">Runout - Striker Out</option>
                <option value="runout_nonstriker">Runout - Non-Striker Out</option>
            </select>
        </div>
        <div class="form-group">
            <label>Choose Incoming Batsman</label>
            <select id="incoming-batsman-dropdown"></select>
        </div>
        <button class="btn" onclick="submitWicketOutcome()">Confirm Wicket ➔</button>
    </div>
</div>

<script>
    let isMatchStarted = false;
    let isSpectatorMode = false;
    let match = {};
    let activeRefreshInterval = null;

    function getFreshMatchObject() {
        return {
            roomId: "", team1: "", team2: "", maxOvers: 5, maxWickets: 10, currentInnings: 1, isFinished: false, matchResult: "",
            t1Players: [], t2Players: [],
            inn1: { runs: 0, wickets: 0, balls: 0, extras: 0, history: [], strikerName: "", nonStrikerName: "", playerData: {}, retiredList: [] },
            inn2: { runs: 0, wickets: 0, balls: 0, extras: 0, history: [], strikerName: "", nonStrikerName: "", playerData: {}, retiredList: [] }
        };
    }

    match = getFreshMatchObject();
    const defaultT1 = ["Virat", "Rohit", "Rahul", "Hardik", "Jadeja"];
    const defaultT2 = ["Dhoni", "Sky", "Rinku", "Axar", "Bumrah"];

    window.onload = function() {
        defaultT1.forEach(p => addPlayerRow('t1', p));
        defaultT2.forEach(p => addPlayerRow('t2', p));
    };

    function addPlayerRow(team, value) {
        let container = document.getElementById(`${team}-players-container`);
        let row = document.createElement('div');
        row.className = "player-entry-row";
        row.innerHTML = `
            <input type="text" class="${team}-player-name-input" value="${value}">
            <button class="btn-remove-player" onclick="this.parentElement.remove()">×</button>
        `;
        container.appendChild(row);
    }

    function switchTab(tab) {
        if (activeRefreshInterval && tab !== 'match') {
            clearInterval(activeRefreshInterval);
            activeRefreshInterval = null;
        }

        document.getElementById('nav-dash').classList.remove('active');
        document.getElementById('nav-match').classList.remove('active');
        document.getElementById('nav-spec').classList.remove('active');
        document.getElementById('dashboard-view').classList.add('hidden');
        document.getElementById('spectate-view').classList.add('hidden');
        document.getElementById('setup-screen').classList.add('hidden');
        document.getElementById('scorer-screen').classList.add('hidden');

        if (tab === 'dashboard') {
            document.getElementById('nav-dash').classList.add('active');
            document.getElementById('dashboard-view').classList.remove('hidden');
        } else if (tab === 'spectate') {
            document.getElementById('nav-spec').classList.add('active');
            document.getElementById('spectate-view').classList.remove('hidden');
        } else if (tab === 'match') {
            document.getElementById('nav-match').classList.add('active');
            if (isMatchStarted) {
                document.getElementById('scorer-screen').classList.remove('hidden');
                if (isSpectatorMode) startSpectatorAutoRefresh();
            }
            else document.getElementById('setup-screen').classList.remove('hidden');
        }
    }

    function generateBroadcastID() {
        let randId = "GULLY-" + Math.floor(1000 + Math.random() * 9000);
        match.roomId = randId;
        document.getElementById('broadcast-link-url').value = randId;
        saveMatchState();
    }

    function copyShareLink() {
        let linkElem = document.getElementById('broadcast-link-url');
        linkElem.select();
        try {
            document.execCommand('copy');
            alert(`Room Code copied: ${linkElem.value}. Share this with spectators!`);
        } catch (err) {
            navigator.clipboard.writeText(linkElem.value).then(() => alert(`Room Code copied: ${linkElem.value}`));
        }
    }

    function saveMatchState() {
        if (!isSpectatorMode && match.roomId) {
            localStorage.setItem(match.roomId, JSON.stringify(match));
        }
    }

    function syncSpectatorStream() {
        let rawInput = document.getElementById('spectate-input-url').value.trim().toUpperCase();
        if(!rawInput) {
            alert("Please type a valid Live Room reference code.");
            return;
        }

        let savedData = localStorage.getItem(rawInput);
        if (!savedData) {
            alert("No live matches found with that Room Code. Please verify the code entered by the scorer.");
            return;
        }

        match = JSON.parse(savedData);
        isMatchStarted = true;
        isSpectatorMode = true; 

        document.getElementById('broadcast-link-url').value = match.roomId;
        
        document.getElementById('spectator-view-badge').classList.remove('hidden');
        document.getElementById('scorer-input-keypad').classList.add('hidden');
        document.getElementById('scorer-action-row').classList.add('hidden');
        document.getElementById('share-widget-container').classList.add('hidden');

        document.getElementById('spectate-view').classList.add('hidden');
        document.getElementById('scorer-screen').classList.remove('hidden');
        document.getElementById('nav-spec').classList.remove('active');
        document.getElementById('nav-match').classList.add('active');
        
        updateUI();
        startSpectatorAutoRefresh();
        alert(`Successfully connected to Room: ${match.roomId}! Screen will mirror live updates.`);
    }

    function startSpectatorAutoRefresh() {
        if (activeRefreshInterval) clearInterval(activeRefreshInterval);
        activeRefreshInterval = setInterval(() => {
            if (isSpectatorMode && match.roomId) {
                let freshData = localStorage.getItem(match.roomId);
                if (freshData) {
                    match = JSON.parse(freshData);
                    updateUI();
                }
            }
        }, 1000);
    }

    function initPlayerDataStructure(inn, squad) {
        inn.playerData = {};
        squad.forEach(name => { inn.playerData[name] = { runs: 0, balls: 0, active: false }; });
        inn.strikerName = squad[0] || "Player 1";
        inn.nonStrikerName = squad[1] || "Player 2";
        if(inn.playerData[inn.strikerName]) inn.playerData[inn.strikerName].active = true;
        if(inn.playerData[inn.nonStrikerName]) inn.playerData[inn.nonStrikerName].active = true;
    }

    function startMatch() {
        match = getFreshMatchObject();
        match.team1 = document.getElementById('team1-name').value || "Titans";
        match.team2 = document.getElementById('team2-name').value || "Knights";
        match.maxOvers = parseInt(document.getElementById('match-overs').value) || 2;
        match.maxWickets = parseInt(document.getElementById('match-wickets').value) || 3;

        match.t1Players = Array.from(document.querySelectorAll('.t1-player-name-input')).map(i => i.value.trim()).filter(v => v !== "");
        match.t2Players = Array.from(document.querySelectorAll('.t2-player-name-input')).map(i => i.value.trim()).filter(v => v !== "");

        if (match.t1Players.length < 2 || match.t2Players.length < 2) {
            alert("Roster configuration requires at least 2 players per team.");
            return;
        }

        initPlayerDataStructure(match.inn1, match.t1Players);
        initPlayerDataStructure(match.inn2, match.t2Players);

        isMatchStarted = true;
        isSpectatorMode = false; 
        
        document.getElementById('spectator-view-badge').classList.add('hidden');
        document.getElementById('scorer-input-keypad').classList.remove('hidden');
        document.getElementById('scorer-action-row').classList.remove('hidden');
        document.getElementById('share-widget-container').classList.remove('hidden');

        generateBroadcastID();
        document.getElementById('setup-screen').classList.add('hidden');
        document.getElementById('scorer-screen').classList.remove('hidden');
        document.getElementById('next-inning-btn').innerText = "End Innings ➔";
        updateUI();
    }

    function forceExitToDashboard() {
        if(activeRefreshInterval) clearInterval(activeRefreshInterval);
        if(!isSpectatorMode && match.roomId) localStorage.removeItem(match.roomId);
        isMatchStarted = false;
        isSpectatorMode = false;
        match = getFreshMatchObject();
        document.getElementById('scorer-screen').classList.add('hidden');
        document.getElementById('setup-screen').classList.remove('hidden');
        switchTab('dashboard');
    }

    function exitMatchRoom() {
        if(confirm("Exit match room? Unsaved sessions will stop updating.")) {
            forceExitToDashboard();
        }
    }

    function getActiveInnings() { return match.currentInnings === 1 ? match.inn1 : match.inn2; }
    function getActiveBattingSquad() { return match.currentInnings === 1 ? match.t1Players : match.t2Players; }

    function rotateStrike() {
        let inn = getActiveInnings();
        let temp = inn.strikerName;
        inn.strikerName = inn.nonStrikerName;
        inn.nonStrikerName = temp;
    }

    function triggerOverCompletionAlert(overNumber) {
        let inn = getActiveInnings();
        let startIndex = Math.max(0, inn.history.length - 6);
        let overHistory = inn.history.slice(startIndex);
        let overRuns = overHistory.reduce((sum, item) => sum + item.runsAdded, 0);
        let overWickets = overHistory.reduce((sum, item) => sum + (item.type === 'wicket' ? 1 : 0), 0);

        document.getElementById('over-alert-title-text').innerText = `OVER ${overNumber} COMPLETED`;
        document.getElementById('over-alert-stats-text').innerText = `${overRuns} Runs • ${overWickets} Wicket(s) | Total: ${inn.runs}/${inn.wickets}`;
        
        let screen = document.getElementById('over-alert-screen');
        screen.classList.add('show');
        setTimeout(() => { screen.classList.remove('show'); }, 2000);
    }

    function addRuns(runs) {
        if(isSpectatorMode || match.isFinished) return;
        let inn = getActiveInnings();
        if (!inn || inn.wickets >= match.maxWickets || inn.balls >= (match.maxOvers * 6)) return;

        inn.runs += runs; inn.balls += 1;
        if(inn.playerData && inn.playerData[inn.strikerName]) {
            inn.playerData[inn.strikerName].runs += runs;
            inn.playerData[inn.strikerName].balls += 1;
        }

        let strikeRotated = false;
        if (runs % 2 !== 0) { rotateStrike(); strikeRotated = true; }

        let overFinished = (inn.balls % 6 === 0);
        let completedOverNum = overFinished ? (inn.balls / 6) : 0;
        if (overFinished) rotateStrike();

        inn.history.push({ 
            type: 'normal', runsAdded: runs, extraAdded: 0, legalBall: true, affectedBatter: inn.strikerName,
            strikeRotated: strikeRotated, overFinished: overFinished, display: runs === 4 || runs === 6 ? runs + '!' : runs 
        });

        saveMatchState();
        updateUI();
        if(overFinished) triggerOverCompletionAlert(completedOverNum);
        checkEndInningsCondition();
    }

    function addExtra(type) {
        if(isSpectatorMode || match.isFinished) return; 
        let inn = getActiveInnings();
        if (!inn || inn.wickets >= match.maxWickets || inn.balls >= (match.maxOvers * 6)) return;

        let strikeRotated = false;
        let overFinished = false;
        let completedOverNum = 0;

        if (type === 'WD') {
            inn.extras += 1; inn.runs += 1;
            inn.history.push({ type: 'extra', runsAdded: 1, extraAdded: 1, legalBall: false, strikeRotated: false, overFinished: false, display: type });
        } 
        else if (type === 'NB') {
            let batRunInput = prompt("How many runs were scored off the bat on this No-Ball? (Enter 0 if none)", "0");
            let batRuns = parseInt(batRunInput);
            if (isNaN(batRuns) || batRuns < 0) return;

            let totalNbRuns = 1 + batRuns;
            inn.extras += 1; 
            inn.runs += totalNbRuns;
            
            if(inn.playerData && inn.playerData[inn.strikerName]) {
                inn.playerData[inn.strikerName].runs += batRuns;
                inn.playerData[inn.strikerName].balls += 1;
            }

            if (batRuns % 2 !== 0) { rotateStrike(); strikeRotated = true; }

            inn.history.push({ 
                type: 'extra', runsAdded: totalNbRuns, extraAdded: 1, legalBall: false, 
                strikeRotated: strikeRotated, overFinished: false, affectedBatter: inn.strikerName,
                display: batRuns > 0 ? `${batRuns}+NB` : 'NB' 
            });
        } 
        else if (type === 'LB' || type === 'B') {
            let runInput = prompt(`Runs taken via ${type}?`, "1");
            let extraRuns = parseInt(runInput);
            if (isNaN(extraRuns) || extraRuns < 0) return;

            inn.extras += extraRuns; inn.runs += extraRuns; inn.balls += 1;
            if(inn.playerData && inn.playerData[inn.strikerName]) inn.playerData[inn.strikerName].balls += 1;

            if (extraRuns % 2 !== 0) { rotateStrike(); strikeRotated = true; }
            if (inn.balls % 6 === 0) { overFinished = true; completedOverNum = (inn.balls / 6); rotateStrike(); }

            inn.history.push({ type: 'extra', runsAdded: extraRuns, extraAdded: extraRuns, legalBall: true, strikeRotated: strikeRotated, overFinished: overFinished, display: `${extraRuns}${type}` });
        }

        saveMatchState();
        updateUI();
        if(overFinished && completedOverNum > 0) triggerOverCompletionAlert(completedOverNum);
        checkEndInningsCondition();
    }

    function triggerWicketWorkflow() {
        if(isSpectatorMode || match.isFinished) return; 
        let inn = getActiveInnings();
        if (inn.wickets >= match.maxWickets) return;

        let squad = getActiveBattingSquad();
        let availableNext = squad.filter(p => !inn.retiredList.includes(p) && p !== inn.strikerName && p !== inn.nonStrikerName);
        let selectDropdown = document.getElementById('incoming-batsman-dropdown');
        selectDropdown.innerHTML = "";

        if(availableNext.length === 0) {
            let option = document.createElement('option');
            option.value = "ALL_OUT_NO_SUB"; option.innerText = "No remaining batsmen";
            selectDropdown.appendChild(option);
        } else {
            availableNext.forEach(player => {
                let option = document.createElement('option');
                option.value = player; option.innerText = player;
                selectDropdown.appendChild(option);
            });
        }
        document.getElementById('wicket-modal').classList.remove('hidden');
    }

    function submitWicketOutcome() {
        if(isSpectatorMode || match.isFinished) return;
        let inn = getActiveInnings();
        let nature = document.getElementById('wkt-nature-select').value;
        let chosenIncoming = document.getElementById('incoming-batsman-dropdown').value;
        document.getElementById('wicket-modal').classList.add('hidden');

        let outgoingBatter = (nature === 'standard' || nature === 'runout_striker') ? inn.strikerName : inn.nonStrikerName;
        inn.wickets += 1; inn.balls += 1;
        inn.retiredList.push(outgoingBatter);

        let backupStriker = inn.strikerName; let backupNonStriker = inn.nonStrikerName;
        if (chosenIncoming !== "ALL_OUT_NO_SUB") {
            if (nature === 'standard' || nature === 'runout_striker') inn.strikerName = chosenIncoming;
            else inn.nonStrikerName = chosenIncoming;
        }

        let overFinished = (inn.balls % 6 === 0);
        let completedOverNum = overFinished ? (inn.balls / 6) : 0;
        if (overFinished) rotateStrike();

        inn.history.push({
            type: 'wicket', runsAdded: 0, extraAdded: 0, legalBall: true, nature: nature, outgoing: outgoingBatter, 
            incoming: chosenIncoming, prevStriker: backupStriker, prevNonStriker: backupNonStriker, overFinished: overFinished, display: 'W'
        });

        saveMatchState();
        updateUI();
        if(overFinished) triggerOverCompletionAlert(completedOverNum);
        checkEndInningsCondition();
    }

    function undoLastBall() {
        if(isSpectatorMode || match.isFinished) return;
        let inn = getActiveInnings();
        if (!inn || inn.history.length === 0) return;

        let last = inn.history.pop();
        inn.runs -= last.runsAdded; inn.extras -= last.extraAdded;
        if (last.legalBall) inn.balls -= 1;

        if (last.type === 'wicket') {
            inn.wickets -= 1; inn.retiredList.pop();
            inn.strikerName = last.prevStriker; inn.nonStrikerName = last.prevNonStriker;
        } else if (last.type === 'normal') {
            if (inn.playerData && inn.playerData[last.affectedBatter]) {
                inn.playerData[last.affectedBatter].runs -= last.runsAdded;
                inn.playerData[last.affectedBatter].balls -= 1;
            }
            if (last.overFinished) rotateStrike();
            if (last.strikeRotated) rotateStrike();
        } else if (last.type === 'extra') {
            if (String(last.display).includes('NB')) {
                let batRunsSubtracted = last.runsAdded - 1; 
                if (inn.playerData && inn.playerData[last.affectedBatter]) {
                    inn.playerData[last.affectedBatter].runs -= batRunsSubtracted;
                    inn.playerData[last.affectedBatter].balls -= 1;
                }
            }
            if (last.overFinished) rotateStrike();
            if (last.strikeRotated) rotateStrike();
        }
        saveMatchState();
        updateUI();
    }

    function checkEndInningsCondition() {
        let inn = getActiveInnings();
        if (!inn) return;
        
        if (match.currentInnings === 2 && inn.runs > match.inn1.runs) {
            declareWinner();
            return;
        }

        if (inn.wickets >= match.maxWickets || inn.balls >= (match.maxOvers * 6)) {
            if (match.currentInnings === 1) {
                if(!isSpectatorMode) {
                    document.getElementById('next-inning-btn').innerText = "Start 2nd Innings ➔";
                }
            } else { declareWinner(); }
        }
    }

    function switchInnings() {
        if(isSpectatorMode || match.isFinished) return;
        if (match.currentInnings === 1) {
            match.currentInnings = 2;
            document.getElementById('next-inning-btn').innerText = "Finish Match 🏆";
            saveMatchState();
            updateUI();
        } else { declareWinner(); }
    }

    function declareWinner() {
        let r1 = match.inn1.runs; let r2 = match.inn2.runs;
        let msg = (r2 > r1) ? `${match.team2} won! 🎉` : (r1 > r2) ? `${match.team1} won! 🎉` : "Match Tie!";
        
        match.isFinished = true;
        match.matchResult = msg;
        saveMatchState();
        updateUI();

        // Let the UI process the update before spawning the blocking alert box
        setTimeout(() => {
            alert(msg);
            forceExitToDashboard();
        }, 100);
    }

    function updateUI() {
        let inn = getActiveInnings();
        if(!inn) return;

        // Check if the running spectator loop reads a finalized match room object
        if (isSpectatorMode && match.isFinished) {
            clearInterval(activeRefreshInterval); // Stop double interval firing
            activeRefreshInterval = null;
            setTimeout(() => {
                alert("Match Broadcast Finished!\n" + match.matchResult);
                forceExitToDashboard();
            }, 100);
            return;
        }
        
        document.getElementById('striker-name').innerText = inn.strikerName || "-";
        let sRuns = (inn.playerData && inn.playerData[inn.strikerName]) ? inn.playerData[inn.strikerName].runs : 0;
        let sBalls = (inn.playerData && inn.playerData[inn.strikerName]) ? inn.playerData[inn.strikerName].balls : 0;
        document.getElementById('striker-stats').innerText = `${sRuns} (${sBalls})`;

        document.getElementById('nonstriker-name').innerText = inn.nonStrikerName || "-";
        let nsRuns = (inn.playerData && inn.playerData[inn.nonStrikerName]) ? inn.playerData[inn.nonStrikerName].runs : 0;
        let nsBalls = (inn.playerData && inn.playerData[inn.nonStrikerName]) ? inn.playerData[inn.nonStrikerName].balls : 0;
        document.getElementById('nonstriker-stats').innerText = `${nsRuns} (${nsBalls})`;

        if (match.currentInnings === 1) {
            document.getElementById('display-teams').innerText = `${match.team1 || "Team 1"} vs ${match.team2 || "Team 2"}`;
            document.getElementById('display-innings').innerText = `Innings 1`;
            document.getElementById('target-container').classList.add('hidden');
            document.getElementById('status-label').innerText = "Extras";
            document.getElementById('extras-disp').innerText = inn.extras;
        } else {
            document.getElementById('display-teams').innerText = `${match.team2 || "Team 2"} vs ${match.team1 || "Team 1"}`;
            document.getElementById('display-innings').innerText = `Innings 2`;
            document.getElementById('target-container').classList.remove('hidden');
            
            let target = (match.inn1 ? match.inn1.runs : 0) + 1;
            document.getElementById('target-score').innerText = target;
            let needed = target - inn.runs; let ballsLeft = (match.maxOvers * 6) - inn.balls;
            
            if (needed > 0 && ballsLeft > 0) {
                document.getElementById('req-rr').innerText = (needed / (ballsLeft / 6)).toFixed(2);
                document.getElementById('status-label').innerText = "Need";
                document.getElementById('extras-disp').innerText = `${needed} off ${ballsLeft}b`;
            } else {
                document.getElementById('status-label').innerText = "Extras";
                document.getElementById('extras-disp').innerText = inn.extras;
            }
        }

        document.getElementById('runs').innerText = inn.runs;
        document.getElementById('wickets').innerText = inn.wickets;
        document.getElementById('overs').innerText = `${Math.floor(inn.balls/6)}.${inn.balls%6}`;
        document.getElementById('max-overs').innerText = match.maxOvers;
        document.getElementById('crr').innerText = inn.balls > 0 ? (inn.runs / (inn.balls/6)).toFixed(2) : "0.00";

        let timeline = document.getElementById('this-over-balls');
        timeline.innerHTML = ""; 
        
        let lastOverCount = inn.balls % 6 === 0 && inn.balls > 0 ? 6 : inn.balls % 6;
        let recent = inn.history ? inn.history.slice(-lastOverCount) : [];
        if (recent.length === 0) timeline.innerHTML = "<span>Ready</span>";
        
        recent.forEach(b => {
            let dot = document.createElement('div');
            dot.className = "ball-dot"; dot.innerText = b.display;
            if (b.type === 'wicket') dot.classList.add('wkt');
            else if (b.runsAdded === 4 || b.runsAdded === 6 || String(b.display).includes('4') || String(b.display).includes('6')) dot.classList.add('boundary');
            else if (b.type === 'extra') dot.classList.add('ext');
            timeline.appendChild(dot);
        });
    }
</script>
</body>
</html>
