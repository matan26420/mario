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
        direction: rtl;
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
    
    /* אזור מיתוג עליון */
    .top-brand-bar {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 25px;
        margin-bottom: 25px;
    }

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

    /* סקציית בחירת אזורי שירות */
    .service-regions-box {
        background: #f0f7ff;
        border: 2px solid #007bff;
        border-radius: 10px;
        padding: 15px;
        margin-bottom: 25px;
    }

    .service-regions-box h3 {
        margin: 0 0 8px 0;
        color: #007bff;
        font-size: 18px;
    }

    .service-regions-box p {
        margin: 0 0 12px 0;
        font-size: 13px;
        color: #555;
    }

    .regions-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
        gap: 8px;
    }

    .region-btn {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 5px;
        background: #ffffff;
        color: #007bff;
        border: 1px solid #007bff;
        padding: 8px 10px;
        border-radius: 6px;
        cursor: pointer;
        font-weight: bold;
        font-size: 13px;
        transition: all 0.2s ease;
    }

    .region-btn:hover {
        background: #007bff;
        color: white;
        transform: translateY(-2px);
    }

    h1 { margin: 10px 0 5px 0; color: #222; font-size: 30px; font-weight: bold; }
    h2 { color: #007bff; margin-top: 25px; }

    /* גריד שירותים */
    .services-grid, .moves-grid {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 10px;
        margin-bottom: 20px;
    }

    a.btn, button.btn {
        display: block;
        width: 100%;
        background: #007bff;
        color: white;
        padding: 12px;
        text-decoration: none;
        border: none;
        border-radius: 6px;
        font-weight: bold;
        font-size: 14px;
        cursor: pointer;
        transition: background 0.3s;
        box-sizing: border-box;
    }
    a.btn:hover, button.btn:hover { background: #0056b3; }

    /* רשתות חברתיות */
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

    /* חתימה */
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
        margin: 0 auto;
        box-sizing: border-box;
    }
    .signature-label {
        font-size: 18px;
        color: #333;
        font-weight: bold;
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
    
    footer {
        margin-top: 30px;
        font-size: 13px;
        color: #777;
        border-top: 1px solid #eee;
        padding-top: 15px;
    }
</style>

<div class="container">
    <!-- אזור מיתוג עליון -->
    <div class="top-brand-bar">
        <div class="business-card-section">
            <img src="21215792-729b-4a30-ac73-18f9a904b58c.jpg" alt="כרטיס ביקור" class="brand-character-img">
        </div>
    </div>

    <!-- סקציית בחירת אזור שירות -->
    <div class="service-regions-box">
        <h3>📍 בחר אזור שירות להזמנה מהירה:</h3>
        <p>לחץ על האזור הרצוי לפניית וואטסאפ ממוקדת</p>
        <div class="regions-grid">
            <button class="region-btn" onclick="openWhatsappWithRegion('חיפה והקריות')">📍 חיפה והקריות</button>
            <button class="region-btn" onclick="openWhatsappWithRegion('השרון')">📍 השרון</button>
            <button class="region-btn" onclick="openWhatsappWithRegion('תל אביב והמרכז')">📍 תל אביב והמרכז</button>
            <button class="region-btn" onclick="openWhatsappWithRegion('השפלה')">📍 השפלה</button>
            <button class="region-btn" onclick="openWhatsappWithRegion('באר שבע והדרום')">📍 באר שבע והדרום</button>
        </div>
    </div>

    <!-- סקציית השירותים שלך -->
    <h2>השירותים שלנו</h2>
    <div class="services-grid">
        <button class="btn" onclick="openWhatsappWithService('עבודות הנדימן כלליות')">🔨 עבודות הנדימן</button>
        <button class="btn" onclick="openWhatsappWithService('תיקוני אינסטלציה')">🚰 תיקוני אינסטלציה</button>
        <button class="btn" onclick="openWhatsappWithService('תליית מדפים וטלוויזיות')">📺 תלייה והתקנות</button>
        <button class="btn" onclick="openWhatsappWithService('עבודות צבע ותיקונים')">🎨 עבודות צבע</button>
    </div>

</div>

<script>
    // הכנס כאן את מספר הוואטסאפ שלך (כולל קידומת 972)
    const whatsappPhone = "972000000000";

    function openWhatsappWithRegion(regionName) {
        const text = encodeURIComponent(`שלום, אני מגיע מאזור ${regionName} ואשמח לקבל הצעת מחיר.`);
        window.open(`https://wa.me/${whatsappPhone}?text=${text}`, '_blank');
    }

    function openWhatsappWithService(serviceName) {
        const text = encodeURIComponent(`שלום, אשמח לקבל הצעת מחיר עבור: ${serviceName}.`);
        window.open(`https://wa.me/${whatsappPhone}?text=${text}`, '_blank');
    }
</script>

