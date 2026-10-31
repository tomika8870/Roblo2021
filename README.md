<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Roblo21 - Full 2021 Edition</title>
    <style>
        body { background-color: #191B1D; color: #FFFFFF; font-family: 'Arial', sans-serif; margin: 0; padding: 0; }
        .header { background-color: #232527; padding: 15px 30px; display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #393B3D; }
        .logo { font-size: 24px; font-weight: bold; color: #FFFFFF; letter-spacing: 1px; }
        .box { background-color: #232527; padding: 20px; border-radius: 8px; border: 1px solid #393B3D; max-width: 400px; margin: 40px auto; }
        .editor-container { display: flex; flex-wrap: wrap; padding: 20px; max-width: 1100px; margin: 0 auto; gap: 20px; }
        .avatar-view-box { flex: 1; min-width: 300px; background-color: #232527; padding: 20px; border-radius: 8px; border: 1px solid #393B3D; text-align: center; }
        .avatar-custom-box { flex: 2; min-width: 350px; background-color: #232527; padding: 20px; border-radius: 8px; border: 1px solid #393B3D; }
        input, select { width: 100%; padding: 10px; margin: 10px 0; background-color: #191B1D; border: 1px solid #393B3D; color: white; border-radius: 4px; box-sizing: border-box; }
        button { background-color: #0084FF; color: white; border: none; padding: 12px; width: 100%; font-weight: bold; border-radius: 4px; cursor: pointer; }
        button:hover { background-color: #0074E0; }
        .hidden { display: none; }
        .r2021-avatar { width: 100%; max-width: 250px; background: #191B1D; border: 2px solid #393B3D; border-radius: 6px; margin: 0 auto; padding: 15px; text-align: left; font-size: 14px; line-height: 1.6; }
        .skin-preview { width: 30px; height: 30px; display: inline-block; border-radius: 50%; border: 1px solid white; vertical-align: middle; }
        .skin-grid { display: flex; gap: 10px; margin: 10px 0; }
        .skin-color { width: 35px; height: 35px; border-radius: 4px; cursor: pointer; border: 2px solid transparent; }
    </style>
</head>
<body>

    <!-- LOGOWANIE i REJESTRACJA -->
    <div id="auth-panel" class="box">
        <h2>Wejdź do Roblo21</h2>
        <input type="text" id="username" placeholder="Nazwa użytkownika">
        <input type="password" id="password" placeholder="Hasło">
        <button onclick="handleAuth('login')">Zaloguj się</button>
        <p style="text-align:center; color:#AAAEB3; margin: 10px 0;">lub</p>
        <button style="background-color: #28A745;" onclick="handleAuth('register')">Stwórz nowe konto</button>
    </div>

    <!-- PANEL GŁÓWNY -->
    <div id="main-panel" class="hidden">
        <div class="header">
            <div class="logo">ROBLO21</div>
            <div>Witaj, <b id="user-display" style="color:#0084FF;"></b> | <span style="color:#00E676; font-weight:bold;">R$ <span id="robux-display"></span></span></div>
        </div>

        <div class="editor-container">
            <!-- PODGLĄD AVATARA 2021 -->
            <div class="avatar-view-box">
                <h3 style="margin-top:0;">Twój Awatar (Late 2021)</h3>
                <div class="r2021-avatar">
                    <div><b>Kolor skóry:</b> <span id="v-skin" class="skin-preview"></span></div>
                    <div><b>Głowa i Ciało:</b> <span id="v-body" style="color:#FF9800;"></span></div>
                    <div><b>Twarz:</b> <span id="v-face"></span></div>
                    <div><b>Włosy:</b> <span id="v-hair" style="color:#A1887F;"></span></div>
                    <div><b>Koszulka:</b> <span id="v-shirt" style="color:#2196F3;"></span></div>
                    <div><b>Podkoszulek (T-Shirt):</b> <span id="v-tshirt" style="color:#E91E63;"></span></div>
                    <div><b>Spodnie:</b> <span id="v-pants" style="color:#4CAF50;"></span></div>
                    <div><b>Akcesorium:</b> <span id="v-accessory" style="color:#9C27B0;"></span></div>
                    <hr style="border: 1px solid #393B3D; margin: 10px 0;">
                    <div><b>Animacja:</b> <span id="v-anim" style="color:#00BCD4; font-style:italic;"></span></div>
                    <div><b>Emotka:</b> <span id="v-emote" style="color:#F44336;"></span></div>
                </div>
            </div>

            <!-- MODYFIKACJA POSTACI -->
            <div class="avatar-custom-box">
                <h3 style="margin-top:0;">Dostosuj postać</h3>
                <label>Kolor skóry:</label>
                <div class="skin-grid">
                    <div class="skin-color" style="background-color: #E5A65E;" onclick="setSkin('#E5A65E')"></div>
                    <div class="skin-color" style="background-color: #FFCDA5;" onclick="setSkin('#FFCDA5')"></div>
                    <div class="skin-color" style="background-color: #7A5333;" onclick="setSkin('#7A5333')"></div>
                </div>

                <label>Głowa i Budowa ciała:</label>
                <select id="s-body" onchange="updateAvatar()">
                    <option value="Roblox Boy (R15)">Roblox Boy (R15) - 2021 Standard</option>
                    <option value="Blocky Classic (R6)">Blocky Classic (R6)</option>
                </select>

                <label>Klasyczne Twarze:</label>
                <select id="s-face" onchange="updateAvatar()">
                    <option value="Smile">Smile</option>
                    <option value="Winning Smile">Winning Smile (2021 Meme)</option>
                    <option value="Man Face">Man Face</option>
                </select>

                <label>Włosy:</label>
                <select id="s-hair" onchange="updateAvatar()">
                    <option value="Pal Hair (Bacon)">Bacon Hair</option>
                    <option value="Black Messy Hair">Black Messy Hair</option>
                </select>

                <label>Koszulki (Shirts):</label>
                <select id="s-shirt" onchange="updateAvatar()">
                    <option value="Classic Roblox Jacket">Classic Roblox Jacket</option>
                </select>

                <label>Podkoszulki (T-Shirts):</label>
                <select id="s-tshirt" onchange="updateAvatar()">
                    <option value="None">Brak nadruku</option>
                    <option value="Epic Face Print">Epic Face Print</option>
                </select>

                <label>Spodnie (Pants):</label>
                <select id="s-pants" onchange="updateAvatar()">
                    <option value="Black Slacks">Black Slacks</option>
                    <option value="Jeans with Sneakers">Jeans with Sneakers</option>
                </select>

                <label>Akcesoria:</label>
                <select id="s-accessory" onchange="updateAvatar()">
                    <option value="Roblox Cap 2021">Roblox Cap 2021</option>
                    <option value="Valkyrie Helmet">Valkyrie Helmet</option>
                </select>

                <label>Animacje:</label>
                <select id="s-anim" onchange="updateAvatar()">
                    <option value="Classic Default Walk">Classic Default Walk</option>
                    <option value="Cartoony Animation Pack">Cartoony Pack</option>
                </select>

                <label>Emotki:</label>
                <select id="s-emote" onchange="updateAvatar()">
                    <option value="Wave (/e wave)">Wave (/e wave)</option>
                </select>
            </div>
        </div>
    </div>

    <script>
        let loggedUser = "";
        let currentSkin = "#E5A65E";

        // Pobieranie "bazy danych" z pamięci przeglądarki
        function getUsersDB() {
            return JSON.parse(localStorage.getItem('roblo21_users')) || {};
        }

        function saveUsersDB(db) {
            localStorage.setItem('roblo21_users', JSON.stringify(db));
        }

        function handleAuth(type) {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value;
            if(!username || !password) return alert("Wpisz dane!");

            let db = getUsersDB();

            if (type === 'register') {
                if (db[username]) return alert("Ta nazwa jest zajęta!");
                db[username] = {
                    password: password,
                    robux: 1000,
                    avatar: { skin: '#E5A65E', head: 'Roblox Boy (R15)', face: 'Smile', hair: 'Bacon Hair', shirt: 'Classic Roblox Jacket', tshirt: 'None', pants: 'Black Slacks', accessory: 'Roblox Cap 2021', animation: 'Classic Default Walk', emote: 'Wave (/e wave)' }
                };
                saveUsersDB(db);
                alert("Konto utworzone w Roblo21! Zaloguj się teraz.");
            } else if (type === 'login') {
                if (!db[username] || db[username].password !== password) return alert("Zły login lub hasło!");
                
                loggedUser = username;
                document.getElementById('auth-panel').classList.add('hidden');
                document.getElementById('main-panel').classList.remove('hidden');
                document.getElementById('user-display').innerText = loggedUser;
                document.getElementById('robux-display').innerText = db[username].robux;
                
                currentSkin = db[username].avatar.skin;
                document.getElementById('s-body').value = db[username].avatar.head;
                document.getElementById('s-face').value = db[username].avatar.face;
                document.getElementById('s-hair').value = db[username].avatar.hair;
                document.getElementById('s-shirt').value = db[username].avatar.shirt;
                document.getElementById('s-tshirt').value = db[username].avatar.tshirt;
                document.getElementById('s-pants').value = db[username].avatar.pants;
