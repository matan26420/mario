<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Super Mario World</title>
    <style>
        body {
            background-color: #5c94fc;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            font-family: 'Courier New', Courier, monospace;
            color: white;
            overflow: hidden;
            user-select: none;
        }

        .game-header {
            text-align: center;
            margin-bottom: 10px;
        }

        h1 {
            margin: 0;
            font-size: 32px;
            color: #fbd000;
            text-shadow: 3px 3px #000, -2px -2px #e52521;
            letter-spacing: 2px;
        }

        #gameCanvas {
            border: 4px solid #000;
            background: linear-gradient(to bottom, #5c94fc 0%, #5c94fc 70%, #d88000 70%, #d88000 100%);
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            max-width: 100%;
            border-radius: 4px;
        }

        .controls-info {
            margin-top: 12px;
            font-size: 14px;
            background: rgba(0,0,0,0.6);
            padding: 8px 20px;
            border-radius: 20px;
            border: 2px solid #fff;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }

        .controls-info span {
            color: #fbd000;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="game-header">
        <h1>SUPER MARIO BROS</h1>
    </div>

    <canvas id="gameCanvas" width="600" height="400"></canvas>

    <div class="controls-info">
        🎮 תנועה: <span>← →</span> | קפיצה: <span>Space</span> / <span>↑</span>
    </div>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

let score = 0;
let coins = 0;
let gameOver = false;
let gameWon = false;

let mario = {
    x: 50,
    y: 260,
    width: 30,
    height: 40,
    vx: 0,
    vy: 0,
    speed: 4,
    jumpPower: -10,
    grounded: false,
    color: '#e52521'
};

let gravity = 0.5;

let platforms = [
    { x: 0, y: 320, width: 1400, height: 80, type: 'ground' },
    { x: 200, y: 220, width: 100, height: 20, type: 'brick' },
    { x: 350, y: 150, width: 120, height: 20, type: 'brick' },
    { x: 550, y: 220, width: 140, height: 20, type: 'brick' },
    { x: 750, y: 180, width: 100, height: 20, type: 'brick' },
    { x: 950, y: 240, width: 120, height: 20, type: 'brick' }
];

let items = [
    { x: 235, y: 180, width: 15, height: 15, collected: false },
    { x: 400, y: 110, width: 15, height: 15, collected: false },
    { x: 600, y: 180, width: 15, height: 15, collected: false },
    { x: 800, y: 140, width: 15, height: 15, collected: false }
];

let enemies = [
    { x: 300, y: 290, width: 30, height: 30, vx: 1, minX: 200, maxX: 300 },
    { x: 600, y: 290, width: 30, height: 30, vx: -1.5, minX: 550, maxX: 690 },
    { x: 850, y: 290, width: 30, height: 30, vx: 1, minX: 750, maxX: 900 }
];

let flagpole = { x: 1200, y: 120, width: 10, height: 200 };

let keys = {};
window.addEventListener('keydown', e => {
    keys[e.code] = true;
    if((e.code === 'Space' || e.code === 'ArrowUp') && mario.grounded) {
        mario.vy = mario.jumpPower;
        mario.grounded = false;
    }
});
window.addEventListener('keyup', e => {
    keys[e.code] = false;
});

let cameraX = 0;

function update() {
    if (gameOver || gameWon) return;

    mario.vx = 0;
    if (keys['ArrowRight']) {
        mario.vx = mario.speed;
    }
    if (keys['ArrowLeft']) {
        mario.vx = -mario.speed;
    }

    mario.vy += gravity;
    mario.x += mario.vx;
    mario.y += mario.vy;

    mario.grounded = false;

    platforms.forEach(plat => {
        if (
            mario.x < plat.x + plat.width &&
            mario.x + mario.width > plat.x &&
            mario.y + mario.height >= plat.y &&
            mario.y + mario.height - mario.vy <= plat.y + 5 &&
            mario.vy >= 0
        ) {
            mario.y = plat.y - mario.height;
            mario.vy = 0;
            mario.grounded = true;
        }
    });

    if (mario.x < 0) mario.x = 0;

    if (mario.x > cameraX + 250) {
        cameraX = mario.x - 250;
    } else if (mario.x < cameraX + 150 && cameraX > 0) {
        cameraX = mario.x - 150;
        if (cameraX < 0) cameraX = 0;
    }

    items.forEach(item => {
        if (!item.collected &&
            mario.x < item.x + item.width &&
            mario.x + mario.width > item.x &&
            mario.y < item.y + item.height &&
            mario.y + mario.height > item.y
        ) {
            item.collected = true;
            coins++;
            score += 100;
        }
    });

    enemies.forEach(en => {
        en.x += en.vx;
        if (en.x <= en.minX || en.x >= en.maxX) {
            en.vx *= -1;
        }

        if (
            mario.x < en.x + en.width &&
            mario.x + mario.width > en.x &&
            mario.y < en.y + en.height &&
            mario.y + mario.height > en.y
        ) {
            if (mario.vy > 0 && mario.y + mario.height - mario.vy <= en.y + 10) {
                en.y = 1000;
                en.vx = 0;
                mario.vy = -7;
                score += 200;
            } else {
                gameOver = true;
            }
        }
    });

    if (
        mario.x < flagpole.x + flagpole.width &&
        mario.x + mario.width > flagpole.x &&
        mario.y < flagpole.y + flagpole.height &&
        mario.y + mario.height > flagpole.y
    ) {
        gameWon = true;
    }

    if (mario.y > canvas.height) {
        gameOver = true;
    }
}

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    ctx.save();
    ctx.translate(-cameraX, 0);

    ctx.fillStyle = "#fff";
    ctx.fillRect(150, 80, 60, 20);
    ctx.fillRect(450, 60, 80, 20);
    ctx.fillRect(750, 90, 70, 20);
    ctx.fillRect(1000, 50, 90, 20);

    platforms.forEach(plat => {
        if (plat.type === 'ground') {
            ctx.fillStyle = '#d88000';
            ctx.fillRect(plat.x, plat.y, plat.width, plat.height);
            ctx.fillStyle = '#00a800';
            ctx.fillRect(plat.x, plat.y, plat.width, 10);
        } else {
            ctx.fillStyle = '#c84c0c';
            ctx.fillRect(plat.x, plat.y, plat.width, plat.height);
            ctx.strokeStyle = '#000';
            ctx.strokeRect(plat.x, plat.y, plat.width, plat.height);
        }
    });

    items.forEach(item => {
        if (!item.collected) {
            ctx.fillStyle = '#fbd000';
            ctx.beginPath();
            ctx.arc(item.x + item.width/2, item.y + item.height/2, item.width/2, 0, Math.PI * 2);
            ctx.fill();
            ctx.strokeStyle = '#000';
            ctx.stroke();
        }
    });

    enemies.forEach(en => {
        ctx.fillStyle = '#8b4513';
        ctx.fillRect(en.x, en.y, en.width, en.height);
        ctx.fillStyle = '#fff';
        ctx.fillRect(en.x + 5, en.y + 8, 6, 6);
        ctx.fillRect(en.x + 18, en.y + 8, 6, 6);
    });

    ctx.fillStyle = '#000';
    ctx.fillRect(flagpole.x, flagpole.y, flagpole.width, flagpole.height);
    ctx.fillStyle = '#00a800';
    ctx.fillRect(flagpole.x + 10, flagpole.y + 10, 40, 30);

    ctx.fillStyle = mario.color;
    ctx.fillRect(mario.x, mario.y, mario.width, mario.height);
    ctx.fillStyle = '#f8b500';
    ctx.fillRect(mario.x + 15, mario.y + 5, 12, 12);

    ctx.restore();

    ctx.fillStyle = '#000';
    ctx.font = 'bold 16px Courier New';
    ctx.fillText(`SCORE: ${score}`, 20, 30);
    ctx.fillText(`COINS: ${coins} 🪙`, 200, 30);

    if (gameOver) {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.75)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#e52521';
        ctx.font = 'bold 30px Courier New';
        ctx.textAlign = 'center';
        ctx.fillText('GAME OVER', canvas.width / 2, canvas.height / 2 - 10);
        ctx.fillStyle = '#fff';
        ctx.font = '16px Courier New';
        ctx.fillText('רענן את הדף כדי לנסות שוב', canvas.width / 2, canvas.height / 2 + 25);
        ctx.textAlign = 'right';
    }

    if (gameWon) {
        ctx.fillStyle = 'rgba(0, 0, 0, 0.75)';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.fillStyle = '#fbd000';
        ctx.font = 'bold 30px Courier New';
        ctx.textAlign = 'center';
        ctx.fillText('STAGE CLEAR! 🎉', canvas.width / 2, canvas.height / 2 - 10);
        ctx.fillStyle = '#fff';
        ctx.font = '16px Courier New';
        ctx.fillText('כל הכבוד! סיימת את השלב בהצלחה', canvas.width / 2, canvas.height / 2 + 25);
        ctx.textAlign = 'right';
    }
}

function loop() {
    update();
    draw();
    requestAnimationFrame(loop);
}

loop();
</script>

</body>
</html>
