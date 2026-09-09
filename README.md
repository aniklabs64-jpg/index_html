# index_html
<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>🤖 بوت التداول الذكي</title>
    <style>
        /* ========== إعدادات عامة ========== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', 'Tahoma', 'Arial', sans-serif;
            background: #0a0e17;
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 10px;
        }
        
        .app-container {
            max-width: 420px;
            width: 100%;
            background: #1a1a2e;
            border-radius: 20px;
            padding: 15px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.8);
            margin: 10px auto;
            position: relative;
        }
        
        /* ========== شريط الحالة ========== */
        .status-bar {
            display: flex;
            justify-content: space-between;
            padding: 5px 0 15px 0;
            border-bottom: 1px solid #2a2a4e;
            margin-bottom: 15px;
            font-size: 12px;
            color: #888;
        }
        
        .status-bar .online {
            color: #4caf50;
        }
        
        .status-bar .offline {
            color: #f44336;
        }
        
        /* ========== العنوان ========== */
        .header {
            text-align: center;
            padding: 10px 0;
            margin-bottom: 15px;
        }
        
        .header h1 {
            color: #ffd700;
            font-size: 26px;
            font-weight: bold;
            text-shadow: 0 0 20px rgba(255,215,0,0.2);
        }
        
        .header .sub {
            color: #888;
            font-size: 12px;
            margin-top: 5px;
        }
        
        /* ========== بطاقة الرصيد ========== */
        .balance-card {
            background: linear-gradient(135deg, #16213e, #0f3460);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #2a3a6e;
        }
        
        .balance-card .label {
            font-size: 14px;
            color: #aaa;
        }
        
        .balance-card .amount {
            font-size: 28px;
            font-weight: bold;
            color: #ffd700;
        }
        
        .balance-card .deposit-btn {
            background: #4caf50;
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 10px;
            font-size: 14px;
            cursor: pointer;
            transition: transform 0.2s;
        }
        
        .balance-card .deposit-btn:hover {
            transform: scale(1.05);
        }
        
        .balance-card .deposit-btn:active {
            transform: scale(0.95);
        }
        
        /* ========== اختيار الأصل ========== */
        .asset-section {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .asset-section select {
            flex: 1;
            padding: 12px;
            background: #16213e;
            border: 1px solid #2a3a6e;
            border-radius: 10px;
            color: white;
            font-size: 16px;
            cursor: pointer;
            appearance: none;
            -webkit-appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='white' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: left 10px center;
            background-size: 20px;
            padding-right: 40px;
        }
        
        .asset-section select option {
            background: #1a1a2e;
            color: white;
        }
        
        .asset-section .analyze-btn {
            padding: 12px 25px;
            background: #e94560;
            border: none;
            border-radius: 10px;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s;
            white-space: nowrap;
        }
        
        .asset-section .analyze-btn:hover {
            background: #c73652;
        }
        
        .asset-section .analyze-btn:active {
            transform: scale(0.95);
        }
        
        /* ========== السعر الحالي ========== */
        .price-display {
            text-align: center;
            padding: 10px;
            background: #0d1117;
            border-radius: 10px;
            margin-bottom: 15px;
            font-size: 18px;
            color: #aaa;
            border: 1px solid #1a2a4e;
        }
        
        .price-display .price {
            color: #fff;
            font-weight: bold;
            font-size: 22px;
        }
        
        /* ========== بطاقة الإشارة ========== */
        .signal-card {
            background: #0d1117;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 15px;
            text-align: center;
            border: 2px solid #2a3a6e;
            transition: all 0.5s;
        }
        
        .signal-card .signal {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .signal-card .signal.buy {
            color: #4caf50;
        }
        
        .signal-card .signal.sell {
            color: #f44336;
        }
        
        .signal-card .signal.wait {
            color: #ffd700;
        }
        
        .signal-card .details {
            color: #888;
            font-size: 14px;
            margin-top: 10px;
        }
        
        .signal-card .details span {
            display: inline-block;
            margin: 0 10px;
        }
        
        /* ========== أزرار التداول ========== */
        .trade-buttons {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .trade-buttons button {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s;
        }
        
        .trade-buttons button:active {
            transform: scale(0.95);
        }
        
        .trade-buttons .buy-btn {
            background: #4caf50;
            color: white;
        }
        
        .trade-buttons .buy-btn:hover {
            background: #43a047;
        }
        
        .trade-buttons .sell-btn {
            background: #f44336;
            color: white;
        }
        
        .trade-buttons .sell-btn:hover {
            background: #d32f2f;
        }
        
        /* ========== زر تشغيل/إيقاف ========== */
        .toggle-bot {
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 15px;
        }
        
        .toggle-bot.running {
            background: #f44336;
            color: white;
        }
        
        .toggle-bot.running:hover {
            background: #d32f2f;
        }
        
        .toggle-bot.stopped {
            background: #4caf50;
            color: white;
        }
        
        .toggle-bot.stopped:hover {
            background: #43a047;
        }
        
        /* ========== سجل التوصيات ========== */
        .history-section {
            margin-top: 10px;
        }
        
        .history-section .title {
            color: #ffd700;
            font-size: 16px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .history-section .title .clear-btn {
            background: none;
            border: none;
            color: #f44336;
            cursor: pointer;
            font-size: 12px;
        }
        
        .history-list {
            max-height: 200px;
            overflow-y: auto;
            background: #0d1117;
            border-radius: 10px;
            padding: 5px;
        }
        
        .history-list::-webkit-scrollbar {
            width: 5px;
        }
        
        .history-list::-webkit-scrollbar-track {
            background: #1a1a2e;
            border-radius: 10px;
        }
        
        .history-list::-webkit-scrollbar-thumb {
            background: #e94560;
            border-radius: 10px;
        }
        
        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 12px;
            border-bottom: 1px solid #1a2a4e;
            font-size: 13px;
            color: #ccc;
        }
        
        .history-item:last-child {
            border-bottom: none;
        }
        
        .history-item .signal-badge {
            padding: 2px 10px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: bold;
        }
        
        .history-item .signal-badge.buy {
            background: #4caf50;
            color: white;
        }
        
        .history-item .signal-badge.sell {
            background: #f44336;
            color: white;
        }
        
        .history-item .signal-badge.wait {
            background: #ffd700;
            color: #1a1a2e;
        }
        
        .history-item .time {
            color: #666;
            font-size: 11px;
        }
        
        /* ========== نافذة الشحن المنبثقة ========== */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .modal-overlay.active {
            display: flex;
        }
        
        .modal {
            background: #1a1a2e;
            border-radius: 20px;
            max-width: 400px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            padding: 25px;
            border: 1px solid #2a3a6e;
        }
        
        .modal .modal-title {
            color: #ffd700;
            font-size: 22px;
            text-align: center;
            margin-bottom: 20px;
        }
        
        .modal .modal-close {
            float: left;
            background: none;
            border: none;
            color: #f44336;
            font-size: 24px;
            cursor: pointer;
        }
        
        .modal .method-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .modal .method-btn {
            padding: 15px 10px;
            border: 2px solid #2a3a6e;
            border-radius: 12px;
            background: #0d1117;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
            font-size: 13px;
        }
        
        .modal .method-btn:hover {
            border-color: #ffd700;
            transform: scale(1.02);
        }
        
        .modal .method-btn.selected {
            border-color: #ffd700;
            background: #16213e;
        }
        
        .modal .method-btn .icon {
            font-size: 28px;
            display: block;
            margin-bottom: 5px;
        }
        
        .modal .method-btn .name {
            font-weight: bold;
        }
        
        .modal .amount-input {
            width: 100%;
            padding: 12px;
            background: #0d1117;
            border: 1px solid #2a3a6e;
            border-radius: 10px;
            color: white;
            font-size: 18px;
            text-align: center;
            margin-bottom: 15px;
        }
        
        .modal .amount-input:focus {
            outline: none;
            border-color: #ffd700;
        }
        
        .modal .method-details {
            background: #0d1117;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 15px;
            font-size: 13px;
            color: #aaa;
            line-height: 1.8;
            display: none;
        }
        
        .modal .method-details.show {
            display: block;
        }
        
        .modal .method-details strong {
            color: #fff;
        }
        
        .modal .confirm-btn {
            width: 100%;
            padding: 14px;
            background: #4caf50;
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        .modal .confirm-btn:hover {
            background: #43a047;
        }
        
        .modal .confirm-btn:disabled {
            background: #444;
            cursor: not-allowed;
        }
        
        /* ========== رسائل التنبيه ========== */
        .toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: #1a1a2e;
            color: white;
            padding: 15px 30px;
            border-radius: 12px;
            border: 1px solid #2a3a6e;
            z-index: 2000;
            display: none;
            max-width: 90%;
            text-align: center;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
        }
        
        .toast.show {
            display: block;
            animation: slideUp 0.3s ease;
        }
        
        @keyframes slideUp {
            from { transform: translateX(-50%) translateY(30px); opacity: 0; }
            to { transform: translateX(-50%) translateY(0); opacity: 1; }
        }
        
        .toast.success {
            border-color: #4caf50;
        }
        
        .toast.error {
            border-color: #f44336;
        }
        
        /* ========== تحميل ========== */
        .loading {
            display: none;
            text-align: center;
            padding: 10px;
            color: #ffd700;
        }
        
        .loading.active {
            display: block;
        }
        
        .spinner {
            display: inline-block;
            width: 30px;
            height: 30px;
            border: 3px solid #2a3a6e;
            border-top: 3px solid #ffd700;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* ========== استجابة ========== */
        @media (max-width: 480px) {
            .app-container {
                padding: 10px;
                border-radius: 12px;
            }
            .balance-card .amount {
                font-size: 22px;
            }
            .header h1 {
                font-size: 20px;
            }
            .signal-card .signal {
                font-size: 20px;
            }
            .modal .method-grid {
                grid-template-columns: 1fr 1fr;
            }
        }
    </style>
</head>
<body>

<!-- ========== التطبيق ========== -->
<div class="app-container" id="app">
    
    <!-- شريط الحالة -->
    <div class="status-bar">
        <span id="botStatus">⏹ البوت: متوقف</span>
        <span id="telegramStatus">📱 تيليجرام: <span class="online">✅ متصل</span></span>
    </div>
    
    <!-- العنوان -->
    <div class="header">
        <h1>🤖 بوت التداول الذكي</h1>
        <div class="sub">📊 تحليل فني لحظي مع إشارات شراء/بيع</div>
    </div>
    
    <!-- بطاقة الرصيد -->
    <div class="balance-card">
        <div>
            <div class="label">💰 الرصيد</div>
            <div class="amount" id="balanceDisplay">$1,000.00</div>
        </div>
        <button class="deposit-btn" onclick="openDeposit()">💳 شحن</button>
    </div>
    
    <!-- اختيار الأصل -->
    <div class="asset-section">
        <select id="assetSelect" onchange="changeAsset()">
            <option value="الذهب">🥇 الذهب</option>
            <option value="الفضة">🥈 الفضة</option>
            <option value="الدولار">💵 الدولار</option>
            <option value="النفط">🛢️ النفط</option>
            <option value="بيتكوين">₿ بيتكوين</option>
            <option value="إيثريوم">⟠ إيثريوم</option>
            <option value="سولانا">◎ سولانا</option>
            <option value="سهم آبل">🍎 آبل</option>
            <option value="سهم تسلا">🚗 تسلا</option>
        </select>
        <button class="analyze-btn" onclick="analyzeAsset()">🔍 تحليل</button>
    </div>
    
    <!-- السعر الحالي -->
    <div class="price-display">
        <span>💰 السعر: </span>
        <span class="price" id="priceDisplay">--</span>
    </div>
    
    <!-- بطاقة الإشارة -->
    <div class="signal-card" id="signalCard">
        <div class="signal wait" id="signalText">⏳ انتظار</div>
        <div class="details">
            <span id="confidenceDisplay">🎯 الثقة: --</span>
            <span id="timeDisplay">⏰ وقت الدخول: --</span>
        </div>
        <div class="details" id="rsiDisplay" style="margin-top:5px;">📊 RSI: --</div>
    </div>
    
    <!-- أزرار التداول -->
    <div class="trade-buttons">
        <button class="buy-btn" onclick="quickBuy()">📈 شراء</button>
        <button class="sell-btn" onclick="quickSell()">📉 بيع</button>
    </div>
    
    <!-- زر تشغيل/إيقاف -->
    <button class="toggle-bot stopped" id="toggleBtn" onclick="toggleBot()">
        ▶ تشغيل البوت
    </button>
    
    <!-- سجل التوصيات -->
    <div class="history-section">
        <div class="title">
            <span>📋 آخر التوصيات</span>
            <button class="clear-btn" onclick="clearHistory()">🗑️ مسح</button>
        </div>
        <div class="history-list" id="historyList">
            <div class="history-item" style="color:#666;text-align:center;padding:20px;">
                لا توجد توصيات بعد
            </div>
        </div>
    </div>
</div>

<!-- ========== نافذة الشحن ========== -->
<div class="modal-overlay" id="depositModal">
    <div class="modal">
        <button class="modal-close" onclick="closeDeposit()">✕</button>
        <div class="modal-title">💳 شحن المحفظة</div>
        
        <div class="method-grid" id="methodGrid">
            <button class="method-btn" onclick="selectMethod('paypal')">
                <span class="icon">💳</span>
                <span class="name">PayPal</span>
            </button>
            <button class="method-btn" onclick="selectMethod('visa')">
                <span class="icon">💳</span>
                <span class="name">فيزا كارد</span>
            </button>
            <button class="method-btn" onclick="selectMethod('mastercard')">
                <span class="icon">💳</span>
                <span class="name">ماستر كارد</span>
            </button>
            <button class="method-btn" onclick="selectMethod('redotpay')">
                <span class="icon">📱</span>
                <span class="name">ريدوت باي</span>
            </button>
            <button class="method-btn" onclick="selectMethod('briedbmob')">
                <span class="icon">📱</span>
                <span class="name">بريدب موب</span>
            </button>
        </div>
        
        <input type="number" class="amount-input" id="depositAmount" placeholder="المبلغ ($)" value="10" min="1">
        
        <div class="method-details" id="methodDetails">
            <div id="methodDetailsContent"></div>
        </div>
        
        <button class="confirm-btn" id="confirmDepositBtn" onclick="confirmDeposit()" disabled>
            💳 تأكيد الشحن
        </button>
    </div>
</div>

<!-- ========== رسائل التنبيه ========== -->
<div class="toast" id="toast"></div>

<!-- ========== تحميل ========== -->
<div class="loading" id="loading">
    <div class="spinner"></div>
    <div style="margin-top:10px;">جاري التحليل...</div>
</div>

<!-- ========== JavaScript ========== -->
<script>
    // ==============================================================
    // ========== بيانات التطبيق ==========
    // ==============================================================
    
    const state = {
        balance: 1000.00,
        currentAsset: 'الذهب',
        currentPrice: 0,
        signal: 'انتظار',
        confidence: 'منخفضة',
        entryTime: null,
        rsi: 0,
        isRunning: false,
        history: [],
        selectedMethod: null,
        botInterval: null,
        priceHistory: [],
        position: null
    };
    
    // ========== بيانات طرق الدفع ==========
    const depositMethods = {
        paypal: {
            name: 'PayPal',
            icon: '💳',
            color: '#0070ba',
            details: '🔹 البريد الإلكتروني: trading@paypal.com\n🔹 العملة: USD\n🔹 الحد الأدنى: $10\n🔹 العمولة: 2.9% + $0.30',
            steps: [
                '1. افتح تطبيق PayPal',
                '2. اضغط على "إرسال"',
                '3. أدخل البريد: trading@paypal.com',
                '4. أدخل المبلغ المطلوب',
                '5. أرسل لقطة شاشة للعملية'
            ]
        },
        visa: {
            name: 'فيزا كارد',
            icon: '💳',
            color: '#1a1f71',
            details: '🔹 رقم البطاقة: 4444 3333 2222 1111\n🔹 تاريخ الانتهاء: 12/28\n🔹 CVV: 123\n🔹 الحد الأدنى: $5\n🔹 العمولة: 2.5%',
            steps: [
                '1. أدخل رقم البطاقة',
                '2. أدخل تاريخ الانتهاء',
                '3. أدخل رمز CVV',
                '4. أدخل المبلغ',
                '5. اضغط تأكيد الدفع'
            ]
        },
        mastercard: {
            name: 'ماستر كارد',
            icon: '💳',
            color: '#eb001b',
            details: '🔹 رقم البطاقة: 5555 4444 3333 2222\n🔹 تاريخ الانتهاء: 12/28\n🔹 CVV: 456\n🔹 الحد الأدنى: $5\n🔹 العمولة: 2.5%',
            steps: [
                '1. أدخل رقم البطاقة',
                '2. أدخل تاريخ الانتهاء',
                '3. أدخل رمز CVV',
                '4. أدخل المبلغ',
                '5. اضغط تأكيد الدفع'
            ]
        },
        redotpay: {
            name: 'ريدوت باي',
            icon: '📱',
            color: '#00b894',
            details: '🔹 رقم المحفظة: 1234567890\n🔹 العملة: USD\n🔹 الحد الأدنى: $1\n🔹 العمولة: 1%',
            steps: [
                '1. افتح تطبيق RedotPay',
                '2. اختر "إرسال"',
                '3. أدخل رقم المحفظة: 1234567890',
                '4. أدخل المبلغ',
                '5. أرسل تأكيد العملية'
            ]
        },
        briedbmob: {
            name: 'بريدب موب',
            icon: '📱',
            color: '#6c5ce7',
            details: '🔹 رقم المحفظة: 9876543210\n🔹 العملة: USD\n🔹 الحد الأدنى: $1\n🔹 العمولة: 1.5%',
            steps: [
                '1. افتح تطبيق BriedbMob',
                '2. اختر "تحويل"',
                '3. أدخل رقم المحفظة: 9876543210',
                '4. أدخل المبلغ',
                '5. أرسل تأكيد العملية'
            ]
        }
    };
    
    // ==============================================================
    // ========== الأسعار (محاكاة) ==========
    // ==============================================================
    
    const prices = {
        'الذهب': 1952.30,
        'الفضة': 23.45,
        'الدولار': 1.05,
        'النفط': 78.90,
        'بيتكوين': 45230.00,
        'إيثريوم': 3120.00,
        'سولانا': 145.00,
        'سهم آبل': 178.50,
        'سهم تسلا': 245.60
    };
    
    function getPrice(asset) {
        // محاكاة تغير السعر بشكل عشوائي
        const base = prices[asset] || 100;
        const change = (Math.random() - 0.5) * 0.5;
        const newPrice = base + change;
        return Math.round(newPrice * 100) / 100;
    }
    
    // ==============================================================
    // ========== الدوال الرئيسية ==========
    // ==============================================================
    
    function analyzeAsset() {
        const asset = document.getElementById('assetSelect').value;
        state.currentAsset = asset;
        
        // عرض تحميل
        document.getElementById('loading').classList.add('active');
        
        // محاكاة تحليل
        setTimeout(() => {
            const price = getPrice(asset);
            state.currentPrice = price;
            
            // تحليل عشوائي (محاكاة)
            const rsi = 20 + Math.random() * 60;
            state.rsi = Math.round(rsi);
            
            let signal, confidence, entryTime;
            
            if (rsi < 30) {
                signal = 'شراء';
                confidence = 'عالية';
                entryTime = new Date(Date.now() + 5 * 60000);
            } else if (rsi > 70) {
                signal = 'بيع';
                confidence = 'عالية';
                entryTime = new Date(Date.now() + 5 * 60000);
            } else if (rsi < 40) {
                signal = 'شراء ضعيف';
                confidence = 'متوسطة';
                entryTime = new Date(Date.now() + 3 * 60000);
            } else if (rsi > 60) {
                signal = 'بيع ضعيف';
                confidence = 'متوسطة';
                entryTime = new Date(Date.now() + 3 * 60000);
            } else {
                signal = 'انتظار';
                confidence = 'منخفضة';
                entryTime = null;
            }
            
            state.signal = signal;
            state.confidence = confidence;
            state.entryTime = entryTime;
            
            // تحديث الواجهة
            updateUI(price, signal, confidence, entryTime, state.rsi);
            
            // إضافة للسجل
            if (signal !== 'انتظار') {
                addHistory(asset, signal, price);
            }
            
            document.getElementById('loading').classList.remove('active');
            
            // إرسال إشعار التيليجرام (محاكاة)
            if (signal !== 'انتظار') {
                showToast(`📢 إشارة ${signal} على ${asset}`, 'success');
            }
        }, 1500);
    }
    
    function updateUI(price, signal, confidence, entryTime, rsi) {
        // تحديث السعر
        document.getElementById('priceDisplay').textContent = `$${price.toFixed(2)}`;
        
        // تحديث الإشارة
        const signalEl = document.getElementById('signalText');
        signalEl.textContent = `📊 ${signal}`;
        signalEl.className = 'signal';
        if (signal.includes('شراء')) {
            signalEl.classList.add('buy');
        } else if (signal.includes('بيع')) {
            signalEl.classList.add('sell');
        } else {
            signalEl.classList.add('wait');
        }
        
        // تحديث الثقة
        document.getElementById('confidenceDisplay').textContent = `🎯 الثقة: ${confidence}`;
        
        // تحديث وقت الدخول
        if (entryTime) {
            const timeStr = entryTime.toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' });
            document.getElementById('timeDisplay').textContent = `⏰ وقت الدخول: ${timeStr}`;
        } else {
            document.getElementById('timeDisplay').textContent = '⏰ وقت الدخول: --';
        }
        
        // تحديث RSI
        document.getElementById('rsiDisplay').textContent = `📊 RSI: ${rsi}`;
    }
    
    function changeAsset() {
        const asset = document.getElementById('assetSelect').value;
        state.currentAsset = asset;
        const price = getPrice(asset);
        state.currentPrice = price;
        document.getElementById('priceDisplay').textContent = `$${price.toFixed(2)}`;
    }
    
    // ==============================================================
    // ========== السجل ==========
    // ==============================================================
    
    function addHistory(asset, signal, price) {
        state.history.unshift({
            asset: asset,
            signal: signal,
            price: price,
            time: new Date().toLocaleString('ar-EG')
        });
        
        if (state.history.length > 20) {
            state.history.pop();
        }
        
        renderHistory();
    }
    
    function renderHistory() {
        const list = document.getElementById('historyList');
        
        if (state.history.length === 0) {
            list.innerHTML = `<div class="history-item" style="color:#666;text-align:center;padding:20px;">لا توجد توصيات بعد</div>`;
            return;
        }
        
        list.innerHTML = state.history.map(item => {
            const badgeClass = item.signal.includes('شراء') ? 'buy' : 
                              item.signal.includes('بيع') ? 'sell' : 'wait';
            return `
                <div class="history-item">
                    <span>${item.asset}</span>
                    <span class="signal-badge ${badgeClass}">${item.signal}</span>
                    <span>$${item.price.toFixed(2)}</span>
                    <span class="time">${item.time}</span>
                </div>
            `;
        }).join('');
    }
    
    function clearHistory() {
        state.history = [];
        renderHistory();
        showToast('🗑️ تم مسح السجل', 'success');
    }
    
    // ==============================================================
    // ========== التداول السريع ==========
    // ==============================================================
    
    function quickBuy() {
        if (state.signal.includes('شراء')) {
            showToast(`📈 تم فتح صفقة شراء على ${state.currentAsset}`, 'success');
        } else {
            showToast('⚠️ لا توجد إشارة شراء حالياً', 'error');
        }
    }
    
    function quickSell() {
        if (state.signal.includes('بيع')) {
            showToast(`📉 تم فتح صفقة بيع على ${state.currentAsset}`, 'success');
        } else {
            showToast('⚠️ لا توجد إشارة بيع حالياً', 'error');
        }
    }
    
    // ==============================================================
    // ========== البوت ==========
    // ==============================================================
    
    function toggleBot() {
        const btn = document.getElementById('toggleBtn');
        
        if (state.isRunning) {
            // إيقاف
            state.isRunning = false;
            clearInterval(state.botInterval);
            btn.textContent = '▶ تشغيل البوت';
            btn.className = 'toggle-bot stopped';
            document.getElementById('botStatus').textContent = '⏹ البوت: متوقف';
            showToast('⏹ تم إيقاف البوت', 'success');
        } else {
            // تشغيل
            state.isRunning = true;
            btn.textContent = '⏹ إيقاف البوت';
            btn.className = 'toggle-bot running';
            document.getElementById('botStatus').textContent = '▶ البوت: يعمل';
            
            // تحليل فوري
            analyzeAsset();
            
            // تحليل كل 30 ثانية
            state.botInterval = setInterval(() => {
                analyzeAsset();
            }, 30000);
            
            showToast('▶️ تم تشغيل البوت (تحليل كل 30 ثانية)', 'success');
        }
    }
    
    // ==============================================================
    // ========== الشحن ==========
    // ==============================================================
    
    function openDeposit() {
        document.getElementById('depositModal').classList.add('active');
        document.getElementById('methodDetails').classList.remove('show');
        document.getElementById('confirmDepositBtn').disabled = true;
        state.selectedMethod = null;
        document.querySelectorAll('.method-btn').forEach(b => b.classList.remove('selected'));
    }
    
    function closeDeposit() {
        document.getElementById('depositModal').classList.remove('active');
    }
    
    function selectMethod(methodId) {
        state.selectedMethod = methodId;
        
        // تحديث الأزرار
        document.querySelectorAll('.method-btn').forEach(b => b.classList.remove('selected'));
        document.querySelector(`.method-btn[onclick="selectMethod('${methodId}')"]`).classList.add('selected');
        
        // عرض التفاصيل
        const method = depositMethods[methodId];
        if (method) {
            const detailsEl = document.getElementById('methodDetails');
            const contentEl = document.getElementById('methodDetailsContent');
            
            contentEl.innerHTML = `
                <strong>${method.icon} ${method.name}</strong><br>
                <div style="margin:10px 0;color:#888;">${method.details.replace(/\n/g, '<br>')}</div>
                <strong>📌 الخطوات:</strong><br>
                ${method.steps.map(s => `• ${s}`).join('<br>')}
            `;
            
            detailsEl.classList.add('show');
            document.getElementById('confirmDepositBtn').disabled = false;
        }
    }
    
    function confirmDeposit() {
        if (!state.selectedMethod) {
            showToast('⚠️ الرجاء اختيار طريقة الدفع', 'error');
            return;
        }
        
        const amount = parseFloat(document.getElementById('depositAmount').value);
        if (isNaN(amount) || amount <= 0) {
            showToast('⚠️ الرجاء إدخال مبلغ صحيح', 'error');
            return;
        }
        
        const method = depositMethods[state.selectedMethod];
        
        // محاكاة الإيداع
        state.balance += amount;
        document.getElementById('balanceDisplay').textContent = `$${state.balance.toFixed(2)}`;
        
        showToast(`✅ تم إيداع $${amount.toFixed(2)} عبر ${method.name} بنجاح!`, 'success');
        closeDeposit();
    }
    
    // ==============================================================
    // ========== رسائل التنبيه ==========
    // ==============================================================
    
    function showToast(message, type = 'info') {
        const toast = document.getElementById('toast');
        toast.textContent = message;
        toast.className = 'toast show ' + type;
        
        clearTimeout(toast._timeout);
        toast._timeout = setTimeout(() => {
            toast.classList.remove('show');
        }, 4000);
    }
    
    // ==============================================================
    // ========== تهيئة ==========
    // ==============================================================
    
    // تهيئة السعر الأولي
    changeAsset();
    
    // إضافة بعض التوصيات التجريبية
    setTimeout(() => {
        addHistory('الذهب', 'شراء', 1952.30);
        addHistory('بيتكوين', 'انتظار', 45230.00);
        addHistory('الدولار', 'بيع', 1.05);
    }, 500);
    
    // تحديث الأسعار كل 10 ثواني
    setInterval(() => {
        if (!state.isRunning) {
            const price = getPrice(state.currentAsset);
            state.currentPrice = price;
            document.getElementById('priceDisplay').textContent = `$${price.toFixed(2)}`;
        }
    }, 10000);
    
    console.log('🤖 بوت التداول الذكي - النسخة الويب');
    console.log('📊 تم التحميل بنجاح!');
</script>

</body>
</html>
