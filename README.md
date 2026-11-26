<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove IL — אתר דוגמא</title>
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
      user-select: none;
    }
    .chess-light { background: #e2e8f0; color: #0f172a; }
    .chess-dark { background: #475569; color: #ffffff; }
    .chess-selected {
      outline: 3px solid #ec4899;
      outline-offset: -3px;
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
  <header class="glass sticky top-0 z-50 px-6 py-4 flex flex-wrap items-center justify-between gap-3 shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">
        TopLove IL
      </h1>
      <span class="text-xs bg-pink-500/20 border border-pink-400/40 text-pink-200 px-2.5 py-0.5 rounded-full">מצב דמו חי</span>
    </div>
    <div class="flex items-center gap-3">
      <span id="user-badge" class="hidden text-sm text-slate-200 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 py-8 space-y-6">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-6">
      <h2 id="auth-title" class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">התחברו, הירשמו או היכנסו מיד לדוגמא חיה</p>

      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr"
          class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <div class="relative">
          <input type="password" id="auth-password" required minlength="6" placeholder="סיסמה (מינימום 6 תווים)" dir="ltr"
            class="w-full px-4 py-2.5 pl-11 rounded-xl bg-slate-900 border border-slate-700 text-left" />
          <button type="button" id="toggle-password-btn" aria-label="הצג או הסתר סיסמה"
            class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 hover:text-white">👁️</button>
        </div>
        <button type="submit" id="auth-submit-btn"
          class="w-full py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
          כניסה / הרשמה
        </button>
      </form>

      <button type="button" id="quick-demo-btn"
        class="mt-3 w-full py-2.5 rounded-xl font-semibold bg-emerald-600 hover:bg-emerald-500 text-sm">
        ⚡ כניסה מהירה לדוגמא (אור, 27, חיפה)
      </button>
    </section><section id="app-section" class="hidden space-y-6">
      <div id="vip-invites-banner" class="hidden glass border border-amber-400/50 rounded-2xl p-4 space-y-2">
        <h3 class="text-sm font-bold text-amber-300">✨ הזמנות לחדר VIP פרטי</h3>
        <div id="vip-invites-list" class="space-y-2"></div>
      </div>

      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">
          1. הפרופיל שלי
        </button>
        <button type="button" data-tab="discover" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">
          2. פרופילים ומעקב
        </button>
        <button type="button" data-tab="rooms" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">
          3. שולחנות וחדרי VIP 💬
        </button>
        <button type="button" data-tab="games" class="tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">
          4. עמודת 10 משחקים 🎮
        </button>
      </div>

      <div id="tab-profile" class="tab-content max-w-2xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="flex flex-col sm:flex-row items-center gap-4 bg-slate-900/70 p-4 rounded-xl border border-slate-700/70">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=Or" alt="תמונת פרופיל"
              class="w-20 h-20 rounded-full object-cover border-2 border-pink-500 bg-slate-800 shrink-0" />
            <div class="w-full space-y-2">
              <label class="block text-sm font-medium text-pink-300">תמונת פרופיל (העלאה מהמחשב או קישור)</label>
              <input type="file" id="prof-avatar-file" accept="image/*"
                class="block w-full text-xs text-slate-300 file:ml-3 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:bg-pink-600 file:text-white" />
              <input type="url" id="prof-avatar-url" placeholder="קישור לתמונה (https://...)" dir="ltr"
                class="w-full px-3 py-1.5 text-sm rounded-lg bg-slate-950 border border-slate-700 text-left" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-name" required value="אור" placeholder="שם / כינוי"
              class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="number" id="prof-age" min="18" max="99" required value="27" placeholder="גיל"
              class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-city" required value="חיפה" placeholder="עיר"
              class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <select id="prof-status" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">
              <option value="פתוח/ה למשחקים 🎲" selected>פתוח/ה למשחקים 🎲</option>
              <option value="זמין/ה להיכרות 💜">זמין/ה להיכרות 💜</option>
              <option value="מחפש/ת קשר רציני 💍">מחפש/ת קשר רציני 💍</option>
              <option value="מוכן/ה לחדר VIP ✨">מוכן/ה לחדר VIP ✨</option>
            </select>
          </div>
          <textarea id="prof-bio" rows="3" placeholder="קצת עליי..."
            class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">אוהב משחקי שולחן, שיחות טובות וקפה של ערב.</textarea>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר בפרופיל!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
              שמור פרופיל
            </button>
          </div>
        </form>
      </div><div id="tab-discover" class="tab-content hidden space-y-4">
        <div class="flex flex-wrap justify-between items-center gap-2">
          <h2 class="text-xl font-bold">פרופילים מחוברים עכשיו</h2>
          <div class="flex items-center gap-2">
            <span id="following-count" class="text-sm bg-pink-600/30 border border-pink-500/40 text-pink-200 px-3 py-1 rounded-full">
              עוקב אחרי: 0
            </span>
            <span id="users-count" class="text-sm glass px-3 py-1 rounded-full">4 משתמשים</span>
          </div>
        </div>
        <div id="profiles-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div>

      <div id="tab-rooms" class="tab-content hidden space-y-6">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <div class="glass rounded-2xl p-5 space-y-4">
            <h2 class="text-lg font-bold">🪑 שולחנות פתוחים</h2>
            <div id="open-tables-list" class="space-y-2"></div>

            <div class="pt-4 border-t border-white/10 space-y-2">
              <h3 class="text-sm font-bold text-amber-300">👑 חדרי VIP פרטיים (בהזמנה בלבד)</h3>
              <p class="text-xs text-slate-400">הזמן משתמש מהפרופילים או מתוך השולחן — החדר נפתח רק לאחר אישור.</p>
              <div id="vip-rooms-list" class="space-y-2"></div>
            </div>
          </div>

          <div class="lg:col-span-2 glass rounded-2xl p-5 flex flex-col justify-between min-h-[460px] space-y-4">
            <div>
              <div class="flex flex-wrap items-center justify-between gap-2 pb-3 border-b border-white/10">
                <div>
                  <h3 id="active-room-title" class="text-lg font-bold">שולחן 1 — קפה ושיחות היכרות ☕</h3>
                  <p id="active-room-subtitle" class="text-xs text-slate-300">יושבים סביב השולחן כעת</p>
                </div>
                <span id="active-room-badge" class="text-xs bg-pink-600/30 border border-pink-400/40 text-pink-200 px-3 py-1 rounded-full">
                  שולחן פתוח
                </span>
              </div>

              <div id="room-seats" class="flex flex-wrap gap-2 py-3 border-b border-white/10"></div>
              <div id="room-chat-messages" class="space-y-2.5 max-h-64 overflow-y-auto py-3"></div>
            </div>

            <form id="room-chat-form" class="flex gap-2 pt-2 border-t border-white/10">
              <input type="text" id="room-chat-input" required placeholder="כתוב הודעה למי שיושב סביב השולחן..."
                class="flex-1 px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-sm" />
              <button type="submit" class="px-5 py-2.5 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
                שלח ✉️
              </button>
            </form>
          </div>
        </div>
      </div><div id="tab-games" class="tab-content hidden space-y-6">
        <div class="glass rounded-2xl p-5 space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-3">
            <div>
              <h2 class="text-2xl font-bold">🎮 עמודת 10 המשחקים של TopLove</h2>
              <p class="text-xs sm:text-sm text-slate-300">אינטראקציה חיה מול שותף/יריב, 3 שלבים בכל משחק ופרס ייחודי לכל משחק</p>
            </div>
            <span id="prizes-summary" class="text-sm bg-amber-500/20 border border-amber-400/40 text-amber-200 px-4 py-1.5 rounded-full font-semibold">
              פרסים שנפתחו: 0 / 10
            </span>
          </div>

          <div class="flex flex-wrap items-center justify-between gap-3 bg-slate-900/80 p-3.5 rounded-xl border border-slate-700">
            <div class="flex items-center gap-3">
              <img id="opponent-avatar" src="" alt="יריב" class="w-11 h-11 rounded-full object-cover border border-pink-400 bg-slate-800" />
              <div>
                <div class="text-xs text-pink-300 font-semibold">משחק מול / עם בלייב:</div>
                <div id="opponent-details" class="text-sm font-bold text-white"></div>
              </div>
            </div>
            <div class="flex items-center gap-2">
              <label for="opponent-select" class="text-xs text-slate-300">בחר יריב:</label>
              <select id="opponent-select" class="px-3 py-1.5 rounded-lg bg-slate-800 border border-slate-600 text-xs sm:text-sm"></select>
            </div>
          </div>

          <div id="prizes-shelf" class="flex flex-wrap gap-2"></div>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="rps" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold bg-pink-600 text-white">1. אבן נייר ומספריים</button>
          <button type="button" data-game="tod" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">2. אמת או חובה</button>
          <button type="button" data-game="backgammon" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">3. שש בש אמיתי</button>
          <button type="button" data-game="chess" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">4. שחמט</button>
          <button type="button" data-game="trivia" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">5. טריוויה דו-קרב</button>
          <button type="button" data-game="memory" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">6. זיכרון משותף</button>
          <button type="button" data-game="number" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">7. ניחוש מספרים</button>
          <button type="button" data-game="ttt" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">8. איקס עיגול</button>
          <button type="button" data-game="romance" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">9. אתגר רומנטי</button>
          <button type="button" data-game="tap" class="game-tab-btn px-3 py-2 rounded-xl text-xs font-semibold glass text-slate-300">10. קרב מהירות</button>
        </div>

        <div id="game-rps" class="game-panel max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="rps-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: כתר האסטרטג 👑</span>
          </div>
          <h3 class="text-xl font-bold">✂️ אבן נייר ומספריים בלייב</h3>
          <p class="text-xs text-slate-300">בחר מהלך — היריב בוחר מולך והתוצאה מוצגת לשניכם מיד!</p>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">✂️ מספריים</button>
          </div>
          <div id="rps-live-box" class="bg-slate-900 border border-slate-700 rounded-xl p-4 text-sm text-pink-200 space-y-1">
            <div>הבחירה שלך: <strong id="rps-my-choice">—</strong></div>
            <div>בחירת היריב: <strong id="rps-opp-choice">—</strong></div>
            <p id="rps-result" class="font-semibold text-white pt-1">בחר אבן, נייר או מספריים כדי לשחק מול היריב!</p>
          </div>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="tod-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: תג שובר הקרח 🔥</span>
          </div>
          <h3 class="text-xl font-bold">🔥 אמת או חובה משותף</h3>
          <div class="flex justify-center gap-3">
            <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600 hover:bg-indigo-500">אמת 💭</button>
            <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600 hover:bg-pink-500">חובה ⚡</button>
          </div>
          <div class="bg-slate-900 border border-slate-700 rounded-2xl p-5 min-h-[105px] flex flex-col items-center justify-center gap-2">
            <p id="tod-text" class="text-base text-pink-200">בחר אמת או חובה — היריב יגיב לתשובה שלך בלייב!</p>
            <p id="tod-opp-reaction" class="text-xs text-emerald-300"></p>
          </div>
        </div><div id="game-backgammon" class="game-panel hidden max-w-4xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="bg-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: גביע הקוביות 🎲</span>
          </div>
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">🎲 לוח שש בש מקורי (24 נקודות)</h3>
            <div class="flex flex-wrap items-center gap-2">
              <button type="button" id="bg-roll" class="px-4 py-1.5 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
                זרוק קוביות 🎲
              </button>
              <button type="button" id="bg-opp-turn" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-amber-600 hover:bg-amber-500">
                מהלך יריב ▶
              </button>
              <button type="button" id="bg-next-stage" class="px-3.5 py-1.5 rounded-xl text-xs font-semibold bg-emerald-600 hover:bg-emerald-500">
                השלם שלב ✓
              </button>
              <button type="button" id="bg-reset" class="px-3.5 py-1.5 rounded-xl text-xs bg-slate-800 border border-slate-600">
                איפוס לוח
              </button>
            </div>
          </div>
          <div class="flex flex-wrap items-center justify-center gap-4 text-sm bg-slate-900/80 py-2 px-4 rounded-xl border border-slate-700">
            <span>קובייה 1: <strong id="bg-d1" class="text-amber-300 text-base">-</strong></span>
            <span>קובייה 2: <strong id="bg-d2" class="text-amber-300 text-base">-</strong></span>
            <span id="bg-status" class="text-pink-200">לחץ "זרוק קוביות", בחר נקודה (1-24) עם כלים שלך ולחץ על נקודת יעד</span>
          </div>
          <div class="bg-table p-3 space-y-3">
            <div class="text-[11px] text-amber-200/80 text-right">חצי עליון (נקודות 13–24)</div>
            <div id="bg-top-row" class="grid grid-cols-6 sm:grid-cols-12 gap-1"></div>
            <div class="h-2 rounded-full bg-amber-900/90 border border-amber-700/60"></div>
            <div id="bg-bottom-row" class="grid grid-cols-6 sm:grid-cols-12 gap-1"></div>
            <div class="text-[11px] text-amber-200/80 text-right">חצי תחתון (נקודות 12–1)</div>
          </div>
        </div>

        <div id="game-chess" class="game-panel hidden max-w-lg mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="chess-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: מדליית האלוף ♟️</span>
          </div>
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">♟️ שחמט מול היריב</h3>
            <div class="flex gap-2">
              <button type="button" id="chess-next-stage" class="text-xs bg-pink-600 px-3 py-1.5 rounded-lg font-semibold">השלם שלב ✓</button>
              <button type="button" id="chess-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">אפס</button>
            </div>
          </div>
          <p id="chess-turn" class="text-sm text-pink-200">תור: לבן (אתה) — הזז כלי והיריב יגיב אוטומטית</p>
          <div id="chess-board" class="chess-board"></div>
        </div>

        <div id="game-trivia" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="trivia-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: לב הזהב 💛</span>
          </div>
          <h3 class="text-xl font-bold">💛 טריוויה דו-קרב</h3>
          <p id="trivia-q" class="text-base text-pink-200 font-medium"></p>
          <div id="trivia-options" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5"></div>
          <p id="trivia-feedback" class="text-sm text-emerald-300 min-h-[1.5rem]"></p>
        </div><div id="game-memory" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="memory-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: יהלום הזיכרון 💎</span>
          </div>
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">💎 זיכרון אמוג'י</h3>
            <button type="button" id="memory-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">ערבב</button>
          </div>
          <div id="memory-grid" class="grid grid-cols-4 gap-2"></div>
          <p id="memory-status" class="text-sm text-pink-200">מצא את כל הזוגות כדי לעלות שלב!</p>
        </div>

        <div id="game-number" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="num-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: כוכב המזל ⭐</span>
          </div>
          <h3 class="text-xl font-bold">⭐ ניחוש מספרים</h3>
          <p id="num-range" class="text-sm text-slate-300"></p>
          <div class="flex justify-center gap-2">
            <input type="number" id="num-input" min="1" max="100" placeholder="מספר"
              class="w-28 px-3 py-2 rounded-xl bg-slate-900 border border-slate-700 text-center" />
            <button type="button" id="num-check" class="px-5 py-2 rounded-xl font-semibold bg-pink-600">בדוק</button>
          </div>
          <p id="num-hint" class="text-sm text-pink-200 min-h-[1.5rem]"></p>
        </div>

        <div id="game-ttt" class="game-panel hidden max-w-sm mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="ttt-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: דגל הניצחון 🚩</span>
          </div>
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">🚩 איקס עיגול</h3>
            <button type="button" id="ttt-reset" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-600">חדש</button>
          </div>
          <div id="ttt-board" class="grid grid-cols-3 gap-2 max-w-[240px] mx-auto"></div>
          <p id="ttt-status" class="text-sm text-pink-200">אתה ❌ מול היריב ⭕</p>
        </div>

        <div id="game-romance" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="rom-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: ורד הקסם 🌹</span>
          </div>
          <h3 class="text-xl font-bold">🌹 אתגר פתיחה רומנטי</h3>
          <p id="rom-prompt" class="text-base text-pink-200 bg-slate-900 border border-slate-700 rounded-2xl p-4"></p>
          <input type="text" id="rom-input" placeholder="כתוב משפט פתיחה..."
            class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          <button type="button" id="rom-submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">
            שלח והתקדם ✨
          </button>
          <p id="rom-feedback" class="text-sm text-emerald-300 min-h-[1.5rem]"></p>
        </div>

        <div id="game-tap" class="game-panel hidden max-w-md mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex justify-between items-center text-xs bg-slate-900/80 px-3.5 py-2 rounded-xl border border-slate-700">
            <span id="tap-stage" class="text-pink-300 font-semibold">שלב 1 / 3</span>
            <span class="text-amber-300">פרס: ברק הזמן ⚡</span>
          </div>
          <h3 class="text-xl font-bold">⚡ קרב מהירות לחיצות</h3>
          <p id="tap-goal" class="text-sm text-slate-300"></p>
          <button type="button" id="tap-btn"
            class="w-full py-5 rounded-2xl text-xl font-bold bg-gradient-to-l from-pink-600 to-indigo-600 active:scale-95 transition">
            לחץ מהר! ⚡
          </button>
          <p id="tap-counter" class="text-base font-semibold text-pink-200">לחיצות: 0</p>
        </div>
      </div>
    </section>
  </main><script>
    const $ = (id) => document.getElementById(id);

    const me = {
      uid: "me",
      name: "אור",
      age: 27,
      city: "חיפה",
      status: "פתוח/ה למשחקים 🎲",
      bio: "אוהב משחקי שולחן, שיחות טובות וקפה של ערב.",
      avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=Or"
    };

    const community = [
      {
        uid: "noa",
        name: "נועה",
        age: 26,
        city: "תל אביב",
        status: "מחפשת קשר רציני 💍",
        bio: "אוהבת שש בש, סרטים ושיחות עומק בלילה.",
        avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=Noa",
        followers: 14
      },
      {
        uid: "daniel",
        name: "דניאל",
        age: 29,
        city: "ירושלים",
        status: "פתוח/ה למשחקים 🎲",
        bio: "אלוף שחמט חובב וקפה הפוך.",
        avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=Daniel",
        followers: 9
      },
      {
        uid: "maya",
        name: "מאיה",
        age: 25,
        city: "הרצליה",
        status: "זמינה להיכרות 💜",
        bio: "תמיד בעד אמת או חובה וטיולים בסופ״ש.",
        avatar: "https://api.dicebear.com/9.x/avataaars/svg?seed=Maya",
        followers: 19
      }
    ];

    const following = new Set(["noa"]);
    let selectedOpponentId = "noa";

    function enterApp(labelText) {
      $("auth-section").classList.add("hidden");
      $("app-section").classList.remove("hidden");
      $("user-badge").classList.remove("hidden");
      $("logout-btn").classList.remove("hidden");
      $("user-badge").textContent = labelText || `${me.name} (${me.city})`;
      renderProfiles();
      renderOpponentSelect();
      renderVipInvites();
      renderRoomsUI();
    }

    $("toggle-password-btn").onclick = () => {
      const inp = $("auth-password");
      inp.type = inp.type === "password" ? "text" : "password";
    };

    $("auth-form").onsubmit = (e) => {
      e.preventDefault();
      enterApp($("auth-email").value.trim());
    };

    $("quick-demo-btn").onclick = () => enterApp(`${me.name}, ${me.age} • ${me.city}`);

    $("logout-btn").onclick = () => {
      $("app-section").classList.add("hidden");
      $("auth-section").classList.remove("hidden");
      $("user-badge").classList.add("hidden");
      $("logout-btn").classList.add("hidden");
    };

    document.querySelectorAll(".tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".tab-btn").forEach((b) => {
          b.classList.remove("bg-pink-600", "text-white");
          b.classList.add("glass", "text-slate-300");
        });
        btn.classList.add("bg-pink-600", "text-white");
        btn.classList.remove("glass", "text-slate-300");
        document.querySelectorAll(".tab-content").forEach((c) => c.classList.add("hidden"));
        $(`tab-${btn.dataset.tab}`).classList.remove("hidden");
      };
    });

    $("prof-avatar-file").onchange = (e) => {
      const file = e.target.files?.[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => {
        me.avatar = String(reader.result);
        $("prof-avatar-preview").src = me.avatar;
      };
      reader.readAsDataURL(file);
    };

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
      me.status = $("prof-status").value;
      me.bio = $("prof-bio").value.trim();
      $("user-badge").textContent = `${me.name}, ${me.age} • ${me.city}`;
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 2000);
      renderProfiles();
    };

    const openTables = [
      { id: "t1", title: "שולחן 1 — קפה ושיחות היכרות ☕", members: ["noa", "daniel"], msgs: [
        { from: "נועה", text: "היי! מי בא לשחק אבן נייר ומספריים או שש בש?" },
        { from: "דניאל", text: "אני פה! שולחן נעים ממש." }
      ]},
      { id: "t2", title: "שולחן 2 — משחקים ואדרנלין 🎲", members: ["daniel", "maya"], msgs: [
        { from: "מאיה", text: "מי מוכן לאמת או חובה?" }
      ]},
      { id: "t3", title: "שולחן 3 — שיחות עומק ומוזיקה 🎶", members: ["noa", "maya"], msgs: [
        { from: "נועה", text: "אפשר להזמין לחדר VIP כשמתאים לשיחה אישית." }
      ]}
    ];

    const pendingVipInvites = [
      { id: "inv-maya", fromUserId: "maya", text: "מאיה (25, הרצליה) מזמינה אותך לחדר VIP פרטי להיכרות מעמיקה" }
    ];

    const approvedVipRooms = [];
    let activeRoom = { type: "open", id: "t1" };

    function getUserById(id) {
      if (id === "me") return me;
      return community.find((u) => u.uid === id);
    }

    function sendVipInvite(userId) {
      const target = getUserById(userId);
      if (!target) return;
      const existingRoom = approvedVipRooms.find((r) => r.partnerId === userId);
      if (existingRoom) {
        activeRoom = { type: "vip", id: existingRoom.id };
        document.querySelector('[data-tab="rooms"]').click();
        renderRoomsUI();
        return;
      }
      const roomId = `vip-${userId}`;
      approvedVipRooms.push({
        id: roomId,
        partnerId: userId,
        title: `חדר VIP פרטי — ${me.name} & ${target.name} ✨`,
        msgs: [
          { from: "מערכת VIP", text: `חדר VIP נפתח בהזמנה עבור ${me.name} ו-${target.name}. שיחה פרטית ושקטה.` }
        ]
      });
      activeRoom = { type: "vip", id: roomId };
      document.querySelector('[data-tab="rooms"]').click();
      renderRoomsUI();
    }

    function renderVipInvites() {
      if (!pendingVipInvites.length) {
        $("vip-invites-banner").classList.add("hidden");
        return;
      }
      $("vip-invites-banner").classList.remove("hidden");
      $("vip-invites-list").innerHTML = pendingVipInvites.map((inv) => `
        <div class="flex flex-wrap items-center justify-between gap-2 bg-slate-900/90 p-3 rounded-xl border border-amber-400/30">
          <span class="text-sm text-amber-100">${inv.text}</span>
          <div class="flex gap-2">
            <button type="button" onclick="acceptInvite('${inv.id}')" class="px-3 py-1 rounded-lg bg-emerald-600 text-xs font-semibold">אשר כניסה</button>
            <button type="button" onclick="declineInvite('${inv.id}')" class="px-3 py-1 rounded-lg bg-slate-700 text-xs">דחה</button>
          </div>
        </div>
      `).join("");
    }

    window.acceptInvite = (invId) => {
      const idx = pendingVipInvites.findIndex((i) => i.id === invId);
      if (idx === -1) return;
      const inv = pendingVipInvites[idx];
      pendingVipInvites.splice(idx, 1);
      const partner = getUserById(inv.fromUserId);
      const roomId = `vip-${inv.fromUserId}`;
      approvedVipRooms.push({
        id: roomId,
        partnerId: inv.fromUserId,
        title: `חדר VIP פרטי — ${me.name} & ${partner.name} ✨`,
        msgs: [{ from: partner.name, text: `שמח/ה שאישרת את ההזמנה לחדר VIP! איך עובר עליך היום?` }]
      });
      activeRoom = { type: "vip", id: roomId };
      renderVipInvites();
      renderRoomsUI();
    };

    window.declineInvite = (invId) => {
      const idx = pendingVipInvites.findIndex((i) => i.id === invId);
      if (idx !== -1) pendingVipInvites.splice(idx, 1);
      renderVipInvites();
    };

    function renderRoomsUI() {
      $("open-tables-list").innerHTML = openTables.map((t) => {
        const isAct = activeRoom.type === "open" && activeRoom.id === t.id;
        return `<button type="button" onclick="selectRoom('open','${t.id}')" class="w-full text-right p-3 rounded-xl border text-sm transition ${isAct ? "bg-pink-600/30 border-pink-400" : "bg-slate-900/70 border-slate-700 hover:border-slate-500"}">
          <div class="font-semibold">${t.title}</div>
          <div class="text-xs text-slate-300 mt-0.5">יושבים: ${t.members.length + 1} / 6</div>
        </button>`;
      }).join("");

      $("vip-rooms-list").innerHTML = approvedVipRooms.length
        ? approvedVipRooms.map((r) => {
            const isAct = activeRoom.type === "vip" && activeRoom.id === r.id;
            return `<button type="button" onclick="selectRoom('vip','${r.id}')" class="w-full text-right p-3 rounded-xl border text-sm transition ${isAct ? "bg-amber-500/25 border-amber-400" : "bg-slate-900/70 border-slate-700"}">
              <div class="font-semibold text-amber-200">${r.title}</div>
              <div class="text-xs text-slate-300">חדר פרטי מאושר בהזמנה</div>
            </button>`;
          }).join("")
        : `<p class="text-xs text-slate-400 bg-slate-900/50 p-3 rounded-xl">אין כרגע חדרי VIP פתוחים. שלח הזמנה מכרטיס פרופיל.</p>`;

      let currentObj, seatsIds = ["me"];
      if (activeRoom.type === "open") {
        currentObj = openTables.find((t) => t.id === activeRoom.id) || openTables[0];
        seatsIds = ["me", ...currentObj.members];
        $("active-room-badge").textContent = "שולחן פתוח";
        $("active-room-badge").className = "text-xs bg-pink-600/30 border border-pink-400/40 text-pink-200 px-3 py-1 rounded-full";
      } else {
        currentObj = approvedVipRooms.find((r) => r.id === activeRoom.id) || openTables[0];
        seatsIds = ["me", currentObj.partnerId];
        $("active-room-badge").textContent = "👑 חדר VIP בהזמנה";
        $("active-room-badge").className = "text-xs bg-amber-500/25 border border-amber-400/50 text-amber-200 px-3 py-1 rounded-full";
      }

      $("active-room-title").textContent = currentObj.title;
      $("active-room-subtitle").textContent = "יושבים סביב השולחן כעת — לחץ על משתמש להזמנה ל-VIP";

      $("room-seats").innerHTML = seatsIds.map((uid) => {
        const u = getUserById(uid);
        if (!u) return "";
        const isMe = uid === "me";
        return `<div class="flex items-center gap-2 bg-slate-900 px-3 py-1.5 rounded-full border border-slate-700 text-xs">
          <img src="${u.avatar}" class="w-6 h-6 rounded-full object-cover" alt="${u.name}" />
          <span>${u.name}${isMe ? " (את/ה)" : ""}</span>
          ${!isMe ? `<button type="button" onclick="sendVipInvite('${u.uid}')" class="text-amber-300 hover:underline font-semibold">הזמן ל-VIP</button>` : ""}
        </div>`;
      }).join("");

      $("room-chat-messages").innerHTML = currentObj.msgs.map((m) => `
        <div class="bg-slate-900/90 border border-slate-800 rounded-xl px-3.5 py-2 text-sm">
          <span class="font-bold text-pink-300">${m.from}:</span>
          <span class="text-slate-200 mr-1">${m.text}</span>
        </div>
      `).join("");
    }

    window.selectRoom = (type, id) => {
      activeRoom = { type, id };
      renderRoomsUI();
    };

    $("room-chat-form").onsubmit = (e) => {
      e.preventDefault();
      const txt = $("room-chat-input").value.trim();
      if (!txt) return;
      const currentObj = activeRoom.type === "open"
        ? openTables.find((t) => t.id === activeRoom.id)
        : approvedVipRooms.find((r) => r.id === activeRoom.id);
      currentObj.msgs.push({ from: me.name, text: txt });
      $("room-chat-input").value = "";
      renderRoomsUI();
    };

    function renderProfiles() {
      $("following-count").textContent = `עוקב אחרי: ${following.size}`;
      $("users-count").textContent = `${community.length + 1} משתמשים`;
      $("profiles-grid").innerHTML = community.map((u) => {
        const isF = following.has(u.uid);
        return `<div class="glass rounded-2xl p-4 shadow-lg flex flex-col justify-between gap-3">
          <div>
            <div class="flex items-center gap-3 mb-2">
              <img src="${u.avatar}" alt="${u.name}" class="w-12 h-12 rounded-full object-cover border border-pink-400/60 bg-slate-800" />
              <div>
                <h3 class="font-bold">${u.name}, ${u.age}</h3>
                <p class="text-xs text-indigo-300">📍 ${u.city}</p>
              </div>
            </div>
            <span class="inline-block text-xs bg-slate-900 text-pink-300 px-2.5 py-1 rounded-full mb-2">${u.status}</span>
            <p class="text-sm text-slate-300">${u.bio}</p>
          </div>
          <div class="flex items-center justify-between pt-2 border-t border-white/10">
            <span class="text-xs text-slate-400">עוקבים: <strong class="text-white">${u.followers + (isF ? 1 : 0)}</strong></span>
            <div class="flex gap-1.5">
              <button type="button" onclick="toggleFollow('${u.uid}')" class="text-xs px-3 py-1.5 rounded-xl font-semibold ${isF ? "bg-emerald-600" : "bg-pink-600"}">
                ${isF ? "עוקב ✓" : "+ עקוב"}
              </button>
              <button type="button" onclick="sendVipInvite('${u.uid}')" class="text-xs px-3 py-1.5 rounded-xl font-semibold bg-amber-500/20 border border-amber-400/50 text-amber-200">
                VIP ✨
              </button>
            </div>
          </div>
        </div>`;
      }).join("");
    }

    window.toggleFollow = (uid) => {
      if (following.has(uid)) following.delete(uid);
      else following.add(uid);
      renderProfiles();
    };

    function renderOpponentSelect() {
      $("opponent-select").innerHTML = community.map((u) =>
        `<option value="${u.uid}" ${u.uid === selectedOpponentId ? "selected" : ""}>${u.name}, ${u.age} (${u.city})</option>`
      ).join("");
      updateOpponentHeader();
    }

    function updateOpponentHeader() {
      const opp = getUserById(selectedOpponentId) || community[0];
      $("opponent-avatar").src = opp.avatar;
      $("opponent-details").textContent = `${opp.name}, ${opp.age} • ${opp.city} — ${opp.status}`;
    }

    $("opponent-select").onchange = (e) => {
      selectedOpponentId = e.target.value;
      updateOpponentHeader();
    };

    const GAMES = [
      { id: "rps", prize: "כתר האסטרטג 👑" },
      { id: "tod", prize: "תג שובר הקרח 🔥" },
      { id: "backgammon", prize: "גביע הקוביות 🎲" },
      { id: "chess", prize: "מדליית האלוף ♟️" },
      { id: "trivia", prize: "לב הזהב 💛" },
      { id: "memory", prize: "יהלום הזיכרון 💎" },
      { id: "number", prize: "כוכב המזל ⭐" },
      { id: "ttt", prize: "דגל הניצחון 🚩" },
      { id: "romance", prize: "ורד הקסם 🌹" },
      { id: "tap", prize: "ברק הזמן ⚡" }
    ];

    const progress = Object.fromEntries(GAMES.map((g) => [g.id, { stage: 1, won: false }]));

    function renderPrizes() {
      const won = GAMES.filter((g) => progress[g.id].won).length;
      $("prizes-summary").textContent = `פרסים שנפתחו: ${won} / 10`;
      $("prizes-shelf").innerHTML = GAMES.map((g) => {
        const u = progress[g.id].won;
        return `<span class="text-xs px-3 py-1.5 rounded-full border ${u ? "bg-amber-500/25 border-amber-400 text-amber-200 font-semibold" : "bg-slate-900/70 border-slate-700 text-slate-400"}">
          ${u ? "✓ " : "🔒 "}${g.prize}
        </span>`;
      }).join("");
    }

    function nextStage(gameId, labelId) {
      const p = progress[gameId];
      if (p.stage < 3) p.stage++;
      else {
        p.won = true;
        p.stage = 1;
      }
      if (labelId) $(labelId).textContent = `שלב ${p.stage} / 3`;
      renderPrizes();
    }

    renderPrizes();document.querySelectorAll(".game-tab-btn").forEach((btn) => {
      btn.onclick = () => {
        document.querySelectorAll(".game-tab-btn").forEach((b) => {
          b.classList.remove("bg-pink-600", "text-white");
          b.classList.add("glass", "text-slate-300");
        });
        btn.classList.add("bg-pink-600", "text-white");
        btn.classList.remove("glass", "text-slate-300");
        document.querySelectorAll(".game-panel").forEach((p) => p.classList.add("hidden"));
        $(`game-${btn.dataset.game}`).classList.remove("hidden");
      };
    });

    const rpsMap = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = () => {
        const opp = getUserById(selectedOpponentId);
        const myMove = btn.dataset.rps;
        const oppMove = ["rock", "paper", "scissors"][Math.floor(Math.random() * 3)];
        $("rps-my-choice").textContent = `${me.name}: ${rpsMap[myMove]}`;
        $("rps-opp-choice").textContent = `${opp.name}: ${rpsMap[oppMove]}`;
        if (myMove === oppMove) {
          $("rps-result").textContent = `תיקו בלייב מול ${opp.name}!`;
        } else if (
          (myMove === "rock" && oppMove === "scissors") ||
          (myMove === "paper" && oppMove === "rock") ||
          (myMove === "scissors" && oppMove === "paper")
        ) {
          nextStage("rps", "rps-stage");
          $("rps-result").textContent = `ניצחת את ${opp.name}! עלית לשלב ${progress.rps.stage}`;
        } else {
          $("rps-result").textContent = `${opp.name} ניצח/ה בסיבוב הזה!`;
        }
      };
    });

    const truths = ["מה הדייט הכי מיוחד שחווית?", "מה מצחיק אותך תמיד?"];
    const dares = ["שלח/י ליריב מחמאה כנה בצ'אט!", "בחר/י שיר לדייט ערב."];
    function runTod(type) {
      const opp = getUserById(selectedOpponentId);
      const q = (type === "truth" ? truths : dares)[Math.floor(Math.random() * 2)];
      nextStage("tod", "tod-stage");
      $("tod-text").textContent = `${type === "truth" ? "💭 אמת" : "⚡ חובה"}: ${q}`;
      $("tod-opp-reaction").textContent = `💬 ${opp.name} צופה בתשובה שלך בלייב: "מעניין! אהבתי 🙂"`;
    }
    $("btn-truth").onclick = () => runTod("truth");
    $("btn-dare").onclick = () => runTod("dare");

    let bgPoints = Array(24).fill(null).map(() => ({ color: null, count: 0 }));
    let bgSelected = null;

    function initBackgammon() {
      bgPoints = Array(24).fill(null).map(() => ({ color: null, count: 0 }));
      bgPoints[0] = { color: "pink", count: 2 };
      bgPoints[11] = { color: "pink", count: 5 };
      bgPoints[16] = { color: "pink", count: 3 };
      bgPoints[18] = { color: "pink", count: 5 };

      bgPoints[23] = { color: "indigo", count: 2 };
      bgPoints[12] = { color: "indigo", count: 5 };
      bgPoints[7] = { color: "indigo", count: 3 };
      bgPoints[5] = { color: "indigo", count: 5 };
      bgSelected = null;
      renderBackgammon();
    }

    function renderPointCard(idx) {
      const pt = bgPoints[idx];
      const isSel = bgSelected === idx;
      const isEven = idx % 2 === 0;
      const pointNum = idx + 1;
      const btn = document.createElement("button");
      btn.type = "button";
      btn.className = `min-h-[105px] rounded-lg p-1 flex flex-col items-center justify-between border text-[10px] ${
        isSel ? "border-pink-400 bg-amber-800" : isEven ? "border-amber-700/60 bg-amber-950/85" : "border-amber-800/60 bg-stone-900/85"
      }`;
      btn.innerHTML = `<span class="text-amber-200/80 font-bold">${pointNum}</span>
        <div class="flex flex-col items-center gap-0.5 my-auto">
          ${Array.from({ length: Math.min(pt.count, 5) }).map(() =>
            `<span class="w-4 h-4 rounded-full inline-block shadow ${pt.color === "pink" ? "bg-pink-500" : "bg-indigo-500"}"></span>`
          ).join("")}
        </div>
        <span class="text-slate-300">${pt.count > 5 ? `x${pt.count}` : pt.count || ""}</span>`;

      btn.onclick = () => {
        if (bgSelected === null) {
          if (pt.count > 0) {
            bgSelected = idx;
            $("bg-status").textContent = `נבחרה נקודה ${pointNum} — לחץ על נקודת יעד`;
            renderBackgammon();
          }
        } else {
          if (bgSelected !== idx) {
            const from = bgPoints[bgSelected];
            if (from.count > 0 && (!pt.color || pt.color === from.color || pt.count <= 1)) {
              const movingColor = from.color;
              from.count--;
              if (from.count === 0) from.color = null;
              if (pt.color && pt.color !== movingColor && pt.count === 1) {
                pt.color = movingColor;
                pt.count = 1;
              } else {
                pt.color = movingColor;
                pt.count++;
              }
              $("bg-status").textContent = `הזזת כלי מנקודה ${bgSelected + 1} לנקודה ${pointNum}!`;
            }
          }
          bgSelected = null;
          renderBackgammon();
        }
      };
      return btn;
    }

    function renderBackgammon() {
      const topRow = $("bg-top-row");
      const bottomRow = $("bg-bottom-row");
      topRow.innerHTML = "";
      bottomRow.innerHTML = "";
      for (let i = 12; i < 24; i++) topRow.appendChild(renderPointCard(i));
      for (let i = 11; i >= 0; i--) bottomRow.appendChild(renderPointCard(i));
    }

    $("bg-roll").onclick = () => {
      const d1 = Math.floor(Math.random() * 6) + 1;
      const d2 = Math.floor(Math.random() * 6) + 1;
      $("bg-d1").textContent = d1;
      $("bg-d2").textContent = d2;
      $("bg-status").textContent = `זרקת ${d1} ו-${d2}${d1 === d2 ? " — דאבל!" : ""}! בחר כלי להזזה`;
    };

    $("bg-opp-turn").onclick = () => {
      const opp = getUserById(selectedOpponentId);
      const d1 = Math.floor(Math.random() * 6) + 1;
      const d2 = Math.floor(Math.random() * 6) + 1;
      $("bg-d1").textContent = d1;
      $("bg-d2").textContent = d2;
      const indigoIdx = bgPoints.findIndex((p) => p.color === "indigo" && p.count > 0);
      const targetIdx = Math.max(0, indigoIdx - d1);
      if (indigoIdx !== -1 && indigoIdx !== targetIdx && (!bgPoints[targetIdx].color || bgPoints[targetIdx].color === "indigo")) {
        bgPoints[indigoIdx].count--;
        if (bgPoints[indigoIdx].count === 0) bgPoints[indigoIdx].color = null;
        bgPoints[targetIdx].color = "indigo";
        bgPoints[targetIdx].count++;
      }
      $("bg-status").textContent = `🎲 ${opp.name} זרק/ה ${d1} ו-${d2} והזיז/ה כלי! תורך`;
      renderBackgammon();
    };

    $("bg-next-stage").onclick = () => {
      nextStage("backgammon", "bg-stage");
      $("bg-status").textContent = `התקדמת לשלב ${progress.backgammon.stage} בשש בש!`;
    };

    $("bg-reset").onclick = initBackgammon;
    initBackgammon();

    const initChess = [
      ["♜","♞","♝","♛","♚","♝","♞","♜"],
      ["♟","♟","♟","♟","♟","♟","♟","♟"],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["♙","♙","♙","♙","♙","♙","♙","♙"],
      ["♖","♘","♗","♕","♔","♗","♘","♖"]
    ];
    let cBoard = initChess.map((r) => [...r]);
    let cSel = null;

    function renderChess() {
      const el = $("chess-board");
      el.innerHTML = "";
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const cell = document.createElement("button");
          cell.type = "button";
          const isLight = (r + c) % 2 === 0;
          const isS = cSel && cSel.r === r && cSel.c === c;
          cell.className = `chess-cell ${isLight ? "chess-light" : "chess-dark"} ${isS ? "chess-selected" : ""}`;
          cell.textContent = cBoard[r][c];
          cell.onclick = () => {
            const opp = getUserById(selectedOpponentId);
            if (cSel) {
              if (cSel.r !== r || cSel.c !== c) {
                cBoard[r][c] = cBoard[cSel.r][cSel.c];
                cBoard[cSel.r][cSel.c] = "";
                for (let br = 0; br < 4; br++) {
                  for (let bc = 0; bc < 8; bc++) {
                    if (cBoard[br][bc] && br + 1 < 8 && !cBoard[br + 1][bc]) {
                      cBoard[br + 1][bc] = cBoard[br][bc];
                      cBoard[br][bc] = "";
                      $("chess-turn").textContent = `הזזת כלי • ${opp.name} הגיב/ה במהלך!`;
                      br = 4;
                      break;
                    }
                  }
                }
              }
              cSel = null;
              renderChess();
            } else if (cBoard[r][c]) {
              cSel = { r, c };
              renderChess();
            }
          };
          el.appendChild(cell);
        }
      }
    }
    $("chess-next-stage").onclick = () => {
      nextStage("chess", "chess-stage");
      $("chess-turn").textContent = `שלב ${progress.chess.stage} בשחמט!`;
    };
    $("chess-reset").onclick = () => { cBoard = initChess.map((r) => [...r]); cSel = null; renderChess(); };
    renderChess();

    const triviaList = [
      { q: "מה שובר קרח מעולה בדייט?", opts: ["משחק קליל וצחוק", "מבחן", "שתיקה", "ריב"], ans: 0 },
      { q: "איפה הכי כיף לשבת לשיחה?", opts: ["שולחן נעים או בית קפה", "מחסן", "כביש מהיר", "מקלט"], ans: 0 }
    ];
    let tIdx = 0;
    function renderTrivia() {
      const item = triviaList[tIdx % triviaList.length];
      $("trivia-q").textContent = item.q;
      $("trivia-options").innerHTML = "";
      item.opts.forEach((opt, i) => {
        const b = document.createElement("button");
        b.type = "button";
        b.className = "px-4 py-2.5 rounded-xl bg-slate-800 hover:bg-pink-600 text-sm";
        b.textContent = opt;
        b.onclick = () => {
          const opp = getUserById(selectedOpponentId);
          if (i === item.ans) {
            tIdx++;
            nextStage("trivia", "trivia-stage");
            $("trivia-feedback").textContent = `ענית נכון לפני ${opp.name}! שלב ${progress.trivia.stage}`;
            renderTrivia();
          } else {
            $("trivia-feedback").textContent = "נסה שוב!";
          }
        };
        $("trivia-options").appendChild(b);
      });
    }
    renderTrivia();

    const memPool = ["💜", "🎲", "🌹", "⚡"];
    let mCards = [], mOpen = [], mMatched = new Set();
    function initMem() {
      mCards = [...memPool, ...memPool].sort(() => Math.random() - 0.5);
      mOpen = [];
      mMatched = new Set();
      renderMem();
    }
    function renderMem() {
      $("memory-grid").innerHTML = "";
      mCards.forEach((sym, i) => {
        const b = document.createElement("button");
        b.type = "button";
        const open = mOpen.includes(i) || mMatched.has(i);
        b.className = `h-14 rounded-xl text-xl border ${open ? "bg-pink-600/40 border-pink-400" : "bg-slate-800 border-slate-700"}`;
        b.textContent = open ? sym : "❓";
        b.onclick = () => {
          if (open || mOpen.length === 2) return;
          mOpen.push(i);
          renderMem();
          if (mOpen.length === 2) {
            const [a, bIdx] = mOpen;
            if (mCards[a] === mCards[bIdx]) {
              mMatched.add(a); mMatched.add(bIdx); mOpen = [];
              if (mMatched.size === mCards.length) {
                nextStage("memory", "memory-stage");
                $("memory-status").textContent = `השלמת שלב! שלב נוכחי: ${progress.memory.stage}`;
                setTimeout(initMem, 600);
              }
              renderMem();
            } else {
              setTimeout(() => { mOpen = []; renderMem(); }, 550);
            }
          }
        };
        $("memory-grid").appendChild(b);
      });
    }
    $("memory-reset").onclick = initMem;
    initMem();

    let targetN = Math.floor(Math.random() * 10) + 1;
    function setupNum() {
      const max = progress.number.stage * 10;
      targetN = Math.floor(Math.random() * max) + 1;
      $("num-range").textContent = `נחש מספר בין 1 ל-${max}`;
    }
    $("num-check").onclick = () => {
      const g = Number($("num-input").value);
      if (!g) return;
      if (g === targetN) {
        nextStage("number", "num-stage");
        $("num-hint").textContent = `פגעת בול! שלב ${progress.number.stage}`;
        setupNum();
      } else {
        $("num-hint").textContent = g < targetN ? "גבוה יותר ⬆️" : "נמוך יותר ⬇️";
      }
    };
    setupNum();

    let ttt = Array(9).fill("");
    function renderTtt() {
      $("ttt-board").innerHTML = "";
      ttt.forEach((v, idx) => {
        const b = document.createElement("button");
        b.type = "button";
        b.className = "h-16 rounded-xl bg-slate-800 border border-slate-700 text-2xl font-bold";
        b.textContent = v;
        b.onclick = () => {
          const opp = getUserById(selectedOpponentId);
          if (v || winTtt(ttt)) return;
          ttt[idx] = "❌";
          if (winTtt(ttt) === "❌") {
            nextStage("ttt", "ttt-stage");
            $("ttt-status").textContent = `ניצחת את ${opp.name}! שלב ${progress.ttt.stage}`;
            renderTtt();
            return;
          }
          const free = ttt.map((x, i) => x === "" ? i : -1).filter((i) => i >= 0);
          if (free.length) {
            ttt[free[Math.floor(Math.random() * free.length)]] = "⭕";
            if (winTtt(ttt) === "⭕") $("ttt-status").textContent = `${opp.name} ניצח/ה בסיבוב!`;
          }
          renderTtt();
        };
        $("ttt-board").appendChild(b);
      });
    }
    function winTtt(c) {
      const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
      for (const [a,b,d] of lines) if (c[a] && c[a] === c[b] && c[a] === c[d]) return c[a];
      return null;
    }
    $("ttt-reset").onclick = () => { ttt = Array(9).fill(""); $("ttt-status").textContent = "אתה ❌ מול היריב ⭕"; renderTtt(); };
    renderTtt();

    $("rom-prompt").textContent = "כתוב משפט פתיחה שנון ליריב/ה והתקדם לשלב הבא!";
    $("rom-submit").onclick = () => {
      const val = $("rom-input").value.trim();
      if (!val) return;
      const opp = getUserById(selectedOpponentId);
      nextStage("romance", "rom-stage");
      $("rom-input").value = "";
      $("rom-feedback").textContent = `המשפט נשלח ל-${opp.name}! שלב ${progress.romance.stage}`;
    };

    let clicks = 0;
    function refreshTapLabel() {
      const goal = progress.tap.stage * 10;
      $("tap-goal").textContent = `הגע ל-${goal} לחיצות כדי לעלות שלב!`;
      $("tap-counter").textContent = `לחיצות: ${clicks} / ${goal}`;
    }
    $("tap-btn").onclick = () => {
      clicks++;
      const goal = progress.tap.stage * 10;
      if (clicks >= goal) {
        clicks = 0;
        nextStage("tap", "tap-stage");
      }
      refreshTapLabel();
    };
    refreshTapLabel();
  </script>
</body>
</html>
