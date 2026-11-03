<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Garcia Bletna - Chat & Social</title>
    <style>
        :root {
            --primary-bg: #000000;
            --card-bg: #121212;
            --text-color: #ffffff;
            --text-secondary: #8e8e8e;
            --neon-green: #00ff66;
            --border-color: #262626;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background-color: var(--primary-bg);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .app-container {
            width: 100%;
            max-width: 430px;
            height: 100vh;
            max-height: 932px;
            background-color: var(--primary-bg);
            display: flex;
            flex-direction: column;
            position: relative;
            overflow: hidden;
            border: 1px solid var(--border-color);
        }

        /* --- ÉCRAN DE DÉMARRAGE (SPLASH SCREEN) --- */
        #splash-screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #000;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            transition: opacity 0.5s ease;
        }

        .splash-logo {
            font-size: 4rem;
            font-weight: bold;
            color: var(--text-color);
            text-shadow: 0 0 15px var(--neon-green);
            letter-spacing: 2px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .splash-logo span {
            color: var(--neon-green);
        }

        .splash-footer {
            position: absolute;
            bottom: 40px;
            font-size: 0.75rem;
            color: var(--text-secondary);
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        /* --- ÉCRAN DE CONNEXION --- */
        #auth-screen {
            display: none;
            flex-direction: column;
            justify-content: center;
            padding: 30px;
            height: 100%;
            text-align: center;
        }

        #auth-screen h1 {
            font-family: 'Brush Script MT', cursive, sans-serif;
            font-size: 3rem;
            color: var(--neon-green);
            margin-bottom: 30px;
            text-shadow: 0 0 10px rgba(0, 255, 102, 0.4);
        }

        .auth-input {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-color);
            font-size: 1rem;
        }

        .auth-btn {
            width: 100%;
            padding: 12px;
            background-color: var(--neon-green);
            color: #000;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            box-shadow: 0 0 10px rgba(0, 255, 102, 0.3);
        }

        /* --- INTERFACE PRINCIPALE (INSTAGRAM STYLE) --- */
        #main-app {
            display: none;
            flex-direction: column;
            height: 100%;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            border-bottom: 1px solid var(--border-color);
        }

        .app-title {
            font-family: 'Brush Script MT', cursive, sans-serif;
            font-size: 1.8rem;
            color: var(--neon-green);
            text-shadow: 0 0 8px rgba(0, 255, 102, 0.4);
        }

        .logout-btn {
            background: none;
            border: none;
            color: #ff4d4d;
            cursor: pointer;
            font-size: 0.9rem;
            font-weight: bold;
        }

        .content-body {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
        }

        /* Profil Section */
        .profile-header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        .avatar-container {
            position: relative;
            width: 80px;
            height: 80px;
            border-radius: 50%;
            overflow: hidden;
            border: 2px solid var(--neon-green);
            box-shadow: 0 0 8px var(--neon-green);
        }

        .avatar-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .avatar-container input[type="file"] {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            cursor: pointer;
        }

        .profile-info {
            flex: 1;
        }

        .profile-name-row {
            display: flex;
            align-items: center;
            gap: 6px;
            margin-bottom: 5px;
        }

        .profile-name {
            font-size: 1.2rem;
            font-weight: bold;
        }

        /* Trident Lumineux (Certification) */
        .trident-badge {
            width: 18px;
            height: 18px;
            fill: var(--neon-green);
            filter: drop-shadow(0 0 5px var(--neon-green));
        }

        .edit-name-input {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            color: white;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 1rem;
            display: none;
            width: 100%;
            margin-bottom: 5px;
        }

        .stats-row {
            display: flex;
            justify-content: space-around;
            text-align: center;
            background: var(--card-bg);
            padding: 12px;
            border-radius: 10px;
            border: 1px solid var(--border-color);
            margin-bottom: 20px;
        }

        .stat-item .number {
            font-weight: bold;
            font-size: 1.1rem;
            color: var(--neon-green);
        }

        .stat-item .label {
            font-size: 0.8rem;
            color: var(--text-secondary);
        }

        .profile-actions {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .action-btn {
            flex: 1;
            padding: 8px;
            background-color: var(--card-bg);
            border: 1px solid var(--border-color);
            color: white;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 500;
        }

        .action-btn:hover {
            border-color: var(--neon-green);
        }

        /* --- BARRE DE NAVIGATION INFÉRIEURE (VERT FONCÉ) --- */
        .bottom-nav {
            display: flex;
            justify-content: space-around;
            align-items: center;
            height: 60px;
            background-color: #051a0b; /* Vert foncé */
            border-top: 1px solid #004d1a;
        }

        .nav-item {
            background: none;
            border: none;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: var(--neon-green);
            opacity: 0.8;
            transition: opacity 0.2s;
        }

        .nav-item:hover, .nav-item.active {
            opacity: 1;
            text-shadow: 0 0 8px var(--neon-green);
        }

        .nav-item svg {
            width: 24px;
            height: 24px;
            fill: var(--neon-green);
        }

        .nav-item span {
            font-size: 0.65rem;
            margin-top: 3px;
        }
    </style>
</head>
<body>

    <div class="app-container">
        
        <!-- 1. ÉCRAN DE DÉMARRAGE -->
        <div id="splash-screen">
            <div class="splash-logo">G 🔱 G</div>
            <div class="splash-footer">Développé par Garcia Bletna</div>
        </div>

        <!-- 2. ÉCRAN DE CONNEXION -->
        <div id="auth-screen">
            <h1>Garcia Bletna</h1>
            <input type="text" id="username-input" class="auth-input" placeholder="Entrez votre nom d'utilisateur">
            <button class="auth-btn" onclick="login()">Se connecter / S'inscrire</button>
        </div>

        <!-- 3. INTERFACE PRINCIPALE -->
        <div id="main-app">
            <header>
                <div class="app-title">garciabletna</div>
                <button class="logout-btn" onclick="logout()">Déconnexion</button>
            </header>

            <div class="content-body">
                <!-- Section Profil -->
                <div class="profile-header">
                    <div class="avatar-container">
                        <img id="profile-pic" src="https://via.placeholder.com/150/121212/00ff66?text=GG" alt="Profil">
                        <input type="file" accept="image/*" onchange="changeProfilePic(event)" title="Changer la photo">
                    </div>
                    <div class="profile-info">
                        <div class="profile-name-row">
                            <span id="display-name" class="profile-name">Utilisateur</span>
                            <!-- Icône Trident Néon Vert (Certification) -->
                            <svg class="trident-badge" viewBox="0 0 24 24"><path d="M12 2v6m-4-3l4 3 4-3M12 8v14m-5-4l5 2 5-2"/></svg>
                        </div>
                        <input type="text" id="edit-name-input" class="edit-name-input" placeholder="Nouveau nom..." onblur="saveName()">
                        <p style="font-size: 0.8rem; color: var(--text-secondary);">Appuyez sur la photo pour la modifier</p>
                    </div>
                </div>

                <!-- Tableau de bord (Abonnés / Suivis) -->
                <div class="stats-row">
                    <div class="stat-item">
                        <div class="number" id="posts-count">0</div>
                        <div class="label">publications</div>
                    </div>
                    <div class="stat-item">
                        <div class="number" id="followers-count">0</div>
                        <div class="label">abonnés</div>
                    </div>
                    <div class="stat-item">
                        <div class="number" id="following-count">120</div>
                        <div class="label">suivis</div>
                    </div>
                </div>

                <div class="profile-actions">
                    <button class="action-btn" onclick="toggleEditName()">Modifier le profil</button>
                    <button class="action-btn" onclick="simulateFollow()">S'abonner / Se désabonner</button>
                </div>
            </div>

            <!-- Barre de navigation inférieure (Vert foncé) -->
            <nav class="bottom-nav">
                <button class="nav-item active">
                    <svg viewBox="0 0 24 24"><path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/></svg>
                    <span>Accueil</span>
                </button>
                <button class="nav-item">
                    <svg viewBox="0 0 24 24"><path d="M20 2H4c-1.1 0-2 .9-2 2v18l4-4h14c1.1 0-2-.9-2-2V4c0-1.1-.9-2-2-2z"/></svg>
                    <span>Discussion</span>
                </button>
                <button class="nav-item">
                    <svg viewBox="0 0 24 24"><path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z"/></svg>
                    <span>Appel</span>
                </button>
            </nav>
        </div>

    </div>

    <script>
        // Gestion du SplashScreen (disparaît après 2.5 secondes)
        window.addEventListener('load', () => {
            setTimeout(() => {
                const splash = document.getElementById('splash-screen');
                splash.style.opacity = '0';
                setTimeout(() => {
                    splash.style.display = 'none';
                    checkAuth();
                }, 500);
            }, 2500);
        });

        function checkAuth() {
            const savedUser = localStorage.getItem('garciabletna_user');
            if (savedUser) {
                document.getElementById('auth-screen').style.display = 'none';
                document.getElementById('main-app').style.display = 'flex';
                loadUserData(savedUser);
            } else {
                document.getElementById('auth-screen').style.display = 'flex';
            }
        }

        function login() {
            const usernameInput = document.getElementById('username-input').value.trim();
            if (!usernameInput) {
                alert("Veuillez entrer un nom d'utilisateur");
                return;
            }
            localStorage.setItem('garciabletna_user', usernameInput);
            document.getElementById('auth-screen').style.display = 'none';
            document.getElementById('main-app').style.display = 'flex';
            loadUserData(usernameInput);
        }

        function logout() {
            localStorage.removeItem('garciabletna_user');
            document.getElementById('main-app').style.display = 'none';
            document.getElementById('auth-screen').style.display = 'flex';
        }

        function loadUserData(username) {
            document.getElementById('display-name').innerText = username;

            // Compteur intelligent avec privilège Fondateur ("Garcia Bletna")
            const followersEl = document.getElementById('followers-count');
            if (username.toLowerCase() === "garcia bletna" || username.toLowerCase() === "garciabletna") {
                followersEl.innerText = "X"; // Accès illimité / Spécial fondateur
            } else {
                let savedFollowers = localStorage.getItem('followers_' + username);
                if (!savedFollowers) {
                    savedFollowers = Math.floor(Math.random() * 50) + 1;
                    localStorage.setItem('followers_' + username, savedFollowers);
                }
                followersEl.innerText = savedFollowers;
            }

            // Charger l'image de profil sauvegardée
            const savedPic = localStorage.getItem('profile_pic_' + username);
            if (savedPic) {
                document.getElementById('profile-pic').src = savedPic;
            }
        }

        // Modification de la photo de profil
        function changeProfilePic(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const base64Image = e.target.result;
                    document.getElementById('profile-pic').src = base64Image;
                    const username = localStorage.getItem('garciabletna_user');
                    localStorage.setItem('profile_pic_' + username, base64Image);
                }
                reader.readAsDataURL(file);
            }
        }

        // Édition du nom de profil
        function toggleEditName() {
            const nameSpan = document.getElementById('display-name');
            const nameInput = document.getElementById('edit-name-input');
            if (nameInput.style.display === 'block') {
                nameInput.style.display = 'none';
                nameSpan.style.display = 'block';
            } else {
                nameInput.style.display = 'block';
                nameInput.value = nameSpan.innerText;
                nameSpan.style.display = 'none';
                nameInput.focus();
            }
        }

        function saveName() {
            const nameInput = document.getElementById('edit-name-input');
            const newName = nameInput.value.trim();
            if (newName) {
                document.getElementById('display-name').innerText = newName;
                localStorage.setItem('garciabletna_user', newName);
            }
            nameInput.style.display = 'none';
            document.getElementById('display-name').style.display = 'block';
        }

        // Simulation d'abonnement / désabonnement intelligent pour les utilisateurs standards
        let isFollowing = false;
        function simulateFollow() {
            const username = localStorage.getItem('garciabletna_user');
            if (username.toLowerCase() === "garcia bletna" || username.toLowerCase() === "garciabletna") {
                alert("En tant que fondateur, vos abonnés sont illimités (X) !");
                return;
            }

            let currentFollowers = parseInt(localStorage.getItem('followers_' + username)) || 0;
            if (isFollowing) {
                currentFollowers -= 1;
                isFollowing = false;
                alert("Vous vous êtes désabonné.");
            } else {
                currentFollowers += 1;
                isFollowing = true;
                alert("Vous vous êtes abonné !");
            }
            localStorage.setItem('followers_' + username, currentFollowers);
            document.getElementById('followers-count').innerText = currentFollowers;
        }
    </script>
</body>
</html>
