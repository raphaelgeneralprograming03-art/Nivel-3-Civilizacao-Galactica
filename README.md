
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador Kardashev Nível 3: Civilização Galáctica</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        galactic: {
                            50: '#f0f3ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            800: '#2e1065',
                            900: '#0f0728',
                            950: '#050212',
                        },
                        singularity: {
                            light: '#a855f7',
                            DEFAULT: '#7e22ce',
                            dark: '#3b0764'
                        },
                        dyson: '#06b6d4'
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 3s infinite alternate',
                        'spin-slow': 'spin 20s linear infinite',
                        'orbit': 'orbit 40s linear infinite'
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%': { boxShadow: '0 0 15px rgba(126, 34, 206, 0.4)' },
                            '100%': { boxShadow: '0 0 35px rgba(6, 182, 212, 0.8)' }
                        },
                        orbit: {
                            '0%': { transform: 'rotate(0deg)' },
                            '100%': { transform: 'rotate(360deg)' }
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #050212;
            color: #e0e7ff;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            overflow-x: hidden;
        }
        
        .glass-panel {
            background: rgba(15, 7, 40, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(99, 102, 241, 0.2);
        }

        .glass-panel-hover:hover {
            border-color: rgba(6, 182, 212, 0.5);
            box-shadow: 0 0 20px rgba(6, 182, 212, 0.2);
        }

        /* Custom scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #050212;
        }
        ::-webkit-scrollbar-thumb {
            background: #2e1065;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #6366f1;
        }

        /* Sliders style */
        input[type=range] {
            accent-color: #06b6d4;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between antialiased selection:bg-purple-500 selection:text-white">

    <!-- HEADER / NAVIGATION -->
    <header class="glass-panel sticky top-0 z-50 border-b border-indigo-900/50 px-4 lg:px-8 py-3">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center space-x-3">
                <div class="p-2 bg-gradient-to-tr from-purple-900 to-indigo-600 rounded-lg text-cyan-400 shadow-lg shadow-purple-900/50">
                    <i data-lucide="orbit" class="w-7 h-7 animate-spin-slow"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 via-purple-300 to-pink-500">
                        SIMULADOR KARDASHEV NÍVEL 3
                    </h1>
                    <p class="text-xs text-indigo-300 flex items-center gap-1">
                        <span>Via Láctea</span> • <span>Domínio de 100-400 Bilhões de Estrelas</span>
                    </p>
                </div>
            </div>

            <!-- METRICAS HEADER PRINCIPAIS -->
            <div class="flex flex-wrap items-center gap-4 text-xs md:text-sm">
                <div class="bg-indigo-950/80 px-3 py-1.5 rounded-md border border-indigo-800/50 flex items-center gap-2">
                    <i data-lucide="zap" class="w-4 h-4 text-yellow-400"></i>
                    <span class="text-indigo-300">Potência Total:</span>
                    <span id="headerPower" class="font-mono font-bold text-cyan-300">1.2 × 10³⁷ W</span>
                </div>
                <div class="bg-indigo-950/80 px-3 py-1.5 rounded-md border border-indigo-800/50 flex items-center gap-2">
                    <i data-lucide="disc" class="w-4 h-4 text-purple-400"></i>
                    <span class="text-indigo-300">Índice Kardashev:</span>
                    <span id="headerKardashev" class="font-mono font-bold text-purple-300">3.08 K</span>
                </div>
                <div class="bg-indigo-950/80 px-3 py-1.5 rounded-md border border-indigo-800/50 flex items-center gap-2">
                    <i data-lucide="clock" class="w-4 h-4 text-cyan-400"></i>
                    <span class="text-indigo-300">Tempo Decorrido:</span>
                    <span id="headerYear" class="font-mono font-bold text-white">+0.00 Ma</span>
                </div>
            </div>
        </div>
    </header>

    <!-- OVERVIEW INFO BANNER -->
    <section class="max-w-7xl mx-auto w-full px-4 lg:px-8 mt-6">
        <div class="glass-panel p-5 rounded-xl border border-purple-500/30 bg-gradient-to-r from-purple-950/40 via-indigo-950/20 to-slate-950/60 relative overflow-hidden">
            <div class="absolute -right-10 -bottom-10 w-60 h-60 bg-purple-600/10 rounded-full blur-3xl pointer-events-none"></div>
            
            <div class="flex flex-col md:flex-row gap-4 items-start md:items-center justify-between">
                <div class="space-y-2 max-w-3xl">
                    <div class="inline-flex items-center gap-2 px-2.5 py-1 rounded-full bg-purple-900/60 border border-purple-400/30 text-purple-200 text-xs font-semibold">
                        <i data-lucide="sparkles" class="w-3.5 h-3.5 text-cyan-400"></i>
                        Visão Geral do Aplicativo
                    </div>
                    <h2 class="text-lg font-bold text-white">Simulador de Engenharia Galáctica e Sociedade Pós-Biológica</h2>
                    <p class="text-xs md:text-sm text-indigo-200 leading-relaxed">
                        Gerencie a transição para uma civilização de Tipo 3. Controle a autorreplicação das <strong>Sondas de Von Neumann</strong>, extraia energia da ergosfera de <strong>Sagittarius A*</strong> via Processo Penrose, manipule <strong>Matéria Escura</strong> e unifique a galáxia com motores de <strong>Dobra Espacial</strong> e mentes virtuais interconectadas.
                    </p>
                </div>

                <div class="flex items-center gap-3 w-full md:w-auto">
                    <button id="btnAdvanceTime" onclick="advanceEpoch()" class="w-full md:w-auto px-5 py-3 bg-gradient-to-r from-purple-600 to-cyan-600 hover:from-purple-500 hover:to-cyan-500 text-white font-semibold rounded-lg shadow-lg shadow-purple-900/50 flex items-center justify-center gap-2 transition-all transform active:scale-95 border border-cyan-400/30">
                        <i data-lucide="fast-forward" class="w-5 h-5"></i>
                        <span>Avançar Era (100 mil Anos)</span>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- MAIN DASHBOARD CONTENT -->
    <main class="max-w-7xl mx-auto w-full px-4 lg:px-8 py-6 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- PANEL ESQUERDO: CONTROLES & PILARES TECNOLÓGICOS (5 colunas) -->
        <section class="lg:col-span-5 space-y-6">

            <!-- CONTROLES DE ENGENHARIA GALÁCTICA -->
            <div class="glass-panel p-5 rounded-xl space-y-5">
                <div class="flex items-center justify-between border-b border-indigo-900/60 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="sliders" class="w-5 h-5 text-cyan-400"></i>
                        Necessidades Críticas & Motores
                    </h3>
                    <span class="text-xs text-indigo-400">Ajustar Alocação</span>
                </div>

                <!-- SLIDER 1: Sondas Von Neumann & Dyson Swarms -->
                <div class="space-y-2">
                    <div class="flex justify-between text-xs">
                        <label for="sliderNeumann" class="font-medium text-indigo-200 flex items-center gap-1.5">
                            <i data-lucide="cpu" class="w-4 h-4 text-cyan-400"></i>
                            Sondas Von Neumann Expansivas
                        </label>
                        <span id="valNeumann" class="font-mono text-cyan-300 font-bold">50%</span>
                    </div>
                    <input type="range" id="sliderNeumann" min="1" max="100" value="50" oninput="updateSimulation()" class="w-full h-2 bg-indigo-950 rounded-lg appearance-none cursor-pointer">
                    <p class="text-[11px] text-indigo-400">Disseminação autônoma para mineração de asteroides e construção de Enxames de Dyson.</p>
                </div>

                <!-- SLIDER 2: Processo Penrose & Buracos Negros -->
                <div class="space-y-2">
                    <div class="flex justify-between text-xs">
                        <label for="sliderPenrose" class="font-medium text-indigo-200 flex items-center gap-1.5">
                            <i data-lucide="black-hole" class="w-4 h-4 text-purple-400"></i>
                            Rede de Ergosferas (Processo Penrose)
                        </label>
                        <span id="valPenrose" class="font-mono text-purple-300 font-bold">40%</span>
                    </div>
                    <input type="range" id="sliderPenrose" min="0" max="100" value="40" oninput="updateSimulation()" class="w-full h-2 bg-indigo-950 rounded-lg appearance-none cursor-pointer">
                    <p class="text-[11px] text-indigo-400">Extração hiper-eficiente de energia lançando matéria em buracos negros supermassivos.</p>
                </div>

                <!-- SLIDER 3: Dobras Espaciais & Buracos de Minhoca -->
                <div class="space-y-2">
                    <div class="flex justify-between text-xs">
                        <label for="sliderWarp" class="font-medium text-indigo-200 flex items-center gap-1.5">
                            <i data-lucide="infinity" class="w-4 h-4 text-pink-400"></i>
                            Rede FTL (Dobra Espacial & Minhoca)
                        </label>
                        <span id="valWarp" class="font-mono text-pink-300 font-bold">30%</span>
                    </div>
                    <input type="range" id="sliderWarp" min="0" max="100" value="30" oninput="updateSimulation()" class="w-full h-2 bg-indigo-950 rounded-lg appearance-none cursor-pointer">
                    <p class="text-[11px] text-indigo-400">Dobra do espaço-tempo para coesão política e comunicação em tempo real em 100k anos-luz.</p>
                </div>

                <!-- SLIDER 4: Propulsores Shkadov & Reorganização Estelar -->
                <div class="space-y-2">
                    <div class="flex justify-between text-xs">
                        <label for="sliderShkadov" class="font-medium text-indigo-200 flex items-center gap-1.5">
                            <i data-lucide="sun-medium" class="w-4 h-4 text-yellow-400"></i>
                            Propulsores Shkadov (Mover Estrelas)
                        </label>
                        <span id="valShkadov" class="font-mono text-yellow-300 font-bold">25%</span>
                    </div>
                    <input type="range" id="sliderShkadov" min="0" max="100" value="25" oninput="updateSimulation()" class="w-full h-2 bg-indigo-950 rounded-lg appearance-none cursor-pointer">
                    <p class="text-[11px] text-indigo-400">Movimentação física de sistemas estelares para desarmar supernovas e agrupar recursos.</p>
                </div>

                <!-- SLIDER 5: Engenharia de Matéria Escura -->
                <div class="space-y-2">
                    <div class="flex justify-between text-xs">
                        <label for="sliderDarkMatter" class="font-medium text-indigo-200 flex items-center gap-1.5">
                            <i data-lucide="ghost" class="w-4 h-4 text-indigo-400"></i>
                            Engenharia de Matéria Escura
                        </label>
                        <span id="valDarkMatter" class="font-mono text-indigo-300 font-bold">20%</span>
                    </div>
                    <input type="range" id="sliderDarkMatter" min="0" max="100" value="20" oninput="updateSimulation()" class="w-full h-2 bg-indigo-950 rounded-lg appearance-none cursor-pointer">
                    <p class="text-[11px] text-indigo-400">Coleta e manipulação de massa invisível para usinas exóticas e ancoragem gravitacional.</p>
                </div>
            </div>

            <!-- STATUS PÓS-HUMANO E MENTES COLMEIA -->
            <div class="glass-panel p-5 rounded-xl space-y-4">
                <div class="flex items-center justify-between border-b border-indigo-900/60 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="users-round" class="w-5 h-5 text-pink-400"></i>
                        Evolução Pós-Humana
                    </h3>
                    <span id="postHumanStatus" class="text-xs px-2 py-0.5 rounded bg-pink-950 border border-pink-700/50 text-pink-300 font-mono">
                        Digital Dominante
                    </span>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div class="bg-indigo-950/50 p-3 rounded-lg border border-indigo-900/40">
                        <div class="text-xs text-indigo-300 mb-1">Mentes Submersas em Redes</div>
                        <div id="mindUploadPct" class="text-lg font-bold font-mono text-cyan-300">99.98%</div>
                        <div class="text-[10px] text-indigo-400">Mentes em Matrioshka Brains</div>
                    </div>
                    <div class="bg-indigo-950/50 p-3 rounded-lg border border-indigo-900/40">
                        <div class="text-xs text-indigo-300 mb-1">Biologia Biológica</div>
                        <div id="bioHumanPct" class="text-lg font-bold font-mono text-pink-400">0.02%</div>
                        <div class="text-[10px] text-indigo-400">Reservas em Mundos Santuário</div>
                    </div>
                </div>

                <div class="space-y-1.5">
                    <div class="flex justify-between text-xs text-indigo-300">
                        <span>Coesão Galáctica de Mente Colmeia</span>
                        <span id="hiveCohesionVal" class="font-mono text-cyan-300">78%</span>
                    </div>
                    <div class="w-full bg-indigo-950 rounded-full h-2 overflow-hidden border border-indigo-900">
                        <div id="hiveCohesionBar" class="bg-gradient-to-r from-purple-500 to-cyan-400 h-full transition-all duration-500" style="width: 78%;"></div>
                    </div>
                </div>
            </div>

        </section>

        <!-- PANEL DIREITO: MAPA, GRÁFICOS E DOMÍNIOS GALÁCTICOS (7 colunas) -->
        <section class="lg:col-span-7 space-y-6">

            <!-- PAINEL VISUAL DE DOMÍNIO E REESTRUTURAÇÃO GALÁCTICA -->
            <div class="glass-panel p-5 rounded-xl space-y-4">
                <div class="flex items-center justify-between border-b border-indigo-900/60 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="globe" class="w-5 h-5 text-purple-400"></i>
                        Transformação da Via Láctea
                    </h3>
                    <div class="flex items-center gap-2 text-xs">
                        <span class="inline-block w-2.5 h-2.5 rounded-full bg-red-500"></span>
                        <span class="text-indigo-300">Emissão Visível</span>
                        <span class="inline-block w-2.5 h-2.5 rounded-full bg-cyan-400 ml-2"></span>
                        <span class="text-indigo-300">Emissão Infravermelha</span>
                    </div>
                </div>

                <!-- CARTÕES DOS DOMÍNIOS GALÁCTICOS -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    
                    <!-- CARTÃO 1: Espectro da Galáxia -->
                    <div class="glass-panel-hover p-4 rounded-lg bg-indigo-950/40 border border-indigo-800/40 space-y-2">
                        <div class="flex justify-between items-start">
                            <span class="text-xs font-semibold text-cyan-300 flex items-center gap-1.5">
                                <i data-lucide="eye" class="w-4 h-4"></i>
                                Assinatura Espectral
                            </span>
                            <span id="infraredShiftStatus" class="text-[10px] px-2 py-0.5 bg-cyan-950 border border-cyan-800 text-cyan-300 rounded">
                                Infravermelho Intenso
                            </span>
                        </div>
                        <p class="text-xs text-indigo-200">
                            Luz visível convertida em calor residual. Para observadores externos, a galáxia pareceu "apagar" no visível.
                        </p>
                        <div class="text-xs font-mono text-indigo-400">
                            Ocupação de Dyson: <span id="dysonCoverageVal" class="text-cyan-300 font-bold">12.4%</span>
                        </div>
                    </div>

                    <!-- CARTÃO 2: Sagittarius A* (O Núcleo) -->
                    <div class="glass-panel-hover p-4 rounded-lg bg-purple-950/30 border border-purple-800/40 space-y-2">
                        <div class="flex justify-between items-start">
                            <span class="text-xs font-semibold text-purple-300 flex items-center gap-1.5">
                                <i data-lucide="orbit" class="w-4 h-4"></i>
                                Núcleo Galactic Center (Sagittarius A*)
                            </span>
                            <span class="text-[10px] px-2 py-0.5 bg-purple-900 border border-purple-700 text-purple-200 rounded">
                                Capital Computacional
                            </span>
                        </div>
                        <p class="text-xs text-indigo-200">
                            Usina Penrose de Penrose acoplada ao buraco negro supermassivo. Processamento central da mente colmeia.
                        </p>
                        <div class="text-xs font-mono text-indigo-400">
                            Rendimento Ergosférico: <span id="penroseEfficiencyVal" class="text-purple-300 font-bold">1.8 × 10³⁵ W</span>
                        </div>
                    </div>

                    <!-- CARTÃO 3: Propulsores Shkadov -->
                    <div class="glass-panel-hover p-4 rounded-lg bg-yellow-950/20 border border-yellow-800/40 space-y-2">
                        <div class="flex justify-between items-start">
                            <span class="text-xs font-semibold text-yellow-300 flex items-center gap-1.5">
                                <i data-lucide="compass" class="w-4 h-4"></i>
                                Arquitetura de Sistemas Estelares
                            </span>
                            <span id="shkadovStatus" class="text-[10px] px-2 py-0.5 bg-yellow-950 border border-yellow-800 text-yellow-300 rounded">
                                4.2k Estrelas Reorientadas
                            </span>
                        </div>
                        <p class="text-xs text-indigo-200">
                            Espelhos gigantescos desviam radiação e usam a estrela como motor. Supernovas são preventivamente esvaziadas.
                        </p>
                        <div class="text-xs font-mono text-indigo-400">
                            Supernovas Neutras: <span id="supernovaePreventedVal" class="text-yellow-300 font-bold">1,840</span>
                        </div>
                    </div>

                    <!-- CARTÃO 4: Rede de Dobras Espaciais -->
                    <div class="glass-panel-hover p-4 rounded-lg bg-pink-950/20 border border-pink-800/40 space-y-2">
                        <div class="flex justify-between items-start">
                            <span class="text-xs font-semibold text-pink-300 flex items-center gap-1.5">
                                <i data-lucide="share-2" class="w-4 h-4"></i>
                                Buracos de Minhoca Artificiais
                            </span>
                            <span id="wormholeStatus" class="text-[10px] px-2 py-0.5 bg-pink-950 border border-pink-800 text-pink-300 rounded">
                                85.000 Nós Conectados
                            </span>
                        </div>
                        <p class="text-xs text-indigo-200">
                            Atalhos contínuos no espaço-tempo evitam o isolamento cultural e biológico provocado pela limitação de $c$.
                        </p>
                        <div class="text-xs font-mono text-indigo-400">
                            Latência Máxima Galáctica: <span id="galaxyLatencyVal" class="text-pink-300 font-bold">0.004 ms</span>
                        </div>
                    </div>

                </div>
            </div>

            <!-- GRÁFICO DINÂMICO DE PROGRESSO KARDASHEV E PODER ENERGÉTICO -->
            <div class="glass-panel p-5 rounded-xl space-y-3">
                <div class="flex items-center justify-between border-b border-indigo-900/60 pb-3">
                    <h3 class="text-base font-bold text-white flex items-center gap-2">
                        <i data-lucide="activity" class="w-5 h-5 text-cyan-400"></i>
                        Projeção Histórica & Galáctica (Watts)
                    </h3>
                    <div class="text-xs text-indigo-300 font-mono">
                        Escala Logarítmica (10³⁰ - 10³⁷+ W)
                    </div>
                </div>

                <!-- CANVAS PARA CHART.JS -->
                <div class="relative w-full h-64">
                    <canvas id="kardashevChart"></canvas>
                </div>
            </div>

            <!-- EVENT LOG DE ENGENHARIA GALÁCTICA -->
            <div class="glass-panel p-4 rounded-xl space-y-2">
                <div class="flex items-center justify-between text-xs text-indigo-300 border-b border-indigo-900/40 pb-2">
                    <span class="font-bold text-white flex items-center gap-1.5">
                        <i data-lucide="terminal" class="w-4 h-4 text-purple-400"></i>
                        Registro de Eventos da Mente Colmeia
                    </span>
                    <span class="text-[10px] text-indigo-400">Rede de Sagitário A*</span>
                </div>
                <div id="eventLog" class="text-xs font-mono space-y-1.5 max-h-32 overflow-y-auto pr-2">
                    <div class="text-indigo-300">
                        <span class="text-indigo-500">[+0.00 Ma]</span> Enxames de Von Neumann colonizaram 40 bilhões de sistemas.
                    </div>
                    <div class="text-purple-300">
                        <span class="text-purple-500">[+0.00 Ma]</span> Usina Penrose em Sagittarius A* atingiu 10³⁵ Watts.
                    </div>
                </div>
            </div>

        </section>

    </main>

    <!-- FOOTER -->
    <footer class="glass-panel border-t border-indigo-900/50 py-4 px-4 text-center text-xs text-indigo-400 mt-auto">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-2">
            <div>
                Simulador Kardashev Nível 3 • Modelo de Civilização Galáctica
            </div>
            <div class="text-indigo-500">
                Via Láctea (100.000 Anos-Luz) • Captura de Energia em Grande Escala
            </div>
        </div>
    </footer>

    <!-- LOGIC & SIMULATION SCRIPT -->
    <script>
        // ESTADO GLOBAL DA SIMULAÇÃO
        let simulationState = {
            elapsedMa: 0.00, // Milhões de anos
            kardashevLevel: 3.08,
            totalPowerWattsExp: 37.08, // 10^37.08 W
            dysonCoveragePct: 12.4, // % das estrelas capturadas
            penrosePowerExp: 35.25,
            mindUploadPct: 99.98,
            bioHumanPct: 0.02,
            systemsColonizedBillions: 48.5,
            preventedSupernovae: 1840,
            wormholeNodes: 85000,
            darkMatterHarvestExp: 32.1
        };

        // CHART.JS INSTANCE
        let kardashevChart;

        // INICIALIZAÇÃO AO CARREGAR A PÁGINA
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            initChart();
            updateSimulation();
        });

        // CRIAÇÃO DO GRÁFICO HISTÓRICO
        function initChart() {
            const ctx = document.getElementById('kardashevChart').getContext('2d');
            
            kardashevChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['+0.0 Ma', '+0.1 Ma', '+0.2 Ma', '+0.3 Ma', '+0.4 Ma', '+0.5 Ma'],
                    datasets: [
                        {
                            label: 'Potência Energética (Exponente 10^x W)',
                            data: [36.8, 37.0, 37.08, 37.15, 37.22, 37.35],
                            borderColor: '#06b6d4',
                            backgroundColor: 'rgba(6, 182, 212, 0.1)',
                            borderWidth: 2,
                            fill: true,
                            tension: 0.4,
                            pointBackgroundColor: '#a855f7'
                        },
                        {
                            label: 'Nível Kardashev (K)',
                            data: [3.01, 3.05, 3.08, 3.10, 3.12, 3.15],
                            borderColor: '#a855f7',
                            borderDash: [5, 5],
                            borderWidth: 2,
                            pointRadius: 0,
                            yAxisID: 'yKardashev'
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            grid: { color: 'rgba(99, 102, 241, 0.1)' },
                            ticks: { color: '#818cf8', font: { size: 10 } }
                        },
                        y: {
                            title: { display: true, text: 'Potência Total (10^x W)', color: '#06b6d4' },
                            grid: { color: 'rgba(99, 102, 241, 0.1)' },
                            ticks: { color: '#06b6d4', font: { size: 10 } },
                            min: 35,
                            max: 38
                        },
                        yKardashev: {
                            position: 'right',
                            title: { display: true, text: 'Índice Kardashev K', color: '#a855f7' },
                            grid: { drawOnChartArea: false },
                            ticks: { color: '#a855f7', font: { size: 10 } },
                            min: 3.0,
                            max: 3.3
                        }
                    },
                    plugins: {
                        legend: {
                            labels: { color: '#e0e7ff', font: { size: 11 } }
                        }
                    }
                }
            });
        }

        // RECALCULAR SIMULAÇÃO A PARTIR DOS SLIDERS
        function updateSimulation() {
            // Obter valores dos sliders (0 a 100)
            const neumannVal = parseFloat(document.getElementById('sliderNeumann').value);
            const penroseVal = parseFloat(document.getElementById('sliderPenrose').value);
            const warpVal = parseFloat(document.getElementById('sliderWarp').value);
            const shkadovVal = parseFloat(document.getElementById('sliderShkadov').value);
            const darkMatterVal = parseFloat(document.getElementById('sliderDarkMatter').value);

            // Atualizar labels dos sliders
            document.getElementById('valNeumann').innerText = neumannVal + '%';
            document.getElementById('valPenrose').innerText = penroseVal + '%';
            document.getElementById('valWarp').innerText = warpVal + '%';
            document.getElementById('valShkadov').innerText = shkadovVal + '%';
            document.getElementById('valDarkMatter').innerText = darkMatterVal + '%';

            // CÁLCULOS DERIVADOS
            
            // Dyson & Von Neumann (% da galáxia capturada)
            const dysonPct = (neumannVal * 0.8) + (simulationState.elapsedMa * 15);
            simulationState.dysonCoveragePct = Math.min(100, dysonPct).toFixed(1);

            // Potência Energética Total (Base de 10^37 Watts)
            // K = (log10(P) - 6) / 10  -> Se P = 10^37 W => K = 3.1
            const basePowerExp = 36.5 + (neumannVal * 0.01) + (penroseVal * 0.012) + (darkMatterVal * 0.005) + (simulationState.elapsedMa * 0.2);
            simulationState.totalPowerWattsExp = basePowerExp.toFixed(2);
            
            // Nível Kardashev exato: (P_exp - 6) / 10
            const kLevel = (basePowerExp - 6) / 10;
            simulationState.kardashevLevel = kLevel.toFixed(2);

            // Sagitário A* Penrose Process
            const penroseWatts = (34.0 + (penroseVal * 0.03)).toFixed(1);
            
            // Mover Estrelas e Supernovas
            const supernovae = Math.floor(shkadovVal * 45 + (simulationState.elapsedMa * 1200));

            // Buracos de Minhoca / Latência
            const wormholes = Math.floor(warpVal * 2200 + (simulationState.elapsedMa * 50000));
            const latency = Math.max(0.001, (100 - warpVal) * 0.05).toFixed(3);

            // Coesão de Mente Colmeia
            const hiveCohesion = Math.min(100, Math.floor((warpVal * 0.5) + (darkMatterVal * 0.2) + 35));

            // ATUALIZAR INTERFACE
            document.getElementById('headerPower').innerText = `1.0 × 10³⁷.${Math.floor((basePowerExp % 1)*100)} W`;
            document.getElementById('headerKardashev').innerText = `${simulationState.kardashevLevel} K`;
            document.getElementById('dysonCoverageVal').innerText = `${simulationState.dysonCoveragePct}%`;
            document.getElementById('penroseEfficiencyVal').innerText = `1.0 × 10³⁵.${Math.floor((penroseWatts % 1)*100)} W`;
            document.getElementById('supernovaePreventedVal').innerText = supernovae.toLocaleString('pt-BR');
            document.getElementById('wormholeStatus').innerText = `${wormholes.toLocaleString('pt-BR')} Nós Conectados`;
            document.getElementById('galaxyLatencyVal').innerText = `${latency} ms`;
            
            // Coesão da Hive Mind
            document.getElementById('hiveCohesionVal').innerText = `${hiveCohesion}%`;
            document.getElementById('hiveCohesionBar').style.width = `${hiveCohesion}%`;

            // Estrelas reorientadas
            document.getElementById('shkadovStatus').innerText = `${Math.floor(shkadovVal * 120)}k Estrelas Reorientadas`;
        }

        // AVANÇAR TEMPO (SIMULAR PRÓXIMA ERA DE 100 MIL ANOS)
        function advanceEpoch() {
            simulationState.elapsedMa += 0.10; // Avança 100k anos (0.10 Ma)
            
            document.getElementById('headerYear').innerText = `+${simulationState.elapsedMa.toFixed(2)} Ma`;

            // Incrementar valores dos sliders dinamicamente para simular progresso autônomo
            const neumannSlider = document.getElementById('sliderNeumann');
            if (parseInt(neumannSlider.value) < 100) {
                neumannSlider.value = parseInt(neumannSlider.value) + 2;
            }

            const warpSlider = document.getElementById('sliderWarp');
            if (parseInt(warpSlider.value) < 100) {
                warpSlider.value = parseInt(warpSlider.value) + 3;
            }

            // Recalcular simulação
            updateSimulation();

            // Adicionar evento ao Log
            const eventLog = document.getElementById('eventLog');
            const newLog = document.createElement('div');
            
            const logsArray = [
                `Sondas Von Neumann alcançaram o Braço de Orion (+${simulationState.elapsedMa.toFixed(2)} Ma).`,
                `Novo buraco de minhoca estabilizado ligando Sagitário A* ao Setor Perseus.`,
                `Propulsores Shkadov neutralizaram risco de supernova no sistema Betelgeuse.`,
                `Usinas de Matéria Escura expandiram capacidade de contenção gravitacional.`
            ];
            
            const randomLog = logsArray[Math.floor(Math.random() * logsArray.length)];
            newLog.className = "text-cyan-300 transition-all animate-fadeIn";
            newLog.innerHTML = `<span class="text-cyan-500">[+${simulationState.elapsedMa.toFixed(2)} Ma]</span> ${randomLog}`;
            
            eventLog.prepend(newLog);

            // Atualizar gráfico Chart.js
            updateChartData();
        }

        // ATUALIZAR GRÁFICO AO AVANÇAR O TEMPO
        function updateChartData() {
            const currentExp = parseFloat(simulationState.totalPowerWattsExp);
            const currentK = parseFloat(simulationState.kardashevLevel);
            
            // Adicionar novo label e ponto de dados
            const newLabel = `+${simulationState.elapsedMa.toFixed(1)} Ma`;
            
            kardashevChart.data.labels.push(newLabel);
            kardashevChart.data.datasets[0].data.push(currentExp);
            kardashevChart.data.datasets[1].data.push(currentK);

            // Manter no máximo 8 pontos no gráfico para clareza
            if (kardashevChart.data.labels.length > 8) {
                kardashevChart.data.labels.shift();
                kardashevChart.data.datasets[0].data.shift();
                kardashevChart.data.datasets[1].data.shift();
            }

            kardashevChart.update();
        }
    </script>
</body>
</html>
