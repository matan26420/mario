<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.R. הכל לבית</title>
    
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
        
        /* אזור כרטיס הביקור והלוגו בחלק העליון */
        .top-brand-bar {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 25px;
            margin-bottom: 30px;
        }

        /* כרטיס הביקור מרובע, מוגדל משמעותית וללא מסגרת כחולה */
        .business-card-section {
            background: #ffffff;
            padding: 10px;
            border-radius: 12px;
            width: 100%;
            max-width: 520px;
            box-sizing: border-box;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }
        .brand-character-img {
            width: 100%;
            height: auto;
            aspect-ratio: 1 / 1;
            object-fit: cover;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* הלוגו מרובע, מוגדל וללא מסגרת כחולה */
        .brand-logo-img {
            width: 260px;
            height: 260px;
            border-radius: 12px;
            object-fit: cover;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        h1 { margin: 10px 0 5px 0; color: #222; font-size: 30px; font-weight: bold; }
        h2 { color: #007bff; margin-top: 25px; }

        .services-grid, .moves-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }
        a.btn {
            display: block;
            background: #007bff;
            color: white;
            padding: 12px;
            text-decoration: none;
            border-radius: 6px;
            font-weight: bold;
            transition: background 0.3s;
        }
        a.btn:hover { background: #0056b3; }

        /* אזור קישורים רשתות חברתיות */
        .social-links {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
            margin: 25px 0;
        }
        .social-btns-row {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        .social-btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 10px 18px;
            border-radius: 6px;
            color: white;
            text-decoration: none;
            font-weight: bold;
            font-size: 14px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .instagram-btn { background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); }
        .tiktok-btn { background: #000000; }
        .whatsapp-btn { background: #25d366; }

        /* חתימה מוגדלת וברורה משמעותית */
        .signature-container {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            background: #f9f9f9;
            padding: 15px 30px;
            border-radius: 12px;
            border: 1px solid #e0e0e0;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            width: 100%;
            max-width: 450px;
            box-sizing: border-box;
        }
        .signature-label {
            font-size: 18px;
            color: #333;
            font-weight: bold;
        }
        .signature-inline-img {
            max-height: 120px;
            width: auto;
            object-fit: contain;
        }

        /* סקציית תגובות */
        .reviews-section {
            margin-top: 30px;
            background: #fafafa;
            border: 2px dashed #007bff;
            padding: 20px;
            border-radius: 8px;
            text-align: right;
        }
        .form-group {
            margin-bottom: 15px;
            text-align: right;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .stars-container {
            display: flex;
            flex-direction: row-reverse;
            justify-content: flex-end;
            gap: 8px;
            font-size: 34px;
            padding: 5px 0;
            unicode-bidi: bidi-override;
        }
        .star {
            color: #ddd;
            cursor: pointer;
            padding: 0 4px;
            display: inline-block;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
            transition: color 0.1s ease, transform 0.1s ease;
        }
        .star.active { color: #ffc107; }
        .star:active { transform: scale(1.2); }

        .reviews-list {
            margin-top: 20px;
            border-top: 1px solid #ddd;
            padding-top: 15px;
        }
        .review-card {
            background: #fff;
            border: 1px solid #e1e1e1;
            padding: 12px 15px;
            border-radius: 6px;
            margin-bottom: 12px;
            text-align: right;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .review-header {
            display: flex;
            justify-content: space-between;
            font-weight: bold;
            font-size: 14px;
            color: #444;
            margin-bottom: 5px;
        }
        .review-images-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(90px, 1fr));
            gap: 8px;
            margin-top: 10px;
        }
        .review-image {
            width: 100%;
            height: 90px;
            object-fit: cover;
            border-radius: 6px;
            display: block;
        }
        
        footer {
            margin-top: 30px;
            font-size: 13px;
            color: #777;
            border-top: 1px solid #eee;
            padding-top: 15px;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="top-brand-bar">
        <!-- כרטיס ביקור מוגדל ומרובע -->
        <div class="business-card-section">
            <img src="1793908727293.jpg" alt="M.R כרטיס ביקור" class="brand-character-img">
        </div>

        <!-- הלוגו מרובע, מוגדל וללא מסגרת כחולה -->
        <img src="1793908641410.jpg" alt="M.R לוגו" class="brand-logo-img">
    </div>

    <h1>M.R. הכל לבית</h1>
    <p>שירות מקיף, מקצועי ומהיר בכל מקום בישראל</p>

    <!-- כפתורי תקשורת וחתימה גדולה וברורה -->
    <div class="social-links">
        <div class="social-btns-row">
            <a href="https://wa.me/972559423309?text=שלום%2C%20אשמח%20לקבל%20פרטים%20נוספים" class="social-btn whatsapp-btn">💬 WhatsApp · 055-9423309</a>
            <a href="https://www.instagram.com/m.r26420" target="_blank" class="social-btn instagram-btn">📸 Instagram @m.r26420</a>
            <a href="https://www.tiktok.com/@m.r26420" target="_blank" class="social-btn tiktok-btn">🎵 TikTok @m.r26420</a>
        </div>
        <div class="signature-container">
            <span class="signature-label">חתימת העסק:</span>
            <img src="IMG_20261021_205959.jpg" alt="חתימה" class="signature-inline-img">
        </div>
    </div>

    <h2>בחרו שירות</h2>
    <div class="services-grid">
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודת%20אינסטלציה.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🚰 אינסטלציה</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודת%20צבע.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🎨 צבע</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בחידוש%20רהיטים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🛋️ חידוש רהיטים</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בניקיון.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🧹 ניקיון</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהריסות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🧱 הריסות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בשיפוצים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">📐 שיפוצים</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בעבודות%20גבס.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🪚 עבודות גבס</a>
    </div>

    <h2>🚚 הובלות</h2>
    <div class="moves-grid">
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20גדולות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🚛 הובלות גדולות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20קטנות.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">📦 הובלות קטנות</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלת%20רהיט%20אחד.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🛋️ הובלת רהיט אחד</a>
        <a class="btn" href="https://wa.me/972559423309?text=שלום%2C%20אני%20מעוניין%20בהובלות%20משרדים.%20נא%20להביא%20לי%20בבקשה%20הצעת%20מחיר%2C%20מצורפות%20תמונות%20או%20וידאו%20או%20גם%20וגם%3A">🏢 הובלות משרדים</a>
    </div>

    <!-- אזור תגובות -->
    <div class="reviews-section">
        <h2>⭐ תגובות לקוחות ודירוגים</h2>
        <h3>✍️ השאר תגובה ודרג אותנו:</h3>
        
        <form id="reviewForm">
            <div class="form-group">
                <label for="reviewerName">שם מלא:</label>
                <input type="text" id="reviewerName" required placeholder="הכנס את שמך">
            </div>

            <div class="form-group">
                <label for="reviewCategory">בחר קטגוריה:</label>
                <select id="reviewCategory" required>
                    <option value="">בחר שירות...</option>
                    <option value="אינסטלציה">אינסטלציה</option>
                    <option value="צבע">צבע</option>
                    <option value="חידוש רהיטים">חידוש רהיטים</option>
                    <option value="ניקיון">ניקיון</option>
                    <option value="הריסות">הריסות</option>
                    <option value="שיפוצים">שיפוצים</option>
                    <option value="עבודות גבס">עבודות גבס</option>
                    <option value="הובלות גדולות">הובלות גדולות</option>
                    <option value="הובלות קטנות">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים">הובלות משרדים</option>
                </select>
            </div>

            <div class="form-group">
                <label>דירוג כוכבים (לחץ על כוכב לבחירה):</label>
                <div class="stars-container" id="starPicker">
                    <span class="star" data-value="5">★</span>
                    <span class="star" data-value="4.5">★</span>
                    <span class="star" data-value="4">★</span>
                    <span class="star" data-value="3.5">★</span>
                    <span class="star" data-value="3">★</span>
                    <span class="star" data-value="2.5">★</span>
                    <span class="star" data-value="2">★</span>
                    <span class="star" data-value="1.5">★</span>
                    <span class="star" data-value="1">★</span>
                    <span class="star" data-value="0.5">★</span>
                </div>
                <div style="margin-top: 5px; font-weight: bold; color: #007bff;" id="ratingText">דירוג נבחר: 5 מתוך 5 כוכבים</div>
                <input type="hidden" id="reviewRating" value="5" required>
            </div>

            <div class="form-group">
                <label for="reviewText">התגובה שלך:</label>
                <textarea id="reviewText" rows="3" required placeholder="כתוב כאן את חוות דעתך..."></textarea>
            </div>

            <div class="form-group">
                <label for="reviewImages">צרף תמונות להוכחת העבודה (עד 10 תמונות):</label>
                <input type="file" id="reviewImages" accept="image/*" multiple>
            </div>

            <button type="submit" class="btn" id="submitBtn" style="background: #28a745; width: 100%; border: none; cursor: pointer; font-size: 16px;">פרסם תגובה באתר ושלח לוואטסאפ 🚀</button>
        </form>

        <div style="margin-top: 35px;">
            <div class="filter-container" style="text-align: right; margin-bottom: 15px;">
                <label for="filterCategory" style="font-weight: bold; margin-left: 10px;">סנן תגובות לפי קטגוריה:</label>
                <select id="filterCategory" onchange="renderReviews()" style="width: 200px; padding: 5px;">
                    <option value="all">הצג הכל</option>
                    <option value="אינסטלציה">אינסטלציה</option>
                    <option value="צבע">צבע</option>
                    <option value="חידוש רהיטים">חידוש רהיטים</option>
                    <option value="ניקיון">ניקיון</option>
                    <option value="הריסות">הריסות</option>
                    <option value="שיפוצים">שיפוצים</option>
                    <option value="עבודות גבס">עבודות גבס</option>
                    <option value="הובלות גדולות">הובלות גדולות</option>
                    <option value="הובלות קטנות">הובלות קטנות</option>
                    <option value="הובלת רהיט אחד">הובלת רהיט אחד</option>
                    <option value="הובלות משרדים">הובלות משרדים</option>
                </select>
            </div>

            <div class="reviews-list" id="reviewsList">
                <p style="color: #777;">טוען תגובות...</p>
            </div>
        </div>
    </div>

    <footer>Matan Richter © M.R. הכל לבית</footer>
</div>

<script>
    const IMGBB_API_KEY = "7b4b0bd1f4a6019c1bb0172dd143e46d";

    const firebaseConfig = {
        databaseURL: "https://mr-services26-default-rtdb.firebaseio.com"
    };
    if (!firebase.apps.length) {
        firebase.initializeApp(firebaseConfig);
    }
    const database = firebase.database();
    const reviewsRef = database.ref('reviews');

    let allReviews = [];

    const reviewForm = document.getElementById('reviewForm');
    const reviewsList = document.getElementById('reviewsList');
    const filterCategory = document.getElementById('filterCategory');
    const reviewRatingInput = document.getElementById('reviewRating');
    const ratingText = document.getElementById('ratingText');
    const stars = document.querySelectorAll('#starPicker .star');
    const submitBtn = document.getElementById('submitBtn');

    // ניהול בחירת כוכבים אמין וישיר לכל מסך (מחשב ומובייל)
    stars.forEach(star => {
        const handleStarSelect = (e) => {
            e.preventDefault();
            e.stopPropagation();
            let val = parseFloat(star.getAttribute('data-value'));
            reviewRatingInput.value = val;
            ratingText.innerHTML = `דירוג נבחר: ${val} מתוך 5 כוכבים`;

            stars.forEach(s => {
                let sVal = parseFloat(s.getAttribute('data-value'));
                if (sVal <= val) {
                    s.classList.add('active');
                } else {
                    s.classList.remove('active');
                }
            });
        };

        star.addEventListener('click', handleStarSelect);
        star.addEventListener('touchstart', handleStarSelect);
    });

    function getStarsHTML(rating) {
        let fulls = Math.floor(rating);
        let hasHalf = (rating - fulls) >= 0.5;
        let str = '';
        for(let i=0; i<fulls; i++) str += '⭐';
        if(hasHalf) str += '✨';
        return `${str} (${rating}/5)`;
    }

    function renderReviews() {
        reviewsList.innerHTML = '';
        let selectedFilter = filterCategory.value;

        let filteredReviews = allReviews;
        if (selectedFilter !== 'all') {
            filteredReviews = allReviews.filter(r => r && r.category === selectedFilter);
        }

        if (filteredReviews.length === 0) {
            reviewsList.innerHTML = '<p style="color: #777; text-align: center; padding: 10px;">אין עדיין תגובות להצגה בקטגוריה זו.</p>';
            return;
        }

        filteredReviews.forEach(review => {
            if (!review) return;
            let card = document.createElement('div');
            card.className = 'review-card';
            
            let imagesHTML = '';
            if (review.imageUrls && review.imageUrls.length > 0) {
                imagesHTML = `<div class="review-images-grid">` + 
                    review.imageUrls.map(url => `<img src="${url}" alt="תמונת עבודה" class="review-image">`).join('') + 
                    `</div>`;
            }

            card.innerHTML = `
                <div class="review-header">
                    <span>👤 ${escapeHTML(review.name)} <span style="color: #007bff; font-weight: normal;">(${escapeHTML(review.category)})</span></span>
                    <span>${getStarsHTML(review.rating)}</span>
                </div>
                <p style="margin: 8px 0; color: #333; word-break: break-word;">${escapeHTML(review.text)}</p>
                ${imagesHTML}
                <div style="font-size: 11px; color: #888; text-align: left; margin-top: 10px;">📅 ${escapeHTML(review.date || '')}</div>
            `;
            reviewsList.appendChild(card);
        });
    }

    function escapeHTML(str) {
        if (!str) return '';
        return str.replace(/[&<>'"]/g, 
            tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
        );
    }

    // טעינת תגובות בזמן אמת עבור כל המשתמשים
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

        let name = document.getElementById('reviewerName').value.trim();
        let category = document.getElementById('reviewCategory').value;
        let rating = parseFloat(reviewRatingInput.value);
        let text = document.getElementById('reviewText').value.trim();
        let imageInput = document.getElementById('reviewImages');
        let imageFiles = imageInput.files ? Array.from(imageInput.files) : [];
        let date = new Date().toLocaleDateString('he-IL');

        if (!name || !category || !text || isNaN(rating)) {
            alert('אנא מלא את כל השדות בטופס בצורה תקינה.');
            return;
        }

        if (imageFiles.length > 10) {
            alert('ניתן להעלות עד 10 תמונות בלבד.');
            return;
        }

        submitBtn.disabled = true;
        submitBtn.innerHTML = 'מעלה תמונות ושולח... ⏳';

        let imageUrls = [];

        if (imageFiles.length > 0) {
            for (let i = 0; i < imageFiles.length; i++) {
                try {
                    let formData = new FormData();
                    formData.append('image', imageFiles[i]);

                    let response = await fetch(`https://api.imgbb.com/1/upload?key=${IMGBB_API_KEY}`, {
                        method: 'POST',
                        body: formData
                    });
                    let result = await response.json();
                    
                    if (result && result.success) {
                        imageUrls.push(result.data.url);
                    } else {
                        console.error('ImgBB Error for image ' + i, result);
                    }
                } catch (error) {
                    console.error('Error uploading image ' + i, error);
                }
            }
        }

        let newReview = { name, category, rating, text, date, imageUrls };
        
        try {
            let newRef = reviewsRef.push();
            await newRef.set(newReview);

            submitBtn.disabled = false;
            submitBtn.innerHTML = 'פרסם תגובה באתר ושלח לוואטסאפ 🚀';

            reviewForm.reset();
            reviewRatingInput.value = '5';
            ratingText.innerHTML = 'דירוג נבחר: 5 מתוך 5 כוכבים';
            stars.forEach(s => s.classList.add('active'));
            filterCategory.value = 'all';

            let whatsappMessage = `*💬 תגובה חדשה התקבלה באתר!*%0A%0A` +
                                  `👤 *שם:* ${encodeURIComponent(name)}%0A` +
                                  `🏷️ *קטגוריה:* ${encodeURIComponent(category)}%0A` +
                                  `⭐ *דירוג:* ${rating} כוכבים%0A` +
                                  `📝 *תוכן התגובה:* ${encodeURIComponent(text)}`;
            
            if (imageUrls.length > 0) {
                whatsappMessage += `%0A%0A🖼️ *תמונות העבודה:*`;
                imageUrls.forEach((url, index) => {
                    whatsappMessage += `%0A${index + 1}. ${url}`;
                });
            }

            let whatsappUrl = `https://wa.me/972559423309?text=${whatsappMessage}`;
            window.open(whatsappUrl, '_blank');
        } catch (error) {
            console.error('Error saving review:', error);
            alert('שגיאה בשמירת התגובה בבסיס הנתונים. אנא נסה שוב.');
            submitBtn.disabled = false;
            submitBtn.innerHTML = 'פרסם תגובה באתר ושלח לוואטסאפ 🚀';
        }
    });

    renderReviews();
</script>

</body>
</html>
