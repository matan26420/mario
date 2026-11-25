<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>TopLove IL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { background: linear-gradient(135deg, #0f172a, #1e1b4b, #311042); min-height: 100vh; font-family: system-ui, sans-serif; }
    .glass { background: rgba(30, 41, 59, 0.75); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.12); }
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

  <main class="max-w-5xl mx-auto px-4 py-8">
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
      <div class="flex gap-2 justify-center">
        <button type="button" data-tab="profile" class="tab-btn px-5 py-2 rounded-xl font-medium bg-pink-600 text-white">הפרופיל שלי</button>
        <button type="button" data-tab="discover" class="tab-btn px-5 py-2 rounded-xl font-medium glass text-slate-300">פרופילים</button>
        <button type="button" data-tab="game" class="tab-btn px-5 py-2 rounded-xl font-medium glass text-slate-300">משחק היכרות</button>
      </div>

      <div id="tab-profile" class="tab-content max-w-xl mx-auto glass rounded-2xl p-6 shadow-xl">
        <h2 class="text-xl font-bold mb-4">הפרופיל האישי שלי</h2>
        <form id="profile-form" class="space-y-4">
          <div class="grid grid-cols-2 gap-3">
            <input type="text" id="prof-name" required placeholder="שם / כינוי" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <input type="number" id="prof-age" min="18" max="99" required placeholder="גיל" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
          </div>
          <div class="grid grid-cols-2 gap-3">
            <input type="text" id="prof-city" required placeholder="עיר" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700" />
            <select id="prof-status" class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700">
              <option value="זמין/ה להיכרות 💜">זמין/ה להיכרות 💜</option>
              <option value="מחפש/ת קשר רציני 💍">מחפש/ת קשר רציני 💍</option>
              <option value="פתוח/ה למשחקים 🎲">פתוח/ה למשחקים 🎲</option>
              <option value="לא פנוי/ה כרגע 🌙">לא פנוי/ה כרגע 🌙</option>
            </select>
          </div>
          <textarea id="prof-bio" rows="3" placeholder="קצת עליי..." class="w-full px-4 py-2.5 rounded-xl bg-slate-900 border border-slate-700"></textarea>
          <div class="flex items-center justify-between">
            <span id="save-feedback" class="text-emerald-400 text-sm opacity-0 transition-opacity">✓ נשמר בהצלחה!</span>
            <button type="submit" class="px-6 py-2.5 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">שמור פרופיל</button>
          </div>
        </form>
      </div>

      <div id="tab-discover" class="tab-content hidden">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-bold">משתמשים פעילים</h2>
          <span id="users-count" class="text-sm glass px-3 py-1 rounded-full">טוען...</span>
        </div>
        <div id="profiles-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </div>

      <div id="tab-game" class="tab-content hidden max-w-xl mx-auto glass rounded-2xl p-8 text-center">
        <h2 class="text-2xl font-bold mb-4">🎲 שובר הקרח של TopLove</h2>
        <div class="bg-slate-900 border border-slate-700 rounded-2xl p-6 mb-6">
          <p id="game-question" class="text-lg text-pink-200">לחצו על הכפתור לקבלת שאלה!</p>
        </div>
        <button type="button" id="next-question-btn" class="px-8 py-3 rounded-xl font-semibold bg-gradient-to-l from-pink-600 to-indigo-600">שאלה חדשה ✨</button>
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

    let isSignUp = false, currentUser = null, unsubUsers = null;
    const $ = (id) => document.getElementById(id);

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
          }
        } catch (err) {
          console.error("שגיאה בטעינת פרופיל:", err);
        }

        unsubUsers = onSnapshot(
          collection(db, "users"),
          (snap) => {
            $("users-count").textContent = `${snap.size} פרופילים`;
            $("profiles-grid").innerHTML = "";
            snap.forEach((docSnap) => {
              const u = docSnap.data();
              const isMe = (u.uid || docSnap.id) === user.uid;
              const div = document.createElement("div");
              div.className = "glass rounded-2xl p-4 shadow-lg";
              div.innerHTML = `<div class="flex justify-between mb-1"><h3 class="font-bold">${u.name || "משתמש"}, ${u.age || ""}</h3>${isMe ? '<span class="text-xs bg-pink-600 px-2 py-0.5 rounded-full">את/ה</span>' : ""}</div>
                <p class="text-xs text-indigo-300 mb-2">📍 ${u.city || ""}</p>
                <span class="text-xs bg-slate-900 text-pink-300 px-2.5 py-1 rounded-full">${u.status || ""}</span>
                <p class="text-sm text-slate-300 mt-2">${u.bio || ""}</p>`;
              $("profiles-grid").appendChild(div);
            });
          },
          (err) => {
            console.error("שגיאה בהאזנה לפרופילים:", err);
          }
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

    const questions = ["מה הדייט המושלם בעיניך?", "לאן היית טס מחר בבוקר?", "מה הדבר הכי ספונטני שעשית?", "איזו תכונה הכי מושכת אותך?"];
    $("next-question-btn").onclick = () => {
      $("game-question").textContent = questions[Math.floor(Math.random() * questions.length)];
    };
  </script>
</body>
</html>
