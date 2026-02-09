<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BorderShield AI - Command & Control Center</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-primary: #0f1419;
            --bg-secondary: #1a1f2e;
            --bg-tertiary: #252d3d;
            --accent-blue: #3b82f6;
            --accent-green: #10b981;
            --accent-yellow: #f59e0b;
            --accent-red: #ef4444;
            --accent-purple: #8b5cf6;
            --text-primary: #f1f5f9;
            --text-secondary: #94a3b8;
            --border-color: #334155;
        }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            overflow-x: hidden;
        }

        .header {
            background: var(--bg-secondary);
            border-bottom: 1px solid var(--border-color);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo-section {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .logo-icon {
            width: 45px;
            height: 45px;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        .logo-text h1 {
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--accent-blue), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .logo-text p {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        .header-actions {
            display: flex;
            gap: 1rem;
            align-items: center;
        }

        .status-badge {
            padding: 0.5rem 1rem;
            background: rgba(16, 185, 129, 0.1);
            border: 1px solid var(--accent-green);
            border-radius: 6px;
            font-size: 0.85rem;
            color: var(--accent-green);
            font-weight: 600;
        }

        .status-badge.alert {
            background: rgba(239, 68, 68, 0.1);
            border-color: var(--accent-red);
            color: var(--accent-red);
        }

        .main-grid {
            display: grid;
            grid-template-columns: 320px 1fr 380px;
            gap: 1rem;
            padding: 1rem;
            min-height: calc(100vh - 80px);
        }

        .panel {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            max-height: calc(100vh - 100px);
        }

        .panel-header {
            padding: 1rem 1.25rem;
            background: var(--bg-tertiary);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .panel-title {
            font-weight: 600;
            font-size: 0.95rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .panel-body {
            padding: 1.25rem;
            overflow-y: auto;
            flex: 1;
        }

        /* Historical Comparison */
        .comparison-section {
            background: var(--bg-tertiary);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1rem;
            margin-bottom: 1rem;
        }

        .comparison-header {
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: var(--accent-blue);
        }

        .time-selector {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .time-btn {
            padding: 0.6rem;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.85rem;
            font-weight: 500;
        }

        .time-btn.active {
            background: var(--accent-blue);
            color: white;
            border-color: var(--accent-blue);
        }

        .time-btn:hover {
            border-color: var(--accent-blue);
        }

        .stat-compare {
            display: grid;
            gap: 0.8rem;
            max-height: 300px;
            overflow-y: auto;
            padding-right: 0.5rem;
        }

        .stat-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.8rem;
            background: var(--bg-primary);
            border-radius: 6px;
        }

        .stat-label {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        .stat-value {
            font-size: 1.1rem;
            font-weight: 700;
        }

        .stat-change {
            font-size: 0.75rem;
            margin-top: 0.2rem;
        }

        .stat-change.up {
            color: var(--accent-red);
        }

        .stat-change.down {
            color: var(--accent-green);
        }

        /* Sector Selection */
        .sector-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            margin-bottom: 1rem;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 0.5rem;
        }

        .sector-card {
            padding: 1rem;
            background: var(--bg-tertiary);
            border: 2px solid var(--border-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
        }

        .sector-card:hover {
            border-color: var(--accent-blue);
            transform: translateY(-2px);
        }

        .sector-card.selected {
            border-color: var(--accent-blue);
            background: rgba(59, 130, 246, 0.1);
        }

        .sector-card.high-risk {
            border-color: var(--accent-red);
        }

        .sector-card.medium-risk {
            border-color: var(--accent-yellow);
        }

        .sector-card.low-risk {
            border-color: var(--accent-green);
        }

        .sector-name {
            font-weight: 600;
            font-size: 0.85rem;
            margin-bottom: 0.3rem;
        }

        .sector-risk {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        .sector-traffic {
            font-size: 0.8rem;
            margin-top: 0.3rem;
            font-weight: 600;
        }

        /* AI Insights */
        .ai-insight {
            background: linear-gradient(135deg, rgba(139, 92, 246, 0.1), rgba(59, 130, 246, 0.1));
            border: 1px solid var(--accent-purple);
            border-radius: 8px;
            padding: 1rem;
            margin-bottom: 1rem;
        }

        .ai-header {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.8rem;
            font-weight: 600;
            color: var(--accent-purple);
        }

        .ai-message {
            font-size: 0.9rem;
            line-height: 1.5;
            color: var(--text-primary);
            margin-bottom: 1rem;
        }

        .ai-recommendation {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 0.5rem;
        }

        /* Action Buttons */
        .action-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.8rem;
            margin-top: 1rem;
        }

        .action-btn {
            padding: 0.9rem;
            background: var(--bg-tertiary);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-primary);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.85rem;
        }

        .action-btn:hover {
            background: var(--accent-blue);
            border-color: var(--accent-blue);
            transform: translateY(-2px);
        }

        .action-btn.primary {
            background: var(--accent-blue);
            border-color: var(--accent-blue);
        }

        .action-btn.danger {
            background: var(--accent-red);
            border-color: var(--accent-red);
        }

        .action-btn.success {
            background: var(--accent-green);
            border-color: var(--accent-green);
        }

        /* Map */
        .map-wrapper {
            position: relative;
            background: #0a0e1a;
            border-radius: 8px;
            height: 100%;
            overflow: hidden;
        }

        .map-controls {
            position: absolute;
            top: 1rem;
            left: 1rem;
            z-index: 10;
            display: flex;
            gap: 0.5rem;
        }

        .map-btn {
            padding: 0.6rem 1rem;
            background: rgba(26, 31, 46, 0.95);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: var(--text-primary);
            font-size: 0.85rem;
            cursor: pointer;
            backdrop-filter: blur(10px);
            transition: all 0.2s;
        }

        .map-btn:hover {
            background: var(--accent-blue);
            border-color: var(--accent-blue);
        }

        .map-btn.active {
            background: var(--accent-blue);
            border-color: var(--accent-blue);
        }

        .map-info {
            position: absolute;
            bottom: 1rem;
            left: 1rem;
            background: rgba(26, 31, 46, 0.95);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1rem;
            backdrop-filter: blur(10px);
            min-width: 250px;
        }

        .map-legend {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: rgba(26, 31, 46, 0.95);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1rem;
            backdrop-filter: blur(10px);
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin: 0.4rem 0;
            font-size: 0.85rem;
        }

        .legend-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }

        /* Timeline */
        .timeline {
            position: relative;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 0.5rem;
        }

        .timeline-item {
            position: relative;
            padding-left: 2rem;
            padding-bottom: 1.5rem;
            border-left: 2px solid var(--border-color);
        }

        .timeline-item:last-child {
            border-left-color: transparent;
        }

        .timeline-dot {
            position: absolute;
            left: -6px;
            top: 0;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: var(--accent-blue);
        }

        .timeline-time {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-bottom: 0.3rem;
        }

        .timeline-content {
            background: var(--bg-tertiary);
            padding: 1rem;
            border-radius: 8px;
            border-left: 3px solid var(--accent-blue);
        }

        .timeline-content.alert {
            border-left-color: var(--accent-red);
        }

        .timeline-title {
            font-weight: 600;
            font-size: 0.9rem;
            margin-bottom: 0.3rem;
        }

        .timeline-desc {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 0.5rem;
        }

        .timeline-action {
            font-size: 0.8rem;
            color: var(--accent-yellow);
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
        }

        .modal.show {
            display: flex;
        }

        .modal-content {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 2rem;
            max-width: 600px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 1rem;
        }

        .modal-body {
            margin-bottom: 1.5rem;
        }

        .option-group {
            margin-bottom: 1.5rem;
        }

        .option-label {
            font-size: 0.9rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--text-secondary);
        }

        .option-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.8rem;
        }

        .option-card {
            padding: 1rem;
            background: var(--bg-tertiary);
            border: 2px solid var(--border-color);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
        }

        .option-card:hover {
            border-color: var(--accent-blue);
        }

        .option-card.selected {
            border-color: var(--accent-blue);
            background: rgba(59, 130, 246, 0.1);
        }

        .option-icon {
            font-size: 2rem;
            margin-bottom: 0.5rem;
        }

        .option-name {
            font-weight: 600;
            font-size: 0.9rem;
        }

        .option-desc {
            font-size: 0.75rem;
            color: var(--text-secondary);
            margin-top: 0.3rem;
        }

        .modal-footer {
            display: flex;
            gap: 1rem;
            justify-content: flex-end;
        }

        .btn {
            padding: 0.8rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            border: none;
            font-size: 0.9rem;
        }

        .btn-primary {
            background: var(--accent-blue);
            color: white;
        }

        .btn-secondary {
            background: var(--bg-tertiary);
            color: var(--text-primary);
            border: 1px solid var(--border-color);
        }

        .btn:hover {
            transform: translateY(-2px);
        }

        /* CCTV Grid */
        .cctv-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0.8rem;
        }

        .cctv-feed {
            background: #000;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            aspect-ratio: 16/9;
            position: relative;
            overflow: hidden;
        }

        .cctv-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
            padding: 0.8rem;
            color: white;
        }

        .cctv-name {
            font-size: 0.85rem;
            font-weight: 600;
        }

        .cctv-status {
            font-size: 0.75rem;
            color: var(--accent-green);
        }

        .chart-container {
            height: 200px;
            margin-top: 1rem;
        }

        .scrollbar::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        .scrollbar::-webkit-scrollbar-track {
            background: var(--bg-primary);
            border-radius: 4px;
        }

        .scrollbar::-webkit-scrollbar-thumb {
            background: var(--accent-blue);
            border-radius: 4px;
        }

        .scrollbar::-webkit-scrollbar-thumb:hover {
            background: #4f92f7;
        }

        /* Firefox scrollbar */
        .scrollbar {
            scrollbar-width: thin;
            scrollbar-color: var(--accent-blue) var(--bg-primary);
        }

        .loading-spinner {
            display: inline-block;
            width: 16px;
            height: 16px;
            border: 2px solid var(--border-color);
            border-top-color: var(--accent-blue);
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @media (max-width: 1400px) {
            .main-grid {
                grid-template-columns: 280px 1fr 320px;
            }
        }

        @media (max-width: 1024px) {
            .main-grid {
                grid-template-columns: 1fr;
                min-height: auto;
            }
            
            .panel {
                height: auto;
                max-height: none;
                margin-bottom: 1rem;
            }

            .panel-body {
                max-height: 600px;
            }

            .map-wrapper {
                min-height: 500px;
            }
        }

        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                gap: 1rem;
            }

            .header-actions {
                width: 100%;
                justify-content: space-between;
            }

            .sector-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .action-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="logo-section">
            <div class="logo-icon">🛡️</div>
            <div class="logo-text">
                <h1>BorderShield AI</h1>
                <p>Command & Control Center</p>
            </div>
        </div>
        <div class="header-actions">
            <div class="status-badge">System Online</div>
            <div class="status-badge alert" id="alertBadge">0 Active Alerts</div>
            <div class="status-badge" id="clockBadge">00:00:00</div>
        </div>
    </div>

    <div class="main-grid">
        <!-- Left Panel -->
        <div class="panel">
            <div class="panel-header">
                <div class="panel-title">Intelligence & Analysis</div>
            </div>
            <div class="panel-body scrollbar">
                <!-- Historical Comparison -->
                <div class="comparison-section">
                    <div class="comparison-header">📊 Historical Data Comparison</div>
                    <div class="time-selector">
                        <button class="time-btn active" onclick="selectTime('today')">Today</button>
                        <button class="time-btn" onclick="selectTime('yesterday')">Yesterday</button>
                        <button class="time-btn" onclick="selectTime('lastYear')">Last Year</button>
                    </div>
                    <div class="stat-compare scrollbar" id="statsCompare">
                        <!-- Stats will be populated -->
                    </div>
                </div>

                <!-- AI Insights -->
                <div class="ai-insight">
                    <div class="ai-header">
                        <span>🤖</span>
                        <span>AI Analysis</span>
                    </div>
                    <div class="ai-message" id="aiMessage">
                        Traffic in Sector A-03 is 340% higher than usual. Historical data shows this is abnormal for Tuesday 14:30. Weather conditions: Foggy (visibility 2km).
                    </div>
                    <div class="ai-recommendation" id="aiRecommendation">
                        ⚠️ Recommendation: Deploy aerial surveillance to verify unusual activity
                    </div>
                </div>

                <!-- Sector Selection -->
                <div class="comparison-header" style="margin-bottom: 1rem;">🎯 Select Sector</div>
                <div class="sector-grid scrollbar" id="sectorGrid">
                    <!-- Sectors will be populated -->
                </div>
            </div>
        </div>

        <!-- Center Panel - Map -->
        <div class="panel">
            <div class="panel-header">
                <div class="panel-title">Live Border Map</div>
                <div>
                    <button class="map-btn" onclick="showCCTV()">📹 CCTV Status</button>
                </div>
            </div>
            <div class="panel-body" style="padding: 0;">
                <div class="map-wrapper">
                    <div class="map-controls">
                        <button class="map-btn active" onclick="toggleLayer('traffic')">Traffic Heat</button>
                        <button class="map-btn" onclick="toggleLayer('patrol')">Patrol Routes</button>
                        <button class="map-btn" onclick="toggleLayer('sensors')">Sensors</button>
                    </div>
                    
                    <canvas id="mapCanvas" width="1000" height="700" style="width: 100%; height: 100%;"></canvas>
                    
                    <div class="map-legend">
                        <div class="legend-item">
                            <div class="legend-dot" style="background: #ef4444;"></div>
                            <span>High Traffic/Risk</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-dot" style="background: #f59e0b;"></div>
                            <span>Medium Traffic</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-dot" style="background: #10b981;"></div>
                            <span>Normal/Low</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-dot" style="background: #3b82f6;"></div>
                            <span>Patrol Active</span>
                        </div>
                    </div>
                    
                    <div class="map-info" id="mapInfo">
                        <div style="font-weight: 600; margin-bottom: 0.5rem;">Selected: <span id="selectedSector">None</span></div>
                        <div style="font-size: 0.85rem; color: var(--text-secondary);">
                            Click any sector for detailed analysis and action options
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Right Panel - Actions -->
        <div class="panel">
            <div class="panel-header">
                <div class="panel-title">Command Actions</div>
            </div>
            <div class="panel-body scrollbar">
                <div class="action-grid">
                    <button class="action-btn primary" onclick="openActionModal('drone')">
                        <span>🚁</span>
                        <span>Deploy Drone</span>
                    </button>
                    <button class="action-btn" onclick="openActionModal('soldiers')">
                        <span>👮</span>
                        <span>Deploy Soldiers</span>
                    </button>
                    <button class="action-btn" onclick="openActionModal('officer')">
                        <span>🎖️</span>
                        <span>Call Officer</span>
                    </button>
                    <button class="action-btn" onclick="showCCTV()">
                        <span>📹</span>
                        <span>Check CCTV</span>
                    </button>
                    <button class="action-btn" onclick="openActionModal('patrol')">
                        <span>🚔</span>
                        <span>Send Patrol</span>
                    </button>
                    <button class="action-btn" onclick="openActionModal('backup')">
                        <span>📞</span>
                        <span>Request Backup</span>
                    </button>
                    <button class="action-btn success" onclick="openActionModal('analyze')">
                        <span>📊</span>
                        <span>Deep Analysis</span>
                    </button>
                    <button class="action-btn danger" onclick="openActionModal('alert')">
                        <span>🚨</span>
                        <span>Raise Alert</span>
                    </button>
                </div>

                <div style="margin-top: 1.5rem;">
                    <div class="panel-title" style="margin-bottom: 1rem;">📅 Activity Timeline</div>
                    <div class="timeline scrollbar" id="timeline">
                        <!-- Timeline items will be populated -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Action Modal -->
    <div class="modal" id="actionModal">
        <div class="modal-content">
            <div class="modal-header" id="modalTitle">Deploy Resources</div>
            <div class="modal-body">
                <div class="option-group">
                    <div class="option-label">Select Resource Type</div>
                    <div class="option-grid" id="resourceOptions">
                        <!-- Options will be populated -->
                    </div>
                </div>
                <div class="option-group">
                    <div class="option-label">Priority Level</div>
                    <div class="option-grid">
                        <div class="option-card" onclick="selectPriority('normal')">
                            <div class="option-icon">⚡</div>
                            <div class="option-name">Normal</div>
                            <div class="option-desc">Standard response</div>
                        </div>
                        <div class="option-card" onclick="selectPriority('urgent')">
                            <div class="option-icon">🚨</div>
                            <div class="option-name">Urgent</div>
                            <div class="option-desc">Immediate action</div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" onclick="closeModal()">Cancel</button>
                <button class="btn btn-primary" onclick="executeAction()">Deploy Now</button>
            </div>
        </div>
    </div>

    <!-- CCTV Modal -->
    <div class="modal" id="cctvModal">
        <div class="modal-content" style="max-width: 900px;">
            <div class="modal-header">📹 CCTV Camera Status</div>
            <div class="modal-body">
                <div class="cctv-grid" id="cctvGrid">
                    <!-- CCTV feeds will be populated -->
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" onclick="closeCCTV()">Close</button>
            </div>
        </div>
    </div>

    <script>
        // Data Storage
        let selectedSector = null;
        let selectedTime = 'today';
        let selectedAction = null;
        let activeAlerts = 3;

        const sectors = [
            { id: 'A-01', name: 'Alpha-01', risk: 'low', traffic: { today: 45, yesterday: 42, lastYear: 38 }, terrain: 'Plain' },
            { id: 'A-02', name: 'Alpha-02', risk: 'medium', traffic: { today: 78, yesterday: 52, lastYear: 48 }, terrain: 'Forest' },
            { id: 'A-03', name: 'Alpha-03', risk: 'high', traffic: { today: 152, yesterday: 45, lastYear: 41 }, terrain: 'River' },
            { id: 'B-01', name: 'Bravo-01', risk: 'low', traffic: { today: 38, yesterday: 40, lastYear: 35 }, terrain: 'Hills' },
            { id: 'B-02', name: 'Bravo-02', risk: 'medium', traffic: { today: 65, yesterday: 48, lastYear: 52 }, terrain: 'Forest' },
            { id: 'B-03', name: 'Bravo-03', risk: 'high', traffic: { today: 134, yesterday: 38, lastYear: 36 }, terrain: 'Plain' },
            { id: 'C-01', name: 'Charlie-01', risk: 'low', traffic: { today: 42, yesterday: 45, lastYear: 39 }, terrain: 'River' },
            { id: 'C-02', name: 'Charlie-02', risk: 'medium', traffic: { today: 71, yesterday: 55, lastYear: 49 }, terrain: 'Hills' },
            { id: 'C-03', name: 'Charlie-03', risk: 'high', traffic: { today: 145, yesterday: 42, lastYear: 44 }, terrain: 'Forest' },
        ];

        const timeline = [
            { time: '14:25', title: 'Unusual Traffic Detected', desc: 'Sector A-03 showing 340% increase', action: 'AI recommends immediate surveillance', type: 'alert' },
            { time: '14:18', title: 'Patrol Completed', desc: 'Unit P-04 finished route in Sector B-02', action: 'Status: All clear', type: 'normal' },
            { time: '14:05', title: 'Drone Deployed', desc: 'D-02 sent to Sector C-03 for reconnaissance', action: 'ETA: 8 minutes', type: 'normal' },
            { time: '13:52', title: 'Weather Alert', desc: 'Fog rolling into northern sectors', action: 'Visibility reduced to 2km', type: 'warning' },
            { time: '13:40', title: 'Shift Change', desc: 'New patrol units taking over', action: 'Units P-05, P-06, P-07 active', type: 'normal' },
        ];

        const cctvCameras = [
            { id: 'CAM-01', sector: 'A-03', status: 'Active', quality: '1080p' },
            { id: 'CAM-02', sector: 'B-03', status: 'Active', quality: '1080p' },
            { id: 'CAM-03', sector: 'C-03', status: 'Active', quality: '720p' },
            { id: 'CAM-04', sector: 'A-01', status: 'Maintenance', quality: 'Offline' },
        ];

        // Initialize
        function init() {
            renderSectors();
            renderStats();
            renderTimeline();
            renderMap();
            updateClock();
            setInterval(updateClock, 1000);
        }

        function updateClock() {
            const now = new Date();
            document.getElementById('clockBadge').textContent = now.toLocaleTimeString();
        }

        function renderSectors() {
            const grid = document.getElementById('sectorGrid');
            grid.innerHTML = sectors.map(sector => `
                <div class="sector-card ${sector.risk}-risk ${selectedSector === sector.id ? 'selected' : ''}" 
                     onclick="selectSectorFunc('${sector.id}')">
                    <div class="sector-name">${sector.id}</div>
                    <div class="sector-risk">${sector.risk.toUpperCase()}</div>
                    <div class="sector-traffic">${sector.traffic[selectedTime]} traffic</div>
                </div>
            `).join('');
        }

        function renderStats() {
            const container = document.getElementById('statsCompare');
            const sector = sectors.find(s => s.id === selectedSector) || sectors[2]; // Default to A-03
            
            const todayTraffic = sector.traffic.today;
            const compareTraffic = sector.traffic[selectedTime];
            const change = selectedTime === 'today' ? 0 : ((todayTraffic - compareTraffic) / compareTraffic * 100).toFixed(0);
            
            container.innerHTML = `
                <div class="stat-row">
                    <div>
                        <div class="stat-label">Current Traffic</div>
                        <div class="stat-value">${todayTraffic}</div>
                    </div>
                    ${selectedTime !== 'today' ? `
                        <div class="stat-change ${change > 0 ? 'up' : 'down'}">
                            ${change > 0 ? '↑' : '↓'} ${Math.abs(change)}%
                        </div>
                    ` : ''}
                </div>
                <div class="stat-row">
                    <div>
                        <div class="stat-label">${selectedTime === 'today' ? 'Soldiers On Duty' : selectedTime.charAt(0).toUpperCase() + selectedTime.slice(1) + ' Traffic'}</div>
                        <div class="stat-value">${selectedTime === 'today' ? '24' : compareTraffic}</div>
                    </div>
                </div>
                <div class="stat-row">
                    <div>
                        <div class="stat-label">Active Patrols</div>
                        <div class="stat-value">4</div>
                    </div>
                </div>
                <div class="stat-row">
                    <div>
                        <div class="stat-label">Sensor Status</div>
                        <div class="stat-value">47/50</div>
                    </div>
                </div>
            `;
        }

        function renderTimeline() {
            const container = document.getElementById('timeline');
            container.innerHTML = timeline.map(item => `
                <div class="timeline-item">
                    <div class="timeline-dot"></div>
                    <div class="timeline-time">${item.time}</div>
                    <div class="timeline-content ${item.type}">
                        <div class="timeline-title">${item.title}</div>
                        <div class="timeline-desc">${item.desc}</div>
                        <div class="timeline-action">${item.action}</div>
                    </div>
                </div>
            `).join('');
        }

        function renderMap() {
            const canvas = document.getElementById('mapCanvas');
            const ctx = canvas.getContext('2d');
            
            // Clear canvas
            ctx.fillStyle = '#0a0e1a';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw grid
            ctx.strokeStyle = 'rgba(59, 130, 246, 0.1)';
            ctx.lineWidth = 1;
            for (let i = 0; i < canvas.width; i += 50) {
                ctx.beginPath();
                ctx.moveTo(i, 0);
                ctx.lineTo(i, canvas.height);
                ctx.stroke();
            }
            for (let i = 0; i < canvas.height; i += 50) {
                ctx.beginPath();
                ctx.moveTo(0, i);
                ctx.lineTo(canvas.width, i);
                ctx.stroke();
            }
            
            // Draw border line
            ctx.strokeStyle = '#10b981';
            ctx.lineWidth = 3;
            ctx.setLineDash([15, 5]);
            ctx.beginPath();
            ctx.moveTo(0, 350);
            ctx.quadraticCurveTo(250, 300, 500, 350);
            ctx.quadraticCurveTo(750, 400, 1000, 350);
            ctx.stroke();
            ctx.setLineDash([]);
            
            // Draw sectors
            const sectorPositions = [
                { x: 150, y: 200 }, { x: 350, y: 250 }, { x: 550, y: 300 },
                { x: 150, y: 400 }, { x: 350, y: 450 }, { x: 550, y: 500 },
                { x: 700, y: 200 }, { x: 700, y: 400 }, { x: 850, y: 300 }
            ];
            
            sectors.forEach((sector, index) => {
                const pos = sectorPositions[index];
                const color = sector.risk === 'high' ? '#ef4444' : 
                             sector.risk === 'medium' ? '#f59e0b' : '#10b981';
                
                // Heat circle
                const gradient = ctx.createRadialGradient(pos.x, pos.y, 0, pos.x, pos.y, 60);
                gradient.addColorStop(0, color + '66');
                gradient.addColorStop(1, color + '00');
                ctx.fillStyle = gradient;
                ctx.beginPath();
                ctx.arc(pos.x, pos.y, 60, 0, Math.PI * 2);
                ctx.fill();
                
                // Marker
                ctx.fillStyle = color;
                ctx.beginPath();
                ctx.arc(pos.x, pos.y, 10, 0, Math.PI * 2);
                ctx.fill();
                ctx.strokeStyle = 'white';
                ctx.lineWidth = 2;
                ctx.stroke();
                
                // Label
                ctx.fillStyle = '#f1f5f9';
                ctx.font = 'bold 14px Inter';
                ctx.textAlign = 'center';
                ctx.fillText(sector.id, pos.x, pos.y - 25);
                
                // Traffic indicator
                ctx.font = '10px Inter';
                ctx.fillText(`${sector.traffic.today}`, pos.x, pos.y + 30);
            });
        }

        function selectTime(time) {
            selectedTime = time;
            document.querySelectorAll('.time-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            renderStats();
            renderSectors();
            
            // Update AI message
            const sector = sectors.find(s => s.id === selectedSector) || sectors[2];
            const todayTraffic = sector.traffic.today;
            const compareTraffic = sector.traffic[time];
            const change = ((todayTraffic - compareTraffic) / compareTraffic * 100).toFixed(0);
            
            if (time !== 'today' && Math.abs(change) > 50) {
                document.getElementById('aiMessage').innerHTML = 
                    `Traffic in ${sector.id} is ${Math.abs(change)}% ${change > 0 ? 'higher' : 'lower'} than ${time}. ${change > 0 ? 'This deviation requires investigation.' : 'Traffic levels are below historical averages.'}`;
            }
        }

        function selectSectorFunc(sectorId) {
            selectedSector = sectorId;
            renderSectors();
            renderStats();
            
            const sector = sectors.find(s => s.id === sectorId);
            document.getElementById('selectedSector').textContent = sector.name;
            document.getElementById('mapInfo').innerHTML = `
                <div style="font-weight: 600; margin-bottom: 0.5rem;">${sector.name}</div>
                <div style="font-size: 0.85rem;">Traffic: ${sector.traffic.today}</div>
                <div style="font-size: 0.85rem;">Risk Level: ${sector.risk.toUpperCase()}</div>
                <div style="font-size: 0.85rem;">Terrain: ${sector.terrain}</div>
            `;
        }

        function openActionModal(actionType) {
            selectedAction = actionType;
            const modal = document.getElementById('actionModal');
            const title = document.getElementById('modalTitle');
            const options = document.getElementById('resourceOptions');
            
            const actionData = {
                drone: {
                    title: '🚁 Deploy Drone',
                    options: [
                        { icon: '🔍', name: 'Surveillance Drone', desc: 'Aerial reconnaissance' },
                        { icon: '📸', name: 'Camera Drone', desc: 'High-res imaging' },
                        { icon: '🌡️', name: 'Thermal Drone', desc: 'Heat signature detection' },
                        { icon: '📡', name: 'Signal Drone', desc: 'Communications relay' }
                    ]
                },
                soldiers: {
                    title: '👮 Deploy Soldiers',
                    options: [
                        { icon: '👮', name: '2 Soldiers', desc: 'Quick response unit' },
                        { icon: '👮‍♂️', name: '5 Soldiers', desc: 'Standard patrol unit' },
                        { icon: '🎖️', name: '10+ Soldiers', desc: 'Full tactical team' },
                        { icon: '🚁', name: 'Special Forces', desc: 'Elite unit deployment' }
                    ]
                },
                officer: {
                    title: '🎖️ Contact Officer',
                    options: [
                        { icon: '👨‍✈️', name: 'Lieutenant', desc: 'Field commander' },
                        { icon: '🎖️', name: 'Captain', desc: 'Sector commander' },
                        { icon: '⭐', name: 'Major', desc: 'Regional commander' },
                        { icon: '🏅', name: 'Colonel', desc: 'Chief commander' }
                    ]
                },
                patrol: {
                    title: '🚔 Send Patrol',
                    options: [
                        { icon: '🚶', name: 'Foot Patrol', desc: '2-person team' },
                        { icon: '🚙', name: 'Vehicle Patrol', desc: 'Mobile unit' },
                        { icon: '🐕', name: 'K9 Unit', desc: 'With detection dog' },
                        { icon: '🚁', name: 'Air Patrol', desc: 'Helicopter surveillance' }
                    ]
                }
            };
            
            const data = actionData[actionType] || { 
                title: 'Select Action', 
                options: [
                    { icon: '✓', name: 'Confirm', desc: 'Execute action' },
                    { icon: '📊', name: 'Analyze', desc: 'Get more data' }
                ]
            };
            
            title.textContent = data.title;
            options.innerHTML = data.options.map(opt => `
                <div class="option-card" onclick="selectOption(this)">
                    <div class="option-icon">${opt.icon}</div>
                    <div class="option-name">${opt.name}</div>
                    <div class="option-desc">${opt.desc}</div>
                </div>
            `).join('');
            
            modal.classList.add('show');
        }

        function selectOption(element) {
            document.querySelectorAll('#resourceOptions .option-card').forEach(card => {
                card.classList.remove('selected');
            });
            element.classList.add('selected');
        }

        function selectPriority(priority) {
            // Handle priority selection
        }

        function closeModal() {
            document.getElementById('actionModal').classList.remove('show');
        }

        function executeAction() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', hour12: false });
            
            timeline.unshift({
                time: timeString,
                title: 'Action Deployed',
                desc: `${selectedAction.toUpperCase()} deployed to Sector ${selectedSector || 'A-03'}`,
                action: 'Status: In progress',
                type: 'normal'
            });
            
            renderTimeline();
            closeModal();
        }

        function showCCTV() {
            const modal = document.getElementById('cctvModal');
            const grid = document.getElementById('cctvGrid');
            
            grid.innerHTML = cctvCameras.map(cam => `
                <div class="cctv-feed" style="background: linear-gradient(135deg, #1a1f2e, #0f1419);">
                    <div style="display: flex; align-items: center; justify-content: center; height: 100%; color: #64748b; font-size: 3rem;">
                        ${cam.status === 'Active' ? '📹' : '⚠️'}
                    </div>
                    <div class="cctv-overlay">
                        <div class="cctv-name">${cam.id} - ${cam.sector}</div>
                        <div class="cctv-status" style="color: ${cam.status === 'Active' ? '#10b981' : '#ef4444'}">
                            ${cam.status} • ${cam.quality}
                        </div>
                    </div>
                </div>
            `).join('');
            
            modal.classList.add('show');
        }

        function closeCCTV() {
            document.getElementById('cctvModal').classList.remove('show');
        }

        function toggleLayer(layer) {
            // Toggle map layers
        }

        // Initialize on load
        window.addEventListener('load', init);
    </script>
</body>
</html>
