<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LuaForge - Curso de Roblox com Lua</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --neon: #00FF88;
            --dark: #0D0D0D;
            --graphite: #1A1A1A;
            --graphite-light: #252525;
            --text: #E0E0E0;
            --text-muted: #999;
            --danger: #FF4757;
            --warning: #FFA502;
            --success: #00CC6A;
            --admin: #6C5CE7;
            --gold: #FFD700;
        }

        body {
            font-family: 'Segoe UI', 'Inter', system-ui, sans-serif;
            background: linear-gradient(135deg, #0D0D0D 0%, #1A1A1A 100%);
            color: var(--text);
            min-height: 100vh;
        }

        /* ========== TELA DE LOGIN ========== */
        .auth-container {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(135deg, #0D0D0D 0%, #1A1A1A 100%);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .auth-card {
            background: var(--graphite);
            border: 1px solid rgba(0, 255, 136, 0.2);
            border-radius: 24px;
            padding: 40px;
            width: 450px;
            max-width: 90%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
        }

        .auth-logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .auth-logo-img {
            max-width: 180px;
            margin-bottom: 15px;
        }

        .auth-logo-text {
            font-size: 28px;
            font-weight: 700;
            color: white;
        }

        .auth-logo-text span {
            color: var(--neon);
        }

        .auth-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            border-bottom: 1px solid #2A2A2A;
        }

        .auth-tab {
            flex: 1;
            padding: 12px;
            background: none;
            border: none;
            color: var(--text-muted);
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .auth-tab.active {
            color: var(--neon);
            border-bottom: 2px solid var(--neon);
        }

        .auth-form {
            display: none;
        }

        .auth-form.active {
            display: block;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            color: var(--text-muted);
            font-size: 12px;
            font-weight: 600;
            margin-bottom: 8px;
            text-transform: uppercase;
        }

        .form-input {
            width: 100%;
            padding: 14px 16px;
            background: var(--dark);
            border: 2px solid #2A2A2A;
            border-radius: 12px;
            color: white;
            font-size: 14px;
            outline: none;
        }

        .form-input:focus {
            border-color: var(--neon);
        }

        .btn-auth {
            width: 100%;
            padding: 14px;
            background: var(--neon);
            color: var(--dark);
            border: none;
            border-radius: 12px;
            font-weight: 700;
            font-size: 16px;
            cursor: pointer;
            margin-top: 10px;
        }

        .btn-auth:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0, 255, 136, 0.3);
        }

        .auth-message {
            background: rgba(255, 71, 87, 0.1);
            border: 1px solid var(--danger);
            color: var(--danger);
            padding: 12px;
            border-radius: 10px;
            font-size: 13px;
            margin-bottom: 20px;
            display: none;
            text-align: center;
        }

        /* ========== APP ========== */
        .app-container {
            display: none;
        }

        .app-container.active {
            display: flex;
        }

        /* ========== SIDEBAR ========== */
        .sidebar {
            width: 260px;
            background: var(--graphite);
            border-right: 1px solid #2A2A2A;
            display: flex;
            flex-direction: column;
            position: fixed;
            top: 0;
            left: 0;
            bottom: 0;
            z-index: 100;
            transition: transform 0.3s;
        }

        .sidebar-header {
            padding: 25px 20px;
            border-bottom: 1px solid #2A2A2A;
            text-align: center;
        }

        .sidebar-logo-img {
            max-width: 160px;
        }

        .nav-menu {
            list-style: none;
            padding: 20px 12px;
            flex: 1;
        }

        .nav-link {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 16px;
            border-radius: 10px;
            color: var(--text-muted);
            cursor: pointer;
            margin-bottom: 4px;
        }

        .nav-link:hover {
            background: var(--graphite-light);
            color: white;
        }

        .nav-link.active {
            background: rgba(0, 255, 136, 0.1);
            color: var(--neon);
        }

        .user-section {
            padding: 20px;
            border-top: 1px solid #2A2A2A;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-avatar {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--neon), #00cc6a);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: var(--dark);
            font-size: 18px;
        }

        .user-info {
            flex: 1;
        }

        .user-name {
            font-weight: 600;
            color: white;
        }

        .user-email {
            font-size: 11px;
            color: var(--text-muted);
        }

        .user-badge {
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 4px;
            background: var(--admin);
            color: white;
            display: inline-block;
            margin-top: 4px;
        }

        .btn-logout {
            background: rgba(255, 71, 87, 0.1);
            border: 1px solid var(--danger);
            color: var(--danger);
            padding: 6px 12px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 12px;
        }

        .btn-logout:hover {
            background: var(--danger);
            color: white;
        }

        /* ========== MAIN ========== */
        .main-content {
            margin-left: 260px;
            flex: 1;
            padding: 30px;
            min-height: 100vh;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .page-title {
            font-size: 28px;
            font-weight: 700;
        }

        .page-title span {
            color: var(--neon);
        }

        /* ========== CURSO ========== */
        .modulo-card {
            background: var(--graphite);
            border: 1px solid #2A2A2A;
            border-radius: 12px;
            padding: 18px 20px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 16px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .modulo-card:hover {
            border-color: var(--neon);
            transform: translateX(5px);
        }

        .modulo-card.completed {
            border-color: var(--success);
            background: rgba(0, 204, 106, 0.05);
        }

        .modulo-numero {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: var(--graphite-light);
            border: 2px solid #2A2A2A;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 18px;
            color: var(--neon);
        }

        .modulo-card.completed .modulo-numero {
            background: var(--success);
            color: var(--dark);
            border-color: var(--success);
        }

        .modulo-info {
            flex: 1;
        }

        .modulo-nome {
            font-weight: 700;
            color: white;
            font-size: 18px;
            margin-bottom: 5px;
        }

        .modulo-desc {
            font-size: 13px;
            color: var(--text-muted);
        }

        .modulo-status {
            font-size: 12px;
            padding: 4px 12px;
            border-radius: 20px;
            background: rgba(0, 255, 136, 0.1);
            color: var(--neon);
        }

        .modulo-status.completed {
            background: rgba(0, 204, 106, 0.15);
            color: var(--success);
        }

        /* ========== AULA ========== */
        .aula-container {
            background: var(--graphite);
            border: 1px solid #2A2A2A;
            border-radius: 16px;
            padding: 30px;
        }

        .aula-header {
            border-bottom: 1px solid #2A2A2A;
            padding-bottom: 20px;
            margin-bottom: 25px;
        }

        .aula-modulo {
            font-size: 12px;
            color: var(--neon);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 8px;
        }

        .aula-titulo {
            font-size: 28px;
            font-weight: 700;
            color: white;
            margin-bottom: 10px;
        }

        .aula-subtitulo {
            font-size: 16px;
            color: var(--text-muted);
        }

        .aula-body {
            line-height: 1.8;
        }

        .aula-body h3 {
            color: var(--neon);
            margin: 25px 0 12px;
            font-size: 20px;
        }

        .aula-body p {
            margin-bottom: 16px;
        }

        .aula-body ul, .aula-body ol {
            margin-bottom: 16px;
            padding-left: 25px;
        }

        .aula-body li {
            margin-bottom: 8px;
        }

        .code-block {
            background: #0A0A0A;
            border: 1px solid #2A2A2A;
            border-radius: 10px;
            padding: 16px;
            margin: 16px 0;
            font-family: 'Courier New', monospace;
            font-size: 13px;
            line-height: 1.6;
            color: #50FA7B;
            overflow-x: auto;
            position: relative;
        }

        .code-block .comment {
            color: #6272A4;
        }
        .code-block .keyword {
            color: #FF79C6;
        }
        .code-block .string {
            color: #F1FA8C;
        }

        .highlight-box {
            background: rgba(0, 255, 136, 0.05);
            border-left: 4px solid var(--neon);
            padding: 16px 20px;
            margin: 16px 0;
            border-radius: 0 10px 10px 0;
        }

        .highlight-box.curiosity {
            border-left-color: var(--admin);
            background: rgba(108, 92, 231, 0.05);
        }

        .highlight-box.warning {
            border-left-color: var(--warning);
            background: rgba(255, 165, 2, 0.05);
        }

        .diagram-box {
            background: var(--graphite-light);
            border: 2px dashed #2A2A2A;
            border-radius: 12px;
            padding: 20px;
            margin: 16px 0;
            text-align: center;
            font-family: monospace;
            font-size: 13px;
        }

        .exercicio-box, .desafio-box {
            background: rgba(255, 215, 0, 0.05);
            border: 1px solid var(--gold);
            border-radius: 12px;
            padding: 20px;
            margin: 16px 0;
        }

        .desafio-box {
            border-color: var(--danger);
            background: rgba(255, 71, 87, 0.05);
        }

        .exercicio-box h4, .desafio-box h4 {
            margin-bottom: 10px;
        }

        .exercicio-box h4 {
            color: var(--gold);
        }

        .desafio-box h4 {
            color: var(--danger);
        }

        .aula-nav {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
            gap: 15px;
        }

        .btn {
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            border: none;
            transition: all 0.2s;
        }

        .btn-primary {
            background: var(--neon);
            color: var(--dark);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 255, 136, 0.3);
        }

        .btn-outline {
            background: transparent;
            border: 2px solid var(--neon);
            color: var(--neon);
        }

        .btn-outline:hover {
            background: rgba(0, 255, 136, 0.1);
        }

        .btn-success {
            background: var(--success);
            color: var(--dark);
        }

        .progress-section {
            background: var(--graphite);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
        }

        .progress-bar-bg {
            background: #2A2A2A;
            border-radius: 10px;
            height: 10px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-bar-fill {
            background: linear-gradient(90deg, var(--neon), var(--success));
            height: 100%;
            width: 0%;
            transition: width 0.3s;
        }

        .toast-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 1000;
        }

        .toast {
            background: var(--graphite);
            border-left: 4px solid var(--neon);
            padding: 12px 20px;
            border-radius: 8px;
            margin-top: 8px;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.95);
            z-index: 200;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--graphite);
            border: 1px solid #2A2A2A;
            border-radius: 20px;
            padding: 30px;
            width: 500px;
            max-width: 90%;
        }

        .hamburger {
            display: none;
            background: var(--graphite);
            border: 1px solid #2A2A2A;
            color: white;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
        }

        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
            }
            .sidebar.open {
                transform: translateX(0);
            }
            .main-content {
                margin-left: 0;
            }
            .hamburger {
                display: block;
            }
        }
    </style>
</head>
<body>

<!-- TELA DE LOGIN -->
<div class="auth-container" id="authContainer">
    <div class="auth-card">
        <div class="auth-logo">
            <img src="https://messages-prod.27c852f3500f38c1e7786e2c9ff9e48f.r2.cloudflarestorage.com/019be747-3b53-7cf2-8f4c-b0a32d839a08/1779161969239-019e3e50-d5b7-762c-94e7-f8f0a5a2122c.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=b33de61d4f22a31b59b25364ab5037c5%2F20260519%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260519T052048Z&X-Amz-Expires=3600&X-Amz-Signature=13323d2105684fbc0ee9129098dedb8347b2df46e84d62184d2161edb3d17d3f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject" 
                 alt="LuaForge Logo" class="auth-logo-img" style="max-width: 200px;">
        </div>

        <div class="auth-tabs">
            <button class="auth-tab active" onclick="switchTab('login')">Entrar</button>
            <button class="auth-tab" onclick="switchTab('register')">Cadastrar</button>
        </div>

        <div id="authMessage" class="auth-message"></div>

        <div id="loginForm" class="auth-form active">
            <div class="form-group">
                <label>Usuário ou Email</label>
                <input type="text" id="loginIdentifier" class="form-input" placeholder="usuario ou email">
            </div>
            <div class="form-group">
                <label>Senha</label>
                <input type="password" id="loginPassword" class="form-input" placeholder="••••••">
            </div>
            <button class="btn-auth" onclick="fazerLogin()">Entrar</button>
        </div>

        <div id="registerForm" class="auth-form">
            <div class="form-group">
                <label>Usuário</label>
                <input type="text" id="regUsername" class="form-input" placeholder="usuario123">
            </div>
            <div class="form-group">
                <label>Email</label>
                <input type="email" id="regEmail" class="form-input" placeholder="seu@email.com">
            </div>
            <div class="form-group">
                <label>Senha</label>
                <input type="password" id="regPassword" class="form-input" placeholder="minimo 6 caracteres">
            </div>
            <div class="form-group">
                <label>Confirmar Senha</label>
                <input type="password" id="regConfirmPassword" class="form-input" placeholder="••••••">
            </div>
            <button class="btn-auth" onclick="fazerCadastro()">Criar Conta</button>
        </div>
    </div>
</div>

<!-- APP PRINCIPAL -->
<div class="app-container" id="appContainer">
    <aside class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <img src="https://messages-prod.27c852f3500f38c1e7786e2c9ff9e48f.r2.cloudflarestorage.com/019be747-3b53-7cf2-8f4c-b0a32d839a08/1779161969239-019e3e50-d5b7-762c-94e7-f8f0a5a2122c.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=b33de61d4f22a31b59b25364ab5037c5%2F20260519%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260519T052048Z&X-Amz-Expires=3600&X-Amz-Signature=13323d2105684fbc0ee9129098dedb8347b2df46e84d62184d2161edb3d17d3f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject" 
                 alt="LuaForge" style="max-width: 180px;">
        </div>
        <nav class="nav-menu">
            <div class="nav-link" onclick="navigateTo('home')">🏠 Dashboard</div>
            <div class="nav-link" onclick="navigateTo('curso')">📚 Curso Roblox</div>
            <div class="nav-link" onclick="navigateTo('editor')">✏️ Editor Lua</div>
            <div class="nav-link" onclick="navigateTo('scripts')">📁 Meus Scripts</div>
            <div class="nav-link" onclick="navigateTo('library')">📖 Biblioteca</div>
            <div class="nav-link" id="adminNavLink" onclick="navigateTo('admin')" style="display: none;">👑 Administração</div>
        </nav>
        <div class="user-section">
            <div class="user-avatar" id="userAvatar">U</div>
            <div class="user-info">
                <div class="user-name" id="userName">Usuário</div>
                <div class="user-email" id="userEmail">email@exemplo.com</div>
                <div id="userBadge"></div>
            </div>
            <button class="btn-logout" onclick="logout()">Sair</button>
        </div>
    </aside>

    <main class="main-content">
        <div class="top-bar">
            <h1 class="page-title" id="pageTitle">Dashboard</h1>
            <button class="hamburger" onclick="toggleSidebar()">☰</button>
        </div>

        <!-- HOME -->
        <div id="page-home">
            <div class="progress-section">
                <h3>📊 Seu Progresso no Curso</h3>
                <div class="progress-bar-bg">
                    <div class="progress-bar-fill" id="progressBarFill" style="width: 0%;"></div>
                </div>
                <p id="progressText" style="margin-top: 10px; color: var(--text-muted);">0 de 5 módulos concluídos</p>
            </div>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;">
                <div style="background: var(--graphite); border-radius: 12px; padding: 20px; text-align: center; cursor: pointer;" onclick="navigateTo('curso')">
                    <div style="font-size: 48px; margin-bottom: 10px;">🎮</div>
                    <h3>Curso Roblox</h3>
                    <p style="font-size: 13px; color: var(--text-muted);">Aprenda Lua do zero</p>
                </div>
                <div style="background: var(--graphite); border-radius: 12px; padding: 20px; text-align: center; cursor: pointer;" onclick="navigateTo('editor')">
                    <div style="font-size: 48px; margin-bottom: 10px;">💻</div>
                    <h3>Editor Lua</h3>
                    <p style="font-size: 13px; color: var(--text-muted);">Teste seus scripts</p>
                </div>
                <div style="background: var(--graphite); border-radius: 12px; padding: 20px; text-align: center; cursor: pointer;" onclick="navigateTo('scripts')">
                    <div style="font-size: 48px; margin-bottom: 10px;">📁</div>
                    <h3>Meus Scripts</h3>
                    <p style="font-size: 13px; color: var(--text-muted);">Salve seus códigos</p>
                </div>
            </div>
        </div>

        <!-- PÁGINA DO CURSO (MÓDULOS) -->
        <div id="page-curso" style="display: none;">
            <h2 style="margin-bottom: 20px;">📚 Curso: Introdução à Programação no Roblox com Lua</h2>
            <p style="margin-bottom: 25px; color: var(--text-muted);">Aprendendo lógica do jeito certo</p>
            
            <div id="modulosList"></div>
        </div>

        <!-- AULAS (serão preenchidas dinamicamente) -->
        <div id="page-aula" style="display: none;">
            <div id="aulaContent"></div>
        </div>

        <!-- EDITOR -->
        <div id="page-editor" style="display: none;">
            <div class="editor-container" style="background: var(--graphite); border-radius: 12px; overflow: hidden;">
                <div style="background: var(--graphite-light); padding: 15px; display: flex; justify-content: space-between;">
                    <span>📝 script.lua</span>
                    <button class="btn btn-primary" onclick="executarLua()">▶ Executar</button>
                </div>
                <textarea id="codeEditor" rows="15" style="width: 100%; background: #0A0A0A; border: none; color: #50FA7B; padding: 20px; font-family: monospace; font-size: 14px; resize: vertical; outline: none;" placeholder='-- Seu código Lua aqui
print("Olá, LuaForge!")'></textarea>
                <div id="outputConsole" style="background: #050505; padding: 15px; color: #50FA7B; font-family: monospace; min-height: 100px; border-top: 1px solid #2A2A2A;">> Console de saída</div>
            </div>
        </div>

        <!-- MEUS SCRIPTS -->
        <div id="page-scripts" style="display: none;">
            <div style="display: flex; justify-content: space-between; margin-bottom: 20px;">
                <h2>Meus Scripts</h2>
                <button class="btn btn-primary" onclick="abrirModalScript()">+ Novo Script</button>
            </div>
            <div id="scriptsList"></div>
        </div>

        <!-- BIBLIOTECA -->
        <div id="page-library" style="display: none;">
            <h2 style="margin-bottom: 20px;">📖 Biblioteca de Scripts</h2>
            <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px;">
                <div class="script-card" style="background: var(--graphite); border-radius: 12px; padding: 20px; cursor: pointer;" onclick="copiarScript('dia_noite')">
                    <h3>🌙 Sistema Dia/Noite</h3>
                    <p style="color: var(--text-muted); font-size: 13px;">Ciclo completo de iluminação para jogos</p>
                    <button class="btn btn-outline" style="margin-top: 12px;">Copiar</button>
                </div>
                <div class="script-card" style="background: var(--graphite); border-radius: 12px; padding: 20px; cursor: pointer;" onclick="copiarScript('teleporte')">
                    <h3>🌀 Sistema de Teleporte</h3>
                    <p style="color: var(--text-muted); font-size: 13px;">Teletransporte com ClickDetector</p>
                    <button class="btn btn-outline" style="margin-top: 12px;">Copiar</button>
                </div>
                <div class="script-card" style="background: var(--graphite); border-radius: 12px; padding: 20px; cursor: pointer;" onclick="copiarScript('contador')">
                    <h3>🔢 Contador de Toques</h3>
                    <p style="color: var(--text-muted); font-size: 13px;">Sistema de contagem interativo</p>
                    <button class="btn btn-outline" style="margin-top: 12px;">Copiar</button>
                </div>
            </div>
        </div>

        <!-- PAINEL ADMIN -->
        <div id="page-admin" style="display: none;">
            <h2 style="margin-bottom: 20px;">👑 Painel de Administração</h2>
            <div class="users-table" style="background: var(--graphite); border-radius: 12px; overflow: hidden;">
                <table style="width: 100%; border-collapse: collapse;">
                    <thead style="background: var(--graphite-light);">
                        <tr><th style="padding: 12px; text-align: left;">Usuário</th><th style="padding: 12px; text-align: left;">Email</th><th style="padding: 12px; text-align: left;">Status</th><th style="padding: 12px; text-align: left;">Premium</th><th style="padding: 12px; text-align: left;">Ações</th></tr>
                    </thead>
                    <tbody id="adminUsersTable"></tbody>
                </table>
            </div>
        </div>
    </main>
</div>

<!-- MODAL NOVO SCRIPT -->
<div class="modal" id="scriptModal">
    <div class="modal-content">
        <h2>Salvar Script</h2>
        <input type="text" id="scriptNomeInput" placeholder="Nome do script" style="width: 100%; padding: 12px; background: var(--dark); border: 1px solid #2A2A2A; border-radius: 8px; color: white; margin-bottom: 12px;">
        <textarea id="scriptCodigoInput" rows="8" placeholder="-- Seu código Lua aqui" style="width: 100%; padding: 12px; background: var(--dark); border: 1px solid #2A2A2A; border-radius: 8px; color: white; margin-bottom: 12px;"></textarea>
        <button class="btn btn-primary" onclick="salvarScript()" style="width: 100%; margin-bottom: 10px;">Salvar</button>
        <button class="btn btn-outline" onclick="fecharModalScript()" style="width: 100%;">Cancelar</button>
    </div>
</div>

<div class="toast-container" id="toastContainer"></div>

<script>
    // ========== SISTEMA DE AUTENTICAÇÃO ==========
    localStorage.removeItem('luforge_session');
    
    const STORAGE_KEY = 'luforge_users_secure';
    const SESSION_KEY = 'luforge_session';

    function hashPassword(password, salt = null) {
        const saltValue = salt || Math.random().toString(36).substring(2, 10);
        return { hash: btoa(password + saltValue), salt: saltValue };
    }

    function verifyPassword(password, storedHash, salt) {
        return btoa(password + salt) === storedHash;
    }

    function loadUsers() {
        const users = localStorage.getItem(STORAGE_KEY);
        if (users) return JSON.parse(users);
        
        // ADMIN: usuário = LuaMaster, senha = Forge@2024!Secure
        const adminHash = hashPassword('DYNO00');
        const defaultUsers = {
            'ADMLINDO_Admin': {
                id: 'ADMLINDO_Admin',
                username: 'ADMLINDO',
                email: 'admin@luforge.com',
                passwordHash: adminHash.hash,
                passwordSalt: adminHash.salt,
                isAdmin: true,
                isPremium: true,
                isBanned: false,
                progress: { modulo1: false, modulo2: false, modulo3: false, modulo4: false, modulo5: false },
                scripts: [],
                createdAt: new Date().toISOString()
            }
        };
        localStorage.setItem(STORAGE_KEY, JSON.stringify(defaultUsers));
        return defaultUsers;
    }

    function saveUsers(users) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(users));
    }

    let currentUser = null;

    function checkSession() {
        const sessionToken = localStorage.getItem(SESSION_KEY);
        if (sessionToken) {
            try {
                const session = JSON.parse(sessionToken);
                const users = loadUsers();
                if (users[session.userId] && session.expires > Date.now()) {
                    currentUser = users[session.userId];
                    currentUser.id = session.userId;
                    entrarNoApp();
                    return true;
                }
            } catch(e) {}
        }
        return false;
    }

    function criarSessao(userId) {
        localStorage.setItem(SESSION_KEY, JSON.stringify({ userId: userId, expires: Date.now() + (7 * 24 * 60 * 60 * 1000) }));
    }

    function destruirSessao() {
        localStorage.removeItem(SESSION_KEY);
    }

    function fazerLogin() {
        const identifier = document.getElementById('loginIdentifier').value.trim();
        const password = document.getElementById('loginPassword').value;

        const users = loadUsers();
        let foundUser = null, userId = null;

        for (const [id, user] of Object.entries(users)) {
            if ((user.username === identifier || user.email === identifier) && !user.isBanned) {
                foundUser = user;
                userId = id;
                break;
            }
        }

        if (!foundUser || !verifyPassword(password, foundUser.passwordHash, foundUser.passwordSalt)) {
            mostrarMensagem('Usuário ou senha incorretos', 'error');
            return;
        }

        currentUser = foundUser;
        currentUser.id = userId;
        criarSessao(userId);
        entrarNoApp();
        mostrarToast('Login realizado!', 'success');
    }

    function fazerCadastro() {
        const username = document.getElementById('regUsername').value.trim();
        const email = document.getElementById('regEmail').value.trim();
        const password = document.getElementById('regPassword').value;
        const confirmPassword = document.getElementById('regConfirmPassword').value;

        if (username.length < 3) return mostrarMensagem('Usuário deve ter pelo menos 3 caracteres', 'error');
        if (!email.includes('@')) return mostrarMensagem('Email inválido', 'error');
        if (password.length < 6) return mostrarMensagem('Senha deve ter pelo menos 6 caracteres', 'error');
        if (password !== confirmPassword) return mostrarMensagem('Senhas não coincidem', 'error');

        const users = loadUsers();
        for (const [id, user] of Object.entries(users)) {
            if (user.username === username) return mostrarMensagem('Usuário já existe', 'error');
            if (user.email === email) return mostrarMensagem('Email já cadastrado', 'error');
        }

        const passwordHash = hashPassword(password);
        const newUserId = 'user_' + Date.now();
        users[newUserId] = {
            id: newUserId, username, email,
            passwordHash: passwordHash.hash, passwordSalt: passwordHash.salt,
            isAdmin: false, isPremium: false, isBanned: false,
            progress: { modulo1: false, modulo2: false, modulo3: false, modulo4: false, modulo5: false },
            scripts: [], createdAt: new Date().toISOString()
        };

        saveUsers(users);
        mostrarMensagem('Cadastro realizado! Faça login.', 'success');
        document.getElementById('regUsername').value = '';
        document.getElementById('regEmail').value = '';
        document.getElementById('regPassword').value = '';
        document.getElementById('regConfirmPassword').value = '';
        switchTab('login');
    }

    function mostrarMensagem(msg, type) {
        const msgDiv = document.getElementById('authMessage');
        msgDiv.textContent = msg;
        msgDiv.className = 'auth-message ' + type;
        msgDiv.style.display = 'block';
        setTimeout(() => msgDiv.style.display = 'none', 3000);
    }

    function entrarNoApp() {
        document.getElementById('authContainer').style.display = 'none';
        document.getElementById('appContainer').classList.add('active');
        
        document.getElementById('userName').textContent = currentUser.username;
        document.getElementById('userEmail').textContent = currentUser.email;
        document.getElementById('userAvatar').textContent = currentUser.username.charAt(0).toUpperCase();
        
        const ehAdmin = (currentUser.isAdmin === true || currentUser.username === 'ADMLINDO');
        const adminNavLink = document.getElementById('adminNavLink');
        if (adminNavLink) adminNavLink.style.display = ehAdmin ? 'flex' : 'none';
        
        document.getElementById('userBadge').innerHTML = '';
        if (ehAdmin) document.getElementById('userBadge').innerHTML = '<span class="user-badge">Administrador</span>';
        if (currentUser.isPremium) document.getElementById('userBadge').innerHTML += '<span class="user-badge" style="background: #FFD700; color:#1A1A1A;">Premium</span>';
        
        carregarModulos();
        atualizarProgresso();
        if (ehAdmin) carregarAdminUsers();
    }

    function logout() {
        destruirSessao();
        currentUser = null;
        document.getElementById('authContainer').style.display = 'flex';
        document.getElementById('appContainer').classList.remove('active');
    }

    function switchTab(tab) {
        const tabs = document.querySelectorAll('.auth-tab');
        tabs.forEach(t => t.classList.remove('active'));
        if (tab === 'login') {
            tabs[0].classList.add('active');
            document.getElementById('loginForm').classList.add('active');
            document.getElementById('registerForm').classList.remove('active');
        } else {
            tabs[1].classList.add('active');
            document.getElementById('registerForm').classList.add('active');
            document.getElementById('loginForm').classList.remove('active');
        }
        document.getElementById('authMessage').style.display = 'none';
    }

    // ========== MÓDULOS E AULAS ==========
    const modulos = [
        { id: 1, nome: "Capítulo 1 — O que é Programação?", descricao: "Entenda o conceito de programação, lógica, eventos e reações" },
        { id: 2, nome: "Capítulo 2 — Conhecendo Lua", descricao: "História da linguagem, por que Roblox usa Lua" },
        { id: 3, nome: "Capítulo 3 — Seu Primeiro Script", descricao: "Função print(), console de saída, erros comuns" },
        { id: 4, nome: "Capítulo 4 — Eventos", descricao: "PlayerAdded, Touched, ClickDetector" },
        { id: 5, nome: "Capítulo 5 — Aprendendo do Jeito Certo", descricao: "Como lidar com erros, prática e desafios finais" }
    ];

    const aulasContent = {
        1: `
            <div class="aula-container">
                <div class="aula-header">
                    <div class="aula-modulo">CAPÍTULO 1</div>
                    <div class="aula-titulo">O que é Programação?</div>
                    <div class="aula-subtitulo">Entendendo o básico antes de escrever código</div>
                </div>
                <div class="aula-body">
                    <h3>🧠 O que é Programação?</h3>
                    <p>Imagine que você quer que seu cachorro traga a bolinha. Você não pode simplesmente pensar nisso e esperar que ele saiba. Você precisa dar instruções claras: <strong>"Pegue a bolinha"</strong>, <strong>"Traga a bolinha"</strong>, <strong>"Solte a bolinha"</strong>.</p>
                    <p>A <strong>programação</strong> é exatamente isso, mas para um computador ou, no nosso caso, para o Roblox!</p>
                    <p>Programação é a arte de dar instruções detalhadas e sequenciais a um computador para que ele execute uma tarefa específica. Essas instruções são escritas em uma linguagem que o computador entende, como o Lua, que usamos no Roblox.</p>
                    
                    <h3>🧩 Lógica Básica: O Coração da Programação</h3>
                    <p>Antes de escrever qualquer código, precisamos pensar na <strong>lógica</strong>. A lógica é a sequência de passos que o computador deve seguir para resolver um problema. É como uma receita de bolo: você precisa dos ingredientes certos e da ordem correta para que o bolo dê certo.</p>
                    
                    <div class="highlight-box">
                        <strong>📌 Exemplo Simples:</strong><br>
                        <em>"Se o jogador clicar em um botão, então a porta deve abrir."</em><br>
                        Aqui, <strong>"clicar em um botão"</strong> é a condição, e <strong>"a porta deve abrir"</strong> é a ação.
                    </div>
                    
                    <h3>🎮 Como os Jogos Funcionam?</h3>
                    <p>Os jogos no Roblox são uma série de <strong>eventos</strong> e <strong>reações</strong>:</p>
                    <ul>
                        <li><strong>Eventos:</strong> O jogador pula, um monstro aparece, um item é coletado.</li>
                        <li><strong>Reações:</strong> O personagem sobe, a música muda, a pontuação aumenta.</li>
                    </ul>
                    
                    <div class="diagram-box">
                        <strong>📊 Diagrama: Evento e Reação</strong><br><br>
                        Jogador Clica → Detectar Clique? → Sim → Porta Abre
                    </div>
                    
                    <div class="highlight-box curiosity">
                        <strong>🌟 Curiosidade:</strong> Você sabia que muitos dos jogos que você adora no Roblox foram criados por pessoas como você, usando programação?
                    </div>
                    
                    <div class="exercicio-box">
                        <h4>✏️ Mini Desafio</h4>
                        <p>Pense em uma ação que você faz em um jogo do Roblox e qual seria a reação do jogo. Escreva em uma frase simples.</p>
                        <p><em>Exemplo: "Se o jogador pisar na lava, então ele perde vida."</em></p>
                    </div>
                </div>
            </div>
        `,
        2: `
            <div class="aula-container">
                <div class="aula-header">
                    <div class="aula-modulo">CAPÍTULO 2</div>
                    <div class="aula-titulo">Conhecendo Lua</div>
                    <div class="aula-subtitulo">A linguagem que dá vida ao Roblox</div>
                </div>
                <div class="aula-body">
                    <h3>🌙 O que é Lua?</h3>
                    <p>Lua é uma linguagem de programação leve, poderosa e eficiente. Ela é projetada para ser facilmente incorporada em outras aplicações, o que a torna perfeita para o Roblox Studio.</p>
                    
                    <div class="highlight-box curiosity">
                        <strong>🇧🇷 História: Um Orgulho Brasileiro!</strong><br>
                        Lua foi criada em 1993 no Tecgraf da PUC-Rio por Roberto Ierusalimschy, Luiz Henrique de Figueiredo e Waldemar Celes. Tecnologia brasileira que conquistou o mundo!
                    </div>
                    
                    <h3>🤔 Por que Roblox usa Lua?</h3>
                    <ul>
                        <li><strong>Simplicidade:</strong> Fácil de aprender para iniciantes</li>
                        <li><strong>Velocidade:</strong> Execução rápida, ótima para jogos</li>
                        <li><strong>Flexibilidade:</strong> Pode ser usada para muitas coisas</li>
                        <li><strong>Leveza:</strong> Roda bem em diversas máquinas</li>
                    </ul>
                    
                    <h3>📜 Como os Scripts Funcionam?</h3>
                    <p>No Roblox Studio, você escreve seu código em algo chamado <strong>Script</strong>. Quando você inicia o jogo, o Roblox lê esses scripts e executa as instruções.</p>
                    
                    <div class="code-block">
                        <span class="comment">-- Este é um comentário! O Roblox ignora o que está aqui.</span><br>
                        <span class="keyword">print</span>(<span class="string">"Olá, mundo!"</span>) <span class="comment">-- Exibe uma mensagem</span>
                    </div>
                    
                    <div class="exercicio-box">
                        <h4>✏️ Exercício</h4>
                        <p>Em suas próprias palavras, explique por que o Roblox se beneficia de usar uma linguagem como Lua.</p>
                    </div>
                </div>
            </div>
        `,
        3: `
            <div class="aula-container">
                <div class="aula-header">
                    <div class="aula-modulo">CAPÍTULO 3</div>
                    <div class="aula-titulo">Seu Primeiro Script</div>
                    <div class="aula-subtitulo">Mãos no código!</div>
                </div>
                <div class="aula-body">
                    <h3>📢 A Função print(): Sua Primeira Voz no Roblox</h3>
                    <p>A função <code>print()</code> é uma das primeiras coisas que aprendemos. Com ela, você pode fazer o Roblox exibir mensagens no <strong>Console de Saída</strong>.</p>
                    
                    <p>O Console de Saída é uma janela especial no Roblox Studio para testar e depurar seu código.</p>
                    
                    <h3>🚀 Escrevendo seu primeiro script</h3>
                    <p>No Roblox Studio, insira um novo Script em ServerScriptService e digite:</p>
                    <div class="code-block">
                        <span class="keyword">print</span>(<span class="string">"Olá mundo!"</span>)
                    </div>
                    
                    <h3>🔍 Explicando Linha por Linha</h3>
                    <ul>
                        <li><strong>print:</strong> Função para exibir mensagens</li>
                        <li><strong>("Olá mundo!"):</strong> Mensagem entre aspas duplas (string)</li>
                    </ul>
                    
                    <div class="highlight-box warning">
                        <strong>⚠️ Erros Comuns:</strong><br>
                        • Esquecer as aspas: <code>print(Olá mundo!)</code><br>
                        • Esquecer os parênteses: <code>print "Olá mundo!"</code><br>
                        • Digitar errado: <code>pint("Olá mundo!")</code>
                    </div>
                    
                    <div class="exercicio-box">
                        <h4>✏️ Desafio</h4>
                        <p>Use a função print() para exibir seu nome no Console de Saída. Depois, exiba uma mensagem de boas-vindas para um amigo!</p>
                    </div>
                </div>
            </div>
        `,
        4: `
            <div class="aula-container">
                <div class="aula-header">
                    <div class="aula-modulo">CAPÍTULO 4</div>
                    <div class="aula-titulo">Eventos</div>
                    <div class="aula-subtitulo">Fazendo o jogo reagir às ações</div>
                </div>
                <div class="aula-body">
                    <h3>🎯 O que são Eventos?</h3>
                    <p>Eventos são <strong>gatilhos</strong> que seu script pode "escutar" e reagir. Quando um evento é ativado, seu script faz algo em resposta.</p>
                    
                    <h3>📋 Eventos Comuns no Roblox</h3>
                    <ul>
                        <li><strong>PlayerAdded:</strong> Quando um jogador entra no jogo</li>
                        <li><strong>Touched:</strong> Quando uma peça toca em outra</li>
                        <li><strong>ClickDetector:</strong> Quando um jogador clica em uma peça</li>
                    </ul>
                    
                    <h3>👤 Exemplo 1: PlayerAdded</h3>
                    <div class="code-block">
                        <span class="keyword">local</span> Players = game:<span class="keyword">GetService</span>(<span class="string">"Players"</span>)<br>
                        Players.PlayerAdded:<span class="keyword">Connect</span>(<span class="keyword">function</span>(player)<br>
                        &nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">print</span>(player.Name .. <span class="string">" entrou no jogo!"</span>)<br>
                        <span class="keyword">end</span>)
                    </div>
                    
                    <h3>🤝 Exemplo 2: Touched</h3>
                    <div class="code-block">
                        <span class="keyword">local</span> minhaPeca = script.Parent<br>
                        minhaPeca.Touched:<span class="keyword">Connect</span>(<span class="keyword">function</span>(otherPart)<br>
                        &nbsp;&nbsp;&nbsp;&nbsp;<span class="keyword">print</span>(<span class="string">"Tocou em: "</span> .. otherPart.Name)<br>
                        &nbsp;&nbsp;&nbsp;&nbsp;minhaPeca.BrickColor = BrickColor.<span class="keyword">Random</span>()<br>
                        <span class="keyword">end</span>)
                    </div>
                    
                    <div class="diagram-box">
                        <strong>📊 Eventos e Reações</strong><br><br>
                        Jogador Entra → PlayerAdded → Exibe mensagem<br>
                        Peça Toca Peça → Touched → Muda cor<br>
                        Jogador Clica → MouseClick → Peça desaparece
                    </div>
                    
                    <div class="exercicio-box">
                        <h4>✏️ Atividades Práticas</h4>
                        <ol>
                            <li>Crie um script que exiba uma mensagem para cada jogador que entrar</li>
                            <li>Faça uma peça que mude de cor ao ser tocada</li>
                            <li>Crie um botão que faça outra peça desaparecer</li>
                        </ol>
                    </div>
                </div>
            </div>
        `,
        5: `
            <div class="aula-container">
                <div class="aula-header">
                    <div class="aula-modulo">CAPÍTULO 5</div>
                    <div class="aula-titulo">Aprendendo do Jeito Certo</div>
                    <div class="aula-subtitulo">Como evoluir na programação</div>
                </div>
                <div class="aula-body">
                    <h3>🚫 Por que Copiar Scripts Atrapalha?</h3>
                    <p>Copiar scripts prontos sem entender é um dos maiores obstáculos para aprender programação de verdade.</p>
                    <ul>
                        <li>❌ Não aprende a lógica</li>
                        <li>❌ Não consegue resolver problemas</li>
                        <li>❌ Fica dependente de outros</li>
                    </ul>
                    
                    <h3>🧠 Como Aprender Lógica de Verdade</h3>
                    <ol>
                        <li><strong>Entenda o problema:</strong> Pense no que você quer que aconteça</li>
                        <li><strong>Planeje os passos:</strong> Divida em pequenas etapas</li>
                        <li><strong>Escreva o código:</strong> Traduza para Lua</li>
                        <li><strong>Teste e depure:</strong> Corrija os erros</li>
                    </ol>
                    
                    <div class="highlight-box">
                        <strong>💡 Dica:</strong> Programadores experientes não sabem tudo de cabeça. Eles sabem como encontrar informações e testar suas ideias!
                    </div>
                    
                    <h3>⚔️ Desafios Finais</h3>
                    
                    <div class="desafio-box">
                        <h4>🔥 Desafio 1: Mensagem de Boas-Vindas</h4>
                        <p>Crie um script que exiba: "Bem-vindo, [NomeDoJogador]! Divirta-se!"</p>
                    </div>
                    
                    <div class="desafio-box">
                        <h4>🔥 Desafio 2: Peça que Muda de Cor</h4>
                        <p>Crie uma peça que mude para uma cor aleatória cada vez que for tocada.</p>
                    </div>
                    
                    <div class="desafio-box">
                        <h4>🔥 Desafio 3: Teletransporte</h4>
                        <p>Crie um botão que teletransporte o jogador para outra posição.</p>
                    </div>
                    
                    <div class="desafio-box">
                        <h4>🔥 Desafio 4: Contador de Toques</h4>
                        <p>Crie um contador que aumente cada vez que a peça for tocada.</p>
                    </div>
                    
                    <div class="highlight-box curiosity">
                        <strong>🌟 Motivação:</strong> Programar pode ser desafiador, mas ver suas ideias ganharem vida é fantástico! Não desista!
                    </div>
                </div>
            </div>
        `
    };

    function carregarModulos() {
        const container = document.getElementById('modulosList');
        if (!container) return;
        
        container.innerHTML = '';
        modulos.forEach(modulo => {
            const isCompleted = currentUser.progress && currentUser.progress[`modulo${modulo.id}`];
            const div = document.createElement('div');
            div.className = `modulo-card ${isCompleted ? 'completed' : ''}`;
            div.onclick = () => abrirAula(modulo.id);
            div.innerHTML = `
                <div class="modulo-numero">${isCompleted ? '✓' : modulo.id}</div>
                <div class="modulo-info">
                    <div class="modulo-nome">${modulo.nome}</div>
                    <div class="modulo-desc">${modulo.descricao}</div>
                </div>
                <div class="modulo-status ${isCompleted ? 'completed' : ''}">${isCompleted ? 'Concluído' : 'Pendente'}</div>
            `;
            container.appendChild(div);
        });
    }

    function abrirAula(moduloId) {
        const content = aulasContent[moduloId];
        if (content) {
            document.getElementById('aulaContent').innerHTML = content + `
                <div class="aula-nav">
                    ${moduloId > 1 ? `<button class="btn btn-outline" onclick="abrirAula(${moduloId - 1})">← Anterior</button>` : '<div></div>'}
                    <button class="btn btn-primary" onclick="marcarModuloConcluido(${moduloId})">✓ Marcar como Concluído</button>
                    ${moduloId < 5 ? `<button class="btn btn-outline" onclick="abrirAula(${moduloId + 1})">Próximo →</button>` : '<div></div>'}
                </div>
            `;
            navigateTo('aula');
        }
    }

    function marcarModuloConcluido(moduloId) {
        if (!currentUser.progress) currentUser.progress = {};
        const key = `modulo${moduloId}`;
        if (!currentUser.progress[key]) {
            currentUser.progress[key] = true;
            const users = loadUsers();
            users[currentUser.id].progress = currentUser.progress;
            saveUsers(users);
            carregarModulos();
            atualizarProgresso();
            mostrarToast(`Módulo ${moduloId} concluído! +50 XP`, 'success');
            
            // Voltar para lista de módulos
            navigateTo('curso');
        } else {
            mostrarToast('Este módulo já foi concluído!', 'error');
        }
    }

    function atualizarProgresso() {
        if (!currentUser.progress) currentUser.progress = {};
        let completed = 0;
        for (let i = 1; i <= 5; i++) {
            if (currentUser.progress[`modulo${i}`]) completed++;
        }
        const percent = (completed / 5) * 100;
        const progressBar = document.getElementById('progressBarFill');
        const progressText = document.getElementById('progressText');
        if (progressBar) progressBar.style.width = percent + '%';
        if (progressText) progressText.textContent = `${completed} de 5 módulos concluídos`;
    }

    // ========== EDITOR LUA ==========
    function executarLua() {
        const codigo = document.getElementById('codeEditor').value;
        const output = document.getElementById('outputConsole');
        output.innerHTML = '';
        let outputLines = [];
        const originalPrint = window.print;
        
        try {
            window.print = function(...args) { outputLines.push(args.join(' ')); };
            new Function('print', codigo)(window.print);
            output.innerHTML = outputLines.length ? outputLines.map(l => `> ${l}`).join('\n') : '✓ Código executado sem saída.';
        } catch (err) {
            output.innerHTML = `❌ Erro: ${err.message}`;
            output.style.color = '#FF4757';
            setTimeout(() => output.style.color = '#50FA7B', 3000);
        } finally {
            window.print = originalPrint;
        }
    }

    // ========== SCRIPTS DO USUÁRIO ==========
    function carregarScriptsUsuario() {
        if (!currentUser.scripts) currentUser.scripts = [];
        const container = document.getElementById('scriptsList');
        if (!container) return;
        
        if (currentUser.scripts.length === 0) {
            container.innerHTML = '<div style="text-align: center; padding: 40px; color: #999;">Nenhum script salvo ainda.</div>';
            return;
        }
        
        container.innerHTML = '';
        currentUser.scripts.forEach((script, index) => {
            const div = document.createElement('div');
            div.className = 'script-card';
            div.style.background = 'var(--graphite)';
            div.style.borderRadius = '12px';
            div.style.padding = '18px';
            div.style.marginBottom = '12px';
            div.style.display = 'flex';
            div.style.justifyContent = 'space-between';
            div.style.alignItems = 'center';
            div.innerHTML = `
                <div><strong>${escapeHtml(script.nome)}</strong><br><span style="font-size: 12px; color: #666;">${script.data || 'Sem data'}</span></div>
                <div>
                    <button class="btn btn-outline" style="padding: 6px 12px; margin-right: 8px;" onclick="executarScriptSalvo(${index})">Executar</button>
                    <button class="btn btn-outline" style="padding: 6px 12px; margin-right: 8px;" onclick="editarScriptSalvo(${index})">Editar</button>
                    <button class="btn btn-outline" style="padding: 6px 12px; border-color: #FF4757; color: #FF4757;" onclick="excluirScriptSalvo(${index})">Excluir</button>
                </div>
            `;
            container.appendChild(div);
        });
    }

    function salvarScriptsUsuario() {
        const users = loadUsers();
        users[currentUser.id].scripts = currentUser.scripts;
        saveUsers(users);
    }

    let scriptEditandoIndex = -1;

    function abrirModalScript() {
        scriptEditandoIndex = -1;
        document.getElementById('scriptNomeInput').value = '';
        document.getElementById('scriptCodigoInput').value = '';
        document.getElementById('scriptModal').classList.add('active');
    }

    function fecharModalScript() {
        document.getElementById('scriptModal').classList.remove('active');
    }

    function salvarScript() {
        const nome = document.getElementById('scriptNomeInput').value.trim();
        const codigo = document.getElementById('scriptCodigoInput').value;
        if (!nome) { mostrarToast('Digite um nome', 'error'); return; }
        
        if (!currentUser.scripts) currentUser.scripts = [];
        const novoScript = { nome, codigo, data: new Date().toLocaleDateString('pt-BR') };
        
        if (scriptEditandoIndex >= 0) {
            currentUser.scripts[scriptEditandoIndex] = novoScript;
            mostrarToast('Script atualizado!', 'success');
        } else {
            currentUser.scripts.push(novoScript);
            mostrarToast('Script salvo!', 'success');
        }
        salvarScriptsUsuario();
        carregarScriptsUsuario();
        fecharModalScript();
    }

    function executarScriptSalvo(index) {
        const script = currentUser.scripts[index];
        document.getElementById('codeEditor').value = script.codigo;
        navigateTo('editor');
        setTimeout(() => executarLua(), 100);
        mostrarToast(`Executando: ${script.nome}`, 'success');
    }

    function editarScriptSalvo(index) {
        scriptEditandoIndex = index;
        const script = currentUser.scripts[index];
        document.getElementById('scriptNomeInput').value = script.nome;
        document.getElementById('scriptCodigoInput').value = script.codigo;
        document.getElementById('scriptModal').classList.add('active');
    }

    function excluirScriptSalvo(index) {
        if (confirm('Excluir este script?')) {
            currentUser.scripts.splice(index, 1);
            salvarScriptsUsuario();
            carregarScriptsUsuario();
            mostrarToast('Script excluído', 'success');
        }
    }

    function copiarScript(tipo) {
        let codigo = '', nome = '';
        if (tipo === 'dia_noite') {
            nome = 'Sistema Dia/Noite';
            codigo = `-- Sistema Dia/Noite
local lighting = game:GetService("Lighting")
while true do
    for hora = 0, 23 do
        lighting.ClockTime = hora
        wait(1)
    end
end`;
        } else if (tipo === 'teleporte') {
            nome = 'Sistema de Teleporte';
            codigo = `-- Sistema de Teleporte
local botao = script.Parent
local destino = game.Workspace.Destino
botao.ClickDetector.MouseClick:Connect(function(player)
    player.Character.HumanoidRootPart.CFrame = destino.CFrame
end)`;
        } else {
            nome = 'Contador de Toques';
            codigo = `-- Contador de Toques
local parte = script.Parent
local contador = 0
parte.Touched:Connect(function()
    contador = contador + 1
    print("Toques: " .. contador)
end)`;
        }
        document.getElementById('codeEditor').value = codigo;
        navigateTo('editor');
        mostrarToast(`Script "${nome}" copiado!`, 'success');
    }

    // ========== ADMIN ==========
    function carregarAdminUsers() {
        const users = loadUsers();
        const tbody = document.getElementById('adminUsersTable');
        tbody.innerHTML = '';
        
        Object.entries(users).forEach(([id, user]) => {
            const row = tbody.insertRow();
            row.innerHTML = `
                <td style="padding: 12px;">${escapeHtml(user.username)}</td>
                <td style="padding: 12px;">${escapeHtml(user.email)}</td>
                <td style="padding: 12px;">${user.isBanned ? '<span style="color:#FF4757;">Banido</span>' : '<span style="color:#00FF88;">Ativo</span>'}</td>
                <td style="padding: 12px;">${user.isPremium ? '<span style="color:#FFD700;">Premium</span>' : 'Free'}</td>
                <td style="padding: 12px;">
                    ${!user.isAdmin ? `
                        <button class="btn-icon" onclick="togglePremium('${id}')" style="background:none; border:none; cursor:pointer; margin-right:8px;">⭐</button>
                        <button class="btn-icon" onclick="toggleBan('${id}')" style="background:none; border:none; cursor:pointer;">🚫</button>
                    ` : '—'}
                </td>
            `;
        });
    }

    function togglePremium(userId) {
        const users = loadUsers();
        if (users[userId] && !users[userId].isAdmin) {
            users[userId].isPremium = !users[userId].isPremium;
            saveUsers(users);
            carregarAdminUsers();
            mostrarToast(`Premium ${users[userId].isPremium ? 'ativado' : 'removido'} para ${users[userId].username}`, 'success');
        }
    }

    function toggleBan(userId) {
        const users = loadUsers();
        if (users[userId] && !users[userId].isAdmin) {
            users[userId].isBanned = !users[userId].isBanned;
            saveUsers(users);
            carregarAdminUsers();
            mostrarToast(`${users[userId].username} ${users[userId].isBanned ? 'banido' : 'desbanido'}`, 'success');
        }
    }

    // ========== NAVEGAÇÃO ==========
    function navigateTo(page) {
        const pages = ['home', 'curso', 'aula', 'editor', 'scripts', 'library', 'admin'];
        pages.forEach(p => {
            const el = document.getElementById(`page-${p}`);
            if (el) el.style.display = 'none';
        });
        document.getElementById(`page-${page}`).style.display = 'block';
        
        const titles = { home: 'Dashboard', curso: 'Curso Roblox', aula: 'Aula', editor: 'Editor Lua', scripts: 'Meus Scripts', library: 'Biblioteca', admin: 'Administração' };
        document.getElementById('pageTitle').innerHTML = titles[page] || 'LuaForge';
        
        document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
        const index = { home: 0, curso: 1, editor: 2, scripts: 3, library: 4, admin: 5 };
        const links = document.querySelectorAll('.nav-link');
        if (links[index[page]]) links[index[page]].classList.add('active');
        
        document.getElementById('sidebar').classList.remove('open');
        
        if (page === 'scripts') carregarScriptsUsuario();
        if (page === 'admin' && (currentUser?.isAdmin || currentUser?.username === 'admin')) carregarAdminUsers();
        if (page === 'curso') carregarModulos();
    }

    function toggleSidebar() {
        document.getElementById('sidebar').classList.toggle('open');
    }

    function escapeHtml(str) {
        return str.replace(/[&<>]/g, m => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;' }[m]));
    }

    function mostrarToast(msg, type = 'success') {
        const container = document.getElementById('toastContainer');
        const toast = document.createElement('div');
        toast.className = 'toast';
        toast.style.borderLeftColor = type === 'error' ? '#FF4757' : '#00FF88';
        toast.innerHTML = msg;
        container.appendChild(toast);
        setTimeout(() => toast.remove(), 3000);
    }

    // ========== INICIALIZAÇÃO ==========
    window.addEventListener('load', () => {
        if (!checkSession()) {
            document.getElementById('authContainer').style.display = 'flex';
        }
    });
</script>
</body>
</html>
