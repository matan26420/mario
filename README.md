>M.R הכול השירותים לבית
<html lang="he" dir="rtl">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>M.R הכול השירותים לבית</title>
  <style>
    .mr-title {
      font-size: 3rem;
      font-weight: 800;
      text-align: center;
      margin: 20px 0;
      background: linear-gradient(90deg, #ff512f, #dd2476, #00c6ff);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
  </style>
</head>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.R. הכל לבית</title>
    <meta name="description" content="M.R. הכל לבית – אינסטלציה, חשמל, צבע, שיפוצים, הובלות וניקיון מקרית שמונה ועד באר שבע. Услуги по дому от Кирьят-Шмоны до Беэр-Шевы.">

    <meta property="og:title" content="M.R. הכל לבית – שיפוצים, אינסטלציה, חשמל והובלות">
    <meta property="og:description" content="שירות מקיף, מקצועי ומהיר מקרית שמונה ועד באר שבע">
    <meta property="og:type" content="website">
    <meta name="theme-color" content="#007bff">

    <!-- נתונים מובנים לגוגל -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "HomeAndConstructionBusiness",
      "name": "M.R. הכל לבית",
      "alternateName": "M.R. Всё для дома",
      "description": "אינסטלציה, חשמל, צבע, חידוש רהיטים, ניקיון, הריסות, שיפוצים, גבס והובלות מקרית שמונה ועד באר שבע",
      "telephone": "+972559423309",
      "areaServed": ["קריית שמונה", "באר שבע", "ישראל"],
      "openingHoursSpecification": [
        {"@type": "OpeningHoursSpecification", "dayOfWeek": ["Sunday","Monday","Tuesday","Wednesday","Thursday"], "opens": "08:00", "closes": "20:00"},
        {"@type": "OpeningHoursSpecification", "dayOfWeek": "Friday", "opens": "09:00", "closes": "14:00"}
      ],
      "hasMap": "https://www.google.com/maps?cid=16449588355030326794",
      "sameAs": ["https://www.instagram.com/m.r26420", "https://www.tiktok.com/@m.r26420", "https://www.b144.co.il/b144_sip/401D0D1A4370655D4011001240/"]
    }
    </script>

    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(rgba(0, 0, 0, 0.4), rgba(0, 0, 0, 0.4)),
                        url('21215792-729b-4a30-ac73-18f9a904b58c.jpg') no-repeat center center fixed;
            background-size: cover;
            color: #333;
            margin: 0;
            padding: 20px;
            text-align: center;
            min-height: 100vh;
        }
        .container {
            max-width: 650px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            backdrop-filter: blur(5px);
        }
        .lang-switch { display: flex; justify-content: center; gap: 8px; margin-bottom: 15px; direction: ltr; }
        .lang-switch button {
            border: 2px solid #007bff; background: #fff; color: #007bff; padding: 6px 18px;
            border-radius: 20px; font-weight: bold; cursor: pointer; font-size: 14px;
        }
        .lang-switch button.on { background: #007bff; color: #fff; }
        .top-brand-bar {
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            gap: 25px; margin-bottom: 30px;
        }
        .business-card-section {
            background: #ffffff; padding: 10px; border-radius: 12px; width: 100%;
            max-width: 520px; box-sizing: border-box; display: flex; justify-content: center;
            align-items: center; box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }
        .brand-character-img {
            width: 100%; height: auto; aspect-ratio: 1 / 1; object-fit: cover;
            border-radius: 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        .brand-logo-img {
            width: 260px; height: 260px; border-radius: 12px; object-fit: cover;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        h1 { margin: 10px 0 5px 0; color: #222; font-size: 30px; font-weight: bold; }
        h2 { color: #007bff; margin-top: 25px; }
        .services-grid, .moves-grid {
            display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px;
        }
        a.btn {
            display: block; background: #007bff; color: white; padding: 12px;
            text-decoration: none; border-radius: 6px; font-weight: bold; transition: background 0.3s;
        }
        a.btn:hover { background: #0056b3; }
        .info-box { background: #f4f8ff; border-radius: 8px; padding: 12px 15px; line-height: 1.8; margin-bottom: 20px; }
        .info-box .row { display: flex; justify-content: space-between; border-bottom: 1px dashed #ccd; padding: 3px 0; }
        .info-box .row:last-child { border: 0; }
        .emergency-box {
            border: 2px solid #dc3545; background: #fff5f5; border-radius: 10px;
            padding: 16px; margin-bottom: 20px; text-align: right; line-height: 1.7;
        }
        html[dir="ltr"] .emergency-box { text-align: left; }
        .emergency-box h3 { margin: 0 0 8px; color: #b01e2c; font-size: 18px; }
        .emergency-tips { margin: 8px 0 14px; padding-inline-start: 20px; color: #444; }
        .faq details { background: #fff; border: 1px solid #e3e3e3; border-radius: 8px; padding: 10px 14px; margin-bottom: 8px; text-align: right; }
        html[dir="ltr"] .faq details { text-align: left; }
        .faq summary { font-weight: bold; cursor: pointer; color: #222; }
        .faq p, .faq ul { margin: 8px 0 0; color: #555; line-height: 1.7; }
        .faq ul { padding-inline-start: 20px; }
        .social-links { display: flex; flex-direction: column; align-items: center; gap: 15px; margin: 25px 0; }
        .social-btns-row { display: flex; justify-content: center; gap: 12px; flex-wrap: wrap; }
        .social-btn {
            display: inline-flex; align-items: center; gap: 8px; padding: 10px 18px;
            border-radius: 6px; color: white; text-decoration: none; font-weight: bold;
            font-size: 14px; box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .instagram-btn { background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); }
        .tiktok-btn { background: #000000; }
        .whatsapp-btn { background: #25d366; }
        .call-btn { background: #222222; }
        .emergency-wa-btn { background: #dc3545; }
        .signature-container {
            display: flex; align-items: center; justify-content: center; gap: 15px;
            background: #f9f9f9; padding: 15px 30px; border-radius: 12px; border: 1px solid #e0e0e0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05); width: 100%; max-width: 450px; box-sizing: border-box;
        }
        .signature-label { font-size: 18px; color: #333; font-weight: bold; }
        .signature-inline-img { max-height: 120px; width: auto; object-fit: contain; }

        /* גלריית עבודות לפני ואחרי */
        .gallery-section {
            margin-top: 30px; background: #f4f8ff; border: 2px solid #007bff;
            padding: 20px; border-radius: 10px; text-align: right;
        }
        html[dir="ltr"] .gallery-section { text-align: left; }
        .gallery-toggle-btn {
            background: #007bff; color: #fff; border: none; padding: 10px 18px;
            border-radius: 6px; font-weight: bold; font-size: 14px; cursor: pointer; margin-bottom: 15px;
        }
        .gallery-toggle-btn:hover { background: #0056b3; }
        .gallery-upload-box {
            display: none; background: #ffffff; border: 1px dashed #007bff;
            border-radius: 8px; padding: 15px; margin-bottom: 20px;
        }
        .gallery-upload-box.open { display: block; }
        .before-after-columns {
            display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 10px;
        }
        @media (max-width: 520px) {
            .before-after-columns { grid-template-columns: 1fr; }
        }
        .ba-col { background: #f9fbff; border: 1px solid #e1e8f5; border-radius: 8px; padding: 8px; }
        .ba-badge {
            display: inline-block; padding: 3px 10px; border-radius: 12px;
            font-size: 12px; font-weight: bold; margin-bottom: 8px;
        }
        .ba-badge.before { background: #fde2e2; color: #a12727; }
        .ba-badge.after { background: #d4f5dd; color: #176b2c; }

        /* סקציית תגובות */
        .reviews-section {
            margin-top: 30px; background: #fafafa; border: 2px dashed #007bff;
            padding: 20px; border-radius: 8px; text-align: right;
        }
        html[dir="ltr"] .reviews-section, html[dir="ltr"] .form-group,
        html[dir="ltr"] .review-card, html[dir="ltr"] .filter-container { text-align: left; }
        .form-group { margin-bottom: 15px; text-align: right; }
        html[dir="ltr"] .form-group { text-align: left; }
        .form-group label { display: block; margin-bottom: 5px; font-weight: bold; }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%; padding: 10px; box-sizing: border-box;
            border: 1px solid #ccc; border-radius: 4px; font-size: 14px;
        }
        .stars-container {
            display: flex; justify-content: flex-start; gap: 6px;
            font-size: 40px; line-height: 1; padding: 5px 0;
        }
        .star {
            position: relative; display: inline-block; color: #ddd; cursor: pointer;
            user-select: none; -webkit-tap-highlight-color: transparent;
            touch-action: manipulation; transition: transform 0.1s ease;
        }
        .star .fill {
            position: absolute; top: 0; inset-inline-start: 0; width: 0;
            overflow: hidden; white-space: nowrap; color: #ffc107; pointer-events: none;
        }
        .star:active { transform: scale(1.12); }
        .star-hint { font-size: 12px; color: #888; margin-top: 2px; }
        .other-reviews { background: #f4f8ff; border-radius: 8px; padding: 14px; margin-top: 20px; text-align: center; }
        .other-reviews p { margin: 0 0 10px; font-weight: bold; color: #444; }
        .other-reviews .social-btns-row { gap: 10px; }
        .google-btn { background: #4285f4; }
        .b144-btn { background: #d32f2f; }
        .reviews-list { margin-top: 20px; border-top: 1px solid #ddd; padding-top: 15px; }
        .review-card {
            background: #fff; border: 1px solid #e1e1e1; padding: 12px 15px;
            border-radius: 6px; margin-bottom: 12px; text-align: right;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        html[dir="ltr"] .review-card { text-align: left; }
        .review-header {
            display: flex; justify-content: space-between; font-weight: bold;
            font-size: 14px; color: #444; margin-bottom: 5px; gap: 8px;
        }

        /* תצוגת תמונות וסרטונים */
        .review-images-grid {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(90px, 1fr));
            gap: 8px; margin-top: 10px;
        }
        .review-image {
            width: 100%; height: 90px; object-fit: cover; border-radius: 6px;
            display: block; cursor: pointer; transition: transform 0.15s ease;
        }
        .review-image:hover { transform: scale(1.03); }
        .review-videos-grid {
            display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
            gap: 10px; margin-top: 10px;
        }
        .review-video {
            width: 100%; max-height: 220px; border-radius: 6px;
            background: #000; display: block;
        }

        /* חלון הגדלה לתמונה או וידאו */
        .lightbox {
            display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.88);
            z-index: 9999; align-items: center; justify-content: center; padding: 20px;
        }
        .lightbox.open { display: flex; }
        .lightbox img, .lightbox video {
            max-width: 95%; max-height: 90vh; border-radius: 8px;
            box-shadow: 0 4px 25px rgba(0,0,0,0.5); background: #000;
        }
        footer {
            margin-top: 30px; font-size: 13px; color: #777;
            border-top: 1px solid #eee; padding-top: 15px;
        }
    </style>
</head>
<body>

<div class="container">

    <!-- החלפת שפה -->
    <div class="lang-switch">
        <button type="button" id="btn-he" class="on" onclick="setLang('he')">עברית</button>
        <button type="button" id="btn-ru" onclick="setLang('ru')">Русский</button>
    </div>

    <div class="top-brand-bar">
        <div class="business-card-section">
            <img src="1793908727293.jpg" alt="M.R כרטיס ביקור" class="brand-character-img">
        </div>
        <img src="1793908641410.jpg" alt="M.R לוגו" class="brand-logo-img">
    </div>

    <h1>M.R. הכל לבית</h1>
    <p data-ru="Комплексный, профессиональный и быстрый сервис от Кирьят-Шмоны до Беэр-Шевы">שירות מקיף, מקצועי ומהיר מקרית שמונה ועד באר שבע</p>

    <!-- כפתורי תקשורת וחתימה -->
    <div class="social-links">
        <div class="social-btns-row">
            <a href="https://wa.me/972559423309?text=שלום%2C%20אשמח%20לקבל%20פרטים%20נוספים" target="_blank" rel="noopener" class="social-btn whatsapp-btn">💬 WhatsApp · 055-9423309</a>
            <a href="tel:+972559423309" class="social-btn call-btn">📞 <span data-ru="Позвонить">התקשר עכשיו</span></a>
            <a href="https://www.instagram.com/m.r26420" target="_blank" rel="noopener" class="social-btn instagram-btn">📸 Instagram @m.r26420</a>
            <a href="https://www.tiktok.com/@m.r26420" target="_blank" rel="noopener" class="social-btn tiktok-btn">🎵 TikTok @m.r26420</a>
        </div>
        <div class="signature-container">
            <span class="signature-label" data-ru="Подпись компании:">חתימת העסק:</span>
            <img src="IMG_20261021_205959.jpg" alt="חתימה" class="signature-inline-img">
        </div>
    </div>

    <h2 data-ru="Выберите услугу">בחרו שירות</h2>
    <div class="services-grid">
        <a class="btn" data-ru="🚰 Сантехника" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודת%20אינסטלציה.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🚰 אינסטלציה</a>
        <a class="btn" data-ru="⚡ Электрика" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודות%20חשמל.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">⚡ חשמל</a>
        <a class="btn" data-ru="🎨 Покраска" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודת%20צבע.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🎨 צבע</a>
        <a class="btn" data-ru="🛋️ Реставрация мебели" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בחידוש%20רהיטים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🛋️ חידוש רהיטים</a>
        <a class="btn" data-ru="🧹 Уборка" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בניקיון.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🧹 ניקיון</a>
        <a class="btn" data-ru="🧱 Демонтаж" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהריסות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🧱 הריסות</a>
        <a class="btn" data-ru="📐 Ремонт" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בשיפוצים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">📐 שיפוצים</a>
        <a class="btn" data-ru="🪚 Гипсокартон" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודות%20גבס.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🪚 עבודות גבס</a>
    </div>

    <h2 data-ru="🚚 Перевозки">🚚 הובלות</h2>
    <div class="moves-grid">
        <a class="btn" data-ru="🚛 Большие перевозки" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20גדולות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🚛 הובלות גדולות</a>
        <a class="btn" data-ru="📦 Малые перевозки" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20קטנות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">📦 הובלות קטנות</a>
        <a class="btn" data-ru="🛋️ Перевозка одного предмета мебели" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלת%20רהיט%20אחד.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🛋️ הובלת רהיט אחד</a>
        <a class="btn" data-ru="🏢 Перевозки офисов" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20משרדים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🏢 הובלות משרדים</a>
    </div>

    <h2 data-ru="📍 Район работы">📍 אזור פעילות</h2>
    <div class="info-box" data-ru="Работаем <b>от Кирьят-Шмоны до Беэр-Шевы</b>">אנחנו פעילים <b>מקרית שמונה ועד באר שבע</b></div>

    <h2 data-ru="🕒 Часы работы">🕒 שעות פעילות</h2>
    <div class="info-box">
        <div class="row"><span data-ru="Воскресенье – четверг">ראשון – חמישי</span><b>08:00 – 20:00</b></div>
        <div class="row"><span data-ru="Пятница">שישי</span><b>09:00 – 14:00</b></div>
        <div class="row"><span data-ru="Суббота">שבת</span><b style="color:#a12727" data-ru="Только экстренные случаи">מקרה חירום בלבד</b></div>
    </div>

    <!-- שירות חירום -->
    <h2 data-ru="🚨 Срочный вызов">🚨 שירות חירום</h2>
    <div class="emergency-box">
        <h3 data-ru="Что включает срочный вызов и как подготовиться заранее:">מה כולל שירות חירום ואיך נערכים מראש:</h3>
        <ul class="emergency-tips" data-ru="<li><b>Когда обращаться:</b> протечка/прорыв воды, короткое замыкание или искрение, срочный ремонт или экстренная перевозка.</li><li><b>Как мы работаем:</b> быстрая оценка ситуации и выезд по возможности, прозрачное согласование условий заранее.</li><li><b>Что отправить сразу:</b> город, этаж/доступ и фото или видео проблемы (если это безопасно).</li>">
            <li><b>מתי פונים:</b> פיצוץ מים או נזילה פעילה, קצר/תקלת חשמל, מפגע בטיחותי או הובלה דחופה.</li>
            <li><b>איך זה עובד:</b> תעדוף מהיר, בירור פרטים מראש ותיאום ברור לפני יציאה/תחילת עבודה.</li>
            <li><b>מה כדאי לשלוח מיד:</b> עיר וכתובת/קומה, ותמונה או סרטון קצר (רק אם בטוח לצלם).</li>
        </ul>

        <div class="form-group">
            <label for="emergencyType" data-ru="Тип экстренного случая:">סוג קריאת החירום:</label>
            <select id="emergencyType">
                <option value="נזילה / פיצוץ מים" data-ru="Прорыв воды / утечка">נזילה / פיצוץ מים</option>
                <option value="תקלת חשמל / קצר" data-ru="Проблема с электричеством / замыкание">תקלת חשמל / קצר</option>
                <option value="מפגע / תיקון דחוף" data-ru="Срочный ремонт / опасность">מפגע / תיקון דחוף</option>
                <option value="הובלה / פינוי דחוף" data-ru="Срочная перевозка">הובלה / פינוי דחוף</option>
            </select>
        </div>

        <div class="form-group">
            <label for="emergencyCity" data-ru="Город и район:">עיר / אזור:</label>
            <input type="text" id="emergencyCity" placeholder="למשל: כרמיאל / חיפה / צפון" data-ru-ph="Например: Кармиэль, Хайфа...">
        </div>

        <div class="social-btns-row">
            <a id="emergencyWaBtn" href="https://wa.me/972559423309" target="_blank" rel="noopener" class="social-btn emergency-wa-btn">
                🚨 <span data-ru="Отправить срочный запрос в WhatsApp">שלח קריאת חירום בוואטסאפ</span>
            </a>
            <a href="tel:+972559423309" class="social-btn call-btn">
                📞 <span data-ru="Срочный звонок">חיוג חירום מיידי</span>
            </a>
        </div>
    </div>

    <!-- גלריית עבודות לפני ואחרי -->
    <div class="gallery-section">
        <h2 style="margin-top: 0;" data-ru="📸 Галерея работ: До и После">📸 גלריית עבודות: לפני ואחרי</h2>

        <button type="button" class="gallery-toggle-btn" id="toggleGalleryUploadBtn" data-ru="➕ Добавить фото работы (До / После)">
            ➕ הוסף תמונות עבודה (לפני / אחרי)
        </button>

        <div class="gallery-upload-box" id="galleryUploadBox">
            <h3 style="margin-top: 0; color: #007bff;" data-ru="Загрузить новую работу в галерею:">העלאת עבודה חדשה לגלריה:</h3>
            <form id="galleryForm">
                <div class="form-group">
                    <label for="galleryPin" data-ru="Пароль администратора:">קוד מנהל (לבעל העסק בלבד):</label>
                    <input type="password" id="galleryPin" required placeholder="הכנס קוד מנהל" data-ru-ph="Введите пароль">
                </div>

                <div class="form-group">
                    <label for="galleryCategory" data-ru="Категория работы:">קטגוריית העבודה:</label>
                    <select id="galleryCategory" required>
                        <option value="" data-ru="Выберите услугу...">בחר שירות...</option>
                        <option value="אינסטלציה" data-ru="Сантехника">אינסטלציה</option>
                        <option value="חשמל" data-ru="Электрика">חשמל</option>
                        <option value="צבע" data-ru="Покраска">צבע</option>
                        <option value="חידוש רהיטים" data-ru="Реставрация мебели">חידוש רהיטים</option>
                        <option value="ניקיון" data-ru="Уборка">ניקיון</option>
                        <option value="הריסות" data-ru="Демонтаж">הריסות</option>
                        <option value="שיפוצים" data-ru="Ремонт">שיפוצים</option>
                        <option value="עבודות גבס" data-ru="Гипсокартон">עבודות גבס</option>
                        <option value="הובלות גדולות" data-ru="Большие перевозки">הובלות גדולות</option>
                        <option value="הובלות קטנות" data-ru="Малые перевозки">הובלות קטנות</option>
                        <option value="הובלת רהיט אחד" data-ru="Перевозка одного предмета мебели">הובלת רהיט אחד</option>
                        <option value="הובלות משרדים" data-ru="Перевозки офисов">הובלות משרדים</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="galleryTitle" data-ru="Краткое описание работы:">תיאור קצר של העבודה:</label>
                    <input type="text" id="galleryTitle" required placeholder="למשל: שיפוץ חדר אמבטיה / צביעת דירה בכרמיאל" data-ru-ph="Например: Ремонт ванной / Покраска квартиры">
                </div>

                <div class="form-group">
                    <label for="beforeImages" data-ru="Фото/видео ДО работы (до 10 файлов):">תמונות / סרטונים לפני העבודה (עד 10 קבצים):</label>
                    <input type="file" id="beforeImages" accept="image/*,video/*" multiple required>
                </div>

                <div class="form-group">
                    <label for="afterImages" data-ru="Фото/видео ПОСЛЕ работы (до 10 файлов):">תמונות / סרטונים אחרי העבודה (עד 10 קבצים):</label>
                    <input type="file" id="afterImages" accept="image/*,video/*" multiple required>
                </div>

                <button type="submit" class="btn" id="gallerySubmitBtn" style="background: #007bff; width: 100%; border: none; cursor: pointer; font-size: 16px;"></button>
            </form>
        </div>

        <div class="filter-container" style="text-align: right; margin-bottom: 15px;">
            <label for="filterGalleryCategory" style="font-weight: bold; margin-left: 10px;" data-ru="Фильтр галереи по категории:">סנן עבודות לפי קטגוריה:</label>
            <select id="filterGalleryCategory" onchange="renderGallery()" style="width: 200px; padding: 5px;">
                <option value="all" data-ru="Показать все">הצג הכל</option>
                <option value="אינסטלציה" data-ru="Сантехника">אינסטלציה</option>
                <option value="חשמל" data-ru="Электрика">חשמל</option>
                <option value="צבע" data-ru="Покраска">צבע</option>
                <option value="חידוש רהיטים" data-ru="Реставрация мебели">חידוש רהיטים</option>
                <option value="ניקיון" data-ru="Уборка">ניקיון</option>
                <option value="הריסות" data-ru="Демонтаж">הריסות</option>
                <option value="שיפוצים" data-ru="Ремонт">שיפוצים</option>
                <option value="עבודות גבס" data-ru="Гипсокартон">עבודות גבס</option>
                <option value="הובלות גדולות" data-ru="Большие перевозки">הובלות גדולות</option>
                <option value="הובלות קטנות" data-ru="Малые перевозки">הובלות קטנות</option>
                <option value="הובלת רהיט אחד" data-ru="Перевозка одного предмета мебели">הובלת רהיט אחד</option>
                <option value="הובלות משרדים" data-ru="Перевозки офисов">הובלות משרדים</option>
            </select>
        </div>

        <div class="reviews-list" id="galleryList"></div>
    </div>

    <!-- שאלות נפוצות -->
    <h2 data-ru="❓ Частые вопросы">❓ שאלות נפוצות</h2>
    <div class="faq">
        <details>
            <summary data-ru="Как получить расчёт стоимости и что отправить?">איך מקבלים הצעת מחיר ומה כדאי לשלוח?</summary>
            <div data-ru="<p>Нажмите на кнопку нужной услуги – откроется WhatsApp с готовым сообщением. Отправьте:</p><ul><li>Короткое описание работы</li><li>Фото или видео</li><li>Город и адрес</li><li>Желаемую дату и срочность</li></ul><p>Для перевозок также: адрес загрузки и выгрузки, этаж и лифт, список вещей.</p>">
                <p>לוחצים על כפתור השירות הרצוי ונפתח וואטסאפ עם הודעה מוכנה. כדאי לשלוח:</p>
                <ul>
                    <li>תיאור קצר של העבודה</li>
                    <li>תמונות או וידאו</li>
                    <li>עיר וכתובת</li>
                    <li>תאריך מבוקש והאם זה דחוף</li>
                </ul>
                <p>להובלות גם: כתובת איסוף ויעד, קומה ומעלית, ורשימת פריטים.</p>
            </div>
        </details>
        <details>
            <summary data-ru="В каких районах и в какие часы вы работаете?">באילו אזורים ובאילו שעות אתם עובדים?</summary>
            <p data-ru="От Кирьят-Шмоны до Беэр-Шевы. Вс–чт 8:00–20:00, пт 9:00–14:00.">מקרית שמונה ועד באר שבע. ראשון–חמישי 8:00–20:00, שישי 9:00–14:00.</p>
        </details>
        <details>
            <summary data-ru="Вы работаете в субботу и в срочных случаях?">האם עובדים בשבת ובמקרים דחופים?</summary>
            <p data-ru="В субботу – только экстренные случаи. Напишите в WhatsApp и укажите, что это срочно.">בשבת אנחנו עובדים במקרי חירום בלבד. שלחו הודעה בוואטסאפ וכתבו שזה דחוף.</p>
        </details>
    </div>

    <!-- אזור תגובות -->
    <div class="reviews-section">
        <h2 data-ru="⭐ Отзывы клиентов и оценки">⭐ תגובות לקוחות ודירוגים</h2>
        <h3 data-ru="✍️ Оставьте отзыв и оцените нас:">✍️ השאר תגובה ודרג אותנו:</h3>

        <form id="reviewForm">
            <div class="form-group">
                <label for="reviewerName" data-ru="Полное имя:">שם מלא:</label>
                <input type="text" id="reviewerName" required placeholder="הכנס את שמך" data-ru-ph="Введите ваше имя">
            </div>

            <div class="form-group">
                <label for="reviewCategory" data-ru="Выберите категорию:">בחר קטגוריה:</label>
                <select id="reviewCategory" required>
                    <option value="" data-ru="Выберите услугу...">בחר שירות...</option>
                    <option value="אינסטלציה" data-ru="Сантехника">אינסטלציה</option>
                    <option value="חשמל" data-ru="Электрика">חשמל</option>
                    <option value="צבע" data-ru="Покраска">צבע</option>
                    <option value="חידוש רהיטים" data-ru="Реставрация мебели">חידוש רהיטים</option>
                    <option value="ניקיון" data-ru="Уборка">ניקיון</option>
                    <option value="הריסות" data-ru="Демонтаж">הריסות</option>
                    <option value="שיפוצים" data-ru="Ремонт">שיפוצים</option>
                    <option value="עבודות גבס" data-ru="Гипсокартон">עבודות גבס</option>
                    <option value="הובלות גדולות" data-ru="Большие перевозки">הובלות גדולות</option>
                    <option value="הובלות קטנות" data-ru="Малые перевозки">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד" data-ru="Перевозка одного предмета мебели">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים" data-ru="Перевозки офисов">הובלות משרדים</option>
                </select>
            </div>

            <div class="form-group">
                <label data-ru="Оценка звёздами (нажмите на звезду):">דירוג כוכבים (לחץ על כוכב לבחירה):</label>
                <div class="stars-container" id="starPicker">
                    <span class="star">★<span class="fill">★</span></span>
                    <span class="star">★<span class="fill">★</span></span>
                    <span class="star">★<span class="fill">★</span></span>
                    <span class="star">★<span class="fill">★</span></span>
                    <span class="star">★<span class="fill">★</span></span>
                </div>
                <div class="star-hint" data-ru="Нажмите на левую или правую половину звезды, чтобы выбрать половинку">לחיצה על חצי כוכב בוחרת חצי דירוג</div>
                <div style="margin-top: 5px; font-weight: bold; color: #007bff;" id="ratingText"></div>
                <input type="hidden" id="reviewRating" value="5" required>
            </div>

            <div class="form-group">
                <label for="reviewText" data-ru="Ваш отзыв:">התגובה שלך:</label>
                <textarea id="reviewText" rows="3" required placeholder="כתוב כאן את חוות דעתך..." data-ru-ph="Напишите здесь свой отзыв..."></textarea>
            </div>

            <div class="form-group">
                <label for="reviewImages" data-ru="Прикрепите фото или видео работы (до 10 файлов):">צרף תמונות או סרטונים להוכחת העבודה (עד 10 קבצים):</label>
                <input type="file" id="reviewImages" accept="image/*,video/*" multiple>
            </div>

            <button type="submit" class="btn" id="submitBtn" style="background: #28a745; width: 100%; border: none; cursor: pointer; font-size: 16px;"></button>
        </form>

        <div class="other-reviews">
            <p data-ru="Хотите оставить отзыв и в других местах?">רוצים לכתוב עלינו גם בגוגל או ב-144?</p>
            <div class="social-btns-row">
                <a class="social-btn google-btn" href="https://www.google.com/maps?cid=16449588355030326794" target="_blank" rel="noopener" data-ru="⭐ Отзыв в Google">⭐ ביקורת בגוגל</a>
                <a class="social-btn b144-btn" href="https://www.b144.co.il/b144_sip/401D0D1A4370655D4011001240/" target="_blank" rel="noopener" data-ru="📒 Отзыв в 144">📒 ביקורת ב-144</a>
            </div>
        </div>

        <div style="margin-top: 35px;">
            <div class="filter-container" style="text-align: right; margin-bottom: 15px;">
                <label for="filterCategory" style="font-weight: bold; margin-left: 10px;" data-ru="Фильтр отзывов по категории:">סנן תגובות לפי קטגוריה:</label>
                <select id="filterCategory" onchange="renderReviews()" style="width: 200px; padding: 5px;">
                    <option value="all" data-ru="Показать все">הצג הכל</option>
                    <option value="אינסטלציה" data-ru="Сантехника">אינסטלציה</option>
                    <option value="חשמל" data-ru="Электрика">חשמל</option>
                    <option value="צבע" data-ru="Покраска">צבע</option>
                    <option value="חידוש רהיטים" data-ru="Реставрация мебели">חידוש רהיטים</option>
                    <option value="ניקיון" data-ru="Уборка">ניקיון</option>
                    <option value="הריסות" data-ru="Демонтаж">הריסות</option>
                    <option value="שיפוצים" data-ru="Ремонт">שיפוצים</option>
                    <option value="עבודות גבס" data-ru="Гипсокартон">עבודות גבס</option>
                    <option value="הובלות גדולות" data-ru="Большие перевозки">הובלות גדולות</option>
                    <option value="הובלות קטנות" data-ru="Малые перевозки">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד" data-ru="Перевозка одного предмета мебели">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים" data-ru="Перевозки офисов">הובלות משרדים</option>
                </select>
            </div>

            <div class="reviews-list" id="reviewsList"></div>
        </div>
    </div>

    <footer>Matan Richter © M.R. הכל לבית</footer>
</div>

<!-- חלון הגדלה לתמונה או סרטון -->
<div class="lightbox" id="lightbox" onclick="closeLightbox(event)">
    <img id="lightboxImg" src="" alt="" style="display: none;">
    <video id="lightboxVideo" src="" controls playsinline style="display: none;"></video>
</div>

<script>
    const CLOUDINARY_CLOUD_NAME = "ve1liculn";
    const CLOUDINARY_UPLOAD_PRESET = "l5javtcs";
    const ADMIN_GALLERY_PIN = "MR26420";

    const firebaseConfig = {
        databaseURL: "https://mr-services26-default-rtdb.firebaseio.com"
    };
    if (!firebase.apps.length) {
        firebase.initializeApp(firebaseConfig);
    }
    const database = firebase.database();
    const reviewsRef = database.ref('reviews');
    const galleryRef = database.ref('gallery');

    let allReviews = [];
    let allGallery = [];
    let lang = 'he';

    const reviewForm = document.getElementById('reviewForm');
    const reviewsList = document.getElementById('reviewsList');
    const filterCategory = document.getElementById('filterCategory');
    const reviewRatingInput = document.getElementById('reviewRating');
    const ratingText = document.getElementById('ratingText');
    const stars = document.querySelectorAll('#starPicker .star');
    const submitBtn = document.getElementById('submitBtn');

    const galleryForm = document.getElementById('galleryForm');
    const galleryList = document.getElementById('galleryList');
    const filterGalleryCategory = document.getElementById('filterGalleryCategory');
    const gallerySubmitBtn = document.getElementById('gallerySubmitBtn');
    const toggleGalleryUploadBtn = document.getElementById('toggleGalleryUploadBtn');
    const galleryUploadBox = document.getElementById('galleryUploadBox');

    const emergencyTypeEl = document.getElementById('emergencyType');
    const emergencyCityEl = document.getElementById('emergencyCity');
    const emergencyWaBtn = document.getElementById('emergencyWaBtn');

    const M = {
        he: {
            rating: v => `דירוג נבחר: ${v} מתוך 5 כוכבים`,
            send: 'פרסם תגובה באתר ושלח לוואטסאפ 🚀',
            sending: 'מעלה קבצים ושולח... ⏳',
            loading: 'טוען תגובות...',
            empty: 'אין עדיין תגובות להצגה בקטגוריה זו.',
            fill: 'אנא מלא את כל השדות בטופס בצורה תקינה.',
            max: 'ניתן להעלות עד 10 קבצים בלבד.',
            err: 'שגיאה בשמירת התגובה. אנא נסה שוב.',
            alt: 'מדיית עבודה',
            galSend: 'פרסם עבודה בגלריה (לפני ואחרי) 📸',
            galSending: 'מעלה קבצים לגלריה... ⏳',
            galLoading: 'טוען עבודות מהגלריה...',
            galEmpty: 'אין עדיין עבודות להצגה בקטגוריה זו.',
            galBadPin: 'קוד מנהל שגוי. רק בעל העסק יכול להעלות עבודות לגלריה.',
            galNeedImgs: 'אנא בחר לפחות קובץ אחד של "לפני" וקובץ אחד של "אחרי".',
            galErr: 'שגיאה בהעלאת העבודה לגלריה. אנא נסה שוב.',
            before: 'לפני העבודה',
            after: 'אחרי העבודה'
        },
        ru: {
            rating: v => `Выбранная оценка: ${v} из 5 звёзд`,
            send: 'Опубликовать отзыв и отправить в WhatsApp 🚀',
            sending: 'Загрузка файлов и отправка... ⏳',
            loading: 'Загрузка отзывов...',
            empty: 'В этой категории пока нет отзывов.',
            fill: 'Пожалуйста, заполните все поля формы.',
            max: 'Можно загрузить не более 10 файлов.',
            err: 'Ошибка сохранения отзыва. Попробуйте ещё раз.',
            alt: 'Медиа работы',
            galSend: 'Опубликовать работу (До и После) 📸',
            galSending: 'Загрузка файлов в галерею... ⏳',
            galLoading: 'Загрузка галереи...',
            galEmpty: 'В этой категории пока нет работ.',
            galBadPin: 'Неверный пароль администратора.',
            galNeedImgs: 'Выберите хотя бы один файл «До» и один файл «После».',
            galErr: 'Ошибка сохранения в галерею. Попробуйте ещё раз.',
            before: 'ДО работы',
            after: 'ПОСЛЕ работы'
        }
    };

    function isVideoUrl(url) {
        if (!url || typeof url !== 'string') return false;
        return /\.(mp4|mov|webm|ogg|m4v)(\?|$)/i.test(url) || url.includes('/video/upload/');
    }

    function openLightbox(url, type = 'image') {
        const lb = document.getElementById('lightbox');
        const img = document.getElementById('lightboxImg');
        const vid = document.getElementById('lightboxVideo');
        if (type === 'video' || isVideoUrl(url)) {
            img.style.display = 'none';
            img.src = '';
            vid.style.display = 'block';
            vid.src = url;
        } else {
            vid.pause();
            vid.style.display = 'none';
            vid.src = '';
            img.style.display = 'block';
            img.src = url;
        }
        lb.classList.add('open');
    }

    function closeLightbox(event) {
        if (event && event.target.tagName === 'VIDEO') return;
        const lb = document.getElementById('lightbox');
        const vid = document.getElementById('lightboxVideo');
        vid.pause();
        vid.src = '';
        lb.classList.remove('open');
    }

    function renderMediaBlock(urls, labelText) {
        if (!Array.isArray(urls) || urls.length === 0) return '';
        const images = urls.filter(u => !isVideoUrl(u));
        const videos = urls.filter(u => isVideoUrl(u));

        const imgsHtml = images.length
            ? `<div class="review-images-grid">${images.map(url =>
                `<img src="${escapeHTML(url)}" alt="${escapeHTML(labelText)}" class="review-image" loading="lazy" onclick="openLightbox('${escapeHTML(url)}', 'image')">`
              ).join('')}</div>`
            : '';

        const vidsHtml = videos.length
            ? `<div class="review-videos-grid">${videos.map(url =>
                `<video src="${escapeHTML(url)}" controls playsinline preload="metadata" class="review-video"></video>`
              ).join('')}</div>`
            : '';

        return imgsHtml + vidsHtml;
    }

    toggleGalleryUploadBtn.addEventListener('click', () => {
        galleryUploadBox.classList.toggle('open');
    });

    function updateEmergencyLink() {
        if (!emergencyTypeEl || !emergencyCityEl || !emergencyWaBtn) return;
        const selectedOption = emergencyTypeEl.options[emergencyTypeEl.selectedIndex];
        const typeText = (lang === 'ru' && selectedOption && selectedOption.dataset.ru)
            ? selectedOption.dataset.ru
            : emergencyTypeEl.value;
        const cityText = emergencyCityEl.value.trim() || (lang === 'ru' ? 'не указан' : 'לא צוין');

        const msg = lang === 'ru'
            ? `🚨 СРОЧНЫЙ ВЫЗОВ – M.R.\nТип случая: ${typeText}\nГород/район: ${cityText}\nПрикрепляю фото/видео и детали:`
            : `🚨 קריאת חירום – M.R. הכל לבית\nסוג המקרה: ${typeText}\nעיר/אזור: ${cityText}\nמצרף תמונה/וידאו ופרטים:`;

        emergencyWaBtn.href = `https://wa.me/972559423309?text=${encodeURIComponent(msg)}`;
    }

    function setLang(l) {
        lang = l;
        try { localStorage.setItem('lang', l); } catch (e) {}
        document.documentElement.lang = l;
        document.documentElement.dir = (l === 'ru') ? 'ltr' : 'rtl';
        document.getElementById('btn-he').classList.toggle('on', l === 'he');
        document.getElementById('btn-ru').classList.toggle('on', l === 'ru');

        document.querySelectorAll('[data-ru]').forEach(el => {
            if (el.dataset.he === undefined) el.dataset.he = el.innerHTML;
            el.innerHTML = (l === 'ru') ? el.dataset.ru : el.dataset.he;
        });
        document.querySelectorAll('[data-ru-ph]').forEach(el => {
            if (el.dataset.hePh === undefined) el.dataset.hePh = el.placeholder;
            el.placeholder = (l === 'ru') ? el.dataset.ruPh : el.dataset.hePh;
        });
        document.title = (l === 'ru') ? 'M.R. Всё для дома' : 'M.R. הכל לבית';

        ratingText.innerHTML = M[l].rating(reviewRatingInput.value);
        if (!submitBtn.disabled) submitBtn.innerHTML = M[l].send;
        if (!gallerySubmitBtn.disabled) gallerySubmitBtn.innerHTML = M[l].galSend;
        updateEmergencyLink();
        renderGallery();
        renderReviews();
    }

    function catLabel(cat) {
        if (lang !== 'ru') return cat;
        const opt = Array.from(document.getElementById('reviewCategory').options).find(o => o.value === cat);
        return opt && opt.dataset.ru ? opt.dataset.ru : cat;
    }

    function paintStars(val) {
        reviewRatingInput.value = val;
        ratingText.innerHTML = M[lang].rating(val);
        stars.forEach((s, i) => {
            const part = Math.max(0, Math.min(1, val - i));
            s.querySelector('.fill').style.width = (part * 100) + '%';
        });
    }

    stars.forEach((star, i) => {
        star.addEventListener('click', (e) => {
            const r = star.getBoundingClientRect();
            const rtl = document.documentElement.dir === 'rtl';
            const frac = rtl ? (r.right - e.clientX) / r.width : (e.clientX - r.left) / r.width;
            paintStars(i + (frac <= 0.5 ? 0.5 : 1));
        });
    });

    function getStarsHTML(rating) {
        const num = parseFloat(rating) || 5;
        const fulls = Math.floor(num);
        const hasHalf = (num - fulls) >= 0.5;
        let str = '';
        for (let i = 0; i < fulls; i++) str += '⭐';
        if (hasHalf) str += '✨';
        return `${str} (${num}/5)`;
    }

    function escapeHTML(str) {
        if (!str) return '';
        return String(str).replace(/[&<>'"]/g,
            tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
        );
    }

    async function uploadMediaToCloudinary(file) {
        const isVid = file.type && file.type.startsWith('video/');
        const resourceType = isVid ? 'video' : 'image';
        const formData = new FormData();
        formData.append('file', file);
        formData.append('upload_preset', CLOUDINARY_UPLOAD_PRESET);

        const res = await fetch(`https://api.cloudinary.com/v1_1/${CLOUDINARY_CLOUD_NAME}/${resourceType}/upload`, {
            method: 'POST',
            body: formData
        });
        const data = await res.json();
        if (!res.ok || !data.secure_url) {
            throw new Error(data.error?.message || 'Cloudinary upload failed');
        }
        return data.secure_url;
    }

    /* ===== גלריית לפני ואחרי ===== */
    function renderGallery() {
        galleryList.innerHTML = '';
        const selectedFilter = filterGalleryCategory.value;

        const filtered = selectedFilter === 'all'
            ? allGallery
            : allGallery.filter(item => item && item.category === selectedFilter);

        if (filtered.length === 0) {
            galleryList.innerHTML = `<p style="color: #777; text-align: center; padding: 10px;">${M[lang].galEmpty}</p>`;
            return;
        }

        filtered.forEach(item => {
            if (!item) return;
            const card = document.createElement('div');
            card.className = 'review-card';

            const beforeImgs = Array.isArray(item.beforeUrls) ? item.beforeUrls : [];
            const afterImgs = Array.isArray(item.afterUrls) ? item.afterUrls : [];

            card.innerHTML = `
                <div class="review-header">
                    <span>🛠️ ${escapeHTML(item.title)} <span style="color: #007bff; font-weight: normal;">(${escapeHTML(catLabel(item.category))})</span></span>
                    <span style="font-size: 11px; color: #888; font-weight: normal;">📅 ${escapeHTML(item.date || '')}</span>
                </div>
                <div class="before-after-columns">
                    <div class="ba-col">
                        <span class="ba-badge before">${M[lang].before}</span>
                        ${renderMediaBlock(beforeImgs, M[lang].before)}
                    </div>
                    <div class="ba-col">
                        <span class="ba-badge after">${M[lang].after}</span>
                        ${renderMediaBlock(afterImgs, M[lang].after)}
                    </div>
                </div>
            `;
            galleryList.appendChild(card);
        });
    }

    galleryList.innerHTML = `<p style="color: #777; text-align: center; padding: 10px;">${M[lang].galLoading}</p>`;
    galleryRef.on('value', (snapshot) => {
        const data = snapshot.val();
        allGallery = [];
        if (data) {
            Object.keys(data).forEach(key => {
                if (data[key]) {
                    allGallery.unshift(data[key]);
                }
            });
        }
        renderGallery();
    });

    galleryForm.addEventListener('submit', async function(e) {
        e.preventDefault();

        const pin = document.getElementById('galleryPin').value.trim();
        const category = document.getElementById('galleryCategory').value;
        const title = document.getElementById('galleryTitle').value.trim();
        const beforeFiles = Array.from(document.getElementById('beforeImages').files || []);
        const afterFiles = Array.from(document.getElementById('afterImages').files || []);

        if (pin !== ADMIN_GALLERY_PIN) {
            alert(M[lang].galBadPin);
            return;
        }
        if (!category || !title) {
            alert(M[lang].fill);
            return;
        }
        if (beforeFiles.length === 0 || afterFiles.length === 0) {
            alert(M[lang].galNeedImgs);
            return;
        }
        if (beforeFiles.length > 10 || afterFiles.length > 10) {
            alert(M[lang].max);
            return;
        }

        gallerySubmitBtn.disabled = true;
        gallerySubmitBtn.innerHTML = M[lang].galSending;

        try {
            const beforeUrls = [];
            for (const file of beforeFiles) {
                beforeUrls.push(await uploadMediaToCloudinary(file));
            }
            const afterUrls = [];
            for (const file of afterFiles) {
                afterUrls.push(await uploadMediaToCloudinary(file));
            }

            const dateStr = new Date().toLocaleDateString(lang === 'ru' ? 'ru-RU' : 'he-IL');
            await galleryRef.push({
                category,
                title,
                beforeUrls,
                afterUrls,
                date: dateStr
            });

            galleryForm.reset();
            galleryUploadBox.classList.remove('open');
        } catch (err) {
            console.error(err);
            alert(M[lang].galErr);
        } finally {
            gallerySubmitBtn.disabled = false;
            gallerySubmitBtn.innerHTML = M[lang].galSend;
        }
    });

    /* ===== תגובות לקוחות ===== */
    function renderReviews() {
        reviewsList.innerHTML = '';
        const selectedFilter = filterCategory.value;

        const filteredReviews = selectedFilter === 'all'
            ? allReviews
            : allReviews.filter(r => r && r.category === selectedFilter);

        if (filteredReviews.length === 0) {
            reviewsList.innerHTML = `<p style="color: #777; text-align: center; padding: 10px;">${M[lang].empty}</p>`;
            return;
        }

        filteredReviews.forEach(review => {
            if (!review) return;
            const card = document.createElement('div');
            card.className = 'review-card';

            const mediaHTML = renderMediaBlock(review.imageUrls, M[lang].alt);

            card.innerHTML = `
                <div class="review-header">
                    <span>👤 ${escapeHTML(review.name)} <span style="color: #007bff; font-weight: normal;">(${escapeHTML(catLabel(review.category))})</span></span>
                    <span>${getStarsHTML(review.rating)}</span>
                </div>
                <p style="margin: 8px 0; color: #333; word-break: break-word;">${escapeHTML(review.text)}</p>
                ${mediaHTML}
                <div style="font-size: 11px; color: #888; text-align: left; margin-top: 10px;">📅 ${escapeHTML(review.date || '')}</div>
            `;
            reviewsList.appendChild(card);
        });
    }

    reviewsList.innerHTML = `<p style="color: #777; text-align: center; padding: 10px;">${M[lang].loading}</p>`;
    reviewsRef.on('value', (snapshot) => {
        const data = snapshot.val();
        allReviews = [];
        if (data) {
            Object.keys(data).forEach(key => {
                if (data[key]) {
                    allReviews.unshift(data[key]);
                }
            });
        }
        renderReviews();
    });

    reviewForm.addEventListener('submit', async function(e) {
        e.preventDefault();

        const name = document.getElementById('reviewerName').value.trim();
        const category = document.getElementById('reviewCategory').value;
        const rating = parseFloat(reviewRatingInput.value) || 5;
        const text = document.getElementById('reviewText').value.trim();
        const files = Array.from(document.getElementById('reviewImages').files || []);

        if (!name || !category || !text) {
            alert(M[lang].fill);
            return;
        }
        if (files.length > 10) {
            alert(M[lang].max);
            return;
        }

        submitBtn.disabled = true;
        submitBtn.innerHTML = M[lang].sending;

        try {
            const imageUrls = [];
            for (const file of files) {
                const url = await uploadMediaToCloudinary(file);
                imageUrls.push(url);
            }

            const dateStr = new Date().toLocaleDateString(lang === 'ru' ? 'ru-RU' : 'he-IL');
            const newReview = {
                name,
                category,
                rating,
                text,
                imageUrls,
                date: dateStr
            };

            await reviewsRef.push(newReview);

            reviewForm.reset();
            paintStars(5);

            const waText = lang === 'ru'
                ? `⭐ Новый отзыв на сайте M.R.\nИмя: ${name}\nУслуга: ${category}\nОценка: ${rating}/5\nОтзыв: ${text}`
                : `⭐ תגובה חדשה באתר M.R. הכל לבית\nשם: ${name}\nשירות: ${category}\nדירוג: ${rating}/5\nתגובה: ${text}`;

            window.open(`https://wa.me/972559423309?text=${encodeURIComponent(waText)}`, '_blank', 'noopener');
        } catch (err) {
            console.error(err);
            alert(M[lang].err);
        } finally {
            submitBtn.disabled = false;
            submitBtn.innerHTML = M[lang].send;
        }
    });

    emergencyTypeEl.addEventListener('change', updateEmergencyLink);
    emergencyCityEl.addEventListener('input', updateEmergencyLink);

    let savedLang = 'he';
    try {
        const stored = localStorage.getItem('lang');
        if (stored === 'he' || stored === 'ru') savedLang = stored;
    } catch (e) {}

    paintStars(5);
    setLang(savedLang);
</script>

</body>
</html>
