<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Super Mario Collection HD - 100 Levels Edition</title>
    <link href="https://fonts.googleapis.com/css2?family=Rubik:wght@500;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --mario-red: #ff3b30;
            --mario-blue: #007aff;
            --mario-yellow: #ffcc00;
            --mario-green: #34c759;
            --bg-dark: #0d1117;
        }

        * {
            box-sizing: border-box;
            user-select: none;
            -webkit-user-select: none;
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-dark);
            color: #fff;
            font-family: 'Rubik', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            overflow-x: hidden;
        }

        .arcade-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 50% 30%, #1f2937 0%, #0d1117 100%);
            z-index: -1;
        }

        .container {
            width: 100%;
            max-width: 950px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .title-container {
            text-align: center;
            margin-bottom: 25px;
        }

        .hd-title {
            font-size: 32px;
            font-weight: 900;
            background: linear-gradient(45deg, #ff3b30, #ffcc00, #34c759);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin: 5px 0;
            letter-spacing: 1px;
            filter: drop-shadow(0 4px 8px rgba(0,0,0,0.5));
        }

        .subtitle {
            font-size: 16px;
            color: #9ca3af;
            margin: 0;
        }

        .game-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
            gap: 20px;
            width: 100%;
        }

        .game-card {
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            flex-direction: column;
            align-items: center;
            backdrop-filter: blur(10px);
        }

        .game-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: var(--mario-yellow);
            box-shadow: 0 12px 30px rgba(255, 204, 0, 0.25);
            background: rgba(255, 255, 255, 0.08);
        }

        .game-card .icon {
            font-size: 48px;
            margin-bottom: 12px;
            filter: drop-shadow(0 4px 6px rgba(0,0,0,0.3));
        }

        .game-card h3 {
            font-size: 18px;
            font-weight: 700;
            color: #fff;
            margin: 5px 0 10px 0;
        }

        .game-card p {
            font-size: 13px;
            color: #9ca3af;
            margin: 0 0 15px 0;
            line-height: 1.4;
        }

        .tag-info {
            display: flex;
            gap: 10px;
            margin-top: auto;
        }

        .high-score-tag, .level-tag {
            font-size: 12px;
            font-weight: 700;
            padding: 5px 10px;
            border-radius: 20px;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .level-tag { color: var(--mario-green); }
        .high-score-tag { color: var(--mario-yellow); }

        .game-view {
            display: none;
            flex-direction: column;
            align-items: center;
            width: 100%;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            max-width: 650px;
            margin-bottom: 12px;
        }

        .btn-back {
            font-size: 14px;
            font-weight: 700;
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-back:hover {
            background: var(--mario-red);
            border-color: var(--mario-red);
        }

        .current-game-title {
            font-size: 18px;
            font-weight: 700;
            color: var(--mario-yellow);
        }

        #canvas-wrapper {
            position: relative;
            box-shadow: 0 20px 50px rgba(0,0,0,0.8);
            border: 3px solid rgba(255, 255, 255, 0.2);
            border-radius: 16px;
            overflow: hidden;
            background: #000;
        }

        canvas {
            display: block;
        }

        .mobile-controls {
            display: none;
            width: 100%;
            max-width: 650px;
            margin-top: 15px;
            justify-content: space-between;
            touch-action: manipulation;
        }

        .d-pad {
            display: grid;
            grid-template-columns: repeat(3, 55px);
            grid-template-rows: repeat(2, 55px);
            gap: 6px;
        }

        .btn-touch {
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 12px;
            color: white;
            font-size: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            backdrop-filter: blur(5px);
        }

        .btn-touch:active {
            background: rgba(255, 255, 255, 0.4);
        }

        .action-btns {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .btn-action {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: var(--mario-red);
            border: 2px solid #fff;
            color: white;
            font-weight: 700;
            font-size: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 15px rgba(255, 59, 48, 0.4);
        }

        @media (max-width: 768px) {
            .mobile-controls { display: flex; }
            .hd-title { font-size: 24px; }
        }
    </style>
</head>
<body>

    <div class="arcade-bg"></div>

    <div class="container">
        <!-- תפריט ראשי -->
        <div id="launcher-view" style="width: 100%;">
            <div class="title-container">
                <div class="hd-title">SUPER MARIO HD</div>
                <p class="subtitle">מהדורה מורחבת: 100 שלבים בכל משחק!</p>
            </div>

            <div class="game-grid">
                <div class="game-card" onclick="startGame(1)">
                    <div class="icon">🍄</div>
                    <h3>סופר מריו HD</h3>
                    <p>פלטפורמר מודרני חלק: דילוג מעל מכשולים וגומבות עד לשלב 100</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-1">שיא: 0</div>
                    </div>
                </div>

                <div class="game-card" onclick="startGame(2)">
                    <div class="icon">🪙</div>
                    <h3>ציד המטבעות</h3>
                    <p>אוסף מטבעות זהב והתחמקות מפצצות ואויבים נופלים</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-2">שיא: 0</div>
                    </div>
                </div>

                <div class="game-card" onclick="startGame(3)">
                    <div class="icon">🪠</div>
                    <h3>מריו מעוף הצינורות</h3>
                    <p>תזמון מדויק של מעוף בין סדרת צינורות ירוקים</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-3">שיא: 0</div>
                    </div>
                </div>

                <div class="game-card" onclick="startGame(4)">
                    <div class="icon">🧱</div>
                    <h3>מריו שובר הלבנים</h3>
                    <p>הרס לבנים והתקדמות בין 100 מבוכים מאתגרים</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-4">שיא: 0</div>
                    </div>
                </div>

                <div class="game-card" onclick="startGame(5)">
                    <div class="icon">🏎️</div>
                    <h3>מריו קארט HD</h3>
                    <p>מרוץ מטורף במסלול מהיר - התחמקות מכשולים עד לקו הסיום</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-5">שיא: 0</div>
                    </div>
                </div>

                <div class="game-card" onclick="startGame(6)">
                    <div class="icon">🔥</div>
                    <h3>בריחה מטירת באוזר</h3>
                    <p>ריצה מהירה מעל לבה, כדורי אש ומכשולים קטלניים</p>
                    <div class="tag-info">
                        <div class="level-tag">100 שלבים</div>
                        <div class="high-score-tag" id="hs-6">שיא: 0</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- אזור המשחק הפעיל -->
        <div id="game-view" class="game-view">
            <div class="game-header">
                <button class="btn-back" onclick="exitGame()">← חזרה לתפריט</button>
                <div class="current-game-title" id="game-title">מריו HD</div>
            </div>

            <div id="canvas-wrapper">
                <canvas id="gameCanvas" width="650" height="420"></canvas>
            </div>

            <!-- בקרים למובייל -->
            <div class="mobile-controls">
                <div class="d-pad">
                    <div class="btn-touch" style="grid-column: 1;" ontouchstart="setKey('ArrowLeft', true)" ontouchend="setKey('ArrowLeft', false)">◄</div>
                    <div class="btn-touch" style="grid-column: 3;" ontouchstart="setKey('ArrowRight', true)" ontouchend="setKey('ArrowRight', false)">►</div>
                </div>
                <div class="action-btns">
                    <div class="btn-action" ontouchstart="setKey('Space', true)" ontouchend="setKey('Space', false)">JUMP</div>
                </div>
            </div>
        </div>
    </div>

<script>
// Web Audio API - אפקטים קוליים
const AudioContext = window.AudioContext || window.webkitAudioContext;
let audioCtx = null;

function playSound(type) {
    if (!audioCtx) audioCtx = new AudioContext();
    if (audioCtx.state === 'suspended') audioCtx.resume();

    const osc = audioCtx.createOscillator();
    const gain = audioCtx.createGain();
    osc.connect(gain);
    gain.connect(audioCtx.destination);
    const now = audioCtx.currentTime;

    if (type === 'jump') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(200, now);
        osc.frequency.exponentialRampToValueAtTime(700, now + 0.12);
        gain.gain.setValueAtTime(0.12, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.12);
        osc.start(now);
        osc.stop(now + 0.12);
    } else if (type === 'coin') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(987.77, now);
        osc.frequency.setValueAtTime(1318.51, now + 0.08);
        gain.gain.setValueAtTime(0.12, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.22);
        osc.start(now);
        osc.stop(now + 0.22);
    } else if (type === 'level') {
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(440, now);
        osc.frequency.setValueAtTime(554.37, now + 0.1);
        osc.frequency.setValueAtTime(659.25, now + 0.2);
        gain.gain.setValueAtTime(0.15, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.35);
        osc.start(now);
        osc.stop(now + 0.35);
    } else if (type === 'gameover') {
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(320, now);
        osc.frequency.linearRampToValueAtTime(80, now + 0.4);
        gain.gain.setValueAtTime(0.15, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.4);
        osc.start(now);
        osc.stop(now + 0.4);
    }
}

function updateHighScoresDisplay() {
    for (let i = 1; i <= 6; i++) {
        const hs = localStorage.getItem(`mario_hd_hs_${i}`) || 0;
        document.getElementById(`hs-${i}`).innerText = `שיא: ${hs}`;
    }
}

function saveHighScore(gameId, score) {
    const current = localStorage.getItem(`mario_hd_hs_${gameId}`) || 0;
    if (score > current) {
        localStorage.setItem(`mario_hd_hs_${gameId}`, score);
        updateHighScoresDisplay();
    }
}

updateHighScoresDisplay();

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

let currentGameId = 0;
let animationFrameId = null;
let keys = {};

window.addEventListener('keydown', e => keys[e.code] = true);
window.addEventListener('keyup', e => keys[e.code] = false);

function setKey(code, val) { keys[code] = val; }

function exitGame() {
    if (animationFrameId) cancelAnimationFrame(animationFrameId);
    document.getElementById('game-view').style.display = 'none';
    document.getElementById('launcher-view').style.display = 'block';
    currentGameId = 0;
}

function startGame(gameId) {
    currentGameId = gameId;
    document.getElementById('launcher-view').style.display = 'none';
    document.getElementById('game-view').style.display = 'flex';
    
    const titles = [
        "", "סופר מריו HD", "ציד המטבעות", 
        "מריו מעוף הצינורות", "מריו שובר הלבנים", "מריו קארט HD", "בריחה מטירת באוזר"
    ];
    document.getElementById('game-title').innerText = titles[gameId];

    if (animationFrameId) cancelAnimationFrame(animationFrameId);

    if (gameId === 1) initGame1();
    else if (gameId === 2) initGame2();
    else if (gameId === 3) initGame3();
    else if (gameId === 4) initGame4();
    else if (gameId === 5) initGame5();
    else if (gameId === 6) initGame6();
}

// ציור דמות מריו חלקות ברזולוציה גבוהה (HD)
function drawMarioHD(x, y, scale = 1, isJumping = false) {
    ctx.save();
    ctx.translate(x, y);
    ctx.scale(scale, scale);

    // צל
    ctx.fillStyle = 'rgba(0,0,0,0.2)';
    ctx.beginPath();
    ctx.ellipse(14, 38, 12, 4, 0, 0, Math.PI * 2);
    ctx.fill();

    // נעליים
    ctx.fillStyle = '#5c3a21';
    ctx.beginPath();
    ctx.roundRect(2, 30, 10, 8, 4);
    ctx.roundRect(16, 30, 10, 8, 4);
    ctx.fill();

    // סרבל כחול
    ctx.fillStyle = '#007aff';
    ctx.beginPath();
    ctx.roundRect(5, 14, 18, 18, 5);
    ctx.fill();

    // כפתורים מוזהבים
    ctx.fillStyle = '#ffcc00';
    ctx.beginPath();
    ctx.arc(9, 20, 2, 0, Math.PI*2);
    ctx.arc(19, 20, 2, 0, Math.PI*2);
    ctx.fill();

    // חולצה אדומה
    ctx.fillStyle = '#ff3b30';
    ctx.beginPath();
    ctx.roundRect(2, 14, 6, 12, 3);
    ctx.roundRect(20, 14, 6, 12, 3);
    ctx.fill();

    // ראש ועור
    ctx.fillStyle = '#ffcc99';
    ctx.beginPath();
    ctx.arc(14, 10, 8, 0, Math.PI*2);
    ctx.fill();

    // שפם
    ctx.fillStyle = '#4a2c11';
    ctx.beginPath();
    ctx.roundRect(10, 10, 10, 4, 2);
    ctx.fill();

    // עיניים
    ctx.fillStyle = '#000';
    ctx.beginPath();
    ctx.arc(16, 8, 1.5, 0, Math.PI*2);
    ctx.fill();

    // כובע אדום
    ctx.fillStyle = '#ff3b30';
    ctx.beginPath();
    ctx.arc(14, 8, 9, Math.PI, Math.PI*2);
    ctx.fill();
    ctx.beginPath();
    ctx.roundRect(6, 6, 18, 4, 2);
    ctx.fill();

    ctx.restore();
}

// ==========================================
// משחק 1: סופר מריו HD (100 שלבים)
// ==========================================
function initGame1() {
    let level = 1;
    let score = 0;
    let gameOver = false;
    let player = { x: 50, y: 260, w: 28, h: 38, vx: 0, vy: 0, grounded: false };
    let cameraX = 0;

    function buildLevel(lvl) {
        let platCount = 4 + Math.min(lvl, 10);
        let plats = [{ x: 0, y: 340, w: 2500 + lvl * 100, h: 80, type: 'ground' }];
        let coins = [];
        let enemies = [];

        for (let i = 0; i < platCount; i++) {
            let px = 250 + i * 200 + Math.random() * 50;
            let py = 240 - (i % 3) * 50;
            plats.push({ x: px, y: py, w: 100, h: 20 });
            coins.push({ x: px + 40, y: py - 30, c: false });
        }

        let enemySpeed = 1.2 + (lvl * 0.05);
        for (let i = 0; i < 3 + Math.floor(lvl / 3); i++) {
            enemies.push({ x: 400 + i * 300, y: 310, w: 26, h: 26, vx: enemySpeed * (i % 2 === 0 ? 1 : -1) });
        }

        let flagX = 2200 + lvl * 100;
        return { plats, coins, enemies, flagX };
    }

    let levelData = buildLevel(level);

    function loop() {
        if (!gameOver) {
            player.vx = 0;
            if (keys['ArrowRight']) player.vx = 4;
            if (keys['ArrowLeft']) player.vx = -4;

            if ((keys['Space'] || keys['ArrowUp']) && player.grounded) {
                player.vy = -11;
                player.grounded = false;
                playSound('jump');
            }

            player.vy += 0.55;
            player.x += player.vx;
            player.y += player.vy;
            player.grounded = false;

            levelData.plats.forEach(p => {
                if (player.x < p.x + p.w && player.x + player.w > p.x &&
                    player.y + player.h >= p.y && player.y + player.h - player.vy <= p.y + 8 && player.vy >= 0) {
                    player.y = p.y - player.h;
                    player.vy = 0;
                    player.grounded = true;
                }
            });

            if (player.x < 0) player.x = 0;
            if (player.x > cameraX + 280) cameraX = player.x - 280;

            levelData.coins.forEach(c => {
                if (!c.c && Math.abs(player.x - c.x) < 25 && Math.abs(player.y - c.y) < 25) {
                    c.c = true;
                    score += 100;
                    playSound('coin');
                }
            });

            levelData.enemies.forEach(e => {
                e.x += e.vx;
                if (e.x < 200 || e.x > levelData.flagX) e.vx *= -1;

                if (Math.abs(player.x - e.x) < 22 && Math.abs(player.y - e.y) < 22) {
                    if (player.vy > 0 && player.y + player.h - player.vy <= e.y + 10) {
                        e.y = 1000;
                        player.vy = -7;
                        score += 200;
                        playSound('jump');
                    } else {
                        gameOver = true;
                        playSound('gameover');
                    }
                }
            });

            // מעבר שלב
            if (player.x >= levelData.flagX) {
                if (level < 100) {
                    level++;
                    score += 500;
                    playSound('level');
                    player.x = 50;
                    player.y = 260;
                    cameraX = 0;
                    levelData = buildLevel(level);
                }
            }

            if (player.y > 420) {
                gameOver = true;
                playSound('gameover');
            }
        }

        // ציור HD
        let skyGradient = ctx.createLinearGradient(0, 0, 0, 420);
        skyGradient.addColorStop(0, '#4a90e2');
        skyGradient.addColorStop(1, '#5c94fc');
        ctx.fillStyle = skyGradient;
        ctx.fillRect(0, 0, 650, 420);

        ctx.save();
        ctx.translate(-cameraX, 0);

        levelData.plats.forEach(p => {
            if (p.type === 'ground') {
                ctx.fillStyle = '#8b5a2b';
                ctx.fillRect(p.x, p.y, p.w, p.h);
                ctx.fillStyle = '#34c759';
                ctx.fillRect(p.x, p.y, p.w, 12);
            } else {
                ctx.fillStyle = '#d35400';
                ctx.beginPath();
                ctx.roundRect(p.x, p.y, p.w, p.h, 4);
                ctx.fill();
            }
        });

        levelData.coins.forEach(c => {
            if (!c.c) {
                ctx.fillStyle = '#ffcc00';
                ctx.beginPath();
                ctx.arc(c.x + 8, c.y + 8, 9, 0, Math.PI * 2);
                ctx.fill();
            }
        });

        // דגל סיום
        ctx.fillStyle = '#fff';
        ctx.fillRect(levelData.flagX, 140, 8, 200);
        ctx.fillStyle = '#34c759';
        ctx.beginPath();
        ctx.arc(levelData.flagX + 4, 136, 10, 0, Math.PI * 2);
        ctx.fill();

        levelData.enemies.forEach(e => {
            if (e.y < 500) {
                ctx.fillStyle = '#a0522d';
                ctx.beginPath();
                ctx.arc(e.x + 13, e.y + 13, 13, 0, Math.PI * 2);
                ctx.fill();
            }
        });

        drawMarioHD(player.x, player.y);

        ctx.restore();

        // מדדים (HUD)
        ctx.fillStyle = '#fff';
        ctx.font = 'bold 14px Rubik';
        ctx.fillText(`שלב: ${level} / 100`, 20, 30);
        ctx.fillText(`ניקוד: ${score}`, 180, 30);

        if (gameOver) {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(1, score);
        } else {
            animationFrameId = requestAnimationFrame(loop);
        }
    }
    loop();
}

// ==========================================
// משחק 2: ציד המטבעות HD (100 שלבים)
// ==========================================
function initGame2() {
    let level = 1;
    let score = 0;
    let coinsCollected = 0;
    let gameOver = false;
    let player = { x: 300, y: 340, w: 28, h: 38 };
    let coins = [];
    let bombs = [];
    let frame = 0;

    let targetCoins = 10 + level * 2;

    function loop() {
        if (!gameOver) {
            frame++;
            if (keys['ArrowRight'] && player.x < 610) player.x += 6;
            if (keys['ArrowLeft'] && player.x > 10) player.x -= 6;

            let spawnRate = Math.max(10, 35 - level);
            if (frame % spawnRate === 0) {
                coins.push({ x: Math.random() * 610 + 10, y: -20, speed: 2.5 + level * 0.1 });
            }
            if (frame % Math.max(30, 80 - level) === 0) {
                bombs.push({ x: Math.random() * 610 + 10, y: -20, speed: 3 + level * 0.1 });
            }

            coins.forEach((c, idx) => {
                c.y += c.speed;
                if (Math.abs(player.x - c.x) < 28 && Math.abs(player.y - c.y) < 28) {
                    score += 50;
                    coinsCollected++;
                    coins.splice(idx, 1);
                    playSound('coin');

                    if (coinsCollected >= targetCoins && level < 100) {
                        level++;
                        coinsCollected = 0;
                        targetCoins = 10 + level * 2;
                        playSound('level');
                    }
                }
            });

            bombs.forEach((b) => {
                b.y += b.speed;
                if (Math.abs(player.x - b.x) < 25 && Math.abs(player.y - b.y) < 25) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            ctx.fillStyle = '#1e293b';
            ctx.fillRect(0, 0, 650, 420);

            ctx.fillStyle = '#34c759';
            ctx.fillRect(0, 385, 650, 35);

            coins.forEach(c => {
                ctx.fillStyle = '#ffcc00';
                ctx.beginPath();
                ctx.arc(c.x, c.y, 11, 0, Math.PI * 2);
                ctx.fill();
            });

            bombs.forEach(b => {
                ctx.fillStyle = '#ff3b30';
                ctx.beginPath();
                ctx.arc(b.x, b.y, 13, 0, Math.PI * 2);
                ctx.fill();
            });

            drawMarioHD(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 14px Rubik';
            ctx.fillText(`שלב: ${level} / 100`, 20, 30);
            ctx.fillText(`מטבעות: ${coinsCollected} / ${targetCoins}`, 180, 30);
            ctx.fillText(`ניקוד: ${score}`, 400, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(2, score);
        }
    }
    loop();
}

// ==========================================
// משחק 3: מריו מעוף הצינורות HD (100 שלבים)
// ==========================================
function initGame3() {
    let level = 1;
    let score = 0;
    let gameOver = false;
    let player = { x: 120, y: 200, vy: 0, w: 28, h: 28 };
    let pipes = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            if (keys['Space'] || keys['ArrowUp']) {
                player.vy = -6.5;
                keys['Space'] = false;
                keys['ArrowUp'] = false;
                playSound('jump');
            }

            player.vy += 0.42;
            player.y += player.vy;

            let pipeSpeed = 2.5 + level * 0.05;
            let gapSize = Math.max(90, 130 - level * 0.4);

            if (frame % Math.max(60, 90 - level) === 0) {
                let gapY = Math.random() * 160 + 80;
                pipes.push({ x: 650, top: gapY, bottom: gapY + gapSize, passed: false });
            }

            pipes.forEach((p) => {
                p.x -= pipeSpeed;

                if (player.x + player.w > p.x && player.x < p.x + 55) {
                    if (player.y < p.top || player.y + player.h > p.bottom) {
                        gameOver = true;
                        playSound('gameover');
                    }
                }

                if (!p.passed && p.x < player.x) {
                    p.passed = true;
                    score += 20;
                    playSound('coin');
                    if (score % 100 === 0 && level < 100) {
                        level++;
                        playSound('level');
                    }
                }
            });

            if (player.y > 400 || player.y < 0) {
                gameOver = true;
                playSound('gameover');
            }

            ctx.fillStyle = '#38bdf8';
            ctx.fillRect(0, 0, 650, 420);

            pipes.forEach(p => {
                ctx.fillStyle = '#34c759';
                ctx.fillRect(p.x, 0, 55, p.top);
                ctx.fillRect(p.x, p.bottom, 55, 420 - p.bottom);
            });

            drawMarioHD(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 14px Rubik';
            ctx.fillText(`שלב: ${level} / 100`, 20, 30);
            ctx.fillText(`ניקוד: ${score}`, 180, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(3, score);
        }
    }
    loop();
}

// ==========================================
// משחק 4: מריו שובר הלבנים HD (100 שלבים)
// ==========================================
function initGame4() {
    let level = 1;
    let score = 0;
    let gameOver = false;
    let paddle = { x: 275, w: 90, h: 14 };
    let ball = { x: 325, y: 300, vx: 3.5, vy: -3.5, r: 9 };
    let bricks = [];

    function buildBricks(lvl) {
        let rows = Math.min(3 + Math.floor(lvl / 5), 7);
        let list = [];
        for (let r = 0; r < rows; r++) {
            for (let c = 0; c < 8; c++) {
                list.push({ x: c * 75 + 25, y: r * 24 + 40, w: 68, h: 18, alive: true });
            }
        }
        return list;
    }

    bricks = buildBricks(level);

    function loop() {
        if (!gameOver) {
            if (keys['ArrowRight'] && paddle.x < 560) paddle.x += 7;
            if (keys['ArrowLeft'] && paddle.x > 0) paddle.x -= 7;

            ball.x += ball.vx;
            ball.y += ball.vy;

            if (ball.x - ball.r < 0 || ball.x + ball.r > 650) ball.vx *= -1;
            if (ball.y - ball.r < 0) ball.vy *= -1;

            if (ball.y + ball.r >= 380 && ball.x > paddle.x && ball.x < paddle.x + paddle.w) {
                ball.vy = -Math.abs(ball.vy);
                playSound('jump');
            }

            let remaining = 0;
            bricks.forEach(b => {
                if (b.alive) {
                    remaining++;
                    if (ball.x > b.x && ball.x < b.x + b.w && ball.y - ball.r < b.y + b.h && ball.y + ball.r > b.y) {
                        b.alive = false;
                        ball.vy *= -1;
                        score += 30;
                        playSound('coin');
                    }
                }
            });

            if (remaining === 0 && level < 100) {
                level++;
                playSound('level');
                ball.x = 325;
                ball.y = 300;
                ball.vx = 3.5 + (level * 0.1);
                ball.vy = -3.5 - (level * 0.1);
                bricks = buildBricks(level);
            }

            if (ball.y > 420) {
                gameOver = true;
                playSound('gameover');
            }

            ctx.fillStyle = '#0f172a';
            ctx.fillRect(0, 0, 650, 420);

            bricks.forEach(b => {
                if (b.alive) {
                    ctx.fillStyle = '#e2e8f0';
                    ctx.beginPath();
                    ctx.roundRect(b.x, b.y, b.w, b.h, 4);
                    ctx.fill();
                }
            });

            ctx.fillStyle = '#ff3b30';
            ctx.beginPath();
            ctx.roundRect(paddle.x, 380, paddle.w, paddle.h, 6);
            ctx.fill();

            ctx.fillStyle = '#ffcc00';
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.r, 0, Math.PI * 2);
            ctx.fill();

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 14px Rubik';
            ctx.fillText(`שלב: ${level} / 100`, 20, 25);
            ctx.fillText(`ניקוד: ${score}`, 180, 25);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(4, score);
        }
    }
    loop();
}

// ==========================================
// משחק 5: מריו קארט HD (100 שלבים)
// ==========================================
function initGame5() {
    let level = 1;
    let score = 0;
    let gameOver = false;
    let playerX = 310;
    let obstacles = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            score++;
            let speed = 4 + level * 0.1;

            if (keys['ArrowRight'] && playerX < 470) playerX += 6;
            if (keys['ArrowLeft'] && playerX > 140) playerX -= 6;

            if (frame % Math.max(15, 45 - level) === 0) {
                obstacles.push({ x: Math.random() * 320 + 150, y: -30 });
            }

            obstacles.forEach((o) => {
                o.y += speed;
                if (Math.abs(playerX - o.x) < 30 && o.y > 330 && o.y < 380) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            if (score % 300 === 0 && level < 100) {
                level++;
                playSound('level');
            }

            ctx.fillStyle = '#334155';
            ctx.fillRect(140, 0, 370, 420);
            ctx.fillStyle = '#22c55e';
            ctx.fillRect(0, 0, 140, 420);
            ctx.fillRect(510, 0, 140, 420);

            obstacles.forEach(o => {
                ctx.fillStyle = '#ffcc00';
                ctx.beginPath();
                ctx.arc(o.x, o.y, 13, 0, Math.PI * 2);
                ctx.fill();
            });

            drawMarioHD(playerX, 340);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 14px Rubik';
            ctx.fillText(`שלב: ${level} / 100`, 20, 30);
            ctx.fillText(`ניקוד: ${score}`, 180, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(5, score);
        }
    }
    loop();
}

// ==========================================
// משחק 6: בריחה מטירת באוזר HD (100 שלבים)
// ==========================================
function initGame6() {
    let level = 1;
    let score = 0;
    let gameOver = false;
    let player = { x: 60, y: 300, vy: 0, grounded: false };
    let obstacles = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            score++;
            let speed = 5 + level * 0.1;

            if ((keys['Space'] || keys['ArrowUp']) && player.grounded) {
                player.vy = -12;
                player.grounded = false;
                playSound('jump');
            }

            player.vy += 0.65;
            player.y += player.vy;

            if (player.y >= 300) {
                player.y = 300;
                player.vy = 0;
                player.grounded = true;
            }

            if (frame % Math.max(35, 75 - level) === 0) {
                obstacles.push({ x: 650, w: 24, h: 36 });
            }

            obstacles.forEach((o) => {
                o.x -= speed;
                if (o.x < player.x + 24 && o.x + o.w > player.x && player.y + 36 > 330 - o.h) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            if (score % 300 === 0 && level < 100) {
                level++;
                playSound('level');
            }

            ctx.fillStyle = '#180808';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.fillRect(0, 360, 650, 60);

            ctx.fillStyle = '#475569';
            ctx.fillRect(0, 330, 650, 30);

            obstacles.forEach(o => {
                ctx.fillStyle = '#ff9500';
                ctx.fillRect(o.x, 330 - o.h, o.w, o.h);
            });

            drawMarioHD(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = 'bold 14px Rubik';
            ctx.fillText(`שלב: ${level} / 100`, 20, 30);
            ctx.fillText(`ניקוד: ${score}`, 180, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.75)';
            ctx.fillRect(0, 0, 650, 420);
            ctx.fillStyle = '#ff3b30';
            ctx.textAlign = 'center';
            ctx.font = 'bold 26px Rubik';
            ctx.fillText('משחק הסתיים!', 325, 210);
            ctx.textAlign = 'left';
            saveHighScore(6, score);
        }
    }
    loop();
}
</script>

</body>
</html>
