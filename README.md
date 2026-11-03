<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Garciabletna - Secure Elite Network</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #030303;
            --neon-green: #00FF66;
            --neon-glow: 0 0 20px rgba(0, 255, 102, 0.3);
            --card-bg: #0A0A0A;
            --border-color: #1a1a1a;
            --text-gray: #888888;
            --error-red: #FF3333;
        }

        body {
            background-color: var(--bg-color);
            color: #FFFFFF;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            height: 100vh;
            justify-content: space-between;
            align-items: center;
            overflow: hidden;
        }

        .screen {
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            width: 100%;
            max-width: 480px;
            padding: 20px;
            box-sizing: border-box;
        }

        .active-screen {
            display: flex;
        }

        .screen#app-screen {
            justify-content: flex-start;
            padding: 0;
            height: 100vh;
        }

        .main-container {
            width: 100%;
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            padding: 30px 25px;
            border-radius: 16px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.9);
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        h1 {
            color: var(--neon-green);
            text-shadow: var(--neon-glow);
            letter-spacing: 2px;
            font-size: 1.4rem;
            margin-bottom: 20px;
            font-family: 'Cinzel Decorative', cursive, sans-serif;
        }

        .input-field {
            width: 100%;
            background-color: #121212;
            border: 1px solid #222222;
            color: #FFFFFF;
            padding: 14px 16px;
            border-radius: 10px;
            font-size: 1rem;
            margin-bottom: 12px;
            outline: none;
            box-sizing: border-box;
            transition: all 0.3s ease;
        }

        .input-field:focus {
            border-color: var(--neon-green);
            box-shadow: 0 0 10px rgba(0, 255, 102, 0.2);
        }

        .error-msg {
            color: var(--error-red);
            font-size: 0.75rem;
            margin-bottom: 12px;
            text-align: left;
            width: 100%;
            display: none;
        }

        .btn-primary {
            width: 100%;
            background-color: var(--neon-green);
            color: #000000;
            border: none;
            padding: 14px;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 800;
            cursor: pointer;
            box-shadow: var(--neon-glow);
            transition: transform 0.1s ease;
        }

        .btn-primary:active {
            transform: scale(0.98);
        }

        /* Style Interface Instagram / Réseau Social */
        .app-header {
            width: 100%;
            padding: 15px 20px;
            background-color: var(--card-bg);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-sizing: border-box;
        }

        .app-content {
            flex: 1;
            width: 100%;
            overflow-y: auto;
            padding: 15px;
            box-sizing: border-box;
            display: none;
        }

        .app-content.active-tab {
            display: block;
        }

        /* Barre de navigation inférieure style Insta */
        .nav-bar {
            width: 100%;
            max-width: 480px;
            background-color: var(--card-bg);
            border-top: 1px solid var(--border-color);
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-sizing: border-box;
        }

        .nav-item {
            background: none;
            border: none;
            color: var(--text-gray);
            font-size: 1.3rem;
            cursor: pointer;
            transition: color 0.2s;
        }

        .nav-item.active {
            color: var(--neon-green);
            text-shadow: var(--neon-glow);
        }

        /* Cartes de profil / Feed */
        .profile-card {
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .profile-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .avatar {
            width: 45px;
            height: 45px;
            background-color: #1a1a1a;
            border: 1px solid var(--neon-green);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--neon-green);
            font-weight: bold;
        }

        .btn-follow {
            background-color: transparent;
            border: 1px solid var(--neon-green);
            color: var(--neon-green);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
            cursor: pointer;
        }

        .btn-follow.following {
            background-color: var(--neon-green);
            color: #000;
        }

        footer {
            width: 100%;
            max-width: 480px;
            text-align: center;
            padding: 10px 0;
            font-size: 0.65rem;
            color: var(--text-gray);
            border-top: 1px solid var(--border-color);
        }
    </style>
</head>
<body>

    <!-- ÉCRAN 1 : AUTHENTIFICATION / CONNEXION SÉCURISÉE -->
    <div id="auth-screen" class="screen active-screen">
        <div class="main-container">
            <h1>𝖌𝖆𝖗𝖈𝖎𝖆 𝖇𝖑𝖊𝖙𝖓𝖆</h1>
            <div style="font-size: 0.8rem; color: var(--neon-green); margin-bottom: 15px; font-weight: bold;">ACCÈS MONDIAL SÉCURISÉ</div>

            <input type="text" id="pseudo-input" class="input-field" placeholder="Pseudo (minuscules, sans espaces)..." oninput="formatPseudo(this)">
            <div id="pseudo-error" class="error-msg">⚠️ Min. 3 caractères (lettres/chiffres).</div>

            <input type="password" id="password-input" class="input-field" maxlength="8" placeholder="Mot de passe (4 à 8 caractères)...">
            <div id="password-error" class="error-msg">⚠️ Le mot de passe doit contenir entre 4 et 8 caractères.</div>

            <button class="btn-primary" onclick="handleAuth()">
                Connexion / Inscription 🔱
            </button>
        </div>
        <footer>PROPRIÉTÉ DE GARCIABLETNA — RÉSEAU D'ÉLITE 2026</footer>
    </div>

    <!-- ÉCRAN 2 : INTERFACE PRINCIPALE (STYLE INSTAGRAM / RÉSEAU) -->
    <div id="app-screen" class="screen">
        <div class="app-header">
            <span style="font-family: 'Cinzel Decorative', cursive; color: var(--neon-green); font-size: 1.1rem;">𝖌𝖆𝖗𝖈𝖎𝖆 𝖇𝖑𝖊𝖙𝖓𝖆 🔱</span>
            <span id="current-user-badge" style="font-size: 0.8rem; color: var(--neon-green); font-weight: bold;"></span>
        </div>

        <!-- Onglet 1 : Accueil / Feed -->
        <div id="tab-feed" class="app-content active-tab">
            <div style="font-size: 0.85rem; color: var(--text-gray); margin-bottom: 15px;">Fil d'actualité sécurisé de la communauté</div>
            <div class="profile-card">
                <div class="profile-info">
                    <div class="avatar">G</div>
                    <div>
                        <div style="font-weight: bold; font-size: 0.9rem;">garciabletna</div>
                        <div style="font-size: 0.75rem; color: var(--text-gray);">Fondateur du réseau</div>
                    </div>
                </div>
                <span style="font-size: 0.75rem; color: var(--neon-green);">Officiel</span>
            </div>
            <div id="feed-container"></div>
        </div>

        <!-- Onglet 2 : Recherche de Profils -->
        <div id="tab-search" class="app-content">
            <input type="text" id="search-input" class="input-field" placeholder="🔍 Rechercher un membre par son pseudo..." oninput="searchProfiles(this)">
            <div id="search-results" style="margin-top: 10px;">
                <!-- Les résultats de recherche s'afficheront ici -->
            </div>
        </div>

        <!-- Onglet 3 : Profil Personnel -->
        <div id="tab-profile" class="app-content" style="text-align: center; padding-top: 30px;">
            <div class="avatar" style="width: 80px; height: 80px; margin: 0 auto 15px; font-size: 2rem;" id="profile-initial">G</div>
            <h2 id="profile-pseudo-display" style="color: var(--neon-green); margin-bottom: 5px;">@pseudo</h2>
            <p style="font-size: 0.8rem; color: var(--text-gray); margin-bottom: 25px;">Membre authentifié du réseau Garciabletna</p>
            <button class="btn-primary" style="background-color: #1a1a1a; color: var(--error-red); border: 1px solid var(--error-red);" onclick="logout()">Déconnexion</button>
        </div>

        <!-- Barre de Navigation de Style Instagram -->
        <div class="nav-bar">
            <button class="nav-item active" onclick="switchTab('feed', this)">🏠</button>
            <button class="nav-item" onclick="switchTab('search', this)">🔍</button>
            <button class="nav-item" onclick="switchTab('profile', this)">👤</button>
        </div>
    </div>

    <script>
        function formatPseudo(input) {
            input.value = input.value.toLowerCase().replace(/\s+/g, '');
        }

        function handleAuth() {
            const pseudo = document.getElementById('pseudo-input').value.trim();
            const password = document.getElementById('password-input').value.trim();
            let isValid = true;

            const pseudoRegex = /^[a-z0-9_]{3,}$/;
            if (!pseudoRegex.test(pseudo)) {
                document.getElementById('pseudo-error').style.display = 'block';
                isValid = false;
            } else {
                document.getElementById('pseudo-error').style.display = 'none';
            }

            if (password.length < 4 || password.length > 8) {
                document.getElementById('password-error').style.display = 'block';
                isValid = false;
            } else {
                document.getElementById('password-error').style.display = 'none';
            }

            if (!isValid) return;

            // Gestion de la base de données locale sécurisée par compte
            let users = JSON.parse(localStorage.getItem('garcia_users') || '{}');
            
            if (users[pseudo]) {
                if (users[pseudo] !== password) {
                    alert("⚠️ Mot de passe incorrect pour ce pseudo !");
                    return;
                }
            } else {
                users[pseudo] = password;
                localStorage.setItem('garcia_users', JSON.stringify(users));
            }

            localStorage.setItem('garcia_current_user', pseudo);
            initApp(pseudo);
        }

        function initApp(pseudo) {
            document.getElementById('auth-screen').classList.remove('active-screen');
            document.getElementById('app-screen').classList.add('active-screen');
            document.getElementById('current-user-badge').innerText = "@" + pseudo;
            document.getElementById('profile-pseudo-display').innerText = "@" + pseudo;
            document.getElementById('profile-initial').innerText = pseudo.charAt(0).toUpperCase();
            loadMockUsers(pseudo);
        }

        function switchTab(tabName, btnElement) {
            document.querySelectorAll('.app-content').forEach(el => el.classList.remove('active-tab'));
            document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));

            if (tabName === 'feed') document.getElementById('tab-feed').classList.add('active-tab');
            if (tabName === 'search') document.getElementById('tab-search').classList.add('active-tab');
            if (tabName === 'profile') document.getElementById('tab-profile').classList.add('active-tab');

            btnElement.classList.add('active');
        }

        function loadMockUsers(currentUser) {
            const container = document.getElementById('search-results');
            const users = JSON.parse(localStorage.getItem('garcia_users') || '{}');
            
            container.innerHTML = "";
            for (let p in users) {
                if (p !== currentUser) {
                    container.innerHTML += `
                        <div class="profile-card">
                            <div class="profile-info">
                                <div class="avatar">${p.charAt(0).toUpperCase()}</div>
                                <div style="font-weight: bold;">@${p}</div>
                            </div>
                            <button class="btn-follow" onclick="toggleFollow(this)">S'abonner</button>
                        </div>
                    `;
                }
            }
        }

        function searchProfiles(input) {
            const query = input.value.toLowerCase();
            const container = document.getElementById('search-results');
            const users = JSON.parse(localStorage.getItem('garcia_users') || '{}');
            const currentUser = localStorage.getItem('garcia_current_user');

            container.innerHTML = "";
            for (let p in users) {
                if (p !== currentUser && p.includes(query)) {
                    container.innerHTML += `
                        <div class="profile-card">
                            <div class="profile-info">
                                <div class="avatar">${p.charAt(0).toUpperCase()}</div>
                                <div style="font-weight: bold;">@${p}</div>
                            </div>
                            <button class="btn-follow" onclick="toggleFollow(this)">S'abonner</button>
                        </div>
                    `;
                }
            }
        }

        function toggleFollow(btn) {
            if (btn.innerText === "S'abonner") {
                btn.innerText = "Abonné(e)";
                btn.classList.add('following');
            } else {
                btn.innerText = "S'abonner";
                btn.classList.remove('following');
            }
        }

        function logout() {
            localStorage.removeItem('garcia_current_user');
            location.reload();
        }

        // Vérification automatique de session active
        window.onload = function() {
            const activeUser = localStorage.getItem('garcia_current_user');
            if (activeUser) {
                initApp(activeUser);
            }
        }
    </script>
</body>
</html>

