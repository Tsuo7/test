<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tsuo Sociais | Hub de Conteúdo</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; transition: all 0.5s ease; background: #050505; color: #fff; }
        
        /* Tema Darkness (Solicitado: Luar, Gradiente, Amarelo Lobo) */
        .theme-darkness {
            background: linear-gradient(135deg, #020205 0%, #0d0d1a 100%);
            background-image: url('https://www.transparenttextures.com/patterns/dark-matter.png');
        }
        .theme-darkness .accent-text { color: #facc15; text-shadow: 0 0 15px rgba(250, 204, 21, 0.6); }
        .theme-darkness .glass-card { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(250, 204, 21, 0.3); backdrop-filter: blur(10px); }

        /* Estilos de Interface */
        .glass { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .hover-glow:hover { box-shadow: 0 0 25px rgba(250, 204, 21, 0.2); transform: translateY(-5px); }
        .transition-soft { transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        
        /* Scrollbar Personalizada */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0a0a0a; }
        ::-webkit-scrollbar-thumb { background: #facc15; border-radius: 10px; }
    </style>
</head>
<body class="theme-darkness min-h-screen pb-20">

    <nav class="sticky top-0 z-40 glass px-6 py-4 flex justify-between items-center max-w-7xl mx-auto mt-4 rounded-2xl">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-yellow-400 rounded-lg flex items-center justify-center text-black font-800 text-xl shadow-[0_0_15px_rgba(250,204,21,0.5)]">T</div>
            <h1 class="text-2xl font-800 accent-text tracking-tighter">TSUO SOCIAIS</h1>
        </div>
        
        <div class="flex items-center gap-6">
            <div class="relative hidden md:block">
                <input type="text" id="searchInput" placeholder="Pesquisar posts..." class="bg-white/5 border border-white/10 rounded-full px-5 py-2 focus:outline-none focus:ring-2 ring-yellow-400 w-64 transition-all">
                <i data-lucide="search" class="absolute right-4 top-2.5 opacity-40 w-5"></i>
            </div>
            <button onclick="toggleModal('loginModal')" class="hover:scale-110 transition-soft text-yellow-400">
                <i data-lucide="user-cog"></i>
            </button>
        </div>
    </nav>

    <header class="max-w-4xl mx-auto text-center py-20 px-6">
        <h2 id="displayTitle" class="text-6xl font-800 mb-6 bg-gradient-to-r from-yellow-100 to-yellow-500 bg-clip-text text-transparent">Tsuo Sociais</h2>
        <p id="displayAbout" class="text-gray-400 text-lg leading-relaxed mb-10">Bem-vindo ao meu hub oficial. Aqui encontras todos os meus blogs, links de download e novidades exclusivas.</p>
        
        <div class="flex justify-center gap-6">
            <a href="#" class="glass p-4 rounded-full hover:bg-yellow-400 hover:text-black transition-soft"><i data-lucide="youtube"></i></a>
            <a href="#" class="glass p-4 rounded-full hover:bg-yellow-400 hover:text-black transition-soft"><i data-lucide="instagram"></i></a>
            <a href="#" class="glass p-4 rounded-full hover:bg-yellow-400 hover:text-black transition-soft"><i data-lucide="twitch"></i></a>
        </div>
    </header>

    <main id="postFeed" class="max-w-6xl mx-auto px-6 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        </main>

    <div id="loginModal" class="fixed inset-0 bg-black/95 flex items-center justify-center hidden z-50 p-4">
        <div class="glass p-8 rounded-3xl w-full max-w-sm border-yellow-400/50 border">
            <h3 class="text-2xl font-bold mb-6 text-yellow-400 flex items-center gap-2">
                <i data-lucide="shield-check"></i> Acesso Admin
            </h3>
            <div class="space-y-4">
                <input type="text" id="adminUser" placeholder="Usuário" class="w-full bg-white/5 p-4 rounded-xl outline-none focus:ring-2 ring-yellow-400">
                <input type="password" id="adminPass" placeholder="Senha" class="w-full bg-white/5 p-4 rounded-xl outline-none focus:ring-2 ring-yellow-400">
                <button onclick="handleLogin()" class="w-full bg-yellow-400 text-black py-4 rounded-xl font-800 hover:bg-yellow-300 transition shadow-lg">Entrar no Painel</button>
                <button onclick="toggleModal('loginModal')" class="w-full text-gray-500 text-sm">Cancelar</button>
            </div>
        </div>
    </div>

    <div id="adminDashboard" class="fixed inset-0 bg-[#07070a] z-50 hidden overflow-y-auto p-6 md:p-12">
        <div class="max-w-6xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-4xl font-800 text-yellow-400">Configurações Tsuo</h2>
                <button onclick="logout()" class="bg-red-500/20 text-red-500 px-6 py-2 rounded-xl border border-red-500/30 font-bold">Encerrar Sessão</button>
            </div>

            <div class="grid lg:grid-cols-2 gap-10">
                <div class="glass p-8 rounded-3xl">
                    <h3 class="text-xl font-bold mb-6 flex items-center gap-2"><i data-lucide="file-plus"></i> Novo Post / Download</h3>
                    <div class="space-y-4">
                        <input type="text" id="pTitle" placeholder="Título" class="w-full bg-black p-3 rounded-lg border border-white/10">
                        <textarea id="pDesc" placeholder="Descrição ou Link de Download" class="w-full bg-black p-3 rounded-lg border border-white/10 h-24"></textarea>
                        <input type="text" id="pImg" placeholder="URL da Imagem (Capa)" class="w-full bg-black p-3 rounded-lg border border-white/10">
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="text-xs text-gray-500 mb-2 block">Escolha o Tema:</label>
                                <select id="pTheme" class="w-full bg-black p-3 rounded-lg border border-white/10 text-sm">
                                    <option value="theme-darkness">Darkness (Lobo & Lua)</option>
                                    <option value="bg-blue-900/40">Ocean Deep</option>
                                    <option value="bg-purple-900/40">Galaxy Retro</option>
                                    <option value="bg-zinc-800">Minimalist Dark</option>
                                </select>
                            </div>
                            <div>
                                <label class="text-xs text-gray-500 mb-2 block">Cor do Embed:</label>
                                <button onclick="randomColor()" class="w-full bg-white/5 p-3 rounded-lg border border-white/10 text-sm text-yellow-400">Auto Cor ✨</button>
                                <input type="hidden" id="pColor" value="#facc15">
                            </div>
                        </div>
                        <button onclick="createPost()" class="w-full bg-green-600 text-white py-4 rounded-xl font-800 mt-4 shadow-xl hover:bg-green-500 transition">PUBLICAR BLOG</button>
                    </div>
                </div>

                <div class="glass p-8 rounded-3xl h-fit">
                    <h3 class="text-xl font-bold mb-6 flex items-center gap-2"><i data-lucide="layout"></i> Editar Página Inicial</h3>
                    <input type="text" id="sTitle" placeholder="Título do Site" class="w-full bg-black p-3 mb-4 rounded-lg border border-white/10">
                    <textarea id="sAbout" placeholder="Sobre o Site" class="w-full bg-black p-3 mb-6 rounded-lg border border-white/10 h-32"></textarea>
                    <button onclick="updateSiteConfig()" class="w-full bg-blue-600 text-white py-4 rounded-xl font-800 shadow-xl">SALVAR ALTERAÇÕES</button>
                    
                    <div class="mt-8 border-t border-white/10 pt-6">
                        <p class="text-sm text-gray-500">Créditos: Criado por Tsuo & Gemini</p>
                    </div>
                </div>
            </div>

            <div class="mt-12 bg-white/5 p-6 rounded-3xl border border-white/10">
                <h3 class="text-xl font-bold mb-6">Gerenciar Posts Ativos</h3>
                <div id="adminPostList" class="space-y-4">
                    </div>
            </div>
        </div>
    </div>

    <script>
        // --- BASE DE DADOS LOCAL (LocalStorage) ---
        let posts = JSON.parse(localStorage.getItem('tsuo_data_posts')) || [];
        let config = JSON.parse(localStorage.getItem('tsuo_data_config')) || {
            title: "Tsuo Sociais",
            about: "O lugar definitivo para meus links de download e blogs. Explore o meu hub oficial."
        };

        // --- INICIALIZAÇÃO ---
        function init() {
            lucide.createIcons();
            renderSite();
            renderPosts();
        }

        // --- SISTEMA DE LOGIN ---
        function toggleModal(id) { document.getElementById(id).classList.toggle('hidden'); }

        function handleLogin() {
            const u = document.getElementById('adminUser').value;
            const p = document.getElementById('adminPass').value;
            if(u === 'tsuo' && p === 'tsuo') {
                toggleModal('loginModal');
                document.getElementById('adminDashboard
