<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CuxeXstud10</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

        * {
            box-sizing: border-box;
            user-select: none;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Press Start 2P', monospace;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            background: linear-gradient(180deg, #050b14 0%, #0a192f 50%, #1e3a8a 100%);
            background-size: cover;
            background-position: center;
            color: #fff;
            position: relative;
        }

        canvas#snow {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 3;
        }

        .landscape-bg {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .container {
            position: relative;
            z-index: 10;
            background: rgba(15, 23, 42, 0.92);
            border: 4px solid #7dd3fc;
            box-shadow: 0 0 20px rgba(56, 189, 248, 0.5), 8px 8px 0px #000;
            padding: 25px 20px;
            max-width: 90%;
            width: 440px;
            text-align: center;
            backdrop-filter: blur(4px);
        }

        .title {
            font-size: 18px;
            color: #7dd3fc;
            text-shadow: 2px 2px 0px #0369a1;
            margin-bottom: 15px;
        }

        .subtitle {
            font-size: 8px;
            color: #e0f2fe;
            line-height: 1.6;
            margin-bottom: 20px;
        }

        .device-options {
            display: flex;
            gap: 12px;
            justify-content: center;
        }

        .card {
            background: #1e293b;
            border: 3px solid #38bdf8;
            padding: 15px 8px;
            cursor: pointer;
            flex: 1;
            box-shadow: 3px 3px 0px #000;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .card:hover {
            background: #0284c7;
            border-color: #ffffff;
            transform: translateY(-2px);
        }

        .pixel-icon {
            width: 40px;
            height: 40px;
            margin-bottom: 10px;
        }

        .card span {
            font-size: 7px;
            color: #ffffff;
        }

        .form-group {
            margin-bottom: 12px;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-size: 7px;
            color: #7dd3fc;
            margin-bottom: 6px;
        }

        .pixel-input {
            width: 100%;
            background: #0f172a;
            border: 2px solid #38bdf8;
            padding: 8px;
            color: #fff;
            font-family: 'Press Start 2P', monospace;
            font-size: 8px;
            outline: none;
        }

        .pixel-input.error {
            border-color: #f43f5e;
        }

        .error-msg {
            color: #f43f5e;
            font-size: 7px;
            margin-bottom: 10px;
            display: none;
            line-height: 1.4;
        }

        .screen { display: none; }
        .screen.active { display: block; }

        .menu-buttons {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 15px;
        }

        .pixel-btn {
            background: #0f172a;
            border: 2px solid #38bdf8;
            color: #fff;
            font-family: 'Press Start 2P', monospace;
            padding: 10px;
            font-size: 8px;
            cursor: pointer;
            box-shadow: 3px 3px 0 #000;
            width: 100%;
        }

        .pixel-btn:hover {
            background: #38bdf8;
            color: #000;
        }

        .btn-admin {
            border-color: #facc15;
            color: #facc15;
        }

        .btn-admin:hover {
            background: #facc15;
            color: #000;
        }

        .btn-back {
            margin-top: 15px;
            background: #f43f5e;
            border: 2px solid #fff;
            color: white;
            font-family: 'Press Start 2P', monospace;
            padding: 8px;
            font-size: 7px;
            cursor: pointer;
            box-shadow: 2px 2px 0 #000;
            width: 100%;
        }

        .user-badge {
            background: #1e293b;
            border: 2px dashed #7dd3fc;
            padding: 8px;
            font-size: 7px;
            margin-bottom: 15px;
            color: #facc15;
            line-height: 1.6;
        }

        .info-box {
            font-size: 7px;
            text-align: left;
            line-height: 1.8;
            background: #0f172a;
            border: 2px solid #38bdf8;
            padding: 12px;
            margin-bottom: 15px;
        }

        .file-upload-btn {
            display: block;
            text-align: center;
            background: #0284c7;
            color: white;
            padding: 8px;
            cursor: pointer;
            border: 2px solid #fff;
            margin-top: 8px;
            font-size: 7px;
        }
    </style>
</head>
<body>

    <!-- Векторный ночной фон -->
    <svg id="night-bg" class="landscape-bg" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMax slice">
        <polygon points="-50,500 200,250 450,500" fill="#1e293b" />
        <polygon points="150,500 450,200 750,500" fill="#0f172a" />
        <polygon points="500,500 750,280 1050,500" fill="#1e293b" />
        <polygon points="170,287 200,250 230,283 215,275 200,285 185,275" fill="#e2e8f0" />
        <rect x="800" y="50" width="30" height="30" fill="#fef08a" />
        <rect x="790" y="50" width="10" height="30" fill="#050b14" />
        <path d="M-50,500 Q 200,380 500,420 T 1050,500 Z" fill="#334155" />
        <path d="M-50,500 Q 150,440 500,450 T 1050,500 Z" fill="#cbd5e1" />
        <g transform="translate(180, 310)">
            <rect x="0" y="60" width="120" height="80" fill="#78350f" />
            <rect x="45" y="90" width="30" height="50" fill="#451a03" />
            <rect x="15" y="80" width="22" height="22" fill="#fef08a" />
            <polygon points="-10,60 60,10 130,60" fill="#991b1b" />
            <polygon points="-15,60 60,5 135,60 125,65 60,15 -5,65" fill="#f8fafc" />
        </g>
    </svg>

    <!-- Векторный дневной фон -->
    <svg id="day-bg" class="landscape-bg" viewBox="0 0 1000 500" preserveAspectRatio="xMidYMax slice" style="display:none;">
        <path d="M-50,500 Q 250,380 500,420 T 1050,500 Z" fill="#93c5fd" />
        <path d="M-50,500 Q 150,420 600,440 T 1050,500 Z" fill="#bfdbfe" />
        <path d="M-50,500 L-50,350 Q 200,360 400,420 T 1050,380 L1050,500 Z" fill="#f8fafc" />
    </svg>

    <canvas id="snow"></canvas>

    <div class="container">
        
        <!-- ЭКРАН 1: ВЫБОР УСТРОЙСТВА -->
        <div id="device-screen" class="screen active">
            <div class="title">CuxeXstud10</div>
            <div class="subtitle">WHAT DEVICE ARE YOU PLAYING ON?</div>
            
            <div class="device-options">
                <div class="card" onclick="selectDevice('PC / LAPTOP')">
                    <svg class="pixel-icon" viewBox="0 0 24 24" fill="#7dd3fc">
                        <path d="M2 2h20v14H2V2zm2 2v10h16V4H4zm5 14h6v2H9v-2zm-3 2h12v2H6v-2z"/>
                    </svg>
                    <span>PC / LAPTOP</span>
                </div>
                
                <div class="card" onclick="selectDevice('PHONE / TABLET')">
                    <svg class="pixel-icon" viewBox="0 0 24 24" fill="#7dd3fc">
                        <path d="M6 2h12v20H6V2zm2 2v16h8V4H8zm3 15h2v1h-2v-1z"/>
                    </svg>
                    <span>PHONE / TABLET</span>
                </div>
            </div>
        </div>

        <!-- ЭКРАН 2: ЛОГИН / РЕГИСТРАЦИЯ -->
        <div id="profile-screen" class="screen">
            <div class="title">ACCOUNT</div>
            <div class="subtitle">ENTER NICKNAME & PASSWORD</div>

            <div id="error-message" class="error-msg">⚠️ FILL IN ALL FIELDS!</div>

            <div class="form-group">
                <label>NICKNAME (*REQUIRED):</label>
                <input type="text" id="username" class="pixel-input" placeholder="Your nick" maxlength="12">
            </div>

            <div class="form-group">
                <label>PASSWORD (*REQUIRED):</label>
                <input type="password" id="userpass" class="pixel-input" placeholder="Your password">
            </div>

            <div class="form-group">
                <label>ADMIN KEY (OPTIONAL):</label>
                <input type="password" id="adminkey" class="pixel-input" placeholder="Admin key">
            </div>

            <button class="pixel-btn" onclick="saveProfile()">LOG IN / REGISTER</button>
        </div>

        <!-- ЭКРАН 3: ГЛАВНОЕ МЕНЮ -->
        <div id="main-screen" class="screen">
            <div class="title">CuxeXstud10</div>
            
            <div id="user-info" class="user-badge"></div>

            <div class="menu-buttons">
                <button class="pixel-btn" onclick="openScreen('device-screen')">🎮 HOME PLAY</button>
                <button class="pixel-btn" onclick="openScreen('credits-screen')">📜 CREDITS</button>
                <button class="pixel-btn" onclick="openScreen('settings-screen')">⚙️ SETTINGS</button>
                <button id="admin-panel-btn" class="pixel-btn btn-admin" style="display: none;">⚡ ADMIN PANEL</button>
            </div>

            <button class="btn-back" onclick="resetToStart()">🚪 LOG OUT</button>
        </div>

        <!-- ЭКРАН 4: CREDITS (/CREATORS) -->
        <div id="credits-screen" class="screen">
            <div class="title">/CREATORS</div>
            
            <div class="info-box">
                <p style="color: #7dd3fc; margin-bottom: 8px;"><b>DEVELOPERS:</b></p>
                <p>• ggs667751 animation site</p>
                <br>
                <p style="color: #7dd3fc; margin-bottom: 8px;"><b>SPECIAL THANKS:</b></p>
                <p>• Seronp2 for example nothing</p>
            </div>

            <button class="pixel-btn" onclick="openScreen('main-screen')">⬅ BACK TO MENU</button>
        </div>

        <!-- ЭКРАН 5: SETTINGS (НАСТРОЙКИ ФОНА) -->
        <div id="settings-screen" class="screen">
            <div class="title">SETTINGS</div>
            
            <div class="info-box">
                <p style="color: #7dd3fc; margin-bottom: 10px;">CHOOSE BACKGROUND:</p>
                
                <button class="pixel-btn" style="margin-bottom: 8px;" onclick="setBgPreset('night')">🌌 NIGHT PIXEL</button>
                <button class="pixel-btn" style="margin-bottom: 8px;" onclick="setBgPreset('day')">❄️ DAY SNOW</button>
                
                <p style="color: #7dd3fc; margin-top: 10px; margin-bottom: 5px;">CUSTOM IMAGE:</p>
                <label class="file-upload-btn">
                    📷 UPLOAD FROM GALLERY
                    <input type="file" id="bg-file-input" accept="image/*" style="display: none;" onchange="uploadCustomBg(event)">
                </label>
            </div>

            <button class="pixel-btn" onclick="openScreen('main-screen')">⬅ BACK TO MENU</button>
        </div>

    </div>

    <script>
        const ADMIN_SECRET = "1337";
        let userData = { device: '', name: '', isAdmin: false };
        let registeredUsers = {};

        try {
            registeredUsers = JSON.parse(localStorage.getItem('cuxe_users')) || {};
        } catch(e) {}

        function openScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
            document.getElementById(screenId).classList.add('active');
        }

        function selectDevice(deviceText) {
            userData.device = deviceText;
            openScreen('profile-screen');
        }

        function saveProfile() {
            const nameInput = document.getElementById('username');
            const passInput = document.getElementById('userpass');
            const adminInput = document.getElementById('adminkey');
            const errorMsg = document.getElementById('error-message');

            const nameValue = nameInput.value.trim();
            const passValue = passInput.value.trim();
            const adminValue = adminInput.value.trim();

            nameInput.classList.remove('error');
            passInput.classList.remove('error');
            errorMsg.style.display = 'none';

            if (nameValue === "" || passValue === "") {
                errorMsg.innerText = "⚠️ FILL IN NICKNAME AND PASSWORD!";
                errorMsg.style.display = 'block';

                if (nameValue === "") nameInput.classList.add('error');
                if (passValue === "") passInput.classList.add('error');
                return;
            }

            if (registeredUsers[nameValue]) {
                if (registeredUsers[nameValue] !== passValue) {
                    errorMsg.innerText = "⚠️ INCORRECT PASSWORD!";
                    errorMsg.style.display = 'block';
                    passInput.classList.add('error');
                    return;
                }
            } else {
                registeredUsers[nameValue] = passValue;
                try {
                    localStorage.setItem('cuxe_users', JSON.stringify(registeredUsers));
                } catch(e) {}
            }

            userData.name = nameValue;

            if (adminValue === ADMIN_SECRET) {
                userData.isAdmin = true;
            }

            openScreen('main-screen');

            const infoBox = document.getElementById('user-info');
            infoBox.innerHTML = `PLAYER: ${userData.name}<br>DEVICE: ${userData.device}` + 
                (userData.isAdmin ? `<br><span style="color:#facc15;">[ STATUS: ADMIN ]</span>` : '');

            if (userData.isAdmin) {
                document.getElementById('admin-panel-btn').style.display = 'block';
            }
        }

        function resetToStart() {
            userData.isAdmin = false;
            userData.name = '';
            document.getElementById('username').value = '';
            document.getElementById('userpass').value = '';
            document.getElementById('adminkey').value = '';
            document.getElementById('admin-panel-btn').style.display = 'none';
            openScreen('device-screen');
        }

        function setBgPreset(type) {
            document.body.style.backgroundImage = 'none';
            const nightBg = document.getElementById('night-bg');
            const dayBg = document.getElementById('day-bg');

            if (type === 'night') {
                document.body.style.background = 'linear-gradient(180deg, #050b14 0%, #0a192f 50%, #1e3a8a 100%)';
                nightBg.style.display = 'block';
                dayBg.style.display = 'none';
            } else if (type === 'day') {
                document.body.style.background = 'linear-gradient(180deg, #38bdf8 0%, #7dd3fc 40%, #bae6fd 70%, #e0f2fe 100%)';
                nightBg.style.display = 'none';
                dayBg.style.display = 'block';
            }
        }

        function uploadCustomBg(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.body.style.backgroundImage = `url('${e.target.result}')`;
                    document.getElementById('night-bg').style.display = 'none';
                    document.getElementById('day-bg').style.display = 'none';
                };
                reader.readAsDataURL(file);
            }
        }

        // Анимация снегопада
        const canvas = document.getElementById('snow');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);

        const flakes = Array.from({ length: 60 }, () => ({
            x: Math.random() * window.innerWidth,
            y: Math.random() * window.innerHeight,
            size: Math.floor(Math.random() * 3) + 2,
            speed: Math.random() * 1.2 + 0.5,
            drift: Math.random() * 0.6 - 0.3
        }));

        function drawSnow() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#ffffff';

            flakes.forEach(flake => {
                ctx.fillRect(Math.floor(flake.x), Math.floor(flake.y), flake.size, flake.size);
                flake.y += flake.speed;
                flake.x += flake.drift;

                if (flake.y > canvas.height) {
                    flake.y = -5;
                    flake.x = Math.random() * canvas.width;
                }
            });

            requestAnimationFrame(drawSnow);
        }
        drawSnow();
    </script>
</body>
</html>

