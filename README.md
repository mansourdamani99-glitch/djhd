<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>الحقني | المساعدة العاجلة على الطريق - الفضاء الذكي</title>
    <!-- Fonts & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- Supabase JS -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Cairo', sans-serif;
            background: radial-gradient(ellipse at 30% 40%, #0a0f1e, #03050b);
            color: #eef5ff;
            scroll-behavior: smooth;
            overflow-x: hidden;
            position: relative;
        }

        /* Stars background dynamic - moving stars */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .star {
            position: absolute;
            background-color: #fff;
            border-radius: 50%;
            opacity: 0.8;
            box-shadow: 0 0 8px rgba(255,255,200,0.8);
            animation: floatStar linear infinite;
        }

        @keyframes floatStar {
            0% {
                transform: translateY(0vh) translateX(0) rotate(0deg);
                opacity: 0.3;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) translateX(20px) rotate(360deg);
                opacity: 0.2;
            }
        }

        @keyframes twinkle {
            0% { opacity: 0.2; transform: scale(1);}
            100% { opacity: 1; transform: scale(1.3);}
        }

        /* Main content layer */
        .container {
            position: relative;
            z-index: 2;
            max-width: 1400px;
            margin: 0 auto;
            padding: 1rem 2rem;
        }

        /* Glowing text & borders */
        .glow-text {
            text-shadow: 0 0 6px #b0f0ff, 0 0 12px #4effdc, 0 0 20px #00a6c4;
            transition: all 0.3s ease;
        }

        h1, h2, h3, .logo {
            font-weight: 700;
        }

        h2 {
            font-size: 2rem;
            margin-bottom: 1rem;
            border-right: 4px solid #0ff;
            padding-right: 1rem;
            display: inline-block;
            text-shadow: 0 0 5px cyan;
        }

        /* Navigation */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            background: rgba(0,0,0,0.65);
            backdrop-filter: blur(12px);
            border-radius: 60px;
            padding: 0.8rem 2rem;
            margin-bottom: 2rem;
            border: 1px solid rgba(0,255,255,0.2);
            box-shadow: 0 0 20px rgba(0,180,220,0.2);
        }

        .logo i {
            font-size: 2rem;
            color: #0ff;
            margin-left: 0.5rem;
        }

        .nav-links {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .nav-links a {
            color: #eef5ff;
            text-decoration: none;
            font-weight: 500;
            padding: 0.5rem 1rem;
            border-radius: 40px;
            transition: 0.2s;
            letter-spacing: 0.5px;
            position: relative;
        }

        .nav-links a:hover, .nav-links a.active {
            background: rgba(0, 255, 255, 0.2);
            text-shadow: 0 0 6px cyan;
            box-shadow: 0 0 10px rgba(0,255,255,0.4);
        }

        /* Page sections */
        .page {
            display: none;
            animation: fadeSlide 0.5s ease-out;
            background: rgba(8, 12, 25, 0.55);
            backdrop-filter: blur(2px);
            border-radius: 2rem;
            padding: 2rem;
            margin-top: 1rem;
            border: 1px solid rgba(0, 255, 255, 0.25);
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .active-page {
            display: block;
        }

        @keyframes fadeSlide {
            from { opacity: 0; transform: translateY(15px);}
            to { opacity: 1; transform: translateY(0);}
        }

        /* Cards grid */
        .services-grid, .features-grid, .faq-grid, .solutions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 1.8rem;
            margin-top: 2rem;
        }

        .card {
            background: rgba(0, 0, 0, 0.65);
            backdrop-filter: blur(5px);
            border-radius: 1.5rem;
            padding: 1.5rem;
            transition: 0.25s;
            border: 1px solid rgba(0, 255, 255, 0.3);
            box-shadow: 0 8px 20px rgba(0,0,0,0.5);
        }

        .card i {
            font-size: 2.5rem;
            color: #0ff;
            margin-bottom: 1rem;
        }

        .card h3 {
            margin-bottom: 0.8rem;
            font-size: 1.5rem;
        }

        .card p {
            color: #ccddf8;
            line-height: 1.5;
        }

        .card:hover {
            transform: translateY(-8px);
            border-color: #0ff;
            box-shadow: 0 0 25px rgba(0,255,255,0.4);
        }

        /* animated transparent glowing boxes for benefits */
        .benefits-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 1.8rem;
            margin-top: 2rem;
        }
        .benefit-card {
            background: rgba(15, 25, 45, 0.35);
            backdrop-filter: blur(12px);
            border-radius: 1.8rem;
            padding: 1.5rem;
            text-align: center;
            border: 1px solid rgba(0, 255, 255, 0.4);
            transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            animation: glowPulse 2.5s infinite ease-in-out;
            box-shadow: 0 0 15px rgba(0, 255, 255, 0.2);
        }
        .benefit-card:hover {
            transform: scale(1.02);
            border-color: #0ff;
            box-shadow: 0 0 35px rgba(0, 255, 255, 0.7);
            animation: none;
        }
        @keyframes glowPulse {
            0% {
                border-color: rgba(0, 255, 255, 0.2);
                box-shadow: 0 0 5px rgba(0, 255, 255, 0.1);
                background: rgba(15, 25, 45, 0.25);
            }
            50% {
                border-color: rgba(0, 255, 255, 0.9);
                box-shadow: 0 0 25px rgba(0, 255, 255, 0.6);
                background: rgba(20, 40, 70, 0.45);
            }
            100% {
                border-color: rgba(0, 255, 255, 0.2);
                box-shadow: 0 0 5px rgba(0, 255, 255, 0.1);
                background: rgba(15, 25, 45, 0.25);
            }
        }
        .benefit-card p {
            font-size: 1rem;
            font-weight: 500;
            letter-spacing: 0.3px;
            color: #eef5ff;
            text-shadow: 0 0 5px rgba(0,255,255,0.5);
        }
        .benefit-card i {
            font-size: 2rem;
            color: #0ff;
            margin-bottom: 0.8rem;
            display: inline-block;
            filter: drop-shadow(0 0 6px cyan);
        }

        /* Buttons */
        .btn {
            background: linear-gradient(95deg, #00b8b0, #0088aa);
            border: none;
            padding: 0.7rem 1.4rem;
            border-radius: 2rem;
            font-family: 'Cairo', sans-serif;
            font-weight: bold;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 0 8px cyan;
            font-size: 1rem;
        }

        .btn-outline {
            background: transparent;
            border: 1px solid #0ff;
            color: #0ff;
        }

        .btn:hover {
            transform: scale(1.02);
            background: #00d4ff;
            color: #010101;
            box-shadow: 0 0 15px cyan;
        }

        /* Form fields - oval transparent with gradient */
        .modern-input, .modern-textarea {
            width: 100%;
            padding: 0.9rem 1.5rem;
            margin: 0.8rem 0;
            background: rgba(20, 30, 55, 0.5);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(0, 255, 200, 0.6);
            border-radius: 60px;
            color: #ffffff;
            font-family: 'Cairo', sans-serif;
            font-size: 1rem;
            transition: all 0.3s ease;
            outline: none;
            box-shadow: 0 0 8px rgba(0, 255, 200, 0.2);
        }
        .modern-textarea {
            border-radius: 2rem;
            resize: vertical;
        }
        .modern-input:focus, .modern-textarea:focus {
            border-color: #0ff;
            background: rgba(30, 50, 85, 0.7);
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.5);
            transform: scale(1.01);
        }

        /* footer socials */
        .footer-social {
            margin-top: 3rem;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(12px);
            border-radius: 2rem;
            padding: 2rem;
            border: 1px solid rgba(0,255,255,0.3);
            text-align: center;
        }
        .social-icons {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin: 1.5rem 0;
            flex-wrap: wrap;
        }
        .social-icons a {
            color: #0ff;
            font-size: 2rem;
            transition: 0.2s;
            display: inline-block;
        }
        .social-icons a:hover {
            transform: scale(1.2);
            text-shadow: 0 0 15px cyan;
            color: white;
        }
        .contact-info p {
            margin: 0.5rem 0;
            font-size: 1rem;
        }
        hr {
            border-color: rgba(0,255,255,0.3);
            margin: 1rem 0;
        }

        .order-list {
            background: rgba(0,0,0,0.5);
            border-radius: 1rem;
            padding: 1rem;
        }

        .order-item {
            border-bottom: 1px solid cyan;
            padding: 1rem;
            margin-bottom: 0.5rem;
        }

        /* Responsive */
        @media (max-width: 780px) {
            .container { padding: 1rem; }
            nav { flex-direction: column; gap: 1rem; }
            h2 { font-size: 1.6rem; }
        }

        .status-badge {
            display: inline-block;
            padding: 0.2rem 1rem;
            border-radius: 30px;
            font-size: 0.75rem;
            font-weight: bold;
        }
        .status-pending { background: #f0b400; color: #1e1a00; }
        .status-progress { background: #0a6eff; color: white; }
        .status-completed { background: #00cc88; color: #002b1a; }
        .status-cancelled { background: #aa2e4e; color: white; }
        
        /* extra sections */
        .extra-sections {
            margin-top: 3rem;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }
        .info-block {
            background: rgba(5, 10, 25, 0.7);
            border-radius: 1.8rem;
            padding: 1.8rem;
            border: 1px solid rgba(0, 255, 255, 0.2);
            transition: 0.3s;
        }
        .info-block h3 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
            color: #0ff;
        }
        .solutions-grid div {
            padding: 0.5rem;
            font-size: 1rem;
        }

        /* Developer section */
        .developers-section {
            display: flex;
            justify-content: center;
            gap: 2.5rem;
            flex-wrap: wrap;
            margin: 1.5rem 0;
            padding: 1rem;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 3rem;
            border: 1px dashed rgba(0,255,255,0.4);
        }
        .dev-card {
            display: flex;
            align-items: center;
            gap: 0.8rem;
            background: rgba(0, 20, 40, 0.6);
            backdrop-filter: blur(10px);
            padding: 0.6rem 1.8rem;
            border-radius: 3rem;
            border: 1px solid rgba(0,255,200,0.5);
            transition: 0.2s;
        }
        .dev-card:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px cyan;
        }
        .fading-star {
            display: inline-block;
            font-size: 1.4rem;
            color: #ffdd44;
            text-shadow: 0 0 8px gold;
            animation: starFade 1.8s infinite ease-in-out;
        }
        @keyframes starFade {
            0% { opacity: 0.2; transform: scale(0.8); text-shadow: 0 0 2px gold;}
            50% { opacity: 1; transform: scale(1.3); text-shadow: 0 0 15px #ffaa33;}
            100% { opacity: 0.2; transform: scale(0.8); text-shadow: 0 0 2px gold;}
        }
        .dev-name {
            font-size: 1.3rem;
            font-weight: 600;
            background: linear-gradient(135deg, #aaffff, #00d4ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: 0.5px;
        }
        .dev-icon {
            font-size: 1.5rem;
            color: #0ff;
        }

        /* Auth forms */
        .auth-tabs {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
            border-bottom: 1px solid rgba(0,255,255,0.3);
        }
        .auth-tab {
            background: transparent;
            border: none;
            padding: 0.5rem 1.5rem;
            font-size: 1rem;
            cursor: pointer;
            color: #ccddf8;
            border-radius: 30px;
            transition: 0.2s;
        }
        .auth-tab.active {
            background: rgba(0,255,255,0.2);
            color: #0ff;
            text-shadow: 0 0 5px cyan;
        }
        .user-info {
            display: flex;
            align-items: center;
            gap: 1rem;
            background: rgba(0,255,255,0.1);
            padding: 0.3rem 1rem;
            border-radius: 40px;
        }
    </style>
</head>
<body>
<div class="stars" id="starsContainer"></div>
<div class="container">
    <nav>
        <div class="logo glow-text"><i class="fas fa-car-crash"></i> الحقني</div>
        <div class="nav-links" id="navLinks">
            <a href="#" data-page="home" class="active">🏠 الرئيسية</a>
            <a href="#" data-page="services">🛠️ الخدمات</a>
            <a href="#" data-page="request">📢 طلب مساعدة</a>
            <a href="#" data-page="myorders">📋 طلباتي</a>
            <a href="#" data-page="features">✨ الميزات</a>
            <a href="#" data-page="faq">❓ الأسئلة</a>
            <a href="#" data-page="contact">📞 تواصل</a>
        </div>
    </nav>

    <!-- PAGE: HOME مع تسجيل الدخول وإنشاء حساب -->
    <div id="home" class="page active-page">
        <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; margin-bottom: 1.5rem;">
            <h2 class="glow-text">⭐ مرحباً بك في الحقني</h2>
            <div id="authStatus"></div>
        </div>
        
        <!-- نموذج تسجيل الدخول / إنشاء حساب -->
        <div class="card" style="max-width: 500px; margin: 0 auto 2rem auto;">
            <div class="auth-tabs">
                <button class="auth-tab active" id="loginTabBtn">تسجيل الدخول</button>
                <button class="auth-tab" id="signupTabBtn">إنشاء حساب جديد</button>
            </div>
            <div id="loginForm">
                <input type="email" id="loginEmail" placeholder="البريد الإلكتروني" class="modern-input">
                <input type="password" id="loginPassword" placeholder="كلمة المرور" class="modern-input">
                <button id="loginBtn" class="btn" style="width:100%">دخول</button>
            </div>
            <div id="signupForm" style="display:none;">
                <input type="text" id="signupFullName" placeholder="الاسم الكامل" class="modern-input">
                <input type="email" id="signupEmail" placeholder="البريد الإلكتروني" class="modern-input">
                <input type="tel" id="signupPhone" placeholder="رقم الهاتف" class="modern-input">
                <input type="password" id="signupPassword" placeholder="كلمة المرور" class="modern-input">
                <button id="signupBtn" class="btn" style="width:100%">إنشاء حساب</button>
            </div>
            <div id="authMessage" style="margin-top: 0.5rem; font-size: 0.8rem; text-align: center;"></div>
        </div>
        
        <p style="font-size:1.2rem; margin-top:1rem;">تطبيق المساعدة العاجلة للسيارات والشاحنات في الجزائر — 24 ساعة، سرعة فائقة، خدمات متكاملة.</p>
        <div class="services-grid" style="margin-top:2rem;">
            <div class="card"><i class="fas fa-wrench"></i><h3>ميكانيكي متنقل</h3><p>إصلاح عاجل في موقع العطل.</p></div>
            <div class="card"><i class="fas fa-gas-pump"></i><h3>توصيل وقود</h3><p>نفذ البنزين؟ نوصل لك الوقود أينما كنت.</p></div>
            <div class="card"><i class="fas fa-oil-can"></i><h3>زيوت وقطع غيار</h3><p>توصيل الزيوت المناسبة وقطع الغيار.</p></div>
            <div class="card"><i class="fas fa-truck"></i><h3>ديبناج (سحب)</h3><p>شاحنة رفع لنقل سيارتك إلى أقرب ورشة.</p></div>
        </div>
        <div style="margin-top:2rem;text-align:center;">
            <button class="btn" id="quickRequestBtnHome">📱 اطلب المساعدة الآن</button>
        </div>

        <div class="extra-sections">
            <div class="info-block">
                <h3><i class="fas fa-lightbulb"></i> فكرة الموقع ورؤيته</h3>
                <p>“الحقني” هو منصة جزائرية ذكية تربط السائقين (شاحنات وسيارات) بأسرع مزودي خدمات الطوارئ على الطريق. فكرتنا تنبع من الحاجة الملحة إلى حل سريع ومنظم عند التعطل في المناطق النائية أو الطرق السريعة.</p>
            </div>
            <div class="info-block">
                <h3><i class="fas fa-mobile-alt"></i> شرح التطبيق</h3>
                <p>تطبيق “الحقني” يعمل كمساعد افتراضي دائم: بمجرد فتح التطبيق، تستطيع اختيار الخدمة المناسبة. يتم تحديد موقعك الجغرافي بدقة، وإرسال طلبك إلى أقرب مزود خدمة. يمكنك متابعة حالة طلبك من لوحة “طلباتي”.</p>
            </div>
            <div class="info-block">
                <h3><i class="fas fa-chart-line"></i> فوائد التطبيق</h3>
                <div class="benefits-grid">
                    <div class="benefit-card"><i class="fas fa-bolt"></i><p>سرعة الاستجابة - وصول المساعدة في أقل من 20 دقيقة</p></div>
                    <div class="benefit-card"><i class="fas fa-clock"></i><p>توفير الوقت والجهد - لا حاجة للبحث عن أرقام الورش</p></div>
                    <div class="benefit-card"><i class="fas fa-shield-alt"></i><p>الراحة والأمان - خدمة 24 ساعة</p></div>
                    <div class="benefit-card"><i class="fas fa-map-marker-alt"></i><p>دقة تحديد الموقع عبر GPS</p></div>
                    <div class="benefit-card"><i class="fas fa-concierge-bell"></i><p>تنوع الخدمات</p></div>
                    <div class="benefit-card"><i class="fas fa-gem"></i><p>مجاني بالكامل</p></div>
                </div>
            </div>
            <div class="info-block">
                <h3><i class="fas fa-exclamation-triangle"></i> المشكلات التي يعالجها التطبيق</h3>
                <div class="solutions-grid" style="grid-template-columns: repeat(auto-fill, minmax(240px,1fr)); margin-top:1rem;">
                    <div><i class="fas fa-car-side"></i> تعطل الشاحنات والسيارات</div>
                    <div><i class="fas fa-gas-pump"></i> نفاد الوقود</div>
                    <div><i class="fas fa-oil-can"></i> نقص الزيوت</div>
                    <div><i class="fas fa-tools"></i> أعطال ميكانيكية</div>
                    <div><i class="fas fa-truck"></i> الحاجة إلى سحب السيارة</div>
                    <div><i class="fas fa-map-marked-alt"></i> صعوبة إيجاد ورشة</div>
                    <div><i class="fas fa-location-dot"></i> صعوبة تحديد الموقع</div>
                    <div><i class="fas fa-clock"></i> بطء طلب المساعدة</div>
                </div>
            </div>
        </div>
    </div>

    <!-- باقي الصفحات مختصرة (SERVICES, REQUEST, MYORDERS, FEATURES, FAQ, CONTACT) -->
    <div id="services" class="page"><h2 class="glow-text">🚛 الخدمات</h2><div class="services-grid"><div class="card"><i class="fas fa-tools"></i><h3>إصلاح ميكانيكي</h3><p>ميكانيكي محترف يصل إلى موقعك</p></div><div class="card"><i class="fas fa-tint"></i><h3>توصيل الزيوت</h3><p>زيت محرك حسب الطلب</p></div><div class="card"><i class="fas fa-charging-station"></i><h3>توصيل الوقود</h3><p>بنزين، ديزل</p></div><div class="card"><i class="fas fa-car-battery"></i><h3>قطع غيار</h3><p>بطاريات وإطارات</p></div><div class="card"><i class="fas fa-map-marked-alt"></i><h3>توجيه إلى ورشات</h3><p>أقرب ورشة</p></div><div class="card"><i class="fas fa-truck-moving"></i><h3>خدمة السحب</h3><p>ديبناج مجهز</p></div></div></div>
    <div id="request" class="page"><h2 class="glow-text">📢 طلب مساعدة</h2><div class="card"><form id="helpRequestForm"><select id="serviceType" class="modern-input"><option>ميكانيكي متنقل</option><option>توصيل وقود</option><option>توصيل زيوت</option><option>ديبناج (سحب)</option></select><textarea id="problemDesc" class="modern-textarea" placeholder="وصف المشكلة"></textarea><input type="tel" id="phoneReq" placeholder="رقم هاتفك" class="modern-input" required><button type="button" id="getLocationBtn" class="btn-outline btn">تحديد موقعي</button><input type="text" id="locationLink" placeholder="رابط الموقع" class="modern-input"><button type="submit" class="btn">إرسال الطلب</button></form></div></div>
    <div id="myorders" class="page"><h2 class="glow-text">📋 طلباتي</h2><div id="ordersContainer" class="order-list"></div><button id="refreshOrdersBtn" class="btn-outline btn">تحديث</button></div>
    <div id="features" class="page"><h2 class="glow-text">💎 الميزات</h2><div class="features-grid"><div class="card"><i class="fas fa-bolt"></i><h3>هز الهاتف</h3><p>تبليغ سريع</p></div><div class="card"><i class="fas fa-moon"></i><h3>وضع ليلي</h3><p>نجوم متحركة</p></div><div class="card"><i class="fas fa-chart-line"></i><h3>متابعة الطلبات</h3><p>حالة فورية</p></div></div></div>
    <div id="faq" class="page"><h2 class="glow-text">❓ الأسئلة</h2><div class="faq-grid"><div class="card"><h3>كيف أطلب المساعدة؟</h3><p>اختر الخدمة وأرسل موقعك</p></div><div class="card"><h3>هل التطبيق مجاني؟</h3><p>نعم بالكامل</p></div></div></div>
    <div id="contact" class="page"><h2 class="glow-text">📞 تواصل</h2><div class="card"><p><i class="fas fa-envelope"></i> support@alhaqni.com</p><p><i class="fas fa-phone-alt"></i> 1555</p><div class="developers-section"><div class="dev-card"><span class="fading-star">⭐</span><span class="dev-name">دماني نعيمة</span></div><div class="dev-card"><span class="fading-star">⭐</span><span class="dev-name">بلعدل فاطيمة</span></div></div><hr><h3>الإبلاغ عن مشكلة</h3><form id="reportIssue"><textarea id="reportMsg" class="modern-textarea" placeholder="تفاصيل المشكلة"></textarea><button type="submit" class="btn">إرسال</button></form></div></div>

    <div class="footer-social">
        <div class="social-icons">
            <a href="#"><i class="fab fa-facebook-f"></i></a><a href="#"><i class="fab fa-instagram"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a><a href="#"><i class="fab fa-linkedin-in"></i></a>
        </div>
        <p>© 2025 الحقني</p>
    </div>
</div>

<script>
    // Supabase initialization
    const SUPABASE_URL = 'https://mpbnwlzlxnqkhugdxmtb.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1wYm53bHpseG5xa2h1Z2R4bXRiIiwicm9sZSI6ImFub24iLCJpYXQiOjE3Nzc1NTE4MjEsImV4cCI6MjA5MzEyNzgyMX0.l5GJ4Wiol38evG7GSX8GzENwyC_tKWd0-P4Y1gZ9kyI';
    const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    let currentUser = null;

    // UI Elements
    const loginFormDiv = document.getElementById('loginForm');
    const signupFormDiv = document.getElementById('signupForm');
    const loginTab = document.getElementById('loginTabBtn');
    const signupTab = document.getElementById('signupTabBtn');
    const authStatus = document.getElementById('authStatus');
    const authMessage = document.getElementById('authMessage');

    loginTab.addEventListener('click', () => {
        loginTab.classList.add('active');
        signupTab.classList.remove('active');
        loginFormDiv.style.display = 'block';
        signupFormDiv.style.display = 'none';
        authMessage.innerHTML = '';
    });
    signupTab.addEventListener('click', () => {
        signupTab.classList.add('active');
        loginTab.classList.remove('active');
        loginFormDiv.style.display = 'none';
        signupFormDiv.style.display = 'block';
        authMessage.innerHTML = '';
    });

    // تسجيل الدخول
    document.getElementById('loginBtn').addEventListener('click', async () => {
        const email = document.getElementById('loginEmail').value;
        const password = document.getElementById('loginPassword').value;
        if (!email || !password) { authMessage.innerHTML = '⚠️ الرجاء ملء جميع الحقول'; return; }
        const { data, error } = await supabase.auth.signInWithPassword({ email, password });
        if (error) { authMessage.innerHTML = '❌ ' + error.message; return; }
        authMessage.innerHTML = '✅ تم تسجيل الدخول بنجاح!';
        currentUser = data.user;
        updateAuthUI();
    });

    // إنشاء حساب
    document.getElementById('signupBtn').addEventListener('click', async () => {
        const fullName = document.getElementById('signupFullName').value;
        const email = document.getElementById('signupEmail').value;
        const phone = document.getElementById('signupPhone').value;
        const password = document.getElementById('signupPassword').value;
        if (!fullName || !email || !phone || !password) { authMessage.innerHTML = '⚠️ الرجاء ملء جميع الحقول'; return; }
        const { data, error } = await supabase.auth.signUp({ email, password });
        if (error) { authMessage.innerHTML = '❌ ' + error.message; return; }
        // إضافة بيانات المستخدم إلى جدول users (id, email, full_name, phone)
        if (data.user) {
            const { error: insertError } = await supabase
                .from('users')
                .insert([{ id: data.user.id, email: email, full_name: fullName, phone: phone }]);
            if (insertError) console.error('Insert error:', insertError);
        }
        authMessage.innerHTML = '✅ تم إنشاء الحساب! يمكنك تسجيل الدخول الآن.';
        loginTab.click();
        document.getElementById('signupFullName').value = '';
        document.getElementById('signupEmail').value = '';
        document.getElementById('signupPhone').value = '';
        document.getElementById('signupPassword').value = '';
    });

    // تسجيل الخروج
    window.logout = async () => {
        await supabase.auth.signOut();
        currentUser = null;
        updateAuthUI();
        authMessage.innerHTML = 'تم تسجيل الخروج';
    };

    function updateAuthUI() {
        if (currentUser) {
            authStatus.innerHTML = `<div class="user-info"><span>👤 ${currentUser.email}</span><button class="btn-outline" onclick="logout()" style="padding:0.3rem 0.8rem;">تسجيل خروج</button></div>`;
            // إظهار العناصر الخاصة بالمستخدم
        } else {
            authStatus.innerHTML = '<span style="opacity:0.7;">⚠️ غير مسجل الدخول</span>';
        }
    }

    // التحقق من الجلسة الحالية
    async function checkSession() {
        const { data: { session } } = await supabase.auth.getSession();
        if (session) {
            currentUser = session.user;
            updateAuthUI();
        }
    }
    checkSession();

    // Stars generation
    function generateMovingStars() {
        const starsDiv = document.getElementById('starsContainer');
        starsDiv.innerHTML = '';
        for(let i = 0; i < 200; i++) {
            let star = document.createElement('div');
            star.classList.add('star');
            star.style.width = (Math.random() * 3 + 1) + 'px';
            star.style.height = star.style.width;
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.animation = `floatStar ${8 + Math.random() * 15}s linear infinite`;
            star.style.animationDelay = Math.random() * 10 + 's';
            starsDiv.appendChild(star);
        }
    }
    generateMovingStars();

    // Page navigation
    const pages = ['home','services','request','myorders','features','faq','contact'];
    function showPage(pageId) {
        pages.forEach(p => document.getElementById(p).classList.remove('active-page'));
        document.getElementById(pageId).classList.add('active-page');
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.classList.remove('active');
            if(link.getAttribute('data-page') === pageId) link.classList.add('active');
        });
        window.scrollTo({ top: 0 });
    }
    document.querySelectorAll('.nav-links a').forEach(link => {
        link.addEventListener('click', (e) => { e.preventDefault(); showPage(link.getAttribute('data-page')); });
    });
    document.getElementById('quickRequestBtnHome')?.addEventListener('click', () => showPage('request'));

    // Orders (local storage for demo, linked to user)
    let orders = JSON.parse(localStorage.getItem('haqni_orders')) || [];
    function saveOrders() { localStorage.setItem('haqni_orders', JSON.stringify(orders)); }
    function renderOrders() {
        const container = document.getElementById('ordersContainer');
        if(!container) return;
        const userOrders = orders.filter(o => o.userId === currentUser?.id);
        if(userOrders.length === 0) { container.innerHTML = '<p>لا توجد طلبات</p>'; return; }
        container.innerHTML = '';
        userOrders.slice().reverse().forEach(order => {
            const div = document.createElement('div'); div.className = 'order-item';
            div.innerHTML = `<strong>${order.service}</strong><br>📞 ${order.phone}<br>📍 ${order.location}<br><span class="status-badge status-pending">${order.status}</span><br><small>${new Date(order.timestamp).toLocaleString()}</small>`;
            container.appendChild(div);
        });
    }
    window.addOrderLocal = function(service, phone, location, desc) {
        if(!currentUser) { alert('الرجاء تسجيل الدخول أولاً'); return false; }
        orders.push({ id: Date.now(), userId: currentUser.id, service, phone, location, description: desc, status: 'pending', timestamp: new Date().toISOString() });
        saveOrders(); renderOrders(); return true;
    };
    document.getElementById('helpRequestForm')?.addEventListener('submit', (e) => {
        e.preventDefault();
        if(!currentUser) { alert('يرجى تسجيل الدخول لتقديم طلب'); return; }
        const service = document.getElementById('serviceType').value;
        const phone = document.getElementById('phoneReq').value;
        const location = document.getElementById('locationLink').value || 'موقع غير محدد';
        const desc = document.getElementById('problemDesc').value;
        if(addOrderLocal(service, phone, location, desc)) {
            alert('تم إرسال الطلب بنجاح');
            e.target.reset();
            showPage('myorders');
        }
    });
    document.getElementById('getLocationBtn')?.addEventListener('click', () => {
        if(navigator.geolocation) navigator.geolocation.getCurrentPosition(pos => {
            document.getElementById('locationLink').value = `https://maps.google.com/?q=${pos.coords.latitude},${pos.coords.longitude}`;
        });
    });
    document.getElementById('refreshOrdersBtn')?.addEventListener('click', () => renderOrders());
    document.getElementById('reportIssue')?.addEventListener('submit', (e) => {
        e.preventDefault();
        alert('تم استلام بلاغك، شكراً لك');
        e.target.reset();
    });
    renderOrders();
</script>
</body>
</html>
