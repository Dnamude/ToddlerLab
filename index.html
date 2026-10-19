<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Toddler Learning Hub</title>
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Toddler Hub">
    <meta name="theme-color" content="#e0f2fe">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🌟</text></svg>">
    <link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🌟</text></svg>">

        <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@500;600;700&family=Nunito:wght@700;800;900&family=Plus+Jakarta+Sans:wght@700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js" defer></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@500;600;700&family=Nunito:wght@700;800;900&family=Plus+Jakarta+Sans:wght@700;800&display=swap');

        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
            -webkit-user-select: none;
        }

        .hidden {
            display: none !important;
        }

        html, body {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            height: 100dvh;
            overflow: hidden;
            font-family: 'Nunito', 'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #e0f2fe 0%, #f0fdf4 50%, #fef3c7 100%);
        }

        h1, h2, h3, .menu-title, #phonics-big-upper, #phonics-big-lower, #number-big-digit, #solar-title, #shape-text, #shape3d-title, #fruits-text, #animal-text, #things-text, #opp-title {
            font-family: 'Fredoka', 'Nunito', cursive, sans-serif;
        }

        .view-section {
            display: none;
            width: 100%;
            height: 100%;
            height: 100dvh;
            position: absolute;
            inset: 0;
            flex-direction: column;
            overflow: hidden;
        }

        #view-menu {
            background: linear-gradient(135deg, #e0f2fe 0%, #f0fdf4 50%, #fef3c7 100%);
            z-index: 10;
        }

        .view-section.active-view {
            display: flex;
        }

        .squish-btn {
            transition: transform 0.1s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.1s ease;
            cursor: pointer;
            touch-action: manipulation;
        }

        .squish-btn:active {
            transform: translateY(4px) scale(0.96);
        }

        .menu-scroll-container {
            flex: 1;
            width: 100%;
            overflow-y: auto;
            touch-action: pan-y;
            -webkit-overflow-scrolling: touch;
            padding: 0.5rem 1rem 3rem 1rem;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            gap: 1rem;
            width: 100%;
            max-width: 680px;
            margin: 0 auto;
        }

        @media (min-width: 640px) {
            .menu-grid {
                grid-template-columns: repeat(3, minmax(0, 1fr));
                gap: 1.25rem;
            }
        }

        .menu-card {
            background: #ffffff;
            border-radius: 2rem;
            padding: 1.15rem 0.85rem;
            box-shadow: 0 8px 0 #cbd5e1, 0 16px 24px -4px rgba(15, 23, 42, 0.08);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 0.35rem;
            cursor: pointer;
            touch-action: manipulation;
            position: relative;
            min-height: 145px;
            border: 3.5px solid #ffffff;
            transition: transform 0.12s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.12s ease;
        }

        .menu-card:active {
            transform: translateY(5px);
            box-shadow: 0 3px 0 #cbd5e1, 0 6px 10px -2px rgba(15, 23, 42, 0.1);
        }

        .menu-icon {
            font-size: 3.4rem;
            line-height: 1.1;
            filter: drop-shadow(0 4px 8px rgba(0,0,0,0.08));
            transition: transform 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .menu-card:hover .menu-icon {
            transform: scale(1.08);
        }

        .menu-title {
            font-weight: 900;
            color: #1e293b;
            font-size: 1.25rem;
            letter-spacing: -0.01em;
            text-align: center;
        }

        .menu-sub {
            font-weight: 800;
            font-size: 0.75rem;
            color: #64748b;
            text-transform: uppercase;
            letter-spacing: 0.04em;
        }

        .top-bar {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0.75rem 1rem;
            padding-top: max(0.6rem, env(safe-area-inset-top));
            z-index: 40;
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
            flex-shrink: 0;
            gap: 0.5rem;
        }

        .home-btn {
            background: #ffffff;
            padding: 0.6rem 1rem;
            border-radius: 9999px;
            box-shadow: 0 4px 0 #cbd5e1, 0 8px 16px -2px rgba(15, 23, 42, 0.08);
            border: 2px solid #e2e8f0;
            display: flex;
            align-items: center;
            gap: 0.4rem;
            font-weight: 900;
            color: #334155;
            font-size: 1rem;
            transition: transform 0.1s ease, box-shadow 0.1s ease;
        }

        .home-btn:active {
            transform: translateY(3px);
            box-shadow: 0 1px 0 #cbd5e1;
        }

        .mode-switch {
            display: flex;
            background: #ffffff;
            padding: 0.3rem;
            border-radius: 9999px;
            box-shadow: 0 4px 0 #cbd5e1, 0 8px 16px -2px rgba(15, 23, 42, 0.06);
            border: 2px solid #e2e8f0;
            gap: 0.3rem;
        }

        .mode-pill {
            padding: 0.45rem 0.95rem;
            border-radius: 9999px;
            font-weight: 900;
            font-size: 0.85rem;
            color: #475569;
            transition: all 0.15s cubic-bezier(0.34, 1.56, 0.64, 1);
            cursor: pointer;
        }

        .mode-pill.active {
            background: #3b82f6;
            color: #ffffff;
            box-shadow: 0 3px 0 #1d4ed8;
            transform: translateY(-1px);
        }

        .main-stage {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            max-width: 860px;
            margin: 0 auto;
            padding: 0.5rem 1rem;
            position: relative;
            overflow: hidden;
        }

        @keyframes popBounce {
            0% { transform: scale(0.86); }
            50% { transform: scale(1.06); }
            100% { transform: scale(1); }
        }

        .pop-anim {
            animation: popBounce 0.22s ease-out;
        }

        @keyframes gentleFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-7px); }
        }

        .float-anim {
            animation: gentleFloat 3s ease-in-out infinite;
        }

        @keyframes shakeWrong {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-8px); }
            75% { transform: translateX(8px); }
        }

        .shake-anim {
            animation: shakeWrong 0.3s ease-in-out;
        }

        .controls-dock {
            width: 100%;
            background: rgba(255, 255, 255, 0.88);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border-top: 3px solid rgba(255, 255, 255, 0.85);
            border-top-left-radius: 2.25rem;
            border-top-right-radius: 2.25rem;
            box-shadow: 0 -8px 32px rgba(15, 23, 42, 0.08);
            padding: 0.8rem 0.75rem 1rem 0.75rem;
            padding-bottom: max(0.85rem, env(safe-area-inset-bottom));
            z-index: 30;
            height: 28vh;
            min-height: 155px;
            max-height: 235px;
            flex-shrink: 0;
        }

        .control-scroll {
            width: 100%;
            height: 100%;
            overflow-y: auto;
            touch-action: pan-y;
            -webkit-overflow-scrolling: touch;
            padding: 0.25rem 0.5rem 1rem 0.5rem;
        }

        .control-grid {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 0.7rem;
            max-width: 820px;
            margin: 0 auto;
        }

        .tray-btn {
            width: 4.4rem;
            height: 4.4rem;
            border-radius: 1.35rem;
            background: #ffffff;
            border: 3px solid #e0e7ff;
            box-shadow: 0 5px 0 #cbd5e1, 0 6px 12px -2px rgba(15, 23, 42, 0.06);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 1.9rem;
            font-weight: 900;
            color: #1e293b;
            cursor: pointer;
            touch-action: manipulation;
            flex-shrink: 0;
            transition: transform 0.1s ease, box-shadow 0.1s ease, border-color 0.1s ease;
        }

        .tray-btn:active, .tray-btn.selected {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #94a3b8;
            border-color: #6366f1;
            background-color: #eef2ff;
        }

        .audio-vis-pill {
            display: inline-flex;
            align-items: center;
            gap: 3px;
            height: 22px;
            padding: 0 7px;
            background: rgba(99, 102, 241, 0.12);
            border: 1.5px solid rgba(99, 102, 241, 0.35);
            border-radius: 9999px;
            vertical-align: middle;
            transition: all 0.2s ease;
        }

        .vis-bar {
            width: 3px;
            height: 5px;
            border-radius: 9999px;
            background: #6366f1;
            transition: height 0.12s ease;
        }

        .audio-vis-pill.speaking .vis-bar {
            animation: visBounce 0.55s ease-in-out infinite alternate;
        }
        .audio-vis-pill.speaking .bar-1 { animation-delay: 0.0s; }
        .audio-vis-pill.speaking .bar-2 { animation-delay: 0.15s; }
        .audio-vis-pill.speaking .bar-3 { animation-delay: 0.3s; }
        .audio-vis-pill.speaking .bar-4 { animation-delay: 0.45s; }

        @keyframes visBounce {
            0% { height: 4px; }
            100% { height: 16px; }
        }

        /* iOS-style touch-friendly toggle switches for Parent Options */
        .toggle-switch {
            position: relative;
            display: inline-flex;
            align-items: center;
            cursor: pointer;
            user-select: none;
        }
        .toggle-switch input {
            position: absolute;
            opacity: 0;
            width: 0;
            height: 0;
        }
        .toggle-slider {
            width: 44px;
            height: 24px;
            background-color: #cbd5e1;
            border-radius: 9999px;
            transition: background-color 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            flex-shrink: 0;
        }
        .toggle-slider:before {
            content: "";
            position: absolute;
            width: 20px;
            height: 20px;
            left: 2px;
            top: 2px;
            background-color: #ffffff;
            border-radius: 50%;
            transition: transform 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 1px 3px rgba(0,0,0,0.25);
        }
        .toggle-switch input:checked + .toggle-slider {
            background-color: #4f46e5;
        }
        .toggle-switch input:checked + .toggle-slider:before {
            transform: translateX(20px);
        }

        .count-item-btn {
            width: 4.4rem;
            height: 4.4rem;
            border-radius: 1.35rem;
            background: #ffffff;
            border: 3px dashed #99f6e4;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.4rem;
            position: relative;
            cursor: pointer;
            touch-action: manipulation;
            opacity: 0.8;
            transform: scale(0.95);
            box-shadow: 0 4px 0 #ccfbf1;
            transition: all 0.15s ease;
        }

        .count-item-btn.counted {
            border: 3px solid #0d9488;
            background: #f0fdfa;
            opacity: 1;
            transform: scale(1.05);
            box-shadow: 0 5px 0 #0f766e;
        }

        .count-badge {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #0d9488;
            color: white;
            font-size: 0.9rem;
            font-weight: 900;
            width: 1.6rem;
            height: 1.6rem;
            border-radius: 9999px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid white;
        }

        .phonics-word-card {
            background: #ffffff;
            border: 3px solid #dbeafe;
            border-radius: 1.5rem;
            padding: 0.65rem 0.9rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-width: 88px;
            box-shadow: 0 6px 0 #bfdbfe, 0 8px 16px -3px rgba(30, 64, 175, 0.08);
            cursor: pointer;
            touch-action: manipulation;
            transition: transform 0.1s ease, box-shadow 0.1s ease;
        }
        .phonics-word-card:active {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #bfdbfe;
        }

        .phonics-bubble {
            position: absolute;
            border-radius: 9999px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            touch-action: manipulation;
            box-shadow: inset -6px -6px 14px rgba(0,0,0,0.12), inset 8px 8px 18px rgba(255,255,255,0.6), 0 8px 18px rgba(0,0,0,0.15);
            border: 4px solid rgba(255,255,255,0.9);
            color: #ffffff;
            font-weight: 900;
            transition: transform 0.2s ease, opacity 0.2s ease;
        }

        .confetti-piece {
            position: fixed;
            width: 11px;
            height: 11px;
            border-radius: 3px;
            pointer-events: none;
            z-index: 100;
            animation: confettiFall 0.95s ease-out forwards;
        }

        @keyframes confettiFall {
            0% { transform: translate(0, 0) rotate(0deg) scale(1); opacity: 1; }
            100% { transform: translate(var(--dx), var(--dy)) rotate(var(--rot)) scale(0.2); opacity: 0; }
        }

        .crumb-piece {
            position: fixed;
            border-radius: 9999px;
            pointer-events: none;
            z-index: 95;
            animation: crumbFly 0.5s ease-out forwards;
        }

        @keyframes crumbFly {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--cx), var(--cy)) scale(0.2); opacity: 0; }
        }

        #shape3d-canvas-container, #shape3d-canvas-container canvas,
        #solar-canvas-container, #solar-canvas-container canvas {
            touch-action: none;
            user-select: none;
            -webkit-user-select: none;
        }

        .solar-space-bg {
            background: radial-gradient(circle at 50% 35%, #1e1b4b 0%, #0f172a 65%, #020617 100%);
            color: #ffffff;
        }

        .fact-badge {
            background: #1e293b;
            border: 2px solid #475569;
            color: #f8fafc;
        }
    </style>
</head>
<body>

    <!-- MAIN MENU -->
    <div id="view-menu" class="view-section active-view" style="background: linear-gradient(135deg, #e0f2fe 0%, #f0fdf4 50%, #fef3c7 100%); z-index: 10;">
        <div class="text-center pt-5 pb-2 px-4 flex-shrink-0">
            <div class="inline-flex items-center gap-2 bg-white px-4 py-1 rounded-full shadow-sm border border-sky-200 mb-1">
                <span class="text-xl">🌟</span>
                <span class="text-xs font-black uppercase tracking-wider text-sky-700">Toddler Explorer • Level 2</span>
            </div>
            <h1 class="text-4xl sm:text-5xl font-black text-slate-800 tracking-tight">Toddler Learning Hub</h1>
                        <p class="text-slate-600 font-bold text-sm sm:text-base mt-0.5">Tap any card to play, count & sound it out!</p>
            <div class="flex justify-center items-center gap-2 mt-2">
                <button id="voice-settings-btn" class="inline-flex items-center gap-2 bg-white px-3.5 py-1.5 rounded-full shadow-sm border-2 border-indigo-200 text-xs sm:text-sm font-black text-indigo-700 squish-btn hover:bg-indigo-50">
                    <span>⚙️</span>
                    <span>Options & Voice</span>
                    <span id="voice-status-pill" class="inline-flex items-center gap-1.5 bg-slate-100 text-slate-700 text-[10px] font-black px-2 py-0.5 rounded-full border border-slate-200">
                        <span id="voice-status-dot" class="w-2 h-2 rounded-full bg-blue-500"></span>
                        <span id="voice-status-text">Device Voice</span>
                    </span>
                    <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
                </button>
            </div>
        </div>

        <div class="menu-scroll-container">
            <div class="menu-grid" id="main-menu-grid">
                <div data-view="letters" class="menu-card border-b-8 border-blue-400 squish-btn">
                    <span class="absolute top-2.5 right-3 bg-blue-100 text-blue-700 text-xs font-black px-2 py-0.5 rounded-full">Phonics!</span>
                    <div class="menu-icon text-blue-600 font-black">Aa</div>
                    <span class="menu-title">Phonics A–Z</span>
                    <span class="menu-sub">Sounds & Bubbles</span>
                </div>

                <div data-view="numbers" class="menu-card border-b-8 border-teal-400 squish-btn">
                    <span class="absolute top-2.5 right-3 bg-teal-100 text-teal-700 text-xs font-black px-2 py-0.5 rounded-full">1 to 20</span>
                    <div class="menu-icon text-teal-600 font-black">123</div>
                    <span class="menu-title">Tap & Count</span>
                    <span class="menu-sub">Touch to Count!</span>
                </div>

                <div data-view="quiz" class="menu-card border-b-8 border-amber-400 squish-btn">
                    <span class="absolute top-2.5 right-3 bg-amber-100 text-amber-800 text-xs font-black px-2 py-0.5 rounded-full">Quiz!</span>
                    <div class="menu-icon">🕵️</div>
                    <span class="menu-title">Look & Find</span>
                    <span class="menu-sub">Fun Quiz Game</span>
                </div>

                <div data-view="shapes" class="menu-card border-b-8 border-emerald-400 squish-btn">
                    <div class="menu-icon">
                        <svg width="54" height="54" viewBox="0 0 100 100">
                            <polygon points="50,12 88,84 12,84" fill="#10b981" stroke="#059669" stroke-width="4" stroke-linejoin="round"/>
                        </svg>
                    </div>
                    <span class="menu-title">2D Shapes</span>
                    <span class="menu-sub">12 Crisp Shapes</span>
                </div>

                <div data-view="shapes3d" class="menu-card border-b-8 border-indigo-400 squish-btn">
                    <div class="menu-icon">🧊</div>
                    <span class="menu-title">3D Shapes</span>
                    <span class="menu-sub">Spin & Examples</span>
                </div>

                <div data-view="colors" class="menu-card border-b-8 border-rose-400 squish-btn">
                    <div class="w-14 h-14 rounded-full bg-gradient-to-tr from-red-500 via-amber-400 to-blue-500 shadow-md border-2 border-white mb-1"></div>
                    <span class="menu-title">Colors & Mix</span>
                    <span class="menu-sub">Learn & Mix Paint</span>
                </div>

                <div data-view="animals" class="menu-card border-b-8 border-orange-400 squish-btn">
                    <div class="menu-icon">🦁</div>
                    <span class="menu-title">Animals</span>
                    <span class="menu-sub">Names & Sounds</span>
                </div>

                <div data-view="fruits" class="menu-card border-b-8 border-pink-400 squish-btn">
                    <div class="menu-icon">🍓</div>
                    <span class="menu-title">Yummy Foods</span>
                    <span class="menu-sub">Tap to Take a Bite!</span>
                </div>

                <div data-view="things" class="menu-card border-b-8 border-purple-400 squish-btn">
                    <div class="menu-icon">🚒</div>
                    <span class="menu-title">Vehicles & Things</span>
                    <span class="menu-sub">Beep & Zoom!</span>
                </div>

                <div data-view="opposites" class="menu-card border-b-8 border-cyan-400 squish-btn">
                    <div class="menu-icon">🐘🐁</div>
                    <span class="menu-title">Opposites</span>
                    <span class="menu-sub">Big, Small & More</span>
                </div>

                <div data-view="solar" class="menu-card border-b-8 border-violet-500 squish-btn">
                    <span class="absolute top-2.5 right-3 bg-violet-100 text-violet-800 text-xs font-black px-2 py-0.5 rounded-full">Space!</span>
                    <div class="menu-icon">🪐</div>
                    <span class="menu-title">Solar System</span>
                    <span class="menu-sub">Sun, Moon & Planets</span>
                </div>
            </div>
        </div>
    </div>

    <!-- VIEW: PHONICS LETTERS -->
    <div id="view-letters" class="view-section bg-blue-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch">
                <button id="phonics-mode-studio" class="mode-pill active">🔤 Sound Studio</button>
                <button id="phonics-mode-bubbles" class="mode-pill">🫧 Pop Bubbles</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div id="phonics-studio-stage" class="main-stage">
            <div id="phonics-main-card" class="bg-white rounded-3xl p-3 sm:p-5 shadow-lg border-4 border-blue-200 flex flex-col items-center w-full max-w-md cursor-pointer squish-btn">
                <div class="flex items-baseline gap-3">
                    <span id="phonics-big-upper" class="text-7xl sm:text-8xl font-black text-blue-600 leading-none">A</span>
                    <span id="phonics-big-lower" class="text-6xl sm:text-7xl font-black text-sky-500 leading-none">a</span>
                </div>
                <div id="phonics-sound-pill" class="mt-2 bg-amber-100 text-amber-900 font-black px-4 py-1 rounded-full text-base sm:text-lg border-2 border-amber-300">
                    🔊 Sound: "ah" (like Apple)
                </div>
            </div>
            <p class="text-xs sm:text-sm font-extrabold text-slate-500 uppercase tracking-wider mt-3 mb-1.5">Tap a picture to sound it out!</p>
            <div id="phonics-words-row" class="flex flex-wrap justify-center gap-2 sm:gap-3 w-full"></div>
            <div id="phonics-blend-bar" class="hidden mt-3 bg-blue-100/90 border-2 border-blue-300 px-4 py-2 rounded-2xl flex items-center justify-center gap-2 shadow-sm max-w-md w-full">
                <span class="text-xs font-black uppercase tracking-wider text-blue-800">Sound it out:</span>
                <div id="phonics-blend-letters" class="flex items-center gap-1 text-lg sm:text-xl font-black text-blue-900"></div>
            </div>
        </div>

        <div id="phonics-bubble-stage" class="main-stage hidden w-full h-full relative">
            <div class="bg-white px-5 py-2.5 rounded-2xl shadow-md border-2 border-blue-200 z-20 flex items-center gap-3 mb-auto mt-1">
                <span class="text-2xl" id="bubble-prompt-emoji">🍎</span>
                <span class="font-black text-slate-800 text-lg sm:text-xl" id="bubble-prompt-text">Pop a bubble!</span>
                <button id="bubble-repeat-btn" class="bg-blue-100 text-blue-700 font-black px-3 py-1 rounded-xl text-sm squish-btn">🔊 Hear</button>
            </div>
            <div id="phonics-bubbles-canvas" class="w-full flex-1 relative overflow-hidden"></div>
        </div>

        <div id="phonics-controls-dock" class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="phonics-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: NUMBERS -->
    <div id="view-numbers" class="view-section bg-teal-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch">
                <button id="num-mode-touch" class="mode-pill active">👆 Tap to Count</button>
                <button id="num-mode-show" class="mode-pill">✨ Auto Count</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div class="main-stage justify-between py-1.5">
            <div class="flex items-center gap-3 sm:gap-4 mb-1 flex-shrink-0">
                <div id="number-big-digit" class="text-5xl sm:text-7xl font-black text-teal-700 leading-none cursor-pointer squish-btn">1</div>
                <div class="flex flex-col">
                    <span id="number-word-label" class="text-xl sm:text-3xl font-black text-slate-800 leading-tight">One</span>
                    <span id="number-instruction" class="text-[11px] sm:text-sm font-extrabold text-teal-600 bg-teal-100 px-2.5 py-0.5 rounded-full">Tap each ☀️ to count! (0/1)</span>
                </div>
                <button id="number-count-all-btn" class="bg-teal-600 text-white font-black px-3 py-1.5 sm:px-3.5 sm:py-2 rounded-2xl shadow-md text-xs sm:text-sm squish-btn">🔊 Count All</button>
            </div>
            <div id="number-items-grid" class="flex-1 min-h-0 w-full max-w-xl flex flex-wrap justify-center items-center content-center gap-1.5 sm:gap-2.5 overflow-hidden px-1 my-1"></div>
            <div id="number-ten-frame" class="flex-shrink-0 z-10 mt-1 mb-1 flex gap-1.5 flex-wrap justify-center bg-white px-3 py-1.5 rounded-2xl border-2 border-teal-200 shadow-sm"></div>
        </div>

        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="number-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: QUIZ -->
    <div id="view-quiz" class="view-section bg-amber-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch flex-wrap justify-center">
                <button data-quiz-cat="all" class="mode-pill active quiz-cat-btn">🌟 All</button>
                <button data-quiz-cat="letters" class="mode-pill quiz-cat-btn">🔤 ABC</button>
                <button data-quiz-cat="numbers" class="mode-pill quiz-cat-btn">🔢 123</button>
                <button data-quiz-cat="animals" class="mode-pill quiz-cat-btn">🦁 Animals</button>
                <button data-quiz-cat="shapes" class="mode-pill quiz-cat-btn">🔷 Shapes</button>
                <button data-quiz-cat="solar" class="mode-pill quiz-cat-btn">🪐 Space</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div class="main-stage">
            <div id="quiz-prompt-box" class="bg-white px-6 py-4 rounded-3xl shadow-md border-4 border-amber-300 text-center max-w-md w-full mb-5 cursor-pointer squish-btn">
                <p class="text-xs font-black uppercase tracking-wider text-amber-600 mb-1">Tap to hear again 🔊</p>
                <h2 id="quiz-question-text" class="text-2xl sm:text-3xl font-black text-slate-800">Can you find the Lion?</h2>
            </div>
            <div id="quiz-choices-grid" class="grid grid-cols-3 gap-3 sm:gap-5 w-full max-w-xl px-2"></div>
            <div class="mt-6 flex items-center gap-3">
                <div class="bg-white px-4 py-1.5 rounded-full font-black text-amber-700 border-2 border-amber-200 shadow-sm">
                    ⭐ Stars: <span id="quiz-score">0</span>
                </div>
                <button id="quiz-next-btn" class="bg-amber-500 text-white font-black px-5 py-2 rounded-full shadow-md squish-btn">Next Question ➡️</button>
            </div>
        </div>
    </div>

    <!-- VIEW: 2D SHAPES -->
    <div id="view-shapes" class="view-section bg-emerald-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="bg-white px-4 py-1.5 rounded-full font-black text-emerald-700 text-sm border-2 border-emerald-100 shadow-sm">Tap the shape to bounce!</div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div class="main-stage">
            <div id="shape-target" class="w-48 h-48 sm:w-56 sm:h-56 flex items-center justify-center cursor-pointer squish-btn"></div>
            <h1 id="shape-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-2">Circle</h1>
            <div id="shape-realworld" class="mt-2 bg-white px-4 py-1.5 rounded-full border-2 border-emerald-200 font-extrabold text-slate-700 text-sm sm:text-base shadow-sm">
                Looks like: 🍕 Pizza • ⏰ Clock • 🛞 Wheel
            </div>
        </div>

        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="shape-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: 3D SHAPES -->
    <div id="view-shapes3d" class="view-section bg-indigo-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="bg-white px-4 py-1.5 rounded-full font-black text-indigo-700 text-sm border-2 border-indigo-100 shadow-sm">Drag any direction to spin! 🔄</div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div class="main-stage">
            <div id="shape3d-examples-bar" class="flex flex-wrap justify-center gap-1.5 sm:gap-2 mb-1 z-20 px-2"></div>
            <div id="shape3d-target" class="w-56 h-56 sm:w-64 sm:h-64 flex items-center justify-center relative">
                <div id="shape3d-canvas-container" class="w-full h-full flex items-center justify-center cursor-grab active:cursor-grabbing"></div>
            </div>
            <h1 id="shape3d-text" class="text-3xl sm:text-4xl font-black text-slate-800 mt-0.5">Cube</h1>
            <div id="shape3d-realworld" class="mt-1 bg-white px-4 py-1 rounded-full border-2 border-indigo-200 font-extrabold text-slate-700 text-xs sm:text-sm shadow-sm">
                Tap an example above or spin with your finger!
            </div>
        </div>

        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="shape3d-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: COLORS -->
    <div id="view-colors" class="view-section bg-slate-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch">
                <button id="color-mode-explore" class="mode-pill active">🎨 Explore Colors</button>
                <button id="color-mode-mix" class="mode-pill">🧪 Mix 2 Colors!</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div id="color-bg-target" class="main-stage rounded-3xl my-1 transition-colors duration-300" style="background-color: #ef4444;">
            <div id="color-explore-box" class="flex flex-col items-center">
                <h1 id="color-text" class="text-5xl sm:text-6xl font-black text-white drop-shadow tracking-tight">Red</h1>
                <div id="color-examples" class="mt-4 flex gap-4 bg-white px-6 py-3 rounded-3xl shadow-lg text-4xl sm:text-5xl cursor-pointer squish-btn">
                    <span>🍎</span><span>🚒</span><span>🍓</span>
                </div>
            </div>

            <div id="color-mix-box" class="hidden flex-col items-center bg-white p-5 rounded-3xl shadow-xl border-4 border-slate-100 max-w-md w-full">
                <p class="text-xs font-black uppercase tracking-wider text-slate-500 mb-2">Tap 2 colors below to mix them!</p>
                <div class="flex items-center justify-center gap-3 sm:gap-4 my-2">
                    <div id="mix-slot-1" class="w-16 h-16 rounded-full border-4 border-slate-300 bg-red-500"></div>
                    <span class="text-3xl font-black text-slate-700">+</span>
                    <div id="mix-slot-2" class="w-16 h-16 rounded-full border-4 border-slate-300 bg-yellow-400"></div>
                    <span class="text-3xl font-black text-slate-700">=</span>
                    <div id="mix-result-circle" class="w-20 h-20 rounded-full border-4 border-slate-800 shadow-md bg-orange-500 flex items-center justify-center text-2xl">✨</div>
                </div>
                <h2 id="mix-result-text" class="text-2xl font-black text-slate-800 mt-2">Red + Yellow = Orange!</h2>
            </div>
        </div>

        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="color-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: ANIMALS -->
    <div id="view-animals" class="view-section bg-orange-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <button id="animal-sound-btn" class="bg-orange-500 text-white font-black px-4 py-2 rounded-full shadow-md squish-btn text-sm">🔊 Hear Animal Sound!</button>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>
        <div class="main-stage">
            <div id="animal-target" class="text-[7.5rem] sm:text-[9rem] leading-none cursor-pointer squish-btn">🦁</div>
            <h1 id="animal-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-2">Lion</h1>
            <div id="animal-sound-pill" class="mt-2 bg-white px-5 py-1.5 rounded-full border-2 border-orange-300 font-black text-orange-700 text-lg shadow-sm cursor-pointer squish-btn">
                🗣️ "ROAR!"
            </div>
        </div>
        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="animal-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: YUMMY FOODS -->
    <div id="view-fruits" class="view-section bg-pink-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <button id="food-chomp-btn" class="bg-pink-500 text-white font-black px-4 py-2 rounded-full shadow-md squish-btn text-sm">😋 Tap Food to Take a Bite!</button>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>
        <div class="main-stage">
            <div id="fruits-target" class="relative w-52 h-52 sm:w-60 sm:h-60 flex items-center justify-center cursor-pointer squish-btn">
                <canvas id="fruits-canvas" width="240" height="240" class="w-full h-full"></canvas>
            </div>
            <h1 id="fruits-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-1">Strawberry</h1>
            <div id="fruits-desc" class="mt-1.5 bg-white px-4 py-1 rounded-full border-2 border-pink-200 font-extrabold text-pink-700 text-sm shadow-sm">
                Sweet Red Berry! Tap anywhere on it to take a bite!
            </div>
        </div>
        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="fruits-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: VEHICLES & THINGS -->
    <div id="view-things" class="view-section bg-purple-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="bg-white px-4 py-1.5 rounded-full font-black text-purple-700 text-sm border-2 border-purple-100 shadow-sm">Tap to hear it go! 🚦</div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>
        <div class="main-stage">
            <div id="things-target" class="text-[7.5rem] sm:text-[9rem] leading-none cursor-pointer squish-btn">🚒</div>
            <h1 id="things-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-2">Fire Truck</h1>
            <div id="things-sound" class="mt-1.5 bg-white px-5 py-1 rounded-full border-2 border-purple-200 font-black text-purple-700 text-base shadow-sm cursor-pointer squish-btn">
                🔊 "Weee-oooo! Weee-oooo!"
            </div>
        </div>
        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="things-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: OPPOSITES -->
    <div id="view-opposites" class="view-section bg-cyan-50">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="bg-white px-4 py-1.5 rounded-full font-black text-cyan-700 text-sm border-2 border-cyan-100 shadow-sm">Tap each card to compare! 🔄</div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>
        <div class="main-stage">
            <div class="grid grid-cols-2 gap-4 sm:gap-6 w-full max-w-lg px-2">
                <div id="opp-card-a" class="bg-white rounded-3xl p-5 shadow-md border-4 border-cyan-300 flex flex-col items-center justify-center min-h-[200px] cursor-pointer squish-btn">
                    <div id="opp-emoji-a" class="text-7xl sm:text-8xl mb-2">🐘</div>
                    <span id="opp-label-a" class="text-2xl sm:text-3xl font-black text-slate-800">Big</span>
                </div>
                <div id="opp-card-b" class="bg-white rounded-3xl p-5 shadow-md border-4 border-amber-300 flex flex-col items-center justify-center min-h-[200px] cursor-pointer squish-btn">
                    <div id="opp-emoji-b" class="text-4xl sm:text-5xl mb-2">🐁</div>
                    <span id="opp-label-b" class="text-2xl sm:text-3xl font-black text-slate-800">Small</span>
                </div>
            </div>
            <h2 id="opp-title" class="text-2xl sm:text-3xl font-black text-slate-700 mt-4">Big vs. Small</h2>
        </div>
        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="opposites-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: SOLAR SYSTEM -->
    <div id="view-solar" class="view-section solar-space-bg">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch">
                <button id="solar-mode-photo" class="mode-pill active">📸 Space View</button>
                <button id="solar-mode-planet" class="mode-pill">🪐 3D Spin</button>
                <button id="solar-mode-orbit" class="mode-pill">☀️ Orbit</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>

        <div class="main-stage">
            <div class="flex flex-wrap items-center justify-center gap-2 z-20 mb-1">
                <span id="solar-order-badge" class="bg-indigo-900/90 border border-indigo-400/50 text-indigo-100 text-xs sm:text-sm font-black px-3 py-0.5 rounded-full">
                    ⭐ Center of the Solar System
                </span>
                <button id="solar-action-btn" class="bg-amber-400 text-slate-900 font-black px-3.5 py-1 rounded-full text-xs sm:text-sm shadow-md squish-btn flex items-center gap-1">
                    <span>🔊</span><span id="solar-action-label">Fun Fact!</span>
                </button>
            </div>

            <div id="solar-stage-box" class="w-60 h-60 sm:w-68 sm:h-68 flex items-center justify-center relative">
                <div id="solar-photo-container" class="w-full h-full flex flex-col items-center justify-center relative cursor-pointer squish-btn">
                    <div id="solar-svg-holder" class="w-52 h-52 sm:w-60 sm:h-60 rounded-full overflow-hidden border-4 border-indigo-300/40 shadow-xl bg-slate-950 flex items-center justify-center"></div>
                    <span id="solar-photo-credit" class="mt-1.5 text-[11px] font-extrabold uppercase tracking-wider text-indigo-200 bg-slate-900 px-3 py-0.5 rounded-full border border-indigo-400/30">
                        🔭 Space Telescope View
                    </span>
                </div>

                <div id="solar-canvas-container" class="hidden w-full h-full flex items-center justify-center cursor-grab active:cursor-grabbing"></div>
            </div>

            <h1 id="solar-title" class="text-3xl sm:text-5xl font-black text-white tracking-tight mt-0.5">The Sun</h1>
            <div id="solar-fact" class="mt-1.5 fact-badge px-4 py-1.5 rounded-2xl font-extrabold text-xs sm:text-base text-center max-w-md shadow-md cursor-pointer squish-btn">
                Our giant, glowing star! It keeps Earth warm and bright!
            </div>
        </div>

        <div class="controls-dock" style="background: #0f172a; border-top-color: #334155;">
            <div class="control-scroll"><div class="control-grid" id="solar-controls"></div></div>
        </div>
    </div>

    <!-- VOICE & AUDIO SETTINGS MODAL -->
        <div id="voice-settings-modal" class="fixed inset-0 z-50 hidden flex items-center justify-center bg-slate-900/60 backdrop-blur-sm p-4">
        <div class="bg-white rounded-3xl max-w-lg w-full p-4 sm:p-6 shadow-2xl border-4 border-indigo-200 flex flex-col gap-3.5 max-h-[92vh] overflow-y-auto">
            <div class="flex items-center justify-between border-b pb-3 flex-shrink-0">
                <div class="flex items-center gap-2.5">
                    <span class="text-3xl">⚙️</span>
                    <div>
                        <h2 class="text-xl sm:text-2xl font-black text-slate-800 leading-tight">Options & Voice Settings</h2>
                        <p class="text-xs text-slate-500 font-bold">App Features, Toddler Controls & Speech Audio</p>
                    </div>
                </div>
                <button id="voice-modal-close-x" class="text-slate-400 hover:text-slate-700 text-2xl font-black p-1 squish-btn" title="Close">✕</button>
            </div>

            <!-- Game & Audio Options Section -->
            <div class="flex flex-col gap-2">
                <div class="flex items-center gap-1.5 mb-0.5">
                    <span class="text-sm">🎛️</span>
                    <h3 class="text-xs font-black uppercase tracking-wider text-slate-700">Game & Audio Options</h3>
                </div>

                <div class="grid grid-cols-1 gap-2">
                    <!-- 1. Announce Game When Opened -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-indigo-50/70 hover:bg-indigo-50 border border-indigo-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-indigo-950 flex items-center gap-1.5">
                                <span>📢</span><span>Announce Game When Opened</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Speak the game name & intro when opening a game</div>
                        </div>
                        <input id="opt-announce-open" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 2. Voice & Speech (TTS) -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🗣️</span><span>Voice & Speech (TTS)</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Read words, letters, numbers, and prompts aloud</div>
                        </div>
                        <input id="opt-voice-enabled" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 3. Sound Effects (SFX) -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔊</span><span>Sound Effects (SFX)</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Play animal sounds, sirens, crunches, and chimes</div>
                        </div>
                        <input id="opt-sfx-enabled" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 4. Speech Speed -->
                    <div class="flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 border border-slate-200 gap-2">
                        <div>
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🐢</span><span>Speech Speed</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Pacing for spoken words and prompts</div>
                        </div>
                        <select id="opt-speech-rate" class="px-2.5 py-1.5 rounded-xl border-2 border-slate-300 font-bold text-xs bg-white text-slate-800 focus:border-indigo-500 focus:outline-none flex-shrink-0">
                            <option value="slow">🐢 Slow (0.82x)</option>
                            <option value="normal">🚶 Normal (0.96x)</option>
                            <option value="fast">🐇 Fast (1.10x)</option>
                        </select>
                    </div>

                    <!-- 5. Counting Range -->
                    <div class="flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 border border-slate-200 gap-2">
                        <div>
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔢</span><span>Counting Range</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Numbers tray and quiz counting pool</div>
                        </div>
                        <select id="opt-max-number" class="px-2.5 py-1.5 rounded-xl border-2 border-slate-300 font-bold text-xs bg-white text-slate-800 focus:border-indigo-500 focus:outline-none flex-shrink-0">
                            <option value="20">1 to 20 (Advanced)</option>
                            <option value="10">1 to 10 (Beginner)</option>
                        </select>
                    </div>

                    <!-- 6. Phonics Style -->
                    <div class="flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 border border-slate-200 gap-2">
                        <div>
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔤</span><span>Phonics Style</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Phonics detail when sounding out letters</div>
                        </div>
                        <select id="opt-phonics-detail" class="px-2.5 py-1.5 rounded-xl border-2 border-slate-300 font-bold text-xs bg-white text-slate-800 focus:border-indigo-500 focus:outline-none flex-shrink-0">
                            <option value="full">Full Phonics (Sound + Cue + Word)</option>
                            <option value="simple">Simple (Letter + Word)</option>
                        </select>
                    </div>

                    <!-- 7. Confetti & Crumb Effects -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🎉</span><span>Confetti & Crumb Effects</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Show celebratory confetti bursts and food crumbs</div>
                        </div>
                        <input id="opt-confetti-enabled" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 8. Auto-Spin 3D Shapes & Planets -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🌀</span><span>Auto-Spin 3D Shapes & Planets</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Gently spin 3D models automatically</div>
                        </div>
                        <input id="opt-autospin-3d" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 9. Toddler Home-Button Lock -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔒</span><span>Toddler Home-Button Lock</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Require double-tap on Home button to exit a game</div>
                        </div>
                        <input id="opt-hold-home" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>
                </div>
            </div>

            <!-- Gemini Voice / Cloud TTS Section -->
            <div class="border-t pt-3 mt-0.5 flex flex-col gap-3">
                <div class="flex items-center justify-between">
                    <div class="flex items-center gap-1.5">
                        <span class="text-sm">🎙️</span>
                        <h3 class="text-xs font-black uppercase tracking-wider text-slate-700">Gemini 3.8 Natural Voice & API Key</h3>
                    </div>
                    <span id="canvas-key-badge" class="text-[11px] font-extrabold text-indigo-600 bg-indigo-50 px-2 py-0.5 rounded-full border border-indigo-100">Canvas Key Auto-Detected</span>
                </div>

                <div class="flex flex-col gap-1.5">
                    <input id="gemini-api-key-input" type="password" placeholder="AIzaSy... (Paste Gemini API Key)"
                           class="w-full px-3.5 py-2.5 rounded-xl border-2 border-slate-300 font-mono text-sm focus:border-indigo-500 focus:outline-none bg-slate-50">
                    <p class="text-[11px] text-slate-500 font-semibold leading-tight">
                        💡 Optional: Gemini natural voices provide expressive storytelling. If left blank, natural device speech works 100% offline!
                    </p>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                    <div class="flex flex-col gap-1">
                        <label class="text-xs font-black uppercase tracking-wider text-slate-700">TTS Model</label>
                        <select id="gemini-tts-model-select" class="w-full px-3 py-2 rounded-xl border-2 border-slate-300 font-bold text-sm bg-slate-50 focus:border-indigo-500 focus:outline-none">
                            <option value="gemini-3.8-flash-tts">gemini-3.8-flash-tts (Expressive Studio)</option>
                            <option value="gemini-3.8-flash-lite-tts">gemini-3.8-flash-lite-tts (Low Latency)</option>
                        </select>
                    </div>

                    <div class="flex flex-col gap-1">
                        <label class="text-xs font-black uppercase tracking-wider text-slate-700">Voice Persona</label>
                        <select id="gemini-tts-voice-select" class="w-full px-3 py-2 rounded-xl border-2 border-slate-300 font-bold text-sm bg-slate-50 focus:border-indigo-500 focus:outline-none">
                            <option value="Kore">Kore (Warm Storyteller — Default)</option>
                            <option value="Puck">Puck (Playful & Energetic Buddy)</option>
                            <option value="Aoede">Aoede (Melodic Educator)</option>
                            <option value="Leda">Leda (Bright & Cheerful)</option>
                            <option value="Fenrir">Fenrir (Friendly Deep Voice)</option>
                        </select>
                    </div>
                </div>

                <div id="voice-test-status" class="hidden text-xs font-bold text-center py-2 px-3 rounded-xl transition-all duration-200"></div>
                <div class="flex flex-wrap items-center gap-2 pt-1">
                    <button id="voice-test-btn" class="flex-1 bg-indigo-100 hover:bg-indigo-200 text-indigo-800 font-black px-4 py-2.5 rounded-xl text-sm squish-btn flex items-center justify-center gap-1.5">
                        <span>🔊</span><span>Test Voice Sample</span>
                        <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
                    </button>
                    <button id="voice-precache-btn" class="flex-1 bg-amber-100 hover:bg-amber-200 text-amber-900 font-black px-4 py-2.5 rounded-xl text-sm squish-btn flex items-center justify-center gap-1.5">
                        <span>⚡</span><span id="voice-precache-label">Pre-cache Core Words</span>
                        <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
                    </button>
                </div>

                <div id="precache-progress-box" class="hidden flex-col gap-1 bg-amber-50 border border-amber-200 rounded-xl p-2.5 text-xs text-amber-900 font-bold">
                    <div class="flex justify-between items-center">
                        <span id="precache-progress-text">Pre-caching audio...</span>
                        <span id="precache-progress-num">0%</span>
                    </div>
                    <div class="w-full bg-amber-200 rounded-full h-2 overflow-hidden">
                        <div id="precache-progress-bar" class="bg-amber-600 h-full w-0 transition-all duration-150"></div>
                    </div>
                </div>
            </div>

            <!-- Footer: Reset Defaults & Save Buttons -->
            <div class="flex items-center justify-between gap-3 border-t pt-3 mt-1 flex-shrink-0">
                <button id="opt-reset-defaults-btn" type="button" class="bg-slate-100 hover:bg-slate-200 text-slate-700 font-black px-4 py-2.5 rounded-xl text-sm squish-btn border border-slate-300">
                    ↺ Reset Defaults
                </button>
                <button id="voice-modal-save-btn" type="button" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white font-black py-2.5 rounded-xl shadow-md squish-btn text-base">
                    Save & Done
                </button>
            </div>
        </div>
    </div><script>
(() => {
'use strict';

function cleanStrayTextNodes() {
    const sanitize = (parent) => {
        if (!parent) return;
        const nodes = Array.from(parent.childNodes);
        nodes.forEach(node => {
            if (node.nodeType === Node.TEXT_NODE) {
                const val = node.nodeValue || '';
                if (/<!?DOCTYPE|<html/i.test(val)) {
                    node.parentNode.removeChild(node);
                } else if (node.parentNode === document.documentElement && val.trim().length > 0) {
                    node.parentNode.removeChild(node);
                } else if (node.parentNode === document.body && /<!?DOCTYPE|<html/i.test(val)) {
                    node.parentNode.removeChild(node);
                }
            }
        });
    };
    try {
        sanitize(document);
        sanitize(document.documentElement);
        sanitize(document.body);
        const menu = document.getElementById('view-menu');
        if (menu) {
            Array.from(menu.childNodes).forEach(node => {
                if (node.nodeType === Node.TEXT_NODE && /<!?DOCTYPE|<html/i.test(node.nodeValue || '')) {
                    node.parentNode.removeChild(node);
                }
            });
        }
    } catch (e) {}
}
cleanStrayTextNodes();
window.addEventListener('DOMContentLoaded', cleanStrayTextNodes);

// scratch/data.js
const GAMES = {
    phonics: [
        {
            letter: 'A', soundSpell: 'ah', cue: 'A says ah!',
            words: [
                { w: 'Apple', e: '🍎', phoneme: 'ah', highlightIdx: 0 },
                { w: 'Ant', e: '🐜', phoneme: 'ah', highlightIdx: 0 },
                { w: 'Astronaut', e: '👨‍🚀', phoneme: 'ah', highlightIdx: 0 }
            ]
        },
        {
            letter: 'B', soundSpell: 'buh', cue: 'B says buh!',
            words: [
                { w: 'Bear', e: '🐻', phoneme: 'buh', highlightIdx: 0 },
                { w: 'Ball', e: '⚽', phoneme: 'buh', highlightIdx: 0 },
                { w: 'Banana', e: '🍌', phoneme: 'buh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'C', soundSpell: 'kuh', cue: 'C says kuh!',
            words: [
                { w: 'Cat', e: '🐱', phoneme: 'kuh', highlightIdx: 0 },
                { w: 'Car', e: '🚗', phoneme: 'kuh', highlightIdx: 0 },
                { w: 'Cookie', e: '🍪', phoneme: 'kuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'D', soundSpell: 'duh', cue: 'D says duh!',
            words: [
                { w: 'Dog', e: '🐶', phoneme: 'duh', highlightIdx: 0 },
                { w: 'Duck', e: '🦆', phoneme: 'duh', highlightIdx: 0 },
                { w: 'Drum', e: '🥁', phoneme: 'duh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'E', soundSpell: 'eh', cue: 'E says eh!',
            words: [
                { w: 'Elephant', e: '🐘', phoneme: 'eh', highlightIdx: 0 },
                { w: 'Egg', e: '🥚', phoneme: 'eh', highlightIdx: 0 },
                { w: 'Engine', e: '🚂', phoneme: 'eh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'F', soundSpell: 'fff', cue: 'F says fff!',
            words: [
                { w: 'Fish', e: '🐟', phoneme: 'fff', highlightIdx: 0 },
                { w: 'Frog', e: '🐸', phoneme: 'fff', highlightIdx: 0 },
                { w: 'Fire Truck', e: '🚒', phoneme: 'fff', highlightIdx: 0 }
            ]
        },
        {
            letter: 'G', soundSpell: 'guh', cue: 'G says guh!',
            words: [
                { w: 'Grapes', e: '🍇', phoneme: 'guh', highlightIdx: 0 },
                { w: 'Goat', e: '🐐', phoneme: 'guh', highlightIdx: 0 },
                { w: 'Guitar', e: '🎸', phoneme: 'guh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'H', soundSpell: 'huh', cue: 'H says huh!',
            words: [
                { w: 'Horse', e: '🐎', phoneme: 'huh', highlightIdx: 0 },
                { w: 'Hat', e: '🧢', phoneme: 'huh', highlightIdx: 0 },
                { w: 'House', e: '🏠', phoneme: 'huh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'I', soundSpell: 'ih', cue: 'I says ih!',
            words: [
                { w: 'Igloo', e: '🛖', phoneme: 'ih', highlightIdx: 0 },
                { w: 'Iguana', e: '🦎', phoneme: 'ih', highlightIdx: 0 },
                { w: 'Insect', e: '🐞', phoneme: 'ih', highlightIdx: 0 }
            ]
        },
        {
            letter: 'J', soundSpell: 'juh', cue: 'J says juh!',
            words: [
                { w: 'Juice', e: '🧃', phoneme: 'juh', highlightIdx: 0 },
                { w: 'Jellyfish', e: '🪼', phoneme: 'juh', highlightIdx: 0 },
                { w: 'Jet', e: '✈️', phoneme: 'juh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'K', soundSpell: 'kuh', cue: 'K says kuh!',
            words: [
                { w: 'Kangaroo', e: '🦘', phoneme: 'kuh', highlightIdx: 0 },
                { w: 'Key', e: '🔑', phoneme: 'kuh', highlightIdx: 0 },
                { w: 'Kite', e: '🪁', phoneme: 'kuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'L', soundSpell: 'lll', cue: 'L says lll!',
            words: [
                { w: 'Lion', e: '🦁', phoneme: 'lll', highlightIdx: 0 },
                { w: 'Lemon', e: '🍋', phoneme: 'lll', highlightIdx: 0 },
                { w: 'Leaf', e: '🍃', phoneme: 'lll', highlightIdx: 0 }
            ]
        },
        {
            letter: 'M', soundSpell: 'mmm', cue: 'M says mmm!',
            words: [
                { w: 'Monkey', e: '🐵', phoneme: 'mmm', highlightIdx: 0 },
                { w: 'Moon', e: '🌙', phoneme: 'mmm', highlightIdx: 0 },
                { w: 'Milk', e: '🥛', phoneme: 'mmm', highlightIdx: 0 }
            ]
        },
        {
            letter: 'N', soundSpell: 'nnn', cue: 'N says nnn!',
            words: [
                { w: 'Nest', e: '🪺', phoneme: 'nnn', highlightIdx: 0 },
                { w: 'Nut', e: '🥜', phoneme: 'nnn', highlightIdx: 0 },
                { w: 'Nose', e: '👃', phoneme: 'nnn', highlightIdx: 0 }
            ]
        },
        {
            letter: 'O', soundSpell: 'ah', cue: 'O says ah!',
            words: [
                { w: 'Octopus', e: '🐙', phoneme: 'ah', highlightIdx: 0 },
                { w: 'Otter', e: '🦦', phoneme: 'ah', highlightIdx: 0 },
                { w: 'Orange', e: '🍊', phoneme: 'or', highlightIdx: 0 }
            ]
        },
        {
            letter: 'P', soundSpell: 'puh', cue: 'P says puh!',
            words: [
                { w: 'Pig', e: '🐷', phoneme: 'puh', highlightIdx: 0 },
                { w: 'Pizza', e: '🍕', phoneme: 'puh', highlightIdx: 0 },
                { w: 'Penguin', e: '🐧', phoneme: 'puh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'Q', soundSpell: 'kwuh', cue: 'Q says kwuh!',
            words: [
                { w: 'Queen', e: '👑', phoneme: 'kwuh', highlightIdx: 0 },
                { w: 'Quack Duck', e: '🦆', phoneme: 'kwuh', highlightIdx: 0 },
                { w: 'Question', e: '❓', phoneme: 'kwuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'R', soundSpell: 'rrr', cue: 'R says rrr!',
            words: [
                { w: 'Rabbit', e: '🐰', phoneme: 'rrr', highlightIdx: 0 },
                { w: 'Rocket', e: '🚀', phoneme: 'rrr', highlightIdx: 0 },
                { w: 'Rainbow', e: '🌈', phoneme: 'rrr', highlightIdx: 0 }
            ]
        },
        {
            letter: 'S', soundSpell: 'sss', cue: 'S says sss!',
            words: [
                { w: 'Sun', e: '☀️', phoneme: 'sss', highlightIdx: 0 },
                { w: 'Star', e: '⭐', phoneme: 'sss', highlightIdx: 0 },
                { w: 'Snake', e: '🐍', phoneme: 'sss', highlightIdx: 0 }
            ]
        },
        {
            letter: 'T', soundSpell: 'tuh', cue: 'T says tuh!',
            words: [
                { w: 'Tiger', e: '🐯', phoneme: 'tuh', highlightIdx: 0 },
                { w: 'Train', e: '🚂', phoneme: 'tuh', highlightIdx: 0 },
                { w: 'Turtle', e: '🐢', phoneme: 'tuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'U', soundSpell: 'uh', cue: 'U says uh!',
            words: [
                { w: 'Umbrella', e: '☂️', phoneme: 'uh', highlightIdx: 0 },
                { w: 'Up', e: '⬆️', phoneme: 'uh', highlightIdx: 0 },
                { w: 'Unicorn', e: '🦄', phoneme: 'yoo', highlightIdx: 0 }
            ]
        },
        {
            letter: 'V', soundSpell: 'vvv', cue: 'V says vvv!',
            words: [
                { w: 'Violin', e: '🎻', phoneme: 'vvv', highlightIdx: 0 },
                { w: 'Van', e: '🚐', phoneme: 'vvv', highlightIdx: 0 },
                { w: 'Volcano', e: '🌋', phoneme: 'vvv', highlightIdx: 0 }
            ]
        },
        {
            letter: 'W', soundSpell: 'wuh', cue: 'W says wuh!',
            words: [
                { w: 'Watermelon', e: '🍉', phoneme: 'wuh', highlightIdx: 0 },
                { w: 'Whale', e: '🐳', phoneme: 'wuh', highlightIdx: 0 },
                { w: 'Watch', e: '⌚', phoneme: 'wuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'X', soundSpell: 'ks', cue: 'X makes the ks sound!',
            words: [
                { w: 'Fox', e: '🦊', phoneme: 'ks', highlightIdx: 2 },
                { w: 'Box', e: '📦', phoneme: 'ks', highlightIdx: 2 },
                { w: 'X-Ray', e: '🩻', phoneme: 'eks', highlightIdx: 0 }
            ]
        },
        {
            letter: 'Y', soundSpell: 'yuh', cue: 'Y says yuh!',
            words: [
                { w: 'Yo-yo', e: '🪀', phoneme: 'yuh', highlightIdx: 0 },
                { w: 'Yarn', e: '🧶', phoneme: 'yuh', highlightIdx: 0 },
                { w: 'Yellow', e: '💛', phoneme: 'yuh', highlightIdx: 0 }
            ]
        },
        {
            letter: 'Z', soundSpell: 'zzz', cue: 'Z says zzz!',
            words: [
                { w: 'Zebra', e: '🦓', phoneme: 'zzz', highlightIdx: 0 },
                { w: 'Zoo', e: '🦒', phoneme: 'zzz', highlightIdx: 0 },
                { w: 'Zipper', e: '🧥', phoneme: 'zzz', highlightIdx: 0 }
            ]
        }
    ],

    numbers: [
        { num: 1, word: 'One', emoji: '☀️', item: 'Sun' },
        { num: 2, word: 'Two', emoji: '👟', item: 'Shoes' },
        { num: 3, word: 'Three', emoji: '🍎', item: 'Apples' },
        { num: 4, word: 'Four', emoji: '🚗', item: 'Cars' },
        { num: 5, word: 'Five', emoji: '⭐', item: 'Stars' },
        { num: 6, word: 'Six', emoji: '🎈', item: 'Balloons' },
        { num: 7, word: 'Seven', emoji: '🍓', item: 'Strawberries' },
        { num: 8, word: 'Eight', emoji: '🐟', item: 'Fish' },
        { num: 9, word: 'Nine', emoji: '🦋', item: 'Butterflies' },
        { num: 10, word: 'Ten', emoji: '🦖', item: 'Dinosaurs' },
        { num: 11, word: 'Eleven', emoji: '🦆', item: 'Ducks' },
        { num: 12, word: 'Twelve', emoji: '🍪', item: 'Cookies' },
        { num: 13, word: 'Thirteen', emoji: '🐞', item: 'Ladybugs' },
        { num: 14, word: 'Fourteen', emoji: '⛵', item: 'Sailboats' },
        { num: 15, word: 'Fifteen', emoji: '🍇', item: 'Grapes' },
        { num: 16, word: 'Sixteen', emoji: '🎵', item: 'Music Notes' },
        { num: 17, word: 'Seventeen', emoji: '✏️', item: 'Pencils' },
        { num: 18, word: 'Eighteen', emoji: '🌸', item: 'Flowers' },
        { num: 19, word: 'Nineteen', emoji: '🐝', item: 'Bumblebees' },
        { num: 20, word: 'Twenty', emoji: '🌟', item: 'Gold Stars' }
    ],

    shapes: [
        { id: 'Circle', real: '🍕 Pizza • ⏰ Clock • 🛞 Wheel', svg: '<circle cx="50" cy="50" r="42" fill="#8b5cf6" stroke="#6d28d9" stroke-width="4"/>' },
        { id: 'Square', real: '🪟 Window • 🎁 Box • 🖼️ Frame', svg: '<rect x="12" y="12" width="76" height="76" rx="8" fill="#ef4444" stroke="#b91c1c" stroke-width="4"/>' },
        { id: 'Triangle', real: '🍕 Pizza Slice • ⛺ Tent • ⛰️ Mountain', svg: '<polygon points="50,10 90,86 10,86" fill="#10b981" stroke="#047857" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Rectangle', real: '🚪 Door • 📱 Phone • 📖 Book', svg: '<rect x="8" y="24" width="84" height="52" rx="8" fill="#3b82f6" stroke="#1d4ed8" stroke-width="4"/>' },
        { id: 'Star', real: '⭐ Night Star • 🌟 Sheriff Badge', svg: '<polygon points="50,6 60.6,35.4 91.8,36.4 67.1,55.6 75.9,85.6 50,68 24.1,85.6 32.9,55.6 8.2,36.4 39.4,35.4" fill="#f59e0b" stroke="#b45309" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Heart', real: '❤️ Love • 🍓 Strawberry Shape', svg: '<path d="M 50 86 C 42 78, 10 56, 10 33 C 10 17, 23 10, 35 10 C 43 10, 48 15, 50 22 C 52 15, 57 10, 65 10 C 77 10, 90 17, 90 33 C 90 56, 58 78, 50 86 Z" fill="#ec4899" stroke="#be185d" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Oval', real: '🥚 Egg • 🍉 Watermelon • 🎈 Balloon', svg: '<ellipse cx="50" cy="50" rx="44" ry="29" fill="#06b6d4" stroke="#0e7490" stroke-width="4"/>' },
        { id: 'Diamond', real: '🪁 Kite • ♦️ Diamond Gem', svg: '<polygon points="50,8 86,50 50,92 14,50" fill="#14b8a6" stroke="#0f766e" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Pentagon', real: '🏠 House Shape • ⚽ Soccer Patch', svg: '<polygon points="50,10 89.9,39 74.7,86 25.3,86 10.1,39" fill="#f97316" stroke="#c2410c" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Hexagon', real: '🐝 Honeycomb • 🔩 Nut Bolt', svg: '<polygon points="50,8 86.4,29 86.4,71 50,92 13.6,71 13.6,29" fill="#6366f1" stroke="#4338ca" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Octagon', real: '🛑 Stop Sign', svg: '<polygon points="32.6,8 67.4,8 92,32.6 92,67.4 67.4,92 32.6,92 8,67.4 8,32.6" fill="#dc2626" stroke="#991b1b" stroke-width="4" stroke-linejoin="round"/>' },
        { id: 'Crescent', real: '🌙 Crescent Moon • 🍌 Banana', svg: '<path d="M 62 12 A 40 40 0 1 0 62 88 A 32 32 0 1 1 62 12 Z" fill="#eab308" stroke="#a16207" stroke-width="4" stroke-linejoin="round"/>' }
    ],

    shapes3d: [
        {
            id: 'Cube', color: '#ef4444', emoji: '🧊',
            real: '6 flat square faces — like a gift box or dice!',
            examples: [
                { id: 'pure', label: 'Cube', emoji: '🟥' },
                { id: 'gift', label: 'Gift Box', emoji: '🎁' },
                { id: 'dice', label: 'Dice', emoji: '🎲' }
            ]
        },
        {
            id: 'Sphere', color: '#3b82f6', emoji: '⚽',
            real: 'Perfectly round like a ball or planet!',
            examples: [
                { id: 'pure', label: 'Sphere', emoji: '🔵' },
                { id: 'earth', label: 'Earth', emoji: '🌍' },
                { id: 'snowman', label: 'Snowman', emoji: '⛄' }
            ]
        },
        {
            id: 'Cone', color: '#10b981', emoji: '🚧',
            real: 'Circle base with a pointy top!',
            examples: [
                { id: 'pure', label: 'Cone', emoji: '🔺' },
                { id: 'trafficcone', label: 'Traffic Cone', emoji: '🚧' },
                { id: 'partyhat', label: 'Party Hat', emoji: '🎉' }
            ]
        },
        {
            id: 'Cylinder', color: '#f59e0b', emoji: '🥁',
            real: 'Flat circles on top and bottom!',
            examples: [
                { id: 'pure', label: 'Cylinder', emoji: '🛢️' },
                { id: 'drum', label: 'Toy Drum', emoji: '🥁' },
                { id: 'cake', label: 'Birthday Cake', emoji: '🎂' }
            ]
        },
        {
            id: 'Donut (Torus)', color: '#ec4899', emoji: '🍩',
            real: 'A ring shape with a hole in the middle!',
            examples: [
                { id: 'pure', label: 'Torus', emoji: '⭕' },
                { id: 'donut', label: 'Donut', emoji: '🍩' },
                { id: 'lifering', label: 'Swim Ring', emoji: '🛟' }
            ]
        },
        {
            id: 'Pyramid', color: '#f97316', emoji: '🏜️',
            real: 'Triangle sides meeting at a pointy peak!',
            examples: [
                { id: 'pure', label: 'Pyramid', emoji: '🔺' },
                { id: 'egypt', label: 'Desert Pyramid', emoji: '🏜️' },
                { id: 'tree', label: 'Pine Tree', emoji: '🌲' }
            ]
        },
        {
            id: 'Cuboid (Box)', color: '#8b5cf6', emoji: '🧃',
            real: 'A rectangular box shape!',
            examples: [
                { id: 'pure', label: 'Cuboid', emoji: '🟪' },
                { id: 'juice', label: 'Juice Box', emoji: '🧃' },
                { id: 'bus', label: 'Toy Bus', emoji: '🚌' }
            ]
        },
        {
            id: 'Prism', color: '#14b8a6', emoji: '⛺',
            real: 'Triangle ends with flat rectangle sides!',
            examples: [
                { id: 'pure', label: 'Prism', emoji: '📐' },
                { id: 'tent', label: 'Camping Tent', emoji: '⛺' },
                { id: 'cheese', label: 'Cheese Wedge', emoji: '🧀' }
            ]
        },
        {
            id: 'Diamond (Octahedron)', color: '#06b6d4', emoji: '💎',
            real: '8 triangle faces like a sparkling crystal!',
            examples: [
                { id: 'pure', label: 'Octahedron', emoji: '🔷' },
                { id: 'gem', label: 'Shiny Gem', emoji: '💎' }
            ]
        },
        {
            id: 'Dome (Hemisphere)', color: '#eab308', emoji: '🛖',
            real: 'Half of a sphere with a flat bottom!',
            examples: [
                { id: 'pure', label: 'Dome', emoji: '🟡' },
                { id: 'igloo', label: 'Snow Igloo', emoji: '🛖' },
                { id: 'mushroom', label: 'Mushroom', emoji: '🍄' }
            ]
        }
    ],

    colors: [
        { id: 'Red', hex: '#ef4444', text: '#ffffff', examples: ['🍎', '🚒', '🍓'] },
        { id: 'Blue', hex: '#3b82f6', text: '#ffffff', examples: ['🐳', '🫐', '🚙'] },
        { id: 'Yellow', hex: '#facc15', text: '#1e293b', examples: ['☀️', '🍌', '🐥'] },
        { id: 'Green', hex: '#22c55e', text: '#ffffff', examples: ['🐸', '🥦', '🌳'] },
        { id: 'Orange', hex: '#f97316', text: '#ffffff', examples: ['🍊', '🥕', '🐯'] },
        { id: 'Purple', hex: '#a855f7', text: '#ffffff', examples: ['🍇', '🍆', '🦄'] },
        { id: 'Pink', hex: '#ec4899', text: '#ffffff', examples: ['🦩', '🐷', '🌸'] },
        { id: 'Brown', hex: '#78350f', text: '#ffffff', examples: ['🐻', '🍪', '🥔'] },
        { id: 'Black', hex: '#1e293b', text: '#ffffff', examples: ['🐧', '🕷️', '🎩'] },
        { id: 'White', hex: '#ffffff', text: '#1e293b', examples: ['⛄', '🐑', '☁️'] }
    ],

    animals: [
        { id: 'Lion', emoji: '🦁', sound: 'Roar!', speech: 'Lion! Roar!' },
        { id: 'Dog', emoji: '🐶', sound: 'Woof woof!', speech: 'Dog! Woof woof!' },
        { id: 'Cat', emoji: '🐱', sound: 'Meow!', speech: 'Cat! Meow!' },
        { id: 'Cow', emoji: '🐮', sound: 'Moooo!', speech: 'Cow! Moooo!' },
        { id: 'Duck', emoji: '🦆', sound: 'Quack quack!', speech: 'Duck! Quack quack!' },
        { id: 'Pig', emoji: '🐷', sound: 'Oink oink!', speech: 'Pig! Oink oink!' },
        { id: 'Sheep', emoji: '🐑', sound: 'Baaaa!', speech: 'Sheep! Baaaa!' },
        { id: 'Horse', emoji: '🐎', sound: 'Neigh!', speech: 'Horse! Neigh!' },
        { id: 'Elephant', emoji: '🐘', sound: 'Pawoo!', speech: 'Elephant! Big trunk!' },
        { id: 'Monkey', emoji: '🐵', sound: 'Ooh ooh aah aah!', speech: 'Monkey! Ooh ooh aah aah!' },
        { id: 'Frog', emoji: '🐸', sound: 'Ribbit ribbit!', speech: 'Frog! Ribbit!' },
        { id: 'Owl', emoji: '🦉', sound: 'Hoo hoo!', speech: 'Owl! Hoo hoo!' },
        { id: 'Bee', emoji: '🐝', sound: 'Bzzzzz!', speech: 'Bee! Bzzzz!' },
        { id: 'Snake', emoji: '🐍', sound: 'Hsssss!', speech: 'Snake! Sssss!' },
        { id: 'Dinosaur', emoji: '🦖', sound: 'Stomp! Roar!', speech: 'T-Rex Dinosaur! Roar!' },
        { id: 'Bear', emoji: '🐻', sound: 'Grrrr!', speech: 'Bear! Grrrr!' },
        { id: 'Penguin', emoji: '🐧', sound: 'Waddle waddle!', speech: 'Penguin! Likes the snow!' },
        { id: 'Whale', emoji: '🐳', sound: 'Splash!', speech: 'Whale! Swims in the ocean!' }
    ],

    fruits: [
        { id: 'Strawberry', emoji: '🍓', desc: 'Sweet Red Berry!', crumbColor: '#ef4444', innerColor: '#fecdd3' },
        { id: 'Apple', emoji: '🍎', desc: 'Crunchy Red Apple!', crumbColor: '#dc2626', innerColor: '#fef3c7' },
        { id: 'Banana', emoji: '🍌', desc: 'Sweet Yellow Banana!', crumbColor: '#facc15', innerColor: '#fef9c3' },
        { id: 'Watermelon', emoji: '🍉', desc: 'Juicy Green & Red Melon!', crumbColor: '#f43f5e', innerColor: '#fda4af' },
        { id: 'Grapes', emoji: '🍇', desc: 'Juicy Purple Grapes!', crumbColor: '#9333ea', innerColor: '#e9d5ff' },
        { id: 'Orange', emoji: '🍊', desc: 'Juicy Vitamin C Orange!', crumbColor: '#f97316', innerColor: '#ffedd5' },
        { id: 'Blueberries', emoji: '🫐', desc: 'Sweet Little Blueberries!', crumbColor: '#2563eb', innerColor: '#dbeafe' },
        { id: 'Broccoli', emoji: '🥦', desc: 'Crunchy Green Broccoli!', crumbColor: '#16a34a', innerColor: '#dcfce7' },
        { id: 'Carrot', emoji: '🥕', desc: 'Crunchy Orange Carrot!', crumbColor: '#ea580c', innerColor: '#ffedd5' },
        { id: 'Avocado', emoji: '🥑', desc: 'Creamy Green Avocado!', crumbColor: '#65a30d', innerColor: '#ecfccb' },
        { id: 'Corn', emoji: '🌽', desc: 'Sweet Yellow Corn!', crumbColor: '#eab308', innerColor: '#fef08a' },
        { id: 'Cheese', emoji: '🧀', desc: 'Yummy Cheddar Cheese!', crumbColor: '#f59e0b', innerColor: '#fde68a' },
        { id: 'Cookie', emoji: '🍪', desc: 'Chocolate Chip Cookie!', crumbColor: '#b45309', innerColor: '#fde68a' },
        { id: 'Pizza', emoji: '🍕', desc: 'Warm Cheesy Pizza Slice!', crumbColor: '#ef4444', innerColor: '#fef08a' }
    ],

    things: [
        { id: 'Fire Truck', emoji: '🚒', sound: 'Weee-oooo! Weee-oooo!', speech: 'Fire truck! Wee-ooo wee-ooo!' },
        { id: 'Police Car', emoji: '🚓', sound: 'Woo-woo-woo!', speech: 'Police car! Woo-woo-woo!' },
        { id: 'Train', emoji: '🚂', sound: 'Choo choo!', speech: 'Train! Choo-choo!' },
        { id: 'Rocket Ship', emoji: '🚀', sound: 'Blast off! Whooosh!', speech: 'Rocket ship! Blast off!' },
        { id: 'Airplane', emoji: '✈️', sound: 'Zoom! In the sky!', speech: 'Airplane! Flying high!' },
        { id: 'Helicopter', emoji: '🚁', sound: 'Chop-chop-chop!', speech: 'Helicopter! Chop-chop-chop!' },
        { id: 'Tractor', emoji: '🚜', sound: 'Chug-chug-chug!', speech: 'Tractor! On the farm!' },
        { id: 'School Bus', emoji: '🚌', sound: 'Honk honk! Beep beep!', speech: 'School bus! Beep beep!' },
        { id: 'Sailboat', emoji: '⛵', sound: 'Splish splash!', speech: 'Sailboat! Sailing on the waves!' },
        { id: 'Bicycle', emoji: '🚲', sound: 'Ring ring!', speech: 'Bicycle! Ring-ring!' },
        { id: 'Soccer Ball', emoji: '⚽', sound: 'Kick! Goal!', speech: 'Soccer ball! Goal!' },
        { id: 'Guitar', emoji: '🎸', sound: 'Strum strum!', speech: 'Guitar! Strum strum!' },
        { id: 'Drum', emoji: '🥁', sound: 'Rat-a-tat-tat!', speech: 'Drum! Bang bang bang!' },
        { id: 'Clock', emoji: '⏰', sound: 'Tick-tock tick-tock!', speech: 'Clock! Tick-tock!' }
    ],

    opposites: [
        {
            title: 'Big vs. Small',
            a: { label: 'Big', emoji: '🐘', scale: 'text-8xl sm:text-9xl' },
            b: { label: 'Small', emoji: '🐁', scale: 'text-4xl sm:text-5xl' }
        },
        {
            title: 'Hot vs. Cold',
            a: { label: 'Hot', emoji: '🔥', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Cold', emoji: '🧊', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Happy vs. Sad',
            a: { label: 'Happy', emoji: '😄', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Sad', emoji: '😢', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Fast vs. Slow',
            a: { label: 'Fast', emoji: '🐆', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Slow', emoji: '🐢', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Day vs. Night',
            a: { label: 'Day', emoji: '☀️', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Night', emoji: '🌙', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Up vs. Down',
            a: { label: 'Up', emoji: '🎈', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Down', emoji: '⚓', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Clean vs. Dirty',
            a: { label: 'Clean', emoji: '✨', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Dirty', emoji: '🧦', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Loud vs. Quiet',
            a: { label: 'Loud', emoji: '📢', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Quiet', emoji: '🤫', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Open vs. Closed',
            a: { label: 'Open', emoji: '📖', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Closed', emoji: '📕', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Heavy vs. Light',
            a: { label: 'Heavy', emoji: '🪨', scale: 'text-8xl sm:text-9xl' },
            b: { label: 'Light', emoji: '🪶', scale: 'text-5xl sm:text-6xl' }
        },
        {
            title: 'Tall vs. Short',
            a: { label: 'Tall', emoji: '🦒', scale: 'text-8xl sm:text-9xl' },
            b: { label: 'Short', emoji: '🐶', scale: 'text-5xl sm:text-6xl' }
        },
        {
            title: 'Full vs. Empty',
            a: { label: 'Full', emoji: '🥛', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Empty', emoji: '🫙', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Wet vs. Dry',
            a: { label: 'Wet', emoji: '☔', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Dry', emoji: '🌵', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Awake vs. Asleep',
            a: { label: 'Awake', emoji: '🤩', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Asleep', emoji: '😴', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Hard vs. Soft',
            a: { label: 'Hard', emoji: '💎', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Soft', emoji: '🧸', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Inside vs. Outside',
            a: { label: 'Inside', emoji: '🏠', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Outside', emoji: '🌳', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'Many vs. Few',
            a: { label: 'Many', emoji: '🐝🐝', scale: 'text-5xl sm:text-6xl' },
            b: { label: 'Few', emoji: '🐝', scale: 'text-5xl sm:text-6xl' }
        },
        {
            title: 'Long vs. Short',
            a: { label: 'Long', emoji: '🐍', scale: 'text-8xl sm:text-9xl' },
            b: { label: 'Short', emoji: '🐛', scale: 'text-4xl sm:text-5xl' }
        },
        {
            title: 'Sweet vs. Sour',
            a: { label: 'Sweet', emoji: '🧁', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Sour', emoji: '🍋', scale: 'text-7xl sm:text-8xl' }
        },
        {
            title: 'On vs. Off',
            a: { label: 'On', emoji: '💡', scale: 'text-7xl sm:text-8xl' },
            b: { label: 'Off', emoji: '🌑', scale: 'text-7xl sm:text-8xl' }
        }
    ],

    solar: [
        {
            id: 'The Sun', short: 'Sun', emoji: '☀️', color: '#facc15',
            badge: '⭐ Giant Star • Center',
            fact: 'Our giant, glowing star! It keeps Earth warm and bright!',
            credit: '🔭 NASA Solar Dynamics Observatory',
            photoUrl: 'https://images-assets.nasa.gov/image/GSFC_20171208_Archive_e001435/GSFC_20171208_Archive_e001435~medium.jpg',
            orbitRadius: 0, orbitSpeed: 0, orbitSize: 1.8,
            speech: 'The Sun! Our giant glowing star that gives light and warmth to everything in our solar system!'
        },
        {
            id: 'Mercury', short: 'Merc', emoji: '🪨', color: '#94a3b8',
            badge: '1st Planet • Rocky',
            fact: 'The closest planet to the Sun! It is covered in rocky craters!',
            credit: '🔭 NASA MESSENGER Spacecraft',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA16853/PIA16853~small.jpg',
            orbitRadius: 1.15, orbitSpeed: 0.042, orbitSize: 0.28,
            speech: 'Mercury! The speedy first planet closest to the Sun!'
        },
        {
            id: 'Venus', short: 'Venus', emoji: '🟡', color: '#fbbf24',
            badge: '2nd Planet • Golden',
            fact: 'The hottest planet! It is covered in thick golden clouds!',
            credit: '🔭 NASA Magellan Radar View',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA00271/PIA00271~medium.jpg',
            orbitRadius: 1.6, orbitSpeed: 0.032, orbitSize: 0.38,
            speech: 'Venus! The hottest planet with thick golden swirling clouds!'
        },
        {
            id: 'Earth', short: 'Earth', emoji: '🌍', color: '#3b82f6',
            badge: '3rd Planet • Our Home',
            fact: 'Our beautiful blue home! It has green land, blue oceans, and life!',
            credit: '🔭 NASA Apollo Blue Marble',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA18033/PIA18033~medium.jpg',
            orbitRadius: 2.1, orbitSpeed: 0.024, orbitSize: 0.42,
            speech: 'Earth! Our wonderful home planet with blue oceans, green trees, and you!'
        },
        {
            id: "Earth's Moon", short: 'Moon', emoji: '🌙', color: '#e2e8f0',
            badge: 'Earth Satellite',
            fact: 'Our friendly Moon! It circles Earth and lights up our night sky!',
            credit: '🔭 NASA Lunar Reconnaissance Orbiter',
            photoUrl: 'https://images-assets.nasa.gov/image/GSFC_20171208_Archive_e001982/GSFC_20171208_Archive_e001982~small.jpg',
            orbitRadius: 2.3, orbitSpeed: 0.05, orbitSize: 0.22,
            speech: "The Moon! Earth's best friend that glows at night!"
        },
        {
            id: 'Mars', short: 'Mars', emoji: '🔴', color: '#ef4444',
            badge: '4th Planet • Red Planet',
            fact: 'The Red Planet! It has giant volcanoes, deep canyons, and polar ice!',
            credit: '🔭 NASA Hubble Space Telescope',
            photoUrl: 'https://images-assets.nasa.gov/image/GSFC_20171208_Archive_e000332/GSFC_20171208_Archive_e000332~medium.jpg',
            orbitRadius: 2.65, orbitSpeed: 0.018, orbitSize: 0.32,
            speech: 'Mars! The dusty red planet where robot rovers explore!'
        },
        {
            id: 'Asteroid Belt', short: 'Asteroids', emoji: '🪨', color: '#78716c',
            badge: 'Rocky Belt',
            fact: 'Millions of tumbling space rocks between Mars and Jupiter!',
            credit: '🔭 NASA Dawn Mission (Vesta)',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA15678/PIA15678~small.jpg',
            orbitRadius: 3.05, orbitSpeed: 0.014, orbitSize: 0.26,
            speech: 'The Asteroid Belt! A giant ring of tumbling space rocks orbiting between Mars and Jupiter!'
        },
        {
            id: 'Jupiter', short: 'Jupiter', emoji: '🪐', color: '#f97316',
            badge: '5th Planet • Giant',
            fact: 'The biggest planet of all! It has colorful stripes and the Great Red Spot storm!',
            credit: '🔭 NASA Juno Spacecraft',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA22946/PIA22946~medium.jpg',
            orbitRadius: 3.55, orbitSpeed: 0.011, orbitSize: 0.72,
            speech: 'Jupiter! The giant king of planets with a huge swirling storm!'
        },
        {
            id: 'Saturn', short: 'Saturn', emoji: '🪐', color: '#eab308',
            badge: '6th Planet • Ringed',
            fact: 'The jewel of the solar system! It wears magnificent glowing rings!',
            credit: '🔭 NASA Cassini Spacecraft',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA06193/PIA06193~medium.jpg',
            orbitRadius: 4.15, orbitSpeed: 0.008, orbitSize: 0.62,
            speech: 'Saturn! The beautiful planet with dazzling rings of ice and rock!'
        },
        {
            id: 'Uranus', short: 'Uranus', emoji: '🩵', color: '#38bdf8',
            badge: '7th Planet • Ice Giant',
            fact: 'The sideways ice giant! It rolls on its side like a ball with vertical rings!',
            credit: '🔭 NASA Voyager 2 / Hubble',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA18182/PIA18182~medium.jpg',
            orbitRadius: 4.75, orbitSpeed: 0.006, orbitSize: 0.48,
            speech: 'Uranus! The chilly cyan ice giant that spins completely on its side!'
        },
        {
            id: 'Neptune', short: 'Neptune', emoji: '🔵', color: '#2563eb',
            badge: '8th Planet • Deep Blue',
            fact: 'The windiest planet! A deep cobalt blue world far away in the dark!',
            credit: '🔭 NASA Voyager 2',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA01492/PIA01492~medium.jpg',
            orbitRadius: 5.35, orbitSpeed: 0.0045, orbitSize: 0.46,
            speech: 'Neptune! The deep blue planet with the fastest winds in the solar system!'
        },
        {
            id: 'Pluto', short: 'Pluto', emoji: '🤎', color: '#fed7aa',
            badge: 'Dwarf Planet • Kuiper Belt',
            fact: 'The beloved dwarf planet! It has a giant bright heart of frozen nitrogen!',
            credit: '🔭 NASA New Horizons',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA19952/PIA19952~medium.jpg',
            orbitRadius: 5.95, orbitSpeed: 0.0035, orbitSize: 0.24,
            speech: 'Pluto! The chilly dwarf planet with a giant heart on its surface!'
        },
        {
            id: 'Comet', short: 'Comet', emoji: '☄️', color: '#a5f3fc',
            badge: 'Icy Wanderer',
            fact: 'A cosmic dirty snowball with a glowing coma and dual streaming tails!',
            credit: '🔭 NASA Hubble Space Telescope',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA18153/PIA18153~small.jpg',
            orbitRadius: 3.8, orbitSpeed: 0.016, orbitSize: 0.26,
            speech: 'Comet! An icy space explorer with glowing tails speeding through space!'
        },
        {
            id: 'Galactic Swirl', short: 'Galaxy', emoji: '🌌', color: '#c084fc',
            badge: 'Spiral Galaxy',
            fact: 'A swirling cosmic spiral made of hundreds of billions of sparkling stars!',
            credit: '🔭 NASA Spitzer / GALEX',
            photoUrl: 'https://images-assets.nasa.gov/image/PIA07904/PIA07904~small.jpg',
            orbitRadius: 6.4, orbitSpeed: 0.002, orbitSize: 0.85,
            speech: 'Galactic Swirl! Hundreds of billions of glittering stars dancing in a spiral!'
        }
    ]
};


// scratch/audio_tts.js

// Canvas automatically injects runtime API key here when loaded in Gemini Canvas
const apiKey = "";

const getApiKey = () => {
    return localStorage.getItem('tlh_isolated_v3_api_key') ||
           localStorage.getItem('toddler_gemini_api_key') ||
           apiKey || "";
};

const getTtsModel = () => {
    return localStorage.getItem('tlh_isolated_v3_tts_model') ||
           localStorage.getItem('toddler_gemini_tts_model') ||
           'gemini-3.8-flash-tts';
};

const getTtsVoice = () => {
    return localStorage.getItem('tlh_isolated_v3_tts_voice') ||
           localStorage.getItem('toddler_gemini_tts_voice') ||
           'Kore';
};

// Strips emojis so TTS and Web Speech don't vocalize raw emoji names
function cleanSpokenText(str) {
    if (!str) return '';
    return str
        .replace(/[\u{1F300}-\u{1F9FF}\u{2600}-\u{26FF}\u{2700}-\u{27BF}\u{1F1E0}-\u{1F1FF}\u{1F600}-\u{1F64F}\u{1F680}-\u{1F6FF}]/gu, '')
        .replace(/\s+/g, ' ')
        .trim();
}

// IndexedDB Cache for Gemini TTS Audio (isolated with tlh_isolated_v3_ prefix)
const ttsDB = {
    db: null,
    async init() {
        if (this.db) return this.db;
        return new Promise((resolve) => {
            try {
                const req = indexedDB.open('tlh_isolated_v3_tts_db', 1);
                req.onupgradeneeded = (e) => {
                    const db = e.target.result;
                    if (!db.objectStoreNames.contains('audio_cache')) {
                        db.createObjectStore('audio_cache');
                    }
                };
                req.onsuccess = (e) => {
                    this.db = e.target.result;
                    resolve(this.db);
                };
                req.onerror = () => resolve(null);
            } catch (err) {
                resolve(null);
            }
        });
    },
    async get(key) {
        const db = await this.init();
        if (!db) return null;
        return new Promise((resolve) => {
            try {
                const tx = db.transaction('audio_cache', 'readonly');
                const store = tx.objectStore('audio_cache');
                const req = store.get(key);
                req.onsuccess = () => resolve(req.result || null);
                req.onerror = () => resolve(null);
            } catch (err) {
                resolve(null);
            }
        });
    },
    async set(key, arrayBuffer) {
        const db = await this.init();
        if (!db) return;
        try {
            const tx = db.transaction('audio_cache', 'readwrite');
            const store = tx.objectStore('audio_cache');
            store.put(arrayBuffer, key);
        } catch (err) {}
    }
};

// Raw PCM to WAV Converter (handles 24kHz 16-bit mono PCM if RIFF header is absent)
function pcmToWav(pcmData, sampleRate = 24000, numChannels = 1, bitDepth = 16) {
    if (pcmData.length >= 4 &&
        pcmData[0] === 0x52 && pcmData[1] === 0x49 && pcmData[2] === 0x46 && pcmData[3] === 0x46) {
        return pcmData.buffer;
    }
    const dataLen = pcmData.byteLength;
    const buffer = new ArrayBuffer(44 + dataLen);
    const view = new DataView(buffer);
    // RIFF chunk descriptor
    view.setUint32(0, 0x52494646, false); // "RIFF"
    view.setUint32(4, 36 + dataLen, true);
    view.setUint32(8, 0x57415645, false); // "WAVE"
    // fmt sub-chunk
    view.setUint32(12, 0x666d7420, false); // "fmt "
    view.setUint32(16, 16, true);          // 16 for PCM
    view.setUint16(20, 1, true);           // PCM format = 1
    view.setUint16(22, numChannels, true);
    view.setUint32(24, sampleRate, true);
    view.setUint32(28, sampleRate * numChannels * (bitDepth / 8), true); // byte rate
    view.setUint16(32, numChannels * (bitDepth / 8), true);              // block align
    view.setUint16(34, bitDepth, true);                                  // bits per sample
    // data sub-chunk
    view.setUint32(36, 0x64617461, false); // "data"
    view.setUint32(40, dataLen, true);
    new Uint8Array(buffer, 44).set(pcmData);
    return buffer;
}

const geminiTTS = {
    memCache: new Map(),
    activeSource: null,
    activeAudioEl: null,
    abortCtrl: null,
    workingStrategy: null,
    playReqId: 0,

    stop() {
        this.playReqId++;
        if (this.abortCtrl) {
            try { this.abortCtrl.abort(); } catch(e) {}
            this.abortCtrl = null;
        }
        if (this.activeSource) {
            try { this.activeSource.stop(); } catch (e) {}
            try { this.activeSource.disconnect(); } catch (e) {}
            this.activeSource = null;
        }
        if (this.activeAudioEl) {
            try {
                this.activeAudioEl.pause();
                this.activeAudioEl.src = '';
            } catch (e) {}
            this.activeAudioEl = null;
        }
        if (typeof app !== 'undefined' && app.setSpeakingUI) {
            app.setSpeakingUI(false);
        }
    },

    async fetchAudio(text, model = getTtsModel(), voice = getTtsVoice(), customKey = null) {
        const key = customKey || getApiKey();
        if (!key) throw new Error("No API key available");
        const cleanText = cleanSpokenText(text);
        if (!cleanText) return null;

        const cacheKey = `${model}:${voice}:${cleanText}`;

        // 1. Check memory cache
        if (this.memCache.has(cacheKey)) {
            return this.memCache.get(cacheKey);
        }

        // 2. Check IndexedDB cache
        const dbCached = await ttsDB.get(cacheKey);
        if (dbCached) {
            this.memCache.set(cacheKey, dbCached);
            return dbCached;
        }

        // 3. Multi-schema fallback chain for Gemini TTS (strictly verbatim text!)
        const strategies = [
            {
                id: 'gemini38-styled',
                model: model,
                body: {
                    contents: [{
                        role: "user",
                        parts: [{
                            text: cleanText,
                            speech_metadata: {
                                style: "warm, cheerful, expressive early-childhood educator speaking clearly and naturally to an advanced two-year-old toddler"
                            }
                        }]
                    }],
                    generationConfig: {
                        responseModalities: ["AUDIO"],
                        speechConfig: {
                            voiceConfig: {
                                voice: voice
                            }
                        }
                    }
                }
            },
            {
                id: 'gemini38-prebuilt',
                model: model,
                body: {
                    contents: [{
                        role: "user",
                        parts: [{ text: cleanText }]
                    }],
                    generationConfig: {
                        responseModalities: ["AUDIO"],
                        speechConfig: {
                            voiceConfig: {
                                prebuiltVoiceConfig: {
                                    voiceName: voice
                                }
                            }
                        }
                    }
                }
            },
            {
                id: 'gemini25-fallback',
                model: 'gemini-2.5-flash-preview-tts',
                body: {
                    contents: [{ parts: [{ text: cleanText }] }],
                    generationConfig: {
                        responseModalities: ["AUDIO"],
                        speechConfig: {
                            voiceConfig: {
                                prebuiltVoiceConfig: {
                                    voiceName: voice
                                }
                            }
                        }
                    }
                }
            }
        ];

        // Prioritize previously verified working strategy to minimize latency
        if (this.workingStrategy) {
            const idx = strategies.findIndex(s => s.id === this.workingStrategy);
            if (idx > 0) {
                const [ws] = strategies.splice(idx, 1);
                strategies.unshift(ws);
            }
        }

        let lastErr = null;
        for (const strat of strategies) {
            try {
                const ctrl = new AbortController();
                this.abortCtrl = ctrl;
                const url = `https://generativelanguage.googleapis.com/v1beta/models/${strat.model}:generateContent?key=${encodeURIComponent(key)}`;
                const resp = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(strat.body),
                    signal: ctrl.signal
                });

                if (!resp.ok) {
                    const errData = await resp.json().catch(() => ({}));
                    throw new Error(errData?.error?.message || `HTTP ${resp.status}`);
                }

                const data = await resp.json();
                const base64Data = data?.candidates?.[0]?.content?.parts?.[0]?.inlineData?.data;
                if (!base64Data) throw new Error("No audio payload returned from Gemini TTS");

                const binaryStr = atob(base64Data);
                const pcmBytes = new Uint8Array(binaryStr.length);
                for (let i = 0; i < binaryStr.length; i++) {
                    pcmBytes[i] = binaryStr.charCodeAt(i);
                }

                const wavBuffer = pcmToWav(pcmBytes, 24000, 1, 16);
                this.workingStrategy = strat.id;

                // Cache in memory and IndexedDB
                this.memCache.set(cacheKey, wavBuffer);
                await ttsDB.set(cacheKey, wavBuffer);
                return wavBuffer;
            } catch (err) {
                lastErr = err;
                if (err.name === 'AbortError') throw err;
            }
        }

        throw lastErr || new Error("All Gemini TTS strategies failed");
    },

    async play(text, model = getTtsModel(), voice = getTtsVoice(), customKey = null) {
        this.stop();
        const myReqId = ++this.playReqId;
        soundFX.init();
        if (!soundFX.ctx) throw new Error("WebAudio context not initialized");

        if (typeof app !== 'undefined' && app.setSpeakingUI) {
            app.setSpeakingUI(true);
        }

        try {
            const wavBuf = await this.fetchAudio(text, model, voice, customKey);
            if (!wavBuf || myReqId !== this.playReqId) {
                if (myReqId === this.playReqId && typeof app !== 'undefined' && app.setSpeakingUI) app.setSpeakingUI(false);
                return;
            }

            if (soundFX.ctx.state !== 'running') {
                try { await soundFX.ctx.resume(); } catch (e) {}
            }

            try {
                const audioBuf = await soundFX.ctx.decodeAudioData(wavBuf.slice(0));
                if (myReqId !== this.playReqId) return;

                const src = soundFX.ctx.createBufferSource();
                src.buffer = audioBuf;
                if (typeof app !== 'undefined' && app.getSpeechRateValue) {
                    src.playbackRate.value = app.getSpeechRateValue();
                }
                const gain = soundFX.ctx.createGain();
                gain.gain.setValueAtTime(1.0, soundFX.ctx.currentTime);
                src.connect(gain);
                gain.connect(soundFX.ctx.destination);

                src.onended = () => {
                    if (this.activeSource === src) {
                        this.activeSource = null;
                        if (typeof app !== 'undefined' && app.setSpeakingUI) app.setSpeakingUI(false);
                    }
                };

                src.start(0);
                this.activeSource = src;
            } catch (decodeErr) {
                // Fallback to HTMLAudioElement with WAV Blob
                if (myReqId !== this.playReqId) return;
                const blob = new Blob([wavBuf.slice(0)], { type: 'audio/wav' });
                const blobUrl = URL.createObjectURL(blob);
                const audio = new Audio(blobUrl);
                if (typeof app !== 'undefined' && app.getSpeechRateValue) {
                    audio.playbackRate = app.getSpeechRateValue();
                }
                this.activeAudioEl = audio;
                audio.onended = () => {
                    URL.revokeObjectURL(blobUrl);
                    if (this.activeAudioEl === audio) {
                        this.activeAudioEl = null;
                        if (typeof app !== 'undefined' && app.setSpeakingUI) app.setSpeakingUI(false);
                    }
                };
                audio.onerror = () => {
                    URL.revokeObjectURL(blobUrl);
                    if (this.activeAudioEl === audio) {
                        this.activeAudioEl = null;
                        if (typeof app !== 'undefined' && app.setSpeakingUI) app.setSpeakingUI(false);
                    }
                };
                await audio.play();
            }
        } catch (e) {
            if (myReqId === this.playReqId && typeof app !== 'undefined' && app.setSpeakingUI) {
                app.setSpeakingUI(false);
            }
            if (e.name === 'AbortError') return;
            throw e;
        }
    }
};

const ANIMAL_SOUND_URLS = {
    Lion: 'https://www.google.com/logos/fnbx/animal_sounds/lion.mp3',
    Dog: 'https://www.google.com/logos/fnbx/animal_sounds/dog.mp3',
    Cat: 'https://www.google.com/logos/fnbx/animal_sounds/cat.mp3',
    Cow: 'https://www.google.com/logos/fnbx/animal_sounds/cow.mp3',
    Duck: 'https://www.google.com/logos/fnbx/animal_sounds/duck.mp3',
    Pig: 'https://www.google.com/logos/fnbx/animal_sounds/pig.mp3',
    Sheep: 'https://www.google.com/logos/fnbx/animal_sounds/sheep.mp3',
    Horse: 'https://www.google.com/logos/fnbx/animal_sounds/horse.mp3',
    Elephant: 'https://www.google.com/logos/fnbx/animal_sounds/elephant.mp3',
    Monkey: 'https://www.google.com/logos/fnbx/animal_sounds/ape.mp3',
    Frog: 'https://www.google.com/logos/fnbx/animal_sounds/frog.mp3',
    Owl: 'https://www.google.com/logos/fnbx/animal_sounds/owl.mp3',
    Bee: 'https://www.google.com/logos/fnbx/animal_sounds/bee.mp3',
    Snake: 'https://www.google.com/logos/fnbx/animal_sounds/rattlesnake.mp3',
    Dinosaur: 'https://www.google.com/logos/fnbx/animal_sounds/dinosaur.mp3',
    Bear: 'https://www.google.com/logos/fnbx/animal_sounds/tiger.mp3',
    Penguin: 'https://www.google.com/logos/fnbx/animal_sounds/penguin.mp3',
    Whale: 'https://www.google.com/logos/fnbx/animal_sounds/humpback-whale.mp3'
};

// Procedural Multi-layered WebAudio Sound Effects Engine (100% offline, zero .ogg network files)
const soundFX = {
    ctx: null,
    noiseBuf: null,
    activeNodes: new Set(),
    activeTimers: new Set(),
    animalBuffers: new Map(),
    activeAudioElements: new Set(),
    munchBuffer: null,

    init() {
        if (!this.ctx) {
            const AudioCtx = window.AudioContext || window.webkitAudioContext;
            if (AudioCtx) this.ctx = new AudioCtx();
        }
        if (this.ctx && this.ctx.state === 'suspended') {
            this.ctx.resume().catch(() => {});
        }
        if (this.ctx && !this.noiseBuf) {
            const sr = this.ctx.sampleRate;
            this.noiseBuf = this.ctx.createBuffer(1, sr * 2.0, sr);
            const data = this.noiseBuf.getChannelData(0);
            for (let i = 0; i < data.length; i++) data[i] = Math.random() * 2 - 1;
        }
        if (this.ctx && !this.munchBuffer) {
            this.buildMunchBuffer();
        }
        this.preloadAnimalSounds();
    },

    buildMunchBuffer() {
        if (!this.ctx) return;
        const sr = this.ctx.sampleRate;
        const totalSamples = Math.floor(sr * 0.52);
        const pcm = new Float32Array(totalSamples);
        const addGrains = (startTime, endTime, count, f1, f2, peakAmp) => {
            for (let i = 0; i < count; i++) {
                const grainStart = startTime + Math.random() * (endTime - startTime - 0.015);
                const grainDur = 0.003 + Math.random() * 0.007;
                const startIdx = Math.floor(grainStart * sr);
                const durSamples = Math.floor(grainDur * sr);
                for (let s = 0; s < durSamples; s++) {
                    const idx = startIdx + s;
                    if (idx >= totalSamples) break;
                    const t = s / sr;
                    const progress = s / durSamples;
                    const env = Math.exp(-progress * 6.0);
                    const noise = (Math.random() * 2 - 1);
                    const res = Math.sin(2 * Math.PI * f1 * t) * 0.6 + Math.sin(2 * Math.PI * f2 * t) * 0.4;
                    pcm[idx] += (noise * 0.6 + res * 0.4) * env * peakAmp;
                }
            }
        };
        addGrains(0.00, 0.15, 20, 1100, 3800, 0.45);
        addGrains(0.19, 0.32, 14, 850, 2600, 0.32);
        addGrains(0.36, 0.48, 10, 700, 2200, 0.24);

        let maxVal = 0;
        for (let i = 0; i < totalSamples; i++) {
            if (Math.abs(pcm[i]) > maxVal) maxVal = Math.abs(pcm[i]);
        }
        if (maxVal > 0) {
            for (let i = 0; i < totalSamples; i++) pcm[i] = (pcm[i] / maxVal) * 0.85;
        }
        const audioBuf = this.ctx.createBuffer(1, totalSamples, sr);
        audioBuf.getChannelData(0).set(pcm);
        this.munchBuffer = audioBuf;
    },

    preloadAnimalSounds() {
        if (!this.ctx) return;
        Object.entries(ANIMAL_SOUND_URLS).forEach(([id, url]) => {
            if (this.animalBuffers.has(id)) return;
            fetch(url)
                .then(r => r.arrayBuffer())
                .then(ab => this.ctx.decodeAudioData(ab))
                .then(dec => this.animalBuffers.set(id, dec))
                .catch(() => {});
        });
    },

    registerTimer(timerId) {
        this.activeTimers.add(timerId);
        return timerId;
    },

    clearTrackedTimer(timerId) {
        clearTimeout(timerId);
        this.activeTimers.delete(timerId);
    },

    trackNode(node) {
        this.activeNodes.add(node);
        const onEnd = () => {
            this.activeNodes.delete(node);
        };
        if (node.addEventListener) {
            node.addEventListener('ended', onEnd);
        } else {
            node.onended = onEnd;
        }
    },

    stopAll() {
        this.activeTimers.forEach(t => clearTimeout(t));
        this.activeTimers.clear();

        this.activeNodes.forEach(node => {
            try { node.stop(); } catch (e) {}
            try { node.disconnect(); } catch (e) {}
        });
        this.activeNodes.clear();

        this.activeAudioElements.forEach(audio => {
            try { audio.pause(); audio.src = ''; } catch (e) {}
        });
        this.activeAudioElements.clear();

        if (typeof animalGame !== 'undefined' && animalGame.speechTimer) {
            clearTimeout(animalGame.speechTimer);
            animalGame.speechTimer = null;
        }
        if (typeof thingsGame !== 'undefined' && thingsGame.speechTimer) {
            clearTimeout(thingsGame.speechTimer);
            thingsGame.speechTimer = null;
        }
    },

    playNote(freq = 440, duration = 0.14, type = 'sine', vol = 0.22, delay = 0) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx) return;
            const t = this.ctx.currentTime + delay;
            const osc = this.ctx.createOscillator();
            const gain = this.ctx.createGain();
            osc.type = type;
            osc.frequency.setValueAtTime(freq, t);
            gain.gain.setValueAtTime(0.001, t);
            gain.gain.linearRampToValueAtTime(vol, t + 0.015);
            gain.gain.exponentialRampToValueAtTime(0.001, t + duration);
            osc.connect(gain);
            gain.connect(this.ctx.destination);
            this.trackNode(osc);
            osc.start(t);
            osc.stop(t + duration + 0.03);
        } catch (e) {}
    },

    playSlide(fStart, fEnd, duration = 0.35, type = 'sawtooth', vol = 0.22, delay = 0, filterFreq = 1800) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx) return;
            const t = this.ctx.currentTime + delay;
            const osc = this.ctx.createOscillator();
            const filter = this.ctx.createBiquadFilter();
            const gain = this.ctx.createGain();
            osc.type = type;
            osc.frequency.setValueAtTime(Math.max(20, fStart), t);
            osc.frequency.exponentialRampToValueAtTime(Math.max(20, fEnd), t + duration);
            filter.type = 'lowpass';
            filter.frequency.setValueAtTime(filterFreq, t);
            gain.gain.setValueAtTime(0.001, t);
            gain.gain.linearRampToValueAtTime(vol, t + 0.02);
            gain.gain.exponentialRampToValueAtTime(0.001, t + duration);
            osc.connect(filter);
            filter.connect(gain);
            gain.connect(this.ctx.destination);
            this.trackNode(osc);
            osc.start(t);
            osc.stop(t + duration + 0.03);
        } catch (e) {}
    },

    playNoise(duration = 0.25, filterType = 'bandpass', freq = 1000, q = 2.0, vol = 0.25, delay = 0) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx || !this.noiseBuf) return;
            const t = this.ctx.currentTime + delay;
            const src = this.ctx.createBufferSource();
            src.buffer = this.noiseBuf;
            const filter = this.ctx.createBiquadFilter();
            filter.type = filterType;
            filter.frequency.setValueAtTime(freq, t);
            filter.Q.setValueAtTime(q, t);
            const gain = this.ctx.createGain();
            gain.gain.setValueAtTime(0.001, t);
            gain.gain.linearRampToValueAtTime(vol, t + 0.02);
            gain.gain.exponentialRampToValueAtTime(0.001, t + duration);
            src.connect(filter);
            filter.connect(gain);
            gain.connect(this.ctx.destination);
            this.trackNode(src);
            src.start(t);
            src.stop(t + duration + 0.03);
        } catch (e) {}
    },

    playCrunch() {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx || !this.munchBuffer) return;
            const now = this.ctx.currentTime;
            const src = this.ctx.createBufferSource();
            src.buffer = this.munchBuffer;
            const gain = this.ctx.createGain();
            gain.gain.setValueAtTime(0.9, now);
            src.connect(gain);
            gain.connect(this.ctx.destination);
            this.trackNode(src);
            src.start(now);
        } catch (e) {}
    },

    playBubblePop() {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx) return;
            const t0 = this.ctx.currentTime;
            const osc = this.ctx.createOscillator();
            const gain = this.ctx.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(380, t0);
            osc.frequency.exponentialRampToValueAtTime(1150, t0 + 0.065);
            gain.gain.setValueAtTime(0.32, t0);
            gain.gain.exponentialRampToValueAtTime(0.001, t0 + 0.075);
            osc.connect(gain);
            gain.connect(this.ctx.destination);
            this.trackNode(osc);
            osc.start(t0);
            osc.stop(t0 + 0.08);
        } catch (e) {}
    },

    playPop() {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        this.playBubblePop();
    },

    playCountStep(stepIndex) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        try {
            this.init();
            if (!this.ctx) return;
            const t0 = this.ctx.currentTime;
            const scale = [261.63, 293.66, 329.63, 392.00, 440.00, 523.25, 587.33, 659.25, 783.99, 880.00, 1046.50];
            const baseFreq = scale[(stepIndex - 1) % scale.length];

            const osc1 = this.ctx.createOscillator();
            const gain1 = this.ctx.createGain();
            osc1.type = 'sine';
            osc1.frequency.setValueAtTime(baseFreq, t0);
            gain1.gain.setValueAtTime(0.35, t0);
            gain1.gain.exponentialRampToValueAtTime(0.001, t0 + 0.28);
            osc1.connect(gain1);
            gain1.connect(this.ctx.destination);
            this.trackNode(osc1);
            osc1.start(t0);
            osc1.stop(t0 + 0.3);

            const osc2 = this.ctx.createOscillator();
            const gain2 = this.ctx.createGain();
            osc2.type = 'sine';
            osc2.frequency.setValueAtTime(baseFreq * 4, t0);
            gain2.gain.setValueAtTime(0.09, t0);
            gain2.gain.exponentialRampToValueAtTime(0.001, t0 + 0.09);
            osc2.connect(gain2);
            gain2.connect(this.ctx.destination);
            this.trackNode(osc2);
            osc2.start(t0);
            osc2.stop(t0 + 0.1);
        } catch (e) {}
    },

    playAnimalSound(id) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        this.init();
        if (!this.ctx) return 800;

        if (this.animalBuffers.has(id)) {
            try {
                const buf = this.animalBuffers.get(id);
                const src = this.ctx.createBufferSource();
                src.buffer = buf;
                const gain = this.ctx.createGain();
                const now = this.ctx.currentTime;
                const maxDur = Math.min(buf.duration, 1.8);
                gain.gain.setValueAtTime(0.95, now);
                gain.gain.setValueAtTime(0.95, now + maxDur - 0.25);
                gain.gain.linearRampToValueAtTime(0.001, now + maxDur);
                src.connect(gain);
                gain.connect(this.ctx.destination);
                this.trackNode(src);
                src.start(now);
                src.stop(now + maxDur);
                return Math.round(maxDur * 1000);
            } catch (e) {}
        }

        const url = ANIMAL_SOUND_URLS[id];
        if (url) {
            try {
                const audio = new Audio(url);
                this.activeAudioElements.add(audio);
                audio.volume = 0.95;
                audio.play().catch(() => {});
                const stopTimer = setTimeout(() => {
                    try { audio.pause(); audio.src = ''; } catch(e){}
                    this.activeAudioElements.delete(audio);
                }, 1800);
                this.registerTimer(stopTimer);
                audio.onended = () => {
                    this.activeAudioElements.delete(audio);
                };
                fetch(url).then(r => r.arrayBuffer()).then(ab => this.ctx.decodeAudioData(ab)).then(dec => this.animalBuffers.set(id, dec)).catch(()=>{});
                return 1800;
            } catch (e) {}
        }

        return this.playAnimalSynth(id);
    },

    playAnimalSynth(id) {
        switch (id) {
            case 'Cat':
                this.playSlide(480, 720, 0.28, 'sine', 0.34, 0);
                this.playSlide(720, 410, 0.42, 'sine', 0.28, 0.27);
                return 720;
            case 'Dog':
                this.playSlide(190, 340, 0.14, 'triangle', 0.38, 0);
                this.playSlide(180, 320, 0.15, 'triangle', 0.36, 0.22);
                return 480;
            case 'Cow':
                this.playSlide(120, 160, 0.45, 'triangle', 0.35, 0);
                this.playSlide(160, 130, 0.48, 'triangle', 0.32, 0.44);
                return 880;
            case 'Duck':
                this.playSlide(380, 260, 0.15, 'sawtooth', 0.32, 0, 1200);
                this.playSlide(380, 260, 0.15, 'sawtooth', 0.32, 0.22, 1200);
                return 460;
            case 'Pig':
                this.playSlide(220, 320, 0.12, 'sawtooth', 0.32, 0, 950);
                this.playSlide(220, 300, 0.14, 'sawtooth', 0.3, 0.2, 950);
                return 450;
            case 'Sheep':
                this.playSlide(280, 250, 0.62, 'triangle', 0.34, 0);
                this.playNoise(0.5, 'bandpass', 650, 2.5, 0.12, 0.05);
                return 680;
            case 'Horse':
                this.playSlide(680, 920, 0.28, 'sine', 0.34, 0);
                this.playSlide(920, 480, 0.45, 'sine', 0.28, 0.28);
                return 780;
            case 'Elephant':
                this.playSlide(360, 680, 0.38, 'sawtooth', 0.34, 0, 2400);
                this.playSlide(680, 520, 0.35, 'sawtooth', 0.3, 0.37, 2200);
                return 760;
            case 'Monkey':
                this.playSlide(520, 780, 0.14, 'sine', 0.35, 0);
                this.playSlide(520, 780, 0.14, 'sine', 0.35, 0.2);
                this.playSlide(600, 900, 0.18, 'sine', 0.32, 0.4);
                return 640;
            case 'Frog':
                this.playSlide(140, 260, 0.18, 'sawtooth', 0.35, 0, 800);
                this.playSlide(140, 240, 0.2, 'sawtooth', 0.33, 0.25, 800);
                return 520;
            case 'Owl':
                this.playSlide(380, 420, 0.28, 'sine', 0.35, 0);
                this.playSlide(370, 340, 0.35, 'sine', 0.35, 0.36);
                return 760;
            case 'Bee':
                this.playNote(220, 0.65, 'sawtooth', 0.26);
                return 650;
            case 'Snake':
                this.playNoise(0.65, 'highpass', 4500, 1.5, 0.3, 0);
                return 650;
            case 'Lion':
            case 'Bear':
            case 'Dinosaur':
                this.playSlide(130, 65, 0.72, 'triangle', 0.44, 0);
                this.playNoise(0.68, 'lowpass', 380, 1.6, 0.35, 0);
                return 800;
            case 'Penguin':
                this.playSlide(880, 1180, 0.12, 'sine', 0.32, 0);
                this.playSlide(920, 1250, 0.14, 'sine', 0.3, 0.2);
                return 480;
            case 'Whale':
                this.playSlide(160, 320, 0.45, 'sine', 0.35, 0);
                this.playSlide(320, 180, 0.45, 'sine', 0.3, 0.44);
                return 900;
            default:
                this.playBubblePop();
                return 300;
        }
    },

    playThingSound(id) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        this.init();
        if (!this.ctx) return 800;
        const t0 = this.ctx.currentTime;
        switch (id) {
            case 'Fire Truck': {
                try {
                    const osc1 = this.ctx.createOscillator();
                    const osc2 = this.ctx.createOscillator();
                    const sFilter = this.ctx.createBiquadFilter();
                    const sGain = this.ctx.createGain();

                    osc1.type = 'sawtooth';
                    osc2.type = 'triangle';
                    osc2.detune.setValueAtTime(6, t0);

                    [osc1, osc2].forEach(osc => {
                        osc.frequency.setValueAtTime(420, t0);
                        osc.frequency.linearRampToValueAtTime(1180, t0 + 0.45);
                        osc.frequency.linearRampToValueAtTime(460, t0 + 0.85);
                        osc.frequency.linearRampToValueAtTime(1180, t0 + 1.30);
                        osc.frequency.linearRampToValueAtTime(900, t0 + 1.45);
                        osc.connect(sFilter);
                        this.trackNode(osc);
                        osc.start(t0);
                        osc.stop(t0 + 1.48);
                    });

                    sFilter.type = 'lowpass';
                    sFilter.frequency.setValueAtTime(1900, t0);
                    sFilter.Q.setValueAtTime(2.0, t0);

                    sGain.gain.setValueAtTime(0.001, t0);
                    sGain.gain.linearRampToValueAtTime(0.24, t0 + 0.05);
                    sGain.gain.setValueAtTime(0.24, t0 + 1.25);
                    sGain.gain.exponentialRampToValueAtTime(0.001, t0 + 1.45);

                    sFilter.connect(sGain);
                    sGain.connect(this.ctx.destination);
                } catch(e) {}

                [0.02, 0.28].forEach(del => {
                    [146.8, 185.0, 220.0].forEach(f => {
                        this.playNote(f, 0.18, 'sawtooth', 0.18, del);
                        this.playNote(f * 2, 0.18, 'triangle', 0.10, del);
                    });
                });

                [0.55, 0.80, 1.05].forEach(del => {
                    this.playNote(2150, 0.22, 'sine', 0.20, del);
                    this.playNote(3200, 0.16, 'sine', 0.14, del);
                });
                return 1450;
            }

            case 'Police Car': {
                try {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = 'sawtooth';
                    const yelpCycles = 6;
                    const halfCycle = 1.2 / (yelpCycles * 2);
                    osc.frequency.setValueAtTime(580, t0);
                    for (let c = 0; c < yelpCycles; c++) {
                        const upT = t0 + (c * 2 + 1) * halfCycle;
                        const downT = t0 + (c * 2 + 2) * halfCycle;
                        osc.frequency.linearRampToValueAtTime(1350, upT);
                        osc.frequency.linearRampToValueAtTime(580, downT);
                    }
                    gain.gain.setValueAtTime(0.001, t0);
                    gain.gain.linearRampToValueAtTime(0.25, t0 + 0.04);
                    gain.gain.setValueAtTime(0.25, t0 + 1.10);
                    gain.gain.exponentialRampToValueAtTime(0.001, t0 + 1.25);
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    this.trackNode(osc);
                    osc.start(t0);
                    osc.stop(t0 + 1.28);
                } catch(e) {}

                [0.0, 0.18].forEach(del => {
                    this.playSlide(420, 980, 0.11, 'triangle', 0.28, del, 2400);
                });
                return 1250;
            }

            case 'Train': {
                [0.05, 0.60].forEach(del => {
                    [370, 440, 554.4, 740].forEach(f => {
                        this.playNote(f, 0.46, 'triangle', 0.18, del);
                    });
                    this.playNoise(0.46, 'bandpass', 1200, 1.2, 0.15, del);
                });

                for (let i = 0; i < 8; i++) {
                    const del = i * 0.14;
                    this.playNoise(0.06, 'bandpass', 450 + (i % 2) * 120, 2.5, 0.24, del);
                    this.playSlide(75, 38, 0.06, 'triangle', 0.22, del);
                }

                [0.10, 0.42, 0.74, 1.06].forEach(del => {
                    this.playNote(1650, 0.18, 'sine', 0.16, del);
                });
                return 1300;
            }

            case 'Rocket Ship': {
                this.playSlide(48, 85, 1.4, 'sine', 0.45, 0);
                this.playSlide(55, 95, 1.4, 'triangle', 0.35, 0);
                try {
                    const src = this.ctx.createBufferSource();
                    src.buffer = this.noiseBuf;
                    const filter = this.ctx.createBiquadFilter();
                    filter.type = 'lowpass';
                    filter.frequency.setValueAtTime(200, t0);
                    filter.frequency.exponentialRampToValueAtTime(1800, t0 + 1.2);
                    const gain = this.ctx.createGain();
                    gain.gain.setValueAtTime(0.01, t0);
                    gain.gain.linearRampToValueAtTime(0.38, t0 + 0.3);
                    gain.gain.exponentialRampToValueAtTime(0.001, t0 + 1.4);
                    src.connect(filter);
                    filter.connect(gain);
                    gain.connect(this.ctx.destination);
                    this.trackNode(src);
                    src.start(t0);
                    src.stop(t0 + 1.42);
                } catch(e) {}
                this.playSlide(350, 1400, 1.35, 'sawtooth', 0.15, 0.05, 2200);
                return 1400;
            }

            case 'Airplane': {
                this.playSlide(1200, 2100, 0.65, 'sine', 0.16, 0);
                this.playSlide(2100, 900, 0.70, 'sine', 0.16, 0.65);
                try {
                    const src = this.ctx.createBufferSource();
                    src.buffer = this.noiseBuf;
                    const bp = this.ctx.createBiquadFilter();
                    bp.type = 'bandpass';
                    bp.frequency.setValueAtTime(250, t0);
                    bp.frequency.linearRampToValueAtTime(2200, t0 + 0.65);
                    bp.frequency.linearRampToValueAtTime(350, t0 + 1.35);
                    bp.Q.setValueAtTime(1.0, t0);
                    const gain = this.ctx.createGain();
                    gain.gain.setValueAtTime(0.01, t0);
                    gain.gain.linearRampToValueAtTime(0.35, t0 + 0.65);
                    gain.gain.exponentialRampToValueAtTime(0.001, t0 + 1.35);
                    src.connect(bp);
                    bp.connect(gain);
                    gain.connect(this.ctx.destination);
                    this.trackNode(src);
                    src.start(t0);
                    src.stop(t0 + 1.38);
                } catch(e) {}
                return 1350;
            }

            case 'Helicopter': {
                for (let i = 0; i < 10; i++) {
                    const del = i * 0.115;
                    this.playSlide(68, 35, 0.07, 'sine', 0.42, del);
                    this.playNoise(0.045, 'bandpass', 750, 2.0, 0.28, del);
                }
                this.playNote(180, 1.20, 'triangle', 0.18, 0);
                return 1250;
            }

            case 'Tractor': {
                for (let i = 0; i < 8; i++) {
                    const del = i * 0.145;
                    this.playSlide(75, 42, 0.08, 'triangle', 0.38, del);
                    this.playNoise(0.035, 'highpass', 1600, 1.2, 0.25, del);
                }
                this.playNote(55, 1.25, 'sawtooth', 0.16, 0);
                return 1300;
            }

            case 'School Bus': {
                [0.02, 0.34].forEach(del => {
                    [415, 523.25, 830, 1046.5].forEach((f, idx) => {
                        this.playNote(f, 0.20, 'sawtooth', idx < 2 ? 0.22 : 0.10, del);
                    });
                });
                this.playNote(85, 1.1, 'triangle', 0.15, 0);
                this.playNoise(0.48, 'highpass', 3200, 1.2, 0.22, 0.65);
                return 1200;
            }

            case 'Sailboat': {
                try {
                    const src = this.ctx.createBufferSource();
                    src.buffer = this.noiseBuf;
                    const filter = this.ctx.createBiquadFilter();
                    filter.type = 'bandpass';
                    filter.frequency.setValueAtTime(300, t0);
                    filter.frequency.linearRampToValueAtTime(1200, t0 + 0.6);
                    filter.frequency.linearRampToValueAtTime(400, t0 + 1.3);
                    filter.Q.setValueAtTime(1.1, t0);
                    const gain = this.ctx.createGain();
                    gain.gain.setValueAtTime(0.01, t0);
                    gain.gain.linearRampToValueAtTime(0.28, t0 + 0.6);
                    gain.gain.exponentialRampToValueAtTime(0.001, t0 + 1.3);
                    src.connect(filter);
                    filter.connect(gain);
                    gain.connect(this.ctx.destination);
                    this.trackNode(src);
                    src.start(t0);
                    src.stop(t0 + 1.32);
                } catch(e) {}

                [0.25, 0.42].forEach(del => {
                    [1318, 2637, 3820].forEach((f, idx) => {
                        this.playNote(f, 0.35, 'sine', idx === 0 ? 0.22 : 0.12, del);
                    });
                });

                this.playSlide(1850, 2450, 0.18, 'sine', 0.16, 0.72);
                this.playSlide(2450, 1600, 0.22, 'sine', 0.14, 0.90);
                return 1300;
            }

            case 'Bicycle': {
                [0.0, 0.42].forEach(baseDel => {
                    for (let i = 0; i < 5; i++) {
                        const d = baseDel + i * 0.032;
                        [2480, 3720, 5210].forEach((f, idx) => {
                            this.playNote(f, 0.08, 'sine', idx === 0 ? 0.22 : 0.12, d);
                        });
                    }
                    this.playNote(2480, 0.55, 'sine', 0.18, baseDel + 0.16);
                });
                return 1200;
            }

            case 'Soccer Ball': {
                this.playSlide(180, 45, 0.12, 'sine', 0.50, 0);
                this.playNoise(0.05, 'lowpass', 550, 1.5, 0.32, 0);

                try {
                    const osc = this.ctx.createOscillator();
                    const lfo = this.ctx.createOscillator();
                    const lfoGain = this.ctx.createGain();
                    const gain = this.ctx.createGain();

                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(2850, t0 + 0.22);

                    lfo.frequency.setValueAtTime(28, t0 + 0.22);
                    lfoGain.gain.setValueAtTime(120, t0 + 0.22);
                    lfo.connect(lfoGain);
                    lfoGain.connect(osc.frequency);

                    gain.gain.setValueAtTime(0.001, t0 + 0.22);
                    gain.gain.linearRampToValueAtTime(0.30, t0 + 0.26);
                    gain.gain.setValueAtTime(0.30, t0 + 0.65);
                    gain.gain.exponentialRampToValueAtTime(0.001, t0 + 0.75);

                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    this.trackNode(osc);
                    this.trackNode(lfo);

                    lfo.start(t0 + 0.22);
                    osc.start(t0 + 0.22);
                    lfo.stop(t0 + 0.78);
                    osc.stop(t0 + 0.78);
                } catch(e) {}

                this.playNoise(0.70, 'bandpass', 950, 1.4, 0.22, 0.35);
                return 1250;
            }

            case 'Guitar': {
                const gChord = [98, 123.47, 146.83, 196, 246.94, 392];
                gChord.forEach((f, i) => {
                    const del = i * 0.022;
                    this.playNote(f, 0.48, 'triangle', 0.22, del);
                    this.playNote(f * 2, 0.42, 'sine', 0.12, del);
                    this.playNote(f * 3, 0.32, 'sine', 0.06, del);
                });
                [...gChord].reverse().forEach((f, i) => {
                    const del = 0.55 + i * 0.018;
                    this.playNote(f, 0.55, 'triangle', 0.20, del);
                    this.playNote(f * 2, 0.45, 'sine', 0.10, del);
                });
                return 1300;
            }

            case 'Drum': {
                [0.0, 0.45, 0.82].forEach(del => {
                    this.playSlide(150, 42, 0.14, 'sine', 0.50, del);
                    this.playNoise(0.04, 'lowpass', 400, 1.2, 0.25, del);
                });
                [0.15, 0.25, 0.35, 0.60, 0.70].forEach(del => {
                    this.playNote(210, 0.10, 'triangle', 0.24, del);
                    this.playNoise(0.09, 'highpass', 1200, 1.5, 0.28, del);
                });
                this.playNoise(0.58, 'highpass', 4500, 1.0, 0.30, 0.82);
                return 1400;
            }

            case 'Clock': {
                this.playNote(1650, 0.045, 'triangle', 0.28, 0);
                this.playNote(1650, 0.045, 'triangle', 0.28, 0.44);
                this.playNote(1180, 0.045, 'triangle', 0.28, 0.22);
                this.playNote(1180, 0.045, 'triangle', 0.28, 0.66);
                for (let i = 0; i < 12; i++) {
                    const del = 0.85 + i * 0.035;
                    const f = i % 2 === 0 ? 2600 : 2850;
                    this.playNote(f, 0.04, 'sine', 0.22, del);
                }
                return 1350;
            }

            default:
                this.playBubblePop();
                return 300;
        }
    },

    playCheer() {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        [523.25, 659.25, 783.99, 1046.5].forEach((f, i) => {
            const timer = setTimeout(() => this.playNote(f, 0.2, 'triangle', 0.25), i * 75);
            this.registerTimer(timer);
        });
    },

    playCosmicChime() {
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return;
        [523.25, 659.25, 783.99, 987.77, 1318.5].forEach((f, i) => {
            const timer = setTimeout(() => this.playNote(f, 0.25, 'sine', 0.18), i * 60);
            this.registerTimer(timer);
        });
    }
};

const DEFAULT_SETTINGS = {
    announceGameOnOpen: true, // Announce game title & intro when opening a game from Home menu
    voiceEnabled: true,       // Master toggle for spoken voice (TTS)
    sfxEnabled: true,         // Master toggle for sound effects (animals, vehicles, crunches, pops)
    confettiEnabled: true,    // Celebratory confetti bursts & food crumbs
    autoSpin3D: true,         // Auto-rotate 3D shapes & 3D planets when idle
    requireHoldHome: false,   // Toddler Lock: require double-tap on Home button to exit a game
    speechRate: 'normal',     // 'slow' (0.82), 'normal' (0.96), 'fast' (1.10)
    maxNumber: 20,            // 10 (1-10 Beginner) or 20 (1-20 Advanced)
    phonicsDetail: 'full'     // 'full' ("A! A says ah! ah, Apple!") or 'simple' ("A! Apple!")
};

const GAME_OPEN_TITLES = {
    letters: 'ABC Phonics!',
    numbers: 'Numbers and Counting!',
    quiz: 'Look and Find!',
    shapes: '2D Shapes!',
    shapes3d: '3D Shapes!',
    colors: 'Colors and Paint!',
    animals: 'Animal Friends!',
    fruits: 'Yummy Foods!',
    things: 'Vehicles and Things!',
    opposites: 'Opposites!',
    solar: 'Solar System!'
};

const app = {
    currentView: 'menu',
    currentUtterance: null,
    speechTimeout: null,
    cachedVoice: null,
    settings: (() => {
        try {
            const saved = localStorage.getItem('tlh_isolated_v3_settings');
            if (saved) return Object.assign({}, DEFAULT_SETTINGS, JSON.parse(saved));
        } catch (e) {}
        return Object.assign({}, DEFAULT_SETTINGS);
    })(),
    isOpeningView: false,
    pendingGameIntro: null,

    saveSettings() {
        try {
            localStorage.setItem('tlh_isolated_v3_settings', JSON.stringify(this.settings));
        } catch (e) {}
        if (typeof numberGame !== 'undefined' && numberGame.applyMaxNumberSetting) {
            numberGame.applyMaxNumberSetting();
        }
        if (typeof updateVoiceStatusIndicator === 'function') {
            updateVoiceStatusIndicator();
        }
    },

    getSpeechRateValue() {
        const rate = (this.settings && this.settings.speechRate) || 'normal';
        if (rate === 'slow') return 0.82;
        if (rate === 'fast') return 1.10;
        return 0.96;
    },

    initVoices() {
        if (!('speechSynthesis' in window)) return;
        const voices = window.speechSynthesis.getVoices();
        if (!voices || voices.length === 0) return;
        let bestVoice = null;
        let bestScore = -1;
        voices.forEach(v => {
            let score = 0;
            const lang = (v.lang || '').toLowerCase();
            const name = (v.name || '').toLowerCase();
            if (lang.startsWith('en')) score += 100;
            if (v.localService === true) score += 60;
            if (name.includes('natural')) score += 50;
            if (name.includes('premium')) score += 40;
            if (name.includes('enhanced')) score += 35;
            if (['samantha', 'ava', 'allison', 'karen', 'daniel', 'moira', 'tessa'].some(n => name.includes(n))) {
                score += 30;
            }
            if (name.includes('google us english') || name.includes('siri')) score += 20;
            if (score > bestScore) {
                bestScore = score;
                bestVoice = v;
            }
        });
        if (bestVoice) {
            this.cachedVoice = bestVoice;
        }
    },

    setSpeakingUI(isSpeaking) {
        document.querySelectorAll('.audio-vis-pill').forEach(el => {
            if (isSpeaking) el.classList.add('speaking');
            else el.classList.remove('speaking');
        });
    },

    switchView(viewName) {
        soundFX.stopAll();
        geminiTTS.stop();

        document.querySelectorAll('.view-section').forEach(el => el.classList.remove('active-view'));
        if (this.currentView === 'letters' && typeof phonicsGame !== 'undefined') phonicsGame.stopBubbles();
        if (this.currentView === 'shapes3d' && typeof shapes3DGame !== 'undefined') shapes3DGame.stop();
        if (this.currentView === 'solar' && typeof solarGame !== 'undefined') solarGame.stop();
        if (this.currentView === 'numbers' && typeof numberGame !== 'undefined') numberGame.clearAutoTimers();

        const target = document.getElementById(`view-${viewName}`);
        if (target) target.classList.add('active-view');
        this.currentView = viewName;

        if (viewName === 'menu') {
            this.pendingGameIntro = null;
            this.isOpeningView = false;
            soundFX.playPop();
            return;
        }

        soundFX.playPop();

        const shouldAnnounce = this.settings && this.settings.announceGameOnOpen;
        this.isOpeningView = true;
        this.pendingGameIntro = shouldAnnounce ? GAME_OPEN_TITLES[viewName] : null;

        if (viewName === 'letters') phonicsGame.open();
        else if (viewName === 'numbers') numberGame.open();
        else if (viewName === 'quiz') quizGame.open();
        else if (viewName === 'shapes') shape2DGame.select(GAMES.shapes[0], true);
        else if (viewName === 'shapes3d') shapes3DGame.select(GAMES.shapes3d[0], true);
        else if (viewName === 'colors') colorGame.open();
        else if (viewName === 'animals') animalGame.select(GAMES.animals[0], true, false);
        else if (viewName === 'fruits') foodGame.select(GAMES.fruits[0], true);
        else if (viewName === 'things') thingsGame.select(GAMES.things[0], true);
        else if (viewName === 'opposites') oppositesGame.select(GAMES.opposites[0], true);
        else if (viewName === 'solar') solarGame.open();

        this.isOpeningView = false;
        this.pendingGameIntro = null;
    },

    speak(text) {
        if (!this.settings.voiceEnabled) {
            this.pendingGameIntro = null;
            return;
        }

        if (this.isOpeningView && !this.settings.announceGameOnOpen) {
            this.pendingGameIntro = null;
            return;
        }

        if (this.pendingGameIntro) {
            const intro = this.pendingGameIntro;
            this.pendingGameIntro = null;
            if (typeof text === 'string' && !text.trim().startsWith(intro)) {
                text = `${intro} ${text}`;
            }
        }

        const clean = cleanSpokenText(text);
        if (!clean) return;

        geminiTTS.stop();
        if (this.speechTimeout) {
            clearTimeout(this.speechTimeout);
            this.speechTimeout = null;
        }

        const key = getApiKey();
        if (key) {
            const cacheKey = `${getTtsModel()}:${getTtsVoice()}:${clean}`;
            if (geminiTTS.memCache.has(cacheKey)) {
                geminiTTS.play(clean).catch(() => {
                    this.speakDeviceVoice(clean);
                });
                return;
            }

            let didFallback = false;
            let timer = setTimeout(() => {
                didFallback = true;
                geminiTTS.stop();
                this.speakDeviceVoice(clean);
            }, 1200);

            geminiTTS.play(clean).then(() => {
                if (timer) { clearTimeout(timer); timer = null; }
            }).catch(() => {
                if (timer) { clearTimeout(timer); timer = null; }
                if (!didFallback) {
                    this.speakDeviceVoice(clean);
                }
            });
        } else {
            this.speakDeviceVoice(clean);
        }
    },

    speakDeviceVoice(cleanText) {
        try {
            if (!this.settings.voiceEnabled) return;
            if (!('speechSynthesis' in window)) return;

            if (window.speechSynthesis.speaking || window.speechSynthesis.pending) {
                try { window.speechSynthesis.cancel(); } catch(e){}
            }

            if (!this.cachedVoice) this.initVoices();

            const msg = new SpeechSynthesisUtterance(cleanText);
            msg.rate = this.getSpeechRateValue();
            msg.pitch = 1.05;
            if (this.cachedVoice) msg.voice = this.cachedVoice;

            msg.onstart = () => app.setSpeakingUI(true);
            msg.onend = () => {
                app.setSpeakingUI(false);
                app.currentUtterance = null;
            };
            msg.onerror = () => {
                app.setSpeakingUI(false);
                app.currentUtterance = null;
            };

            this.currentUtterance = msg;
            window.speechSynthesis.speak(msg);
        } catch (e) {
            app.setSpeakingUI(false);
        }
    },

    burstConfetti(x = window.innerWidth / 2, y = window.innerHeight / 2) {
        if (this.settings && !this.settings.confettiEnabled) return;
        const colors = ['#ef4444', '#3b82f6', '#facc15', '#22c55e', '#ec4899', '#a855f7', '#06b6d4'];
        for (let i = 0; i < 22; i++) {
            const p = document.createElement('div');
            p.className = 'confetti-piece';
            p.style.left = `${x}px`;
            p.style.top = `${y}px`;
            p.style.backgroundColor = colors[i % colors.length];
            const angle = (Math.PI * 2 * i) / 22;
            const dist = 55 + Math.random() * 110;
            p.style.setProperty('--dx', `${Math.cos(angle) * dist}px`);
            p.style.setProperty('--dy', `${Math.sin(angle) * dist - 40}px`);
            p.style.setProperty('--rot', `${Math.random() * 540 - 270}deg`);
            document.body.appendChild(p);
            setTimeout(() => p.remove(), 980);
        }
    },

    animatePop(el) {
        if (!el) return;
        el.classList.remove('pop-anim');
        void el.offsetWidth;
        el.classList.add('pop-anim');
    }
};


// scratch/solar.js

function getSolarSVG(id, uidPrefix) {
    const uid = uidPrefix || ('s' + Math.random().toString(36).slice(2, 7));
    const stars = `
        <circle cx="28" cy="32" r="1.5" fill="#fff" opacity="0.9"/>
        <circle cx="172" cy="38" r="1.8" fill="#fef08a" opacity="0.9"/>
        <circle cx="38" cy="168" r="1.4" fill="#bae6fd" opacity="0.8"/>
        <circle cx="166" cy="162" r="1.6" fill="#fff" opacity="0.9"/>
        <circle cx="24" cy="98" r="1.2" fill="#fff" opacity="0.7"/>
        <circle cx="182" cy="104" r="1.3" fill="#fbcfe8" opacity="0.8"/>
        <circle cx="85" cy="22" r="1.0" fill="#fff" opacity="0.6"/>
        <circle cx="120" cy="180" r="1.2" fill="#fde68a" opacity="0.7"/>
    `;
    let body = '';

    switch (id) {
        case 'The Sun':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="44%" cy="44%" r="56%">
                        <stop offset="0%" stop-color="#ffffff"/>
                        <stop offset="25%" stop-color="#fef08a"/>
                        <stop offset="55%" stop-color="#facc15"/>
                        <stop offset="82%" stop-color="#f97316"/>
                        <stop offset="100%" stop-color="#dc2626"/>
                    </radialGradient>
                    <filter id="${uid}_glow" x="-30%" y="-30%" width="160%" height="160%">
                        <feGaussianBlur stdDeviation="7" result="blur"/>
                        <feComposite in="SourceGraphic" in2="blur" operator="over"/>
                    </filter>
                </defs>
                <circle cx="100" cy="100" r="84" fill="#f97316" opacity="0.25" filter="url(#${uid}_glow)"/>
                <circle cx="100" cy="100" r="74" fill="#facc15" opacity="0.35"/>
                <!-- Solar prominences / flares -->
                <path d="M 40,75 Q 22,60 35,90" stroke="#f97316" stroke-width="3" fill="none" opacity="0.8"/>
                <path d="M 160,70 Q 182,55 168,90" stroke="#f97316" stroke-width="3.5" fill="none" opacity="0.8"/>
                <path d="M 90,26 Q 105,12 115,28" stroke="#facc15" stroke-width="3" fill="none" opacity="0.8"/>
                <circle cx="100" cy="100" r="68" fill="url(#${uid}_g)"/>
                <!-- Sunspots -->
                <circle cx="76" cy="88" r="5" fill="#9a3412" opacity="0.75"/>
                <circle cx="81" cy="91" r="3" fill="#7c2d12" opacity="0.85"/>
                <circle cx="124" cy="114" r="4.5" fill="#9a3412" opacity="0.75"/>
                <circle cx="120" cy="117" r="2.5" fill="#7c2d12" opacity="0.85"/>
            `;
            break;

        case 'Mercury':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#f1f5f9"/>
                        <stop offset="45%" stop-color="#94a3b8"/>
                        <stop offset="85%" stop-color="#475569"/>
                        <stop offset="100%" stop-color="#0f172a"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="64"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="64" fill="url(#${uid}_g)"/>
                    <!-- Major impact craters & rays -->
                    <circle cx="75" cy="78" r="14" fill="#64748b" stroke="#cbd5e1" stroke-width="2"/>
                    <circle cx="75" cy="78" r="6" fill="#475569"/>
                    <circle cx="122" cy="94" r="16" fill="#64748b" stroke="#cbd5e1" stroke-width="2"/>
                    <circle cx="122" cy="94" r="7" fill="#334155"/>
                    <circle cx="92" cy="128" r="11" fill="#475569" stroke="#94a3b8" stroke-width="1.5"/>
                    <path d="M 75,78 L 45,55 M 75,78 L 95,50 M 75,78 L 55,105" stroke="#e2e8f0" stroke-width="1.2" opacity="0.6"/>
                    <!-- Night terminator crescent shadow -->
                    <path d="M 100,36 A 64,64 0 0,1 100,164 A 48,64 0 0,0 100,36" fill="#020617" opacity="0.65"/>
                </g>
            `;
            break;

        case 'Venus':
            body = `
                <defs>
                    <linearGradient id="${uid}_g" x1="0" y1="0" x2="1" y2="1">
                        <stop offset="0%" stop-color="#fef3c7"/>
                        <stop offset="35%" stop-color="#fbbf24"/>
                        <stop offset="70%" stop-color="#d97706"/>
                        <stop offset="100%" stop-color="#451a03"/>
                    </linearGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="66"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="66" fill="url(#${uid}_g)"/>
                    <!-- Swirling sulfuric clouds -->
                    <path d="M 20,70 Q 95,90 180,65" stroke="#fef3c7" stroke-width="14" fill="none" opacity="0.65"/>
                    <path d="M 20,95 Q 100,120 180,95" stroke="#b45309" stroke-width="16" fill="none" opacity="0.45"/>
                    <path d="M 20,125 Q 95,145 180,120" stroke="#fde68a" stroke-width="12" fill="none" opacity="0.55"/>
                    <path d="M 35,48 Q 110,65 175,45" stroke="#fef9c3" stroke-width="9" fill="none" opacity="0.7"/>
                    <!-- Night terminator shadow -->
                    <path d="M 100,34 A 66,66 0 0,1 100,166 A 50,66 0 0,0 100,34" fill="#1c1917" opacity="0.55"/>
                </g>
                <circle cx="100" cy="100" r="67" fill="none" stroke="#fde68a" stroke-width="2" opacity="0.4"/>
            `;
            break;

        case 'Earth':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="36%" cy="36%" r="64%">
                        <stop offset="0%" stop-color="#38bdf8"/>
                        <stop offset="35%" stop-color="#0284c7"/>
                        <stop offset="75%" stop-color="#1d4ed8"/>
                        <stop offset="100%" stop-color="#051b47"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="67"/></clipPath>
                    <filter id="${uid}_atm">
                        <feGaussianBlur stdDeviation="3" result="blur"/>
                    </filter>
                </defs>
                <!-- Blue atmosphere rim glow -->
                <circle cx="100" cy="100" r="70" fill="none" stroke="#60a5fa" stroke-width="4" opacity="0.65" filter="url(#${uid}_atm)"/>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="67" fill="url(#${uid}_g)"/>
                    <!-- Continents: Eurasia/Africa & Americas -->
                    <path d="M 52,58 Q 74,50 82,72 Q 72,92 54,88 Z" fill="#22c55e"/>
                    <path d="M 72,102 Q 94,108 90,136 Q 74,148 68,126 Z" fill="#16a34a"/>
                    <path d="M 112,68 Q 146,62 154,100 Q 138,138 116,122 Z" fill="#22c55e"/>
                    <path d="M 124,80 Q 138,78 140,90 Z" fill="#ca8a04"/> <!-- Sahara desert -->
                    <!-- Polar Ice Caps -->
                    <ellipse cx="100" cy="36" rx="36" ry="10" fill="#ffffff" opacity="0.95"/>
                    <ellipse cx="100" cy="164" rx="34" ry="9" fill="#ffffff" opacity="0.95"/>
                    <!-- Cloud bands -->
                    <path d="M 40,82 Q 75,72 110,84 Q 145,95 168,78" stroke="#ffffff" stroke-width="7" stroke-linecap="round" fill="none" opacity="0.75"/>
                    <path d="M 55,120 Q 95,130 145,115" stroke="#ffffff" stroke-width="6" stroke-linecap="round" fill="none" opacity="0.65"/>
                    <!-- Terminator shadow -->
                    <path d="M 100,33 A 67,67 0 0,1 100,167 A 50,67 0 0,0 100,33" fill="#020617" opacity="0.6"/>
                </g>
            `;
            break;

        case "Earth's Moon":
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#ffffff"/>
                        <stop offset="45%" stop-color="#cbd5e1"/>
                        <stop offset="85%" stop-color="#64748b"/>
                        <stop offset="100%" stop-color="#1e293b"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="64"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="64" fill="url(#${uid}_g)"/>
                    <!-- Lunar Maria (Dark Basalt Plains) -->
                    <ellipse cx="80" cy="74" rx="22" ry="18" fill="#475569" opacity="0.55"/>
                    <ellipse cx="118" cy="84" rx="20" ry="16" fill="#475569" opacity="0.5"/>
                    <ellipse cx="76" cy="114" rx="18" ry="22" fill="#334155" opacity="0.45"/>
                    <!-- Tycho ray crater -->
                    <circle cx="98" cy="138" r="9" fill="#64748b" stroke="#f8fafc" stroke-width="2.5"/>
                    <path d="M 98,138 L 72,115 M 98,138 L 126,118 M 98,138 L 100,160" stroke="#f8fafc" stroke-width="1.2" opacity="0.6"/>
                    <!-- Night terminator shadow -->
                    <path d="M 100,36 A 64,64 0 0,1 100,164 A 48,64 0 0,0 100,36" fill="#0f172a" opacity="0.65"/>
                </g>
            `;
            break;

        case 'Mars':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#fed7aa"/>
                        <stop offset="35%" stop-color="#f97316"/>
                        <stop offset="75%" stop-color="#b91c1c"/>
                        <stop offset="100%" stop-color="#450a0a"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="65"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="65" fill="url(#${uid}_g)"/>
                    <!-- Syrtis Major basalt & canyons -->
                    <ellipse cx="118" cy="94" rx="24" ry="28" fill="#7f1d1d" opacity="0.6"/>
                    <path d="M 55,104 Q 96,115 136,98" stroke="#450a0a" stroke-width="5" stroke-linecap="round" fill="none"/>
                    <!-- White North Polar Ice Cap -->
                    <ellipse cx="100" cy="37" rx="28" ry="8" fill="#ffffff" opacity="0.95"/>
                    <ellipse cx="100" cy="163" rx="20" ry="6" fill="#ffffff" opacity="0.85"/>
                    <!-- Terminator shadow -->
                    <path d="M 100,35 A 65,65 0 0,1 100,165 A 48,65 0 0,0 100,35" fill="#2d0606" opacity="0.6"/>
                </g>
                <circle cx="100" cy="100" r="66" fill="none" stroke="#fdba74" stroke-width="2" opacity="0.35"/>
            `;
            break;

        case 'Asteroid Belt':
            body = `
                <defs>
                    <radialGradient id="${uid}_vesta" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#d6d3d1"/>
                        <stop offset="60%" stop-color="#78716c"/>
                        <stop offset="100%" stop-color="#292524"/>
                    </radialGradient>
                </defs>
                <!-- Mini tumbling asteroids around -->
                <ellipse cx="44" cy="52" rx="10" ry="7" fill="#a8a29e"/>
                <ellipse cx="158" cy="58" rx="12" ry="8" fill="#78716c"/>
                <ellipse cx="38" cy="146" rx="11" ry="8" fill="#a8a29e"/>
                <ellipse cx="162" cy="142" rx="9" ry="6" fill="#78716c"/>
                <circle cx="82" cy="35" r="5" fill="#a8a29e"/>
                <circle cx="120" cy="168" r="6" fill="#78716c"/>
                <!-- Main lumpy Vesta asteroid -->
                <path d="M 100,46 C 142,42 168,70 164,104 C 160,138 134,158 96,156 C 58,154 36,132 38,98 C 40,66 68,48 100,46 Z" fill="url(#${uid}_vesta)" stroke="#57534e" stroke-width="3"/>
                <!-- Impact craters -->
                <circle cx="82" cy="82" r="11" fill="#44403c" stroke="#a8a29e" stroke-width="1.5"/>
                <circle cx="106" cy="86" r="8" fill="#44403c"/>
                <circle cx="118" cy="120" r="14" fill="#292524" stroke="#a8a29e" stroke-width="2"/>
            `;
            break;

        case 'Jupiter':
            body = `
                <defs>
                    <clipPath id="${uid}_c"><ellipse cx="100" cy="100" rx="72" ry="67"/></clipPath>
                    <linearGradient id="${uid}_g" x1="0" y1="0" x2="0" y2="1">
                        <stop offset="0%" stop-color="#d97706"/>
                        <stop offset="100%" stop-color="#78350f"/>
                    </linearGradient>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <rect x="20" y="30" width="160" height="14" fill="#78350f"/>
                    <rect x="20" y="44" width="160" height="15" fill="#fde68a"/>
                    <rect x="20" y="59" width="160" height="18" fill="#c2410c"/>
                    <rect x="20" y="77" width="160" height="22" fill="#fffbeb"/>
                    <rect x="20" y="99" width="160" height="20" fill="#ea580c"/>
                    <rect x="20" y="119" width="160" height="17" fill="#fde68a"/>
                    <rect x="20" y="136" width="160" height="34" fill="#78350f"/>
                    <!-- Wavy turbulence -->
                    <path d="M 25,68 Q 65,74 105,67 Q 145,61 175,68" stroke="#fde68a" stroke-width="4" fill="none"/>
                    <path d="M 25,108 Q 65,102 105,109 Q 145,115 175,108" stroke="#fffbeb" stroke-width="4" fill="none"/>
                    <!-- Great Red Spot Storm -->
                    <ellipse cx="122" cy="116" rx="20" ry="13" fill="#fef3c7"/>
                    <ellipse cx="122" cy="116" rx="17" ry="10" fill="#b91c1c"/>
                    <ellipse cx="122" cy="116" rx="10" ry="5.5" fill="#f97316"/>
                    <!-- Terminator shadow -->
                    <path d="M 100,33 A 72,67 0 0,1 100,167 A 52,67 0 0,0 100,33" fill="#1e1005" opacity="0.6"/>
                </g>
            `;
            break;

        case 'Saturn':
            body = `
                <g transform="translate(100,100) rotate(-22)">
                    <!-- Back ring segment -->
                    <path d="M -98,0 A 98,34 0 1,1 98,0" fill="none" stroke="#fef08a" stroke-width="14" opacity="0.85"/>
                    <path d="M -80,0 A 80,27 0 1,1 80,0" fill="none" stroke="#ca8a04" stroke-width="8" opacity="0.9"/>
                    <!-- Cassini division gap -->
                    <path d="M -85,0 A 85,29 0 1,1 85,0" fill="none" stroke="#060b19" stroke-width="2.5"/>
                    <!-- Planet body (oblate) -->
                    <ellipse cx="0" cy="0" rx="46" ry="41" fill="#eab308"/>
                    <ellipse cx="0" cy="-12" rx="44" ry="10" fill="#fef08a" opacity="0.65"/>
                    <ellipse cx="0" cy="10" rx="44" ry="9" fill="#ca8a04" opacity="0.5"/>
                    <!-- Shadow of planet on back ring -->
                    <ellipse cx="14" cy="-8" rx="22" ry="8" fill="#060b19" opacity="0.6"/>
                    <!-- Front ring segment -->
                    <path d="M 98,0 A 98,34 0 1,1 -98,0" fill="none" stroke="#fef08a" stroke-width="14" opacity="0.95"/>
                    <path d="M 80,0 A 80,27 0 1,1 -80,0" fill="none" stroke="#ca8a04" stroke-width="8" opacity="0.95"/>
                    <path d="M 85,0 A 85,29 0 1,1 -85,0" fill="none" stroke="#060b19" stroke-width="2.5"/>
                </g>
            `;
            break;

        case 'Uranus':
            body = `
                <g transform="translate(100,100) rotate(82)">
                    <!-- Vertical back ring -->
                    <path d="M -86,0 A 86,22 0 1,1 86,0" fill="none" stroke="#bae6fd" stroke-width="4.5" opacity="0.8"/>
                    <!-- Cyan ice giant sphere -->
                    <circle cx="0" cy="0" r="54" fill="#38bdf8"/>
                    <circle cx="-12" cy="-12" r="34" fill="#67e8f9" opacity="0.55"/>
                    <!-- Front vertical ring -->
                    <path d="M 86,0 A 86,22 0 1,1 -86,0" fill="none" stroke="#e0f2fe" stroke-width="5" opacity="0.95"/>
                </g>
            `;
            break;

        case 'Neptune':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#60a5fa"/>
                        <stop offset="40%" stop-color="#2563eb"/>
                        <stop offset="85%" stop-color="#1d4ed8"/>
                        <stop offset="100%" stop-color="#0a1236"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="66"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="66" fill="url(#${uid}_g)"/>
                    <!-- Great Dark Spot -->
                    <ellipse cx="84" cy="108" rx="20" ry="11" fill="#0f172a" opacity="0.85"/>
                    <!-- White methane cloud streaks -->
                    <path d="M 72,96 L 112,94 M 102,74 L 144,78 M 64,126 L 108,128" stroke="#e0f2fe" stroke-width="4" stroke-linecap="round" opacity="0.9"/>
                    <!-- Terminator shadow -->
                    <path d="M 100,34 A 66,66 0 0,1 100,166 A 48,66 0 0,0 100,34" fill="#030712" opacity="0.6"/>
                </g>
                <circle cx="100" cy="100" r="67" fill="none" stroke="#93c5fd" stroke-width="2" opacity="0.45"/>
            `;
            break;

        case 'Pluto':
            body = `
                <defs>
                    <radialGradient id="${uid}_g" cx="35%" cy="35%" r="65%">
                        <stop offset="0%" stop-color="#fed7aa"/>
                        <stop offset="55%" stop-color="#d6d3d1"/>
                        <stop offset="85%" stop-color="#78716c"/>
                        <stop offset="100%" stop-color="#292524"/>
                    </radialGradient>
                    <clipPath id="${uid}_c"><circle cx="100" cy="100" r="64"/></clipPath>
                </defs>
                <g clip-path="url(#${uid}_c)">
                    <circle cx="100" cy="100" r="64" fill="url(#${uid}_g)"/>
                    <!-- Tombaugh Regio Heart Basin -->
                    <path d="M 112,130 C 104,120 84,104 86,90 C 88,76 106,76 112,90 C 118,76 136,76 138,90 C 140,104 120,120 112,130 Z" fill="#ffffff" opacity="0.92"/>
                    <!-- Terminator shadow -->
                    <path d="M 100,36 A 64,64 0 0,1 100,164 A 48,64 0 0,0 100,36" fill="#1c1917" opacity="0.6"/>
                </g>
                <!-- Companion moon Charon -->
                <circle cx="166" cy="48" r="16" fill="#a8a29e" stroke="#57534e" stroke-width="1.5"/>
            `;
            break;

        case 'Comet':
            body = `
                <!-- Blue straight ion tail -->
                <path d="M 58,82 L 192,42 L 194,76 L 60,92 Z" fill="#38bdf8" opacity="0.65"/>
                <!-- Curved golden dust tail -->
                <path d="M 54,78 Q 124,88 192,122 L 174,166 Q 106,128 50,96 Z" fill="#fef08a" opacity="0.85"/>
                <!-- Glowing Cyan Coma -->
                <circle cx="58" cy="84" r="32" fill="#a5f3fc" opacity="0.45"/>
                <circle cx="58" cy="84" r="20" fill="#67e8f9" opacity="0.75"/>
                <!-- Craggy nucleus -->
                <polygon points="56,76 64,80 62,90 54,92 50,84" fill="#ffffff"/>
            `;
            break;

        case 'Galactic Swirl':
            body = `
                <g transform="translate(100,100) rotate(-24) scale(1, 0.65)">
                    <circle cx="0" cy="0" r="88" fill="#a855f7" opacity="0.22"/>
                    <!-- 4 Logarithmic spiral arms -->
                    <path d="M 0,0 Q 48,-12 68,36 Q 78,82 16,88" fill="none" stroke="#f472b6" stroke-width="13" stroke-linecap="round" opacity="0.8"/>
                    <path d="M 0,0 Q -48,12 -68,-36 Q -78,-82 -16,-88" fill="none" stroke="#38bdf8" stroke-width="13" stroke-linecap="round" opacity="0.8"/>
                    <path d="M 0,0 Q 22,48 -36,68" fill="none" stroke="#c084fc" stroke-width="11" stroke-linecap="round" opacity="0.8"/>
                    <path d="M 0,0 Q -22,-48 36,-68" fill="none" stroke="#fde047" stroke-width="11" stroke-linecap="round" opacity="0.8"/>
                    <!-- Glowing galactic core -->
                    <circle cx="0" cy="0" r="26" fill="#fef08a"/>
                    <circle cx="0" cy="0" r="14" fill="#ffffff"/>
                </g>
            `;
            break;
    }

    return `<svg viewBox="0 0 200 200" width="100%" height="100%" xmlns="http://www.w3.org/2000/svg"><rect width="200" height="200" fill="#060b19"/>${stars}${body}</svg>`;
}

const solarGame = {
    mode: 'photo',
    current: GAMES.solar[0],
    scene: null, camera: null, renderer: null, rootGroup: null,
    orbitEntries: [], animId: null, isDragging: false,
    prevX: 0, prevY: 0, velX: 0.011, velY: 0.002, turboBoost: 1,
    textureCache: new Map(),

    open() {
        this.select(this.current, true);
    },

    init3D() {
        if (this.renderer || typeof THREE === 'undefined') return;
        const container = document.getElementById('solar-canvas-container');
        if (!container) return;
        container.innerHTML = '';

        this.scene = new THREE.Scene();
        this.scene.add(new THREE.AmbientLight(0xffffff, 0.9));
        const sunLight = new THREE.DirectionalLight(0xffffff, 1.0);
        sunLight.position.set(8, 12, 10);
        this.scene.add(sunLight);

        this.camera = new THREE.PerspectiveCamera(42, 1, 0.1, 100);
        this.camera.position.z = 6.8;

        this.renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        this.renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
        this.renderer.setSize(240, 240);
        container.appendChild(this.renderer.domElement);

        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);

        container.addEventListener('pointerdown', e => {
            this.isDragging = true;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            try { container.setPointerCapture(e.pointerId); } catch (err) {}
        });

        container.addEventListener('pointermove', e => {
            if (!this.isDragging || !this.rootGroup) return;
            const dx = e.clientX - this.prevX;
            const dy = e.clientY - this.prevY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            this.velX = dx * 0.014;
            this.velY = dy * 0.014;
            this.rootGroup.rotateOnWorldAxis(worldY, this.velX);
            this.rootGroup.rotateOnWorldAxis(worldX, this.velY);
        });

        const endDrag = e => {
            this.isDragging = false;
            try { container.releasePointerCapture(e.pointerId); } catch (err) {}
        };
        container.addEventListener('pointerup', endDrag);
        container.addEventListener('pointercancel', endDrag);
    },

    // Procedural 512x256 High-Resolution Planet Texture Generator
    getPlanetTexture(id) {
        if (this.textureCache.has(id)) return this.textureCache.get(id);
        const cvs = document.createElement('canvas');
        cvs.width = 512;
        cvs.height = 256;
        const ctx = cvs.getContext('2d');

        if (id === 'The Sun') {
            ctx.fillStyle = '#f59e0b';
            ctx.fillRect(0, 0, 512, 256);
            for (let i = 0; i < 400; i++) {
                ctx.fillStyle = i % 2 === 0 ? '#fef08a' : '#f97316';
                ctx.beginPath();
                ctx.arc(Math.random() * 512, Math.random() * 256, 4 + Math.random() * 12, 0, Math.PI * 2);
                ctx.fill();
            }
        } else if (id === 'Mercury') {
            ctx.fillStyle = '#94a3b8';
            ctx.fillRect(0, 0, 512, 256);
            for (let i = 0; i < 90; i++) {
                const cx = Math.random() * 512, cy = Math.random() * 256, r = 4 + Math.random() * 14;
                ctx.fillStyle = '#64748b';
                ctx.beginPath(); ctx.arc(cx, cy, r, 0, Math.PI * 2); ctx.fill();
                ctx.fillStyle = '#cbd5e1';
                ctx.beginPath(); ctx.arc(cx - r * 0.2, cy - r * 0.2, r * 0.35, 0, Math.PI * 2); ctx.fill();
            }
        } else if (id === 'Venus') {
            ctx.fillStyle = '#d97706';
            ctx.fillRect(0, 0, 512, 256);
            for (let y = 0; y < 256; y += 12) {
                ctx.fillStyle = y % 24 === 0 ? '#fef3c7' : '#fbbf24';
                ctx.fillRect(0, y, 512, 10);
            }
        } else if (id === 'Earth') {
            // Blue oceans
            ctx.fillStyle = '#1d4ed8';
            ctx.fillRect(0, 0, 512, 256);
            // Continents
            ctx.fillStyle = '#15803d';
            // Americas
            ctx.beginPath(); ctx.ellipse(120, 100, 45, 60, 0.2, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.ellipse(150, 180, 35, 50, -0.2, 0, Math.PI * 2); ctx.fill();
            // Eurasia & Africa
            ctx.beginPath(); ctx.ellipse(320, 95, 75, 45, 0, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.ellipse(310, 160, 45, 55, 0, 0, Math.PI * 2); ctx.fill();
            // Australia
            ctx.beginPath(); ctx.ellipse(430, 190, 28, 22, 0, 0, Math.PI * 2); ctx.fill();
            // Polar Ice Caps
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, 512, 24);
            ctx.fillRect(0, 232, 512, 24);
        } else if (id === "Earth's Moon") {
            ctx.fillStyle = '#cbd5e1';
            ctx.fillRect(0, 0, 512, 256);
            // Lunar Maria
            ctx.fillStyle = '#475569';
            ctx.beginPath(); ctx.ellipse(180, 110, 65, 45, 0, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.ellipse(310, 120, 75, 50, 0, 0, Math.PI * 2); ctx.fill();
            // Craters
            for (let i = 0; i < 60; i++) {
                ctx.fillStyle = '#ffffff';
                ctx.beginPath(); ctx.arc(Math.random() * 512, Math.random() * 256, 2 + Math.random() * 6, 0, Math.PI * 2); ctx.fill();
            }
        } else if (id === 'Mars') {
            ctx.fillStyle = '#c2410c';
            ctx.fillRect(0, 0, 512, 256);
            // Syrtis Major
            ctx.fillStyle = '#7f1d1d';
            ctx.beginPath(); ctx.ellipse(280, 125, 65, 45, 0.3, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.ellipse(140, 110, 55, 35, 0, 0, Math.PI * 2); ctx.fill();
            // Polar caps
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(0, 0, 512, 16);
            ctx.fillRect(0, 240, 512, 16);
        } else if (id === 'Jupiter') {
            const bands = ['#78350f', '#fde68a', '#c2410c', '#fffbeb', '#ea580c', '#fde68a', '#78350f'];
            for (let i = 0; i < bands.length; i++) {
                ctx.fillStyle = bands[i];
                ctx.fillRect(0, i * 36, 512, 38);
            }
            // Great Red Spot
            ctx.fillStyle = '#fef3c7';
            ctx.beginPath(); ctx.ellipse(330, 155, 42, 24, 0, 0, Math.PI * 2); ctx.fill();
            ctx.fillStyle = '#b91c1c';
            ctx.beginPath(); ctx.ellipse(330, 155, 34, 18, 0, 0, Math.PI * 2); ctx.fill();
            ctx.fillStyle = '#f97316';
            ctx.beginPath(); ctx.ellipse(330, 155, 18, 9, 0, 0, Math.PI * 2); ctx.fill();
        } else if (id === 'Saturn') {
            const sBands = ['#ca8a04', '#eab308', '#fef08a', '#eab308', '#ca8a04'];
            for (let i = 0; i < sBands.length; i++) {
                ctx.fillStyle = sBands[i];
                ctx.fillRect(0, i * 52, 512, 54);
            }
        } else if (id === 'Uranus') {
            ctx.fillStyle = '#38bdf8';
            ctx.fillRect(0, 0, 512, 256);
            ctx.fillStyle = '#7dd3fc';
            ctx.fillRect(0, 100, 512, 56);
        } else if (id === 'Neptune') {
            ctx.fillStyle = '#1d4ed8';
            ctx.fillRect(0, 0, 512, 256);
            // Great Dark Spot
            ctx.fillStyle = '#0f172a';
            ctx.beginPath(); ctx.ellipse(260, 140, 45, 25, 0, 0, Math.PI * 2); ctx.fill();
            // High altitude cirrus streaks
            ctx.fillStyle = '#e0f2fe';
            ctx.fillRect(160, 115, 80, 5);
            ctx.fillRect(290, 85, 95, 6);
        } else if (id === 'Pluto') {
            ctx.fillStyle = '#a8a29e';
            ctx.fillRect(0, 0, 512, 256);
            // Tombaugh Regio Heart
            ctx.fillStyle = '#ffffff';
            ctx.beginPath();
            ctx.ellipse(250, 140, 50, 45, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(300, 140, 45, 40, 0, 0, Math.PI * 2);
            ctx.fill();
        }

        const tex = new THREE.CanvasTexture(cvs);
        this.textureCache.set(id, tex);
        return tex;
    },

    build3DPlanet(item) {
        const group = new THREE.Group();
        const mat = (hex, rough = 0.35, emissive = 0x000000) =>
            new THREE.MeshStandardMaterial({ color: hex, roughness: rough, emissive, emissiveIntensity: emissive ? 0.6 : 0 });

        if (item.id === 'The Sun') {
            const sunGeo = new THREE.SphereGeometry(1.8, 32, 32);
            const sunMat = new THREE.MeshBasicMaterial({ map: this.getPlanetTexture('The Sun') });
            group.add(new THREE.Mesh(sunGeo, sunMat));
            // Corona glow halo
            const coronaGeo = new THREE.SphereGeometry(2.1, 24, 24);
            const coronaMat = new THREE.MeshBasicMaterial({ color: 0xf97316, transparent: true, opacity: 0.28, side: THREE.BackSide });
            group.add(new THREE.Mesh(coronaGeo, coronaMat));
        } else if (item.id === 'Saturn') {
            const planet = new THREE.Mesh(new THREE.SphereGeometry(1.35, 32, 32), new THREE.MeshStandardMaterial({ map: this.getPlanetTexture('Saturn'), roughness: 0.4 }));
            planet.scale.set(1.12, 0.98, 1.12);
            group.add(planet);

            // Realistic textured concentric rings with Cassini division
            const ringCvs = document.createElement('canvas');
            ringCvs.width = 256; ringCvs.height = 1;
            const rCtx = ringCvs.getContext('2d');
            const rGrad = rCtx.createLinearGradient(0, 0, 256, 0);
            rGrad.addColorStop(0.0, 'rgba(0,0,0,0)');
            rGrad.addColorStop(0.2, 'rgba(217, 119, 6, 0.4)'); // C ring
            rGrad.addColorStop(0.38, 'rgba(254, 240, 138, 0.95)'); // B ring
            rGrad.addColorStop(0.68, 'rgba(254, 240, 138, 0.95)');
            rGrad.addColorStop(0.70, 'rgba(0, 0, 0, 0)'); // Cassini division
            rGrad.addColorStop(0.75, 'rgba(202, 138, 4, 0.85)'); // A ring
            rGrad.addColorStop(0.96, 'rgba(202, 138, 4, 0.85)');
            rGrad.addColorStop(1.0, 'rgba(0,0,0,0)');
            rCtx.fillStyle = rGrad;
            rCtx.fillRect(0, 0, 256, 1);
            const ringTex = new THREE.CanvasTexture(ringCvs);

            const ringGeo = new THREE.RingGeometry(1.65, 3.25, 64);
            const ringMat = new THREE.MeshBasicMaterial({ map: ringTex, side: THREE.DoubleSide, transparent: true });
            const ring = new THREE.Mesh(ringGeo, ringMat);
            ring.rotation.x = Math.PI / 2.3;
            group.add(ring);
        } else if (item.id === 'Uranus') {
            const uSphere = new THREE.Mesh(new THREE.SphereGeometry(1.4, 32, 32), new THREE.MeshStandardMaterial({ map: this.getPlanetTexture('Uranus'), roughness: 0.35 }));
            group.add(uSphere);
            // 98-degree axial tilt ring
            const uRing = new THREE.Mesh(
                new THREE.RingGeometry(1.7, 2.3, 48),
                new THREE.MeshBasicMaterial({ color: 0xbae6fd, side: THREE.DoubleSide, transparent: true, opacity: 0.75 })
            );
            uRing.rotation.y = Math.PI * 0.54;
            group.add(uRing);
        } else if (item.id === 'Earth') {
            // Earth surface with realistic continents & oceans
            const earthMesh = new THREE.Mesh(new THREE.SphereGeometry(1.45, 32, 32), new THREE.MeshStandardMaterial({ map: this.getPlanetTexture('Earth'), roughness: 0.4 }));
            group.add(earthMesh);

            // Cloud layer sphere
            const cloudCvs = document.createElement('canvas');
            cloudCvs.width = 512; cloudCvs.height = 256;
            const cCtx = cloudCvs.getContext('2d');
            cCtx.fillStyle = 'rgba(0,0,0,0)';
            cCtx.fillRect(0, 0, 512, 256);
            cCtx.fillStyle = 'rgba(255, 255, 255, 0.65)';
            for (let i = 0; i < 45; i++) {
                cCtx.beginPath();
                cCtx.ellipse(Math.random() * 512, 40 + Math.random() * 176, 30 + Math.random() * 55, 10 + Math.random() * 15, Math.random() * 0.4 - 0.2, 0, Math.PI * 2);
                cCtx.fill();
            }
            const cloudTex = new THREE.CanvasTexture(cloudCvs);
            const cloudMesh = new THREE.Mesh(new THREE.SphereGeometry(1.48, 32, 32), new THREE.MeshStandardMaterial({ map: cloudTex, transparent: true, opacity: 0.55 }));
            group.add(cloudMesh);

            // Orbiting Moon
            const moonPivot = new THREE.Group();
            const moonMesh = new THREE.Mesh(new THREE.SphereGeometry(0.35, 20, 20), new THREE.MeshStandardMaterial({ map: this.getPlanetTexture("Earth's Moon"), roughness: 0.6 }));
            moonMesh.position.x = 2.45;
            moonPivot.add(moonMesh);
            group.add(moonPivot);
        } else if (item.id === 'Asteroid Belt') {
            // Main cratered asteroid Vesta (displaced geometry)
            const vestaGeo = new THREE.DodecahedronGeometry(1.4, 2);
            const pos = vestaGeo.attributes.position;
            for (let i = 0; i < pos.count; i++) {
                const u = pos.getX(i), v = pos.getY(i), w = pos.getZ(i);
                const noise = 1 + (Math.sin(u * 5) * Math.cos(v * 5) * 0.12);
                pos.setXYZ(i, u * noise, v * noise, w * noise);
            }
            vestaGeo.computeVertexNormals();
            const vestaMesh = new THREE.Mesh(vestaGeo, new THREE.MeshStandardMaterial({ color: 0x78716c, roughness: 0.85 }));
            group.add(vestaMesh);

            // 35 tumbling mini-asteroids
            for (let i = 0; i < 35; i++) {
                const mini = new THREE.Mesh(new THREE.DodecahedronGeometry(0.08 + Math.random() * 0.1, 0), new THREE.MeshStandardMaterial({ color: 0xa8a29e, roughness: 0.9 }));
                const angle = (i / 35) * Math.PI * 2;
                const dist = 2.2 + Math.random() * 0.8;
                mini.position.set(Math.cos(angle) * dist, (Math.random() - 0.5) * 0.6, Math.sin(angle) * dist);
                group.add(mini);
            }
        } else if (item.id === 'Pluto') {
            const plutoMesh = new THREE.Mesh(new THREE.SphereGeometry(1.35, 32, 32), new THREE.MeshStandardMaterial({ map: this.getPlanetTexture('Pluto'), roughness: 0.7 }));
            group.add(plutoMesh);

            // Orbiting Charon moon
            const charonPivot = new THREE.Group();
            const charon = new THREE.Mesh(new THREE.SphereGeometry(0.55, 20, 20), new THREE.MeshStandardMaterial({ color: 0x78716c, roughness: 0.8 }));
            charon.position.x = 2.3;
            charonPivot.add(charon);
            group.add(charonPivot);
        } else if (item.id === 'Comet') {
            // Craggy icy nucleus
            const cometGeo = new THREE.DodecahedronGeometry(0.85, 1);
            const comet = new THREE.Mesh(cometGeo, new THREE.MeshStandardMaterial({ color: 0xe0f2fe, roughness: 0.7 }));
            group.add(comet);
            // Glowing cyan coma sphere
            const coma = new THREE.Mesh(new THREE.SphereGeometry(1.3, 24, 24), new THREE.MeshBasicMaterial({ color: 0x38bdf8, transparent: true, opacity: 0.45 }));
            group.add(coma);
            // Dual streaming tails: blue ion tail + golden dust tail
            const ionTail = new THREE.Mesh(new THREE.ConeGeometry(0.65, 3.8, 16), new THREE.MeshBasicMaterial({ color: 0x0284c7, transparent: true, opacity: 0.55 }));
            ionTail.rotation.x = Math.PI / 2;
            ionTail.position.z = -2.1;
            const dustTail = new THREE.Mesh(new THREE.ConeGeometry(1.1, 3.4, 16), new THREE.MeshBasicMaterial({ color: 0xfef08a, transparent: true, opacity: 0.4 }));
            dustTail.rotation.x = Math.PI / 2 + 0.25;
            dustTail.position.set(0.4, 0.4, -2.0);
            group.add(ionTail, dustTail);
        } else if (item.id === 'Galactic Swirl') {
            // Real 3D Spiral Galaxy (1,800 points along 4 logarithmic arms)
            const count = 1800;
            const starGeo = new THREE.BufferGeometry();
            const positions = new Float32Array(count * 3);
            const colors = new Float32Array(count * 3);
            const cCore = new THREE.Color('#fef08a');
            const cArmBlue = new THREE.Color('#38bdf8');
            const cArmPink = new THREE.Color('#f472b6');

            for (let i = 0; i < count; i++) {
                const arm = i % 4;
                const armOffset = (arm * Math.PI * 2) / 4;
                const r = Math.pow(Math.random(), 1.5) * 3.2;
                const theta = r * 2.2 + armOffset;
                const spread = (Math.random() - 0.5) * (0.35 + r * 0.12);
                const x = Math.cos(theta) * r + spread;
                const z = Math.sin(theta) * r + spread;
                const y = (Math.random() - 0.5) * (0.2 + (3.2 - r) * 0.15);

                positions[i * 3] = x;
                positions[i * 3 + 1] = y;
                positions[i * 3 + 2] = z;

                const col = r < 0.8 ? cCore : (i % 2 === 0 ? cArmBlue : cArmPink);
                colors[i * 3] = col.r;
                colors[i * 3 + 1] = col.g;
                colors[i * 3 + 2] = col.b;
            }
            starGeo.setAttribute('position', new THREE.BufferAttribute(positions, 3));
            starGeo.setAttribute('color', new THREE.BufferAttribute(colors, 3));
            const starMat = new THREE.PointsMaterial({ size: 0.08, vertexColors: true, transparent: true, opacity: 0.95 });
            const galaxyPoints = new THREE.Points(starGeo, starMat);
            galaxyPoints.rotation.x = 0.5;
            group.add(galaxyPoints);
        } else {
            // General textured planet (Mercury, Venus, Mars, Jupiter, Neptune, Moon)
            const tex = this.getPlanetTexture(item.id);
            const sphMat = tex
                ? new THREE.MeshStandardMaterial({ map: tex, roughness: 0.4 })
                : mat(item.color);
            group.add(new THREE.Mesh(new THREE.SphereGeometry(1.45, 32, 32), sphMat));
        }
        return group;
    },

    build3DOrbit() {
        const group = new THREE.Group();
        this.orbitEntries = [];

        // 3D Background Starfield
        const starCount = 600;
        const starGeo = new THREE.BufferGeometry();
        const starPos = new Float32Array(starCount * 3);
        for (let i = 0; i < starCount * 3; i += 3) {
            starPos[i] = (Math.random() - 0.5) * 45;
            starPos[i + 1] = (Math.random() - 0.5) * 45;
            starPos[i + 2] = (Math.random() - 0.5) * 45;
        }
        starGeo.setAttribute('position', new THREE.BufferAttribute(starPos, 3));
        const starField = new THREE.Points(starGeo, new THREE.PointsMaterial({ color: 0xffffff, size: 0.09, transparent: true, opacity: 0.75 }));
        group.add(starField);

        // Glowing Sun at center
        const sun = new THREE.Mesh(
            new THREE.SphereGeometry(0.72, 28, 28),
            new THREE.MeshBasicMaterial({ color: '#facc15' })
        );
        group.add(sun);

        const planets = GAMES.solar.filter(p => p.id !== 'The Sun' && p.id !== 'Asteroid Belt' && p.id !== 'Comet' && p.id !== 'Galactic Swirl');
        const rScale = 0.55;

        planets.forEach((p, idx) => {
            const radius = 1.0 + idx * 0.46;

            // Orbit ring line
            const ring = new THREE.Mesh(
                new THREE.RingGeometry(radius - 0.015, radius + 0.015, 64),
                new THREE.MeshBasicMaterial({ color: p.id === this.current.id ? '#facc15' : '#334155', side: THREE.DoubleSide })
            );
            ring.rotation.x = Math.PI / 2;
            group.add(ring);

            // Orbiting planet pivot
            const pivot = new THREE.Group();
            pivot.rotation.y = idx * 1.25;
            const pSize = Math.max(0.12, p.orbitSize * rScale);
            const pMesh = new THREE.Mesh(new THREE.SphereGeometry(pSize, 18, 18), new THREE.MeshStandardMaterial({ color: p.color }));
            pMesh.position.x = radius;

            // Saturn mini-rings in orbit mode
            if (p.id === 'Saturn') {
                const sRing = new THREE.Mesh(new THREE.RingGeometry(pSize * 1.3, pSize * 2.1, 24), new THREE.MeshBasicMaterial({ color: 0xfef08a, side: THREE.DoubleSide, transparent: true, opacity: 0.8 }));
                sRing.rotation.x = Math.PI / 2.4;
                pMesh.add(sRing);
            }

            pivot.add(pMesh);
            group.add(pivot);
            this.orbitEntries.push({ pivot, speed: p.orbitSpeed });
        });

        // Particle Asteroid Belt between Mars & Jupiter (around radius 2.6)
        const beltCount = 140;
        const beltGeo = new THREE.BufferGeometry();
        const beltPos = new Float32Array(beltCount * 3);
        for (let i = 0; i < beltCount; i++) {
            const angle = Math.random() * Math.PI * 2;
            const dist = 2.45 + Math.random() * 0.28;
            beltPos[i * 3] = Math.cos(angle) * dist;
            beltPos[i * 3 + 1] = (Math.random() - 0.5) * 0.12;
            beltPos[i * 3 + 2] = Math.sin(angle) * dist;
        }
        beltGeo.setAttribute('position', new THREE.BufferAttribute(beltPos, 3));
        const beltPoints = new THREE.Points(beltGeo, new THREE.PointsMaterial({ color: 0xa8a29e, size: 0.04 }));
        group.add(beltPoints);

        group.rotation.x = 0.58;
        return group;
    },

    setMode(newMode) {
        this.mode = newMode;
        document.getElementById('solar-mode-photo').classList.toggle('active', newMode === 'photo');
        document.getElementById('solar-mode-planet').classList.toggle('active', newMode === 'planet');
        document.getElementById('solar-mode-orbit').classList.toggle('active', newMode === 'orbit');
        document.getElementById('solar-action-label').textContent = newMode === 'orbit' ? '🚀 Turbo Orbit!' : '🔊 Fun Fact!';
        this.select(this.current, false);
    },

    select(item, speak = true) {
        this.current = item;
        document.getElementById('solar-order-badge').textContent = item.badge;
        document.getElementById('solar-title').textContent = item.id;
        document.getElementById('solar-fact').textContent = item.fact;

        document.querySelectorAll('#solar-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.solarId === item.id);
        });

        const photoContainer = document.getElementById('solar-photo-container');
        const canvasContainer = document.getElementById('solar-canvas-container');

        if (this.mode === 'photo') {
            this.stop();
            photoContainer.classList.remove('hidden');
            canvasContainer.classList.add('hidden');
            const fitClass = (item.id === 'Saturn' || item.id === 'Comet') ? 'object-contain' : 'object-cover';
            const holder = document.getElementById('solar-svg-holder');
            holder.innerHTML = '';
            const img = document.createElement('img');
            img.src = item.photoUrl;
            img.alt = item.id;
            img.className = `w-full h-full ${fitClass} rounded-2xl drop-shadow-xl transition-all duration-300`;
            img.addEventListener('error', () => {
                holder.innerHTML = getSolarSVG(item.id, 'fallback_stage');
            }, { once: true });
            holder.appendChild(img);
            document.getElementById('solar-photo-credit').textContent = item.credit;
            app.animatePop(document.getElementById('solar-stage-box'));
            if (speak && !(app.isOpeningView && !app.settings.announceGameOnOpen)) {
                soundFX.stopAll();
                soundFX.playCosmicChime();
                app.speak(item.speech);
            }
            return;
        }

        photoContainer.classList.add('hidden');
        canvasContainer.classList.remove('hidden');
        this.init3D();

        if (typeof THREE === 'undefined') {
            canvasContainer.innerHTML = `<span class="text-8xl">${item.emoji}</span>`;
            if (speak) app.speak(item.speech);
            return;
        }

        if (this.rootGroup && this.scene) this.scene.remove(this.rootGroup);
        this.rootGroup = this.mode === 'orbit' ? this.build3DOrbit() : this.build3DPlanet(item);
        this.scene.add(this.rootGroup);
        app.animatePop(document.getElementById('solar-stage-box'));

        if (speak && !(app.isOpeningView && !app.settings.announceGameOnOpen)) {
            soundFX.playCosmicChime();
            app.speak(item.speech);
        }
        this.start();
    },

    triggerAction() {
        if (this.mode === 'orbit') {
            this.turboBoost = 4.0;
            soundFX.playCosmicChime();
            app.speak('Zoom! Super fast planet orbits!');
            setTimeout(() => { this.turboBoost = 1; }, 2000);
        } else {
            soundFX.playCosmicChime();
            app.animatePop(document.getElementById('solar-fact'));
            app.speak(this.current.speech);
        }
    },

    start() {
        if (this.animId) return;
        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);
        const loop = () => {
            this.animId = requestAnimationFrame(loop);
            if (document.hidden) return;
            if (this.rootGroup) {
                if (this.mode === 'orbit') {
                    this.orbitEntries.forEach(e => { e.pivot.rotation.y += e.speed * this.turboBoost; });
                } else if (!this.isDragging) {
                    if (typeof app === 'undefined' || !app.settings || app.settings.autoSpin3D) {
                        this.rootGroup.rotateOnWorldAxis(worldY, this.velX);
                        this.rootGroup.rotateOnWorldAxis(worldX, this.velY);
                        this.velX = this.velX * 0.95 + 0.011 * 0.05;
                        this.velY = this.velY * 0.94;
                    }
                }
            }
            if (this.renderer && this.scene && this.camera) {
                this.renderer.render(this.scene, this.camera);
            }
        };
        loop();
    },

    stop() {
        if (this.animId) {
            cancelAnimationFrame(this.animId);
            this.animId = null;
        }
    }
};


// scratch/games.js

const phonicsGame = {
    mode: 'studio',
    currentIndex: 0,
    bubbleTimer: null,
    bubbleSubTimers: [],

    open() {
        this.stopBubbles();
        this.mode = 'studio';
        const pStudio = document.getElementById('phonics-mode-studio');
        const pBubbles = document.getElementById('phonics-mode-bubbles');
        if (pStudio) pStudio.classList.add('active');
        if (pBubbles) pBubbles.classList.remove('active');
        const sStage = document.getElementById('phonics-studio-stage');
        const bStage = document.getElementById('phonics-bubble-stage');
        const cDock = document.getElementById('phonics-controls-dock');
        if (sStage) sStage.classList.remove('hidden');
        if (bStage) bStage.classList.add('hidden');
        if (cDock) cDock.classList.remove('hidden');
        this.selectLetter(this.currentIndex, true);
    },

    setMode(newMode) {
        this.mode = newMode;
        document.getElementById('phonics-mode-studio').classList.toggle('active', newMode === 'studio');
        document.getElementById('phonics-mode-bubbles').classList.toggle('active', newMode === 'bubbles');
        document.getElementById('phonics-studio-stage').classList.toggle('hidden', newMode !== 'studio');
        document.getElementById('phonics-bubble-stage').classList.toggle('hidden', newMode !== 'bubbles');
        document.getElementById('phonics-controls-dock').classList.toggle('hidden', newMode !== 'studio');

        if (newMode === 'bubbles') this.startBubbles();
        else {
            this.stopBubbles();
            this.selectLetter(this.currentIndex, true);
        }
    },

    selectLetter(idx, speakIt = true) {
        this.currentIndex = idx;
        const item = GAMES.phonics[idx];
        document.getElementById('phonics-big-upper').textContent = item.letter;
        document.getElementById('phonics-big-lower').textContent = item.letter.toLowerCase();
        document.getElementById('phonics-sound-pill').textContent = `🔊 "${item.soundSpell}" — ${item.cue}`;
        app.animatePop(document.getElementById('phonics-main-card'));

        document.querySelectorAll('#phonics-controls .tray-btn').forEach((b, i) => {
            b.classList.toggle('selected', i === idx);
        });

        // Words row
        const row = document.getElementById('phonics-words-row');
        row.innerHTML = '';
        const blendBar = document.getElementById('phonics-blend-bar');
        const blendLetters = document.getElementById('phonics-blend-letters');
        if (blendBar) blendBar.classList.add('hidden');

        item.words.forEach(wObj => {
            const wCard = document.createElement('div');
            wCard.className = 'phonics-word-card squish-btn';
            
            // Format letter highlighting
            const hIdx = wObj.highlightIdx !== undefined ? wObj.highlightIdx : 0;
            let formattedWord = '';
            for (let c = 0; c < wObj.w.length; c++) {
                if (c === hIdx) formattedWord += `<span class="text-blue-600 underline font-black">${wObj.w[c]}</span>`;
                else formattedWord += wObj.w[c];
            }

            wCard.innerHTML = `<span class="text-4xl sm:text-5xl mb-1">${wObj.e}</span><span class="font-black text-slate-800 text-base sm:text-lg">${formattedWord}</span>`;
            wCard.addEventListener('click', () => {
                soundFX.playPop();
                app.animatePop(wCard);

                // Update sound-it-out blend bar
                if (blendBar && blendLetters) {
                    blendBar.classList.remove('hidden');
                    blendLetters.innerHTML = `
                        <span class="bg-blue-200 text-blue-900 px-2 py-0.5 rounded-lg">${item.soundSpell}</span>
                        <span>+</span>
                        <span class="bg-blue-100 text-blue-800 px-2 py-0.5 rounded-lg">${wObj.w}</span>
                        <span>=</span>
                        <span class="bg-amber-100 text-amber-900 px-2.5 py-0.5 rounded-lg border border-amber-300">${wObj.w}!</span>
                    `;
                    app.animatePop(blendBar);
                }

                if (typeof app !== 'undefined' && app.settings && app.settings.phonicsDetail === 'simple') {
                    app.speak(`${wObj.w}!`);
                } else {
                    app.speak(`${item.soundSpell}, ${item.soundSpell}, ${wObj.w}!`);
                }
            });
            row.appendChild(wCard);
        });

        if (speakIt) {
            if (typeof app !== 'undefined' && app.settings && app.settings.phonicsDetail === 'simple') {
                app.speak(`${item.letter}! ${item.words[0].w}!`);
            } else {
                app.speak(`${item.letter}! ${item.cue} ${item.soundSpell}, ${item.words[0].w}!`);
            }
        }
    },

    startBubbles() {
        this.stopBubbles();
        this.nextBubbleTarget();
    },

    stopBubbles() {
        if (this.bubbleTimer) {
            clearTimeout(this.bubbleTimer);
            this.bubbleTimer = null;
        }
        if (this.bubbleSubTimers && this.bubbleSubTimers.length > 0) {
            this.bubbleSubTimers.forEach(t => clearTimeout(t));
            this.bubbleSubTimers = [];
        }
        const stage = document.getElementById('phonics-bubbles-canvas');
        if (stage) stage.innerHTML = '';
    },

    nextBubbleTarget() {
        const stage = document.getElementById('phonics-bubbles-canvas');
        if (!stage) return;
        stage.innerHTML = '';

        const targetIdx = Math.floor(Math.random() * GAMES.phonics.length);
        this.currentIndex = targetIdx;
        const targetData = GAMES.phonics[targetIdx];

        document.getElementById('bubble-prompt-emoji').textContent = targetData.words[0].e;
        document.getElementById('bubble-prompt-text').textContent = `Find "${targetData.letter}" (${targetData.soundSpell} for ${targetData.words[0].w})`;
        app.speak(`Pop ${targetData.letter}! ${targetData.cue} ${targetData.words[0].w}!`);

        const indices = [targetIdx];
        while (indices.length < 3) {
            const r = Math.floor(Math.random() * GAMES.phonics.length);
            if (!indices.includes(r)) indices.push(r);
        }
        indices.sort(() => Math.random() - 0.5);

        const palette = ['#ef4444', '#3b82f6', '#10b981', '#f59e0b', '#ec4899', '#8b5cf6'];
        indices.forEach((idx, pos) => {
            const pData = GAMES.phonics[idx];
            const b = document.createElement('div');
            b.className = 'phonics-bubble float-anim';
            const size = Math.min(window.innerWidth * 0.25, 112);
            b.style.width = `${size}px`;
            b.style.height = `${size}px`;
            b.style.backgroundColor = palette[(idx + pos) % palette.length];
            b.style.left = pos === 0 ? '6%' : pos === 1 ? '38%' : '68%';
            b.style.top = pos === 1 ? '44%' : '16%';
            b.innerHTML = `<span class="text-4xl sm:text-5xl leading-none">${pData.letter}${pData.letter.toLowerCase()}</span><span class="text-xl mt-0.5">${pData.words[0].e}</span>`;

            b.addEventListener('click', () => {
                const rect = b.getBoundingClientRect();
                if (idx === targetIdx) {
                    soundFX.playCheer();
                    app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
                    app.speak(`Yay! ${pData.letter} says ${pData.soundSpell}! ${pData.words[0].w}!`);
                    b.style.transform = 'scale(1.35)';
                    b.style.opacity = '0';
                    this.bubbleTimer = setTimeout(() => this.nextBubbleTarget(), 950);
                } else {
                    soundFX.playBubblePop();
                    b.classList.add('shake-anim');
                    app.speak(`That is ${pData.letter}. Find ${targetData.letter}!`);
                    const t = setTimeout(() => b.classList.remove('shake-anim'), 350);
                    this.bubbleSubTimers.push(t);
                }
            });
            stage.appendChild(b);
        });
    }
};

const numberGame = {
    mode: 'touch',
    currentData: GAMES.numbers[0],
    countedSoFar: 0,
    autoTimers: [],

    open() {
        this.clearAutoTimers();
        this.mode = 'touch';
        document.getElementById('num-mode-touch')?.classList.add('active');
        document.getElementById('num-mode-show')?.classList.remove('active');
        this.applyMaxNumberSetting();
        this.select(this.currentData, true);
    },

    applyMaxNumberSetting() {
        const max = (typeof app !== 'undefined' && app.settings && app.settings.maxNumber) ? app.settings.maxNumber : 20;
        document.querySelectorAll('#number-controls .tray-btn').forEach(btn => {
            const num = parseInt(btn.dataset.num, 10);
            if (num > max) {
                btn.style.display = 'none';
            } else {
                btn.style.display = '';
            }
        });
        if (this.currentData && this.currentData.num > max) {
            this.currentData = GAMES.numbers[0];
            if (typeof app !== 'undefined' && app.currentView === 'numbers') {
                this.select(this.currentData, false);
            }
        }
    },

    clearAutoTimers() {
        if (this.autoTimers && this.autoTimers.length > 0) {
            this.autoTimers.forEach(t => clearTimeout(t));
            this.autoTimers = [];
        }
    },

    setMode(newMode) {
        this.clearAutoTimers();
        this.mode = newMode;
        document.getElementById('num-mode-touch').classList.toggle('active', newMode === 'touch');
        document.getElementById('num-mode-show').classList.toggle('active', newMode === 'show');
        this.select(this.currentData, false);
    },

    select(numData, speakIntro = true) {
        this.clearAutoTimers();
        this.currentData = numData;
        this.countedSoFar = 0;

        const digitEl = document.getElementById('number-big-digit');
        const wordEl = document.getElementById('number-word-label');
        const instrEl = document.getElementById('number-instruction');

        digitEl.textContent = numData.num;
        wordEl.textContent = `${numData.word} ${numData.item}`;
        app.animatePop(digitEl);

        document.querySelectorAll('#number-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', parseInt(b.dataset.num, 10) === numData.num);
        });

        const grid = document.getElementById('number-items-grid');
        grid.innerHTML = '';

        let btnWidth = '4.4rem';
        let btnHeight = '4.4rem';
        let btnFont = '2.4rem';
        let btnRadius = '1.35rem';
        let isSmallBadge = false;

        if (numData.num <= 5) {
            btnWidth = '4.4rem';
            btnHeight = '4.4rem';
            btnFont = '2.4rem';
            btnRadius = '1.35rem';
        } else if (numData.num <= 10) {
            btnWidth = '3.35rem';
            btnHeight = '3.35rem';
            btnFont = '1.85rem';
            btnRadius = '1.15rem';
        } else if (numData.num <= 15) {
            btnWidth = '2.85rem';
            btnHeight = '2.85rem';
            btnFont = '1.55rem';
            btnRadius = '1rem';
        } else {
            btnWidth = '2.55rem';
            btnHeight = '2.55rem';
            btnFont = '1.35rem';
            btnRadius = '0.85rem';
            isSmallBadge = true;
        }

        for (let i = 1; i <= numData.num; i++) {
            const itemBtn = document.createElement('div');
            itemBtn.className = 'count-item-btn';
            itemBtn.style.width = btnWidth;
            itemBtn.style.height = btnHeight;
            itemBtn.style.fontSize = btnFont;
            itemBtn.style.borderRadius = btnRadius;
            itemBtn.innerHTML = `<span>${numData.emoji}</span>`;

            itemBtn.addEventListener('click', () => {
                if (itemBtn.classList.contains('counted')) {
                    const badgeNum = itemBtn.querySelector('.count-badge')?.textContent || i;
                    soundFX.playCountStep(parseInt(badgeNum, 10));
                    app.speak(String(badgeNum));
                    return;
                }
                this.countedSoFar++;
                const myCount = this.countedSoFar;
                itemBtn.classList.add('counted');
                const badge = document.createElement('div');
                badge.className = 'count-badge';
                if (isSmallBadge) {
                    badge.style.width = '1.2rem';
                    badge.style.height = '1.2rem';
                    badge.style.fontSize = '0.7rem';
                    badge.style.top = '-5px';
                    badge.style.right = '-5px';
                }
                badge.textContent = myCount;
                itemBtn.appendChild(badge);

                soundFX.playCountStep(myCount);
                this.updateTenFrame(myCount, numData.num);

                if (myCount === numData.num) {
                    instrEl.textContent = `🎉 You counted all ${numData.num} ${numData.item}!`;
                    const rect = itemBtn.getBoundingClientRect();
                    app.burstConfetti(rect.left + 30, rect.top + 30);
                    setTimeout(() => soundFX.playCheer(), 180);
                    app.speak(`${myCount}! Yay! ${numData.word} ${numData.item}!`);
                } else {
                    instrEl.textContent = `Great! Keep tapping: ${myCount} of ${numData.num}`;
                    app.speak(String(myCount));
                }
            });
            grid.appendChild(itemBtn);
        }

        this.updateTenFrame(0, numData.num);

        if (this.mode === 'show') {
            instrEl.textContent = `Counting to ${numData.num}...`;
            this.countAllSequentially();
        } else {
            instrEl.textContent = `Tap each ${numData.emoji} to count! (0/${numData.num})`;
            if (speakIntro) app.speak(`${numData.word}! Tap to count to ${numData.num}!`);
        }
    },

    countAllSequentially() {
        this.clearAutoTimers();
        const freshItems = Array.from(document.querySelectorAll('#number-items-grid .count-item-btn'));
        freshItems.forEach((el, idx) => {
            const t = setTimeout(() => {
                if (app.currentView === 'numbers' && !el.classList.contains('counted')) {
                    el.click();
                }
            }, (idx + 1) * 450);
            this.autoTimers.push(t);
        });
    },

    updateTenFrame(activeCount, total) {
        const tf = document.getElementById('number-ten-frame');
        tf.innerHTML = '';
        const numFrames = total <= 10 ? 1 : 2;

        for (let f = 0; f < numFrames; f++) {
            const frameBox = document.createElement('div');
            frameBox.className = 'grid grid-cols-5 grid-rows-2 gap-1 sm:gap-1.5 p-1.5 bg-teal-50/90 rounded-2xl border-2 border-teal-300 shadow-sm';
            for (let i = 1; i <= 10; i++) {
                const overallIdx = f * 10 + i;
                const cell = document.createElement('div');
                const isFilled = overallIdx <= activeCount;
                const isTarget = overallIdx <= total;

                cell.className = `w-4 h-4 sm:w-5 sm:h-5 rounded-lg flex items-center justify-center font-black text-[9px] transition-all duration-150 ${
                    isFilled
                        ? 'bg-teal-600 text-white shadow-sm scale-105'
                        : isTarget
                        ? 'bg-white border-2 border-dashed border-teal-300 text-teal-300'
                        : 'bg-slate-100 border border-slate-200 opacity-40'
                }`;
                if (isFilled) cell.textContent = overallIdx;
                frameBox.appendChild(cell);
            }
            tf.appendChild(frameBox);
        }
    }
};

const quizGame = {
    category: 'all',
    score: 0,
    currentAnswer: null,
    answered: false,
    nextTimer: null,

    open() {
        this.nextQuestion(true);
    },

    setCategory(cat) {
        if (this.nextTimer) {
            clearTimeout(this.nextTimer);
            this.nextTimer = null;
        }
        this.category = cat;
        document.querySelectorAll('.quiz-cat-btn').forEach(btn => {
            btn.classList.toggle('active', btn.dataset.quizCat === cat);
        });
        this.nextQuestion(false);
    },

    getPool() {
        const lettersPool = GAMES.phonics.map(p => ({
            label: `Letter ${p.letter}`, display: `${p.letter}${p.letter.toLowerCase()}`,
            sub: `${p.words[0].e} ${p.words[0].w}`, prompt: `Can you find the letter ${p.letter}?`
        }));
        const maxNum = (typeof app !== 'undefined' && app.settings && app.settings.maxNumber) ? app.settings.maxNumber : 20;
        const numbersPool = GAMES.numbers.filter(n => n.num <= maxNum).map(n => ({
            label: `Number ${n.num}`, display: `${n.num}`,
            sub: `${n.emoji} ${n.word}`, prompt: `Where is the number ${n.num}?`
        }));
        const animalsPool = GAMES.animals.map(a => ({
            label: a.id, display: a.emoji,
            sub: a.id, prompt: `Can you find the ${a.id}?`
        }));
        const shapesPool = GAMES.shapes.map(s => ({
            label: s.id, display: s.id === 'Circle' ? '🟣' : s.id === 'Square' ? '🟥' : s.id === 'Triangle' ? '🔺' : s.id === 'Star' ? '⭐' : s.id === 'Heart' ? '❤️' : '🔷',
            sub: s.id, prompt: `Can you find the ${s.id}?`
        }));
        const solarPool = GAMES.solar.slice(0, 10).map(s => ({
            label: s.id, display: s.emoji,
            sub: s.id, prompt: `Where is ${s.id}?`
        }));

        if (this.category === 'letters') return lettersPool;
        if (this.category === 'numbers') return numbersPool;
        if (this.category === 'animals') return animalsPool;
        if (this.category === 'shapes') return shapesPool;
        if (this.category === 'solar') return solarPool;
        return [...lettersPool, ...numbersPool, ...animalsPool, ...shapesPool, ...solarPool];
    },

    nextQuestion(isOpening = false) {
        if (this.nextTimer) {
            clearTimeout(this.nextTimer);
            this.nextTimer = null;
        }
        this.answered = false;
        const pool = this.getPool();
        const choices = [...pool].sort(() => Math.random() - 0.5).slice(0, 3);
        const winner = choices[Math.floor(Math.random() * choices.length)];
        this.currentAnswer = winner;

        document.getElementById('quiz-question-text').textContent = `Find: ${winner.label}!`;
        const shouldAnnounce = (typeof app !== 'undefined' && app.settings) ? app.settings.announceGameOnOpen : true;
        const spoken = (isOpening && shouldAnnounce) ? `Look and Find! ${winner.prompt}` : winner.prompt;
        app.speak(spoken);

        const grid = document.getElementById('quiz-choices-grid');
        grid.innerHTML = '';

        choices.forEach(item => {
            const card = document.createElement('div');
            card.className = 'bg-white rounded-3xl p-4 sm:p-6 shadow-md border-4 border-amber-200 flex flex-col items-center justify-center min-h-[145px] cursor-pointer squish-btn';
            card.innerHTML = `<div class="text-5xl sm:text-6xl font-black text-slate-800 mb-2">${item.display}</div><div class="text-xs sm:text-sm font-extrabold text-slate-500 text-center">${item.sub}</div>`;

            card.addEventListener('click', () => {
                if (this.answered && item.label === winner.label) return;

                const rect = card.getBoundingClientRect();
                if (item.label === winner.label) {
                    this.answered = true;
                    this.score++;
                    document.getElementById('quiz-score').textContent = this.score;
                    card.classList.replace('border-amber-200', 'border-emerald-500');
                    card.classList.add('bg-emerald-50');
                    soundFX.playCheer();
                    app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
                    app.speak(`You found it! ${winner.label}!`);
                    this.nextTimer = setTimeout(() => this.nextQuestion(false), 1150);
                } else {
                    soundFX.playNote(220, 0.15, 'sine');
                    card.classList.add('shake-anim');
                    app.speak(`Try to find ${winner.label}!`);
                    setTimeout(() => card.classList.remove('shake-anim'), 350);
                }
            });
            grid.appendChild(card);
        });
    }
};

const shape2DGame = {
    current: GAMES.shapes[0],
    select(s, speak = true) {
        this.current = s;
        const target = document.getElementById('shape-target');
        target.innerHTML = `<svg width="100%" height="100%" viewBox="0 0 100 100">${s.svg}</svg>`;
        document.getElementById('shape-text').textContent = s.id;
        document.getElementById('shape-realworld').textContent = `Looks like: ${s.real}`;
        document.querySelectorAll('#shape-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.shapeId === s.id);
        });
        app.animatePop(target);
        if (speak) app.speak(`${s.id}!`);
    }
};

function createTriangularPrismGeometry(width, height, depth) {
    const shape = new THREE.Shape();
    const w2 = width / 2;
    const h2 = height / 2;
    shape.moveTo(-w2, -h2);
    shape.lineTo(w2, -h2);
    shape.lineTo(0, h2);
    shape.closePath();
    const geo = new THREE.ExtrudeGeometry(shape, { depth: depth, bevelEnabled: false });
    geo.center();
    return geo;
}

function getEarthTexture() {
    const canvas = document.createElement('canvas');
    canvas.width = 512;
    canvas.height = 256;
    const ctx = canvas.getContext('2d');

    // Deep ocean blue
    ctx.fillStyle = '#1d4ed8';
    ctx.fillRect(0, 0, 512, 256);

    // Subtle ocean gradient
    const grad = ctx.createLinearGradient(0, 0, 0, 256);
    grad.addColorStop(0, 'rgba(30, 58, 138, 0.35)');
    grad.addColorStop(0.5, 'rgba(59, 130, 246, 0.25)');
    grad.addColorStop(1, 'rgba(30, 58, 138, 0.35)');
    ctx.fillStyle = grad;
    ctx.fillRect(0, 0, 512, 256);

    const drawLand = (coords, fillColor, strokeColor) => {
        ctx.beginPath();
        ctx.moveTo(coords[0][0], coords[0][1]);
        for (let i = 1; i < coords.length; i++) ctx.lineTo(coords[i][0], coords[i][1]);
        ctx.closePath();
        ctx.fillStyle = fillColor;
        ctx.fill();
        if (strokeColor) {
            ctx.strokeStyle = strokeColor;
            ctx.lineWidth = 1.5;
            ctx.stroke();
        }
    };

    // North America
    drawLand([[40, 50], [90, 42], [140, 48], [150, 75], [130, 95], [115, 115], [95, 135], [75, 125], [60, 100], [35, 75]], '#22c55e', '#15803d');
    drawLand([[105, 105], [118, 108], [114, 122], [102, 115]], '#15803d');
    // Greenland
    drawLand([[175, 30], [210, 28], [205, 52], [178, 48]], '#f8fafc', '#93c5fd');
    // South America
    drawLand([[105, 135], [145, 150], [155, 185], [135, 230], [118, 235], [108, 190], [98, 150]], '#15803d', '#166534');
    drawLand([[115, 155], [140, 160], [135, 185], [115, 175]], '#22c55e');

    // Europe
    drawLand([[230, 60], [275, 55], [285, 75], [260, 95], [235, 90], [225, 72]], '#22c55e', '#166534');
    drawLand([[220, 65], [230, 62], [228, 75], [218, 72]], '#22c55e');

    // Africa
    drawLand([[230, 95], [285, 95], [305, 140], [285, 205], [255, 215], [235, 175], [215, 125]], '#16a34a', '#14532d');
    // Sahara Desert
    drawLand([[235, 100], [290, 100], [295, 125], [225, 128]], '#eab308');
    drawLand([[310, 180], [318, 185], [312, 205], [305, 195]], '#22c55e');

    // Asia
    drawLand([[280, 55], [420, 50], [450, 75], [440, 115], [380, 120], [350, 150], [330, 130], [315, 145], [295, 120], [285, 80]], '#16a34a', '#14532d');
    drawLand([[295, 115], [320, 118], [318, 138], [298, 132]], '#eab308');
    drawLand([[330, 125], [352, 130], [342, 160], [332, 148]], '#22c55e');
    drawLand([[435, 85], [445, 95], [438, 110]], '#22c55e');

    // Australia
    drawLand([[390, 175], [445, 170], [450, 205], [425, 225], [385, 210]], '#16a34a', '#14532d');
    drawLand([[402, 182], [435, 180], [432, 205], [400, 200]], '#eab308');
    drawLand([[460, 215], [470, 230], [458, 235]], '#22c55e');

    // Antarctica
    ctx.fillStyle = '#ffffff';
    ctx.beginPath();
    ctx.ellipse(256, 252, 260, 16, 0, 0, Math.PI * 2);
    ctx.fill();

    // North Polar Ice Cap
    ctx.beginPath();
    ctx.ellipse(256, 4, 230, 12, 0, 0, Math.PI * 2);
    ctx.fill();

    const tex = new THREE.CanvasTexture(canvas);
    tex.wrapS = THREE.RepeatWrapping;
    tex.wrapT = THREE.ClampToEdgeWrapping;
    return tex;
}

function getCloudTexture() {
    const canvas = document.createElement('canvas');
    canvas.width = 512;
    canvas.height = 256;
    const ctx = canvas.getContext('2d');
    ctx.clearRect(0, 0, 512, 256);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.75)';

    const drawCloud = (cx, cy, rx, ry, rot) => {
        ctx.save();
        ctx.translate(cx, cy);
        ctx.rotate(rot);
        ctx.beginPath();
        ctx.ellipse(0, 0, rx, ry, 0, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
    };
    [[80, 80, 60, 14, 0.1], [160, 95, 75, 16, -0.08], [280, 75, 90, 18, 0.12],
     [400, 90, 70, 15, -0.1], [120, 170, 80, 16, -0.15], [260, 165, 85, 17, 0.1],
     [370, 175, 75, 16, -0.05], [50, 210, 55, 12, 0.2], [220, 45, 65, 14, -0.1],
     [340, 215, 60, 14, 0.15], [460, 60, 50, 12, 0.05]].forEach(([x, y, rx, ry, rot]) => {
        drawCloud(x, y, rx, ry, rot);
    });

    return new THREE.CanvasTexture(canvas);
}

function getIglooTexture() {
    const canvas = document.createElement('canvas');
    canvas.width = 512;
    canvas.height = 256;
    const ctx = canvas.getContext('2d');
    ctx.fillStyle = '#f8fafc';
    ctx.fillRect(0, 0, 512, 256);

    const rows = 8;
    const rowH = 256 / rows;
    ctx.strokeStyle = '#93c5fd';
    ctx.lineWidth = 3;

    for (let r = 0; r <= rows; r++) {
        const y = r * rowH;
        ctx.beginPath();
        ctx.moveTo(0, y);
        ctx.lineTo(512, y);
        ctx.stroke();

        if (r < rows) {
            const cols = 12;
            const colW = 512 / cols;
            const offset = (r % 2) * (colW / 2);
            for (let c = 0; c <= cols; c++) {
                const x = c * colW + offset;
                ctx.beginPath();
                ctx.moveTo(x % 512, y);
                ctx.lineTo(x % 512, y + rowH);
                ctx.stroke();
            }
        }
    }
    return new THREE.CanvasTexture(canvas);
}

const shapes3DGame = {
    scene: null, camera: null, renderer: null, mesh: null, animId: null,
    isDragging: false, prevX: 0, prevY: 0, velX: 0.012, velY: 0.004, time: 0,
    currentShape: GAMES.shapes3d[0],
    currentExampleId: 'pure',

    init() {
        if (this.renderer || typeof THREE === 'undefined') return;
        const container = document.getElementById('shape3d-canvas-container');
        if (!container) return;
        container.innerHTML = '';

        this.scene = new THREE.Scene();
        this.scene.add(new THREE.AmbientLight(0xffffff, 0.85));
        const dirLight = new THREE.DirectionalLight(0xffffff, 0.95);
        dirLight.position.set(8, 16, 12);
        this.scene.add(dirLight);

        this.camera = new THREE.PerspectiveCamera(42, 1, 0.1, 100);
        this.camera.position.z = 7.0;

        this.renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        this.renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
        this.renderer.setSize(230, 230);
        container.appendChild(this.renderer.domElement);

        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);

        container.addEventListener('pointerdown', e => {
            this.isDragging = true;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            try { container.setPointerCapture(e.pointerId); } catch (err) {}
        });

        container.addEventListener('pointermove', e => {
            if (!this.isDragging || !this.mesh) return;
            const dx = e.clientX - this.prevX;
            const dy = e.clientY - this.prevY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            this.velX = dx * 0.014;
            this.velY = dy * 0.014;
            this.mesh.rotateOnWorldAxis(worldY, this.velX);
            this.mesh.rotateOnWorldAxis(worldX, this.velY);
        });

        const endDrag = e => {
            this.isDragging = false;
            try { container.releasePointerCapture(e.pointerId); } catch (err) {}
        };
        container.addEventListener('pointerup', endDrag);
        container.addEventListener('pointercancel', endDrag);
    },

    buildModel(shapeItem, exampleId) {
        const group = new THREE.Group();
        const mat = (hex, rough = 0.3) => new THREE.MeshStandardMaterial({ color: hex, roughness: rough, metalness: 0.08 });

        if (exampleId === 'gift') {
            group.add(new THREE.Mesh(new THREE.BoxGeometry(2.2, 2.2, 2.2), mat('#ef4444')));
            group.add(new THREE.Mesh(new THREE.BoxGeometry(2.24, 2.24, 0.45), mat('#facc15')));
            group.add(new THREE.Mesh(new THREE.BoxGeometry(0.45, 2.24, 2.24), mat('#facc15')));
            const bow = new THREE.Mesh(new THREE.TorusGeometry(0.35, 0.12, 12, 24), mat('#facc15'));
            bow.position.y = 1.35;
            bow.rotation.x = Math.PI / 2;
            group.add(bow);
            return group;
        }

        if (exampleId === 'dice') {
            group.add(new THREE.Mesh(new THREE.BoxGeometry(2.1, 2.1, 2.1), mat('#ffffff', 0.2)));
            const pipMat = mat('#1e293b', 0.1);
            const addPip = (x, y, z) => {
                const pip = new THREE.Mesh(new THREE.SphereGeometry(0.12, 10, 10), pipMat);
                pip.position.set(x, y, z);
                group.add(pip);
            };
            addPip(0, 0, 1.07);
            [-0.45, 0.45].forEach(dx => {
                [-0.55, 0, 0.55].forEach(dy => addPip(dx, dy, -1.07));
            });
            addPip(-0.45, 1.07, -0.45);
            addPip(0.45, 1.07, 0.45);
            addPip(0, -1.07, 0);
            [-0.45, 0.45].forEach(dx => [-0.45, 0.45].forEach(dz => addPip(dx, -1.07, dz)));
            addPip(1.07, -0.45, -0.45);
            addPip(1.07, 0, 0);
            addPip(1.07, 0.45, 0.45);
            [-0.45, 0.45].forEach(dy => [-0.45, 0.45].forEach(dz => addPip(-1.07, dy, dz)));
            return group;
        }

        if (exampleId === 'earth') {
            const earthMat = new THREE.MeshStandardMaterial({
                map: getEarthTexture(),
                roughness: 0.45,
                metalness: 0.05
            });
            const earthMesh = new THREE.Mesh(new THREE.SphereGeometry(1.68, 36, 36), earthMat);
            group.add(earthMesh);

            const cloudMat = new THREE.MeshStandardMaterial({
                map: getCloudTexture(),
                transparent: true,
                opacity: 0.38,
                roughness: 0.9,
                depthWrite: false
            });
            const cloudMesh = new THREE.Mesh(new THREE.SphereGeometry(1.72, 32, 32), cloudMat);
            group.add(cloudMesh);

            const haloMat = new THREE.MeshBasicMaterial({
                color: 0x60a5fa,
                transparent: true,
                opacity: 0.15,
                side: THREE.BackSide
            });
            const haloMesh = new THREE.Mesh(new THREE.SphereGeometry(1.82, 28, 28), haloMat);
            group.add(haloMesh);
            return group;
        }

        if (exampleId === 'snowman') {
            const b1 = new THREE.Mesh(new THREE.SphereGeometry(1.25, 24, 24), mat('#ffffff'));
            b1.position.y = -0.75;
            const b2 = new THREE.Mesh(new THREE.SphereGeometry(0.85, 24, 24), mat('#ffffff'));
            b2.position.y = 0.85;
            const nose = new THREE.Mesh(new THREE.ConeGeometry(0.18, 0.7, 12), mat('#f97316'));
            nose.rotation.x = Math.PI / 2;
            nose.position.set(0, 0.85, 0.95);
            group.add(b1, b2, nose);
            return group;
        }

        if (exampleId === 'trafficcone') {
            const cone = new THREE.Mesh(new THREE.ConeGeometry(1.2, 2.6, 32), mat('#f97316', 0.3));
            cone.position.y = 0.1;
            group.add(cone);
            const s1 = new THREE.Mesh(new THREE.CylinderGeometry(0.42, 0.62, 0.42, 32), mat('#ffffff', 0.2));
            s1.position.y = 0.52;
            const s2 = new THREE.Mesh(new THREE.CylinderGeometry(0.75, 0.95, 0.42, 32), mat('#ffffff', 0.2));
            s2.position.y = -0.22;
            group.add(s1, s2);
            const base = new THREE.Mesh(new THREE.BoxGeometry(2.1, 0.18, 2.1), mat('#ea580c', 0.4));
            base.position.y = -1.15;
            group.add(base);
            return group;
        }

        if (exampleId === 'partyhat') {
            const canvas = document.createElement('canvas');
            canvas.width = 256; canvas.height = 256;
            const pCtx = canvas.getContext('2d');
            pCtx.fillStyle = '#8b5cf6';
            pCtx.fillRect(0, 0, 256, 256);
            pCtx.fillStyle = '#ec4899';
            for (let i = -256; i < 512; i += 40) {
                pCtx.beginPath();
                pCtx.moveTo(i, 0); pCtx.lineTo(i + 24, 0); pCtx.lineTo(i + 24 + 120, 256); pCtx.lineTo(i + 120, 256);
                pCtx.fill();
            }
            const dotColors = ['#fde047', '#38bdf8', '#4ade80', '#ffffff'];
            for (let y = 20; y < 256; y += 45) {
                for (let x = 20; x < 256; x += 45) {
                    pCtx.beginPath();
                    pCtx.arc(x, y, 7, 0, Math.PI * 2);
                    pCtx.fillStyle = dotColors[(x + y) % dotColors.length];
                    pCtx.fill();
                }
            }
            const hatTex = new THREE.CanvasTexture(canvas);
            const hatMat = new THREE.MeshStandardMaterial({ map: hatTex, roughness: 0.35 });
            const cone = new THREE.Mesh(new THREE.ConeGeometry(1.35, 2.6, 32), hatMat);
            group.add(cone);

            const trim = new THREE.Mesh(new THREE.TorusGeometry(1.35, 0.08, 12, 32), mat('#38bdf8', 0.2));
            trim.rotation.x = Math.PI / 2;
            trim.position.y = -1.3;
            group.add(trim);

            const pom = new THREE.Mesh(new THREE.SphereGeometry(0.32, 16, 16), mat('#facc15', 0.6));
            pom.position.y = 1.38;
            group.add(pom);
            [['#ec4899', 0.12, 1.45, 0], ['#38bdf8', -0.1, 1.42, 0.08], ['#22c55e', 0.05, 1.44, -0.1]].forEach(([col, x, y, z]) => {
                const tuft = new THREE.Mesh(new THREE.SphereGeometry(0.14, 10, 10), mat(col, 0.6));
                tuft.position.set(x, y, z);
                group.add(tuft);
            });
            return group;
        }

        if (exampleId === 'drum') {
            const body = new THREE.Mesh(new THREE.CylinderGeometry(1.4, 1.4, 1.7, 24), mat('#ef4444'));
            const rim1 = new THREE.Mesh(new THREE.TorusGeometry(1.42, 0.08, 10, 24), mat('#facc15'));
            rim1.rotation.x = Math.PI / 2;
            rim1.position.y = 0.85;
            const rim2 = new THREE.Mesh(new THREE.TorusGeometry(1.42, 0.08, 10, 24), mat('#facc15'));
            rim2.rotation.x = Math.PI / 2;
            rim2.position.y = -0.85;
            const skinTop = new THREE.Mesh(new THREE.CircleGeometry(1.4, 24), mat('#fef3c7'));
            skinTop.rotation.x = -Math.PI / 2;
            skinTop.position.y = 0.86;
            const skinBottom = new THREE.Mesh(new THREE.CircleGeometry(1.4, 24), mat('#fef3c7'));
            skinBottom.rotation.x = Math.PI / 2;
            skinBottom.position.y = -0.86;
            const stickGeo = new THREE.CylinderGeometry(0.06, 0.04, 1.9, 12);
            const tipGeo = new THREE.SphereGeometry(0.11, 12, 12);
            const s1 = new THREE.Mesh(stickGeo, mat('#d97706'));
            s1.rotation.set(Math.PI / 2, 0, 0.45);
            s1.position.set(-0.15, 0.96, 0);
            const t1 = new THREE.Mesh(tipGeo, mat('#fef3c7'));
            t1.position.set(0.25, 0.96, 0.82);
            const s2 = new THREE.Mesh(stickGeo, mat('#d97706'));
            s2.rotation.set(Math.PI / 2, 0, -0.45);
            s2.position.set(0.15, 1.04, 0);
            const t2 = new THREE.Mesh(tipGeo, mat('#fef3c7'));
            t2.position.set(-0.25, 1.04, 0.82);
            group.add(body, rim1, rim2, skinTop, skinBottom, s1, t1, s2, t2);
            return group;
        }

        if (exampleId === 'cake') {
            const base = new THREE.Mesh(new THREE.CylinderGeometry(1.6, 1.6, 1.2, 24), mat('#f472b6'));
            base.position.y = -0.4;
            const candle = new THREE.Mesh(new THREE.CylinderGeometry(0.14, 0.14, 0.9, 12), mat('#ffffff'));
            candle.position.y = 0.65;
            const flame = new THREE.Mesh(new THREE.SphereGeometry(0.2, 12, 12), mat('#facc15'));
            flame.position.y = 1.2;
            group.add(base, candle, flame);
            return group;
        }

        if (exampleId === 'donut') {
            const dough = new THREE.Mesh(new THREE.TorusGeometry(1.3, 0.52, 24, 48), mat('#d97706', 0.5));
            group.add(dough);
            const icing = new THREE.Mesh(new THREE.TorusGeometry(1.3, 0.54, 18, 48), mat('#ec4899', 0.2));
            icing.position.z = 0.09;
            icing.scale.set(1.0, 1.0, 0.6);
            group.add(icing);
            const sprinkleColors = ['#fde047', '#38bdf8', '#ffffff', '#a855f7', '#22c55e'];
            for (let i = 0; i < 28; i++) {
                const angle = (i / 28) * Math.PI * 2;
                const r = 1.15 + (i % 3) * 0.15;
                const sp = new THREE.Mesh(new THREE.CylinderGeometry(0.04, 0.04, 0.22, 6), mat(sprinkleColors[i % sprinkleColors.length]));
                sp.position.set(Math.cos(angle) * r, Math.sin(angle) * r, 0.58);
                sp.rotation.z = Math.random() * Math.PI;
                sp.rotation.x = Math.PI / 2;
                group.add(sp);
            }
            return group;
        }

        if (exampleId === 'lifering') {
            const ring = new THREE.Mesh(new THREE.TorusGeometry(1.35, 0.48, 24, 48), mat('#ef4444'));
            group.add(ring);
            [0, Math.PI / 2, Math.PI, (Math.PI * 3) / 2].forEach(angle => {
                const stripe = new THREE.Mesh(new THREE.TorusGeometry(1.36, 0.49, 12, 8, 0.35), mat('#ffffff'));
                stripe.rotation.z = angle - 0.17;
                group.add(stripe);
            });
            return group;
        }

        if (exampleId === 'egypt') {
            group.add(new THREE.Mesh(new THREE.ConeGeometry(2.0, 2.6, 4), mat('#eab308', 0.6)));
            return group;
        }

        if (exampleId === 'tree') {
            const t1 = new THREE.Mesh(new THREE.ConeGeometry(1.6, 2.2, 6), mat('#16a34a'));
            t1.position.y = 0.3;
            const trunk = new THREE.Mesh(new THREE.CylinderGeometry(0.35, 0.35, 1.1, 12), mat('#78350f'));
            trunk.position.y = -1.1;
            group.add(t1, trunk);
            return group;
        }

        if (exampleId === 'juice') {
            group.add(new THREE.Mesh(new THREE.BoxGeometry(1.6, 2.5, 1.1), mat('#22c55e')));
            const straw = new THREE.Mesh(new THREE.CylinderGeometry(0.08, 0.08, 1.0, 10), mat('#facc15'));
            straw.position.set(0.35, 1.5, 0);
            group.add(straw);
            return group;
        }

        if (exampleId === 'bus') {
            // Yellow body
            const body = new THREE.Mesh(new THREE.BoxGeometry(2.8, 1.4, 1.3), mat('#facc15'));
            group.add(body);
            // 4 Black wheels with rims
            const wheelMat = mat('#1e293b', 0.8);
            const rimMat = mat('#cbd5e1', 0.2);
            [[-0.9, -0.65], [0.9, -0.65]].forEach(([x, y]) => {
                [-0.7, 0.7].forEach(z => {
                    const w = new THREE.Mesh(new THREE.CylinderGeometry(0.34, 0.34, 0.2, 16), wheelMat);
                    w.rotation.x = Math.PI / 2;
                    w.position.set(x, y, z);
                    const rim = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.16, 0.22, 10), rimMat);
                    rim.rotation.x = Math.PI / 2;
                    rim.position.set(x, y, z);
                    group.add(w, rim);
                });
            });
            // Windows
            const winMat = mat('#38bdf8', 0.2);
            const windshield = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.6, 1.1), winMat);
            windshield.position.set(1.42, 0.2, 0);
            const rearWin = new THREE.Mesh(new THREE.BoxGeometry(0.05, 0.5, 1.1), winMat);
            rearWin.position.set(-1.42, 0.2, 0);
            group.add(windshield, rearWin);
            // Headlights
            const headL = new THREE.Mesh(new THREE.SphereGeometry(0.14, 10, 10), mat('#ffffff'));
            headL.position.set(1.42, -0.2, 0.45);
            const headR = new THREE.Mesh(new THREE.SphereGeometry(0.14, 10, 10), mat('#ffffff'));
            headR.position.set(1.42, -0.2, -0.45);
            group.add(headL, headR);
            return group;
        }

        if (exampleId === 'tent') {
            const canvas = document.createElement('canvas');
            canvas.width = 256; canvas.height = 256;
            const tCtx = canvas.getContext('2d');
            tCtx.fillStyle = '#f97316';
            tCtx.fillRect(0, 0, 256, 256);
            tCtx.fillStyle = '#fbbf24';
            for (let x = 0; x < 256; x += 32) {
                tCtx.fillRect(x, 0, 16, 256);
            }
            const tentTex = new THREE.CanvasTexture(canvas);
            const tentMat = new THREE.MeshStandardMaterial({ map: tentTex, roughness: 0.45 });

            const tentGeo = createTriangularPrismGeometry(2.5, 2.1, 2.7);
            const tentBody = new THREE.Mesh(tentGeo, tentMat);
            group.add(tentBody);

            const matMesh = new THREE.Mesh(new THREE.BoxGeometry(2.9, 0.12, 3.1), mat('#15803d', 0.6));
            matMesh.position.y = -1.1;
            group.add(matMesh);

            const pole = new THREE.Mesh(new THREE.CylinderGeometry(0.06, 0.06, 3.0, 12), mat('#78350f', 0.5));
            pole.rotation.x = Math.PI / 2;
            pole.position.y = 1.05;
            group.add(pole);

            const doorShape = new THREE.Shape();
            doorShape.moveTo(-0.55, -1.05);
            doorShape.lineTo(0.55, -1.05);
            doorShape.lineTo(0, 0.35);
            doorShape.closePath();
            const door = new THREE.Mesh(new THREE.ShapeGeometry(doorShape), mat('#451a03'));
            door.position.set(0, 0, 1.36);
            group.add(door);

            const flapL = new THREE.Mesh(new THREE.CylinderGeometry(0.08, 0.08, 1.2, 10), mat('#ea580c', 0.4));
            flapL.position.set(-0.62, -0.45, 1.37);
            flapL.rotation.z = -0.35;
            const flapR = new THREE.Mesh(new THREE.CylinderGeometry(0.08, 0.08, 1.2, 10), mat('#ea580c', 0.4));
            flapR.position.set(0.62, -0.45, 1.37);
            flapR.rotation.z = 0.35;
            group.add(flapL, flapR);

            return group;
        }

        if (exampleId === 'cheese') {
            const cheeseShape = new THREE.Shape();
            cheeseShape.moveTo(-1.2, -1.0);
            cheeseShape.lineTo(1.5, -1.0);
            cheeseShape.lineTo(-1.2, 1.2);
            cheeseShape.closePath();
            const cheeseGeo = new THREE.ExtrudeGeometry(cheeseShape, {
                depth: 1.5,
                bevelEnabled: true,
                bevelThickness: 0.06,
                bevelSize: 0.06,
                bevelSegments: 3
            });
            cheeseGeo.center();
            const cheeseBody = new THREE.Mesh(cheeseGeo, mat('#facc15', 0.35));
            group.add(cheeseBody);

            const holeMat = mat('#ca8a04', 0.5);
            [
                [0.4, 0.25, 0.77], [-0.5, -0.2, 0.77], [0.1, -0.4, 0.77],
                [0.4, 0.25, -0.77], [-0.5, -0.2, -0.77],
                [-1.27, 0.3, 0.2], [-1.27, -0.4, -0.2],
                [0.2, -1.07, 0.3], [-0.4, -1.07, -0.3]
            ].forEach(([x, y, z]) => {
                const hole = new THREE.Mesh(new THREE.SphereGeometry(0.18, 12, 12), holeMat);
                hole.position.set(x, y, z);
                group.add(hole);
            });
            return group;
        }

        if (exampleId === 'gem') {
            group.add(new THREE.Mesh(new THREE.OctahedronGeometry(1.9, 0), mat('#38bdf8', 0.15)));
            return group;
        }

        if (exampleId === 'igloo') {
            const iglooTex = getIglooTexture();
            const iglooMat = new THREE.MeshStandardMaterial({ map: iglooTex, roughness: 0.5 });
            const dome = new THREE.Mesh(new THREE.SphereGeometry(1.65, 32, 20, 0, Math.PI * 2, 0, Math.PI / 2), iglooMat);
            dome.position.y = -0.55;
            const base = new THREE.Mesh(new THREE.CylinderGeometry(1.85, 1.95, 0.18, 32), mat('#f1f5f9', 0.6));
            base.position.y = -0.64;
            group.add(dome, base);

            const archShape = new THREE.Shape();
            archShape.moveTo(-0.62, 0);
            archShape.lineTo(-0.62, 0.08);
            archShape.absarc(0, 0.08, 0.62, Math.PI, 0, true);
            archShape.lineTo(0.62, 0);
            archShape.closePath();
            const tunnelGeo = new THREE.ExtrudeGeometry(archShape, { depth: 1.15, bevelEnabled: false });
            const tunnel = new THREE.Mesh(tunnelGeo, iglooMat);
            tunnel.position.set(0, -0.55, 0.70);
            group.add(tunnel);

            const doorShape = new THREE.Shape();
            doorShape.moveTo(-0.48, 0);
            doorShape.lineTo(-0.48, 0.06);
            doorShape.absarc(0, 0.06, 0.48, Math.PI, 0, true);
            doorShape.lineTo(0.48, 0);
            doorShape.closePath();
            const door = new THREE.Mesh(new THREE.ShapeGeometry(doorShape), mat('#1e3a8a', 0.3));
            door.position.set(0, -0.55, 1.86);
            group.add(door);

            const rimShape = new THREE.Shape();
            rimShape.moveTo(-0.62, 0);
            rimShape.lineTo(-0.62, 0.08);
            rimShape.absarc(0, 0.08, 0.62, Math.PI, 0, true);
            rimShape.lineTo(0.62, 0);
            rimShape.lineTo(0.48, 0);
            rimShape.lineTo(0.48, 0.06);
            rimShape.absarc(0, 0.06, 0.48, 0, Math.PI, false);
            rimShape.lineTo(-0.48, 0);
            rimShape.closePath();
            const rimGeo = new THREE.ExtrudeGeometry(rimShape, { depth: 0.08, bevelEnabled: true, bevelThickness: 0.03, bevelSize: 0.03, bevelSegments: 2 });
            const rimMesh = new THREE.Mesh(rimGeo, mat('#e2e8f0', 0.4));
            rimMesh.position.set(0, -0.55, 1.85);
            group.add(rimMesh);

            return group;
        }

        if (exampleId === 'mushroom') {
            const cap = new THREE.Mesh(new THREE.SphereGeometry(1.6, 24, 16, 0, Math.PI * 2, 0, Math.PI / 2), mat('#ef4444'));
            cap.position.y = 0.2;
            const capBottom = new THREE.Mesh(new THREE.CircleGeometry(1.6, 24), mat('#fef3c7'));
            capBottom.rotation.x = Math.PI / 2;
            capBottom.position.y = 0.2;
            group.add(cap, capBottom);
            const spotMat = mat('#ffffff');
            [[0, 1.7, 0], [0.8, 1.2, 0.6], [-0.8, 1.2, 0.6], [0, 1.2, -0.9], [1.1, 0.6, -0.4], [-1.1, 0.6, -0.4]].forEach(([x, y, z]) => {
                const spot = new THREE.Mesh(new THREE.SphereGeometry(0.22, 10, 10), spotMat);
                spot.position.set(x, y, z);
                group.add(spot);
            });
            const stem = new THREE.Mesh(new THREE.CylinderGeometry(0.55, 0.68, 1.4, 18), mat('#fef3c7'));
            stem.position.y = -0.5;
            group.add(stem);
            return group;
        }

        if (exampleId === 'pure' && shapeItem.id === 'Prism') {
            const geo = createTriangularPrismGeometry(2.4, 2.1, 2.6);
            group.add(new THREE.Mesh(geo, mat('#14b8a6', 0.3)));
            const edges = new THREE.LineSegments(new THREE.EdgesGeometry(geo), new THREE.LineBasicMaterial({ color: 0x0f766e, linewidth: 2 }));
            group.add(edges);
            return group;
        }

        let geo;
        switch (shapeItem.id) {
            case 'Cube': geo = new THREE.BoxGeometry(2.2, 2.2, 2.2); break;
            case 'Sphere': geo = new THREE.SphereGeometry(1.75, 28, 28); break;
            case 'Cone': geo = new THREE.ConeGeometry(1.65, 2.9, 28); break;
            case 'Cylinder': geo = new THREE.CylinderGeometry(1.35, 1.35, 2.7, 28); break;
            case 'Pyramid': geo = new THREE.ConeGeometry(1.9, 2.8, 4); break;
            case 'Cuboid (Box)': geo = new THREE.BoxGeometry(1.7, 2.6, 1.3); break;
            case 'Prism': geo = createTriangularPrismGeometry(2.4, 2.1, 2.6); break;
            case 'Diamond (Octahedron)': geo = new THREE.OctahedronGeometry(1.9, 0); break;
            case 'Dome (Hemisphere)': {
                const domeMesh = new THREE.Mesh(new THREE.SphereGeometry(1.75, 28, 16, 0, Math.PI * 2, 0, Math.PI / 2), mat(shapeItem.color));
                domeMesh.position.y = -0.5;
                const flatCap = new THREE.Mesh(new THREE.CircleGeometry(1.75, 28), mat(shapeItem.color));
                flatCap.rotation.x = Math.PI / 2;
                flatCap.position.y = -0.5;
                group.add(domeMesh, flatCap);
                return group;
            }
            default: geo = new THREE.TorusGeometry(1.3, 0.52, 22, 48); break;
        }
        group.add(new THREE.Mesh(geo, mat(shapeItem.color)));
        return group;
    },

    select(item, speak = true, exampleId = 'pure') {
        this.currentShape = item;
        this.currentExampleId = exampleId;

        document.getElementById('shape3d-text').textContent = item.id;
        document.getElementById('shape3d-realworld').textContent = item.real;

        document.querySelectorAll('#shape3d-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.shape3dId === item.id);
        });

        const exBar = document.getElementById('shape3d-examples-bar');
        exBar.innerHTML = '';
        (item.examples || []).forEach(ex => {
            const pill = document.createElement('button');
            const active = ex.id === exampleId;
            pill.className = `px-3 py-1 rounded-full font-black text-xs sm:text-sm border-2 squish-btn flex items-center gap-1 ${
                active ? 'bg-indigo-600 text-white border-indigo-600 shadow' : 'bg-white text-slate-700 border-indigo-200'
            }`;
            pill.innerHTML = `<span>${ex.emoji}</span><span>${ex.label}</span>`;
            pill.addEventListener('click', () => {
                soundFX.playPop();
                this.select(item, true, ex.id);
            });
            exBar.appendChild(pill);
        });

        app.animatePop(document.getElementById('shape3d-target'));
        if (speak) {
            const exObj = (item.examples || []).find(e => e.id === exampleId);
            const speakName = exObj && exObj.id !== 'pure' ? `${exObj.label}! A 3D ${item.id}!` : `${item.id}! ${item.real}`;
            app.speak(speakName);
        }

        this.init();
        if (typeof THREE === 'undefined') return;

        if (this.mesh && this.scene) this.scene.remove(this.mesh);
        this.mesh = this.buildModel(item, exampleId);
        this.mesh.rotation.x = 0.45;
        this.mesh.rotation.y = -0.35;
        this.scene.add(this.mesh);
        this.start();
    },

    start() {
        if (this.animId) return;
        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);
        const loop = () => {
            this.animId = requestAnimationFrame(loop);
            if (document.hidden) return;
            this.time += 0.035;
            if (this.mesh && !this.isDragging) {
                if (typeof app === 'undefined' || !app.settings || app.settings.autoSpin3D) {
                    this.mesh.rotateOnWorldAxis(worldY, this.velX);
                    this.mesh.rotateOnWorldAxis(worldX, this.velY);
                    this.velX = this.velX * 0.95 + 0.011 * 0.05;
                    this.velY = this.velY * 0.94;
                    this.mesh.position.y = Math.sin(this.time) * 0.12;
                }
            }
            if (this.renderer && this.scene && this.camera) {
                this.renderer.render(this.scene, this.camera);
            }
        };
        this.animId = requestAnimationFrame(loop);
    },

    stop() {
        if (this.animId) {
            cancelAnimationFrame(this.animId);
            this.animId = null;
        }
    }
};

const colorGame = {
    mode: 'explore',
    mixPick1: GAMES.colors[0],
    mixPick2: GAMES.colors[2],
    activeSlot: 1,

    open() {
        this.select(GAMES.colors[0], true);
    },

    setMode(newMode) {
        this.mode = newMode;
        document.getElementById('color-mode-explore').classList.toggle('active', newMode === 'explore');
        document.getElementById('color-mode-mix').classList.toggle('active', newMode === 'mix');
        document.getElementById('color-explore-box').classList.toggle('hidden', newMode !== 'explore');
        document.getElementById('color-mix-box').classList.toggle('hidden', newMode !== 'mix');
        document.getElementById('color-mix-box').classList.toggle('flex', newMode === 'mix');
        if (newMode === 'mix') {
            this.setActiveSlot(1);
            this.updateMixDisplay(true);
        } else {
            this.select(this.mixPick1, false);
        }
    },

    setActiveSlot(slotNum) {
        this.activeSlot = slotNum;
        const s1 = document.getElementById('mix-slot-1');
        const s2 = document.getElementById('mix-slot-2');
        if (s1 && s2) {
            s1.classList.toggle('ring-4', slotNum === 1);
            s1.classList.toggle('ring-indigo-400', slotNum === 1);
            s2.classList.toggle('ring-4', slotNum === 2);
            s2.classList.toggle('ring-indigo-400', slotNum === 2);
        }
    },

    select(cData, speak = true) {
        if (this.mode === 'mix') {
            if (this.activeSlot === 1) {
                this.mixPick1 = cData;
                this.setActiveSlot(2);
            } else {
                this.mixPick2 = cData;
                this.setActiveSlot(1);
            }
            this.updateMixDisplay(true);
            return;
        }
        const bg = document.getElementById('color-bg-target');
        const txt = document.getElementById('color-text');
        const ex = document.getElementById('color-examples');

        bg.style.backgroundColor = cData.hex;
        txt.textContent = cData.id;
        txt.style.color = cData.text;
        ex.innerHTML = cData.examples.map(e => `<span>${e}</span>`).join('');
        app.animatePop(ex);
        if (speak) app.speak(cData.id);
    },

    updateMixDisplay(speak = true) {
        const c1 = this.mixPick1.id;
        const c2 = this.mixPick2.id;
        document.getElementById('mix-slot-1').style.backgroundColor = this.mixPick1.hex;
        document.getElementById('mix-slot-2').style.backgroundColor = this.mixPick2.hex;

        const pairKey = [c1, c2].sort().join('+');
        const recipes = {
            // Primaries & Secondaries
            'Red+Yellow': { name: 'Orange', hex: '#f97316', emoji: '🍊' },
            'Blue+Yellow': { name: 'Green', hex: '#22c55e', emoji: '🐸' },
            'Blue+Red': { name: 'Purple', hex: '#a855f7', emoji: '🍇' },
            // Tints (with White)
            'Red+White': { name: 'Pink', hex: '#ec4899', emoji: '🦩' },
            'Blue+White': { name: 'Sky Blue', hex: '#38bdf8', emoji: '☁️' },
            'White+Yellow': { name: 'Cream Yellow', hex: '#fef08a', emoji: '🍦' },
            'Green+White': { name: 'Mint Green', hex: '#86efac', emoji: '🌱' },
            'Orange+White': { name: 'Peach', hex: '#fed7aa', emoji: '🍑' },
            'Purple+White': { name: 'Lavender', hex: '#d8b4fe', emoji: '🪻' },
            'Pink+White': { name: 'Light Pink', hex: '#fbcfe8', emoji: '🌸' },
            'Brown+White': { name: 'Tan Khaki', hex: '#d6d3d1', emoji: '🏖️' },
            'Black+White': { name: 'Gray', hex: '#94a3b8', emoji: '🐘' },
            // Shades (with Black)
            'Black+Red': { name: 'Burgundy Dark Red', hex: '#7f1d1d', emoji: '🍒' },
            'Black+Blue': { name: 'Midnight Navy', hex: '#0f172a', emoji: '🌌' },
            'Black+Yellow': { name: 'Olive Green', hex: '#3f6212', emoji: '🫒' },
            'Black+Green': { name: 'Forest Green', hex: '#064e3b', emoji: '🌲' },
            'Black+Orange': { name: 'Rust Brown', hex: '#7c2d12', emoji: '🍁' },
            'Black+Purple': { name: 'Deep Violet', hex: '#3b0764', emoji: '🔮' },
            'Black+Pink': { name: 'Dusty Plum', hex: '#701a75', emoji: '🍇' },
            'Black+Brown': { name: 'Dark Chocolate', hex: '#451a03', emoji: '🍫' },
            // Tertiary & Earthy combinations
            'Green+Red': { name: 'Brown', hex: '#78350f', emoji: '🐻' },
            'Blue+Orange': { name: 'Warm Slate', hex: '#64748b', emoji: '🪨' },
            'Purple+Yellow': { name: 'Golden Bronze', hex: '#a16207', emoji: '🪙' },
            'Green+Yellow': { name: 'Lime Green', hex: '#84cc16', emoji: '🍋' },
            'Blue+Green': { name: 'Teal Turquoise', hex: '#0d9488', emoji: '🪸' },
            'Orange+Red': { name: 'Coral Red', hex: '#ea580c', emoji: '🔥' },
            'Pink+Purple': { name: 'Magenta Rose', hex: '#c026d3', emoji: '🌺' },
            'Blue+Pink': { name: 'Lilac Violet', hex: '#818cf8', emoji: '🪻' },
            'Brown+Orange': { name: 'Caramel', hex: '#b45309', emoji: '🥞' },
            'Brown+Red': { name: 'Terracotta', hex: '#991b1b', emoji: '🏺' }
        };

        let res = recipes[pairKey];
        if (!res) {
            if (c1 === c2) {
                res = { name: c1, hex: this.mixPick1.hex, emoji: this.mixPick1.examples[0] };
            } else {
                // Perceptual RGB interpolation fallback
                const hexToRgb = h => {
                    const c = parseInt(h.slice(1), 16);
                    return [(c >> 16) & 255, (c >> 8) & 255, c & 255];
                };
                const rgb1 = hexToRgb(this.mixPick1.hex);
                const rgb2 = hexToRgb(this.mixPick2.hex);
                const r = Math.round((rgb1[0] + rgb2[0]) / 2);
                const g = Math.round((rgb1[1] + rgb2[1]) / 2);
                const b = Math.round((rgb1[2] + rgb2[2]) / 2);
                const mixedHex = `#${((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1)}`;
                res = { name: `${c1} & ${c2} Blend`, hex: mixedHex, emoji: '🎨' };
            }
        }

        const resCircle = document.getElementById('mix-result-circle');
        resCircle.style.backgroundColor = res.hex;
        resCircle.textContent = res.emoji;
        document.getElementById('color-bg-target').style.backgroundColor = res.hex;
        document.getElementById('mix-result-text').textContent = `${c1} + ${c2} = ${res.name}!`;
        app.animatePop(resCircle);
        if (speak) app.speak(`${c1} plus ${c2} makes ${res.name}!`);
    }
};

const animalGame = {
    current: GAMES.animals[0],
    speechTimer: null,
    select(a, playAudio = true, soundOnly = false) {
        this.current = a;
        soundFX.stopAll();
        if (soundOnly || !playAudio) {
            geminiTTS.stop();
            if ('speechSynthesis' in window && (window.speechSynthesis.speaking || window.speechSynthesis.pending)) {
                try { window.speechSynthesis.cancel(); } catch (e) {}
            }
        }
        const t = document.getElementById('animal-target');
        t.textContent = a.emoji;
        document.getElementById('animal-text').textContent = a.id;
        document.getElementById('animal-sound-pill').textContent = `🗣️ "${a.sound}"`;
        document.querySelectorAll('#animal-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.animalId === a.id);
        });
        app.animatePop(t);
        if (playAudio) {
            if (app.isOpeningView && !app.settings.announceGameOnOpen) {
                return;
            }
            if (soundOnly) {
                soundFX.playAnimalSound(a.id);
            } else {
                app.speak(a.id);
                const delay = app.isOpeningView ? 950 : 380;
                const timer = setTimeout(() => {
                    soundFX.playAnimalSound(a.id);
                }, delay);
                soundFX.registerTimer(timer);
            }
        }
    }
};

const foodGame = {
    current: GAMES.fruits[0],
    biteList: [],
    maxBites: 5,

    select(f, speak = true) {
        this.current = f;
        this.biteList = [];
        document.getElementById('fruits-text').textContent = f.id;
        document.getElementById('fruits-desc').textContent = `${f.desc} Tap on it to take a bite!`;
        document.querySelectorAll('#fruits-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.foodId === f.id);
        });
        this.renderFoodCanvas();
        app.animatePop(document.getElementById('fruits-target'));
        if (speak) app.speak(`${f.id}! ${f.desc}`);
    },

    renderFoodCanvas() {
        const canvas = document.getElementById('fruits-canvas');
        if (!canvas) return;
        const ctx = canvas.getContext('2d');
        ctx.clearRect(0, 0, canvas.width, canvas.height);

        ctx.save();
        ctx.font = '165px "Apple Color Emoji", "Segoe UI Emoji", "Noto Color Emoji", sans-serif';
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.fillText(this.current.emoji, canvas.width / 2, canvas.height / 2 + 10);

        // Creamy tooth-shaped bite rims
        ctx.globalCompositeOperation = 'source-atop';
        ctx.fillStyle = this.current.innerColor || '#fef3c7';
        this.biteList.forEach(b => {
            this.drawScallopedBite(ctx, b.x, b.y, b.r + 6, b.angle);
        });

        // Punch out bite holes
        ctx.globalCompositeOperation = 'destination-out';
        ctx.fillStyle = '#000000';
        this.biteList.forEach(b => {
            this.drawScallopedBite(ctx, b.x, b.y, b.r, b.angle);
        });
        ctx.restore();
    },

    drawScallopedBite(ctx, cx, cy, r, angle) {
        ctx.save();
        ctx.translate(cx, cy);
        ctx.rotate(angle);
        ctx.beginPath();
        const teeth = 4;
        const toothR = r / (teeth * 0.9);
        ctx.arc(0, 0, r, 0, Math.PI, true);
        for (let i = 0; i < teeth; i++) {
            const tx = -r + toothR + i * (toothR * 2);
            ctx.arc(tx, 0, toothR, 0, Math.PI, false);
        }
        ctx.closePath();
        ctx.fill();
        ctx.restore();
    },

    burstCrumbs(x, y) {
        if (typeof app !== 'undefined' && app.settings && !app.settings.confettiEnabled) return;
        const color = this.current.crumbColor || '#ef4444';
        for (let i = 0; i < 9; i++) {
            const p = document.createElement('div');
            p.className = 'crumb-piece';
            p.style.left = `${x}px`;
            p.style.top = `${y}px`;
            const size = 6 + Math.random() * 8;
            p.style.width = `${size}px`;
            p.style.height = `${size}px`;
            p.style.backgroundColor = color;
            const angle = Math.random() * Math.PI * 2;
            const dist = 30 + Math.random() * 55;
            p.style.setProperty('--cx', `${Math.cos(angle) * dist}px`);
            p.style.setProperty('--cy', `${Math.sin(angle) * dist + 25}px`);
            document.body.appendChild(p);
            setTimeout(() => p.remove(), 520);
        }
    },

    chomp(e) {
        // ALWAYS play crisp physical bite crunch!
        soundFX.playCrunch();

        const canvas = document.getElementById('fruits-canvas');
        if (!canvas) return;
        const rect = canvas.getBoundingClientRect();
        const preset = [
            { x: 165, y: 80 },
            { x: 75, y: 85 },
            { x: 168, y: 155 },
            { x: 75, y: 155 },
            { x: 120, y: 120 }
        ];

        let bx, by, cx, cy;
        const idx = this.biteList.length;
        if (e && e.clientX && idx < this.maxBites - 1) {
            cx = e.clientX;
            cy = e.clientY;
            bx = ((cx - rect.left) / rect.width) * canvas.width;
            by = ((cy - rect.top) / rect.height) * canvas.height;
            bx = Math.max(55, Math.min(canvas.width - 55, bx));
            by = Math.max(55, Math.min(canvas.height - 55, by));
        } else {
            const pt = preset[idx % preset.length];
            bx = pt.x;
            by = pt.y;
            cx = rect.left + (bx / canvas.width) * rect.width;
            cy = rect.top + (by / canvas.height) * rect.height;
        }

        this.biteList.push({ x: bx, y: by, r: 34 + idx * 4, angle: idx * 0.9 });
        this.renderFoodCanvas();
        this.burstCrumbs(cx, cy);
        app.animatePop(document.getElementById('fruits-target'));

        const cheers = ['Crunch! Delicious!', 'Yum yum!', 'So tasty!', 'One more bite!'];

        if (this.biteList.length < this.maxBites) {
            const left = this.maxBites - this.biteList.length;
            document.getElementById('fruits-desc').textContent = `Yum! ${left} more bite${left > 1 ? 's' : ''} left! 😋`;
            app.speak(cheers[idx % cheers.length]);
        } else {
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
            soundFX.playCheer();
            document.getElementById('fruits-desc').textContent = `All gone! Getting another ${this.current.id}... 🎉`;
            app.speak(`All gone! Yummy ${this.current.id}! Delicious!`);
            setTimeout(() => {
                if (app.currentView === 'fruits') {
                    this.biteList = [];
                    this.renderFoodCanvas();
                    document.getElementById('fruits-desc').textContent = `Fresh ${this.current.id}! Tap to take a bite!`;
                }
            }, 980);
        }
    }
};

const thingsGame = {
    current: GAMES.things[0],
    speechTimer: null,
    select(item, speak = true, soundOnly = false) {
        this.current = item;
        soundFX.stopAll();
        geminiTTS.stop();
        if ('speechSynthesis' in window && (window.speechSynthesis.speaking || window.speechSynthesis.pending)) {
            try { window.speechSynthesis.cancel(); } catch (e) {}
        }
        const t = document.getElementById('things-target');
        t.textContent = item.emoji;
        document.getElementById('things-text').textContent = item.id;
        document.getElementById('things-sound').textContent = `🔊 "${item.sound}"`;
        document.querySelectorAll('#things-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.thingId === item.id);
        });
        app.animatePop(t);
        if (speak) {
            if (app.isOpeningView && !app.settings.announceGameOnOpen) {
                return;
            }
            if (app.isOpeningView) {
                app.speak(item.id);
                this.speechTimer = setTimeout(() => {
                    soundFX.playThingSound(item.id);
                    this.speechTimer = null;
                }, 950);
                soundFX.registerTimer(this.speechTimer);
            } else {
                soundFX.playThingSound(item.id);
                if (!soundOnly) {
                    this.speechTimer = setTimeout(() => {
                        app.speak(item.id);
                        this.speechTimer = null;
                    }, 350);
                    soundFX.registerTimer(this.speechTimer);
                }
            }
        }
    }
};

const oppositesGame = {
    current: GAMES.opposites[0],
    select(pair, speak = true) {
        this.current = pair;
        document.getElementById('opp-title').textContent = pair.title;
        const emojiA = document.getElementById('opp-emoji-a');
        const emojiB = document.getElementById('opp-emoji-b');
        emojiA.className = `${pair.a.scale} mb-2`;
        emojiB.className = `${pair.b.scale} mb-2`;
        emojiA.textContent = pair.a.emoji;
        emojiB.textContent = pair.b.emoji;
        document.getElementById('opp-label-a').textContent = pair.a.label;
        document.getElementById('opp-label-b').textContent = pair.b.label;
        document.querySelectorAll('#opposites-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.oppTitle === pair.title);
        });
        app.animatePop(document.getElementById('opp-card-a'));
        app.animatePop(document.getElementById('opp-card-b'));
        if (speak) app.speak(`${pair.a.label}, and ${pair.b.label}!`);
    }
};


// scratch/init.js

function updateVoiceStatusIndicator() {
    const key = getApiKey();
    const dot = document.getElementById('voice-status-dot');
    const txt = document.getElementById('voice-status-text');
    const badge = document.getElementById('canvas-key-badge');
    const input = document.getElementById('gemini-api-key-input');
    const modelSel = document.getElementById('gemini-tts-model-select');
    const voiceSel = document.getElementById('gemini-tts-voice-select');

    const storedKey = localStorage.getItem('tlh_isolated_v3_api_key') || localStorage.getItem('toddler_gemini_api_key');
    if (input && document.activeElement !== input) {
        input.value = storedKey || (apiKey ? "●●●●●●●● (Canvas Injected)" : "");
    }
    if (modelSel && document.activeElement !== modelSel) modelSel.value = getTtsModel();
    if (voiceSel && document.activeElement !== voiceSel) voiceSel.value = getTtsVoice();

    if (typeof app !== 'undefined' && app.settings && !app.settings.voiceEnabled) {
        if (dot) dot.className = 'w-2 h-2 rounded-full bg-slate-400';
        if (txt) {
            txt.textContent = 'Voice Off';
            txt.className = 'text-slate-500 font-bold';
        }
        if (badge) {
            badge.textContent = 'Voice Spoken Output Disabled';
            badge.className = 'text-[11px] font-extrabold text-slate-500 bg-slate-100 px-2 py-0.5 rounded-full border border-slate-200';
        }
    } else if (key) {
        if (dot) dot.className = 'w-2 h-2 rounded-full bg-emerald-500 animate-pulse';
        if (txt) {
            txt.textContent = 'Gemini 3.8 Voice';
            txt.className = 'text-emerald-700 font-black';
        }
        if (badge) {
            badge.textContent = apiKey && !storedKey ? 'Canvas Key Active' : 'API Key Active';
            badge.className = 'text-[11px] font-extrabold text-emerald-700 bg-emerald-50 px-2 py-0.5 rounded-full border border-emerald-200';
        }
    } else {
        if (dot) dot.className = 'w-2 h-2 rounded-full bg-blue-500';
        if (txt) {
            txt.textContent = 'Device Voice';
            txt.className = 'text-slate-600 font-bold';
        }
        if (badge) {
            badge.textContent = 'Using Device Voice';
            badge.className = 'text-[11px] font-extrabold text-slate-500 bg-slate-100 px-2 py-0.5 rounded-full border border-slate-200';
        }
    }
}

window.addEventListener('DOMContentLoaded', () => {
    app.initVoices();
    if ('speechSynthesis' in window) {
        window.speechSynthesis.onvoiceschanged = () => app.initVoices();
    }
    // 1. Initial Voice Status Indicator
    updateVoiceStatusIndicator();

    // 2. Voice & Options Modal Setup & Live Synchronization
    const voiceModal = document.getElementById('voice-settings-modal');
    const inp = document.getElementById('gemini-api-key-input');
    const modelSel = document.getElementById('gemini-tts-model-select');
    const voiceSel = document.getElementById('gemini-tts-voice-select');
    const testStatus = document.getElementById('voice-test-status');

    const syncSettingsToUI = () => {
        const s = app.settings;
        const optAnnounce = document.getElementById('opt-announce-open');
        if (optAnnounce) optAnnounce.checked = !!s.announceGameOnOpen;
        const optVoice = document.getElementById('opt-voice-enabled');
        if (optVoice) optVoice.checked = !!s.voiceEnabled;
        const optSfx = document.getElementById('opt-sfx-enabled');
        if (optSfx) optSfx.checked = !!s.sfxEnabled;
        const optSpeechRate = document.getElementById('opt-speech-rate');
        if (optSpeechRate) optSpeechRate.value = s.speechRate || 'normal';
        const optMaxNum = document.getElementById('opt-max-number');
        if (optMaxNum) optMaxNum.value = String(s.maxNumber || 20);
        const optPhonics = document.getElementById('opt-phonics-detail');
        if (optPhonics) optPhonics.value = s.phonicsDetail || 'full';
        const optConfetti = document.getElementById('opt-confetti-enabled');
        if (optConfetti) optConfetti.checked = !!s.confettiEnabled;
        const optAutoSpin = document.getElementById('opt-autospin-3d');
        if (optAutoSpin) optAutoSpin.checked = !!s.autoSpin3D;
        const optHoldHome = document.getElementById('opt-hold-home');
        if (optHoldHome) optHoldHome.checked = !!s.requireHoldHome;
    };

    const openVoiceModal = () => {
        syncSettingsToUI();
        updateVoiceStatusIndicator();
        if (testStatus) {
            testStatus.classList.add('hidden');
            testStatus.textContent = '';
        }
        if (voiceModal) voiceModal.classList.remove('hidden');
    };
    const closeVoiceModal = () => {
        if (voiceModal) voiceModal.classList.add('hidden');
    };

    document.getElementById('voice-settings-btn')?.addEventListener('click', openVoiceModal);
    document.querySelectorAll('.options-quick-btn').forEach(btn => {
        btn.addEventListener('click', openVoiceModal);
    });
    document.getElementById('voice-modal-close-x')?.addEventListener('click', closeVoiceModal);

    // Live option input listeners
    document.getElementById('opt-announce-open')?.addEventListener('change', (e) => {
        app.settings.announceGameOnOpen = e.target.checked;
        app.saveSettings();
    });
    document.getElementById('opt-voice-enabled')?.addEventListener('change', (e) => {
        app.settings.voiceEnabled = e.target.checked;
        app.saveSettings();
    });
    document.getElementById('opt-sfx-enabled')?.addEventListener('change', (e) => {
        app.settings.sfxEnabled = e.target.checked;
        app.saveSettings();
    });
    document.getElementById('opt-speech-rate')?.addEventListener('change', (e) => {
        app.settings.speechRate = e.target.value;
        app.saveSettings();
    });
    document.getElementById('opt-max-number')?.addEventListener('change', (e) => {
        app.settings.maxNumber = parseInt(e.target.value, 10);
        app.saveSettings();
    });
    document.getElementById('opt-phonics-detail')?.addEventListener('change', (e) => {
        app.settings.phonicsDetail = e.target.value;
        app.saveSettings();
    });
    document.getElementById('opt-confetti-enabled')?.addEventListener('change', (e) => {
        app.settings.confettiEnabled = e.target.checked;
        app.saveSettings();
    });
    document.getElementById('opt-autospin-3d')?.addEventListener('change', (e) => {
        app.settings.autoSpin3D = e.target.checked;
        app.saveSettings();
    });
    document.getElementById('opt-hold-home')?.addEventListener('change', (e) => {
        app.settings.requireHoldHome = e.target.checked;
        app.saveSettings();
    });

    document.getElementById('opt-reset-defaults-btn')?.addEventListener('click', () => {
        app.settings = Object.assign({}, DEFAULT_SETTINGS);
        app.saveSettings();
        syncSettingsToUI();
        soundFX.playPop();
    });

    // Live input listeners so changes take effect immediately
    inp?.addEventListener('input', () => {
        const val = inp.value.trim();
        if (!val.includes('●●●●●●●●')) {
            if (val) localStorage.setItem('tlh_isolated_v3_api_key', val);
            else localStorage.removeItem('tlh_isolated_v3_api_key');
            updateVoiceStatusIndicator();
        }
    });
    modelSel?.addEventListener('change', () => {
        localStorage.setItem('tlh_isolated_v3_tts_model', modelSel.value);
    });
    voiceSel?.addEventListener('change', () => {
        localStorage.setItem('tlh_isolated_v3_tts_voice', voiceSel.value);
    });

    // Save & Done button
    document.getElementById('voice-modal-save-btn')?.addEventListener('click', () => {
        if (inp) {
            const val = inp.value.trim();
            if (!val.includes('●●●●●●●●')) {
                if (val) localStorage.setItem('tlh_isolated_v3_api_key', val);
                else localStorage.removeItem('tlh_isolated_v3_api_key');
            }
        }
        if (modelSel) localStorage.setItem('tlh_isolated_v3_tts_model', modelSel.value);
        if (voiceSel) localStorage.setItem('tlh_isolated_v3_tts_voice', voiceSel.value);

        app.saveSettings();
        updateVoiceStatusIndicator();
        closeVoiceModal();
        if (app.settings.voiceEnabled) {
            app.speak("Options saved! Let's explore together!");
        }
    });

    // Live Test Voice Sample Button (tests live input values directly)
    document.getElementById('voice-test-btn')?.addEventListener('click', async () => {
        const testText = "Hello little explorer! Let's count and play together!";
        const curModel = modelSel?.value || getTtsModel();
        const curVoice = voiceSel?.value || getTtsVoice();
        const liveKeyVal = inp?.value.trim();
        const testKey = (!liveKeyVal || liveKeyVal.includes('●●●●●●●●')) ? getApiKey() : liveKeyVal;

        if (testStatus) {
            testStatus.classList.remove('hidden');
            testStatus.className = 'text-xs font-bold text-center py-1.5 px-3 rounded-xl bg-indigo-50 text-indigo-700 border border-indigo-200';
            testStatus.textContent = 'Connecting to Gemini Voice...';
        }

        if (testKey) {
            try {
                await geminiTTS.play(testText, curModel, curVoice, testKey);
                if (testStatus) {
                    testStatus.className = 'text-xs font-bold text-center py-1.5 px-3 rounded-xl bg-emerald-50 text-emerald-800 border border-emerald-200';
                    testStatus.textContent = `✨ Gemini 3.8 voice (${curVoice}) playing successfully!`;
                }
            } catch (err) {
                if (testStatus) {
                    testStatus.className = 'text-xs font-bold text-center py-1.5 px-3 rounded-xl bg-amber-50 text-amber-800 border border-amber-200';
                    testStatus.textContent = `⚠️ Gemini API error (${err.message}). Using Device Voice fallback.`;
                }
                app.speakDeviceVoice(testText);
            }
        } else {
            if (testStatus) {
                testStatus.className = 'text-xs font-bold text-center py-1.5 px-3 rounded-xl bg-blue-50 text-blue-800 border border-blue-200';
                testStatus.textContent = '🔊 Playing with natural Device Voice (No Gemini API key set).';
            }
            app.speakDeviceVoice(testText);
        }
    });

    // Pre-cache Core Words into IndexedDB
    document.getElementById('voice-precache-btn')?.addEventListener('click', async () => {
        const key = getApiKey();
        if (!key) {
            alert("Please paste your Gemini API Key first to pre-cache Gemini natural voices!");
            return;
        }

        const wordsToCache = [
            "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten",
            "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen", "Twenty",
            "Great job!", "You found it!", "Yay!", "Yum yum!", "Crunch! Delicious!",
            "Choo choo!", "Blast off!", "Roar!", "Splish splash!", "Ring ring!",
            "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
            "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"
        ];

        const progressBox = document.getElementById('precache-progress-box');
        const progressBar = document.getElementById('precache-progress-bar');
        const progressNum = document.getElementById('precache-progress-num');
        const precacheLabel = document.getElementById('voice-precache-label');

        if (progressBox) progressBox.classList.remove('hidden');
        if (precacheLabel) precacheLabel.textContent = 'Caching...';

        const model = getTtsModel();
        const voice = getTtsVoice();

        for (let i = 0; i < wordsToCache.length; i++) {
            const word = wordsToCache[i];
            try {
                await geminiTTS.fetchAudio(word, model, voice);
            } catch (err) {}
            const pct = Math.round(((i + 1) / wordsToCache.length) * 100);
            if (progressBar) progressBar.style.width = `${pct}%`;
            if (progressNum) progressNum.textContent = `${pct}%`;
        }

        if (precacheLabel) precacheLabel.textContent = '⚡ Core Words Cached!';
        setTimeout(() => {
            if (progressBox) progressBox.classList.add('hidden');
        }, 1500);
        app.speak("All core words are ready for instant play!");
    });

    // 3. Main Menu Navigation
    document.querySelectorAll('#main-menu-grid .menu-card').forEach(card => {
        card.addEventListener('click', () => {
            soundFX.init();
            app.switchView(card.dataset.view);
        });
    });

    document.querySelectorAll('[data-action="home"]').forEach(btn => {
        let lockTimer = null;
        btn.addEventListener('click', () => {
            if (app.settings && app.settings.requireHoldHome) {
                if (btn.dataset.confirmHome !== 'true') {
                    btn.dataset.confirmHome = 'true';
                    btn.innerHTML = '<span>🔒</span><span>Tap Again</span>';
                    soundFX.playPop();
                    clearTimeout(lockTimer);
                    lockTimer = setTimeout(() => {
                        btn.dataset.confirmHome = 'false';
                        btn.innerHTML = '<span>🏠</span><span>Home</span>';
                    }, 2000);
                    return;
                }
                clearTimeout(lockTimer);
                btn.dataset.confirmHome = 'false';
                btn.innerHTML = '<span>🏠</span><span>Home</span>';
            }
            app.switchView('menu');
        });
    });

    // 4. Phonics Setup
    const phonicsTray = document.getElementById('phonics-controls');
    GAMES.phonics.forEach((p, idx) => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn text-blue-700';
        btn.innerHTML = `<span class="text-xl leading-none font-black">${p.letter}${p.letter.toLowerCase()}</span><span class="text-xs">${p.words[0].e}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            phonicsGame.selectLetter(idx, true);
        });
        phonicsTray.appendChild(btn);
    });
    document.getElementById('phonics-mode-studio').addEventListener('click', () => phonicsGame.setMode('studio'));
    document.getElementById('phonics-mode-bubbles').addEventListener('click', () => phonicsGame.setMode('bubbles'));
    document.getElementById('phonics-main-card').addEventListener('click', () => {
        soundFX.playPop();
        phonicsGame.selectLetter(phonicsGame.currentIndex, true);
    });
    document.getElementById('bubble-repeat-btn').addEventListener('click', () => {
        const d = GAMES.phonics[phonicsGame.currentIndex];
        app.speak(`Pop ${d.letter}! ${d.cue} ${d.words[0].w}!`);
    });

    // 5. Numbers Setup
    const numberTray = document.getElementById('number-controls');
    GAMES.numbers.forEach(n => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn text-teal-700';
        btn.dataset.num = n.num;
        btn.innerHTML = `<span class="text-xl leading-none font-black">${n.num}</span><span class="text-xs">${n.emoji}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            numberGame.select(n, true);
        });
        numberTray.appendChild(btn);
    });
    numberGame.applyMaxNumberSetting();
    document.getElementById('num-mode-touch').addEventListener('click', () => numberGame.setMode('touch'));
    document.getElementById('num-mode-show').addEventListener('click', () => numberGame.setMode('show'));
    document.getElementById('number-big-digit').addEventListener('click', () => {
        soundFX.playPop();
        numberGame.select(numberGame.currentData, true);
    });
    document.getElementById('number-count-all-btn').addEventListener('click', () => {
        soundFX.playPop();
        numberGame.countAllSequentially();
    });

    // 6. Quiz Setup
    document.querySelectorAll('.quiz-cat-btn').forEach(btn => {
        btn.addEventListener('click', () => quizGame.setCategory(btn.dataset.quizCat));
    });
    document.getElementById('quiz-prompt-box').addEventListener('click', () => {
        if (quizGame.currentAnswer) app.speak(quizGame.currentAnswer.prompt);
    });
    document.getElementById('quiz-next-btn').addEventListener('click', () => {
        soundFX.playPop();
        quizGame.nextQuestion();
    });

    // 7. 2D Shapes Setup
    const shapeTray = document.getElementById('shape-controls');
    GAMES.shapes.forEach(s => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn p-2';
        btn.dataset.shapeId = s.id;
        btn.innerHTML = `<svg width="36" height="36" viewBox="0 0 100 100">${s.svg}</svg>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            shape2DGame.select(s, true);
        });
        shapeTray.appendChild(btn);
    });
    document.getElementById('shape-target').addEventListener('click', () => {
        soundFX.playPop();
        shape2DGame.select(shape2DGame.current, true);
    });

    // 8. 3D Shapes Setup
    const shape3dTray = document.getElementById('shape3d-controls');
    GAMES.shapes3d.forEach(s => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.shape3dId = s.id;
        btn.innerHTML = `<span class="text-2xl leading-none">${s.emoji}</span><span class="text-[10px] font-black text-slate-600 mt-0.5">${s.id.split(' ')[0]}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            shapes3DGame.select(s, true);
        });
        shape3dTray.appendChild(btn);
    });

    // 9. Colors Setup
    const colorTray = document.getElementById('color-controls');
    GAMES.colors.forEach(c => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.style.backgroundColor = c.hex;
        btn.style.borderColor = c.id === 'White' ? '#cbd5e1' : '#ffffff';
        btn.innerHTML = `<span class="text-xl">${c.examples[0]}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            colorGame.select(c, true);
        });
        colorTray.appendChild(btn);
    });
    document.getElementById('color-mode-explore').addEventListener('click', () => colorGame.setMode('explore'));
    document.getElementById('color-mode-mix').addEventListener('click', () => colorGame.setMode('mix'));
    document.getElementById('mix-slot-1')?.addEventListener('click', () => colorGame.setActiveSlot(1));
    document.getElementById('mix-slot-2')?.addEventListener('click', () => colorGame.setActiveSlot(2));
    document.getElementById('color-examples').addEventListener('click', () => {
        soundFX.playPop();
        app.speak(document.getElementById('color-text').textContent);
    });

    // 10. Animals Setup
    const animalTray = document.getElementById('animal-controls');
    GAMES.animals.forEach(a => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.animalId = a.id;
        btn.innerHTML = `<span class="text-3xl">${a.emoji}</span>`;
        btn.addEventListener('click', () => animalGame.select(a, true, false));
        animalTray.appendChild(btn);
    });
    const triggerAnimalSoundOnly = () => animalGame.select(animalGame.current, true, true);
    document.getElementById('animal-target').addEventListener('click', triggerAnimalSoundOnly);
    document.getElementById('animal-sound-btn').addEventListener('click', triggerAnimalSoundOnly);
    document.getElementById('animal-sound-pill').addEventListener('click', triggerAnimalSoundOnly);

    // 11. Yummy Foods Setup
    const foodTray = document.getElementById('fruits-controls');
    GAMES.fruits.forEach(f => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.foodId = f.id;
        btn.innerHTML = `<span class="text-3xl">${f.emoji}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            foodGame.select(f, true);
        });
        foodTray.appendChild(btn);
    });
    document.getElementById('fruits-target').addEventListener('pointerdown', e => foodGame.chomp(e));
    document.getElementById('food-chomp-btn').addEventListener('click', () => foodGame.chomp());

    // 12. Vehicles & Things Setup
    const thingsTray = document.getElementById('things-controls');
    GAMES.things.forEach(t => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.thingId = t.id;
        btn.innerHTML = `<span class="text-3xl">${t.emoji}</span>`;
        btn.addEventListener('click', () => thingsGame.select(t, true));
        thingsTray.appendChild(btn);
    });
    const triggerThingSpeak = () => thingsGame.select(thingsGame.current, true, true);
    document.getElementById('things-target').addEventListener('click', triggerThingSpeak);
    document.getElementById('things-sound').addEventListener('click', triggerThingSpeak);

    // 13. Opposites Setup
    const oppTray = document.getElementById('opposites-controls');
    GAMES.opposites.forEach(pair => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.oppTitle = pair.title;
        btn.innerHTML = `<span class="text-xl leading-none">${Array.from(pair.a.emoji)[0]}${Array.from(pair.b.emoji)[0]}</span><span class="text-[10px] font-black text-slate-600 mt-0.5">${pair.a.label}</span>`;
        btn.addEventListener('click', () => {
            soundFX.playPop();
            oppositesGame.select(pair, true);
        });
        oppTray.appendChild(btn);
    });
    document.getElementById('opp-card-a').addEventListener('click', () => {
        soundFX.playNote(523.25, 0.14, 'triangle');
        app.animatePop(document.getElementById('opp-card-a'));
        app.speak(oppositesGame.current.a.label);
    });
    document.getElementById('opp-card-b').addEventListener('click', () => {
        soundFX.playNote(392.0, 0.14, 'triangle');
        app.animatePop(document.getElementById('opp-card-b'));
        app.speak(oppositesGame.current.b.label);
    });

    // 14. Solar System Setup with Real Official NASA Photos in Tray
    const solarTray = document.getElementById('solar-controls');
    GAMES.solar.forEach((s, idx) => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn p-1';
        btn.dataset.solarId = s.id;
        const thumbWrap = document.createElement('div');
        thumbWrap.className = 'w-9 h-9 rounded-full overflow-hidden border border-slate-400 bg-slate-950 flex items-center justify-center';
        const thumbImg = document.createElement('img');
        thumbImg.src = s.photoUrl;
        thumbImg.alt = s.short;
        thumbImg.className = 'w-full h-full object-cover';
        thumbImg.addEventListener('error', () => {
            thumbWrap.innerHTML = getSolarSVG(s.id, 'tray_' + idx);
        }, { once: true });
        thumbWrap.appendChild(thumbImg);
        const labelSpan = document.createElement('span');
        labelSpan.className = 'text-[10px] font-black text-slate-700 mt-0.5 leading-none';
        labelSpan.textContent = s.short;
        btn.appendChild(thumbWrap);
        btn.appendChild(labelSpan);
        btn.addEventListener('click', () => solarGame.select(s, true));
        solarTray.appendChild(btn);
    });
    document.getElementById('solar-mode-photo').addEventListener('click', () => solarGame.setMode('photo'));
    document.getElementById('solar-mode-planet').addEventListener('click', () => solarGame.setMode('planet'));
    document.getElementById('solar-mode-orbit').addEventListener('click', () => solarGame.setMode('orbit'));
    document.getElementById('solar-photo-container').addEventListener('click', () => solarGame.triggerAction());
    document.getElementById('solar-action-btn').addEventListener('click', () => solarGame.triggerAction());
    document.getElementById('solar-fact').addEventListener('click', () => solarGame.triggerAction());

    // 15. Cross-tab & Multi-app Audio Isolation (clean shutdown on visibilitychange / pagehide)
    const pauseAllAudio = () => {
        soundFX.stopAll();
        geminiTTS.stop();
        if ('speechSynthesis' in window) {
            try { window.speechSynthesis.cancel(); } catch (e) {}
        }
    };
    document.addEventListener('visibilitychange', () => {
        if (document.hidden) pauseAllAudio();
    });
    window.addEventListener('pagehide', pauseAllAudio);
    window.addEventListener('beforeunload', pauseAllAudio);

    // Pre-warm audio and unlock WebAudio on initial touch/pointer
    const unlockAudio = () => {
        soundFX.init();
        document.removeEventListener('pointerdown', unlockAudio);
        document.removeEventListener('touchstart', unlockAudio);
    };
    document.addEventListener('pointerdown', unlockAudio, { once: true });
    document.addEventListener('touchstart', unlockAudio, { once: true });
});


window.ToddlerLearningHub = {
    app,
    soundFX,
    geminiTTS,
    DEFAULT_SETTINGS,
    GAME_OPEN_TITLES,
    GAMES,
    phonicsGame,
    numberGame,
    quizGame,
    shape2DGame,
    shapes3DGame,
    colorGame,
    animalGame,
    foodGame,
    thingsGame,
    oppositesGame,
    solarGame
};
})();

    </script>
</body>
</html>
