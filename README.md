<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Atomic Particle System with Hand Gesture Control</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #0c0c0c 0%, #1a1a2e 50%, #16213e 100%);
            min-height: 100vh;
        }
        .container { max-width: 1200px; margin: 0 auto; padding: 20px; }
        .header { 
            text-align: center; 
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #96ceb4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 40px;
        }
        .header h1 { 
            font-size: clamp(2.5rem, 5vw, 4rem); 
            font-weight: 800;
            margin-bottom: 10px;
            text-shadow: 0 0 30px rgba(255,107,107,0.5);
        }
        .subtitle { 
            font-size: 1.3rem; 
            color: #a8b2d1;
            font-weight: 300;
        }
        .features-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px; 
            margin: 40px 0;
        }
        .feature-card { 
            background: rgba(255,255,255,0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255,255,255,0.1);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        .feature-card::before {
            content: '';
            position: absolute;
            top: 0; left: -100%;
            width: 100%; height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: 0.5s;
        }
        .feature-card:hover::before { left: 100%; }
        .feature-card:hover { 
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }
        .feature-icon { 
            font-size: 3rem; 
            margin-bottom: 15px;
            display: block;
        }
        .feature-card h3 { 
            color: #4ecdc4; 
            font-size: 1.4rem; 
            margin-bottom: 10px;
        }
        .install { 
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 15px;
            padding: 40px;
            text-align: center;
            margin: 40px 0;
            color: white;
        }
        .install-command { 
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            font-size: 1.1rem;
            margin: 20px 0;
            border-left: 4px solid #4ecdc4;
        }
        .controls { 
            background: rgba(255,255,255,0.05);
            border-radius: 15px;
            padding: 25px;
            margin: 30px 0;
        }
        .controls h3 { color: #96ceb4; margin-bottom: 15px; }
        .control-list { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            list-style: none;
        }
        .control-item { 
            background: rgba(150,206,180,0.2);
            padding: 12px 20px;
            border-radius: 25px;
            text-align: center;
            font-weight: 500;
        }
        .demo-section { 
            text-align: center; 
            margin: 50px 0;
            padding: 40px;
            background: rgba(0,0,0,0.3);
            border-radius: 20px;
        }
        .demo-placeholder { 
            width: 100%; 
            height: 300px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
            margin: 20px 0;
            border: 3px dashed rgba(255,255,255,0.3);
        }
        .structure-tree {
            background: rgba(255,255,255,0.05);
            border-radius: 15px;
            padding: 25px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            margin: 30px 0;
        }
        .stats { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        .stat-card { 
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%);
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            color: #333;
            font-weight: 600;
        }
        footer { 
            text-align: center; 
            padding: 30px;
            color: #a8b2d1;
            border-top: 1px solid rgba(255,255,255,0.1);
            margin-top: 50px;
        }
        @media (max-width: 768px) {
            .container { padding: 15px; }
            .features-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>🧬 Atomic Particle System</h1>
            <p class="subtitle">Hand Gesture Control • Real-time Physics • Electromagnetic Forces</p>
        </header>

        <section class="features-grid">
            <div class="feature-card">
                <span class="feature-icon">⚛️</span>
                <h3>Interactive Physics</h3>
                <p>Real-time particle simulation with electromagnetic forces, electron orbits, and collision detection.</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">✋</span>
                <h3>Hand Gesture Control</h3>
                <p>Control particles using webcam hand tracking via MediaPipe. Open palm attracts, fist repels.</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">🎨</span>
                <h3>Visual Effects</h3>
                <p>Atom bonding visualization, energy glow effects, particle trails, and molecular structures.</p>
            </div>
            <div class="feature-card">
                <span class="feature-icon">📊</span>
                <h3>Performance Monitor</h3>
                <p>Live CPU/GPU/RAM/FPS dashboard with psutil & GPUtil integration.</p>
            </div>
        </section>

        <section class="install">
            <h2>🚀 Quick Start</h2>
            <div class="install-command">python particle_system.py</div>
            <p><strong>Prerequisites:</strong> Python 3.8+ • Webcam (optional) • SSE4.2 CPU</p>
        </section>

        <section class="controls">
            <h3>🎮 Controls</h3>
            <ul class="control-list">
                <li class="control-item">🖐️ Open Palm: Attract</li>
                <li class="control-item">✊ Fist: Repel</li>
                <li class="control-item">🖱️ Mouse: Drag particles</li>
                <li class="control-item">SPACE: Pause</li>
                <li class="control-item">R: Reset</li>
                <li class="control-item">M: Molecules</li>
                <li class="control-item">C: Camera Toggle</li>
            </ul>
        </section>

        <section class="demo-section">
            <h2>🎮 Live Demo</h2>
            <div class="demo-placeholder">
                📹 Demo Video / GIF Coming Soon
            </div>
            <p>Watch particles form atoms and molecules in real-time!</p>
        </section>

        <section class="structure-tree">
            <h3>🏗️ Repository Structure</h3>
            <pre>
├── particle_system.py     # Main app
├── particle.py           # Physics engine
├── gesture_controller.py # MediaPipe tracking
├── renderer.py          # Pygame visuals
├── molecules.json       # H2O, CO2, etc.
├── requirements.txt
└── README.html
            </pre>
        </section>

        <section class="stats">
            <div class="stat-card">
                <div>60+ FPS</div>
                <small>1000+ Particles</small>
            </div>
            <div class="stat-card">
                <div>Real-time</div>
                <small>Physics Calc</small>
            </div>
            <div class="stat-card">
                <div>Webcam</div>
                <small>30 FPS Tracking</small>
            </div>
            <div class="stat-card">
                <div>Cross-platform</div>
                <small>Windows/Linux/Mac</small>
            </div>
        </section>

        <section>
            <h3>📦 Dependencies</h3>
            <div class="install-command">
                pygame>=2.5.0 opencv-python>=4.8.0 numpy>=1.24.0<br>
                mediapipe>=0.10.0 psutil>=5.9.0 GPUtil>=1.4.0
            </div>
        </section>

        <footer>
            <p>MIT License • Made with ❤️ for physics & gesture tech enthusiasts</p>
            <p>⭐ Star on <a href="#" style="color: #4ecdc4;">GitHub</a> • 🐛 Report issues</p>
        </footer>
    </div>
</body>
</html>
