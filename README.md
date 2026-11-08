<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Super Mario Arcade Collection</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Rubik:wght@700&display=swap" rel="stylesheet">
    <style>
        :root {
            --mario-red: #e52521;
            --mario-blue: #00247d;
            --mario-yellow: #fbd000;
            --mario-green: #43b047;
            --sky-blue: #5c94fc;
        }

        * {
            box-sizing: border-box;
            user-select: none;
            -webkit-user-select: none;
        }

        body {
            margin: 0;
            padding: 0;
            background-color: #0f0f1b;
            color: #fff;
            font-family: 'Rubik', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* רקע ארקייד דינמי */
        .arcade-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, #1b2735 0%, #090a0f 100%);
            z-index: -1;
        }

        .container {
            width: 100%;
            max-width: 900px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* כותרת ארקייד retro */
        .title-container {
            text-align: center;
            margin-bottom: 20px;
        }

        .pixel-title {
            font-family: 'Press Start 2P', cursive;
            font-size: 26px;
            color: var(--mario-yellow);
            text-shadow: 4px 4px var(--mario-red), -2px -2px #000;
            margin: 10px 0;
            letter-spacing: 2px;
            line-height: 1.4;
        }

        .subtitle {
            font-size: 14px;
            color: #aaa;
            margin: 0;
        }

        /* לוח הבחירה - Launcher Dashboard */
        .game-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            width: 100%;
            margin-top: 10px;
        }

        .game-card {
            background: rgba(255, 255, 255, 0.05);
            border: 4px solid #333;
            border-radius: 12px;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .game-card:hover {
            transform: translateY(-5px);
            border-color: var(--mario-yellow);
            box-shadow: 0 8px 20px rgba(251, 208, 0, 0.3);
            background: rgba(255, 255, 255, 0.1);
        }

        .game-card .icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        .game-card h3 {
            font-family: 'Press Start 2P', cursive;
            font-size: 13px;
            color: #fff;
            margin: 10px 0;
        }

        .game-card p {
            font-size: 12px;
            color: #ccc;
            margin: 0 0 10px 0;
        }

        .high-score-tag {
            font-size: 11px;
            color: var(--mario-yellow);
            background: rgba(0,0,0,0.5);
            padding: 4px 8px;
            border-radius: 4px;
            margin-top: auto;
        }

        /* אזור המשחק */
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
            max-width: 600px;
            margin-bottom: 10px;
        }

        .btn-back {
            font-family: 'Press Start 2P', cursive;
            font-size: 10px;
            background: var(--mario-red);
            color: white;
            border: 2px solid #fff;
            padding: 8px 12px;
            border-radius: 6px;
            cursor: pointer;
            box-shadow: 2px 2px 0 #000;
        }

        .btn-back:active {
            transform: translate(2px, 2px);
            box-shadow: none;
        }

        .current-game-title {
            font-family: 'Press Start 2P', cursive;
            font-size: 14px;
            color: var(--mario-yellow);
        }

        #canvas-wrapper {
            position: relative;
            box-shadow: 0 0 30px rgba(0,0,0,0.8);
            border: 4px solid #fff;
            border-radius: 8px;
            overflow: hidden;
            background: #000;
        }

        canvas {
            display: block;
            background: var(--sky-blue);
        }

        /* בקרים למובייל */
        .mobile-controls {
            display: none;
            width: 100%;
            max-width: 600px;
            margin-top: 15px;
            justify-content: space-between;
            touch-action: manipulation;
        }

        .d-pad {
            display: grid;
            grid-template-columns: repeat(3, 50px);
            grid-template-rows: repeat(2, 50px);
            gap: 5px;
        }

        .btn-touch {
            background: rgba(255, 255, 255, 0.2);
            border: 2px solid #fff;
            border-radius: 8px;
            color: white;
            font-size: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        .btn-touch:active {
            background: rgba(255, 255, 255, 0.5);
        }

        .action-btns {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .btn-action {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: var(--mario-red);
            border: 3px solid #fff;
            color: white;
            font-family: 'Press Start 2P', cursive;
            font-size: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 3px 3px 0 #000;
        }

        @media (max-width: 768px) {
            .mobile-controls {
                display: flex;
            }
            .pixel-title {
                font-size: 18px;
            }
        }
    </style>
</head>
<body>

    <div class="arcade-bg"></div>

    <div class="container">
        <!-- תפריט ראשי -->
        <div id="launcher-view" style="width: 100%;">
            <div class="title-container">
                <div class="pixel-title">SUPER MARIO<br>ARCADE COLLECTION</div>
                <p class="subtitle">בחר משחק והתחל לשחק!</p>
            </div>

            <div class="game-grid">
                <div class="game-card" onclick="startGame(1)">
                    <div class="icon">🍄</div>
                    <h3>סופר מריו קלאסי</h3>
                    <p>ריצה, קפיצות מעל גומבות והגעה לדגל</p>
                    <div class="high-score-tag" id="hs-1">שיא: 0</div>
                </div>

                <div class="game-card" onclick="startGame(2)">
                    <div class="icon">🪙</div>
                    <h3>תפוס את המטבעות</h3>
                    <p>אוסף מטבעות מהאוויר והתחמק מבאוזר</p>
                    <div class="high-score-tag" id="hs-2">שיא: 0</div>
                </div>

                <div class="game-card" onclick="startGame(3)">
                    <div class="icon">🪠</div>
                    <h3>Pipe Jump</h3>
                    <p>תזמון מדויק של מעוף בין הצינורות</p>
                    <div class="high-score-tag" id="hs-3">שיא: 0</div>
                </div>

                <div class="game-card" onclick="startGame(4)">
                    <div class="icon">🧱</div>
                    <h3>שובר הלבנים</h3>
                    <p>הרס את כל הלבנים בעזרת השריון</p>
                    <div class="high-score-tag" id="hs-4">שיא: 0</div>
                </div>

                <div class="game-card" onclick="startGame(5)">
                    <div class="icon">🏎️</div>
                    <h3>מריו קארט רטרו</h3>
                    <p>מרוץ התחמקות מכשולים במסלול</p>
                    <div class="high-score-tag" id="hs-5">שיא: 0</div>
                </div>

                <div class="game-card" onclick="startGame(6)">
                    <div class="icon">🔥</div>
                    <h3>בריחה מטירת באוזר</h3>
                    <p>דילוג מעל מכשולי אש ולבה</p>
                    <div class="high-score-tag" id="hs-6">שיא: 0</div>
                </div>
            </div>
        </div>

        <!-- אזור המשחק הפעיל -->
        <div id="game-view" class="game-view">
            <div class="game-header">
                <button class="btn-back" onclick="exitGame()">← חזרה לתפריט</button>
                <div class="current-game-title" id="game-title">מריו קלאסי</div>
            </div>

            <div id="canvas-wrapper">
                <canvas id="gameCanvas" width="600" height="400"></canvas>
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
// מחולל צלילים (Web Audio API)
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
        osc.type = 'square';
        osc.frequency.setValueAtTime(150, now);
        osc.frequency.exponentialRampToValueAtTime(600, now + 0.15);
        gain.gain.setValueAtTime(0.1, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.15);
        osc.start(now);
        osc.stop(now + 0.15);
    } else if (type === 'coin') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(987.77, now); // B5
        osc.frequency.setValueAtTime(1318.51, now + 0.08); // E6
        gain.gain.setValueAtTime(0.1, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.25);
        osc.start(now);
        osc.stop(now + 0.25);
    } else if (type === 'gameover') {
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(300, now);
        osc.frequency.linearRampToValueAtTime(100, now + 0.4);
        gain.gain.setValueAtTime(0.15, now);
        gain.gain.linearRampToValueAtTime(0.01, now + 0.4);
        osc.start(now);
        osc.stop(now + 0.4);
    }
}

// ניהול שיאים
function updateHighScoresDisplay() {
    for (let i = 1; i <= 6; i++) {
        const hs = localStorage.getItem(`mario_hs_${i}`) || 0;
        document.getElementById(`hs-${i}`).innerText = `שיא: ${hs}`;
    }
}

function saveHighScore(gameId, score) {
    const current = localStorage.getItem(`mario_hs_${gameId}`) || 0;
    if (score > current) {
        localStorage.setItem(`mario_hs_${gameId}`, score);
        updateHighScoresDisplay();
    }
}

updateHighScoresDisplay();

// מנוע המשחקים
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

let currentGameId = 0;
let animationFrameId = null;
let keys = {};

window.addEventListener('keydown', e => keys[e.code] = true);
window.addEventListener('keyup', e => keys[e.code] = false);

function setKey(code, val) {
    keys[code] = val;
}

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
        "", "סופר מריו קלאסי", "תפוס את המטבעות", 
        "Pipe Jump", "שובר הלבנים", "מריו קארט רטרו", "בריחה מטירת באוזר"
    ];
    document.getElementById('game-title').innerText = titles[gameId];

    if (animationFrameId) cancelAnimationFrame(animationFrameId);

    // אתחול משחק לפי ID
    if (gameId === 1) initGame1();
    else if (gameId === 2) initGame2();
    else if (gameId === 3) initGame3();
    else if (gameId === 4) initGame4();
    else if (gameId === 5) initGame5();
    else if (gameId === 6) initGame6();
}

// ציור דמות מריו 8-Bit
function drawMarioSprite(x, y, isJumping = false) {
    // כובע ופנים
    ctx.fillStyle = '#e52521'; // אדום
    ctx.fillRect(x + 4, y, 16, 6);
    ctx.fillStyle = '#f8b500'; // עור
    ctx.fillRect(x + 4, y + 6, 16, 8);
    ctx.fillStyle = '#000'; // עיניים
    ctx.fillRect(x + 14, y + 8, 4, 4);

    // סרבל כחול
    ctx.fillStyle = '#00247d';
    ctx.fillRect(x + 4, y + 14, 16, 14);
    ctx.fillStyle = '#e52521';
    ctx.fillRect(x, y + 14, 4, 10);
    ctx.fillRect(x + 20, y + 14, 4, 10);

    // נעליים
    ctx.fillStyle = '#6b3c00';
    ctx.fillRect(x + 2, y + 28, 8, 4);
    ctx.fillRect(x + 14, y + 28, 8, 4);
}

// ==========================================
// משחק 1: סופר מריו קלאסי
// ==========================================
function initGame1() {
    let score = 0;
    let gameOver = false;
    let win = false;

    let player = { x: 50, y: 260, w: 24, h: 32, vx: 0, vy: 0, grounded: false };
    let cameraX = 0;

    const platforms = [
        { x: 0, y: 320, w: 1200, h: 80, type: 'ground' },
        { x: 200, y: 230, w: 90, h: 20 },
        { x: 380, y: 170, w: 100, h: 20 },
        { x: 580, y: 220, w: 120, h: 20 },
        { x: 800, y: 180, w: 100, h: 20 }
    ];

    const coins = [
        { x: 230, y: 190, c: false },
        { x: 420, y: 130, c: false },
        { x: 630, y: 180, c: false }
    ];

    const enemies = [
        { x: 300, y: 290, w: 24, h: 24, vx: -1.2, dir: -1 },
        { x: 650, y: 290, w: 24, h: 24, vx: 1.2, dir: 1 }
    ];

    const flag = { x: 1100, y: 120, w: 10, h: 200 };

    function loop() {
        if (!gameOver && !win) {
            // מקשים
            player.vx = 0;
            if (keys['ArrowRight']) player.vx = 3.5;
            if (keys['ArrowLeft']) player.vx = -3.5;

            if ((keys['Space'] || keys['ArrowUp']) && player.grounded) {
                player.vy = -10;
                player.grounded = false;
                playSound('jump');
            }

            player.vy += 0.5;
            player.x += player.vx;
            player.y += player.vy;

            player.grounded = false;

            // התנגשות משטחים
            platforms.forEach(p => {
                if (player.x < p.x + p.w && player.x + player.w > p.x &&
                    player.y + player.h >= p.y && player.y + player.h - player.vy <= p.y + 6 && player.vy >= 0) {
                    player.y = p.y - player.h;
                    player.vy = 0;
                    player.grounded = true;
                }
            });

            if (player.x < 0) player.x = 0;

            // מצלמה
            if (player.x > cameraX + 250) cameraX = player.x - 250;

            // איסוף מטבעות
            coins.forEach(c => {
                if (!c.c && Math.abs(player.x - c.x) < 20 && Math.abs(player.y - c.y) < 20) {
                    c.c = true;
                    score += 100;
                    playSound('coin');
                }
            });

            // אויבים
            enemies.forEach(e => {
                e.x += e.vx;
                if (e.x < 200 || e.x > 800) e.vx *= -1;

                if (Math.abs(player.x - e.x) < 20 && Math.abs(player.y - e.y) < 20) {
                    if (player.vy > 0 && player.y + player.h - player.vy <= e.y + 10) {
                        e.y = 1000;
                        player.vy = -6;
                        score += 200;
                        playSound('jump');
                    } else {
                        gameOver = true;
                        playSound('gameover');
                    }
                }
            });

            // ניצחון
            if (player.x >= flag.x) {
                win = true;
                score += 500;
                saveHighScore(1, score);
            }

            if (player.y > 400) {
                gameOver = true;
                playSound('gameover');
            }
        }

        // ציור
        ctx.fillStyle = '#5c94fc';
        ctx.fillRect(0, 0, 600, 400);

        ctx.save();
        ctx.translate(-cameraX, 0);

        // משטחים
        platforms.forEach(p => {
            if (p.type === 'ground') {
                ctx.fillStyle = '#d88000';
                ctx.fillRect(p.x, p.y, p.w, p.h);
                ctx.fillStyle = '#00a800';
                ctx.fillRect(p.x, p.y, p.w, 8);
            } else {
                ctx.fillStyle = '#c84c0c';
                ctx.fillRect(p.x, p.y, p.w, p.h);
            }
        });

        // מטבעות
        coins.forEach(c => {
            if (!c.c) {
                ctx.fillStyle = '#fbd000';
                ctx.beginPath();
                ctx.arc(c.x + 8, c.y + 8, 8, 0, Math.PI * 2);
                ctx.fill();
            }
        });

        // דגל
        ctx.fillStyle = '#fff';
        ctx.fillRect(flag.x, flag.y, flag.w, flag.h);
        ctx.fillStyle = '#43b047';
        ctx.fillRect(flag.x + 10, flag.y + 10, 40, 25);

        // אויבים
        enemies.forEach(e => {
            if (e.y < 500) {
                ctx.fillStyle = '#795548';
                ctx.fillRect(e.x, e.y, e.w, e.h);
            }
        });

        // מריו
        drawMarioSprite(player.x, player.y);

        ctx.restore();

        // ניקוד
        ctx.fillStyle = '#fff';
        ctx.font = '12px "Press Start 2P"';
        ctx.fillText(`SCORE: ${score}`, 20, 30);

        if (gameOver || win) {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = win ? '#fbd000' : '#e52521';
            ctx.textAlign = 'center';
            ctx.fillText(win ? 'STAGE CLEAR!' : 'GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(1, score);
        } else {
            animationFrameId = requestAnimationFrame(loop);
        }
    }
    loop();
}

// ==========================================
// משחק 2: תפוס את המטבעות
// ==========================================
function initGame2() {
    let score = 0;
    let gameOver = false;
    let player = { x: 280, y: 340, w: 24, h: 32 };
    let coins = [];
    let bombs = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            if (keys['ArrowRight'] && player.x < 570) player.x += 5;
            if (keys['ArrowLeft'] && player.x > 10) player.x -= 5;

            if (frame % 30 === 0) {
                coins.push({ x: Math.random() * 560 + 10, y: -20, speed: 2 + Math.random() * 2 });
            }
            if (frame % 90 === 0) {
                bombs.push({ x: Math.random() * 560 + 10, y: -20, speed: 3 });
            }

            // עדכון מטבעות
            coins.forEach((c, idx) => {
                c.y += c.speed;
                if (Math.abs(player.x - c.x) < 25 && Math.abs(player.y - c.y) < 25) {
                    score += 50;
                    coins.splice(idx, 1);
                    playSound('coin');
                }
            });

            // עדכון פצצות
            bombs.forEach((b) => {
                b.y += b.speed;
                if (Math.abs(player.x - b.x) < 25 && Math.abs(player.y - b.y) < 25) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            ctx.fillStyle = '#5c94fc';
            ctx.fillRect(0, 0, 600, 400);

            // קרקע
            ctx.fillStyle = '#00a800';
            ctx.fillRect(0, 372, 600, 28);

            // מטבעות
            coins.forEach(c => {
                ctx.fillStyle = '#fbd000';
                ctx.beginPath();
                ctx.arc(c.x, c.y, 10, 0, Math.PI * 2);
                ctx.fill();
            });

            // פצצות
            bombs.forEach(b => {
                ctx.fillStyle = '#000';
                ctx.beginPath();
                ctx.arc(b.x, b.y, 12, 0, Math.PI * 2);
                ctx.fill();
            });

            drawMarioSprite(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText(`SCORE: ${score}`, 20, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#e52521';
            ctx.textAlign = 'center';
            ctx.font = '16px "Press Start 2P"';
            ctx.fillText('GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(2, score);
        }
    }
    loop();
}

// ==========================================
// משחק 3: Pipe Jump (סגנון מריו מעופף)
// ==========================================
function initGame3() {
    let score = 0;
    let gameOver = false;
    let player = { x: 100, y: 200, vy: 0, w: 24, h: 24 };
    let pipes = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            if (keys['Space'] || keys['ArrowUp']) {
                player.vy = -6;
                keys['Space'] = false;
                keys['ArrowUp'] = false;
                playSound('jump');
            }

            player.vy += 0.4;
            player.y += player.vy;

            if (frame % 90 === 0) {
                let gapY = Math.random() * 180 + 80;
                pipes.push({ x: 600, top: gapY, bottom: gapY + 110, passed: false });
            }

            pipes.forEach((p, idx) => {
                p.x -= 2.5;

                // התנגשות צינורות
                if (player.x + player.w > p.x && player.x < p.x + 50) {
                    if (player.y < p.top || player.y + player.h > p.bottom) {
                        gameOver = true;
                        playSound('gameover');
                    }
                }

                if (!p.passed && p.x < player.x) {
                    p.passed = true;
                    score += 10;
                    playSound('coin');
                }
            });

            if (player.y > 380 || player.y < 0) {
                gameOver = true;
                playSound('gameover');
            }

            ctx.fillStyle = '#70c5ce';
            ctx.fillRect(0, 0, 600, 400);

            // צינורות
            pipes.forEach(p => {
                ctx.fillStyle = '#73c700';
                ctx.fillRect(p.x, 0, 50, p.top);
                ctx.fillRect(p.x, p.bottom, 50, 400 - p.bottom);
            });

            drawMarioSprite(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText(`SCORE: ${score}`, 20, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#e52521';
            ctx.textAlign = 'center';
            ctx.font = '16px "Press Start 2P"';
            ctx.fillText('GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(3, score);
        }
    }
    loop();
}

// ==========================================
// משחק 4: שובר הלבנים
// ==========================================
function initGame4() {
    let score = 0;
    let gameOver = false;
    let paddle = { x: 250, w: 80, h: 12 };
    let ball = { x: 300, y: 300, vx: 3, vy: -3, r: 8 };

    let bricks = [];
    for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 7; c++) {
            bricks.push({ x: c * 80 + 20, y: r * 25 + 40, w: 70, h: 18, alive: true });
        }
    }

    function loop() {
        if (!gameOver) {
            if (keys['ArrowRight'] && paddle.x < 520) paddle.x += 6;
            if (keys['ArrowLeft'] && paddle.x > 0) paddle.x -= 6;

            ball.x += ball.vx;
            ball.y += ball.vy;

            // התנגשות קירות
            if (ball.x < 0 || ball.x > 600) ball.vx *= -1;
            if (ball.y < 0) ball.vy *= -1;

            // התנגשות מחבט
            if (ball.y + ball.r >= 360 && ball.x > paddle.x && ball.x < paddle.x + paddle.w) {
                ball.vy = -Math.abs(ball.vy);
                playSound('jump');
            }

            // התנגשות לבנים
            bricks.forEach(b => {
                if (b.alive && ball.x > b.x && ball.x < b.x + b.w && ball.y - ball.r < b.y + b.h && ball.y + ball.r > b.y) {
                    b.alive = false;
                    ball.vy *= -1;
                    score += 20;
                    playSound('coin');
                }
            });

            if (ball.y > 400) {
                gameOver = true;
                playSound('gameover');
            }

            ctx.fillStyle = '#111';
            ctx.fillRect(0, 0, 600, 400);

            // לבנים
            bricks.forEach(b => {
                if (b.alive) {
                    ctx.fillStyle = '#c84c0c';
                    ctx.fillRect(b.x, b.y, b.w, b.h);
                }
            });

            // מחבט וכדור
            ctx.fillStyle = '#e52521';
            ctx.fillRect(paddle.x, 360, paddle.w, paddle.h);

            ctx.fillStyle = '#fbd000';
            ctx.beginPath();
            ctx.arc(ball.x, ball.y, ball.r, 0, Math.PI * 2);
            ctx.fill();

            ctx.fillStyle = '#fff';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText(`SCORE: ${score}`, 20, 25);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#e52521';
            ctx.textAlign = 'center';
            ctx.font = '16px "Press Start 2P"';
            ctx.fillText('GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(4, score);
        }
    }
    loop();
}

// ==========================================
// משחק 5: מריו קארט רטרו
// ==========================================
function initGame5() {
    let score = 0;
    let gameOver = false;
    let playerX = 280;
    let obstacles = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            score++;
            if (keys['ArrowRight'] && playerX < 440) playerX += 5;
            if (keys['ArrowLeft'] && playerX > 120) playerX -= 5;

            if (frame % 40 === 0) {
                obstacles.push({ x: Math.random() * 300 + 130, y: -30 });
            }

            obstacles.forEach((o) => {
                o.y += 4;
                if (Math.abs(playerX - o.x) < 30 && o.y > 320 && o.y < 370) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            ctx.fillStyle = '#555'; // כביש
            ctx.fillRect(120, 0, 360, 400);
            ctx.fillStyle = '#43b047'; // דשא בצדדים
            ctx.fillRect(0, 0, 120, 400);
            ctx.fillRect(480, 0, 120, 400);

            // מכשולים (בננות)
            obstacles.forEach(o => {
                ctx.fillStyle = '#fbd000';
                ctx.beginPath();
                ctx.arc(o.x, o.y, 12, 0, Math.PI * 2);
                ctx.fill();
            });

            // מריו קארט
            drawMarioSprite(playerX, 330);

            ctx.fillStyle = '#fff';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText(`SCORE: ${score}`, 20, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#e52521';
            ctx.textAlign = 'center';
            ctx.font = '16px "Press Start 2P"';
            ctx.fillText('GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(5, score);
        }
    }
    loop();
}

// ==========================================
// משחק 6: בריחה מטירת באוזר
// ==========================================
function initGame6() {
    let score = 0;
    let gameOver = false;
    let player = { x: 50, y: 280, vy: 0, grounded: false };
    let obstacles = [];
    let frame = 0;

    function loop() {
        if (!gameOver) {
            frame++;
            score++;
            if ((keys['Space'] || keys['ArrowUp']) && player.grounded) {
                player.vy = -11;
                player.grounded = false;
                playSound('jump');
            }

            player.vy += 0.6;
            player.y += player.vy;

            if (player.y >= 280) {
                player.y = 280;
                player.vy = 0;
                player.grounded = true;
            }

            if (frame % 80 === 0) {
                obstacles.push({ x: 600, w: 20, h: 30 });
            }

            obstacles.forEach((o) => {
                o.x -= 5;
                if (o.x < player.x + 20 && o.x + o.w > player.x && player.y + 32 > 310 - o.h) {
                    gameOver = true;
                    playSound('gameover');
                }
            });

            ctx.fillStyle = '#220000'; // טירה
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#d88000'; // לבה
            ctx.fillRect(0, 340, 600, 60);

            // רצפת טירה
            ctx.fillStyle = '#444';
            ctx.fillRect(0, 310, 600, 30);

            // מכשולי אש
            obstacles.forEach(o => {
                ctx.fillStyle = '#e52521';
                ctx.fillRect(o.x, 310 - o.h, o.w, o.h);
            });

            drawMarioSprite(player.x, player.y);

            ctx.fillStyle = '#fff';
            ctx.font = '12px "Press Start 2P"';
            ctx.fillText(`SCORE: ${score}`, 20, 30);

            animationFrameId = requestAnimationFrame(loop);
        } else {
            ctx.fillStyle = 'rgba(0,0,0,0.7)';
            ctx.fillRect(0, 0, 600, 400);
            ctx.fillStyle = '#e52521';
            ctx.textAlign = 'center';
            ctx.font = '16px "Press Start 2P"';
            ctx.fillText('GAME OVER', 300, 200);
            ctx.textAlign = 'left';
            saveHighScore(6, score);
        }
    }
    loop();
}
</script>

</body>
</html>
