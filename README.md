<!DOCTYPE html>
<html lang="id" class="scroll-smooth dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SAYYID://DATA_TERMINAL | Data Analyst, Data Scientist & ML Engineer</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: JetBrains Mono & Fira Code -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" rel="stylesheet" />

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            mono: ['"JetBrains Mono"', '"Fira Code"', 'monospace'],
          },
          colors: {
            term: {
              bg: '#090A10',
              panel: '#0E101A',
              border: '#1E2235',
              cyan: '#00F5D4',
              pink: '#FF2A85',
              yellow: '#FEE440',
              green: '#39FF14',
              purple: '#9B5DE5',
            }
          }
        }
      }
    };
  </script>

  <style>
    body {
      background-color: #090A10;
      color: #E2E8F0;
      font-family: 'JetBrains Mono', monospace;
      overflow-x: hidden;
    }

    /* Subtle CRT Scanline Effect (Toggleable) */
    .crt-overlay {
      background: linear-gradient(
        rgba(18, 16, 16, 0) 50%,
        rgba(0, 0, 0, 0.28) 50%
      ), linear-gradient(
        90deg,
        rgba(255, 0, 0, 0.03),
        rgba(0, 255, 0, 0.01),
        rgba(0, 0, 255, 0.03)
      );
      background-size: 100% 3px, 6px 100%;
      pointer-events: none;
    }

    /* Neon ASCII Box Borders */
    .ascii-box {
      background: rgba(14, 16, 26, 0.88);
      border: 1px solid #262B44;
      position: relative;
      transition: all 0.25s ease;
    }

    .ascii-box-cyan:hover {
      border-color: #00F5D4;
      box-shadow: 0 0 22px rgba(0, 245, 212, 0.18);
    }

    .ascii-box-pink:hover {
      border-color: #FF2A85;
      box-shadow: 0 0 22px rgba(255, 42, 133, 0.18);
    }

    .ascii-box-yellow:hover {
      border-color: #FEE440;
      box-shadow: 0 0 22px rgba(254, 228, 64, 0.18);
    }

    .ascii-box-green:hover {
      border-color: #39FF14;
      box-shadow: 0 0 22px rgba(57, 255, 20, 0.18);
    }

    .ascii-box-purple:hover {
      border-color: #9B5DE5;
      box-shadow: 0 0 22px rgba(155, 93, 229, 0.2);
    }

    /* Neon Text Glows */
    .glow-cyan { text-shadow: 0 0 10px rgba(0, 245, 212, 0.55); }
    .glow-pink { text-shadow: 0 0 10px rgba(255, 42, 133, 0.55); }
    .glow-yellow { text-shadow: 0 0 10px rgba(254, 228, 64, 0.5); }
    .glow-green { text-shadow: 0 0 10px rgba(57, 255, 20, 0.55); }
    .glow-purple { text-shadow: 0 0 10px rgba(155, 93, 229, 0.55); }

    /* Custom Neon Range Sliders */
    input[type="range"] {
      -webkit-appearance: none;
      appearance: none;
      background: #1A1E30;
      height: 8px;
      border: 1px solid #2F3654;
    }
    input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 16px;
      height: 22px;
      background: #00F5D4;
      border: 2px solid #090A10;
      cursor: pointer;
      box-shadow: 0 0 12px #00F5D4;
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-track { background: #090A10; }
    ::-webkit-scrollbar-thumb { background: #2A304D; }
    ::-webkit-scrollbar-thumb:hover { background: #00F5D4; }

    @keyframes blinkCursor {
      0%, 49% { opacity: 1; }
      50%, 100% { opacity: 0; }
    }
    .cursor-blink {
      animation: blinkCursor 1s infinite;
    }
  </style>
</head>
<body class="selection:bg-[#FF2A85] selection:text-white">

  <!-- CRT Scanline Overlay -->
  <div id="crt-layer" class="crt-overlay fixed inset-0 z-50"></div>

  <!-- Matrix Rain Canvas Overlay (Activated via CLI `matrix`) -->
  <canvas id="matrix-canvas" class="fixed inset-0 z-30 pointer-events-none opacity-0 transition-opacity duration-500"></canvas>

  <!-- Toast Notification -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

  <!-- TOP ANSI STATUS BAR / NAVBAR -->
  <header class="sticky top-0 z-40 bg-[#090A10]/95 backdrop-blur-md border-b border-[#252A42]">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 h-14 flex items-center justify-between text-xs sm:text-sm">
      <a href="#hero" class="flex items-center gap-2 font-bold tracking-tight">
        <span class="text-[#FF2A85]">[</span>
        <span class="text-[#00F5D4] glow-cyan">SAYYID</span>
        <span class="text-[#FEE440]">@</span>
        <span class="text-[#9B5DE5]">DATA_OS</span>
        <span class="text-[#FF2A85]">]</span>
        <span class="hidden sm:inline text-[#39FF14] text-xs ml-1">● ONLINE</span>
      </a>

      <!-- Desktop Navigation Links -->
      <nav class="hidden md:flex items-center gap-5 text-xs font-semibold">
        <a href="#cli-section" class="text-slate-300 hover:text-[#00F5D4] transition-colors">[01:CLI_SHELL]</a>
        <a href="#analytics-ascii" class="text-slate-300 hover:text-[#FEE440] transition-colors">[02:ASCII_CHARTS]</a>
        <a href="#projects" class="text-slate-300 hover:text-[#FF2A85] transition-colors">[03:PROJECTS]</a>
        <a href="#ml-playground" class="text-slate-300 hover:text-[#39FF14] transition-colors">[04:ML_SIMULATOR]</a>
        <a href="#git-export" class="text-slate-300 hover:text-[#9B5DE5] transition-colors">[05:GIT_README]</a>
      </nav>

      <div class="flex items-center gap-2">
        <button id="crt-toggle-btn" onclick="toggleCRT()" class="px-2.5 py-1 text-[11px] font-bold border border-[#39FF14]/50 text-[#39FF14] hover:bg-[#39FF14]/15 transition">
          CRT:ON
        </button>
        <button id="mobile-menu-btn" aria-label="Menu" class="md:hidden px-2.5 py-1 border border-[#00F5D4]/50 text-[#00F5D4] text-xs font-bold">
          [MENU]
        </button>
      </div>
    </div>

    <!-- Mobile Dropdown -->
    <div id="mobile-menu" class="hidden md:hidden px-4 py-3 bg-[#0E101A] border-b border-[#252A42] space-y-2 text-xs">
      <a href="#cli-section" class="block py-1.5 text-[#00F5D4]">&gt; 01: INTERACTIVE_CLI_SHELL</a>
      <a href="#analytics-ascii" class="block py-1.5 text-[#FEE440]">&gt; 02: ASCII_ANALYTICS_CHARTS</a>
      <a href="#projects" class="block py-1.5 text-[#FF2A85]">&gt; 03: PROJECT_REPOSITORIES</a>
      <a href="#ml-playground" class="block py-1.5 text-[#39FF14]">&gt; 04: ML_CHURN_SIMULATOR</a>
      <a href="#git-export" class="block py-1.5 text-[#9B5DE5]">&gt; 05: EXPORT_GIT_README</a>
    </div>
  </header>

  <main class="relative z-10 max-w-6xl mx-auto px-4 sm:px-6 py-8 sm:py-12 space-y-16">

    <!-- HERO SECTION WITH COLORFUL ASCII BANNER & PIPELINE DIAGRAM -->
    <section id="hero" class="space-y-8">
      <!-- Top Window Frame -->
      <div class="ascii-box ascii-box-cyan p-4 sm:p-8">
        <div class="flex flex-wrap items-center justify-between gap-2 pb-4 mb-6 border-b border-[#252A42] text-xs">
          <div class="flex items-center gap-2">
            <span class="text-[#FF2A85] font-bold">■</span>
            <span class="text-[#FEE440] font-bold">■</span>
            <span class="text-[#39FF14] font-bold">■</span>
            <span class="text-slate-400 ml-2">~/portfolio/sayyid_abdul_wasye.sh — bash — 120x38</span>
          </div>
          <span class="text-[#00F5D4] font-semibold">LOC: TANGERANG, ID // 2026</span>
        </div>

        <!-- Multi-Color ASCII Art Banner -->
        <div class="overflow-x-auto pb-2">
          <pre class="text-[9px] sm:text-xs md:text-sm lg:text-[15px] leading-[1.15] font-extrabold select-all">
<span class="text-[#00F5D4] glow-cyan">███████╗ █████╗ ██╗   ██╗██╗   ██╗██╗██████╗ </span>    <span class="text-[#FF2A85] glow-pink">   ██╗██╗</span>    <span class="text-[#FEE440] glow-yellow">██████╗  █████╗ ████████╗ █████╗ </span>
<span class="text-[#00F5D4]">██╔════╝██╔══██╗╚██╗ ██╔╝╚██╗ ██╔╝██║██╔══██╗</span>    <span class="text-[#FF2A85]">  ██╔╝██╔╝</span>    <span class="text-[#FEE440]">██╔══██╗██╔══██╗╚══██╔══╝██╔══██╗</span>
<span class="text-[#39FF14] glow-green">███████╗███████║ ╚████╔╝  ╚████╔╝ ██║██║  ██║</span>    <span class="text-[#9B5DE5] glow-purple"> ██╔╝██╔╝ </span>    <span class="text-[#39FF14]">██║  ██║███████║   ██║   ███████║</span>
<span class="text-[#39FF14]">╚════██║██╔══██║  ╚██╔╝    ╚██╔╝  ██║██║  ██║</span>    <span class="text-[#9B5DE5]">██╔╝██╔╝  </span>    <span class="text-[#00F5D4]">██║  ██║██╔══██║   ██║   ██╔══██║</span>
<span class="text-[#9B5DE5] glow-purple">███████║██║  ██║   ██║      ██║   ██║██████╔╝</span>    <span class="text-[#FF2A85]">╚═╝ ╚═╝   </span>    <span class="text-[#FF2A85]">██████╔╝██║  ██║   ██║   ██║  ██║</span>
<span class="text-[#9B5DE5]">╚══════╝╚═╝  ╚═╝   ╚═╝      ╚═╝   ╚═╝╚═════╝ </span>                  <span class="text-[#FF2A85]">╚═════╝ ╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝</span></pre>
        </div>

        <!-- Role Badges -->
        <div class="mt-6 flex flex-wrap items-center gap-2.5 text-xs sm:text-sm font-bold">
          <span class="px-3 py-1 bg-[#00F5D4]/15 text-[#00F5D4] border border-[#00F5D4]/50">[DATA_ANALYST]</span>
          <span class="text-slate-500">::</span>
          <span class="px-3 py-1 bg-[#FF2A85]/15 text-[#FF2A85] border border-[#FF2A85]/50">[DATA_SCIENTIST]</span>
          <span class="text-slate-500">::</span>
          <span class="px-3 py-1 bg-[#FEE440]/15 text-[#FEE440] border border-[#FEE440]/50">[ML_ENGINEER]</span>
        </div>

        <p class="mt-5 text-slate-300 text-xs sm:text-sm leading-relaxed max-w-3xl">
          <span class="text-[#39FF14] font-bold">&gt;&gt; MISSION:</span> Mengubah jutaan baris data mentah menjadi wawasan bisnis yang tajam, dashboard analitik reaktif (<span class="text-[#00F5D4]">Marimo / Streamlit</span>), dan model <span class="text-[#FF2A85]">Machine Learning</span> berakurasi tinggi menggunakan <span class="text-[#FEE440]">Python & PostgreSQL</span>.
        </p>

        <!-- Colorful ASCII Neural Net & Data Pipeline Architecture Diagram -->
        <div class="mt-7 p-4 bg-[#07080D] border border-[#252A42] overflow-x-auto">
          <div class="text-[11px] text-slate-400 mb-2 font-bold">
            <span class="text-[#9B5DE5]">[ARCHITECTURE_FLOW]</span> End-to-End Data & ML Pipeline:
          </div>
          <pre class="text-[10px] sm:text-xs leading-snug">
<span class="text-[#00F5D4]">+-----------------+</span>      <span class="text-[#FEE440]">+-------------------+</span>      <span class="text-[#FF2A85]">+--------------------+</span>      <span class="text-[#39FF14]">+-------------------+</span>
<span class="text-[#00F5D4]">|  RAW DATA LAKE  |</span> ===&gt; <span class="text-[#FEE440]">|  EDA & SQL ENGINE |</span> ===&gt; <span class="text-[#FF2A85]">|  ML / XGBOOST CORE |</span> ===&gt; <span class="text-[#39FF14]">|  BUSINESS IMPACT  |</span>
<span class="text-[#00F5D4]">| (Logs, CSV, DB) |</span>      <span class="text-[#FEE440]">| (Pandas, CTE, IQR)|</span>      <span class="text-[#FF2A85]">| (SMOTE, SHAP, Tun) |</span>      <span class="text-[#39FF14]">| (ROC-AUC: 0.89+)  |</span>
<span class="text-[#00F5D4]">+-----------------+</span>      <span class="text-[#FEE440]">+-------------------+</span>      <span class="text-[#FF2A85]">+--------------------+</span>      <span class="text-[#39FF14]">+-------------------+</span>
        <span class="text-slate-500">|</span>                         <span class="text-slate-500">|</span>                          <span class="text-slate-500">|</span>                          <span class="text-slate-500">^</span>
        <span class="text-slate-500">+------&gt;</span> <span class="text-[#9B5DE5]">[PostgreSQL Window Functions]</span> <span class="text-slate-500">---&gt;</span> <span class="text-[#00F5D4]">[Marimo / Streamlit UI]</span> <span class="text-slate-500">--------+</span></pre>
        </div>

        <!-- CTA Action Row -->
        <div class="mt-6 flex flex-wrap gap-3 text-xs font-bold">
          <a href="#cli-section" class="px-4 py-2.5 bg-[#00F5D4] text-[#090A10] hover:bg-[#39FF14] transition shadow-lg shadow-[#00F5D4]/20">
            $ ./launch_interactive_cli.sh
          </a>
          <a href="#projects" class="px-4 py-2.5 border border-[#FF2A85] text-[#FF2A85] hover:bg-[#FF2A85]/15 transition">
            [EXPLORE_PROJECTS]
          </a>
          <button onclick="copyGitReadme()" class="px-4 py-2.5 border border-[#FEE440] text-[#FEE440] hover:bg-[#FEE440]/15 transition">
            [COPY_GIT_README_ASCII]
          </button>
        </div>
      </div>
    </section>

    <!-- 01: INTERACTIVE CLI COMMAND TERMINAL -->
    <section id="cli-section" class="space-y-4">
      <div class="flex items-center justify-between flex-wrap gap-2">
        <h2 class="text-lg sm:text-xl font-extrabold text-[#00F5D4] glow-cyan">
          +--- [01 // INTERACTIVE_CLI_TERMINAL] ---+
        </h2>
        <span class="text-xs text-slate-400">Ketik perintah atau klik chip di bawah</span>
      </div>

      <div class="ascii-box ascii-box-green p-4 sm:p-6 space-y-4">
        <!-- Quick Command Chips -->
        <div class="flex flex-wrap items-center gap-2 text-xs">
          <span class="text-slate-400 font-semibold">QUICK_CMDS:</span>
          <button onclick="runCliCommand('help')" class="px-2.5 py-1 bg-[#161929] border border-[#00F5D4]/50 text-[#00F5D4] hover:bg-[#00F5D4] hover:text-[#090A10] transition font-bold">help</button>
          <button onclick="runCliCommand('whoami')" class="px-2.5 py-1 bg-[#161929] border border-[#FF2A85]/50 text-[#FF2A85] hover:bg-[#FF2A85] hover:text-white transition font-bold">whoami</button>
          <button onclick="runCliCommand('skills')" class="px-2.5 py-1 bg-[#161929] border border-[#FEE440]/50 text-[#FEE440] hover:bg-[#FEE440] hover:text-[#090A10] transition font-bold">skills</button>
          <button onclick="runCliCommand('projects')" class="px-2.5 py-1 bg-[#161929] border border-[#9B5DE5]/50 text-[#9B5DE5] hover:bg-[#9B5DE5] hover:text-white transition font-bold">projects</button>
          <button onclick="runCliCommand('contact')" class="px-2.5 py-1 bg-[#161929] border border-[#39FF14]/50 text-[#39FF14] hover:bg-[#39FF14] hover:text-[#090A10] transition font-bold">contact</button>
          <button onclick="runCliCommand('matrix')" class="px-2.5 py-1 bg-[#161929] border border-emerald-400/50 text-emerald-300 hover:bg-emerald-400 hover:text-[#090A10] transition font-bold">matrix</button>
          <button onclick="runCliCommand('clear')" class="px-2.5 py-1 bg-[#161929] border border-slate-600 text-slate-300 hover:bg-slate-700 transition">clear</button>
        </div>

        <!-- Live Terminal Output Window -->
        <div id="cli-output" class="h-64 sm:h-72 overflow-y-auto p-4 bg-[#06070B] border border-[#22273D] text-xs sm:text-sm space-y-3 leading-relaxed">
          <div class="text-[#39FF14]">
            Welcome to Sayyid's Interactive Data & ML Shell v2.6.0 (tty1)<br />
            Type <span class="text-[#FEE440] font-bold">'help'</span> to list all available commands or click any command chip above.
          </div>
        </div>

        <!-- Command Input Form -->
        <form id="cli-form" class="flex items-center gap-2 bg-[#06070B] border border-[#00F5D4]/60 px-3 py-2.5">
          <span class="text-[#FF2A85] font-bold text-xs sm:text-sm shrink-0">guest@sayyid-ml:~$</span>
          <input
            id="cli-input"
            type="text"
            autocomplete="off"
            placeholder="ketik 'help', 'skills', 'matrix', 'contact'..."
            class="w-full bg-transparent text-[#00F5D4] placeholder-slate-600 text-xs sm:text-sm focus:outline-none"
          />
          <button type="submit" class="px-3 py-1 bg-[#00F5D4]/20 text-[#00F5D4] text-xs font-bold hover:bg-[#00F5D4] hover:text-[#090A10] transition shrink-0">
            EXEC ↵
          </button>
        </form>
      </div>
    </section>

    <!-- 02: COLORFUL ASCII ANALYTICS BAR CHARTS & SPARKLINES -->
    <section id="analytics-ascii" class="space-y-4">
      <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3">
        <h2 class="text-lg sm:text-xl font-extrabold text-[#FEE440] glow-yellow">
          +--- [02 // COLORFUL_ASCII_ANALYTICS_ENGINE] ---+
        </h2>

        <!-- Dataset Switcher Tabs -->
        <div class="flex flex-wrap gap-2 text-xs font-bold">
          <button onclick="renderAsciiChart('ecommerce', this)" class="ascii-chart-tab px-3 py-1.5 bg-[#FEE440] text-[#090A10] transition">
            [E-Commerce_Conversion]
          </button>
          <button onclick="renderAsciiChart('rfm', this)" class="ascii-chart-tab px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#00F5D4] transition">
            [RFM_Customer_Segments]
          </button>
          <button onclick="renderAsciiChart('models', this)" class="ascii-chart-tab px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#FF2A85] transition">
            [Model_Accuracy_Benchmark]
          </button>
        </div>
      </div>

      <div class="ascii-box ascii-box-yellow p-4 sm:p-6 space-y-5">
        <div class="flex flex-wrap items-center justify-between gap-2 border-b border-[#252A42] pb-3 text-xs">
          <span id="ascii-chart-title" class="text-[#00F5D4] font-bold">DATASET: E-COMMERCE SESSION DURATION VS CONVERSION RATE</span>
          <span id="ascii-sparkline" class="text-[#39FF14] font-bold">SPARKLINE: ▂▃▅▆█ [TREND: +248%]</span>
        </div>

        <!-- ASCII Bar Chart Container -->
        <div id="ascii-chart-container" class="overflow-x-auto py-2">
          <!-- Populated dynamically by JS -->
        </div>

        <!-- Analytical Takeaway Box -->
        <div class="p-3.5 bg-[#06070B] border-l-4 border-[#FF2A85] text-xs text-slate-300 leading-relaxed">
          <span class="text-[#FF2A85] font-bold">[INSIGHT_SUMMARY]:</span>
          <span id="ascii-chart-insight">Returning visitors dengan durasi sesi &gt; 3 menit mencatatkan lonjakan konversi hingga 28.7% (3.5x lebih tinggi dari pengunjung baru).</span>
        </div>
      </div>
    </section>

    <!-- 03: FILTERABLE ASCII PROJECT CARDS -->
    <section id="projects" class="space-y-5">
      <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
        <h2 class="text-lg sm:text-xl font-extrabold text-[#FF2A85] glow-pink">
          +--- [03 // FEATURED_PROJECT_REPOSITORIES] ---+
        </h2>

        <!-- Filter Buttons -->
        <div id="project-filters" class="flex flex-wrap gap-2 text-xs font-bold">
          <button data-filter="ALL" class="proj-filter-btn px-3 py-1.5 bg-[#FF2A85] text-white transition">
            [ALL]
          </button>
          <button data-filter="DATA_ANALYSIS" class="proj-filter-btn px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#00F5D4] transition">
            [DATA_ANALYSIS]
          </button>
          <button data-filter="DATA_SCIENCE" class="proj-filter-btn px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#FEE440] transition">
            [DATA_SCIENCE]
          </button>
          <button data-filter="MACHINE_LEARNING" class="proj-filter-btn px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#39FF14] transition">
            [MACHINE_LEARNING]
          </button>
        </div>
      </div>

      <!-- Projects Grid -->
      <div id="projects-grid" class="grid md:grid-cols-3 gap-5">
        <!-- Populated dynamically by JS -->
      </div>
    </section>

    <!-- 04: INTERACTIVE ASCII ML CHURN PREDICTOR PLAYGROUND -->
    <section id="ml-playground" class="space-y-4">
      <div class="flex flex-wrap items-center justify-between gap-2">
        <h2 class="text-lg sm:text-xl font-extrabold text-[#39FF14] glow-green">
          +--- [04 // INTERACTIVE_ASCII_ML_CHURN_PREDICTOR] ---+
        </h2>
        <span class="text-xs text-[#9B5DE5] font-bold">[ENGINE: XGBOOST_LOGISTIC_SIM v1.4]</span>
      </div>

      <div class="ascii-box ascii-box-green p-5 sm:p-7">
        <div class="grid lg:grid-cols-12 gap-8 items-center">
          <!-- Sliders Control Panel -->
          <div class="lg:col-span-7 space-y-6">
            <p class="text-xs text-slate-400 leading-relaxed">
              Geser parameter fitur pelanggan di bawah untuk mensimulasikan inferensi probabilitas <span class="text-[#FF2A85] font-bold">Customer Churn</span> secara real-time dalam format meteran ASCII.
            </p>

            <!-- Slider 1: Contract Tenure -->
            <div class="space-y-2">
              <div class="flex justify-between text-xs font-bold">
                <label for="slider-tenure" class="text-[#00F5D4]">01. CONTRACT_TENURE (Bulan)</label>
                <span class="text-[#FEE440]">[<span id="disp-tenure">12</span> MONTHS]</span>
              </div>
              <input id="slider-tenure" type="range" min="1" max="60" value="12" oninput="updateAsciiChurn()" class="w-full" />
              <div class="flex justify-between text-[10px] text-slate-500">
                <span>1m (New User)</span>
                <span>30m (Mid-Term)</span>
                <span>60m (Veteran)</span>
              </div>
            </div>

            <!-- Slider 2: Monthly Charges -->
            <div class="space-y-2">
              <div class="flex justify-between text-xs font-bold">
                <label for="slider-charges" class="text-[#00F5D4]">02. MONTHLY_CHARGES (IDR)</label>
                <span class="text-[#FEE440]">[Rp <span id="disp-charges">550</span>.000/bln]</span>
              </div>
              <input id="slider-charges" type="range" min="100" max="1200" step="25" value="550" oninput="updateAsciiChurn()" class="w-full" />
              <div class="flex justify-between text-[10px] text-slate-500">
                <span>Rp 100rb (Basic)</span>
                <span>Rp 650rb (Pro)</span>
                <span>Rp 1.2jt (Enterprise)</span>
              </div>
            </div>

            <!-- Slider 3: Support Tickets -->
            <div class="space-y-2">
              <div class="flex justify-between text-xs font-bold">
                <label for="slider-tickets" class="text-[#00F5D4]">03. SUPPORT_TICKETS (30 Hari Terakhir)</label>
                <span class="text-[#FEE440]">[<span id="disp-tickets">3</span> TICKETS]</span>
              </div>
              <input id="slider-tickets" type="range" min="0" max="8" value="3" oninput="updateAsciiChurn()" class="w-full" />
              <div class="flex justify-between text-[10px] text-slate-500">
                <span>0 (Zero Issue)</span>
                <span>4 (Warning)</span>
                <span>8 (Critical Friction)</span>
              </div>
            </div>
          </div>

          <!-- ASCII Gauge & Verdict Output -->
          <div class="lg:col-span-5">
            <div id="churn-ascii-panel" class="p-5 bg-[#06070B] border-2 border-[#FEE440] space-y-4">
              <div class="text-xs text-slate-400 font-bold border-b border-[#252A42] pb-2 flex justify-between">
                <span>&gt; INFERENCE_OUTPUT</span>
                <span class="text-[#00F5D4]">SHAP_ACTIVE</span>
              </div>

              <!-- Dynamic ASCII Progress Bar Gauge -->
              <div class="space-y-1.5">
                <div class="text-[11px] text-slate-400">CHURN_PROBABILITY_GAUGE:</div>
                <div id="ascii-gauge-bar" class="text-xs sm:text-sm font-extrabold tracking-tight text-[#FEE440] break-all">
                  [██████████░░░░░░░░░░] 52.4%
                </div>
              </div>

              <!-- Risk Verdict Status -->
              <div class="py-2">
                <div class="text-[11px] text-slate-400 mb-1">CLASSIFICATION_VERDICT:</div>
                <div id="churn-verdict-badge" class="inline-block px-3 py-1 text-xs sm:text-sm font-extrabold bg-[#FEE440]/20 text-[#FEE440] border border-[#FEE440]">
                  [!] MODERATE_RISK
                </div>
              </div>

              <!-- Actionable Recommendation -->
              <div class="text-xs text-slate-300 leading-relaxed pt-2 border-t border-[#252A42]">
                <span class="text-[#00F5D4] font-bold">ACTION_PLAN:</span>
                <span id="churn-action-text">Kirimkan survei kepuasan otomatis dan tawarkan insentif perpanjangan paket 3 bulan.</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 05: ONE-CLICK GITHUB README ASCII GENERATOR & CONTACT -->
    <section id="git-export" class="grid lg:grid-cols-12 gap-6">
      <!-- GitHub README ASCII Preview & Copy -->
      <div class="lg:col-span-7 ascii-box ascii-box-purple p-5 sm:p-6 space-y-4">
        <div class="flex flex-wrap items-center justify-between gap-2">
          <h2 class="text-base sm:text-lg font-extrabold text-[#9B5DE5] glow-purple">
            +--- [05 // GITHUB_README_ASCII_TEMPLATE] ---+
          </h2>
          <button onclick="copyGitReadme()" class="px-3.5 py-1.5 bg-[#9B5DE5] text-white text-xs font-bold hover:bg-[#FF2A85] transition shadow-md">
            [COPY_GIT_README_ASCII]
          </button>
        </div>

        <p class="text-xs text-slate-400">
          Klik tombol di atas untuk menyalin template <code class="text-[#00F5D4]">README.md</code> bergaya ASCII + ANSI Badges siap tempel ke profil GitHub Anda.
        </p>

        <pre id="git-readme-preview" class="p-4 bg-[#06070B] border border-[#252A42] text-[11px] text-[#00F5D4] overflow-x-auto leading-relaxed max-h-60">
```text
+-----------------------------------------------------------------------+
|  SAYYID ABDUL WASYE // DATA ANALYST | DATA SCIENTIST | ML ENGINEER    |
+-----------------------------------------------------------------------+
|  [STACK]  Python • PostgreSQL • Scikit-Learn • XGBoost • Marimo       |
|  [IMPACT] ROC-AUC 0.89 Churn Model | +3.5x E-Commerce Conversion      |
|  [CERT]   BNSP Certified Data & IT Practitioner (2026)                |
+-----------------------------------------------------------------------+
```</pre>
      </div>

      <!-- Direct Contact & Credentials Box -->
      <div class="lg:col-span-5 ascii-box ascii-box-cyan p-5 sm:p-6 flex flex-col justify-between space-y-5">
        <div class="space-y-3">
          <h2 class="text-base sm:text-lg font-extrabold text-[#00F5D4] glow-cyan">
            +--- [CONNECT & CREDENTIALS] ---+
          </h2>
          <div class="p-3 bg-[#06070B] border border-[#252A42] text-xs space-y-1">
            <div class="text-[#39FF14] font-bold">✓ BNSP_CERTIFIED_DATA_PRACTITIONER (2026)</div>
            <div class="text-slate-400">Badan Nasional Sertifikasi Profesi — Indonesia</div>
          </div>
          <p class="text-xs text-slate-300 leading-relaxed">
            Siap berkolaborasi untuk peran <span class="text-[#00F5D4]">Data Analyst</span>, <span class="text-[#FF2A85]">Data Scientist</span>, atau <span class="text-[#FEE440]">ML Engineer</span>.
          </p>
        </div>

        <div class="space-y-3 text-xs">
          <div class="flex items-center justify-between gap-2 p-3 bg-[#06070B] border border-[#00F5D4]/40">
            <span id="email-addr" class="text-[#00F5D4] truncate">sayyid.wasye@data-portfolio.id</span>
            <button onclick="copyEmailAddress()" class="px-2.5 py-1 bg-[#00F5D4] text-[#090A10] font-bold shrink-0 hover:bg-[#39FF14] transition">
              COPY
            </button>
          </div>

          <div class="grid grid-cols-3 gap-2 font-bold text-center">
            <a href="https://github.com" target="_blank" rel="noopener noreferrer" class="py-2 border border-slate-700 hover:border-[#00F5D4] text-slate-200 hover:text-[#00F5D4] transition">
              [GITHUB]
            </a>
            <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="py-2 border border-slate-700 hover:border-[#FF2A85] text-slate-200 hover:text-[#FF2A85] transition">
              [LINKEDIN]
            </a>
            <a href="https://kaggle.com" target="_blank" rel="noopener noreferrer" class="py-2 border border-slate-700 hover:border-[#FEE440] text-slate-200 hover:text-[#FEE440] transition">
              [KAGGLE]
            </a>
          </div>
        </div>
      </div>
    </section>

  </main>

  <!-- FOOTER -->
  <footer class="border-t border-[#252A42] py-6 px-4 text-center text-xs text-slate-500">
    <p>EOF // © 2026 SAYYID ABDUL WASYE — BUILT IN PURE ANSI TERMINAL & ASCII AESTHETIC.</p>
  </footer>

  <!-- ASCII CASE STUDY MODAL -->
  <div id="case-modal" class="fixed inset-0 z-50 hidden items-center justify-center p-4 bg-black/85 backdrop-blur-sm">
    <div class="ascii-box border-2 border-[#00F5D4] max-w-2xl w-full max-h-[90vh] overflow-y-auto p-5 sm:p-7 space-y-5 shadow-2xl">
      <div class="flex items-center justify-between border-b border-[#252A42] pb-3">
        <span id="modal-cat-tag" class="text-xs font-extrabold text-[#FF2A85]">[CATEGORY]</span>
        <button onclick="closeCaseModal()" class="px-2.5 py-1 bg-[#FF2A85] text-white text-xs font-bold hover:opacity-85">
          [ESC / CLOSE X]
        </button>
      </div>

      <h3 id="modal-proj-title" class="text-lg sm:text-xl font-extrabold text-[#00F5D4]">Project Title</h3>

      <div id="modal-tech-list" class="flex flex-wrap gap-2 text-xs"></div>

      <div class="space-y-4 text-xs leading-relaxed">
        <div class="p-3.5 bg-[#06070B] border border-[#FF2A85]/40">
          <div class="text-[#FF2A85] font-bold mb-1">+-- [01. BUSINESS_PROBLEM] --+</div>
          <p id="modal-prob-text" class="text-slate-300"></p>
        </div>

        <div class="p-3.5 bg-[#06070B] border border-[#FEE440]/40">
          <div class="text-[#FEE440] font-bold mb-1">+-- [02. TECHNICAL_EXECUTION] --+</div>
          <ul id="modal-exec-list" class="space-y-1.5 text-slate-300"></ul>
        </div>

        <div class="p-3.5 bg-[#06070B] border border-[#39FF14]/50">
          <div class="text-[#39FF14] font-bold mb-1">+-- [03. MEASURED_IMPACT] --+</div>
          <p id="modal-imp-text" class="text-[#39FF14] font-semibold"></p>
        </div>
      </div>

      <div class="flex flex-wrap gap-3 pt-2 text-xs font-bold">
        <a href="https://github.com" target="_blank" rel="noopener noreferrer" class="flex-1 text-center py-2.5 border border-[#00F5D4] text-[#00F5D4] hover:bg-[#00F5D4] hover:text-[#090A10] transition">
          [OPEN_GITHUB_REPO ↗]
        </a>
        <button onclick="jumpToPlaygroundFromModal()" class="flex-1 text-center py-2.5 bg-[#39FF14] text-[#090A10] hover:opacity-90 transition">
          [TEST_IN_PLAYGROUND &gt;&gt;]
        </button>
      </div>
    </div>
  </div>

  <!-- INTERACTIVE JAVASCRIPT -->
  <script>
    // ==========================================
    // 1. PROJECT DATA & FILTERABLE ASCII CARDS
    // ==========================================
    const projectsData = [
      {
        id: 1,
        category: "DATA_ANALYSIS",
        colorClass: "ascii-box-cyan",
        badgeColor: "text-[#00F5D4] border-[#00F5D4]",
        title: "E-Commerce Visitor Behavior & Conversion Funnel",
        metric: "CONVERSION: +3.5x",
        summary: "Analisis komparatif pengunjung baru vs berulang dengan deteksi outlier IQR & dashboard Marimo.",
        tags: ["Python", "Pandas", "NumPy", "Marimo", "IQR"],
        problem: "Tingginya trafik pengunjung situs e-commerce belum berbanding lurus dengan rasio penyelesaian transaksi (revenue).",
        execution: [
          "> Pembersihan anomali durasi sesi & deteksi outlier menggunakan metode Interquartile Range (IQR).",
          "> Komparasi statistik bounce rate & halaman produk antara Returning vs New Visitor.",
          "> Pembuatan dashboard reaktif berbasis Marimo untuk pemfilteran kanal secara real-time."
        ],
        impact: "Returning visitor dengan durasi sesi > 3 menit mencatatkan konversi 28.7% (3.5x lebih tinggi), mendorong kampanye retargeting terarah.",
        targetSection: "analytics-ascii"
      },
      {
        id: 2,
        category: "DATA_SCIENCE",
        colorClass: "ascii-box-yellow",
        badgeColor: "text-[#FEE440] border-[#FEE440]",
        title: "RFM Customer Segmentation & K-Means Clustering",
        metric: "CLUSTERS: 4 PERSONAS",
        summary: "Segmentasi pelanggan berbasis kueri PostgreSQL Window Functions dan algoritma K-Means.",
        tags: ["PostgreSQL", "Scikit-Learn", "K-Means", "RFM"],
        problem: "Kampanye promosi massal menyebabkan biaya diskon membengkak dengan tingkat retensi pelanggan yang rendah.",
        execution: [
          "> Ekstraksi jutaan baris transaksi historis menggunakan CTE & Window Functions di PostgreSQL.",
          "> Kalkulasi skor Recency, Frequency, Monetary (RFM) dan standardisasi fitur.",
          "> Penentuan k-optimal via Elbow Method & Silhouette Score pada K-Means Clustering."
        ],
        impact: "Berhasil memetakan basis pelanggan ke dalam 4 segmen utama (Champions, Loyal, At-Risk, Hibernating) untuk efisiensi anggaran promo.",
        targetSection: "analytics-ascii"
      },
      {
        id: 3,
        category: "MACHINE_LEARNING",
        colorClass: "ascii-box-green",
        badgeColor: "text-[#39FF14] border-[#39FF14]",
        title: "End-to-End Customer Churn Prediction (XGBoost)",
        metric: "ROC-AUC: 0.89 | REC: 84%",
        summary: "Model klasifikasi deteksi dini pelanggan berhenti berlangganan dilengkapi explainability SHAP.",
        tags: ["XGBoost", "SMOTE", "SHAP", "Streamlit"],
        problem: "Kehilangan recurring revenue akibat pelanggan membatalkan langganan tanpa sistem peringatan dini.",
        execution: [
          "> Penanganan dataset tidak seimbang (imbalanced class) menggunakan oversampling SMOTE.",
          "> Komparasi performa Logistic Regression, Random Forest, dan XGBoost Tuned.",
          "> Implementasi SHAP Values untuk menjelaskan faktor pendorong churn tiap pelanggan."
        ],
        impact: "Mencapai skor ROC-AUC 0.89 dan Recall 84%, memungkinkan tim retensi melakukan intervensi proaktif H-14 sebelum churn.",
        targetSection: "ml-playground"
      }
    ];

    function renderProjects(filter = "ALL") {
      const grid = document.getElementById("projects-grid");
      grid.innerHTML = "";

      const list = filter === "ALL" ? projectsData : projectsData.filter(p => p.category === filter);

      list.forEach(proj => {
        const card = document.createElement("div");
        card.className = `ascii-box ${proj.colorClass} p-5 flex flex-col justify-between space-y-4`;

        card.innerHTML = `
          <div class="space-y-3">
            <div class="flex items-center justify-between gap-2 text-[11px] font-bold">
              <span class="px-2 py-0.5 border ${proj.badgeColor}">[${proj.category}]</span>
              <span class="text-[#FF2A85]">${proj.metric}</span>
            </div>

            <div class="text-slate-600 text-xs select-none">+-----------------------------------+</div>

            <h3 class="text-sm sm:text-base font-extrabold text-white leading-snug">
              ${proj.title}
            </h3>

            <p class="text-xs text-slate-400 leading-relaxed">
              ${proj.summary}
            </p>
          </div>

          <div class="space-y-4 pt-2">
            <div class="flex flex-wrap gap-1.5 text-[11px]">
              ${proj.tags.map(t => `<span class="px-2 py-0.5 bg-[#06070B] border border-[#252A42] text-[#00F5D4]">#${t}</span>`).join("")}
            </div>

            <button onclick="openCaseModal(${proj.id})" class="w-full py-2.5 bg-[#151829] hover:bg-[#00F5D4] text-[#00F5D4] hover:text-[#090A10] border border-[#00F5D4]/60 text-xs font-extrabold transition">
              [INSPECT_CASE_STUDY &gt;&gt;]
            </button>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    document.querySelectorAll(".proj-filter-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        document.querySelectorAll(".proj-filter-btn").forEach(b => {
          b.className = "proj-filter-btn px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#00F5D4] transition";
        });
        btn.className = "proj-filter-btn px-3 py-1.5 bg-[#FF2A85] text-white transition";
        renderProjects(btn.dataset.filter);
      });
    });

    // Modal Case Study Handlers
    let currentModalTarget = "ml-playground";

    function openCaseModal(id) {
      const p = projectsData.find(item => item.id === id);
      if (!p) return;
      currentModalTarget = p.targetSection;

      document.getElementById("modal-cat-tag").textContent = `[${p.category}] // ${p.metric}`;
      document.getElementById("modal-proj-title").textContent = p.title;
      document.getElementById("modal-prob-text").textContent = p.problem;
      document.getElementById("modal-imp-text").textContent = p.impact;

      document.getElementById("modal-tech-list").innerHTML = p.tags
        .map(t => `<span class="px-2.5 py-0.5 bg-[#06070B] border border-[#9B5DE5] text-[#9B5DE5]">${t}</span>`)
        .join("");

      document.getElementById("modal-exec-list").innerHTML = p.execution
        .map(step => `<li>${step}</li>`)
        .join("");

      const modal = document.getElementById("case-modal");
      modal.classList.remove("hidden");
      modal.classList.add("flex");
    }

    function closeCaseModal() {
      const modal = document.getElementById("case-modal");
      modal.classList.add("hidden");
      modal.classList.remove("flex");
    }

    function jumpToPlaygroundFromModal() {
      closeCaseModal();
      document.getElementById(currentModalTarget).scrollIntoView({ behavior: "smooth" });
    }

    document.getElementById("case-modal").addEventListener("click", (e) => {
      if (e.target.id === "case-modal") closeCaseModal();
    });

    // ==========================================
    // 2. COLORFUL ASCII BAR CHARTS ENGINE
    // ==========================================
    const asciiDatasets = {
      ecommerce: {
        title: "DATASET: E-COMMERCE SESSION DURATION VS CONVERSION RATE",
        sparkline: "SPARKLINE: ▂▃▅▆█ [PEAK: 28.7%]",
        insight: "Returning visitors dengan durasi sesi > 3 menit mencatatkan lonjakan konversi hingga 28.7% (3.5x lebih tinggi dari pengunjung baru).",
        bars: [
          { label: "< 1 Min (New)   ", val: 3.2, max: 35, color: "text-[#9B5DE5]" },
          { label: "1-3 Min (New)   ", val: 6.8, max: 35, color: "text-[#00F5D4]" },
          { label: "1-3 Min (Return)", val: 14.5, max: 35, color: "text-[#FEE440]" },
          { label: "3-5 Min (Return)", val: 22.4, max: 35, color: "text-[#FF2A85]" },
          { label: "> 5 Min (Return)", val: 28.7, max: 35, color: "text-[#39FF14]" }
        ]
      },
      rfm: {
        title: "DATASET: RFM CUSTOMER SEGMENTATION DISTRIBUTION (N = 12,450)",
        sparkline: "SPARKLINE: █▆▄▂ [CHAMPIONS: 34.2%]",
        insight: "Segmen Champions (34.2%) dan Loyal (28.5%) menyumbang 74% total GMV tahunan; segmen At-Risk (21.8%) menjadi target utama retensi.",
        bars: [
          { label: "Champions       ", val: 34.2, max: 40, color: "text-[#39FF14]" },
          { label: "Loyal Customers ", val: 28.5, max: 40, color: "text-[#00F5D4]" },
          { label: "At-Risk Users   ", val: 21.8, max: 40, color: "text-[#FEE440]" },
          { label: "Hibernating     ", val: 15.5, max: 40, color: "text-[#FF2A85]" }
        ]
      },
      models: {
        title: "DATASET: CHURN PREDICTION MODEL BENCHMARK (ROC-AUC SCORE)",
        sparkline: "SPARKLINE: ▅▆▇█ [BEST: XGBOOST 89.0%]",
        insight: "XGBoost dengan SMOTE oversampling mengungguli baseline Logistic Regression (+11.5% ROC-AUC) serta menekan False Negatives.",
        bars: [
          { label: "Dummy Baseline  ", val: 50.0, max: 100, color: "text-slate-500" },
          { label: "Logistic Reg    ", val: 77.5, max: 100, color: "text-[#9B5DE5]" },
          { label: "Random Forest   ", val: 84.2, max: 100, color: "text-[#00F5D4]" },
          { label: "LightGBM Tuned  ", val: 87.6, max: 100, color: "text-[#FEE440]" },
          { label: "XGBoost + SMOTE ", val: 89.0, max: 100, color: "text-[#39FF14]" }
        ]
      }
    };

    function renderAsciiChart(key, btnEl = null) {
      const ds = asciiDatasets[key];
      if (!ds) return;

      if (btnEl) {
        document.querySelectorAll(".ascii-chart-tab").forEach(b => {
          b.className = "ascii-chart-tab px-3 py-1.5 bg-[#141726] text-slate-300 border border-[#2A304D] hover:border-[#00F5D4] transition";
        });
        btnEl.className = "ascii-chart-tab px-3 py-1.5 bg-[#FEE440] text-[#090A10] transition";
      }

      document.getElementById("ascii-chart-title").textContent = ds.title;
      document.getElementById("ascii-sparkline").textContent = ds.sparkline;
      document.getElementById("ascii-chart-insight").textContent = ds.insight;

      const container = document.getElementById("ascii-chart-container");
      const totalBlocks = 28;

      let rowsHtml = `<div class="space-y-2.5 font-mono text-xs sm:text-sm min-w-[540px]">`;
      ds.bars.forEach(item => {
        const filledCount = Math.round((item.val / item.max) * totalBlocks);
        const emptyCount = Math.max(0, totalBlocks - filledCount);
        const filledStr = "█".repeat(filledCount);
        const emptyStr = "░".repeat(emptyCount);

        rowsHtml += `
          <div class="flex items-center gap-3">
            <span class="text-slate-300 font-bold whitespace-pre">${item.label}</span>
            <span class="text-slate-600">|</span>
            <span class="${item.color} font-extrabold tracking-tighter">${filledStr}<span class="text-slate-700">${emptyStr}</span></span>
            <span class="${item.color} font-bold ml-1">${item.val.toFixed(1)}%</span>
          </div>
        `;
      });
      rowsHtml += `</div>`;
      container.innerHTML = rowsHtml;
    }

    // ==========================================
    // 3. INTERACTIVE ASCII ML CHURN SIMULATOR
    // ==========================================
    function updateAsciiChurn() {
      const tenure = parseFloat(document.getElementById("slider-tenure").value);
      const charges = parseFloat(document.getElementById("slider-charges").value);
      const tickets = parseFloat(document.getElementById("slider-tickets").value);

      document.getElementById("disp-tenure").textContent = tenure;
      document.getElementById("disp-charges").textContent = charges;
      document.getElementById("disp-tickets").textContent = tickets;

      // Logistic Regression / XGBoost-inspired probability scoring
      const z = -1.1 - (0.045 * tenure) + (0.0014 * charges) + (0.48 * tickets);
      const prob = 1 / (1 + Math.exp(-z));
      const pct = (prob * 100).toFixed(1);

      // Build 20-block ASCII Gauge
      const totalSlots = 20;
      const filledSlots = Math.round(prob * totalSlots);
      const emptySlots = totalSlots - filledSlots;
      const gaugeText = `[${"█".repeat(filledSlots)}${"░".repeat(emptySlots)}] ${pct}%`;

      const gaugeEl = document.getElementById("ascii-gauge-bar");
      const badgeEl = document.getElementById("churn-verdict-badge");
      const actionEl = document.getElementById("churn-action-text");
      const panelEl = document.getElementById("churn-ascii-panel");

      gaugeEl.textContent = gaugeText;

      if (prob < 0.35) {
        gaugeEl.className = "text-xs sm:text-sm font-extrabold tracking-tight text-[#39FF14] glow-green break-all";
        badgeEl.className = "inline-block px-3 py-1 text-xs sm:text-sm font-extrabold bg-[#39FF14]/20 text-[#39FF14] border border-[#39FF14]";
        badgeEl.textContent = "[OK] LOW_RISK";
        panelEl.className = "p-5 bg-[#06070B] border-2 border-[#39FF14] space-y-4 transition-colors";
        actionEl.textContent = "Pelanggan sangat loyal. Pertahankan SLA layanan dan tawarkan program referral berhadiah.";
      } else if (prob < 0.68) {
        gaugeEl.className = "text-xs sm:text-sm font-extrabold tracking-tight text-[#FEE440] glow-yellow break-all";
        badgeEl.className = "inline-block px-3 py-1 text-xs sm:text-sm font-extrabold bg-[#FEE440]/20 text-[#FEE440] border border-[#FEE440]";
        badgeEl.textContent = "[!] MODERATE_RISK";
        panelEl.className = "p-5 bg-[#06070B] border-2 border-[#FEE440] space-y-4 transition-colors";
        actionEl.textContent = "Kirimkan survei kepuasan otomatis dan tawarkan insentif perpanjangan paket 3 bulan.";
      } else {
        gaugeEl.className = "text-xs sm:text-sm font-extrabold tracking-tight text-[#FF2A85] glow-pink break-all";
        badgeEl.className = "inline-block px-3 py-1 text-xs sm:text-sm font-extrabold bg-[#FF2A85]/20 text-[#FF2A85] border border-[#FF2A85]";
        badgeEl.textContent = "[CRITICAL] CRITICAL_CHURN";
        panelEl.className = "p-5 bg-[#06070B] border-2 border-[#FF2A85] space-y-4 transition-colors";
        actionEl.textContent = "PRIORITAS TINGGI: Eskalasi tiket keluhan ke Account Manager dalam < 24 jam & berikan kompensasi retensi.";
      }
    }

    // ==========================================
    // 4. INTERACTIVE CLI COMMAND PROMPT
    // ==========================================
    const cliResponses = {
      help: `
        <div class="text-[#00F5D4] font-bold">AVAILABLE COMMANDS:</div>
        <div class="grid sm:grid-cols-2 gap-1 text-xs mt-1">
          <div><span class="text-[#FEE440] font-bold">whoami</span>   - Profil & spesialisasi Sayyid Abdul Wasye</div>
          <div><span class="text-[#FEE440] font-bold">skills</span>   - Daftar Tech Stack Data & Machine Learning</div>
          <div><span class="text-[#FEE440] font-bold">projects</span> - Ringkasan 3 studi kasus unggulan</div>
          <div><span class="text-[#FEE440] font-bold">contact</span>  - Email, GitHub, LinkedIn & Kaggle</div>
          <div><span class="text-[#FEE440] font-bold">matrix</span>   - Toggle efek hujan kode Matrix ANSI</div>
          <div><span class="text-[#FEE440] font-bold">clear</span>    - Bersihkan layar terminal</div>
        </div>
      `,
      whoami: `
        <div class="text-[#FF2A85] font-bold">+-- [USER_IDENTITY: SAYYID ABDUL WASYE] --+</div>
        <div class="text-slate-300 mt-1">
          Role     : <span class="text-[#00F5D4]">Data Analyst | Data Scientist | ML Engineer</span><br/>
          Location : Tangerang, Banten, Indonesia<br/>
          Cert     : <span class="text-[#39FF14]">BNSP Certified Data & IT Practitioner (2026)</span><br/>
          Focus    : Mengubah data mentah menjadi sistem keputusan prediktif & dashboard interaktif.
        </div>
      `,
      skills: `
        <div class="text-[#FEE440] font-bold">+-- [TECH_STACK_INVENTORY] --+</div>
        <div class="text-xs space-y-1 mt-1">
          <div><span class="text-[#00F5D4]">[LANGUAGES]</span> : Python (Pandas, NumPy, SciPy), SQL (PostgreSQL, MySQL)</div>
          <div><span class="text-[#FF2A85]">[ML_CORE]</span>   : Scikit-Learn, XGBoost, LightGBM, SMOTE, SHAP Values</div>
          <div><span class="text-[#39FF14]">[VIZ_APPS]</span>  : Marimo Reactive Notebooks, Streamlit, Matplotlib, Seaborn</div>
          <div><span class="text-[#9B5DE5]">[DEVOPS]</span>    : Docker, Git/GitHub, Linux Bash, Excel Automation (openpyxl)</div>
        </div>
      `,
      projects: `
        <div class="text-[#9B5DE5] font-bold">+-- [LOADED_REPOSITORIES] --+</div>
        <div class="text-xs space-y-1.5 mt-1">
          <div><span class="text-[#00F5D4] font-bold">[01] E-Commerce Conversion Funnel</span> -> +3.5x conversion lift via Marimo & IQR</div>
          <div><span class="text-[#FEE440] font-bold">[02] RFM Customer Segmentation</span>    -> 4 customer personas via PostgreSQL & K-Means</div>
          <div><span class="text-[#39FF14] font-bold">[03] Customer Churn Prediction</span>    -> ROC-AUC 0.89 & Recall 84% via XGBoost + SHAP</div>
        </div>
      `,
      contact: `
        <div class="text-[#39FF14] font-bold">+-- [COMMUNICATION_CHANNELS] --+</div>
        <div class="text-xs space-y-1 mt-1">
          <div>Email    : <span class="text-[#00F5D4]">sayyid.wasye@data-portfolio.id</span></div>
          <div>GitHub   : <span class="text-[#FF2A85]">github.com/sayyid-wasye</span></div>
          <div>LinkedIn : <span class="text-[#FEE440]">linkedin.com/in/sayyid-abdul-wasye</span></div>
          <div>Kaggle   : <span class="text-[#9B5DE5]">kaggle.com/sayyidwasye</span></div>
        </div>
      `
    };

    function runCliCommand(rawCmd) {
      const cmd = rawCmd.trim().toLowerCase();
      const output = document.getElementById("cli-output");
      if (!cmd) return;

      if (cmd === "clear") {
        output.innerHTML = `<div class="text-slate-500">Terminal cleared. Type <span class="text-[#FEE440]">'help'</span> for commands.</div>`;
        return;
      }

      const cmdEcho = document.createElement("div");
      cmdEcho.innerHTML = `<span class="text-[#FF2A85] font-bold">guest@sayyid-ml:~$</span> <span class="text-white font-bold">${escapeHtml(rawCmd)}</span>`;
      output.appendChild(cmdEcho);

      const responseDiv = document.createElement("div");
      if (cmd === "matrix") {
        const isActive = toggleMatrixRain();
        responseDiv.innerHTML = `<span class="text-[#39FF14]">[SYSTEM] Matrix ANSI Rain ${isActive ? "ENABLED (klik 'matrix' lagi untuk mematikan)" : "DISABLED"}.</span>`;
      } else if (cliResponses[cmd]) {
        responseDiv.innerHTML = cliResponses[cmd];
      } else {
        responseDiv.innerHTML = `<span class="text-[#FF2A85]">Command not found: '${escapeHtml(cmd)}'. Ketik <span class="text-[#FEE440]">'help'</span> untuk melihat daftar perintah.</span>`;
      }

      output.appendChild(responseDiv);
      output.scrollTop = output.scrollHeight;
    }

    document.getElementById("cli-form").addEventListener("submit", (e) => {
      e.preventDefault();
      const input = document.getElementById("cli-input");
      runCliCommand(input.value);
      input.value = "";
    });

    function escapeHtml(str) {
      return str.replace(/[&<>"']/g, m => ({
        '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
      })[m]);
    }

    // ==========================================
    // 5. MATRIX RAIN EASTER EGG & CRT TOGGLE
    // ==========================================
    let matrixActive = false;
    let matrixInterval = null;

    function toggleMatrixRain() {
      const canvas = document.getElementById("matrix-canvas");
      matrixActive = !matrixActive;

      if (matrixActive) {
        canvas.classList.remove("opacity-0");
        canvas.classList.add("opacity-25");
        startMatrixAnimation(canvas);
      } else {
        canvas.classList.remove("opacity-25");
        canvas.classList.add("opacity-0");
        clearInterval(matrixInterval);
      }
      return matrixActive;
    }

    function startMatrixAnimation(canvas) {
      const ctx = canvas.getContext("2d");
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const chars = "01アイウエオカキクケコDATA_ML_SQL_PYTHON_XGBOOST_#%*+";
      const fontSize = 14;
      const columns = Math.floor(canvas.width / fontSize);
      const drops = Array(columns).fill(1);
      const colors = ["#00F5D4", "#39FF14", "#FF2A85", "#FEE440", "#9B5DE5"];

      clearInterval(matrixInterval);
      matrixInterval = setInterval(() => {
        ctx.fillStyle = "rgba(9, 10, 16, 0.12)";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.font = fontSize + "px JetBrains Mono";

        for (let i = 0; i < drops.length; i++) {
          const text = chars[Math.floor(Math.random() * chars.length)];
          ctx.fillStyle = colors[i % colors.length];
          ctx.fillText(text, i * fontSize, drops[i] * fontSize);

          if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
            drops[i] = 0;
          }
          drops[i]++;
        }
      }, 45);
    }

    let crtOn = true;
    function toggleCRT() {
      crtOn = !crtOn;
      const layer = document.getElementById("crt-layer");
      const btn = document.getElementById("crt-toggle-btn");
      if (crtOn) {
        layer.classList.remove("hidden");
        btn.textContent = "CRT:ON";
      } else {
        layer.classList.add("hidden");
        btn.textContent = "CRT:OFF";
      }
    }

    // ==========================================
    // 6. COPY GIT README ASCII & CLIPBOARD UTILS
    // ==========================================
    function copyToClipboardFallback(text, successMsg) {
      const textarea = document.createElement("textarea");
      textarea.value = text;
      textarea.style.position = "fixed";
      textarea.style.opacity = "0";
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand("copy");
      document.body.removeChild(textarea);
      showToast(successMsg);
    }

    function copyGitReadme() {
      const asciiReadme = `<div align="center">

\`\`\`text
+-------------------------------------------------------------------------+
|   ███████╗ █████╗ ██╗   ██╗██╗   ██╗██╗██████╗     ██████╗  █████╗ ████████╗ █████╗  |
|   ██╔════╝██╔══██╗╚██╗ ██╔╝╚██╗ ██╔╝██║██╔══██╗    ██╔══██╗██╔══██╗╚══██╔══╝██╔══██╗ |
|   ███████╗███████║ ╚████╔╝  ╚████╔╝ ██║██║  ██║    ██║  ██║███████║   ██║   ███████║ |
|   ╚════██║██╔══██║  ╚██╔╝    ╚██╔╝  ██║██║  ██║    ██║  ██║██╔══██║   ██║   ██╔══██║ |
|   ███████║██║  ██║   ██║      ██║   ██║██████╔╝    ██████╔╝██║  ██║   ██║   ██║  ██║ |
|   ╚══════╝╚═╝  ╚═╝   ╚═╝      ╚═╝   ╚═╝╚═════╝     ╚═════╝ ╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝ |
+-------------------------------------------------------------------------+
|   SAYYID ABDUL WASYE  //  DATA ANALYST | DATA SCIENTIST | ML ENGINEER   |
+-------------------------------------------------------------------------+
\`\`\`

![Python](https://img.shields.io/badge/Python-00F5D4?style=for-the-badge&logo=python&logoColor=090A10)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-FF2A85?style=for-the-badge&logo=postgresql&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-FEE440?style=for-the-badge&logoColor=090A10)
![Marimo](https://img.shields.io/badge/Marimo-39FF14?style=for-the-badge&logoColor=090A10)
![Streamlit](https://img.shields.io/badge/Streamlit-9B5DE5?style=for-the-badge&logo=streamlit&logoColor=white)

</div>

\`\`\`text
+--- [FEATURED_DATA_&_ML_PROJECTS] ---------------------------------------+
| [01] E-Commerce Conversion Funnel  => +3.5x Conversion (Python/Marimo)  |
| [02] RFM Customer Segmentation     => 4 Personas (PostgreSQL/K-Means)   |
| [03] Customer Churn Prediction     => ROC-AUC 0.89 (XGBoost/SMOTE/SHAP) |
+-------------------------------------------------------------------------+
\`\`\``;

      copyToClipboardFallback(asciiReadme, "[COPIED] Template GitHub README ASCII berhasil disalin ke clipboard!");
    }

    function copyEmailAddress() {
      const email = document.getElementById("email-addr").textContent;
      copyToClipboardFallback(email, `[COPIED] ${email} disalin ke clipboard!`);
    }

    function showToast(msg) {
      const container = document.getElementById("toast-container");
      const toast = document.createElement("div");
      toast.className = "px-4 py-3 bg-[#0E101A] border-2 border-[#39FF14] text-[#39FF14] text-xs font-bold shadow-2xl";
      toast.textContent = msg;
      container.appendChild(toast);
      setTimeout(() => toast.remove(), 3200);
    }

    // Mobile Menu Toggle
    document.getElementById("mobile-menu-btn").addEventListener("click", () => {
      document.getElementById("mobile-menu").classList.toggle("hidden");
    });

    document.querySelectorAll("#mobile-menu a").forEach(link => {
      link.addEventListener("click", () => {
        document.getElementById("mobile-menu").classList.add("hidden");
      });
    });

    // Initialize All Components on Load
    window.addEventListener("DOMContentLoaded", () => {
      renderAsciiChart("ecommerce");
      renderProjects("ALL");
      updateAsciiChurn();
    });
  </script>
</body>
</html>
