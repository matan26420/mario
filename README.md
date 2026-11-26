<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove IL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background: linear-gradient(135deg, #0f172a, #1e1b4b, #311042);
      min-height: 100vh;
      font-family: system-ui, -apple-system, sans-serif;
    }
    .glass {
      background: rgba(30, 41, 59, 0.78);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.12);
    }
    .chess-board {
      display: grid;
      grid-template-columns: repeat(8, minmax(0, 1fr));
      border: 2px solid #f472b6;
      border-radius: 12px;
      overflow: hidden;
    }
    .chess-cell {
      aspect-ratio: 1 / 1;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: clamp(1.1rem, 3vw, 1.8rem);
      cursor: pointer;
    }
    .chess-light { background: #e2e8f0; color: #0f172a; }
    .chess-dark { background: #475569; color: #ffffff; }
    .chess-selected {
      outline: 3px solid #ec4899;
      background: #fbcfe8 !important;
      color: #0f172a !important;
    }
    .bg-table {
      background: radial-gradient(circle at center, #78350f, #451a03);
      border: 4px solid #92400e;
      border-radius: 18px;
    }
  </style>
</head>
<body class="text-white antialiased">
  <header class="glass sticky top-0 z-50 px-6 py-4 flex items-center justify-between gap-3 shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">
        TopLove IL
      </h1>
    </div>
    <div class="flex items-center gap-3">
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">
        התנתק
      </button>
    </div>
  </header><main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">
        התחבר או הירשם כדי לנהל את הפרופיל שלך, להיכנס לצ'אט ולשחק מול שחקן אחר
      </p>
      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <div class="relative">
          <input type="password" id="auth-password" required minlength="6" placeholder="סיסמה (מינימום 6 תווים)" dir="ltr"
            class="w-full px-4 py-2.5 pl-11 rounded-xl bg-slate-900 border border-slate-700 text-left" />
          <button type="button" id="toggle-password-btn" aria-label="הצג או הסתר סיסמה"
            class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400">👁️</button>
        </div>
        <button type="submit" class="w-full py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
          כניסה / הרשמה
        </button>
      </form>
      <button type="button" id="quick-demo-btn" class="mt-3 w-full py-2.5 rounded-xl font-semibold bg-emerald-600 text-sm">
        ⚡ כניסה מהירה
      </button>
    </section><section id="app-section" class="hidden space-y-6">
      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">
          1. הפרופיל שלי
        </button>
        <button type="button" data-tab="chat" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">
          2. צ'אט וחדרים 💬
        </button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">
          3. 10 משחקים 🎮
        </button>
      </div>

      <div id="tab-profile" class="tab-content max-w-2xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="flex items-center gap-4 bg-slate-900/70 p-4 rounded-xl border border-slate-700">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=User" alt="תמונת פרופיל"
              class="w-16 h-16 rounded-full object-cover border-2 border-pink-500 bg-slate-800" />
            <input type="url" id="prof-avatar-url" placeholder="קישור לתמונת פרופיל (https://...)" dir="ltr"
              class="w-full px-3 py-2 text-sm rounded-lg bg-slate-950 border border-slate-700 text-left" />
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <input type="text" id="prof-name" required placeholder="שם"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="number" id="prof-age" min="18" max="99" required placeholder="גיל"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="text" id="prof-city" required placeholder="עיר"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>
          <textarea id="prof-bio" rows="2" placeholder="קצת עליי..."
            class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700"></textarea>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              שמור פרופיל
            </button>
          </div>
        </form>
      </div><div id="tab-chat" class="tab-content hidden max-w-3xl mx-auto glass rounded-2xl p-6 space-y-4">
        <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-3">
          <div>
            <h2 class="text-xl font-bold">💬 צ'אט חדרים</h2>
            <p id="chat-room-label" class="text-xs text-pink-300">חדר פעיל: כללי</p>
          </div>
          <div class="flex gap-2">
            <button type="button" data-room="כללי" class="room-btn px-3 py-1 rounded-lg text-xs font-semibold bg-pink-600">
              חדר כללי
            </button>
            <button type="button" data-room="VIP" class="room-btn px-3 py-1 rounded-lg text-xs font-semibold bg-amber-600/30 border border-amber-400/50 text-amber-200">
              חדר VIP 👑
            </button>
          </div>
        </div>
        <div id="chat-messages" class="space-y-2 max-h-72 overflow-y-auto bg-slate-900/70 p-4 rounded-xl border border-slate-800">
          <p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה. כתוב הודעה ראשונה!</p>
        </div>
        <form id="chat-form" class="flex gap-2">
          <input type="text" id="chat-input" required placeholder="כתוב הודעה..."
            class="flex-1 px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
          <button type="submit" class="px-5 py-2.5 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
            שלח
          </button>
        </form>
      </div><div id="tab-games" class="tab-content hidden space-y-6">
        <div class="glass rounded-2xl p-4 flex flex-wrap items-center justify-between gap-3 border border-pink-500/30">
          <div class="flex items-center gap-2 text-xs sm:text-sm">
            <label for="active-player-select" class="text-slate-300">פרופיל פעיל כעת:</label>
            <select id="active-player-select" class="px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-700 font-semibold">
              <option value="player1">שחקן 1 (אני)</option>
              <option value="player2">שחקן 2 (פרופיל אחר)</option>
            </select>
          </div>
          <span id="sync-turn-banner" class="text-xs sm:text-sm font-semibold text-amber-200 bg-amber-500/20 border border-amber-400/40 px-3.5 py-1.5 rounded-full">
            ממתין ללחיצת שחקן 1...
          </span>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="rps" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. אבן נייר מספריים</button>
          <button type="button" data-game="tod" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אמת או חובה</button>
          <button type="button" data-game="backgammon" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. שש בש</button>
          <button type="button" data-game="chess" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. שחמט</button>
          <button type="button" data-game="trivia" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. טריוויה</button>
          <button type="button" data-game="memory" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">6. זיכרון</button>
          <button type="button" data-game="number" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">7. ניחוש מספר</button>
          <button type="button" data-game="ttt" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">8. איקס עיגול</button>
          <button type="button" data-game="romance" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">9. פתיחה</button>
          <button type="button" data-game="tap" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">10. מהירות</button>
        </div>

        <div id="game-rps" class="game-panel max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">✂️ אבן נייר ומספריים (המתנה לשחקן השני)</h3>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-4 rounded-xl">
            שחקן 1 בוחר ראשון, ואז מחכים לשחקן 2 שילחץ על הבחירה שלו
          </p>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">🔥 אמת או חובה</h3>
          <div class="flex justify-center gap-3">
            <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600">אמת 💭</button>
            <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600">חובה ⚡</button>
          </div>
          <p id="tod-text" class="text-base text-pink-200 bg-slate-900 p-4 rounded-xl">לחץ על אמת או חובה</p>
        </div><div id="game-backgammon" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">🎲 שש בש (24 נקודות)</h3>
            <div class="flex gap-2">
              <button type="button" id="bg-roll" class="px-4 py-1.5 rounded-xl text-sm font-semibold bg-pink-600">זרוק קוביות</button>
              <button type="button" id="bg-reset" class="px-3 py-1.5 rounded-xl text-xs bg-slate-800 border border-slate-600">איפוס</button>
            </div>
          </div>
          <p id="bg-status" class="text-sm text-pink-200">קוביות: <strong id="bg-dice">-</strong> | בחר נקודה ואז יעד</p>
          <div class="bg-table p-3 space-y-2">
            <div id="bg-top-row" class="grid grid-cols-6 sm:grid-cols-12 gap-1"></div>
            <div class="h-2 rounded-full bg-amber-900"></div>
            <div id="bg-bottom-row" class="grid grid-cols-6 sm:grid-cols-12 gap-1"></div>
          </div>
        </div>

        <div id="game-chess" class="game-panel hidden max-w-lg mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">♟️ שחמט</h3>
            <button type="button" id="chess-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">אפס לוח</button>
          </div>
          <p id="chess-turn" class="text-sm text-pink-200">תור: לבן</p>
          <div id="chess-board" class="chess-board"></div>
        </div>

        <div id="game-trivia" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">💛 טריוויה</h3>
          <p id="trivia-q" class="text-base text-pink-200"></p>
          <div id="trivia-options" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5"></div>
          <p id="trivia-feedback" class="text-sm text-emerald-300"></p>
        </div>

        <div id="game-memory" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">💎 זיכרון</h3>
            <button type="button" id="memory-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">ערבב</button>
          </div>
          <div id="memory-grid" class="grid grid-cols-4 gap-2"></div>
          <p id="memory-status" class="text-sm text-pink-200"></p>
        </div><div id="game-number" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">⭐ ניחוש מספר (1–20)</h3>
          <div class="flex justify-center gap-2">
            <input type="number" id="num-input" min="1" max="20" class="w-24 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-center" />
            <button type="button" id="num-check" class="px-5 py-2 rounded-xl font-semibold bg-pink-600">בדוק</button>
          </div>
          <p id="num-hint" class="text-sm text-pink-200"></p>
        </div>

        <div id="game-ttt" class="game-panel hidden max-w-sm mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">🚩 איקס עיגול</h3>
            <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">חדש</button>
          </div>
          <div id="ttt-board" class="grid grid-cols-3 gap-2 max-w-[240px] mx-auto"></div>
          <p id="ttt-status" class="text-sm text-pink-200">תור: ❌</p>
        </div>

        <div id="game-romance" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">🌹 משפט פתיחה</h3>
          <input type="text" id="rom-input" placeholder="כתוב משפט פתיחה..." class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          <button type="button" id="rom-submit" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600">שלח</button>
          <p id="rom-feedback" class="text-sm text-emerald-300"></p>
        </div>

        <div id="game-tap" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">⚡ קרב מהירות (יעד 20)</h3>
          <button type="button" id="tap-btn" class="w-full py-5 rounded-2xl text-xl font-bold bg-gradient-to-l from-pink-600 to-indigo-600">
            לחץ! ⚡
          </button>
          <p id="tap-counter" class="text-base text-pink-200">לחיצות: 0</p>
        </div>
      </div>
    </section>
  </main><script>
    const $ = (id) => document.getElementById(id);
    const me = { name: "משתמש", age: 25, city: "ישראל", avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=User" };
    const chatRooms = { "כללי": [], "VIP": [] };
    let currentRoom = "כללי";

    function openMain() {
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name}, ${me.age} • ${me.city}`;
    }

    $("toggle-password-btn").onclick = () => {
      $("auth-password").type = $("auth-password").type === "password" ? "text" : "password";
    };
    $("auth-form").onsubmit = (e) => { e.preventDefault(); openMain(); };
    $("quick-demo-btn").onclick = openMain;
    $("logout-btn").onclick = () => location.reload();

    document.querySelectorAll(".tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".tab-btn").forEach((b) => { b.className = "tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300"; });
        btn.className = "tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white";
        document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
        $(`tab-${btn.dataset.tab}`).classList.remove("hidden");
      };
    });

    $("prof-avatar-url").oninput = (e) => {
      if (e.target.value.trim()) {
        me.avatar = e.target.value.trim();
        $("prof-avatar-preview").src = me.avatar;
      }
    };
    $("profile-form").onsubmit = (e) => {
      e.preventDefault();
      me.name = $("prof-name").value.trim() || me.name;
      me.age = Number($("prof-age").value) || me.age;
      me.city = $("prof-city").value.trim() || me.city;
      $("user-badge").textContent = `${me.name}, ${me.age} • ${me.city}`;
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };

    function renderChat() {
      $("chat-room-label").textContent = `חדר פעיל: ${currentRoom}`;
      const list = chatRooms[currentRoom];
      $("chat-messages").innerHTML = list.length
        ? list.map((m) => `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from}:</strong> ${m.text}</div>`).join("")
        : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר ${currentRoom}.</p>`;
    }
    document.querySelectorAll(".room-btn").forEach((b) => {
      b.onclick = () => { currentRoom = b.dataset.room; renderChat(); };
    });
    $("chat-form").onsubmit = (e) => {
      e.preventDefault();
      const t = $("chat-input").value.trim();
      if (!t) return;
      chatRooms[currentRoom].push({ from: me.name, text: t });
      $("chat-input").value = "";
      renderChat();
    };

    // סנכרון תור: מחכים לפרופיל השני (player2) אחרי ש-player1 לחץ, ולא משחקים מול עצמנו
    const matchSync = {
      activeProfile: "player1",
      waitingFor: "player1",
      rpsMoves: { player1: null, player2: null }
    };

    function refreshTurnBanner() {
      const targetName = matchSync.waitingFor === "player1" ? "שחקן 1" : "שחקן 2";
      $("sync-turn-banner").textContent = `ממתין ללחיצת ${targetName}...`;
    }

    $("active-player-select").onchange = (e) => {
      matchSync.activeProfile = e.target.value;
      refreshTurnBanner();
    };
    refreshTurnBanner();document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".game-tab-btn").forEach((b) => { b.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        btn.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600";
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${btn.dataset.game}`).classList.remove("hidden");
      };
    });

    const rpsNames = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
    document.querySelectorAll(".rps-choice").forEach((b) => {
      b.onclick = () => {
        const p = matchSync.activeProfile;
        if (matchSync.waitingFor !== p) {
          $("rps-result").textContent = `עכשיו תור ${matchSync.waitingFor === "player1" ? "שחקן 1" : "שחקן 2"} ללחוץ!`;
          return;
        }
        matchSync.rpsMoves[p] = b.dataset.rps;
        if (!matchSync.rpsMoves.player1 || !matchSync.rpsMoves.player2) {
          matchSync.waitingFor = p === "player1" ? "player2" : "player1";
          refreshTurnBanner();
          $("rps-result").textContent = `${p === "player1" ? "שחקן 1" : "שחקן 2"} בחר! ממתין לשחקן השני שילחץ...`;
          return;
        }
        const m1 = matchSync.rpsMoves.player1;
        const m2 = matchSync.rpsMoves.player2;
        $("rps-result").textContent = `שחקן 1: ${rpsNames[m1]} | שחקן 2: ${rpsNames[m2]}`;
        matchSync.rpsMoves = { player1: null, player2: null };
        matchSync.waitingFor = "player1";
        refreshTurnBanner();
      };
    });

    $("btn-truth").onclick = () => { $("tod-text").textContent = "💭 אמת: מה הרגע הכי מצחיק שקרה לך לאחרונה?"; };
    $("btn-dare").onclick = () => { $("tod-text").textContent = "⚡ חובה: שלח הודעה טובה בצ'אט לחדר!"; };

    let bgBoard = Array(24).fill(null).map(() => ({ c: null, n: 0 })), bgSel = null;
    function initBg() {
      bgBoard = Array(24).fill(null).map(() => ({ c: null, n: 0 }));
      bgBoard[0] = { c: "pink", n: 2 }; bgBoard[11] = { c: "pink", n: 5 };
      bgBoard[23] = { c: "indigo", n: 2 }; bgBoard[12] = { c: "indigo", n: 5 };
      bgSel = null; renderBg();
    }
    function renderBg() {
      $("bg-top-row").innerHTML = ""; $("bg-bottom-row").innerHTML = "";
      for (let i = 12; i < 24; i++) $("bg-top-row").appendChild(makeBgCell(i));
      for (let i = 11; i >= 0; i--) $("bg-bottom-row").appendChild(makeBgCell(i));
    }
    function makeBgCell(i) {
      const pt = bgBoard[i], btn = document.createElement("button");
      btn.type = "button";
      btn.className = `min-h-[90px] rounded-lg p-1 flex flex-col items-center justify-between border text-[10px] ${bgSel === i ? "border-pink-400 bg-amber-800" : "border-amber-700/60 bg-amber-950/85"}`;
      btn.innerHTML = `<span>${i + 1}</span><span>${pt.n ? `${pt.c === "pink" ? "🔴" : "🔵"}x${pt.n}` : ""}</span>`;
      btn.onclick = () => {
        if (bgSel === null) { if (pt.n > 0) { bgSel = i; renderBg(); } }
        else {
          if (bgSel !== i && bgBoard[bgSel].n > 0) {
            const m = bgBoard[bgSel].c; bgBoard[bgSel].n--; if (!bgBoard[bgSel].n) bgBoard[bgSel].c = null;
            pt.c = m; pt.n++;
          }
          bgSel = null; renderBg();
        }
      };
      return btn;
    }
    $("bg-roll").onclick = () => { $("bg-dice").textContent = `${Math.floor(Math.random()*6)+1} ו-${Math.floor(Math.random()*6)+1}`; };
    $("bg-reset").onclick = initBg;
    initBg();

    const startChess = [["♜","♞","♝","♛","♚","♝","♞","♜"],["♟","♟","♟","♟","♟","♟","♟","♟"],["","","","","","","",""],["","","","","","","",""],["","","","","","","",""],["","","","","","","",""],["♙","♙","♙","♙","♙","♙","♙","♙"],["♖","♘","♗","♕","♔","♗","♘","♖"]];
    let cb = startChess.map((r) => [...r]), cs = null, whiteTurn = true;
    function renderChess() {
      $("chess-board").innerHTML = "";
      for (let r = 0; r < 8; r++) for (let c = 0; c < 8; c++) {
        const cell = document.createElement("button");
        cell.type = "button";
        cell.className = `chess-cell ${(r + c) % 2 === 0 ? "chess-light" : "chess-dark"} ${cs && cs.r === r && cs.c === c ? "chess-selected" : ""}`;
        cell.textContent = cb[r][c];
        cell.onclick = () => {
          if (cs) {
            if (cs.r !== r || cs.c !== c) {
              cb[r][c] = cb[cs.r][cs.c]; cb[cs.r][cs.c] = "";
              whiteTurn = !whiteTurn;
              $("chess-turn").textContent = `תור: ${whiteTurn ? "לבן" : "שחור"}`;
            }
            cs = null; renderChess();
          } else if (cb[r][c]) { cs = { r, c }; renderChess(); }
        };
        $("chess-board").appendChild(cell);
      }
    }
    $("chess-reset").onclick = () => { cb = startChess.map((r) => [...r]); cs = null; whiteTurn = true; $("chess-turn").textContent = "תור: לבן"; renderChess(); };
    renderChess();

    const trList = [{ q: "מה שובר קרח טוב?", opts: ["משחק קליל", "מבחן", "ריב", "שתיקה"], ok: 0 }];
    $("trivia-q").textContent = trList[0].q;
    trList[0].opts.forEach((o, i) => {
      const b = document.createElement("button"); b.type = "button"; b.className = "px-4 py-2 rounded-xl bg-slate-800 text-sm"; b.textContent = o;
      b.onclick = () => { $("trivia-feedback").textContent = i === trList[0].ok ? "תשובה מעולה!" : "נסה שוב"; };
      $("trivia-options").appendChild(b);
    });

    const mSyms = ["💜", "🎲", "🌹", "⚡"];
    let mDeck = [], mPick = [], mDone = new Set();
    function initMem() { mDeck = [...mSyms, ...mSyms].sort(() => Math.random() - 0.5); mPick = []; mDone = new Set(); renderMem(); }
    function renderMem() {
      $("memory-grid").innerHTML = "";
      mDeck.forEach((s, i) => {
        const b = document.createElement("button"); b.type = "button"; const show = mPick.includes(i) || mDone.has(i);
        b.className = "h-12 rounded-xl bg-slate-800 border border-slate-700 text-lg"; b.textContent = show ? s : "❓";
        b.onclick = () => {
          if (show || mPick.length === 2) return; mPick.push(i); renderMem();
          if (mPick.length === 2) {
            if (mDeck[mPick[0]] === mDeck[mPick[1]]) { mDone.add(mPick[0]); mDone.add(mPick[1]); mPick = []; renderMem(); }
            else setTimeout(() => { mPick = []; renderMem(); }, 500);
          }
        };
        $("memory-grid").appendChild(b);
      });
    }
    $("memory-reset").onclick = initMem; initMem();

    let secret = Math.floor(Math.random() * 20) + 1;
    $("num-check").onclick = () => {
      const g = Number($("num-input").value); if (!g) return;
      if (g === secret) { $("num-hint").textContent = "פגעת! מספר חדש נבחר"; secret = Math.floor(Math.random() * 20) + 1; }
      else $("num-hint").textContent = g < secret ? "גבוה יותר ⬆️" : "נמוך יותר ⬇️";
    };

    let ttt = Array(9).fill(""), xTurn = true;
    function renderTtt() {
      $("ttt-board").innerHTML = "";
      ttt.forEach((v, i) => {
        const b = document.createElement("button"); b.type = "button"; b.className = "h-14 rounded-xl bg-slate-800 border border-slate-700 text-xl font-bold"; b.textContent = v;
        b.onclick = () => {
          if (!v) {
            ttt[i] = xTurn ? "❌" : "⭕";
            xTurn = !xTurn;
            $("ttt-status").textContent = `תור: ${xTurn ? "❌" : "⭕"}`;
            renderTtt();
          }
        };
        $("ttt-board").appendChild(b);
      });
    }
    $("ttt-reset").onclick = () => { ttt = Array(9).fill(""); xTurn = true; $("ttt-status").textContent = "תור: ❌"; renderTtt(); }; renderTtt();

    $("rom-submit").onclick = () => {
      const v = $("rom-input").value.trim();
      if (v) { $("rom-feedback").textContent = `נשמר: "${v}"`; $("rom-input").value = ""; }
    };

    let taps = 0;
    $("tap-btn").onclick = () => {
      taps++;
      $("tap-counter").textContent = `לחיצות: ${taps}${taps >= 20 ? " — יעד הושג! 🎉" : ""}`;
    };
  </script>
</body>
</html>};
  </script>
</body>
</html>
