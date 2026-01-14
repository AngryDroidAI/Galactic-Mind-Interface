<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galactic Mind Interface</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #0a0e17;
            color: #c2e0ff;
            overflow-x: hidden;
            min-height: 100vh;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(28, 58, 173, 0.1) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(113, 28, 173, 0.1) 0%, transparent 20%);
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            padding: 30px 0;
            border-bottom: 1px solid rgba(64, 156, 255, 0.2);
            margin-bottom: 30px;
            position: relative;
        }
        
        h1 {
            font-size: 3.2rem;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #4cc9f0, #4361ee, #7209b7);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 15px rgba(76, 201, 240, 0.3);
            letter-spacing: 1.5px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: #89b4fa;
            max-width: 800px;
            margin: 0 auto;
            line-height: 1.6;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        @media (max-width: 1100px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .panel {
            background: rgba(16, 23, 41, 0.8);
            border-radius: 15px;
            padding: 25px;
            border: 1px solid rgba(64, 156, 255, 0.2);
            box-shadow: 0 10px 30px rgba(0, 15, 40, 0.5);
            backdrop-filter: blur(5px);
        }
        
        .panel-title {
            font-size: 1.8rem;
            color: #72a7ff;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            border-bottom: 1px solid rgba(64, 156, 255, 0.2);
            padding-bottom: 10px;
        }
        
        .panel-title i {
            color: #4cc9f0;
        }
        
        .visualization-container {
            height: 500px;
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            background: rgba(5, 10, 24, 0.9);
        }
        
        #galaxyCanvas {
            width: 100%;
            height: 100%;
            display: block;
        }
        
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        
        .control-group {
            flex: 1;
            min-width: 200px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            color: #89b4fa;
            font-weight: 600;
        }
        
        select, button {
            width: 100%;
            padding: 12px 15px;
            background: rgba(20, 33, 61, 0.8);
            border: 1px solid rgba(64, 156, 255, 0.3);
            border-radius: 8px;
            color: #c2e0ff;
            font-size: 1rem;
            transition: all 0.3s ease;
        }
        
        select:focus, button:hover {
            outline: none;
            border-color: #4cc9f0;
            box-shadow: 0 0 10px rgba(76, 201, 240, 0.3);
        }
        
        button {
            background: linear-gradient(90deg, #4361ee, #3a0ca3);
            color: white;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        button:active {
            transform: translateY(2px);
        }
        
        .protocol-layers {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-top: 20px;
        }
        
        .layer {
            background: rgba(20, 33, 61, 0.7);
            border-radius: 10px;
            padding: 15px;
            border-left: 4px solid #4361ee;
            transition: all 0.3s ease;
        }
        
        .layer.active {
            border-left-color: #4cc9f0;
            background: rgba(20, 33, 61, 0.9);
            box-shadow: 0 0 15px rgba(76, 201, 240, 0.2);
        }
        
        .layer-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .layer-name {
            font-weight: 600;
            color: #72a7ff;
        }
        
        .layer-status {
            font-size: 0.9rem;
            padding: 3px 10px;
            border-radius: 20px;
            background: rgba(28, 58, 173, 0.3);
        }
        
        .layer.active .layer-status {
            background: rgba(76, 201, 240, 0.3);
            color: #4cc9f0;
        }
        
        .layer-desc {
            font-size: 0.95rem;
            color: #a3c8ff;
            line-height: 1.5;
        }
        
        .communication-log {
            height: 300px;
            overflow-y: auto;
            background: rgba(5, 10, 24, 0.9);
            border-radius: 10px;
            padding: 15px;
            margin-top: 20px;
            border: 1px solid rgba(64, 156, 255, 0.1);
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
        }
        
        .log-entry {
            padding: 8px 0;
            border-bottom: 1px solid rgba(64, 156, 255, 0.05);
            display: flex;
            gap: 10px;
        }
        
        .log-time {
            color: #4cc9f0;
            min-width: 70px;
        }
        
        .log-source {
            color: #f72585;
            min-width: 100px;
        }
        
        .log-message {
            color: #c2e0ff;
            flex-grow: 1;
        }
        
        .footer {
            text-align: center;
            padding: 30px 0;
            border-top: 1px solid rgba(64, 156, 255, 0.2);
            color: #89b4fa;
            font-size: 0.9rem;
            line-height: 1.6;
        }
        
        .simulation-info {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }
        
        .info-card {
            background: rgba(20, 33, 61, 0.5);
            border-radius: 10px;
            padding: 20px;
            text-align: center;
        }
        
        .info-value {
            font-size: 2rem;
            color: #4cc9f0;
            font-weight: 700;
            margin: 10px 0;
        }
        
        .info-label {
            font-size: 0.9rem;
            color: #89b4fa;
        }
        
        .signal-strength {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 15px;
        }
        
        .signal-bars {
            display: flex;
            gap: 3px;
            height: 20px;
        }
        
        .signal-bar {
            width: 8px;
            background: rgba(64, 156, 255, 0.3);
            border-radius: 2px;
        }
        
        .signal-bar.active {
            background: #4cc9f0;
        }
        
        .power-btn {
            background: linear-gradient(90deg, #f72585, #b5179e);
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { opacity: 0.7; }
            50% { opacity: 1; }
            100% { opacity: 0.7; }
        }
        
        .connection-status {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 20px;
            padding: 10px;
            border-radius: 8px;
            background: rgba(20, 33, 61, 0.5);
        }
        
        .status-indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #f72585;
        }
        
        .status-indicator.connected {
            background: #4cc9f0;
            box-shadow: 0 0 10px #4cc9f0;
        }
        
        .star {
            position: absolute;
            border-radius: 50%;
            background-color: white;
        }
        
        .planet {
            position: absolute;
            border-radius: 50%;
        }
        
        .signal {
            position: absolute;
            border-radius: 50%;
            border: 2px solid;
            opacity: 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-satellite"></i> Galactic Mind Interface</h1>
            <p class="subtitle">A simulation of communication protocols for intelligence at planetary and star-system scales. Experience interstellar message transmission across vast cosmic distances using quantum entanglement, neutrino beams, and gravitational wave modulation.</p>
        </header>
        
        <div class="main-content">
            <div class="panel">
                <h2 class="panel-title"><i class="fas fa-globe-americas"></i> Stellar Network Visualization</h2>
                <div class="visualization-container">
                    <canvas id="galaxyCanvas"></canvas>
                </div>
                
                <div class="controls">
                    <div class="control-group">
                        <label for="protocolSelect"><i class="fas fa-broadcast-tower"></i> Communication Protocol</label>
                        <select id="protocolSelect">
                            <option value="quantum">Quantum Entanglement (Instantaneous)</option>
                            <option value="neutrino">Neutrino Beam (0.99c)</option>
                            <option value="gravitational">Gravitational Wave (1c)</option>
                            <option value="laser">Focused Laser (1c)</option>
                            <option value="radio">Radio Wave (1c)</option>
                        </select>
                    </div>
                    
                    <div class="control-group">
                        <label for="destinationSelect"><i class="fas fa-star"></i> Destination</label>
                        <select id="destinationSelect">
                            <option value="proxima">Proxima Centauri (4.24 ly)</option>
                            <option value="trappist">TRAPPIST-1 (39.5 ly)</option>
                            <option value="kepler">Kepler-186 (492 ly)</option>
                            <option value="andromeda">Andromeda Galaxy (2.5M ly)</option>
                        </select>
                    </div>
                    
                    <div class="control-group">
                        <label for="messageType"><i class="fas fa-comment-dots"></i> Message Type</label>
                        <select id="messageType">
                            <option value="greeting">First Contact Greeting</option>
                            <option value="mathematical">Mathematical Primer</option>
                            <option value="cultural">Cultural Data Packet</option>
                            <option value="scientific">Scientific Knowledge</option>
                        </select>
                    </div>
                </div>
                
                <div class="controls" style="margin-top: 20px;">
                    <button id="sendButton" class="pulse">
                        <i class="fas fa-paper-plane"></i> Transmit Message
                    </button>
                    <button id="powerButton" class="power-btn">
                        <i class="fas fa-power-off"></i> Initialize Connection
                    </button>
                </div>
                
                <div class="connection-status">
                    <div class="status-indicator" id="statusIndicator"></div>
                    <span id="statusText">Connection offline - Initialize to begin</span>
                </div>
            </div>
            
            <div class="panel">
                <h2 class="panel-title"><i class="fas fa-layer-group"></i> Protocol Stack Layers</h2>
                
                <div class="protocol-layers">
                    <div class="layer active" id="layer1">
                        <div class="layer-header">
                            <span class="layer-name">Application Layer</span>
                            <span class="layer-status">Active</span>
                        </div>
                        <div class="layer-desc">Encodes intelligence into transmittable formats using semantic compression algorithms and universal concept mapping.</div>
                    </div>
                    
                    <div class="layer" id="layer2">
                        <div class="layer-header">
                            <span class="layer-name">Quantum Encryption</span>
                            <span class="layer-status">Standby</span>
                        </div>
                        <div class="layer-desc">Applies quantum-key distribution for secure communication that cannot be intercepted without detection.</div>
                    </div>
                    
                    <div class="layer" id="layer3">
                        <div class="layer-header">
                            <span class="layer-name">Interstellar Transport</span>
                            <span class="layer-status">Standby</span>
                        </div>
                        <div class="layer-desc">Manages data packetization, error correction for cosmic interference, and light-year scale transmission timing.</div>
                    </div>
                    
                    <div class="layer" id="layer4">
                        <div class="layer-header">
                            <span class="layer-name">Physical Layer</span>
                            <span class="layer-status">Standby</span>
                        </div>
                        <div class="layer-desc">Modulates signals onto carrier medium (neutrinos, gravitational waves, entangled particles, EM radiation).</div>
                    </div>
                </div>
                
                <h2 class="panel-title" style="margin-top: 30px;"><i class="fas fa-history"></i> Communication Log</h2>
                <div class="communication-log" id="communicationLog">
                    <div class="log-entry">
                        <span class="log-time">00:00:00</span>
                        <span class="log-source">SYSTEM</span>
                        <span class="log-message">Galactic Mind Interface initialized. Awaiting connection.</span>
                    </div>
                </div>
                
                <div class="signal-strength">
                    <span>Signal Integrity:</span>
                    <div class="signal-bars">
                        <div class="signal-bar" id="bar1"></div>
                        <div class="signal-bar" id="bar2"></div>
                        <div class="signal-bar" id="bar3"></div>
                        <div class="signal-bar" id="bar4"></div>
                        <div class="signal-bar" id="bar5"></div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="simulation-info">
            <div class="info-card">
                <i class="fas fa-clock" style="font-size: 2rem; color: #4361ee;"></i>
                <div class="info-value" id="transmissionTime">--</div>
                <div class="info-label">Transmission Time</div>
            </div>
            
            <div class="info-card">
                <i class="fas fa-ruler-combined" style="font-size: 2rem; color: #4361ee;"></i>
                <div class="info-value" id="distance">4.24 ly</div>
                <div class="info-label">Distance to Target</div>
            </div>
            
            <div class="info-card">
                <i class="fas fa-tachometer-alt" style="font-size: 2rem; color: #4361ee;"></i>
                <div class="info-value" id="dataRate">--</div>
                <div class="info-label">Data Rate</div>
            </div>
            
            <div class="info-card">
                <i class="fas fa-database" style="font-size: 2rem; color: #4361ee;"></i>
                <div class="info-value" id="messageSize">3.2 ZB</div>
                <div class="info-label">Message Size</div>
            </div>
        </div>
        
        <div class="footer">
            <p>Galactic Mind Interface v2.1 | Simulation of theoretical communication protocols for interstellar intelligence exchange</p>
            <p>Protocols based on current theoretical physics models. Transmission times account for relativistic effects and cosmic medium interference.</p>
        </div>
    </div>

    <script>
        // Galaxy visualization
        const canvas = document.getElementById('galaxyCanvas');
        const ctx = canvas.getContext('2d');
        
        // Set canvas dimensions
        function resizeCanvas() {
            canvas.width = canvas.offsetWidth;
            canvas.height = canvas.offsetHeight;
            drawGalaxy();
        }
        
        // Stars and planets data
        const stars = [];
        const planets = [];
        const signals = [];
        
        // Initialize visualization
        function initVisualization() {
            // Create stars
            for (let i = 0; i < 150; i++) {
                stars.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 1.5 + 0.5,
                    brightness: Math.random() * 0.8 + 0.2
                });
            }
            
            // Create planets (communication nodes)
            const planetData = [
                { id: 'earth', name: 'Earth', x: 0.15, y: 0.5, color: '#4cc9f0', size: 20 },
                { id: 'proxima', name: 'Proxima Centauri', x: 0.85, y: 0.5, color: '#f72585', size: 18 },
                { id: 'trappist', name: 'TRAPPIST-1', x: 0.8, y: 0.2, color: '#7209b7', size: 16 },
                { id: 'kepler', name: 'Kepler-186', x: 0.9, y: 0.8, color: '#4361ee', size: 17 },
                { id: 'andromeda', name: 'Andromeda', x: 0.95, y: 0.1, color: '#ff9e00', size: 15 }
            ];
            
            planetData.forEach(planet => {
                planets.push({
                    ...planet,
                    x: planet.x * canvas.width,
                    y: planet.y * canvas.height
                });
            });
            
            drawGalaxy();
        }
        
        // Draw the galaxy visualization
        function drawGalaxy() {
            // Clear canvas with space gradient
            const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
            gradient.addColorStop(0, '#050a18');
            gradient.addColorStop(1, '#0a142f');
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // Draw stars
            stars.forEach(star => {
                ctx.beginPath();
                ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
                ctx.fillStyle = `rgba(255, 255, 255, ${star.brightness})`;
                ctx.fill();
            });
            
            // Draw faint galactic arms
            ctx.beginPath();
            ctx.ellipse(canvas.width/2, canvas.height/2, canvas.width/2.5, canvas.height/3, 0, 0, Math.PI * 2);
            ctx.strokeStyle = 'rgba(64, 156, 255, 0.05)';
            ctx.lineWidth = 50;
            ctx.stroke();
            
            // Draw planet connections
            ctx.strokeStyle = 'rgba(64, 156, 255, 0.1)';
            ctx.lineWidth = 1;
            ctx.setLineDash([5, 5]);
            
            for (let i = 0; i < planets.length; i++) {
                for (let j = i + 1; j < planets.length; j++) {
                    ctx.beginPath();
                    ctx.moveTo(planets[i].x, planets[i].y);
                    ctx.lineTo(planets[j].x, planets[j].y);
                    ctx.stroke();
                }
            }
            
            ctx.setLineDash([]);
            
            // Draw planets
            planets.forEach(planet => {
                // Glow effect
                const glow = ctx.createRadialGradient(
                    planet.x, planet.y, 0,
                    planet.x, planet.y, planet.size * 2
                );
                glow.addColorStop(0, planet.color + '80');
                glow.addColorStop(1, 'transparent');
                
                ctx.beginPath();
                ctx.arc(planet.x, planet.y, planet.size * 2, 0, Math.PI * 2);
                ctx.fillStyle = glow;
                ctx.fill();
                
                // Planet body
                ctx.beginPath();
                ctx.arc(planet.x, planet.y, planet.size, 0, Math.PI * 2);
                ctx.fillStyle = planet.color;
                ctx.fill();
                
                // Planet label
                ctx.fillStyle = '#c2e0ff';
                ctx.font = '12px Arial';
                ctx.textAlign = 'center';
                ctx.fillText(planet.name, planet.x, planet.y + planet.size + 15);
            });
            
            // Draw active signals
            signals.forEach((signal, index) => {
                const progress = (Date.now() - signal.startTime) / signal.duration;
                
                if (progress >= 1) {
                    signals.splice(index, 1);
                    return;
                }
                
                const currentRadius = signal.startRadius + (signal.endRadius - signal.startRadius) * progress;
                const opacity = 1 - progress;
                
                ctx.beginPath();
                ctx.arc(signal.fromX, signal.fromY, currentRadius, 0, Math.PI * 2);
                ctx.strokeStyle = signal.color.replace(')', `, ${opacity})`).replace('rgb', 'rgba');
                ctx.lineWidth = 2;
                ctx.stroke();
                
                // Draw signal dot
                const angle = Math.atan2(signal.toY - signal.fromY, signal.toX - signal.fromX);
                const dotX = signal.fromX + Math.cos(angle) * currentRadius;
                const dotY = signal.fromY + Math.sin(angle) * currentRadius;
                
                ctx.beginPath();
                ctx.arc(dotX, dotY, 3, 0, Math.PI * 2);
                ctx.fillStyle = signal.color.replace(')', `, ${opacity})`).replace('rgb', 'rgba');
                ctx.fill();
            });
            
            requestAnimationFrame(drawGalaxy);
        }
        
        // Send a signal between planets
        function sendSignal(fromId, toId, color) {
            const fromPlanet = planets.find(p => p.id === fromId);
            const toPlanet = planets.find(p => p.id === toId);
            
            if (!fromPlanet || !toPlanet) return;
            
            const distance = Math.sqrt(
                Math.pow(toPlanet.x - fromPlanet.x, 2) + 
                Math.pow(toPlanet.y - fromPlanet.y, 2)
            );
            
            signals.push({
                fromX: fromPlanet.x,
                fromY: fromPlanet.y,
                toX: toPlanet.x,
                toY: toPlanet.y,
                startRadius: fromPlanet.size,
                endRadius: distance,
                color: color || '#4cc9f0',
                startTime: Date.now(),
                duration: 3000 // 3 seconds animation
            });
        }
        
        // DOM Elements
        const protocolSelect = document.getElementById('protocolSelect');
        const destinationSelect = document.getElementById('destinationSelect');
        const messageTypeSelect = document.getElementById('messageType');
        const sendButton = document.getElementById('sendButton');
        const powerButton = document.getElementById('powerButton');
        const statusIndicator = document.getElementById('statusIndicator');
        const statusText = document.getElementById('statusText');
        const communicationLog = document.getElementById('communicationLog');
        const transmissionTime = document.getElementById('transmissionTime');
        const distanceElement = document.getElementById('distance');
        const dataRate = document.getElementById('dataRate');
        const messageSize = document.getElementById('messageSize');
        const layer1 = document.getElementById('layer1');
        const layer2 = document.getElementById('layer2');
        const layer3 = document.getElementById('layer3');
        const layer4 = document.getElementById('layer4');
        const signalBars = [
            document.getElementById('bar1'),
            document.getElementById('bar2'),
            document.getElementById('bar3'),
            document.getElementById('bar4'),
            document.getElementById('bar5')
        ];
        
        // System state
        let isConnected = false;
        let transmissionCount = 0;
        
        // Protocol data
        const protocols = {
            quantum: { name: 'Quantum Entanglement', speed: 'Instantaneous', color: '#4cc9f0', rate: '∞ bps' },
            neutrino: { name: 'Neutrino Beam', speed: '0.99c', color: '#f72585', rate: '10 Gbps' },
            gravitational: { name: 'Gravitational Wave', speed: '1c', color: '#7209b7', rate: '1 Mbps' },
            laser: { name: 'Focused Laser', speed: '1c', color: '#4361ee', rate: '100 Gbps' },
            radio: { name: 'Radio Wave', speed: '1c', color: '#ff9e00', rate: '10 Mbps' }
        };
        
        const destinations = {
            proxima: { name: 'Proxima Centauri', distance: 4.24, planetId: 'proxima' },
            trappist: { name: 'TRAPPIST-1', distance: 39.5, planetId: 'trappist' },
            kepler: { name: 'Kepler-186', distance: 492, planetId: 'kepler' },
            andromeda: { name: 'Andromeda Galaxy', distance: 2500000, planetId: 'andromeda' }
        };
        
        const messages = {
            greeting: { name: 'First Contact Greeting', size: '1.2 ZB' },
            mathematical: { name: 'Mathematical Primer', size: '0.8 ZB' },
            cultural: { name: 'Cultural Data Packet', size: '5.4 ZB' },
            scientific: { name: 'Scientific Knowledge', size: '3.2 ZB' }
        };
        
        // Update UI based on selections
        function updateUI() {
            const protocol = protocolSelect.value;
            const destination = destinationSelect.value;
            const message = messageTypeSelect.value;
            
            // Update distance
            distanceElement.textContent = destinations[destination].distance.toLocaleString() + ' ly';
            
            // Update message size
            messageSize.textContent = messages[message].size;
            
            // Update transmission time based on protocol and distance
            const destDistance = destinations[destination].distance;
            let time = '--';
            
            if (protocol === 'quantum') {
                time = 'Instant';
            } else if (protocol === 'neutrino') {
                // 0.99c
                time = (destDistance / 0.99).toFixed(2) + ' years';
            } else {
                // 1c
                time = destDistance.toFixed(2) + ' years';
            }
            
            transmissionTime.textContent = time;
            
            // Update data rate
            dataRate.textContent = protocols[protocol].rate;
            
            // Update signal bars
            updateSignalStrength(protocol);
        }
        
        // Update signal strength visualization
        function updateSignalStrength(protocol) {
            // Reset all bars
            signalBars.forEach(bar => bar.classList.remove('active'));
            
            // Set active bars based on protocol
            let activeBars = 3; // Default
            
            if (protocol === 'quantum') activeBars = 5;
            else if (protocol === 'laser') activeBars = 4;
            else if (protocol === 'neutrino') activeBars = 3;
            else if (protocol === 'gravitational') activeBars = 2;
            else if (protocol === 'radio') activeBars = 1;
            
            for (let i = 0; i < activeBars; i++) {
                signalBars[i].classList.add('active');
            }
        }
        
        // Add log entry
        function addLogEntry(source, message) {
            const now = new Date();
            const timeString = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}`;
            
            const logEntry = document.createElement('div');
            logEntry.className = 'log-entry';
            logEntry.innerHTML = `
                <span class="log-time">${timeString}</span>
                <span class="log-source">${source}</span>
                <span class="log-message">${message}</span>
            `;
            
            communicationLog.appendChild(logEntry);
            communicationLog.scrollTop = communicationLog.scrollHeight;
        }
        
        // Activate protocol layers with animation
        function activateLayers() {
            // Reset all layers
            [layer1, layer2, layer3, layer4].forEach(layer => {
                layer.classList.remove('active');
                layer.querySelector('.layer-status').textContent = 'Standby';
            });
            
            // Activate layer 1 immediately
            layer1.classList.add('active');
            layer1.querySelector('.layer-status').textContent = 'Active';
            
            // Activate other layers with delays
            setTimeout(() => {
                layer2.classList.add('active');
                layer2.querySelector('.layer-status').textContent = 'Active';
            }, 500);
            
            setTimeout(() => {
                layer3.classList.add('active');
                layer3.querySelector('.layer-status').textContent = 'Active';
            }, 1000);
            
            setTimeout(() => {
                layer4.classList.add('active');
                layer4.querySelector('.layer-status').textContent = 'Active';
            }, 1500);
        }
        
        // Initialize connection
        function initializeConnection() {
            if (isConnected) {
                // Disconnect
                isConnected = false;
                statusIndicator.classList.remove('connected');
                statusIndicator.classList.remove('pulse');
                statusText.textContent = 'Connection offline - Initialize to begin';
                powerButton.innerHTML = '<i class="fas fa-power-off"></i> Initialize Connection';
                sendButton.disabled = true;
                sendButton.classList.remove('pulse');
                
                addLogEntry('SYSTEM', 'Galactic Mind Interface connection terminated.');
            } else {
                // Connect
                isConnected = true;
                statusIndicator.classList.add('connected');
                statusIndicator.classList.add('pulse');
                statusText.textContent = 'Connected to interstellar network';
                powerButton.innerHTML = '<i class="fas fa-power-off"></i> Terminate Connection';
                sendButton.disabled = false;
                
                activateLayers();
                updateUI();
                
                addLogEntry('SYSTEM', 'Initializing Galactic Mind Interface...');
                addLogEntry('SYSTEM', 'Establishing quantum entanglement link...');
                addLogEntry('SYSTEM', 'Calibrating neutrino beam transceivers...');
                addLogEntry('SYSTEM', 'Connection established. Ready for transmission.');
            }
        }
        
        // Send message
        function sendMessage() {
            if (!isConnected) return;
            
            const protocol = protocolSelect.value;
            const destination = destinationSelect.value;
            const messageType = messageTypeSelect.value;
            
            const protocolData = protocols[protocol];
            const destinationData = destinations[destination];
            const messageData = messages[messageType];
            
            // Add to log
            addLogEntry('TRANSMIT', `Initiating ${protocolData.name} transmission to ${destinationData.name}`);
            addLogEntry('PROTOCOL', `Using ${protocolData.speed} propagation with ${protocolData.rate} data rate`);
            addLogEntry('PAYLOAD', `Sending ${messageData.name} (${messageData.size})`);
            
            // Update transmission counter
            transmissionCount++;
            
            // Calculate transmission time
            let timeYears = destinationData.distance;
            if (protocol === 'neutrino') timeYears = destinationData.distance / 0.99;
            if (protocol === 'quantum') timeYears = 0;
            
            // Show transmission in visualization
            sendSignal('earth', destinationData.planetId, protocolData.color);
            
            // Simulate response after delay
            const responseDelay = protocol === 'quantum' ? 3000 : 5000;
            
            setTimeout(() => {
                addLogEntry('RECEIVE', `Signal received at ${destinationData.name}`);
                addLogEntry('PROCESSING', `Decoding ${messageData.name} payload...`);
                
                // Show return signal
                sendSignal(destinationData.planetId, 'earth', '#4ade80');
                
                setTimeout(() => {
                    addLogEntry('RESPONSE', `Response received from ${destinationData.name}: "Message acknowledged. Cultural exchange initiated."`);
                    
                    // Update transmission time with actual
                    if (protocol !== 'quantum') {
                        transmissionTime.textContent = `${timeYears.toFixed(2)} years (round trip: ${(timeYears * 2).toFixed(2)} years)`;
                    }
                }, 2000);
            }, responseDelay);
        }
        
        // Event Listeners
        protocolSelect.addEventListener('change', updateUI);
        destinationSelect.addEventListener('change', updateUI);
        messageTypeSelect.addEventListener('change', updateUI);
        powerButton.addEventListener('click', initializeConnection);
        sendButton.addEventListener('click', sendMessage);
        
        // Initialize
        window.addEventListener('load', () => {
            resizeCanvas();
            initVisualization();
            updateUI();
            
            // Make send button initially disabled
            sendButton.disabled = true;
            
            // Add welcome log entries
            setTimeout(() => {
                addLogEntry('SYSTEM', 'Welcome to the Galactic Mind Interface.');
                addLogEntry('SYSTEM', 'This simulation demonstrates interstellar communication protocols.');
                addLogEntry('SYSTEM', 'Please initialize connection to begin transmission.');
            }, 1000);
        });
        
        window.addEventListener('resize', () => {
            resizeCanvas();
        });
    </script>
</body>
</html>
