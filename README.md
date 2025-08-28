<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sipariş Sistemi - Telefon Bildirimli</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4a2c2a;
            --tea: #C8E6C9;
            --coffee: #D7CCC8;
            --food: #FFECB3;
            --shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #e4e8f0 100%);
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 25px;
            background: white;
            border-radius: 15px;
            box-shadow: var(--shadow);
            position: relative;
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 10px;
            font-size: 2.2rem;
        }
        
        .logo {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: var(--primary);
        }
        
        .content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        @media (max-width: 768px) {
            .content {
                grid-template-columns: 1fr;
            }
        }
        
        .card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: var(--shadow);
            transition: transform 0.3s;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #555;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 14px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border 0.3s;
        }
        
        input:focus, select:focus, textarea:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 2px rgba(74, 44, 42, 0.2);
        }
        
        .btn-group {
            display: flex;
            gap: 12px;
            margin: 25px 0;
        }
        
        button {
            flex: 1;
            padding: 14px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .tea-btn {
            background-color: var(--tea);
            color: #2E7D32;
        }
        
        .coffee-btn {
            background-color: var(--coffee);
            color: #4E342E;
        }
        
        .food-btn {
            background-color: var(--food);
            color: #F57F17;
        }
        
        .submit-btn {
            background-color: var(--primary);
            color: white;
            width: 100%;
            padding: 16px;
        }
        
        button:hover {
            opacity: 0.9;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.15);
        }
        
        button.active {
            transform: translateY(0);
            box-shadow: inset 0 3px 5px rgba(0,0,0,0.2);
        }
        
        .orders-list {
            margin-top: 20px;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 10px;
        }
        
        .order-item {
            padding: 18px;
            border-radius: 10px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            animation: fadeIn 0.5s;
            transition: transform 0.2s;
        }
        
        .order-item:hover {
            transform: scale(1.02);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .tea-order {
            background-color: var(--tea);
            border-left: 5px solid #2E7D32;
        }
        
        .coffee-order {
            background-color: var(--coffee);
            border-left: 5px solid #4E342E;
        }
        
        .food-order {
            background-color: var(--food);
            border-left: 5px solid #F57F17;
        }
        
        .order-info {
            flex-grow: 1;
        }
        
        .order-name {
            font-weight: bold;
            font-size: 18px;
            color: #333;
        }
        
        .order-type {
            font-size: 15px;
            opacity: 0.9;
            margin: 5px 0;
        }
        
        .order-time {
            font-size: 13px;
            opacity: 0.7;
        }
        
        .notification-section {
            margin-top: 25px;
            grid-column: 1 / -1;
        }
        
        .notification {
            padding: 18px;
            background: #E3F2FD;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 5px solid #2196F3;
            display: flex;
            align-items: center;
            gap: 15px;
            animation: slideIn 0.5s;
        }
        
        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        }
        
        .notification-icon {
            font-size: 24px;
            color: #2196F3;
        }
        
        .notification-content {
            flex-grow: 1;
        }
        
        .notification-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .clear-btn {
            background-color: #f44336;
            color: white;
            margin-top: 10px;
            padding: 12px 20px;
        }
        
        .status {
            padding: 10px;
            border-radius: 5px;
            text-align: center;
            margin: 15px 0;
            font-weight: 500;
        }
        
        .status.success {
            background: #E8F5E9;
            color: #2E7D32;
        }
        
        .status.error {
            background: #FFEBEE;
            color: #C62828;
        }
        
        /* Telefon Bildirim Simülasyonu */
        .phone-notification {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 320px;
            background: white;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            z-index: 1000;
            overflow: hidden;
            animation: slideInRight 0.5s, fadeOut 0.5s 4.5s forwards;
            display: none;
            border: 1px solid #e0e0e0;
        }
        
        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        
        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; display: none; }
        }
        
        .notification-header {
            padding: 15px 20px;
            background: var(--primary);
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .notification-body {
            padding: 20px;
        }
        
        .notification-item {
            margin-bottom: 10px;
            display: flex;
        }
        
        .notification-label {
            font-weight: bold;
            min-width: 80px;
            color: #555;
        }
        
        .notification-value {
            flex-grow: 1;
        }
        
        .notification-close {
            background: none;
            border: none;
            color: white;
            font-size: 18px;
            cursor: pointer;
            padding: 0;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .phone-icon {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 24px;
            color: var(--primary);
        }
        
        /* Telefon simülasyonu için ek stiller */
        .phone-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 999;
        }
        
        .phone {
            width: 300px;
            height: 600px;
            background: #222;
            border-radius: 40px;
            padding: 20px;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
            position: relative;
            border: 4px solid #444;
        }
        
        .phone-screen {
            width: 100%;
            height: 100%;
            background: #111;
            border-radius: 30px;
            overflow: hidden;
            position: relative;
            display: flex;
            flex-direction: column;
        }
        
        .phone-status-bar {
            height: 25px;
            background: #000;
            color: white;
            display: flex;
            justify-content: space-between;
            padding: 0 15px;
            align-items: center;
            font-size: 12px;
        }
        
        .phone-notification-list {
            flex-grow: 1;
            overflow-y: auto;
            padding: 10px;
            background: #222;
        }
        
        .phone-notification-item {
            background: #1c1c1e;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 10px;
            color: white;
            font-size: 14px;
        }
        
        .phone-notification-app {
            font-weight: bold;
            color: #8e8e93;
            margin-bottom: 5px;
        }
        
        .phone-notification-title {
            font-weight: bold;
            margin-bottom: 5px;
            color: #fff;
        }
        
        .phone-notification-content {
            color: #8e8e93;
        }
        
        .phone-home-button {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 50px;
            background: #333;
            border-radius: 50%;
            border: 2px solid #555;
        }
        
        .toggle-phone {
            position: absolute;
            top: -40px;
            right: 0;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            padding: 10px 15px;
            cursor: pointer;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-coffee"></i>
                <i class="fas fa-utensils"></i>
                <i class="fas fa-bell"></i>
            </div>
            <h1>Telefon Bildirimli Sipariş Sistemi</h1>
            <p>Sipariş verin, telefon bildirimi olarak gösterilsin!</p>
            <i class="fas fa-mobile-alt phone-icon"></i>
        </header>
        
        <div class="content">
            <section class="card">
                <h2><i class="fas fa-concierge-bell"></i> Sipariş Ver</h2>
                <div class="form-group">
                    <label for="name">İsim:</label>
                    <input type="text" id="name" placeholder="Adınızı girin">
                </div>
                
                <div class="form-group">
                    <label for="phone">Telefonunuz:</label>
                    <input type="text" id="phone" placeholder="Telefon numaranız">
                </div>
                
                <div class="btn-group">
                    <button class="tea-btn" onclick="selectType('çay')">
                        <i class="fas fa-mug-hot"></i> Çay
                    </button>
                    <button class="coffee-btn" onclick="selectType('kahve')">
                        <i class="fas fa-coffee"></i> Kahve
                    </button>
                    <button class="food-btn" onclick="selectType('yemek')">
                        <i class="fas fa-utensils"></i> Yemek
                    </button>
                </div>
                
                <div class="form-group">
                    <label for="details">Detaylar:</label>
                    <input type="text" id="details" placeholder="Örneğin: Türk kahvesi, tost, vs.">
                </div>
                
                <button class="submit-btn" onclick="addOrder()">
                    <i class="fas fa-paper-plane"></i> Siparişi Gönder
                </button>
            </section>
            
            <section class="card">
                <h2><i class="fas fa-history"></i> Son Siparişler</h2>
                <div class="orders-list" id="ordersList">
                    <!-- Siparişler buraya dinamik olarak eklenecek -->
                </div>
            </section>
            
            <section class="card notification-section">
                <h2><i class="fas fa-bell"></i> Bildirim Geçmişi</h2>
                <div id="notifications">
                    <!-- Bildirimler buraya eklenecek -->
                </div>
                
                <button class="clear-btn" onclick="clearNotifications()">
                    <i class="fas fa-trash"></i> Bildirimleri Temizle
                </button>
            </section>
        </div>
    </div>

    <!-- Telefon Bildirim Kutusu -->
    <div class="phone-notification" id="phoneNotification">
        <div class="notification-header">
            <span><i class="fas fa-bell"></i> Yeni Sipariş!</span>
            <button class="notification-close" onclick="closeNotification()">
                <i class="fas fa-times"></i>
            </button>
        </div>
        <div class="notification-body" id="notificationBody">
            <!-- Bildirim içeriği buraya eklenecek -->
        </div>
    </div>

    <!-- Telefon Simülasyonu -->
    <div class="phone-container">
        <button class="toggle-phone" onclick="togglePhone()">Telefonu Gizle</button>
        <div class="phone" id="phoneSimulation">
            <div class="phone-screen">
                <div class="phone-status-bar">
                    <span>19:30</span>
                    <span>
                        <i class="fas fa-signal"></i>
                        <i class="fas fa-wifi"></i>
                        <i class="fas fa-battery-full"></i>
                    </span>
                </div>
                <div class="phone-notification-list" id="phoneNotificationList">
                    <div class="phone-notification-item">
                        <div class="phone-notification-app">Sipariş Sistemi</div>
                        <div class="phone-notification-title">Hoş Geldiniz</div>
                        <div class="phone-notification-content">Sipariş bildirimleri burada görünecek</div>
                    </div>
                </div>
                <div class="phone-home-button"></div>
            </div>
        </div>
    </div>

    <script>
        let selectedType = '';
        let phoneVisible = true;
        
        // Sayfa yüklendiğinde
        window.onload = function() {
            // Kaydedilmiş siparişleri yükle
            loadOrders();
            
            // Örnek siparişleri göster
            addExampleOrders();
        };
        
        function selectType(type) {
            selectedType = type;
            // Seçilen butonu vurgula
            document.querySelectorAll('.btn-group button').forEach(btn => {
                btn.classList.remove('active');
            });
            
            if (type === 'çay') {
                document.querySelector('.tea-btn').classList.add('active');
            } else if (type === 'kahve') {
                document.querySelector('.coffee-btn').classList.add('active');
            } else if (type === 'yemek') {
                document.querySelector('.food-btn').classList.add('active');
            }
        }
        
        function addOrder() {
            const name = document.getElementById('name').value;
            const phone = document.getElementById('phone').value;
            const details = document.getElementById('details').value;
            
            if (!name || !phone || !selectedType) {
                showStatus('Lütfen isim, telefon ve sipariş türünü girin!', 'error');
                return;
            }
            
            const now = new Date();
            const time = now.toLocaleTimeString('tr-TR', { hour: '2-digit', minute: '2-digit' });
            const date = now.toLocaleDateString('tr-TR');
            
            // Sipariş nesnesi oluştur
            const order = {
                id: Date.now(),
                name,
                phone,
                type: selectedType,
                details,
                time,
                date
            };
            
            // Siparişi listeye ekle
            addOrderToList(order);
            
            // Siparişleri localStorage'a kaydet
            saveOrder(order);
            
            // Telefon bildirimi göster
            showPhoneNotification(order);
            
            // Formu temizle
            document.getElementById('name').value = '';
            document.getElementById('phone').value = '';
            document.getElementById('details').value = '';
            selectedType = '';
            
            document.querySelectorAll('.btn-group button').forEach(btn => {
                btn.classList.remove('active');
            });
        }
        
        function addOrderToList(order) {
            const ordersList = document.getElementById('ordersList');
            const orderItem = document.createElement('div');
            
            let orderClass = '';
            let icon = '';
            if (order.type === 'çay') {
                orderClass = 'tea-order';
                icon = '<i class="fas fa-mug-hot"></i>';
            } else if (order.type === 'kahve') {
                orderClass = 'coffee-order';
                icon = '<i class="fas fa-coffee"></i>';
            } else if (order.type === 'yemek') {
                orderClass = 'food-order';
                icon = '<i class="fas fa-utensils"></i>';
            }
            
            orderItem.className = `order-item ${orderClass}`;
            orderItem.innerHTML = `
                <div class="order-info">
                    <div class="order-name">${icon} ${order.name}</div>
                    <div class="order-type">${order.details || order.type}</div>
                    <div class="order-time">${order.date} ${order.time}</div>
                </div>
                <div class="order-phone">${order.phone}</div>
            `;
            
            ordersList.prepend(orderItem);
        }
        
        function createNotification(message, time) {
            const notificationsContainer = document.getElementById('notifications');
            const notification = document.createElement('div');
            notification.className = 'notification';
            notification.innerHTML = `
                <div class="notification-icon">
                    <i class="fas fa-bell"></i>
                </div>
                <div class="notification-content">
                    <div class="notification-title">Yeni Sipariş Bildirimi!</div>
                    <p>${message}</p>
                    <div class="order-time">${time}</div>
                </div>
            `;
            
            notificationsContainer.prepend(notification);
        }
        
        function clearNotifications() {
            const notificationsContainer = document.getElementById('notifications');
            notificationsContainer.innerHTML = '';
        }
        
        function saveOrder(order) {
            // localStorage'dan mevcut siparişleri al
            let orders = JSON.parse(localStorage.getItem('orders')) || [];
            
            // Yeni siparişi ekle
            orders.unshift(order);
            
            // En son 50 siparişi tut
            if (orders.length > 50) {
                orders = orders.slice(0, 50);
            }
            
            // localStorage'a kaydet
            localStorage.setItem('orders', JSON.stringify(orders));
        }
        
        function loadOrders() {
            const orders = JSON.parse(localStorage.getItem('orders')) || [];
            const ordersList = document.getElementById('ordersList');
            
            // Listeyi temizle
            ordersList.innerHTML = '';
            
            // Siparişleri listeye ekle
            orders.forEach(order => {
                addOrderToList(order);
            });
        }
        
        function addExampleOrders() {
            const ordersList = document.getElementById('ordersList');
            if (ordersList.children.length === 0) {
                const examples = [
                    {
                        name: "Ahmet",
                        phone: "5551234567",
                        type: "çay",
                        details: "",
                        date: "26.08.2023",
                        time: "10:30"
                    },
                    {
                        name: "Ayşe",
                        phone: "5557654321",
                        type: "kahve",
                        details: "Türk kahvesi",
                        date: "26.08.2023",
                        time: "11:15"
                    }
                ];
                
                examples.forEach(order => {
                    addOrderToList(order);
                });
            }
        }
        
        function showPhoneNotification(order) {
            const notification = document.getElementById('phoneNotification');
            const notificationBody = document.getElementById('notificationBody');
            
            // Bildirim içeriğini oluştur
            let icon = '';
            if (order.type === 'çay') {
                icon = '<i class="fas fa-mug-hot" style="color: #2E7D32;"></i>';
            } else if (order.type === 'kahve') {
                icon = '<i class="fas fa-coffee" style="color: #4E342E;"></i>';
            } else if (order.type === 'yemek') {
                icon = '<i class="fas fa-utensils" style="color: #F57F17;"></i>';
            }
            
            notificationBody.innerHTML = `
                <div class="notification-item">
                    <span class="notification-label">Müşteri:</span>
                    <span class="notification-value">${order.name}</span>
                </div>
                <div class="notification-item">
                    <span class="notification-label">Telefon:</span>
                    <span class="notification-value">${order.phone}</span>
                </div>
                <div class="notification-item">
                    <span class="notification-label">Sipariş:</span>
                    <span class="notification-value">${icon} ${order.details || order.type}</span>
                </div>
                <div class="notification-item">
                    <span class="notification-label">Zaman:</span>
                    <span class="notification-value">${order.date} ${order.time}</span>
                </div>
            `;
            
            // Telefon bildirim listesine ekle
            addToPhoneNotificationList(order);
            
            // Bildirimi göster
            notification.style.display = 'block';
            
            // Bildirimi bildirim geçmişine ekle
            const now = new Date();
            const time = now.toLocaleTimeString('tr-TR', { hour: '2-digit', minute: '2-digit' });
            const date = now.toLocaleDateString('tr-TR');
            createNotification(`${order.name} ${order.details || order.type} siparişi verdi.`, `${date} ${time}`);
            
            // 5 saniye sonra bildirimi otomatik kapat
            setTimeout(() => {
                notification.style.display = 'none';
            }, 5000);
        }
        
        function addToPhoneNotificationList(order) {
            const phoneNotificationList = document.getElementById('phoneNotificationList');
            const notificationItem = document.createElement('div');
            notificationItem.className = 'phone-notification-item';
            
            let orderText = '';
            if (order.type === 'çay') {
                orderText = 'Çay Siparişi';
            } else if (order.type === 'kahve') {
                orderText = 'Kahve Siparişi';
            } else if (order.type === 'yemek') {
                orderText = 'Yemek Siparişi';
            }
            
            notificationItem.innerHTML = `
                <div class="phone-notification-app">Sipariş Sistemi</div>
                <div class="phone-notification-title">${order.name}</div>
                <div class="phone-notification-content">${order.details || orderText} - ${order.time}</div>
            `;
            
            phoneNotificationList.prepend(notificationItem);
        }
        
        function closeNotification() {
            const notification = document.getElementById('phoneNotification');
            notification.style.display = 'none';
        }
        
        function showStatus(message, type) {
            // Önceki durum mesajlarını temizle
            const existingStatus = document.querySelector('.status');
            if (existingStatus) {
                existingStatus.remove();
            }
            
            // Yeni durum mesajı oluştur
            const status = document.createElement('div');
            status.className = `status ${type}`;
            status.textContent = message;
            
            // Formun altına ekle
            const form = document.querySelector('.card');
            form.appendChild(status);
            
            // 3 saniye sonra kaldır
            setTimeout(() => {
                status.remove();
            }, 3000);
        }
        
        function togglePhone() {
            const phone = document.getElementById('phoneSimulation');
            const toggleBtn = document.querySelector('.toggle-phone');
            
            if (phoneVisible) {
                phone.style.display = 'none';
                toggleBtn.textContent = 'Telefonu Göster';
                phoneVisible = false;
            } else {
                phone.style.display = 'block';
                toggleBtn.textContent = 'Telefonu Gizle';
                phoneVisible = true;
            }
        }
    </script>
</body>
</html>
