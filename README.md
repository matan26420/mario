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
    .chess-selected { outline: 3px solid #ec4899; background: #fbcfe8 !important; color: #0f172a !important; }
    .bg-table { background: radial-gradient(circle at center, #78350f, #451a03); border: 4px solid #92400e; border-radius: 18px; }
  </style>
</head>
<body class="text-white antialiased">
  <header class="glass sticky top-0 z-50 px-6 py-4 flex flex-wrap items-center justify-between gap-3 shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">TopLove IL</h1>
      <span class="text-xs bg-emerald-500/20 border border-emerald-400/40 text-emerald-200 px-2.5 py-0.5 rounded-full">
        חינם לגמרי • 18+
      </span>
    </div>
    <div class="flex items-center gap-3">
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header><main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">כניסה והרשמה חינם לגילאי 18 ומעלה בלבד</p>
      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <input type="number" id="auth-age" required min="18" max="99" placeholder="גיל (18+ בלבד)"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
        <div class="relative">
          <input type="password" id="auth-password" required minlength="6" placeholder="סיסמה (מינימום 6 תווים)" dir="ltr"
            class="w-full px-4 py-2.5 pl-11 rounded-xl bg-slate-900 border border-slate-700 text-left" />
          <button type="button" id="toggle-password-btn" class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400">👁️</button>
        </div>
        <p id="auth-error" class="text-rose-400 text-xs hidden"></p>
        <button type="submit" class="w-full py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
          כניסה / הרשמה
        </button>
      </form>
    </section><section id="app-section" class="hidden space-y-6">
      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">1. הפרופיל שלי</button>
        <button type="button" data-tab="users" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">2. משתמשים מחוברים 👥</button>
        <button type="button" data-tab="chat" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">3. חדרי שיחה 💬</button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">4. 10 משחקים ושולחנות 🎮</button>
      </div>

      <div id="tab-profile" class="tab-content max-w-2xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="flex flex-col sm:flex-row items-center gap-4 bg-slate-900/70 p-4 rounded-xl border border-slate-700">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt="תמונת פרופיל"
              class="w-20 h-20 rounded-full object-cover border-2 border-pink-500 bg-slate-800 shrink-0" />
            <div class="w-full space-y-2">
              <label class="block text-xs font-semibold text-pink-300">העלה תמונה מהמחשב או הכנס קישור</label>
              <input type="file" id="prof-avatar-file" accept="image/*"
                class="block w-full text-xs text-slate-300 file:ml-3 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:bg-pink-600 file:text-white" />
              <input type="url" id="prof-avatar-url" placeholder="קישור לתמונה (https://...)" dir="ltr"
                class="w-full px-3 py-1.5 text-sm rounded-lg bg-slate-950 border border-slate-700 text-left" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-name" required placeholder="שם / כינוי"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <select id="prof-gender" class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">
              <option value="זכר">מגדר: זכר</option>
              <option value="נקבה">מגדר: נקבה</option>
            </select>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="number" id="prof-age" min="18" max="99" required value="18" placeholder="גיל (18+)"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="text" id="prof-city" required placeholder="עיר"
              class="px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>

          <textarea id="prof-bio" rows="2" placeholder="קצת עליי..."
            class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700"></textarea>

          <p id="profile-error" class="text-rose-400 text-xs hidden"></p>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">שמור פרופיל</button>
          </div>
        </form>
      </div>

      <div id="tab-users" class="tab-content hidden max-w-4xl mx-auto glass rounded-2xl p-6 space-y-4">
        <h2 class="text-xl font-bold">👥 משתמשים אמיתיים במערכת</h2>
        <p class="text-xs text-slate-300">כאן מופיעים משתמשים שנרשמו למערכת. אפשר לפתוח שיחה אישית או להזמין למשחק.</p>
        <div id="real-users-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div><div id="tab-chat" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 space-y-3">
          <h3 class="text-sm font-bold text-pink-300">➕ פתיחת חדר שיחה חדש לפי נושא</h3>
          <form id="create-room-form" class="flex flex-col sm:flex-row gap-2.5">
            <input type="text" id="new-room-topic" required placeholder="נושא השיחה (למשל: מוזיקה, טיולים, סרטים)"
              class="flex-1 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              פתח חדר שיחה
            </button>
          </form>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <div class="space-y-2">
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרים לפי נושאי שיחה</h3>
            <div id="rooms-list" class="space-y-2 max-h-80 overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/70 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[340px] space-y-3">
            <div class="border-b border-white/10 pb-2">
              <h3 id="active-room-title" class="font-bold text-base">בחר חדר</h3>
              <p id="active-room-meta" class="text-xs text-slate-400">חדר שיחה פתוח</p>
            </div>

            <div id="chat-messages" class="space-y-2 max-h-56 overflow-y-auto py-1"></div>

            <form id="chat-form" class="flex gap-2 pt-2 border-t border-white/10">
              <input type="text" id="chat-input" required placeholder="כתוב הודעה בחדר..."
                class="flex-1 px-4 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
              <button type="submit" class="px-5 py-2 rounded-xl text-sm font-semibold bg-pink-600">שלח</button>
            </form>
          </div>
        </div>
      </div><div id="tab-games" class="tab-content hidden space-y-6">
        <div class="glass rounded-2xl p-4 space-y-3 border border-pink-500/30">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <div>
              <h3 class="text-base font-bold">🪑 שולחנות פעילים של משתמשים במשחק הנבחר</h3>
              <p class="text-xs text-slate-300">בחר שולחן של משתמש קיים כדי להיכנס אליו, או פתח שולחן משלך שמחכה למשתמש אחר</p>
            </div>
            <button type="button" id="create-my-table-btn" class="px-4 py-2 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
              + פתח שולחן שלי במשחק זה
            </button>
          </div>

          <div id="game-tables-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-2.5"></div>

          <div class="pt-2 border-t border-white/10 flex flex-wrap items-center justify-between gap-2 text-xs">
            <span id="selected-table-info" class="text-pink-200 font-semibold">לא נבחר שולחן עדיין</span>
            <span id="turn-lock-banner" class="text-amber-200 bg-amber-500/20 border border-amber-400/40 px-3 py-1 rounded-full">
              ממתין למשתמש אחר
            </span>
          </div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="ttt" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600">1. איקס עיגול</button>
          <button type="button" data-game="rps" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אבן נייר מספריים</button>
          <button type="button" data-game="tod" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. אמת או חובה</button>
          <button type="button" data-game="backgammon" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. שש בש</button>
          <button type="button" data-game="chess" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. שחמט</button>
          <button type="button" data-game="trivia" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">6. טריוויה</button>
          <button type="button" data-game="memory" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">7. זיכרון</button>
          <button type="button" data-game="number" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">8. ניחוש מספר</button>
          <button type="button" data-game="romance" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">9. פתיחה</button>
          <button type="button" data-game="tap" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">10. מהירות</button>
        </div><div id="game-ttt" class="game-panel max-w-sm mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">🚩 איקס עיגול</h3>
            <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">איפוס לוח</button>
          </div>
          <div id="ttt-board" class="grid grid-cols-3 gap-2 max-w-[240px] mx-auto"></div>
          <p id="ttt-status" class="text-sm text-pink-200">בחר שולחן של משתמש כדי לשחק</p>
        </div>

        <div id="game-rps" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">✂️ אבן נייר ומספריים</h3>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-4 rounded-xl">בחר שולחן של משתמש כדי לשחק</p>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">🔥 אמת או חובה</h3>
          <div class="flex justify-center gap-3">
            <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600">אמת 💭</button>
            <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600">חובה ⚡</button>
          </div>
          <p id="tod-text" class="text-base text-pink-200 bg-slate-900 p-4 rounded-xl">בחר שולחן של משתמש כדי לשחק</p>
        </div>

        <div id="game-backgammon" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
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
        </div><div id="game-chess" class="game-panel hidden max-w-lg mx-auto glass rounded-2xl p-6 text-center space-y-4">
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
        </div>

        <div id="game-number" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">⭐ ניחוש מספר (1–20)</h3>
          <div class="flex justify-center gap-2">
            <input type="number" id="num-input" min="1" max="20" class="w-24 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-center" />
            <button type="button" id="num-check" class="px-5 py-2 rounded-xl font-semibold bg-pink-600">בדוק</button>
          </div>
          <p id="num-hint" class="text-sm text-pink-200"></p>
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
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-analytics.js";
    import {
      getFirestore, collection, doc, setDoc, addDoc, updateDoc,
      onSnapshot, query, orderBy, serverTimestamp
    } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyDU1U8pC_xrEh6Kl0yyn4p20w5jzW7bWgI",
      authDomain: "toplove-il.firebaseapp.com",
      projectId: "toplove-il",
      storageBucket: "toplove-il.firebasestorage.app",
      messagingSenderId: "143390156671",
      appId: "1:143390156671:web:f7b74f1d5d815277f75c4a",
      measurementId: "G-VNTDRK1SVV"
    };

    const app = initializeApp(firebaseConfig);
    if (location.protocol !== "file:") getAnalytics(app);
    const db = getFirestore(app);

    const $ = (id) => document.getElementById(id);
    const me = { uid: "", email: "", name: "משתמש", gender: "זכר", age: 18, city: "ישראל", bio: "", avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" };
    const chatRooms = [
      { id: "r-music", topic: "מוזיקה והופעות" },
      { id: "r-travel", topic: "טיולים וסופ״ש" },
      { id: "r-games", topic: "משחקים וצחוק" }
    ];
    let activeRoomId = chatRooms[0].id;
    let unsubMsgs = null;
    let allUsers = [];

    function switchTab(tabName) {
      document.querySelectorAll(".tab-btn").forEach((b) => {
        b.className = b.dataset.tab === tabName
          ? "tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white"
          : "tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300";
      });
      document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
      $(`tab-${tabName}`).classList.remove("hidden");
    }

    function openApp(session) {
      Object.assign(me, session);
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      $("prof-name").value = me.name;
      $("prof-gender").value = me.gender;
      $("prof-age").value = me.age;
      $("prof-city").value = me.city;
      $("prof-bio").value = me.bio;
      $("prof-avatar-preview").src = me.avatar;
      switchTab("profile");
      renderRooms();
      subscribeUsers();
      subscribeGameTables();
    }

    $("toggle-password-btn").onclick = () => {
      $("auth-password").type = $("auth-password").type === "password" ? "text" : "password";
    };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim().toLowerCase();
      const age = Number($("auth-age").value);
      if (!age || age < 18) {
        $("auth-error").textContent = "כניסה והרשמה מותרים מגיל 18 ומעלה בלבד.";
        $("auth-error").classList.remove("hidden");
        return;
      }
      $("auth-error").classList.add("hidden");
      const uid = "u_" + email.replace(/[^a-z0-9]/g, "_");
      const session = { uid, email, name: email.split("@")[0] || "משתמש", gender: "זכר", age, city: "ישראל", bio: "", avatar: `https://api.dicebear.com/9.x/avataaars/svg?seed=${encodeURIComponent(uid)}` };
      localStorage.setItem("toplove_session", JSON.stringify(session));
      try { await setDoc(doc(db, "users", uid), { ...session, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp(session);
    };

    $("logout-btn").onclick = () => {
      localStorage.removeItem("toplove_session");
      location.reload();
    };

    document.querySelectorAll(".tab-btn").forEach((btn) => {
      btn.onclick = () => switchTab(btn.dataset.tab);
    });

    $("prof-avatar-file").onchange = (e) => {
      const f = e.target.files?.[0];
      if (!f) return;
      const rd = new FileReader();
      rd.onload = () => { me.avatar = String(rd.result); $("prof-avatar-preview").src = me.avatar; };
      rd.readAsDataURL(f);
    };
    $("prof-avatar-url").oninput = (e) => {
      if (e.target.value.trim()) { me.avatar = e.target.value.trim(); $("prof-avatar-preview").src = me.avatar; }
    };

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      const age = Number($("prof-age").value);
      if (!age || age < 18) {
        $("profile-error").textContent = "גיל חייב להיות 18 ומעלה.";
        $("profile-error").classList.remove("hidden");
        return;
      }
      $("profile-error").classList.add("hidden");
      me.name = $("prof-name").value.trim() || me.name;
      me.gender = $("prof-gender").value;
      me.age = age;
      me.city = $("prof-city").value.trim() || me.city;
      me.bio = $("prof-bio").value.trim();
      localStorage.setItem("toplove_session", JSON.stringify(me));
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      try { await setDoc(doc(db, "users", me.uid), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };

    function subscribeUsers() {
      onSnapshot(collection(db, "users"), (snap) => {
        allUsers = snap.docs.map((d) => ({ id: d.id, ...d.data() })).filter((u) => u.id !== me.uid);
        $("real-users-grid").innerHTML = allUsers.length
          ? allUsers.map((u) => `
              <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 flex flex-col justify-between gap-3">
                <div class="flex items-center gap-3">
                  <img src="${u.avatar || "https://api.dicebear.com/9.x/avataaars/svg?seed=" + u.id}" alt="" class="w-12 h-12 rounded-full object-cover border border-pink-500" />
                  <div>
                    <div class="font-bold text-sm">${u.name || "משתמש"}</div>
                    <div class="text-xs text-slate-300">${u.gender || ""} • גיל ${u.age || 18} • ${u.city || ""}</div>
                  </div>
                </div>
                <p class="text-xs text-slate-400">${u.bio || "אין תיאור עדיין"}</p>
                <div class="flex gap-2">
                  <button type="button" data-dm-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-pink-600">שיחה</button>
                  <button type="button" data-invite-user="${u.id}" class="flex-1 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600">שולחן משחק</button>
                </div>
              </div>
            `).join("")
          : `<p class="text-xs text-slate-400 col-span-full">עדיין אין משתמשים אחרים רשומים במערכת.</p>`;

        document.querySelectorAll("[data-dm-user]").forEach((btn) => {
          btn.onclick = () => {
            const other = allUsers.find((x) => x.id === btn.dataset.dmUser);
            if (!other) return;
            const dmId = "dm_" + [me.uid, other.id].sort().join("_");
            if (!chatRooms.some((r) => r.id === dmId)) chatRooms.unshift({ id: dmId, topic: `שיחה עם ${other.name}` });
            activeRoomId = dmId;
            switchTab("chat");
            renderRooms();
          };
        });

        document.querySelectorAll("[data-invite-user]").forEach(() => {
          // מעבר ללשונית המשחקים לבחירת או פתיחת שולחן מול משתמש אחר
        });
        document.querySelectorAll("[data-invite-user]").forEach((btn) => {
          btn.onclick = () => switchTab("games");
        });
      });
    }function listenMsgs(roomId) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      const q = query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc"));
      unsubMsgs = onSnapshot(q, (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length
          ? msgs.map((m) => `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from || "משתמש"}:</strong> ${m.text || ""}</div>`).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = chatRooms.map((r) => `
        <button type="button" data-room="${r.id}" class="w-full text-right p-3 rounded-xl border text-xs ${r.id === activeRoomId ? "bg-pink-600/30 border-pink-400" : "bg-slate-950/70 border-slate-800"}">
          💬 ${r.topic}
        </button>
      `).join("");
      document.querySelectorAll("[data-room]").forEach((b) => {
        b.onclick = () => { activeRoomId = b.dataset.room; renderRooms(); };
      });
      const cur = chatRooms.find((r) => r.id === activeRoomId) || chatRooms[0];
      $("active-room-title").textContent = cur.topic;
      listenMsgs(cur.id);
    }

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim();
      if (!topic) return;
      const room = { id: `r-${Date.now()}`, topic };
      chatRooms.unshift(room);
      activeRoomId = room.id;
      $("new-room-topic").value = "";
      try { await setDoc(doc(db, "rooms", room.id), { ...room, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      const txt = $("chat-input").value.trim();
      if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", activeRoomId, "messages"), { from: me.name, text: txt, createdAt: serverTimestamp() });
    };

    let currentGameType = "ttt";
    let allTables = [];
    let selectedTable = null;
    let unsubTableDoc = null;
    let isSubmittingMove = false;

    function canPlayInSelectedTable() {
      if (!selectedTable || isSubmittingMove) return false;
      if (!selectedTable.hostUid || !selectedTable.guestUid) return false;
      if (selectedTable.hostUid === selectedTable.guestUid) return false;
      return selectedTable.turnUid === me.uid;
    }

    function applyTurnLockToBoard() {
      const allowed = canPlayInSelectedTable();
      document.querySelectorAll("#ttt-board button, .rps-choice, #btn-truth, #btn-dare").forEach((el) => {
        el.disabled = !allowed;
        el.classList.toggle("opacity-50", !allowed);
      });
      if (!selectedTable) {
        $("turn-lock-banner").textContent = "בחר שולחן של משתמש כדי להתחיל";
      } else if (!selectedTable.guestUid) {
        $("turn-lock-banner").textContent = "ממתין למשתמש אמיתי נוסף שיצטרף לשולחן...";
      } else if (allowed) {
        $("turn-lock-banner").textContent = "תורך לשחק! לחץ והמתן למשתמש השני";
      } else {
        $("turn-lock-banner").textContent = "ממתין למשתמש השני שילחץ...";
      }
    }

    function renderTablesList() {
      const filtered = allTables.filter((t) => t.gameType === currentGameType);
      $("game-tables-list").innerHTML = filtered.length
        ? filtered.map((t) => {
            const isSel = selectedTable && selectedTable.id === t.id;
            const statusText = t.guestUid ? `${t.hostName} מול ${t.guestName}` : `ממתין למשתמש נוסף (שולחן של ${t.hostName})`;
            return `<button type="button" data-join-table="${t.id}" class="text-right p-3 rounded-xl border text-xs transition ${isSel ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/80 border-slate-700 hover:border-pink-400/60"}">
              <div class="font-bold text-sm">🪑 שולחן של ${t.hostName || "משתמש"}</div>
              <div class="text-slate-300 mt-0.5">${statusText}</div>
            </button>`;
          }).join("")
        : `<p class="text-xs text-slate-400 col-span-full">אין שולחנות פתוחים למשחק זה עדיין. פתח שולחן משלך או הצטרף למשתמש אחר.</p>`;

      document.querySelectorAll("[data-join-table]").forEach((btn) => {
        btn.onclick = () => joinTableById(btn.dataset.joinTable);
      });
    }

    function subscribeGameTables() {
      onSnapshot(collection(db, "gameTables"), (snap) => {
        allTables = snap.docs.map((d) => ({ id: d.id, ...d.data() }));
        renderTablesList();
      });
    }

    async function joinTableById(tableId) {
      const t = allTables.find((x) => x.id === tableId);
      if (!t) return;
      if (t.hostUid !== me.uid && !t.guestUid) {
        await updateDoc(doc(db, "gameTables", t.id), { guestUid: me.uid, guestName: me.name });
      }
      if (unsubTableDoc) { unsubTableDoc(); unsubTableDoc = null; }
      unsubTableDoc = onSnapshot(doc(db, "gameTables", t.id), (snap) => {
        if (!snap.exists()) return;
        selectedTable = { id: snap.id, ...snap.data() };
        isSubmittingMove = false;
        $("selected-table-info").textContent = `שולחן: ${selectedTable.hostName} ${selectedTable.guestName ? "מול " + selectedTable.guestName : "(ממתין לשחקן שני)"}`;
        renderTttBoard(selectedTable.board || Array(9).fill(""));
        applyTurnLockToBoard();
      });
    }

    $("create-my-table-btn").onclick = async () => {
      const id = `tbl_${currentGameType}_${Date.now()}`;
      const newTbl = {
        gameType: currentGameType,
        hostUid: me.uid,
        hostName: me.name,
        guestUid: null,
        guestName: null,
        turnUid: me.uid,
        board: Array(9).fill(""),
        createdAt: serverTimestamp()
      };
      await setDoc(doc(db, "gameTables", id), newTbl);
      await joinTableById(id);
    };document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        currentGameType = btn.dataset.game;
        document.querySelectorAll(".game-tab-btn").forEach((b) => { b.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        btn.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600";
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${currentGameType}`).classList.remove("hidden");
        renderTablesList();
      };
    });

    function renderTttBoard(board) {
      $("ttt-board").innerHTML = "";
      board.forEach((v, idx) => {
        const b = document.createElement("button");
        b.type = "button";
        b.className = "h-16 rounded-xl bg-slate-800 border border-slate-700 text-2xl font-bold";
        b.textContent = v === "X" ? "❌" : v === "O" ? "⭕" : "";
        b.onclick = async () => {
          if (!canPlayInSelectedTable() || v) return;
          isSubmittingMove = true;
          applyTurnLockToBoard();
          const mark = selectedTable.hostUid === me.uid ? "X" : "O";
          const nextBoard = [...board];
          nextBoard[idx] = mark;
          const nextTurnUid = selectedTable.turnUid === selectedTable.hostUid ? selectedTable.guestUid : selectedTable.hostUid;
          await updateDoc(doc(db, "gameTables", selectedTable.id), { board: nextBoard, turnUid: nextTurnUid });
        };
        $("ttt-board").appendChild(b);
      });
      applyTurnLockToBoard();
    }
    renderTttBoard(Array(9).fill(""));

    $("ttt-reset").onclick = async () => {
      if (!selectedTable) return;
      await updateDoc(doc(db, "gameTables", selectedTable.id), { board: Array(9).fill(""), turnUid: selectedTable.hostUid });
    };

    document.querySelectorAll(".rps-choice").forEach((b) => {
      b.onclick = async () => {
        if (!canPlayInSelectedTable()) return;
        isSubmittingMove = true;
        applyTurnLockToBoard();
        const nextTurnUid = selectedTable.turnUid === selectedTable.hostUid ? selectedTable.guestUid : selectedTable.hostUid;
        await updateDoc(doc(db, "gameTables", selectedTable.id), { lastRpsMove: b.dataset.rps, lastRpsBy: me.name, turnUid: nextTurnUid });
        $("rps-result").textContent = `${me.name} בחר ${b.dataset.rps} — ממתין למשתמש השני`;
      };
    });

    function handleTod(kind) {
      return async () => {
        if (!canPlayInSelectedTable()) return;
        isSubmittingMove = true;
        applyTurnLockToBoard();
        const nextTurnUid = selectedTable.turnUid === selectedTable.hostUid ? selectedTable.guestUid : selectedTable.hostUid;
        await updateDoc(doc(db, "gameTables", selectedTable.id), { lastTod: `${kind}: ${me.name}`, turnUid: nextTurnUid });
        $("tod-text").textContent = `${kind === "truth" ? "💭 אמת" : "⚡ חובה"} נשלח ע"י ${me.name} — ממתין למשתמש השני`;
      };
    }
    $("btn-truth").onclick = handleTod("truth");
    $("btn-dare").onclick = handleTod("dare");

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
    $("bg-reset").onclick = initBg; initBg();

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
              whiteTurn = !whiteTurn; $("chess-turn").textContent = `תור: ${whiteTurn ? "לבן" : "שחור"}`;
            }
            cs = null; renderChess();
          } else if (cb[r][c]) { cs = { r, c }; renderChess(); }
        };
        $("chess-board").appendChild(cell);
      }
    }
    $("chess-reset").onclick = () => { cb = startChess.map((r) => [...r]); cs = null; whiteTurn = true; renderChess(); };
    renderChess();

    const trList = [{ q: "מה שובר קרח טוב?", opts: ["שיחה מעניינת", "מבחן", "ריב", "שתיקה"], ok: 0 }];
    $("trivia-q").textContent = trList[0].q;
    trList[0].opts.forEach((o, i) => {
      const b = document.createElement("button"); b.type = "button"; b.className = "px-4 py-2 rounded-xl bg-slate-800 text-sm"; b.textContent = o;
      b.onclick = () => { $("trivia-feedback").textContent = i === trList[0].ok ? "תשובה מצוינת!" : "נסה שוב"; };
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

    $("rom-submit").onclick = () => { const v = $("rom-input").value.trim(); if (v) { $("rom-feedback").textContent = `נשמר: "${v}"`; $("rom-input").value = ""; } };

    let taps = 0;
    $("tap-btn").onclick = () => { taps++; $("tap-counter").textContent = `לחיצות: ${taps}${taps >= 20 ? " — יעד הושג! 🎉" : ""}`; };

    const savedSession = localStorage.getItem("toplove_session");
    if (savedSession) {
      try {
        const parsed = JSON.parse(savedSession);
        if (parsed && Number(parsed.age) >= 18) openApp(parsed);
      } catch {}
    }
  </script>
</body>
</html>
