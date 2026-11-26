
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
        האתר חינם • VIP 5 ש"ח/יום
      </span>
    </div>
    <div class="flex items-center gap-3">
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header><main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">הכניסה וההרשמה חינם לגילאי 18 ומעלה בלבד</p>
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
          כניסה / הרשמה (חינם)
        </button>
      </form>
    </section><section id="app-section" class="hidden space-y-6">
      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">1. הפרופיל שלי</button>
        <button type="button" data-tab="chat" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">2. חדרי שיחה ו-VIP 💬</button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">3. 10 משחקים 🎮</button>
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
      </div><div id="tab-chat" class="tab-content hidden max-w-5xl mx-auto glass rounded-2xl p-6 space-y-5">
        <div class="bg-slate-900/80 border border-slate-700 rounded-xl p-4 space-y-3">
          <h3 class="text-sm font-bold text-pink-300">➕ פתיחת חדר שיחה חדש לפי נושא</h3>
          <form id="create-room-form" class="grid grid-cols-1 sm:grid-cols-3 gap-2.5">
            <input type="text" id="new-room-topic" required placeholder="נושא השיחה (למשל: מוזיקה, טיולים, סרטים)"
              class="sm:col-span-2 px-3.5 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm" />
            <select id="new-room-type" class="px-3 py-2 rounded-xl bg-slate-950 border border-slate-700 text-sm">
              <option value="free">חדר נושא רגיל (חינם)</option>
              <option value="vip">חדר VIP (5 ש"ח ליום)</option>
            </select>
            <button type="submit" class="sm:col-span-3 py-2 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              פתח חדר שיחה
            </button>
          </form>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-5">
          <div class="space-y-3">
            <h3 class="text-sm font-bold text-slate-200">🗂️ חדרים קיימים (לפי נושאי שיחה)</h3>
            <div id="rooms-list" class="space-y-2 max-h-80 overflow-y-auto"></div>
          </div>

          <div class="lg:col-span-2 bg-slate-900/70 border border-slate-800 rounded-2xl p-4 flex flex-col justify-between min-h-[340px] space-y-3">
            <div class="flex flex-wrap items-center justify-between gap-2 border-b border-white/10 pb-2">
              <div>
                <h3 id="active-room-title" class="font-bold text-base">בחר חדר</h3>
                <p id="active-room-meta" class="text-xs text-slate-400"></p>
              </div>
              <button type="button" id="unlock-vip-btn" class="hidden px-3 py-1.5 rounded-lg text-xs font-bold bg-amber-500 text-slate-950">
                שלם 5 ש"ח ליום עבור VIP
              </button>
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
        <div class="glass rounded-2xl p-4 flex flex-wrap items-center justify-between gap-3 border border-pink-500/30">
          <div class="flex items-center gap-2 text-xs sm:text-sm">
            <label for="game-profile-select" class="text-slate-300">פרופיל פעיל:</label>
            <select id="game-profile-select" class="px-3 py-1.5 rounded-lg bg-slate-900 border border-slate-700 font-semibold">
              <option value="p1">פרופיל א' (שחקן 1)</option>
              <option value="p2">פרופיל ב' (שחקן 2)</option>
            </select>
          </div>
          <span id="multiplayer-status" class="text-xs sm:text-sm font-semibold text-amber-200 bg-amber-500/20 border border-amber-400/40 px-3.5 py-1.5 rounded-full">
            ברירת מחדל: ממתין לפרופיל א' — אסור לשחק לבד
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
          <h3 class="text-xl font-bold">✂️ אבן נייר ומספריים (2 שחקנים)</h3>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 text-lg">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-sm text-pink-200 bg-slate-900 p-4 rounded-xl">
            פרופיל א' לוחץ ראשון, ואז מחכים לפרופיל ב' שילחץ
          </p>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <h3 class="text-xl font-bold">🔥 אמת או חובה (תור בין 2 שחקנים)</h3>
          <div class="flex justify-center gap-3">
            <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600">אמת 💭</button>
            <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600">חובה ⚡</button>
          </div>
          <p id="tod-text" class="text-base text-pink-200 bg-slate-900 p-4 rounded-xl">ממתין לשחקן הפעיל ללחוץ...</p>
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
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.0.0/firebase-analytics.js";
    import {
      getFirestore,
      collection,
      doc,
      setDoc,
      addDoc,
      onSnapshot,
      query,
      orderBy,
      serverTimestamp
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
    const me = { name: "משתמש", gender: "זכר", age: 18, city: "ישראל", bio: "", avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" };
    let currentUserKey = "guest_user";
    let vipActiveUntil = 0;
    let activeRoomId = "r-music";
    let unsubMsgs = null;
    const localRooms = [
      { id: "r-music", topic: "מוזיקה והופעות", type: "free" },
      { id: "r-travel", topic: "טיולים וסופ״ש", type: "free" },
      { id: "r-games", topic: "משחקי חברה וצחוק", type: "free" },
      { id: "r-vip-1", topic: "טרקלין VIP פרטי", type: "vip" }
    ];

    function openApp() {
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      renderRooms();
    }

    $("toggle-password-btn").onclick = () => {
      $("auth-password").type = $("auth-password").type === "password" ? "text" : "password";
    };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      const email = $("auth-email").value.trim();
      const age = Number($("auth-age").value);
      if (!age || age < 18) {
        $("auth-error").textContent = "הרשמה וכניסה מותרים מגיל 18 ומעלה בלבד.";
        $("auth-error").classList.remove("hidden");
        return;
      }
      $("auth-error").classList.add("hidden");
      me.age = age;
      $("prof-age").value = age;
      currentUserKey = email.replace(/[^a-zA-Z0-9_-]/g, "_") || "user_18";
      try { await setDoc(doc(db, "users", currentUserKey), { email, age, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      openApp();
    };

    $("logout-btn").onclick = () => location.reload();

    document.querySelectorAll(".tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".tab-btn").forEach((b) => { b.className = "tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300"; });
        btn.className = "tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white";
        document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
        $(`tab-${btn.dataset.tab}`).classList.remove("hidden");
      };
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
      $("user-badge").textContent = `${me.name} • ${me.gender}, ${me.age}`;
      try { await setDoc(doc(db, "users", currentUserKey), { ...me, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 1500);
    };function hasVipPass() { return Date.now() < vipActiveUntil; }

    function listenRoomMessages(roomId, lockedVip) {
      if (unsubMsgs) { unsubMsgs(); unsubMsgs = null; }
      if (lockedVip) {
        $("chat-messages").innerHTML = `<p class="text-xs text-amber-300">חדר VIP עולה 5 ש"ח ליום. לחץ על "שלם 5 ש"ח ליום עבור VIP" לפתיחה.</p>`;
        return;
      }
      const q = query(collection(db, "rooms", roomId, "messages"), orderBy("createdAt", "asc"));
      unsubMsgs = onSnapshot(q, (snap) => {
        const msgs = snap.docs.map((d) => d.data());
        $("chat-messages").innerHTML = msgs.length
          ? msgs.map((m) => `<div class="bg-slate-800 px-3 py-2 rounded-xl text-sm"><strong class="text-pink-300">${m.from || "משתמש"}:</strong> ${m.text || ""}</div>`).join("")
          : `<p class="text-xs text-slate-400">אין עדיין הודעות בחדר הזה.</p>`;
      });
    }

    function renderRooms() {
      $("rooms-list").innerHTML = localRooms.map((r) => {
        const isVip = r.type === "vip";
        const isAct = r.id === activeRoomId;
        return `<button type="button" data-select-room="${r.id}" class="w-full text-right p-3 rounded-xl border text-xs transition ${isAct ? "bg-pink-600/30 border-pink-400" : "bg-slate-950/70 border-slate-800"}">
          <div class="font-bold text-sm">${isVip ? "👑 " : "💬 "}${r.topic}</div>
          <div class="mt-0.5 ${isVip ? "text-amber-300" : "text-emerald-300"}">${isVip ? "VIP • 5 ש\"ח ליום" : "חינם"}</div>
        </button>`;
      }).join("");

      document.querySelectorAll("[data-select-room]").forEach((btn) => {
        btn.onclick = () => { activeRoomId = btn.dataset.selectRoom; renderRooms(); };
      });

      const cur = localRooms.find((r) => r.id === activeRoomId) || localRooms[0];
      activeRoomId = cur.id;
      const lockedVip = cur.type === "vip" && !hasVipPass();
      $("active-room-title").textContent = cur.topic;
      $("active-room-meta").textContent = cur.type === "vip"
        ? (hasVipPass() ? "חדר VIP פעיל (שולם 5 ש\"ח ליום)" : "חדר VIP נעול — תשלום 5 ש\"ח ליום")
        : "חדר נושא רגיל — חינם";
      $("unlock-vip-btn").classList.toggle("hidden", !lockedVip);
      listenRoomMessages(cur.id, lockedVip);
    }

    $("unlock-vip-btn").onclick = async () => {
      vipActiveUntil = Date.now() + 24 * 60 * 60 * 1000;
      try { await setDoc(doc(db, "vipPasses", currentUserKey), { priceILS: 5, period: "day", vipActiveUntil, updatedAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("create-room-form").onsubmit = async (e) => {
      e.preventDefault();
      const topic = $("new-room-topic").value.trim();
      const type = $("new-room-type").value;
      if (!topic) return;
      const roomObj = { id: `r-${Date.now()}`, topic, type };
      localRooms.unshift(roomObj);
      activeRoomId = roomObj.id;
      $("new-room-topic").value = "";
      try { await setDoc(doc(db, "rooms", roomObj.id), { ...roomObj, createdAt: serverTimestamp() }, { merge: true }); } catch {}
      renderRooms();
    };

    $("chat-form").onsubmit = async (e) => {
      e.preventDefault();
      const cur = localRooms.find((r) => r.id === activeRoomId);
      if (!cur || (cur.type === "vip" && !hasVipPass())) return;
      const txt = $("chat-input").value.trim();
      if (!txt) return;
      $("chat-input").value = "";
      await addDoc(collection(db, "rooms", cur.id, "messages"), { from: me.name, text: txt, createdAt: serverTimestamp() });
    };

    const mp = { active: "p1", waiting: "p1", rps: { p1: null, p2: null } };
    function updateMpBanner() {
      const who = mp.waiting === "p1" ? "פרופיל א'" : "פרופיל ב'";
      $("multiplayer-status").textContent = `ממתין לפעולה של ${who} (אסור לשחק לבד)`;
    }
    $("game-profile-select").onchange = (e) => { mp.active = e.target.value; updateMpBanner(); };
    updateMpBanner();

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".game-tab-btn").forEach((b) => { b.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300"; });
        btn.className = "game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600";
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${btn.dataset.game}`).classList.remove("hidden");
      };
    });

    const rpsMap = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
    document.querySelectorAll(".rps-choice").forEach((b) => {
      b.onclick = () => {
        if (mp.active !== mp.waiting) { $("rps-result").textContent = `עכשיו מחכים ל${mp.waiting === "p1" ? "פרופיל א'" : "פרופיל ב'"} שילחץ!`; return; }
        mp.rps[mp.active] = b.dataset.rps;
        if (!mp.rps.p1 || !mp.rps.p2) {
          mp.waiting = mp.active === "p1" ? "p2" : "p1"; updateMpBanner();
          $("rps-result").textContent = "הבחירה נשמרה! ממתין לפרופיל השני שילחץ..."; return;
        }
        $("rps-result").textContent = `פרופיל א': ${rpsMap[mp.rps.p1]} | פרופיל ב': ${rpsMap[mp.rps.p2]}`;
        mp.rps = { p1: null, p2: null }; mp.waiting = "p1"; updateMpBanner();
      };
    });

    $("btn-truth").onclick = () => {
      if (mp.active !== mp.waiting) { $("tod-text").textContent = "ממתין לשחקן השני בתור..."; return; }
      $("tod-text").textContent = "💭 אמת: מה הנושא שהכי מעניין אותך לשיחה?";
      mp.waiting = mp.waiting === "p1" ? "p2" : "p1"; updateMpBanner();
    };
    $("btn-dare").onclick = () => {
      if (mp.active !== mp.waiting) { $("tod-text").textContent = "ממתין לשחקן השני בתור..."; return; }
      $("tod-text").textContent = "⚡ חובה: פתח חדר שיחה חדש בנושא שמעניין אותך!";
      mp.waiting = mp.waiting === "p1" ? "p2" : "p1"; updateMpBanner();
    };let bgBoard = Array(24).fill(null).map(() => ({ c: null, n: 0 })), bgSel = null;
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
    $("chess-reset").onclick = () => { cb = startChess.map((r) => [...r]); cs = null; whiteTurn = true; $("chess-turn").textContent = "תור: לבן"; renderChess(); };
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

    let ttt = Array(9).fill(""), xTurn = true;
    function renderTtt() {
      $("ttt-board").innerHTML = "";
      ttt.forEach((v, i) => {
        const b = document.createElement("button"); b.type = "button"; b.className = "h-14 rounded-xl bg-slate-800 border border-slate-700 text-xl font-bold"; b.textContent = v;
        b.onclick = () => { if (!v) { ttt[i] = xTurn ? "❌" : "⭕"; xTurn = !xTurn; $("ttt-status").textContent = `תור: ${xTurn ? "❌" : "⭕"}`; renderTtt(); } };
        $("ttt-board").appendChild(b);
      });
    }
    $("ttt-reset").onclick = () => { ttt = Array(9).fill(""); xTurn = true; $("ttt-status").textContent = "תור: ❌"; renderTtt(); }; renderTtt();

    $("rom-submit").onclick = () => { const v = $("rom-input").value.trim(); if (v) { $("rom-feedback").textContent = `נשמר: "${v}"`; $("rom-input").value = ""; } };

    let taps = 0;
    $("tap-btn").onclick = () => { taps++; $("tap-counter").textContent = `לחיצות: ${taps}${taps >= 20 ? " — יעד הושג! 🎉" : ""}`; };
  </script>
</body>
</html>
