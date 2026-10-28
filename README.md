# OFProjetc[ProjetoDG.html](https://github.com/user-attachments/files/34075893/ProjetoDG.html)
<!DOCTYPE html>
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MetaDG eSports Center - Gestão de Estações e Simuladores</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        grafite: {
                            DEFAULT: '#1C1C1F',
                            surface: '#222226',
                            card: '#2A2A30',
                            input: '#141417',
                            border: '#383840'
                        },
                        navy: {
                            DEFAULT: '#0F4C81',
                            hover: '#0C3E6A',
                            dark: '#082845',
                            light: '#1B619E',
                            subtle: 'rgba(15, 76, 129, 0.15)'
                        },
                        cyan: {
                            DEFAULT: '#00F5FF',
                            hover: '#33F7FF',
                            dim: 'rgba(0, 245, 255, 0.12)',
                            border: 'rgba(0, 245, 255, 0.3)'
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        display: ['Space Grotesk', 'sans-serif'],
                        mono: ['ui-monospace', 'SFMono-Regular', 'Menlo', 'Monaco', 'Consolas', 'monospace']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #1C1C1F;
            color: #E4E4E7;
            font-family: 'Inter', sans-serif;
        }

        /* Custom scrollbar for tabular data and modal preview */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #141417;
        }
        ::-webkit-scrollbar-thumb {
            background: #0F4C81;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00F5FF;
        }

        .accent-glow {
            box-shadow: 0 0 15px rgba(0, 245, 255, 0.15);
        }
        
        .accent-glow-button {
            box-shadow: 0 0 12px rgba(0, 245, 255, 0.25);
            transition: all 0.2s ease-in-out;
        }
        .accent-glow-button:hover {
            box-shadow: 0 0 20px rgba(0, 245, 255, 0.45);
        }

        .tab-btn.active {
            border-bottom-color: #00F5FF;
            color: #00F5FF;
            background-color: rgba(15, 76, 129, 0.2);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-grafite text-zinc-100 antialiased selection:bg-cyan selection:text-grafite">

    <!-- Toast Notifications Container -->
    <div id="toastContainer" class="fixed top-20 right-6 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none"></div>

    <!-- HEADER / NAVIGATION BAR -->
    <header class="bg-grafite-surface border-b border-grafite-border sticky top-0 z-40 shadow-xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                
                 
<!-- BRAND / LOGO AREA -->
<div class="flex items-center gap-4">

    <!-- LOGO METADG -->
    <div class="flex-shrink-0 flex items-center justify-center">
        <img
            src="./metadg-logo.jpeg"
            alt="Logo da MetaDG eSports"
            class="w-16 h-[72px] object-contain"
        >
    </div>

    <!-- DIVISOR -->
    <div class="h-10 w-px bg-grafite-border hidden sm:block"></div>

</div>

                    <!-- Title & System Identifier -->
                    <div>
                        <div class="flex items-center gap-2">
                            <h1 class="font-display font-bold text-lg sm:text-xl text-white tracking-tight">
                                MetaDG <span class="text-cyan">eSports Center</span>
                            </h1>
                            <span class="hidden md:inline-block px-2 py-0.5 text-[10px] font-semibold tracking-wider text-cyan bg-cyan-dim border border-cyan-border rounded">
                                UNIDADE METADG
                            </span>
                        </div>
                        <p class="text-xs text-zinc-400">Sistema de Gestão de Estações e Simuladores VR</p>
                    </div>
                </div>

                <!-- RIGHT HEADER CONTROLS -->
                <div class="flex items-center gap-3">
                    <div class="hidden lg:flex items-center gap-2 bg-grafite-input border border-grafite-border px-3 py-1.5 rounded-lg text-xs font-mono text-zinc-300">
                        <i class="fa-solid fa-file-lines text-navy-light"></i>
                        <span>jogadores_sessoes.txt</span>
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse ml-1"></span>
                    </div>

                    <button onclick="openTxtModal()" 
                        class="px-3.5 py-2 bg-navy hover:bg-navy-hover text-white rounded-lg text-xs font-semibold border border-navy-light/40 transition flex items-center gap-2">
                        <i class="fa-solid fa-terminal text-cyan"></i>
                        <span class="hidden sm:inline">Visualizar TXT</span>
                    </button>

                    <button onclick="exportTxtFile()" 
                        class="px-3.5 py-2 bg-cyan hover:bg-cyan-hover text-grafite font-bold rounded-lg text-xs transition flex items-center gap-2 accent-glow-button">
                        <i class="fa-solid fa-download"></i>
                        <span class="hidden sm:inline">Exportar TXT</span>
                    </button>
                </div>

            </div>
        </div>
    </header>

    <!-- MAIN DASHBOARD CONTENT -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- DASHBOARD METRICS SUMMARY -->
        <section class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            
            <!-- Metric 1: Total Sessions -->
            <div class="bg-grafite-surface border border-grafite-border rounded-xl p-4 flex items-center justify-between shadow-md">
                <div>
                    <span class="text-xs font-semibold text-zinc-400 uppercase tracking-wider">Sessões Registradas</span>
                    <div id="statTotalSessao" class="font-display text-2xl font-bold text-white mt-1">0</div>
                    <span class="text-[11px] text-zinc-400 mt-1 block">Atendimentos na unidade</span>
                </div>
                <div class="w-12 h-12 rounded-xl bg-navy/30 border border-navy-light/40 flex items-center justify-center text-cyan text-lg">
                    <i class="fa-solid fa-gamepad"></i>
                </div>
            </div>

            <!-- Metric 2: Gross Revenue -->
            <div class="bg-grafite-surface border border-grafite-border rounded-xl p-4 flex items-center justify-between shadow-md">
                <div>
                    <span class="text-xs font-semibold text-zinc-400 uppercase tracking-wider">Faturamento Acumulado</span>
                    <div id="statTotalFaturamento" class="font-display text-2xl font-bold text-emerald-400 mt-1">R$ 0,00</div>
                    <span class="text-[11px] text-zinc-400 mt-1 block">Receita bruta em caixa</span>
                </div>
                <div class="w-12 h-12 rounded-xl bg-emerald-500/10 border border-emerald-500/20 flex items-center justify-center text-emerald-400 text-lg">
                    <i class="fa-solid fa-wallet"></i>
                </div>
            </div>

            <!-- Metric 3: VR Usage -->
            <div class="bg-grafite-surface border border-grafite-border rounded-xl p-4 flex items-center justify-between shadow-md">
                <div>
                    <span class="text-xs font-semibold text-zinc-400 uppercase tracking-wider">Simuladores VR</span>
                    <div id="statTotalVR" class="font-display text-2xl font-bold text-purple-300 mt-1">0</div>
                    <span class="text-[11px] text-zinc-400 mt-1 block">Sessões em realidade virtual</span>
                </div>
                <div class="w-12 h-12 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400 text-lg">
                    <i class="fa-solid fa-vr-cardboard"></i>
                </div>
            </div>

            <!-- Metric 4: Operational Regime -->
            <div class="bg-grafite-surface border border-grafite-border rounded-xl p-4 flex items-center justify-between shadow-md">
                <div>
                    <span class="text-xs font-semibold text-zinc-400 uppercase tracking-wider">Regime Operacional</span>
                    <div id="statOperacaoStatus" class="font-display text-sm font-semibold text-zinc-200 mt-2 flex items-center gap-2">
                        <span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span> Padrão Semanal
                    </div>
                    <span id="statOperacaoSub" class="text-[11px] text-zinc-400 mt-1 block">Tarifação regular de estação</span>
                </div>
                <div class="w-12 h-12 rounded-xl bg-navy/30 border border-navy-light/40 flex items-center justify-center text-cyan text-lg">
                    <i class="fa-solid fa-clock-rotate-left"></i>
                </div>
            </div>

        </section>

        <!-- MAIN WORKSPACE GRID -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

            <!-- LEFT COLUMN: SESSION REGISTRATION FORM (5 Cols) -->
            <section class="lg:col-span-5 bg-grafite-surface border border-grafite-border rounded-xl shadow-xl overflow-hidden">
                
                <!-- Form Section Header -->
                <div class="bg-grafite-card px-5 py-4 border-b border-grafite-border flex items-center justify-between">
                    <div class="flex items-center gap-2.5">
                        <div class="w-2 h-4 bg-cyan rounded-full"></div>
                        <h2 class="font-display font-bold text-base text-white">Nova Sessão de Uso</h2>
                    </div>
                    
                    <button type="button" onclick="fillPersonaPedro()" 
                        class="text-xs font-medium text-cyan hover:text-cyan-hover bg-cyan-dim border border-cyan-border px-2.5 py-1 rounded transition flex items-center gap-1.5">
                        <i class="fa-solid fa-user-check text-[10px]"></i>
                        <span>Persona Pedro</span>
                    </button>
                </div>

                <!-- Registration Form -->
                <form id="sessionForm" onsubmit="handleFormSubmit(event)" class="p-5 space-y-4">

                    <!-- ID Cabine -->
                    <div>
                        <label class="block text-xs font-semibold text-zinc-300 mb-1.5">
                            ID da Cabine / Estação <span class="text-cyan">*</span>
                        </label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-zinc-500 text-xs">
                                <i class="fa-solid fa-desktop"></i>
                            </span>
                            <input type="text" id="idCabine" required placeholder="Ex: CAB-01 ou VR-02"
                                class="w-full bg-grafite-input border border-grafite-border rounded-lg pl-9 pr-3 py-2.5 text-xs text-white placeholder-zinc-500 focus:outline-none focus:border-cyan focus:ring-1 focus:ring-cyan transition">
                        </div>
                    </div>

                    <!-- Nick Jogador -->
                    <div>
                        <label class="block text-xs font-semibold text-zinc-300 mb-1.5">
                            Nick do Jogador <span class="text-cyan">*</span>
                        </label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-zinc-500 text-xs">
                                <i class="fa-solid fa-user"></i>
                            </span>
                            <input type="text" id="nickJogador" required placeholder="Ex: shaolinmatadordeporco67"
                                class="w-full bg-grafite-input border border-grafite-border rounded-lg pl-9 pr-3 py-2.5 text-xs text-white placeholder-zinc-500 focus:outline-none focus:border-cyan focus:ring-1 focus:ring-cyan transition">
                        </div>
                    </div>

                    <!-- Jogo Escolhido -->
                    <div>
                        <label class="block text-xs font-semibold text-zinc-300 mb-1.5">
                            Jogo / Simulador Escolhido <span class="text-cyan">*</span>
                        </label>
                        <div class="relative">
                            <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-zinc-500 text-xs">
                                <i class="fa-solid fa-crosshairs"></i>
                            </span>
                            <input type="text" id="jogoEscolhado" required placeholder="Ex: Valorant, CS2, Beat Saber VR"
                                class="w-full bg-grafite-input border border-grafite-border rounded-lg pl-9 pr-3 py-2.5 text-xs text-white placeholder-zinc-500 focus:outline-none focus:border-cyan focus:ring-1 focus:ring-cyan transition">
                        </div>
                    </div>

                    <!-- Minutes & Cost Row -->
                    <div class="grid grid-cols-2 gap-3">
                        
                        <!-- Minutos de Uso -->
                        <div>
                            <label class="block text-xs font-semibold text-zinc-300 mb-1.5">
                                Minutos de Uso <span class="text-cyan">*</span>
                            </label>
                            <div class="relative">
                                <input type="number" id="minutosUso" min="0" required placeholder="120" oninput="validatePositiveInputs()"
                                    class="w-full bg-grafite-input border border-grafite-border rounded-lg px-3 py-2.5 text-xs text-white font-mono placeholder-zinc-500 focus:outline-none focus:border-cyan focus:ring-1 focus:ring-cyan transition">
                            </div>
                            <span id="errorMinutos" class="text-[10px] text-red-400 hidden mt-1 block">Não aceita números negativos</span>
                        </div>

                        <!-- Valor Total R$ -->
                        <div>
                            <label class="block text-xs font-semibold text-zinc-300 mb-1.5">
                                Valor Total (R$) <span class="text-cyan">*</span>
                            </label>
                            <div class="relative">
                                <input type="number" id="valorTotal" min="0" step="0.01" required placeholder="25.00" oninput="validatePositiveInputs()"
                                    class="w-full bg-grafite-input border border-grafite-border rounded-lg px-3 py-2.5 text-xs text-white font-mono placeholder-zinc-500 focus:outline-none focus:border-cyan focus:ring-1 focus:ring-cyan transition">
                            </div>
                            <span id="errorValor" class="text-[10px] text-red-400 hidden mt-1 block">Não aceita valores negativos</span>
                        </div>

                    </div>

                    <!-- Status VR -->
                    <div>
                        <label class="block text-xs font-semibold text-zinc-300 mb-1.5">Recursos de VR (Realidade Virtual)</label>
                        <select id="statusVR" class="w-full bg-grafite-input border border-grafite-border rounded-lg px-3 py-2.5 text-xs text-white focus:outline-none focus:border-cyan transition">
                            <option value="Desativado">Desativado (Estação PC Gamer)</option>
                            <option value="Ativado">Ativado (Óculos / Simulador VR)</option>
                        </select>
                    </div>

                    <!-- Weekend Operation Toggle -->
                    <div class="p-3 bg-grafite-input border border-grafite-border rounded-lg flex items-center justify-between">
                        <div>
                            <label for="plantaoFDS" class="text-xs font-semibold text-zinc-200 block cursor-pointer">Operação de Final de Semana</label>
                            <span class="text-[11px] text-zinc-400 block">Regra de fechamento e tarifação especial</span>
                        </div>
                        <input type="checkbox" id="plantaoFDS" class="w-4 h-4 accent-cyan rounded cursor-pointer">
                    </div>

                    <!-- Submit Button -->
                    <button type="submit" 
                        class="w-full py-3 px-4 bg-cyan hover:bg-cyan-hover text-grafite font-bold rounded-lg text-xs transition duration-200 flex items-center justify-center gap-2 accent-glow-button mt-3">
                        <i class="fa-solid fa-floppy-disk"></i>
                        <span>Registrar e Persistir Sessão</span>
                    </button>

                </form>

            </section>

            <!-- RIGHT COLUMN: RECORDS TABLE & PERSISTENCE PREVIEW (7 Cols) -->
            <section class="lg:col-span-7 space-y-4">
                
                <div class="bg-grafite-surface border border-grafite-border rounded-xl shadow-xl overflow-hidden">
                    
                    <!-- Table Toolbar -->
                    <div class="bg-grafite-card px-5 py-4 border-b border-grafite-border flex flex-col sm:flex-row items-start sm:items-center justify-between gap-3">
                        <div class="flex items-center gap-2.5">
                            <div class="w-2 h-4 bg-navy-light rounded-full"></div>
                            <h2 class="font-display font-bold text-base text-white">Registros Ativos</h2>
                        </div>

                        <!-- Real-time Filter -->
                        <div class="relative w-full sm:w-64">
                            <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-zinc-500 text-xs">
                                <i class="fa-solid fa-magnifying-glass"></i>
                            </span>
                            <input type="text" id="searchInput" oninput="filterTable()" placeholder="Buscar por Nick ou Cabine..."
                                class="w-full bg-grafite-input border border-grafite-border rounded-lg pl-9 pr-3 py-1.5 text-xs text-white placeholder-zinc-500 focus:outline-none focus:border-cyan transition">
                        </div>
                    </div>

                    <!-- Table Data Container -->
                    <div class="overflow-x-auto min-h-[320px]">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="bg-navy/30 border-b border-grafite-border text-[11px] font-semibold text-zinc-300 uppercase tracking-wider">
                                    <th class="p-3 pl-5">Cabine</th>
                                    <th class="p-3">Jogador</th>
                                    <th class="p-3">Jogo / Simulador</th>
                                    <th class="p-3">Tempo</th>
                                    <th class="p-3">Valor</th>
                                    <th class="p-3">VR</th>
                                    <th class="p-3 pr-5 text-right">Ação</th>
                                </tr>
                            </thead>
                            <tbody id="sessionTableBody" class="divide-y divide-grafite-border text-xs text-zinc-200">
                                <!-- Dynamic rows via JavaScript -->
                            </tbody>
                        </table>

                        <!-- Empty State Indicator -->
                        <div id="emptyState" class="hidden py-12 text-center">
                            <i class="fa-solid fa-folder-open text-zinc-600 text-3xl mb-2"></i>
                            <p class="text-xs text-zinc-400">Nenhuma sessão encontrada no arquivo de registros.</p>
                        </div>
                    </div>

                    <!-- Table Footer Status -->
                    <div class="bg-grafite-card px-5 py-3 border-t border-grafite-border flex flex-wrap items-center justify-between text-xs text-zinc-400 gap-2">
                        <span id="recordCountText">Carregando registros...</span>
                        <div class="flex items-center gap-2">
                            <button onclick="clearAllData()" class="text-zinc-500 hover:text-red-400 transition text-[11px]">
                                Redefinir Dados
                            </button>
                        </div>
                    </div>

                </div>

                <!-- PERSISTENCE SPECIFICATION BOX -->
                <div class="bg-grafite-surface border border-grafite-border rounded-xl p-4 text-xs space-y-2">
                    <div class="flex items-center justify-between border-b border-grafite-border pb-2">
                        <span class="font-semibold text-zinc-200 flex items-center gap-2">
                            <i class="fa-solid fa-database text-cyan"></i>
                            Estrutura de Persistência em Disco
                        </span>
                        <span class="text-[10px] font-mono text-zinc-400">Delimitador ';'</span>
                    </div>
                    <p class="text-zinc-400 text-[11px] leading-relaxed">
                        Os dados registrados nesta interface são formatados e sincronizados no padrão delimitado para consumo pelas rotinas de manipulação de arquivos em Java.
                    </p>
                    <div class="bg-grafite-input p-2.5 rounded-lg border border-grafite-border font-mono text-[11px] text-emerald-400 overflow-x-auto">
                        ID_CABINE;NICK_JOGADOR;JOGO;MINUTOS;VALOR;STATUS_VR
                    </div>
                </div>

            </section>

        </div>

    </main>

    <!-- FOOTER -->
    <footer class="bg-grafite-surface border-t border-grafite-border py-4 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between text-xs text-zinc-500 gap-2">
            <div>
                <span class="font-semibold text-zinc-400">MetaDG eSports Center</span> &bull; Unidade MetaDG Gestão Operacional
            </div>
            <div class="text-[11px]">
                Sistemas e Banco de Dados &bull; Aula 2
            </div>
        </div>
    </footer>

    <!-- TXT FILE PREVIEW MODAL -->
    <div id="txtModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-grafite-surface border border-grafite-border rounded-xl max-w-2xl w-full p-6 shadow-2xl relative flex flex-col max-h-[85vh]">
            
            <!-- Modal Header -->
            <div class="flex items-center justify-between border-b border-grafite-border pb-4 mb-4">
                <div>
                    <h3 class="font-display font-bold text-white text-base">Visualizador de Arquivo Bruto</h3>
                    <p class="text-xs text-zinc-400">Conteúdo exato gravado em <code class="text-cyan font-mono">jogadores_sessoes.txt</code></p>
                </div>
                <button onclick="closeTxtModal()" class="text-zinc-400 hover:text-white transition p-1">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>

            <!-- TXT Content Box -->
            <div class="flex-1 bg-grafite-input rounded-lg p-4 border border-grafite-border overflow-y-auto font-mono text-xs text-emerald-400 leading-relaxed min-h-[220px]">
                <pre id="txtContentDisplay" class="whitespace-pre-wrap"></pre>
            </div>

            <!-- Modal Footer Actions -->
            <div class="flex items-center justify-between mt-5 pt-4 border-t border-grafite-border">
                <button onclick="copyTxtContent()" 
                    class="px-4 py-2 bg-navy hover:bg-navy-hover text-white rounded-lg text-xs font-semibold transition flex items-center gap-2">
                    <i class="fa-solid fa-copy text-cyan"></i>
                    <span>Copiar Conteúdo</span>
                </button>
                <button onclick="exportTxtFile()" 
                    class="px-4 py-2 bg-cyan hover:bg-cyan-hover text-grafite font-bold rounded-lg text-xs transition flex items-center gap-2 accent-glow-button">
                    <i class="fa-solid fa-download"></i>
                    <span>Baixar Arquivo TXT</span>
                </button>
            </div>

        </div>
    </div>

    <!-- JAVASCRIPT LOGIC AND BUSINESS RULES -->
    <script>
        // Default initial session dataset
        const defaultInitialData = [
            {
                idCabine: 'CAB-01',
                nickJogador: 'shaolinmatadordeporco67',
                jogoEscolhado: 'Valorant',
                minutosUso: 120,
                valorTotal: 25.00,
                statusVR: 'Desativado',
                plantaoFDS: false
            },
            {
                idCabine: 'VR-01',
                nickJogador: 'Pedro_Gamer',
                jogoEscolhado: 'Assetto Corsa VR',
                minutosUso: 60,
                valorTotal: 35.00,
                statusVR: 'Ativado',
                plantaoFDS: false
            }
        ];

        let sessions = [];

        // INITIALIZATION
        window.onload = function() {
            loadSessionsFromStorage();
            renderTable();
            updateDashboardMetrics();
        };

        // LOCAL STORAGE HELPERS
        function loadSessionsFromStorage() {
            const saved = localStorage.getItem('metadg_sessoes_data');
            if (saved) {
                try {
                    sessions = JSON.parse(saved);
                } catch(e) {
                    sessions = [...defaultInitialData];
                }
            } else {
                sessions = [...defaultInitialData];
                saveSessionsToStorage();
            }
        }

        function saveSessionsToStorage() {
            localStorage.setItem('metadg_sessoes_data', JSON.stringify(sessions));
        }

        // VALIDATION HELPERS
        function validatePositiveInputs() {
            const minutos = parseFloat(document.getElementById('minutosUso').value);
            const valor = parseFloat(document.getElementById('valorTotal').value);

            const errMin = document.getElementById('errorMinutos');
            const errVal = document.getElementById('errorValor');

            let isValid = true;

            if (minutos < 0) {
                errMin.classList.remove('hidden');
                isValid = false;
            } else {
                errMin.classList.add('hidden');
            }

            if (valor < 0) {
                errVal.classList.remove('hidden');
                isValid = false;
            } else {
                errVal.classList.add('hidden');
            }

            return isValid;
        }

        // RENDER TABLE
        function renderTable(filteredData = null) {
            const tbody = document.getElementById('sessionTableBody');
            const emptyState = document.getElementById('emptyState');
            const dataToRender = filteredData || sessions;

            tbody.innerHTML = '';

            if (dataToRender.length === 0) {
                emptyState.classList.remove('hidden');
            } else {
                emptyState.classList.add('hidden');
                dataToRender.forEach((session) => {
                    const actualIndex = sessions.indexOf(session);
                    const isPedro = session.nickJogador.toLowerCase() === 'shaolinmatadordeporco67';

                    const tr = document.createElement('tr');
                    tr.className = `hover:bg-navy/10 transition ${isPedro ? 'bg-navy/10' : ''}`;

                    tr.innerHTML = `
                        <td class="p-3 pl-5 font-mono font-semibold text-white">${escapeHtml(session.idCabine)}</td>
                        <td class="p-3 font-medium">
                            ${escapeHtml(session.nickJogador)}
                            ${isPedro ? '<span class="ml-1.5 px-1.5 py-0.5 text-[9px] font-mono bg-cyan-dim text-cyan border border-cyan-border rounded">PERSONA</span>' : ''}
                        </td>
                        <td class="p-3 text-zinc-300">${escapeHtml(session.jogoEscolhado)}</td>
                        <td class="p-3 font-mono text-zinc-300">${session.minutosUso} min</td>
                        <td class="p-3 font-mono font-semibold text-emerald-400">R$ ${Number(session.valorTotal).toFixed(2)}</td>
                        <td class="p-3">
                            <span class="px-2 py-0.5 rounded text-[10px] font-semibold ${session.statusVR === 'Ativado' ? 'bg-purple-500/20 text-purple-300 border border-purple-500/30' : 'bg-zinc-800 text-zinc-400'}">
                                ${session.statusVR}
                            </span>
                        </td>
                        <td class="p-3 pr-5 text-right">
                            <button onclick="deleteSession(${actualIndex})" class="text-zinc-500 hover:text-red-400 transition p-1" title="Remover Registro">
                                <i class="fa-solid fa-trash-can"></i>
                            </button>
                        </td>
                    `;
                    tbody.appendChild(tr);
                });
            }

            document.getElementById('recordCountText').innerText = `Exibindo ${dataToRender.length} de ${sessions.length} registros persistidos`;
        }

        // FORM SUBMISSION
        function handleFormSubmit(e) {
            e.preventDefault();

            if (!validatePositiveInputs()) {
                showToast('Atenção: Correção necessária nos campos de minutos ou valor.', 'error');
                return;
            }

            const idCabine = document.getElementById('idCabine').value.trim();
            const nickJogador = document.getElementById('nickJogador').value.trim();
            const jogoEscolhado = document.getElementById('jogoEscolhado').value.trim();
            const minutosUso = parseInt(document.getElementById('minutosUso').value);
            const valorTotal = parseFloat(document.getElementById('valorTotal').value);
            const statusVR = document.getElementById('statusVR').value;
            const plantaoFDS = document.getElementById('plantaoFDS').checked;

            if (minutosUso < 0 || valorTotal < 0) {
                showToast('Valores negativos não são permitidos.', 'error');
                return;
            }

            const newSession = {
                idCabine,
                nickJogador,
                jogoEscolhado,
                minutosUso,
                valorTotal,
                statusVR,
                plantaoFDS
            };

            sessions.unshift(newSession);
            saveSessionsToStorage();
            renderTable();
            updateDashboardMetrics();

            document.getElementById('sessionForm').reset();
            document.getElementById('plantaoFDS').checked = false;

            showToast('Sessão cadastrada e salva com sucesso.', 'success');
        }

        // PREFILL PERSONA PEDRO
        function fillPersonaPedro() {
            document.getElementById('idCabine').value = 'CAB-01';
            document.getElementById('nickJogador').value = 'shaolinmatadordeporco67';
            document.getElementById('jogoEscolhado').value = 'Valorant';
            document.getElementById('minutosUso').value = 180;
            document.getElementById('valorTotal').value = 35.00;
            document.getElementById('statusVR').value = 'Desativado';
            document.getElementById('plantaoFDS').checked = false;

            validatePositiveInputs();
            showToast('Atleta Pedro Henrique (shaolinmatadordeporco67) carregado.', 'info');
        }

        // DELETE SESSION
        function deleteSession(index) {
            if (confirm('Confirmar exclusão deste registro de sessão?')) {
                sessions.splice(index, 1);
                saveSessionsToStorage();
                renderTable();
                updateDashboardMetrics();
                showToast('Registro excluído do arquivo.', 'info');
            }
        }

        // SEARCH FILTER
        function filterTable() {
            const query = document.getElementById('searchInput').value.toLowerCase().trim();
            if (!query) {
                renderTable();
                return;
            }
            const filtered = sessions.filter(s => 
                s.nickJogador.toLowerCase().includes(query) || 
                s.idCabine.toLowerCase().includes(query) ||
                s.jogoEscolhado.toLowerCase().includes(query)
            );
            renderTable(filtered);
        }

        // METRICS UPDATE
        function updateDashboardMetrics() {
            document.getElementById('statTotalSessao').innerText = sessions.length;

            const totalFaturamento = sessions.reduce((acc, curr) => acc + Number(curr.valorTotal), 0);
            document.getElementById('statTotalFaturamento').innerText = `R$ ${totalFaturamento.toFixed(2)}`;

            const totalVR = sessions.filter(s => s.statusVR === 'Ativado').length;
            document.getElementById('statTotalVR').innerText = totalVR;

            const hasFDS = sessions.some(s => s.plantaoFDS);
            const statusEl = document.getElementById('statOperacaoStatus');
            const subEl = document.getElementById('statOperacaoSub');

            if (hasFDS) {
                statusEl.className = 'font-display text-sm font-semibold text-amber-400 mt-2 flex items-center gap-2';
                statusEl.innerHTML = '<span class="w-2.5 h-2.5 rounded-full bg-amber-400"></span> Operação de Fim de Semana';
                subEl.innerText = 'Fechamento de plantão ativo';
            } else {
                statusEl.className = 'font-display text-sm font-semibold text-emerald-400 mt-2 flex items-center gap-2';
                statusEl.innerHTML = '<span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span> Operação Semanal Padrão';
                subEl.innerText = 'Tarifação regular de estação';
            }
        }

        // TXT DELIMITED STRING GENERATOR
        function generateTxtContent() {
            if (sessions.length === 0) return '';
            return sessions.map(s => 
                `${s.idCabine};${s.nickJogador};${s.jogoEscolhado};${s.minutosUso};${Number(s.valorTotal).toFixed(2)};${s.statusVR}`
            ).join('\n');
        }

        // MODAL FUNCTIONS
        function openTxtModal() {
            const content = generateTxtContent();
            document.getElementById('txtContentDisplay').innerText = content || '// Arquivo de registros vazio.';
            document.getElementById('txtModal').classList.remove('hidden');
        }

        function closeTxtModal() {
            document.getElementById('txtModal').classList.add('hidden');
        }

        function copyTxtContent() {
            const content = generateTxtContent();
            if (!content) {
                showToast('Sem registros para copiar.', 'info');
                return;
            }
            const tempTextArea = document.createElement('textarea');
            document.body.appendChild(tempTextArea);
            tempTextArea.value = content;
            tempTextArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextArea);
            showToast('Conteúdo TXT copiado para a área de transferência.', 'success');
        }

        function exportTxtFile() {
            const content = generateTxtContent();
            const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = 'jogadores_sessoes.txt';
            link.click();
            URL.revokeObjectURL(link.href);
            showToast('Download de jogadores_sessoes.txt concluído.', 'success');
        }

        function clearAllData() {
            if (confirm('Deseja redefinir os dados para o padrão inicial?')) {
                sessions = [...defaultInitialData];
                saveSessionsToStorage();
                renderTable();
                updateDashboardMetrics();
                showToast('Dados redefinidos.', 'info');
            }
        }

        // UTILITY: TOAST NOTIFICATION
        function showToast(message, type = 'info') {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');

            let borderColor = 'border-navy-light';
            if (type === 'success') borderColor = 'border-emerald-500';
            if (type === 'error') borderColor = 'border-red-500';

            toast.className = `bg-grafite-surface border ${borderColor} p-3 rounded-lg shadow-2xl text-xs text-white pointer-events-auto transition duration-200 flex items-center gap-2`;
            
            let icon = 'fa-circle-info text-cyan';
            if (type === 'success') icon = 'fa-circle-check text-emerald-400';
            if (type === 'error') icon = 'fa-triangle-exclamation text-red-400';

            toast.innerHTML = `<i class="fa-solid ${icon}"></i> <span>${escapeHtml(message)}</span>`;

            container.appendChild(toast);

            setTimeout(() => {
                if (toast.parentNode) {
                    toast.parentNode.removeChild(toast);
                }
            }, 3200);
        }

        // UTILITY: ESCAPE HTML
        function escapeHtml(text) {
            if (!text) return '';
            return String(text).replace(/[&<>"']/g, function(m) {
                return {
                    '&': '&amp;',
                    '<': '&lt;',
                    '>': '&gt;',
                    '"': '&quot;',
                    "'": '&#039;'
                }[m];
            });
        }
    </script>
</body>
</html>
