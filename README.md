<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove IL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { background: linear-gradient(135deg, #0f172a, #1e1b4b, #311042); min-height: 100vh; font-family: system-ui, sans-serif; }
    .glass { background: rgba(30, 41, 59, 0.78); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.12); }
    .chess-board { display: grid; grid-template-columns: repeat(8, minmax(0, 1fr)); border: 2px solid #f472b6; border-radius: 12px; overflow: hidden; }
    .chess-cell { aspect-ratio: 1 / 1; display: flex; align-items: center; justify-content: center; font-size: clamp(1.1rem, 3vw, 1.8rem); cursor: pointer; user-select: none; }
    .chess-light { background: #e2e8f0; color: #0f172a; }
    .chess-dark { background: #475569; color: #ffffff; }
    .chess-selected { outline: 3px solid #ec4899; outline-offset: -3px; background: #fbcfe8 !important; color: #0f172a !important; }
  </style>
</head>
<body class="text-white antialiased">
  <header class="glass sticky top-0 z-50 px-6 py-4 flex items-center justify-between shadow-lg">
    <div class="flex items-center gap-2">
      <span class="text-2xl">💜</span>
      <h1 class="text-xl font-bold bg-gradient-to-l from-pink-400 to-indigo-400 bg-clip-text text-transparent">TopLove IL</h1>
    </div>
    <div class="flex items-center gap-3">
      <span id="user-badge" class="hidden text-sm text-slate-300 bg-slate-800 px-3 py-1 rounded-full"></span>
      <button id="logout-btn" type="button" class="hidden bg-rose-600 hover:bg-rose-500 text-sm px-4 py-1.5 rounded-lg">התנתק</button>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 py-8">
    <section id="auth-section" class="max-w-md mx-auto glass rounded-2xl p-8 shadow-2xl mt-8">
      <h2 id="auth-title" class="text-2xl font-bold text-center mb-2">ברוכים הבאים ל-TopLove IL</h2>
      <p class="text-slate-300 text-sm text-center mb-6">התחברו או צרו חשבון אישי מאובטח</p>
      <form id="auth-form" class="space-y-4">
        <input type="email" id="auth-email" required placeholder="אימייל" dir="ltr" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700 text-left" />
        <div class="relative">
          <input type="password" id="auth-password" required minlength="6" placeholder="סיסמה (מינימום 6 תווים)" dir="ltr" class="w-full px-4 py-2.5 pl-11 rounded-xl bg-slate-900 border border-slate-700 text-left" />
          <button type="button" id="toggle-password-btn" aria-label="הצג או הסתר סיסמה" class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 hover:text-white transition-colors">
            <svg id="eye-open" class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
              <circle cx="12" cy="12" r="3"></circle>
            </svg>
            <svg id="eye-closed" class="w-5 h-5 hidden" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19m-6.72-1.07a3 3 0 1 1-4.24-4.24"></path>
              <line x1="1" y1="1" x2="23" y2="23"></line>
            </svg>
          </button>
        </div>
        <p id="auth-error" class="hidden text-rose-400 text-sm text-center"></p>
        <button type="submit" id="auth-submit-btn" class="w-full py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">התחברות</button>
      </form>
      <div class="mt-5 text-center text-sm text-slate-300">
        <span id="auth-toggle-text">אין לך חשבון?</span>
        <button type="button" id="auth-toggle-btn" class="text-pink-400 hover:underline font-medium mr-1">הירשם עכשיו</button>
      </div>
    </section>

    <section id="app-section" class="hidden space-y-8">
      <div class="flex flex-wrap gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-5 py-2 rounded-xl font-medium bg-pink-600 text-white">הפרופיל שלי</button>
        <button type="button" data-tab="discover" class="tab-btn px-5 py-2 rounded-xl font-medium glass text-slate-300">פרופילים ומעקב</button>
        <button type="button" data-tab="games" class="tab-btn px-5 py-2 rounded-xl font-medium glass text-slate-300">עמודת משחקים 🎮</button>
      </div>

      <div id="tab-profile" class="tab-content max-w-2xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="flex flex-col sm:flex-row items-center gap-4 bg-slate-900/70 p-4 rounded-xl border border-slate-700/70">
            <img id="prof-avatar-preview" src="https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove" alt="תמונת פרופיל" class="w-20 h-20 rounded-full object-cover border-2 border-pink-500 bg-slate-800 shrink-0" />
            <div class="w-full space-y-2">
              <label class="block text-sm font-medium text-pink-300">תמונת פרופיל (העלאה או קישור)</label>
              <input type="file" id="prof-avatar-file" accept="image/*" class="block w-full text-xs text-slate-300 file:mr-0 file:ml-3 file:py-1.5 file:px-3 file:rounded-lg file:border-0 file:bg-pink-600 file:text-white hover:file:bg-pink-500" />
              <input type="url" id="prof-avatar-url" placeholder="או הדבק קישור ישיר לתמונה (https://...)" dir="ltr" class="w-full px-3 py-1.5 text-sm rounded-lg bg-slate-950 border border-slate-700 text-left" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-name" required placeholder="שם / כינוי" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="number" id="prof-age" min="18" max="99" required placeholder="גיל" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <input type="text" id="prof-city" required placeholder="עיר" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <select id="prof-status" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">
              <option value="זמין/ה להיכרות 💜">זמין/ה להיכרות 💜</option>
              <option value="מחפש/ת קשר רציני 💍">מחפש/ת קשר רציני 💍</option>
              <option value="פתוח/ה למשחקים 🎲">פתוח/ה למשחקים 🎲</option>
              <option value="לא פנוי/ה כרגע 🌙">לא פנוי/ה כרגע 🌙</option>
            </select>
          </div>
          <textarea id="prof-bio" rows="3" placeholder="קצת עליי, מה מחפש/ת ומה אוהב/ת..." class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700"></textarea>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר בהצלחה!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">שמור פרופיל</button>
          </div>
        </form>
      </div>

      <div id="tab-discover" class="tab-content hidden space-y-4">
        <div class="flex flex-wrap justify-between items-center gap-2">
          <h2 class="text-xl font-bold">קהילת TopLove IL</h2>
          <div class="flex items-center gap-2">
            <span id="following-count" class="text-sm bg-pink-600/30 border border-pink-500/40 text-pink-200 px-3 py-1 rounded-full">עוקב אחרי: 0</span>
            <span id="users-count" class="text-sm glass px-3 py-1 rounded-full">טוען...</span>
          </div><div id="tab-games" class="tab-content hidden space-y-6">
        <div class="text-center">
          <h2 class="text-2xl font-bold mb-2">🎮 עמודת המשחקים של TopLove</h2>
          <p class="text-slate-300 text-sm">בחר משחק מתוך העמודות שלמטה ושחק בכיף</p>
        </div>

        <div class="flex flex-wrap gap-2 justify-center">
          <button type="button" data-game="rps" class="game-tab-btn px-4 py-2 rounded-xl text-sm font-semibold bg-pink-600 text-white">✂️ אבן נייר ומספריים</button>
          <button type="button" data-game="tod" class="game-tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">🔥 אמת או חובה</button>
          <button type="button" data-game="chess" class="game-tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">♟️ שחמט</button>
          <button type="button" data-game="backgammon" class="game-tab-btn px-4 py-2 rounded-xl text-sm font-semibold glass text-slate-300">🎲 שש בש</button>
        </div>

        <div id="game-rps" class="game-panel max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-5">
          <h3 class="text-xl font-bold">✂️ אבן נייר ומספריים</h3>
          <div class="flex justify-around text-sm bg-slate-900/80 py-2.5 px-4 rounded-xl border border-slate-700">
            <span>ניצחונות שלך: <strong id="rps-wins" class="text-emerald-400">0</strong></span>
            <span>תיקו: <strong id="rps-draws" class="text-amber-300">0</strong></span>
            <span>הפסדים: <strong id="rps-losses" class="text-rose-400">0</strong></span>
          </div>
          <div class="flex justify-center gap-3">
            <button type="button" data-rps="rock" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">🪨 אבן</button>
            <button type="button" data-rps="paper" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">📄 נייר</button>
            <button type="button" data-rps="scissors" class="rps-choice px-5 py-3 rounded-xl bg-slate-800 hover:bg-pink-600 transition text-lg">✂️ מספריים</button>
          </div>
          <p id="rps-result" class="text-base font-medium text-pink-200 min-h-[2rem]">בחר מהלך כדי להתחיל!</p>
        </div>

        <div id="game-tod" class="game-panel hidden max-w-xl mx-auto glass rounded-2xl p-6 text-center space-y-5">
          <h3 class="text-xl font-bold">🔥 אמת או חובה לדייטים והיכרות</h3>
          <div class="flex justify-center gap-3">
            <button type="button" id="btn-truth" class="px-6 py-2.5 rounded-xl font-semibold bg-indigo-600 hover:bg-indigo-500">אמת 💭</button>
            <button type="button" id="btn-dare" class="px-6 py-2.5 rounded-xl font-semibold bg-pink-600 hover:bg-pink-500">חובה ⚡</button>
          </div>
          <div class="bg-slate-900 border border-slate-700 rounded-2xl p-6 min-h-[110px] flex items-center justify-center">
            <p id="tod-text" class="text-lg text-pink-200">לחץ על "אמת" או "חובה" לקבלת משימה!</p>
          </div>
        </div>

        <div id="game-chess" class="game-panel hidden max-w-lg mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex items-center justify-between">
            <h3 class="text-xl font-bold">♟️ שחמט</h3>
            <button type="button" id="chess-reset" class="text-xs bg-slate-800 hover:bg-slate-700 px-3 py-1.5 rounded-lg border border-slate-600">אפס לוח</button>
          </div>
          <p id="chess-turn" class="text-sm text-pink-200">תור: לבן — לחץ על כלי ואז על משבצת יעד</p>
          <div id="chess-board" class="chess-board"></div>
        </div>

        <div id="game-backgammon" class="game-panel hidden max-w-2xl mx-auto glass rounded-2xl p-6 text-center space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <h3 class="text-xl font-bold">🎲 שש בש</h3>
            <div class="flex items-center gap-2">
              <button type="button" id="bg-roll" class="px-4 py-1.5 rounded-xl text-sm font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">הטל קוביות 🎲</button>
              <button type="button" id="bg-reset" class="text-xs bg-slate-800 hover:bg-slate-700 px-3 py-1.5 rounded-lg border border-slate-600">איפוס</button>
            </div>
          </div>
          <p id="bg-dice-info" class="text-sm text-amber-300 font-medium">קוביות: לחץ "הטל קוביות" • לחץ על נקודה עם כלים ואז על נקודת יעד</p>
          <div id="bg-board" class="grid grid-cols-6 sm:grid-cols-12 gap-1.5 bg-amber-950/70 p-3 rounded-2xl border border-amber-700/50"></div>
        </div>
      </div>
    </section>
  </main><script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-app.js";
    import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-auth.js";
    import { getFirestore, doc, setDoc, getDoc, collection, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/11.0.2/firebase-firestore.js";

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
    const auth = getAuth(app);
    const db = getFirestore(app);

    const DEFAULT_AVATAR = "https://api.dicebear.com/9.x/avataaars/svg?seed=TopLove";
    let isSignUp = false, currentUser = null, unsubUsers = null;
    let currentAvatarData = DEFAULT_AVATAR;
    let followingSet = new Set();
    let allUsersDocs = [];

    const $ = (id) => document.getElementById(id);

    function escapeHtml(str) {
      return String(str || "")
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;");
    }

    $("toggle-password-btn").onclick = () => {
      const input = $("auth-password");
      const show = input.type === "password";
      input.type = show ? "text" : "password";
      $("eye-open").classList.toggle("hidden", show);
      $("eye-closed").classList.toggle("hidden", !show);
    };

    $("auth-toggle-btn").onclick = () => {
      isSignUp = !isSignUp;
      $("auth-title").textContent = isSignUp ? "יצירת חשבון חדש" : "ברוכים הבאים ל-TopLove IL";
      $("auth-submit-btn").textContent = isSignUp ? "הרשמה" : "התחברות";
      $("auth-toggle-text").textContent = isSignUp ? "כבר רשום?" : "אין לך חשבון?";
      $("auth-toggle-btn").textContent = isSignUp ? "התחבר" : "הירשם עכשיו";
      $("auth-error").classList.add("hidden");
    };

    $("auth-form").onsubmit = async (e) => {
      e.preventDefault();
      $("auth-error").classList.add("hidden");
      const email = $("auth-email").value.trim(), pass = $("auth-password").value;
      try {
        if (isSignUp) {
          await createUserWithEmailAndPassword(auth, email, pass);
        } else {
          await signInWithEmailAndPassword(auth, email, pass);
        }
      } catch (err) {
        $("auth-error").textContent = "שגיאה: " + err.message;
        $("auth-error").classList.remove("hidden");
      }
    };

    $("logout-btn").onclick = () => signOut(auth);

    $("prof-avatar-file").onchange = (e) => {
      const file = e.target.files?.[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => {
        currentAvatarData = String(reader.result);
        $("prof-avatar-preview").src = currentAvatarData;
        $("prof-avatar-url").value = "";
      };
      reader.readAsDataURL(file);
    };

    $("prof-avatar-url").oninput = (e) => {
      const url = e.target.value.trim();
      currentAvatarData = url || DEFAULT_AVATAR;
      $("prof-avatar-preview").src = currentAvatarData;
    };

    function renderProfilesGrid() {
      if (!currentUser) return;
      $("users-count").textContent = `${allUsersDocs.length} פרופילים`;
      $("following-count").textContent = `עוקב אחרי: ${followingSet.size}`;
      $("profiles-grid").innerHTML = "";

      allUsersDocs.forEach(({ id, data: u }) => {
        const targetUid = u.uid || id;
        const isMe = targetUid === currentUser.uid;
        const isFollowing = followingSet.has(targetUid);
        const followersCount = Array.isArray(u.followers) ? u.followers.length : 0;
        const safeAvatar = escapeHtml(u.avatar || DEFAULT_AVATAR);

        const div = document.createElement("div");
        div.className = "glass rounded-2xl p-4 shadow-lg flex flex-col justify-between gap-3";
        div.innerHTML = `
          <div>
            <div class="flex items-center justify-between gap-2 mb-2">
              <div class="flex items-center gap-3">
                <img src="${safeAvatar}" alt="${escapeHtml(u.name || "משתמש")}" class="w-12 h-12 rounded-full object-cover border border-pink-400/60 bg-slate-800 shrink-0" />
                <div>
                  <h3 class="font-bold leading-tight">${escapeHtml(u.name || "משתמש")}, ${escapeHtml(u.age || "")}</h3>
                  <p class="text-xs text-indigo-300">📍 ${escapeHtml(u.city || "ישראל")}</p>
                </div>
              </div>
              ${isMe ? '<span class="text-xs bg-pink-600 px-2.5 py-1 rounded-full">את/ה</span>' : ""}
            </div>
            <span class="inline-block text-xs bg-slate-900 text-pink-300 px-2.5 py-1 rounded-full mb-2">${escapeHtml(u.status || "")}</span>
            <p class="text-sm text-slate-300">${escapeHtml(u.bio || "אין תיאור עדיין")}</p>
          </div>
          <div class="flex items-center justify-between pt-2 border-t border-white/10">
            <span class="text-xs text-slate-400">עוקבים: <strong class="text-white">${followersCount}</strong></span>
            ${!isMe ? `<button type="button" data-follow-uid="${escapeHtml(targetUid)}" class="follow-btn text-xs px-3.5 py-1.5 rounded-xl font-semibold transition ${isFollowing ? "bg-emerald-600 hover:bg-emerald-500 text-white" : "bg-pink-600 hover:bg-pink-500 text-white"}">${isFollowing ? "עוקב ✓" : "+ עקוב"}</button>` : ""}
          </div>
        `;
        $("profiles-grid").appendChild(div);
      });

      document.querySelectorAll(".follow-btn").forEach((btn) => {
        btn.onclick = async () => {
          const targetUid = btn.dataset.followUid;
          if (!currentUser || !targetUid) return;
          const nowFollowing = !followingSet.has(targetUid);
          if (nowFollowing) followingSet.add(targetUid);
          else followingSet.delete(targetUid);

          const updatedFollowing = Array.from(followingSet);
          await setDoc(doc(db, "users", currentUser.uid), { following: updatedFollowing }, { merge: true });

          const targetDoc = allUsersDocs.find((x) => (x.data.uid || x.id) === targetUid);
          const currentFollowers = new Set(Array.isArray(targetDoc?.data?.followers) ? targetDoc.data.followers : []);
          if (nowFollowing) currentFollowers.add(currentUser.uid);
          else currentFollowers.delete(currentUser.uid);

          await setDoc(doc(db, "users", targetUid), { followers: Array.from(currentFollowers) }, { merge: true });
          renderProfilesGrid();
        };
      });
    }

    onAuthStateChanged(auth, async (user) => {
      currentUser = user;
      $("auth-section").classList.toggle("hidden", !!user);
      $("app-section").classList.toggle("hidden", !user);
      $("user-badge").classList.toggle("hidden", !user);
      $("logout-btn").classList.toggle("hidden", !user);

      if (unsubUsers) {
        unsubUsers();
        unsubUsers = null;
      }

      if (user) {
        $("user-badge").textContent = user.email;
        try {
          const snap = await getDoc(doc(db, "users", user.uid));
          if (snap.exists()) {
            const d = snap.data();
            $("prof-name").value = d.name || "";
            $("prof-age").value = d.age || "";
            $("prof-city").value = d.city || "";
            $("prof-status").value = d.status || "זמין/ה להיכרות 💜";
            $("prof-bio").value = d.bio || "";
            currentAvatarData = d.avatar || DEFAULT_AVATAR;
            $("prof-avatar-preview").src = currentAvatarData;
            if (d.avatar && !d.avatar.startsWith("data:")) {
              $("prof-avatar-url").value = d.avatar;
            }
            followingSet = new Set(Array.isArray(d.following) ? d.following : []);
          }
        } catch (err) {
          console.error("שגיאה בטעינת פרופיל:", err);
        }

        unsubUsers = onSnapshot(
          collection(db, "users"),
          (snap) => {
            allUsersDocs = [];
            snap.forEach((docSnap) => {
              const data = docSnap.data();
              if ((data.uid || docSnap.id) === user.uid && Array.isArray(data.following)) {
                followingSet = new Set(data.following);
              }
              allUsersDocs.push({ id: docSnap.id, data });
            });
            renderProfilesGrid();
          },
          (err) => console.error("שגיאה בהאזנה לפרופילים:", err)
        );
      }
    });

    $("profile-form").onsubmit = async (e) => {
      e.preventDefault();
      if (!currentUser) return;
      await setDoc(doc(db, "users", currentUser.uid), {
        uid: currentUser.uid,
        name: $("prof-name").value.trim(),
        age: Number($("prof-age").value),
        city: $("prof-city").value.trim(),
        status: $("prof-status").value,
        bio: $("prof-bio").value.trim(),
        avatar: currentAvatarData || DEFAULT_AVATAR,
        following: Array.from(followingSet),
        updatedAt: serverTimestamp()
      }, { merge: true });
      $("save-feedback").classList.remove("opacity-0");
      setTimeout(() => $("save-feedback").classList.add("opacity-0"), 2000);
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

    document.querySelectorAll(".game-tab-btn").forEach((btn) => {
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

    let wins = 0, draws = 0, losses = 0;
    const rpsLabels = { rock: "🪨 אבן", paper: "📄 נייר", scissors: "✂️ מספריים" };
    document.querySelectorAll(".rps-choice").forEach((btn) => {
      btn.onclick = () => {
        const player = btn.dataset.rps;
        const choices = ["rock", "paper", "scissors"];
        const bot = choices[Math.floor(Math.random() * choices.length)];
        if (player === bot) {
          draws++;
          $("rps-result").textContent = `תיקו! שניכם בחרתם ${rpsLabels[player]}`;
        } else if (
          (player === "rock" && bot === "scissors") ||
          (player === "paper" && bot === "rock") ||
          (player === "scissors" && bot === "paper")
        ) {
          wins++;
          $("rps-result").textContent = `ניצחת! ${rpsLabels[player]} מנצח ${rpsLabels[bot]}`;
        } else {
          losses++;
          $("rps-result").textContent = `הפסדת! ${rpsLabels[bot]} מנצח ${rpsLabels[player]}`;
        }
        $("rps-wins").textContent = wins;
        $("rps-draws").textContent = draws;
        $("rps-losses").textContent = losses;
      };
    });

    const truths = [
      "מה הדייט הכי בלתי נשכח שהיה לך?",
      "מה הדבר הראשון שאתה שם לב אליו בבן/בת זוג?",
      "מה הסוד הכי מצחיק שלך?"
    ];
    const dares = [
      "שלח הודעת פתיחה מצחיקה למישהו שמעניין אותך.",
      "ספר בדיחה גרועה במיוחד ב-10 שניות.",
      "בחר שיר שמתאר את המצב רוח שלך עכשיו."
    ];
    $("btn-truth").onclick = () => {
      $("tod-text").textContent = "💭 אמת: " + truths[Math.floor(Math.random() * truths.length)];
    };
    $("btn-dare").onclick = () => {
      $("tod-text").textContent = "⚡ חובה: " + dares[Math.floor(Math.random() * dares.length)];
    };

    const initialChess = [
      ["♜","♞","♝","♛","♚","♝","♞","♜"],
      ["♟","♟","♟","♟","♟","♟","♟","♟"],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["","","","","","","",""],
      ["♙","♙","♙","♙","♙","♙","♙","♙"],
      ["♖","♘","♗","♕","♔","♗","♘","♖"]
    ];
    let chessBoard = initialChess.map((r) => [...r]);
    let selectedChess = null;
    let whiteTurn = true;

    function renderChess() {
      const el = $("chess-board");
      el.innerHTML = "";
      for (let r = 0; r < 8; r++) {
        for (let c = 0; c < 8; c++) {
          const cell = document.createElement("button");
          cell.type = "button";
          const isLight = (r + c) % 2 === 0;
          const isSel = selectedChess && selectedChess.r === r && selectedChess.c === c;
          cell.className = `chess-cell ${isLight ? "chess-light" : "chess-dark"} ${isSel ? "chess-selected" : ""}`;
          cell.textContent = chessBoard[r][c];
          cell.onclick = () => {
            if (selectedChess) {
              if (selectedChess.r !== r || selectedChess.c !== c) {
                chessBoard[r][c] = chessBoard[selectedChess.r][selectedChess.c];
                chessBoard[selectedChess.r][selectedChess.c] = "";
                whiteTurn = !whiteTurn;
              }
              selectedChess = null;
              $("chess-turn").textContent = `תור: ${whiteTurn ? "לבן" : "שחור"} — לחץ על כלי ואז על משבצת יעד`;
              renderChess();
            } else if (chessBoard[r][c]) {
              selectedChess = { r, c };
              renderChess();
            }
          };
          el.appendChild(cell);
        }
      }
    }
    $("chess-reset").onclick = () => {
      chessBoard = initialChess.map((r) => [...r]);
      selectedChess = null;
      whiteTurn = true;
      $("chess-turn").textContent = "תור: לבן — לחץ על כלי ואז על משבצת יעד";
      renderChess();
    };
    renderChess();

    let bgPoints = Array(12).fill(null).map(() => ({ color: null, count: 0 }));
    let bgSelected = null;

    function initBackgammon() {
      bgPoints = Array(12).fill(null).map(() => ({ color: null, count: 0 }));
      bgPoints[0] = { color: "pink", count: 3 };
      bgPoints[5] = { color: "indigo", count: 3 };
      bgPoints[6] = { color: "pink", count: 3 };
      bgPoints[11] = { color: "indigo", count: 3 };
      bgSelected = null;
      renderBackgammon();
    }

    function renderBackgammon() {
      const board = $("bg-board");
      board.innerHTML = "";
      bgPoints.forEach((pt, idx) => {
        const col = document.createElement("button");
        col.type = "button";
        const isSel = bgSelected === idx;
        col.className = `min-h-[120px] rounded-xl p-1.5 flex flex-col items-center justify-between border ${isSel ? "border-pink-400 bg-amber-900" : "border-amber-800/70 bg-amber-950/80"}`;
        col.innerHTML = `<span class="text-[11px] text-amber-200/70">#${idx + 1}</span>
          <div class="flex flex-col items-center gap-1 my-auto">
            ${Array.from({ length: pt.count }).map(() => `<span class="w-6 h-6 rounded-full flex items-center justify-center text-xs font-bold shadow ${pt.color === "pink" ? "bg-pink-500 text-white" : "bg-indigo-500 text-white"}">${pt.color === "pink" ? "●" : "◆"}</span>`).join("")}
          </div>
          <span class="text-xs text-slate-300">${pt.count || ""}</span>`;
        col.onclick = () => {
          if (bgSelected === null) {
            if (pt.count > 0) {
              bgSelected = idx;
              renderBackgammon();
            }
          } else {
            if (bgSelected !== idx) {
              const from = bgPoints[bgSelected];
              if (from.count > 0 && (!pt.color || pt.color === from.color || pt.count === 0)) {
                from.count--;
                const moverColor = from.color;
                if (from.count === 0) from.color = null;
                pt.color = moverColor;
                pt.count++;
              }
            }
            bgSelected = null;
            renderBackgammon();
          }
        };
        board.appendChild(col);
      });
    }

    $("bg-roll").onclick = () => {
      const d1 = Math.floor(Math.random() * 6) + 1;
      const d2 = Math.floor(Math.random() * 6) + 1;
      $("bg-dice-info").textContent = `קוביות: ${d1} ו-${d2} ${d1 === d2 ? "(דאבל! 🎉)" : ""} • בחר נקודה להזזת כלי`;
    };
    $("bg-reset").onclick = initBackgammon;
    initBackgammon();
  </script>
</body>
</html>
        </div>
        <div id="profiles-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div>
