<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Toddler Learning Hub</title>
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Toddler Hub">
    <meta name="theme-color" content="#bae6fd">
    <link rel="icon" type="image/png" sizes="64x64" href="favicon.png?v=2">
    <link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png?v=2">
    <link rel="apple-touch-icon-precomposed" sizes="180x180" href="apple-touch-icon.png?v=2">
    <link rel="manifest" href="manifest.json?v=2">
    <script>
        (function() {
            function syncIOSStandaloneState() {
                var ua = navigator.userAgent || '';
                var isIOS = /iPad|iPhone|iPod/.test(ua) || (navigator.platform === 'MacIntel' && navigator.maxTouchPoints > 1);
                var isStandalone = window.navigator.standalone === true || (window.matchMedia && window.matchMedia('(display-mode: standalone)').matches);
                var root = document.documentElement;
                if (root) {
                    root.classList.toggle('ios-device', Boolean(isIOS));
                    root.classList.toggle('ios-standalone', Boolean(isStandalone));
                }
                return Boolean(isStandalone);
            }
            syncIOSStandaloneState();
            window.addEventListener('DOMContentLoaded', syncIOSStandaloneState, { passive: true });
            window.addEventListener('resize', syncIOSStandaloneState, { passive: true });
            window.addEventListener('pageshow', syncIOSStandaloneState, { passive: true });
            window.addEventListener('orientationchange', function() {
                setTimeout(syncIOSStandaloneState, 60);
            }, { passive: true });
        })();
    </script>

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

        :root {
            --safe-top: env(safe-area-inset-top, 0px);
            --safe-bottom: env(safe-area-inset-bottom, 0px);
            --safe-left: env(safe-area-inset-left, 0px);
            --safe-right: env(safe-area-inset-right, 0px);
        }

        html.ios-standalone {
            --safe-top: max(env(safe-area-inset-top, 0px), 54px);
            --safe-bottom: max(env(safe-area-inset-bottom, 0px), 28px);
        }

        @media (min-width: 768px), (max-height: 500px) {
            html.ios-standalone {
                --safe-top: max(env(safe-area-inset-top, 0px), 28px);
                --safe-bottom: max(env(safe-area-inset-bottom, 0px), 22px);
            }
        }

        html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: #bae6fd;
            -webkit-text-size-adjust: 100%;
        }

        body {
            margin: 0;
            padding: 0;
            position: fixed;
            inset: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            overscroll-behavior: none;
            background-color: #e0f2fe;
            background-image: linear-gradient(135deg, #e0f2fe 0%, #f0fdf4 50%, #fef3c7 100%);
            font-family: 'Nunito', 'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        #menu-top-container {
            padding-top: max(1rem, calc(var(--safe-top) + 0.55rem));
        }

        #menu-top-container.pt-2 {
            padding-top: max(0.5rem, calc(var(--safe-top) + 0.35rem));
        }

        h1, h2, h3, .menu-title, #phonics-big-upper, #phonics-big-lower, #number-big-digit, #solar-title, #shape-text, #shape3d-title, #fruits-text, #animal-text, #things-text, #opp-title {
            font-family: 'Fredoka', 'Nunito', cursive, sans-serif;
        }

        .view-section {
            display: none;
            width: 100%;
            height: 100%;
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
            padding: 0.5rem 1rem max(3rem, calc(var(--safe-bottom) + 2rem)) 1rem;
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
            padding: 0.65rem 0.85rem;
            padding-top: max(0.75rem, calc(var(--safe-top) + 0.45rem));
            position: relative;
            z-index: 50;
            width: 100%;
            max-width: 900px;
            margin: 0 auto;
            flex-shrink: 0;
            gap: 0.5rem;
        }

        .home-btn {
            background: #ffffff;
            padding: 0.6rem 1rem;
            min-height: 42px;
            border-radius: 9999px;
            box-shadow: 0 4px 0 #cbd5e1, 0 8px 16px -2px rgba(15, 23, 42, 0.08);
            border: 2px solid #e2e8f0;
            display: flex;
            align-items: center;
            gap: 0.4rem;
            font-weight: 900;
            color: #334155;
            font-size: 1rem;
            cursor: pointer;
            pointer-events: auto;
            touch-action: manipulation;
            transition: transform 0.1s ease, box-shadow 0.1s ease;
        }

        .home-btn:active {
            transform: translateY(3px);
            box-shadow: 0 1px 0 #cbd5e1;
        }

        .options-quick-btn {
            min-height: 42px;
            min-width: 42px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            pointer-events: auto;
            touch-action: manipulation;
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
            min-height: 38px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            border-radius: 9999px;
            font-weight: 900;
            font-size: 0.85rem;
            color: #475569;
            transition: all 0.15s cubic-bezier(0.34, 1.56, 0.64, 1);
            cursor: pointer;
            pointer-events: auto;
            touch-action: manipulation;
        }

        .mode-pill.active {
            background: #3b82f6;
            color: #ffffff;
            box-shadow: 0 3px 0 #1d4ed8;
            transform: translateY(-1px);
        }

        .main-stage {
            flex: 1;
            min-height: 0;
            container-type: size;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: safe center;
            width: 100%;
            max-width: 860px;
            margin: 0 auto;
            padding: 0.35rem 0.75rem max(0.5rem, calc(var(--safe-bottom) + 0.35rem)) 0.75rem;
            position: relative;
            overflow-y: auto;
            overflow-x: hidden;
            -webkit-overflow-scrolling: touch;
        }

        /* Container Query Responsive Visual Sizing (Item 4) */
        #shape-target {
            width: min(16rem, calc(100cqh - 7.5rem), 82cqw);
            height: min(16rem, calc(100cqh - 7.5rem), 82cqw);
            padding: 0.5rem;
            transition: width 0.22s ease, height 0.22s ease;
        }
        #shape3d-target {
            width: min(18rem, calc(100cqh - 9.5rem), 86cqw);
            height: min(18rem, calc(100cqh - 9.5rem), 86cqw);
            transition: width 0.22s ease, height 0.22s ease;
        }
        #fruits-target {
            width: min(16rem, calc(100cqh - 7rem), 80cqw);
            height: min(16rem, calc(100cqh - 7rem), 80cqw);
            transition: width 0.22s ease, height 0.22s ease;
        }
        #animal-target, #things-target {
            font-size: min(9.5rem, calc(100cqh - 8rem), 40cqw);
            transition: font-size 0.22s ease;
        }
        #view-solar .main-stage {
            flex: 1;
            min-height: 0;
            overflow: hidden !important;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            gap: 0.2rem;
            padding: 0.45rem 0.65rem 0.45rem 0.65rem;
        }
        #solar-stage-row {
            flex: 1;
            min-height: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            position: relative;
        }
        #solar-stage-box {
            width: min(22rem, calc(100cqh - 7.5rem), calc(100cqw - 1.5rem));
            height: min(22rem, calc(100cqh - 7.5rem), calc(100cqw - 1.5rem));
            min-width: 6.5rem;
            min-height: 6.5rem;
            flex-shrink: 0;
            transition: width 0.22s ease, height 0.22s ease;
        }
        @media (min-width: 640px) {
            #solar-stage-box {
                width: min(28rem, calc(100cqh - 8.2rem), calc(100cqw - 3rem));
                height: min(28rem, calc(100cqh - 8.2rem), calc(100cqw - 3rem));
            }
        }
        @media (min-width: 1024px) {
            #solar-stage-box {
                width: min(32rem, calc(100cqh - 8.8rem), calc(100cqw - 4rem));
                height: min(32rem, calc(100cqh - 8.8rem), calc(100cqw - 4rem));
            }
        }
        /* Sleek Single-Row Horizontal Scrollable Planet Selection Tray — Full Visibility */
        #solar-controls-dock {
            height: auto !important;
            min-height: 0 !important;
            max-height: none !important;
            flex-shrink: 0 !important;
            padding: 0.2rem 0.5rem max(0.5rem, calc(var(--safe-bottom) + 0.45rem)) 0.5rem !important;
            background: #0f172a !important;
            backdrop-filter: none !important;
            -webkit-backdrop-filter: none !important;
            border-top: 2px solid #334155 !important;
            overflow: visible !important;
            z-index: 30;
        }
        #solar-controls-dock.dock-collapsed {
            max-height: calc(38px + var(--safe-bottom)) !important;
            padding-bottom: max(0.25rem, calc(var(--safe-bottom) + 0.25rem)) !important;
            overflow: hidden !important;
        }
        #solar-controls-dock .control-scroll {
            height: auto !important;
            overflow-x: auto !important;
            overflow-y: hidden !important;
            touch-action: pan-x !important;
            -webkit-overflow-scrolling: touch;
            padding: 0.15rem 0.35rem 0.35rem 0.35rem !important;
            scrollbar-width: thin;
            scrollbar-color: #475569 transparent;
        }
        #solar-controls-dock .control-scroll::-webkit-scrollbar {
            height: 3px;
        }
        #solar-controls-dock .control-scroll::-webkit-scrollbar-thumb {
            background: #475569;
            border-radius: 9999px;
        }
        #solar-controls {
            display: flex !important;
            flex-wrap: nowrap !important;
            flex-direction: row !important;
            justify-content: flex-start !important;
            align-items: center !important;
            gap: 0.5rem !important;
            width: max-content !important;
            max-width: none !important;
            margin: 0 auto !important;
            padding: 0 0.25rem 4px 0.25rem !important;
        }
        #solar-controls .tray-btn {
            width: 3.5rem !important;
            min-width: 3.5rem !important;
            height: 3.45rem !important;
            min-height: 3.45rem !important;
            padding: 0.2rem 0.1rem !important;
            border-radius: 0.95rem !important;
            background: #1e293b !important;
            border: 2px solid #475569 !important;
            box-shadow: 0 2px 0 #0f172a !important;
            display: flex !important;
            flex-direction: column !important;
            align-items: center !important;
            justify-content: center !important;
            gap: 2px !important;
            flex-shrink: 0 !important;
            overflow: hidden !important;
        }
        #solar-controls .tray-btn:active,
        #solar-controls .tray-btn.selected {
            transform: translateY(1px) !important;
            background: #312e81 !important;
            border-color: #fbbf24 !important;
            box-shadow: 0 0 0 2px rgba(251, 191, 36, 0.45), 0 1px 0 #1e1b4b !important;
        }
        #solar-controls .tray-btn span {
            color: #f1f5f9 !important;
        }
        #solar-svg-holder {
            width: 100%;
            height: 100%;
            background-color: #000000 !important;
            padding: 0 !important;
        }
        #opposites-cards-grid .squish-btn {
            min-height: min(210px, calc(100cqh - 5rem));
            transition: min-height 0.22s ease;
        }
        #opp-emoji-a, #opp-emoji-b {
            font-size: clamp(2.5rem, 14cqh, 5.5rem);
            transition: font-size 0.22s ease;
        }
        #shape3d-canvas-container canvas, #solar-canvas-container canvas {
            width: 100% !important;
            height: 100% !important;
            display: block;
        }
        @supports not (container-type: size) {
            #shape-target { width: 13rem; height: 13rem; }
            #shape3d-target { width: 15rem; height: 15rem; }
            #fruits-target { width: 14rem; height: 14rem; }
            #animal-target, #things-target { font-size: 8rem; }
            #solar-stage-box { width: 19rem; height: 19rem; }
            #opposites-cards-grid .squish-btn { min-height: 180px; }
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
            background: #ffffff;
            backdrop-filter: none;
            -webkit-backdrop-filter: none;
            border-top: 3px solid #e2e8f0;
            border-top-left-radius: 2rem;
            border-top-right-radius: 2rem;
            box-shadow: 0 -8px 28px rgba(15, 23, 42, 0.08);
            padding: 0.35rem 0.65rem 0.75rem 0.65rem;
            padding-bottom: max(0.75rem, calc(var(--safe-bottom) + 0.55rem));
            z-index: 30;
            height: calc(22vh + var(--safe-bottom));
            min-height: calc(118px + var(--safe-bottom));
            max-height: calc(185px + var(--safe-bottom));
            flex-shrink: 0;
            display: flex;
            flex-direction: column;
            transition: height 0.22s ease, min-height 0.22s ease, padding 0.22s ease;
        }

        .controls-dock.dock-collapsed {
            height: auto !important;
            min-height: 0 !important;
            max-height: calc(44px + var(--safe-bottom)) !important;
            padding-top: 0.25rem;
            padding-bottom: max(0.25rem, calc(var(--safe-bottom) + 0.25rem));
        }

        .controls-dock.dock-collapsed .control-scroll {
            display: none !important;
        }

        .dock-toggle-bar {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            padding-bottom: 0.2rem;
            flex-shrink: 0;
        }

        .dock-toggle-btn {
            display: inline-flex;
            align-items: center;
            gap: 0.35rem;
            background: rgba(241, 245, 249, 0.92);
            border: 1.5px solid rgba(203, 213, 225, 0.9);
            color: #475569;
            font-size: 0.68rem;
            font-weight: 800;
            padding: 0.15rem 0.65rem;
            border-radius: 9999px;
            cursor: pointer;
            touch-action: manipulation;
            transition: all 0.15s ease;
            user-select: none;
        }

        .dock-toggle-btn:hover {
            background: #e2e8f0;
            color: #1e293b;
        }

        .dock-toggle-btn:active {
            transform: scale(0.96);
        }

        .controls-dock[style*="0f172a"] .dock-toggle-btn {
            background: rgba(30, 41, 59, 0.9);
            border-color: rgba(71, 85, 105, 0.8);
            color: #cbd5e1;
        }

        .controls-dock[style*="0f172a"] .dock-toggle-btn:hover {
            background: #334155;
            color: #f8fafc;
        }

        .zoom-hud-pill {
            position: absolute;
            top: 0.65rem;
            right: 0.65rem;
            opacity: 0.85;
            cursor: grab;
            transition: opacity 0.15s ease;
            display: inline-flex;
            align-items: center;
            gap: 0.2rem;
            background: rgba(255, 255, 255, 0.94);
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            border: 1.5px solid rgba(203, 213, 225, 0.9);
            border-radius: 9999px;
            box-shadow: 0 4px 12px rgba(15, 23, 42, 0.12);
            padding: 0.15rem 0.4rem;
            font-size: 0.72rem;
            font-weight: 900;
            color: #475569;
            z-index: 35;
            user-select: none;
            touch-action: none;
        }
        .zoom-hud-pill:hover, .zoom-hud-pill:active {
            opacity: 1;
        }
        .zoom-hud-pill.minimized {
            padding: 0.2rem 0.45rem;
            cursor: pointer;
        }
        .zoom-hud-pill.minimized .zoom-controls-group {
            display: none !important;
        }
        .zoom-hud-pill .zoom-min-badge {
            display: none;
        }
        .zoom-hud-pill.minimized .zoom-min-badge {
            display: inline-flex !important;
            align-items: center;
            gap: 0.2rem;
            font-size: 0.75rem;
            font-weight: 900;
            color: #334155;
        }

        .zoom-hud-pill button {
            background: none;
            border: none;
            padding: 0.15rem 0.35rem;
            font-size: 0.75rem;
            font-weight: 900;
            color: #334155;
            cursor: pointer;
            border-radius: 0.5rem;
            transition: background 0.1s ease;
        }

        .zoom-hud-pill button:active {
            background: #e2e8f0;
        }

        .zoom-hud-pill .zoom-reset-btn {
            font-variant-numeric: tabular-nums;
            min-width: 38px;
            text-align: center;
        }

        #view-solar .zoom-hud-pill {
            background: rgba(15, 23, 42, 0.94);
            border-color: rgba(51, 65, 85, 0.9);
            color: #cbd5e1;
        }

        #view-solar .zoom-hud-pill button {
            color: #e2e8f0;
        }

        #view-solar .zoom-hud-pill button:active {
            background: #334155;
        }

        /* 1-Finger Long-Press & Drag Visual Feedback */
        .item-drag-active {
            box-shadow: 0 20px 42px rgba(15, 23, 42, 0.35) !important;
            filter: drop-shadow(0 16px 28px rgba(0, 0, 0, 0.28)) brightness(1.08) !important;
            cursor: grabbing !important;
            z-index: 45 !important;
            transition: filter 0.15s ease, box-shadow 0.15s ease !important;
        }

        .drag-hud-badge {
            position: absolute;
            top: 0.65rem;
            left: 50%;
            transform: translateX(-50%) translateY(-8px) scale(0.85);
            background: rgba(30, 41, 59, 0.94);
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            border: 1.5px solid rgba(255, 255, 255, 0.3);
            color: #ffffff;
            padding: 0.22rem 0.85rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 900;
            letter-spacing: 0.02em;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.28);
            z-index: 50;
            pointer-events: none;
            opacity: 0;
            display: inline-flex;
            align-items: center;
            gap: 0.35rem;
            transition: opacity 0.18s ease, transform 0.18s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .drag-hud-badge.visible {
            opacity: 1;
            transform: translateX(-50%) translateY(0) scale(1);
        }

        #view-solar .drag-hud-badge {
            background: rgba(15, 23, 42, 0.96);
            border-color: rgba(99, 102, 241, 0.6);
            box-shadow: 0 8px 24px rgba(79, 70, 229, 0.3);
        }

        .main-stage {
            touch-action: none;
        }

        #shape-target, #shape3d-target, #animal-target, #fruits-target, #things-target, #solar-stage-box, #color-bg-target, #phonics-main-card, #number-items-grid, #quiz-choices-grid, #opposites-cards-grid {
            touch-action: none !important;
            user-select: none !important;
            -webkit-user-select: none !important;
            -webkit-touch-callout: none !important;
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
            width: 3.85rem;
            height: 3.85rem;
            border-radius: 1.15rem;
            background: #ffffff;
            border: 3px solid #e0e7ff;
            box-shadow: 0 4px 0 #cbd5e1, 0 6px 12px -2px rgba(15, 23, 42, 0.06);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-size: 1.65rem;
            font-weight: 900;
            color: #1e293b;
            cursor: pointer;
            touch-action: manipulation;
            flex-shrink: 0;
            transition: transform 0.1s ease, box-shadow 0.1s ease, border-color 0.1s ease;
        }

        @media (min-width: 640px) {
            .tray-btn {
                width: 4.4rem;
                height: 4.4rem;
                border-radius: 1.35rem;
                font-size: 1.9rem;
                box-shadow: 0 5px 0 #cbd5e1, 0 6px 12px -2px rgba(15, 23, 42, 0.06);
            }
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
            border-radius: 1.35rem;
            padding: 0.5rem 0.35rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-width: 0;
            width: 100%;
            box-shadow: 0 5px 0 #bfdbfe, 0 8px 16px -3px rgba(30, 64, 175, 0.08);
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

        #view-quiz .mode-switch {
            max-width: 100%;
            border-radius: 20px;
            padding: 6px;
        }
        @media (max-width: 480px) {
            #view-quiz .top-bar {
                padding: max(8px, calc(var(--safe-top) + 6px)) 6px 5px 6px;
                gap: 4px;
            }
            #view-quiz .mode-switch {
                border-radius: 20px;
                padding: 5px;
            }
            #view-quiz .quiz-cat-btn {
                padding: 3px 6px;
                font-size: 11px;
                min-height: 36px;
            }
        }
    </style>
    <style id="nb-inline-styles">
/* ==========================================================================
   nb-styles.css - Number Blocks Game Stylesheet
   Toddler Learning Hub - Scoped strictly to #view-blocks & [data-view="blocks"]
   ========================================================================== */

/* Main Full-Viewport Container */
#view-blocks {
  user-select: none;
  -webkit-user-select: none;
  background: linear-gradient(180deg, #bae6fd 0%, #e0f2fe 48%, #fef9c3 78%, #dcfce7 100%);
  font-family: 'Fredoka', 'Nunito', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  color: #1e293b;
  isolation: isolate;
}

#view-blocks:not(.active-view) {
  display: none !important;
  pointer-events: none !important;
}

#view-blocks.active-view {
  display: flex;
  z-index: 20;
}

/* --------------------------------------------------------------------------
   Top Bar & Header Chrome
   -------------------------------------------------------------------------- */
#view-blocks .top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 12px;
  padding-top: max(10px, calc(var(--safe-top) + 6px));
  position: relative;
  z-index: 50;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
  flex-shrink: 0;
  gap: 8px;
  flex-wrap: nowrap;
}

#view-blocks .home-btn {
  background: #ffffff;
  padding: 0.55rem 0.95rem;
  min-height: 42px;
  border-radius: 9999px;
  box-shadow: 0 4px 0 #cbd5e1, 0 8px 16px -2px rgba(15, 23, 42, 0.08);
  border: 2px solid #e2e8f0;
  display: flex;
  align-items: center;
  gap: 0.35rem;
  font-weight: 900;
  color: #334155;
  font-size: 0.95rem;
  flex-shrink: 0;
  white-space: nowrap;
  cursor: pointer;
  pointer-events: auto;
  touch-action: manipulation;
  transition: transform 0.1s ease, box-shadow 0.1s ease;
}

#view-blocks .home-btn:active {
  transform: translateY(2px);
  box-shadow: 0 1px 0 #cbd5e1;
}

#view-blocks .mode-switch {
  display: flex;
  background: #ffffff;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  padding: 0.25rem;
  border-radius: 9999px;
  box-shadow: 0 4px 0 #cbd5e1, 0 8px 16px -2px rgba(15, 23, 42, 0.06);
  border: 2px solid #e2e8f0;
  gap: 0.25rem;
  flex-shrink: 1;
  min-width: 0;
}

#view-blocks .mode-pill {
  padding: 0.45rem 0.85rem;
  min-height: 38px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 9999px;
  font-family: 'Fredoka', 'Nunito', sans-serif;
  font-weight: 700;
  font-size: 0.85rem;
  color: #475569;
  cursor: pointer;
  pointer-events: auto;
  touch-action: manipulation;
  white-space: nowrap;
  border: none;
  background: transparent;
  transition: all 0.15s cubic-bezier(0.34, 1.56, 0.64, 1);
}

#view-blocks .mode-pill.active {
  background: #3b82f6;
  color: #ffffff;
  box-shadow: 0 3px 0 #1d4ed8;
  transform: translateY(-1px);
}

/* Mobile <=480px Compact Top Bar Fit (Guarantees zero wrapping on 375px) */
@media (max-width: 480px) {
  #view-blocks .top-bar {
    padding: max(8px, calc(var(--safe-top) + 6px)) 6px 5px 6px;
    gap: 4px;
    flex-wrap: nowrap;
  }
  #view-blocks .home-btn {
    padding: 5px 8px;
    font-size: 11.5px;
    min-height: 42px;
    gap: 0.25rem;
    flex-shrink: 0;
  }
  #view-blocks .mode-switch {
    padding: 2px;
    gap: 2px;
    flex-shrink: 1;
  }
  #view-blocks .mode-pill {
    padding: 4px 7px;
    font-size: 11px;
    min-height: 38px;
    white-space: nowrap;
  }
  #view-blocks .options-quick-btn {
    padding: 4px 6px !important;
    font-size: 12px !important;
    min-height: 42px !important;
    min-width: 42px !important;
    flex-shrink: 0;
  }
  #view-blocks .audio-vis-pill {
    padding: 4px 5px !important;
    gap: 2px !important;
    flex-shrink: 0;
  }
  #view-blocks #nb-stage-tools,
  #view-blocks .nb-stage-tools {
    gap: 4px;
    margin-right: 2px;
    flex-wrap: nowrap;
  }
  #view-blocks .nb-tool-pill {
    padding: 4px 7px;
    font-size: 11px;
    gap: 3px;
    min-height: 36px;
    white-space: nowrap;
  }
}

/* --------------------------------------------------------------------------
   Stage Area & Canvas
   -------------------------------------------------------------------------- */
#view-blocks #nb-stage-wrap,
#view-blocks .nb-stage-wrap {
  position: relative;
  flex: 1 1 auto;
  min-height: 0;
  width: 100%;
  overflow: hidden;
  touch-action: none;
}

#view-blocks #nb-stage-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  touch-action: none;
  z-index: 1;
  display: block;
}

/* --------------------------------------------------------------------------
   HUD Overlay (Pure flex, non-blocking to canvas)
   -------------------------------------------------------------------------- */
#view-blocks #nb-hud-overlay,
#view-blocks .nb-hud-overlay {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 20;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 6px 8px 0;
  gap: 6px;
}

/* Interactive Challenge Bar Pill */
#view-blocks #nb-challenge-bar,
#view-blocks .nb-challenge-bar {
  pointer-events: auto;
  width: min(96%, 620px);
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #ffffff;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  border: 2.5px solid #e2e8f0;
  border-radius: 9999px;
  box-shadow: 0 5px 0 rgba(148, 163, 184, 0.35), 0 10px 22px -3px rgba(15, 23, 42, 0.12);
  padding: 5px 12px;
  gap: 8px;
  transition: opacity 0.2s ease, transform 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
}

#view-blocks #nb-challenge-bar.hidden,
#view-blocks .nb-challenge-bar.hidden {
  display: none !important;
}

#view-blocks #nb-challenge-speak-btn {
  display: flex;
  align-items: center;
  gap: 4px;
  background: #eff6ff;
  border: 2px solid #bfdbfe;
  border-radius: 9999px;
  padding: 3px 8px;
  cursor: pointer;
  flex-shrink: 0;
  transition: transform 0.1s ease;
}

#view-blocks #nb-challenge-speak-btn:active {
  transform: scale(0.94);
}

#view-blocks #nb-challenge-icon {
  width: 32px;
  height: 32px;
  border-radius: 8px;
  display: block;
}

#view-blocks #nb-challenge-text,
#view-blocks .nb-challenge-text {
  font-family: 'Nunito', 'Fredoka', sans-serif;
  font-weight: 800;
  font-size: clamp(12px, 2.8vw, 16px);
  color: #1e293b;
  text-align: center;
  flex: 1 1 auto;
  min-width: 0;
  line-height: 1.25;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

#view-blocks .nb-challenge-actions {
  display: flex;
  align-items: center;
  gap: 4px;
  flex-shrink: 0;
}

#view-blocks #nb-challenge-stars,
#view-blocks .nb-star-pill {
  background: #fef9c3;
  border: 2px solid #fde047;
  color: #854d0e;
  font-family: 'Fredoka', sans-serif;
  font-weight: 700;
  font-size: 13px;
  padding: 4px 8px;
  border-radius: 9999px;
  box-shadow: 0 2px 0 #facc15;
  display: inline-flex;
  align-items: center;
}

#view-blocks .nb-mini-btn {
  background: #ffffff;
  border: 2px solid #e2e8f0;
  border-radius: 9999px;
  box-shadow: 0 3px 0 #cbd5e1;
  padding: 4px 8px;
  font-size: 14px;
  cursor: pointer;
  transition: transform 0.1s ease, box-shadow 0.1s ease;
  line-height: 1;
}

#view-blocks .nb-mini-btn:active {
  transform: translateY(2px);
  box-shadow: 0 1px 0 #cbd5e1;
}

/* Floating Stage Tools (Split, Unlock, Reset) */
#view-blocks #nb-stage-tools,
#view-blocks .nb-stage-tools {
  pointer-events: auto;
  align-self: flex-end;
  display: flex;
  gap: 6px;
  margin-right: 4px;
}

#view-blocks .nb-tool-pill {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  background: #ffffff;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  border: 2px solid #e2e8f0;
  border-radius: 9999px;
  box-shadow: 0 3px 0 #cbd5e1, 0 6px 14px -2px rgba(15, 23, 42, 0.08);
  padding: 6px 12px;
  font-family: 'Fredoka', sans-serif;
  font-weight: 700;
  font-size: 13px;
  color: #334155;
  min-height: 44px;
  cursor: pointer;
  pointer-events: auto;
  touch-action: manipulation;
  transition: all 0.15s cubic-bezier(0.34, 1.56, 0.64, 1);
}

#view-blocks .nb-tool-pill:active {
  transform: translateY(2px);
  box-shadow: 0 1px 0 #cbd5e1;
}

/* Split Tool Active Warm Amber Glow */
#view-blocks #nb-tool-split.is-active {
  background: #fffbeb;
  border-color: #f59e0b;
  color: #b45309;
  box-shadow: 0 0 0 2px #fef3c7, 0 0 12px rgba(245, 158, 11, 0.45), 0 3px 0 #d97706;
  transform: translateY(-1px);
}

/* --------------------------------------------------------------------------
   Tactile Spawner Dock & Tiles
   -------------------------------------------------------------------------- */
#view-blocks #nb-dock,
#view-blocks .nb-dock {
  z-index: 20;
  touch-action: none;
  flex-shrink: 0;
  padding: 8px 10px max(10px, calc(var(--safe-bottom) + 8px));
  background: #ffffff;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  border-top: 2.5px solid #e2e8f0;
  box-shadow: 0 -4px 16px rgba(15, 23, 42, 0.08);
}

#view-blocks .nb-dock-tile {
  touch-action: none;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: #ffffff;
  border: 2px solid #e2e8f0;
  border-radius: 16px;
  box-shadow: 0 3px 0 #cbd5e1, 0 6px 12px -2px rgba(15, 23, 42, 0.06);
  cursor: pointer;
  pointer-events: auto;
  padding: 4px;
  gap: 2px;
  transition: transform 0.12s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.12s ease;
  user-select: none;
  -webkit-user-select: none;
}

#view-blocks .nb-dock-tile:active {
  transform: translateY(2px) scale(0.97);
  box-shadow: 0 1px 0 #cbd5e1;
}

#view-blocks .nb-dock-canvas {
  display: block;
  pointer-events: none;
}

#view-blocks .nb-dock-num {
  font-family: 'Fredoka', sans-serif;
  font-weight: 700;
  font-size: 13px;
  color: #1e293b;
  line-height: 1;
  pointer-events: none;
}

/* Hero "1" Tile Highlight */
#view-blocks .nb-dock-tile.is-hero {
  border-color: #fca5a5;
  background: linear-gradient(180deg, #ffffff 0%, #fef2f2 100%);
  box-shadow: 0 3px 0 #f87171, 0 6px 14px -2px rgba(239, 68, 68, 0.2);
}

#view-blocks .nb-dock-tile.is-hero .nb-dock-num {
  color: #dc2626;
  font-weight: 800;
}

/* Locked Tile Treatment (6..10 initially) */
#view-blocks .nb-dock-tile.is-locked {
  opacity: 0.65;
  background: #f1f5f9;
  border-color: #cbd5e1;
  box-shadow: 0 2px 0 #94a3b8;
}

#view-blocks .nb-dock-tile.is-locked .nb-dock-num {
  color: #64748b;
  font-weight: 800;
}

/* Hint Glow Treatment */
#view-blocks .nb-dock-tile.is-hint {
  border-color: #facc15;
  background: #fefce8;
  box-shadow: 0 0 0 3px #fef08a, 0 0 16px rgba(250, 204, 21, 0.65), 0 3px 0 #ca8a04;
  animation: nb-hint-pulse 1.4s ease-in-out infinite alternate;
}

@keyframes nb-hint-pulse {
  0% {
    transform: scale(1);
    box-shadow: 0 0 0 2px #fef08a, 0 0 10px rgba(250, 204, 21, 0.5), 0 3px 0 #ca8a04;
  }
  100% {
    transform: scale(1.04);
    box-shadow: 0 0 0 4px #facc15, 0 0 22px rgba(250, 204, 21, 0.8), 0 4px 0 #ca8a04;
  }
}

/* Wiggle Feedback for Locked Tile Tap */
@keyframes nb-wiggle {
  0%, 100% { transform: translateX(0); }
  20% { transform: translateX(-4px) rotate(-3deg); }
  40% { transform: translateX(4px) rotate(3deg); }
  60% { transform: translateX(-3px) rotate(-1.5deg); }
  80% { transform: translateX(3px) rotate(1.5deg); }
}

#view-blocks .nb-dock-tile.is-wiggling {
  animation: nb-wiggle 0.4s ease;
}

/* --------------------------------------------------------------------------
   Responsive Dock Grid & Flex Layouts (Scroll-Free Guarantee)
   -------------------------------------------------------------------------- */

/* Desktop & Tablet (>= 768px): Single Centered 10-Column Flex Row */
@media (min-width: 768px) {
  #view-blocks #nb-dock-friends,
  #view-blocks .nb-dock-friends {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
    max-width: 820px;
    margin: 0 auto;
  }

  #view-blocks .nb-dock-tile {
    width: 56px;
    height: 56px;
    min-width: 56px;
    border-radius: 16px;
  }
}

/* Short Landscape (max-height: 500px): Ultra-Compact Single Row */
@media (max-height: 500px) {
  #view-blocks #nb-dock,
  #view-blocks .nb-dock {
    padding: 3px 8px max(4px, calc(var(--safe-bottom) + 3px));
  }

  #view-blocks #nb-dock-friends,
  #view-blocks .nb-dock-friends {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4px;
    max-width: 620px;
    margin: 0 auto;
  }

  #view-blocks .nb-dock-tile {
    width: 40px;
    height: 40px;
    min-width: 40px;
    padding: 2px;
    border-radius: 10px;
  }

  #view-blocks .nb-dock-num {
    font-size: 10px;
  }

  #view-blocks #nb-hud-overlay,
  #view-blocks .nb-hud-overlay {
    padding: 2px 6px 0;
    gap: 3px;
  }

  #view-blocks #nb-challenge-bar,
  #view-blocks .nb-challenge-bar {
    padding: 3px 8px;
  }

  #view-blocks .nb-tool-pill {
    min-height: 36px;
    padding: 4px 8px;
    font-size: 11px;
  }
}

/* Portrait Mobile (< 768px and > 500px height): Symmetrical 5x2 Grid */
@media (max-width: 767px) and (min-height: 501px) {
  #view-blocks #nb-dock-friends,
  #view-blocks .nb-dock-friends {
    display: grid;
    grid-template-columns: repeat(5, minmax(0, 1fr));
    gap: 6px;
    max-width: 380px;
    margin: 0 auto;
  }

  #view-blocks .nb-dock-tile {
    min-height: 50px;
    padding: 4px 2px;
  }

  #view-blocks .nb-dock-num {
    font-size: 12px;
  }
}

/* --------------------------------------------------------------------------
   Hub Main Menu Card (12th Card)
   -------------------------------------------------------------------------- */
.menu-card[data-view="blocks"] {
  position: relative;
  transition: transform 0.15s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.15s ease;
}

.menu-card[data-view="blocks"]:hover {
  transform: translateY(-2px);
}

    </style>
</head>
<body>

    <!-- MAIN MENU -->
    <div id="view-menu" class="view-section active-view" style="background: linear-gradient(135deg, #e0f2fe 0%, #f0fdf4 50%, #fef3c7 100%); z-index: 10;">
        <div id="menu-top-container" class="text-center pt-4 pb-2 px-4 flex-shrink-0 transition-all duration-200">
            <div id="menu-header-banner" class="transition-all duration-200 overflow-hidden">
                <div class="inline-flex items-center gap-2 bg-white px-4 py-1 rounded-full shadow-sm border border-sky-200 mb-1">
                    <span class="text-xl">🌟</span>
                    <span class="text-xs font-black uppercase tracking-wider text-sky-700">Toddler Explorer • Level 2</span>
                </div>
                <h1 class="text-4xl sm:text-5xl font-black text-slate-800 tracking-tight">Toddler Learning Hub</h1>
                <p class="text-slate-600 font-bold text-sm sm:text-base mt-0.5">Tap any card to play, count & sound it out!</p>
            </div>
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
                <button id="menu-minimize-btn" class="inline-flex items-center gap-1.5 bg-white px-3.5 py-1.5 rounded-full shadow-sm border-2 border-sky-200 text-xs sm:text-sm font-black text-sky-700 squish-btn hover:bg-sky-50" title="Minimize or Expand Header">
                    <span id="menu-minimize-icon">🔼</span>
                    <span id="menu-minimize-label">Minimize</span>
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

                <div data-view="blocks" class="menu-card border-b-8 border-rose-400 squish-btn">
                    <span class="absolute top-2.5 right-3 bg-rose-100 text-rose-700 text-xs font-black px-2 py-0.5 rounded-full">Magic!</span>
                    <div class="menu-icon">
                        <svg width="56" height="56" viewBox="0 0 64 64" aria-hidden="true">
                          <!-- Sparkle -->
                          <path d="M18 11 L19.6 15.2 L23.8 16.8 L19.6 18.4 L18 22.6 L16.4 18.4 L12.2 16.8 L16.4 15.2 Z" fill="#facc15" stroke="#ca8a04" stroke-width="0.8" stroke-linejoin="round"/>
                        
                          <!-- ONE (Left): Arms, Legs & Shoes -->
                          <g id="menu-one">
                            <!-- Deep-red waving arms + mitts -->
                            <path d="M8.5 41 Q3 35 3.5 29" fill="none" stroke="#991b1b" stroke-width="3" stroke-linecap="round"/>
                            <circle cx="3.5" cy="28.5" r="2.3" fill="#991b1b"/>
                            <path d="M26.5 41 Q29.5 39 30.2 35.5" fill="none" stroke="#991b1b" stroke-width="2.8" stroke-linecap="round"/>
                            <circle cx="30.2" cy="35" r="2.0" fill="#991b1b"/>
                            <!-- Legs & Shoes -->
                            <line x1="13.5" y1="51" x2="13.5" y2="56.5" stroke="#991b1b" stroke-width="3" stroke-linecap="round"/>
                            <ellipse cx="12" cy="57" rx="3.8" ry="2.2" fill="#991b1b"/>
                            <line x1="21.5" y1="51" x2="21.5" y2="56.5" stroke="#991b1b" stroke-width="3" stroke-linecap="round"/>
                            <ellipse cx="23" cy="57" rx="3.8" ry="2.2" fill="#991b1b"/>
                            <!-- Red Cube -->
                            <rect x="7.5" y="31" width="20" height="20" rx="2" fill="#ef4444" stroke="#b91c1c" stroke-width="2"/>
                            <path d="M9.5 33 H25.5 V35 H11.5 V49 H9.5 Z" fill="#ffffff" opacity="0.28"/>
                            <!-- Cyclops Eye (dark-red rim, NO eyebrow) -->
                            <circle cx="17.5" cy="39.5" r="4.8" fill="#ffffff" stroke="#991b1b" stroke-width="1.8"/>
                            <circle cx="17.5" cy="39.5" r="2.3" fill="#0f172a"/>
                            <circle cx="16.7" cy="38.6" r="0.85" fill="#ffffff"/>
                            <!-- Curved Smile -->
                            <path d="M13.8 46.2 Q17.5 49 21.2 46.2" fill="none" stroke="#991b1b" stroke-width="1.7" stroke-linecap="round"/>
                          </g>
                        
                          <!-- TWO (Right): Arms, Legs & Two-Tone Dancing Shoes -->
                          <g id="menu-two">
                            <!-- Purple-plum arms + mitts -->
                            <path d="M38.5 31 Q34.5 34 34.2 39" fill="none" stroke="#6b21a8" stroke-width="2.8" stroke-linecap="round"/>
                            <circle cx="34.2" cy="39.5" r="2.0" fill="#6b21a8"/>
                            <path d="M57.5 31 Q61.2 27 61.2 22.5" fill="none" stroke="#6b21a8" stroke-width="3" stroke-linecap="round"/>
                            <circle cx="61.2" cy="22" r="2.3" fill="#6b21a8"/>
                            <!-- Purple legs -->
                            <line x1="43.5" y1="51" x2="43.5" y2="56.5" stroke="#6b21a8" stroke-width="3" stroke-linecap="round"/>
                            <line x1="52.5" y1="51" x2="52.5" y2="56.5" stroke="#6b21a8" stroke-width="3" stroke-linecap="round"/>
                            <!-- Two-tone orange-and-cream dancing shoes -->
                            <ellipse cx="42" cy="57" rx="4.1" ry="2.3" fill="#ea580c" stroke="#9a3412" stroke-width="0.9"/>
                            <path d="M38.2 57.3 Q42 59.2 45.8 57.3 L45.4 58.3 Q42 59.6 38.6 58.3 Z" fill="#fed7aa"/>
                            <circle cx="39.2" cy="56.8" r="1.5" fill="#fed7aa"/>
                            <ellipse cx="54" cy="57" rx="4.1" ry="2.3" fill="#ea580c" stroke="#9a3412" stroke-width="0.9"/>
                            <path d="M50.2 57.3 Q54 59.2 57.8 57.3 L57.4 58.3 Q54 59.6 50.6 58.3 Z" fill="#fed7aa"/>
                            <circle cx="56.8" cy="56.8" r="1.5" fill="#fed7aa"/>
                        
                            <!-- Flush Stacked Golden-Orange 1x2 Blocks -->
                            <rect x="38" y="31" width="20" height="20" rx="2" fill="#f97316" stroke="#c2410c" stroke-width="2"/>
                            <path d="M40 33 H56 V35 H42 V49 H40 Z" fill="#ffffff" opacity="0.28"/>
                            <rect x="38" y="11" width="20" height="20" rx="2" fill="#f97316" stroke="#c2410c" stroke-width="2"/>
                            <path d="M40 13 H56 V15 H42 V29 H40 Z" fill="#ffffff" opacity="0.28"/>
                        
                            <!-- Bold Purple Rounded-Rectangle Glasses with Bridge -->
                            <line x1="46.6" y1="19.5" x2="49.4" y2="19.5" stroke="#9333ea" stroke-width="2"/>
                            <rect x="39.4" y="15.6" width="7.8" height="7.6" rx="2" fill="#ffffff" stroke="#9333ea" stroke-width="1.8"/>
                            <rect x="48.8" y="15.6" width="7.8" height="7.6" rx="2" fill="#ffffff" stroke="#9333ea" stroke-width="1.8"/>
                            <!-- Eyes inside glasses -->
                            <circle cx="43.3" cy="19.4" r="1.65" fill="#0f172a"/>
                            <circle cx="42.7" cy="18.8" r="0.6" fill="#ffffff"/>
                            <circle cx="52.7" cy="19.4" r="1.65" fill="#0f172a"/>
                            <circle cx="52.1" cy="18.8" r="0.6" fill="#ffffff"/>
                            <!-- Coral-pink curved smile -->
                            <path d="M44.2 26.2 Q48 28.8 51.8 26.2" fill="none" stroke="#e11d48" stroke-width="1.7" stroke-linecap="round"/>
                          </g>
                        </svg>
                    </div>
                    <span class="menu-title">Number Blocks</span>
                    <span class="menu-sub">Stack, Add &amp; Split!</span>
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
            <div id="phonics-zoom-target" class="flex flex-col items-center w-full max-w-md origin-center">
                <div id="phonics-main-card" class="bg-white rounded-3xl p-2.5 sm:p-4 shadow-lg border-4 border-blue-200 flex flex-col items-center w-full max-w-md cursor-pointer squish-btn">
                    <div class="flex items-baseline gap-3">
                        <span id="phonics-big-upper" class="text-7xl sm:text-8xl font-black text-blue-600 leading-none">A</span>
                        <span id="phonics-big-lower" class="text-6xl sm:text-7xl font-black text-sky-500 leading-none">a</span>
                    </div>
                    <div id="phonics-sound-pill" class="mt-1.5 bg-amber-100 text-amber-900 font-black px-4 py-0.5 rounded-full text-sm sm:text-base border-2 border-amber-300">
                        🔊 Sound: "ah" (like Apple)
                    </div>
                </div>
                <p class="text-[11px] sm:text-xs font-extrabold text-slate-500 uppercase tracking-wider mt-1.5 mb-1">Tap a picture to sound it out!</p>
                <div id="phonics-words-row" class="grid grid-cols-3 gap-2 sm:gap-3 w-full max-w-md px-1"></div>
                <div id="phonics-blend-bar" class="hidden mt-1.5 bg-blue-100/90 border-2 border-blue-300 px-3 py-1 rounded-2xl flex items-center justify-center gap-1.5 shadow-sm max-w-md w-full">
                    <span class="text-xs font-black uppercase tracking-wider text-blue-800">Sound it out:</span>
                    <div id="phonics-blend-letters" class="flex items-center gap-1 text-xs sm:text-sm font-black text-blue-900"></div>
                </div>
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

        <div class="main-stage justify-between py-1">
            <div class="flex flex-col items-center justify-center text-center mb-1 flex-shrink-0 w-full">
                <div class="flex items-center justify-center gap-2">
                    <div id="number-big-digit" class="text-4xl sm:text-6xl font-black text-teal-700 leading-none cursor-pointer squish-btn">1</div>
                    <span id="number-word-label" class="text-lg sm:text-2xl font-black text-slate-800 leading-tight">One</span>
                </div>
                <div class="flex flex-wrap items-center justify-center gap-2 mt-0.5">
                    <span id="number-instruction" class="text-[11px] sm:text-xs font-extrabold text-teal-600 bg-teal-100 px-2.5 py-0.5 rounded-full text-center">Tap each ☀️ to count! (0/1)</span>
                    <button id="number-count-all-btn" class="bg-teal-600 text-white font-black px-2.5 py-1 sm:px-3 sm:py-1 rounded-2xl shadow-md text-xs squish-btn flex items-center gap-1">🔊 Count All</button>
                    <button id="number-open-blocks-btn" type="button" class="bg-rose-500 hover:bg-rose-600 text-white font-black px-2.5 py-1 sm:px-3 sm:py-1 rounded-2xl shadow-md text-xs squish-btn flex items-center gap-1">🧱 Build Block</button>
                </div>
            </div>
            <div id="number-items-grid" class="flex-1 min-h-0 w-full max-w-xl flex flex-wrap justify-center items-center content-center gap-1.5 sm:gap-2.5 px-1 my-1"></div>
            <div id="number-ten-frame" class="flex-shrink-0 z-10 mt-1 mb-1 flex gap-1.5 flex-wrap justify-center bg-white px-3 py-1.5 rounded-2xl border-2 border-teal-200 shadow-sm"></div>
        </div>

        <div class="controls-dock">
            <div class="control-scroll"><div class="control-grid" id="number-controls"></div></div>
        </div>
    </div>

    <!-- VIEW: NUMBER BLOCKS -->
    <div id="view-blocks" class="view-section bg-sky-100">
        <div class="top-bar">
            <button data-action="home" class="home-btn squish-btn"><span>🏠</span><span>Home</span></button>
            <div class="mode-switch">
                <button id="nb-mode-play" type="button" class="mode-pill active">🧱 Free Play</button>
                <button id="nb-mode-challenge" type="button" class="mode-pill">⭐ Challenges</button>
            </div>
            <div class="flex items-center gap-1.5 flex-shrink-0">
                <button class="options-quick-btn bg-white hover:bg-slate-100 text-slate-700 font-black px-2.5 py-1.5 rounded-full shadow-sm border-2 border-slate-200 squish-btn text-sm" title="Options & Settings">⚙️</button>
                <div class="audio-vis-pill" title="Audio Activity"><span class="vis-bar bar-1"></span><span class="vis-bar bar-2"></span><span class="vis-bar bar-3"></span><span class="vis-bar bar-4"></span></div>
            </div>
        </div>
        <div id="nb-stage-wrap" class="nb-stage-wrap">
            <canvas id="nb-stage-canvas"></canvas>
            <div id="nb-hud-overlay" class="nb-hud-overlay">
                <div id="nb-challenge-bar" class="nb-challenge-bar hidden">
                    <button id="nb-challenge-speak-btn" type="button" class="nb-icon-btn squish-btn" title="Hear Prompt">
                        <canvas id="nb-challenge-icon" width="40" height="40"></canvas>
                        <span>🔊</span>
                    </button>
                    <span id="nb-challenge-text" class="nb-challenge-text">Put One and One together!</span>
                    <div class="nb-challenge-actions">
                        <span id="nb-challenge-stars" class="nb-star-pill">⭐ 0</span>
                        <button id="nb-challenge-hint-btn" type="button" class="nb-mini-btn squish-btn" title="Hint">💡</button>
                        <button id="nb-challenge-skip-btn" type="button" class="nb-mini-btn squish-btn" title="Next Challenge">⏭️</button>
                    </div>
                </div>
                <div id="nb-stage-tools" class="nb-stage-tools">
                    <button id="nb-tool-count" type="button" class="nb-tool-pill squish-btn" title="Count in Tap & Count"><span>🔢</span><span>Count</span></button>
                    <button id="nb-tool-split" type="button" class="nb-tool-pill squish-btn" aria-pressed="false"><span>🪄</span><span>Split</span></button>
                    <button id="nb-tool-unlock" type="button" class="nb-tool-pill squish-btn" title="Unlock 1 to 10"><span>🔓</span><span>1–10</span></button>
                    <button id="nb-tool-reset" type="button" class="nb-tool-pill squish-btn" title="Reset Stage"><span>🧹</span><span>Reset</span></button>
                </div>
            </div>
        </div>
        <div id="nb-dock" class="nb-dock" aria-label="Number Blocks Spawner">
            <div id="nb-dock-friends" class="nb-dock-friends"></div>
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
                <button data-quiz-cat="blocks" class="mode-pill quiz-cat-btn">🧱 Blocks</button>
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
            <div id="quiz-prompt-box" class="bg-white px-5 py-3 rounded-3xl shadow-md border-4 border-amber-300 text-center max-w-md w-full mb-3 cursor-pointer squish-btn">
                <p class="text-[11px] sm:text-xs font-black uppercase tracking-wider text-amber-600 mb-0.5">Tap to hear again 🔊</p>
                <h2 id="quiz-question-text" class="text-xl sm:text-2xl font-black text-slate-800">Can you find the Lion?</h2>
            </div>
            <div id="quiz-choices-grid" class="grid grid-cols-3 gap-2.5 sm:gap-4 w-full max-w-xl px-2"></div>
            <div class="mt-3 flex items-center gap-3">
                <div class="bg-white px-4 py-1.5 rounded-full font-black text-amber-700 border-2 border-amber-200 shadow-sm">
                    ⭐ Stars: <span id="quiz-score">0</span>
                </div>
                <button id="quiz-next-btn" class="bg-amber-500 text-white font-black px-4 py-1.5 rounded-full shadow-md squish-btn text-sm">Next Question ➡️</button>
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
            <div id="shape-target" class="w-52 h-52 sm:w-64 sm:h-64 p-2 flex items-center justify-center cursor-pointer squish-btn"></div>
            <h1 id="shape-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-1">Circle</h1>
            <div id="shape-realworld" class="mt-1.5 bg-white px-4 py-1 rounded-full border-2 border-emerald-200 font-extrabold text-slate-700 text-xs sm:text-sm shadow-sm">
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
            <div id="shape3d-target" class="w-60 h-60 sm:w-72 sm:h-72 flex items-center justify-center relative">
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
                <h1 id="color-text" class="text-5xl sm:text-6xl font-black tracking-tight transition-all duration-200">Red</h1>
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
            <div id="animal-target" class="text-[8rem] sm:text-[9.5rem] p-2 leading-none cursor-pointer squish-btn">🦁</div>
            <h1 id="animal-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-1">Lion</h1>
            <div id="animal-sound-pill" class="mt-1.5 bg-white px-5 py-1.5 rounded-full border-2 border-orange-300 font-black text-orange-700 text-base sm:text-lg shadow-sm cursor-pointer squish-btn">
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
            <div id="fruits-target" class="relative w-56 h-56 sm:w-64 sm:h-64 flex items-center justify-center cursor-pointer squish-btn">
                <canvas id="fruits-canvas" width="240" height="240" class="w-full h-full"></canvas>
            </div>
            <h1 id="fruits-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-1">Strawberry</h1>
            <div id="fruits-desc" class="mt-1 bg-white px-4 py-1 rounded-full border-2 border-pink-200 font-extrabold text-pink-700 text-xs sm:text-sm shadow-sm">
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
            <div id="things-target" class="text-[8rem] sm:text-[9.5rem] p-2 leading-none cursor-pointer squish-btn">🚒</div>
            <h1 id="things-text" class="text-4xl sm:text-5xl font-black text-slate-800 mt-1">Fire Truck</h1>
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
            <div id="opposites-cards-grid" class="grid grid-cols-2 gap-3 sm:gap-5 w-full max-w-lg px-2">
                <div id="opp-card-a" class="bg-white rounded-3xl p-4 sm:p-5 shadow-md border-4 border-cyan-300 flex flex-col items-center justify-center min-h-[180px] sm:min-h-[210px] cursor-pointer squish-btn">
                    <div id="opp-emoji-a" class="text-7xl sm:text-8xl mb-1 sm:mb-2">🐘</div>
                    <span id="opp-label-a" class="text-xl sm:text-3xl font-black text-slate-800">Big</span>
                </div>
                <div id="opp-card-b" class="bg-white rounded-3xl p-4 sm:p-5 shadow-md border-4 border-amber-300 flex flex-col items-center justify-center min-h-[180px] sm:min-h-[210px] cursor-pointer squish-btn">
                    <div id="opp-emoji-b" class="text-4xl sm:text-5xl mb-1 sm:mb-2">🐁</div>
                    <span id="opp-label-b" class="text-xl sm:text-3xl font-black text-slate-800">Small</span>
                </div>
            </div>
            <h2 id="opp-title" class="text-xl sm:text-2xl font-black text-slate-700 mt-2">Big vs. Small</h2>
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
            <!-- Compact Orbit Status & Drawer Launcher Bar (Upgrade 2b, visible only in Orbit mode) -->
            <div id="solar-orbit-controls" class="hidden flex flex-wrap items-center justify-center gap-2 mb-0.5 z-20">
                <button id="solar-play-pause-quick-btn" type="button" class="min-h-[36px] px-3.5 py-1 rounded-full bg-slate-900/90 hover:bg-slate-800 text-amber-300 border border-amber-400/40 font-black text-xs shadow-md squish-btn flex items-center gap-1.5" title="Play / Pause simulation">
                    <span id="solar-quick-play-icon">⏸</span>
                    <span id="solar-quick-play-label">Playing</span>
                </button>
                <button id="solar-orbit-drawer-btn" type="button" class="min-h-[36px] px-3.5 py-1 rounded-full bg-indigo-600 hover:bg-indigo-500 text-white border-2 border-indigo-300/60 font-black text-xs sm:text-sm shadow-lg squish-btn flex items-center gap-1.5" title="Open Orbit Controls">
                    <span>🎛️</span>
                    <span>Orbit Controls</span>
                    <span id="solar-orbit-summary-badge" class="bg-indigo-950/80 text-amber-300 px-2 py-0.5 rounded-full text-[11px] font-extrabold">1x</span>
                </button>
            </div>

            <!-- Slide-Out Side Control Panel (Upgrade 2b, tucked on side, hidden by default) -->
            <div id="solar-orbit-drawer" class="hidden absolute top-2 right-2 sm:right-4 z-40 w-72 sm:w-80 max-h-[calc(100%-1rem)] overflow-y-auto bg-slate-900/95 backdrop-blur-xl border-2 border-indigo-400/60 rounded-3xl p-4 shadow-2xl text-white flex flex-col gap-3.5 transition-all duration-200">
                <!-- Drawer Header -->
                <div class="flex items-center justify-between border-b border-slate-700/80 pb-2.5">
                    <div class="flex items-center gap-2">
                        <span class="text-xl">🪐</span>
                        <div>
                            <h3 class="text-sm font-black text-white leading-tight">Orbit Controls</h3>
                            <p class="text-[11px] text-indigo-300 font-bold">Speed, Motion & Time Travel</p>
                        </div>
                    </div>
                    <button id="solar-orbit-drawer-close" type="button" class="w-8 h-8 rounded-full bg-slate-800 hover:bg-slate-700 text-slate-300 hover:text-white font-black text-sm flex items-center justify-center squish-btn" title="Close Panel">✕</button>
                </div>

                <!-- Section 1 — Playback & Turbo -->
                <div class="grid grid-cols-2 gap-2">
                    <button id="solar-play-pause-btn" type="button" class="min-h-[42px] rounded-2xl bg-indigo-600 hover:bg-indigo-500 text-white font-black text-xs sm:text-sm flex items-center justify-center gap-1.5 shadow-md squish-btn">
                        <span id="solar-play-icon">⏸</span>
                        <span id="solar-play-label">Pause</span>
                    </button>
                    <button id="solar-turbo-btn" type="button" class="min-h-[42px] rounded-2xl bg-amber-400 hover:bg-amber-300 text-slate-950 font-black text-xs sm:text-sm flex items-center justify-center gap-1.5 shadow-md squish-btn">
                        <span>🚀</span>
                        <span>Turbo Boost</span>
                    </button>
                </div>

                <!-- Section 2 — Orbit Speed Control -->
                <div class="bg-slate-800/90 border border-slate-700 rounded-2xl p-3 flex flex-col gap-2.5">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-black uppercase tracking-wider text-slate-300">⚡ Orbit Speed</span>
                        <button id="solar-speed-btn" type="button" class="px-2.5 py-0.5 rounded-lg bg-amber-500/20 text-amber-300 border border-amber-400/40 font-black text-xs squish-btn" title="Click to cycle speed">⚡ 1x</button>
                    </div>
                    <div class="flex items-center gap-2">
                        <button id="solar-speed-down-btn" type="button" class="w-9 h-9 rounded-xl bg-slate-700 hover:bg-slate-600 text-white font-black text-sm flex items-center justify-center squish-btn flex-shrink-0" title="Slower">🐢</button>
                        <input type="range" id="solar-speed-slider" min="0.25" max="10" step="0.25" value="1" class="flex-1 accent-amber-400 cursor-pointer h-2" title="Orbit Speed">
                        <button id="solar-speed-up-btn" type="button" class="w-9 h-9 rounded-xl bg-slate-700 hover:bg-slate-600 text-white font-black text-sm flex items-center justify-center squish-btn flex-shrink-0" title="Faster">🚀</button>
                    </div>
                    <div class="grid grid-cols-6 gap-1">
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-slate-900/80 hover:bg-indigo-900 text-slate-200 border border-slate-600/80 font-extrabold text-[11px] squish-btn text-center" data-speed="0.25">0.25x</button>
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-slate-900/80 hover:bg-indigo-900 text-slate-200 border border-slate-600/80 font-extrabold text-[11px] squish-btn text-center" data-speed="0.5">0.5x</button>
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-amber-400 text-slate-950 border-amber-300 font-extrabold text-[11px] squish-btn text-center" data-speed="1">1x</button>
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-slate-900/80 hover:bg-indigo-900 text-slate-200 border border-slate-600/80 font-extrabold text-[11px] squish-btn text-center" data-speed="2">2x</button>
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-slate-900/80 hover:bg-indigo-900 text-slate-200 border border-slate-600/80 font-extrabold text-[11px] squish-btn text-center" data-speed="5">5x</button>
                        <button type="button" class="solar-speed-preset py-1 rounded-lg bg-slate-900/80 hover:bg-indigo-900 text-slate-200 border border-slate-600/80 font-extrabold text-[11px] squish-btn text-center" data-speed="10">10x</button>
                    </div>
                </div>

                <!-- Section 3 — On-Demand Date / Time Travel -->
                <div class="bg-slate-800/90 border border-slate-700 rounded-2xl p-3 flex flex-col gap-2">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-black uppercase tracking-wider text-slate-300">📅 Planet Date</span>
                        <button id="solar-date-toggle-btn" type="button" class="bg-indigo-600/90 hover:bg-indigo-500 text-white font-black text-xs px-3 py-1 rounded-xl shadow-sm squish-btn flex items-center gap-1">
                            <span>📅</span>
                            <span id="solar-date-btn-text">Pick Date</span>
                        </button>
                    </div>
                    <!-- Date Picker Popover inside Section 3 (hidden by default) -->
                    <div id="solar-date-popover" class="hidden flex flex-col gap-2 pt-1 border-t border-slate-700/80 mt-1">
                        <div class="flex items-center justify-between">
                            <span class="text-[11px] font-bold text-slate-400">Selected Date:</span>
                            <div class="flex items-center gap-1.5">
                                <span id="solar-date-label" class="text-amber-300 font-extrabold text-xs">Oct 20, 2026</span>
                                <button id="solar-date-close-btn" type="button" class="text-slate-400 hover:text-white font-black text-xs px-1.5 py-0.5 rounded squish-btn" title="Hide Date Picker">✕</button>
                            </div>
                        </div>
                        <div class="flex items-center gap-2">
                            <input type="date" id="solar-date-input" min="1800-01-01" max="2050-12-31" class="flex-1 bg-slate-900 text-white text-xs sm:text-sm font-bold px-3 py-2 rounded-xl border border-indigo-400/50 focus:outline-none cursor-pointer min-h-[40px]">
                            <button id="solar-today-btn" type="button" class="bg-indigo-600 hover:bg-indigo-500 text-white font-black text-xs px-3.5 py-2 rounded-xl shadow-sm squish-btn min-h-[40px]">Today</button>
                        </div>
                    </div>
                </div>
            </div>

            <div id="solar-header-row" class="flex flex-wrap items-center justify-center gap-2 z-20 mb-0.5">
                <span id="solar-order-badge" class="bg-indigo-900/90 border border-indigo-400/50 text-indigo-100 text-xs sm:text-sm font-black px-3 py-0.5 rounded-full">
                    ⭐ Center of the Solar System
                </span>
                <button id="solar-action-btn" class="bg-amber-400 text-slate-900 font-black px-3.5 py-1 rounded-full text-xs sm:text-sm shadow-md squish-btn flex items-center gap-1">
                    <span>🔊</span><span id="solar-action-label">Fun Fact!</span>
                </button>
            </div>

            <!-- Stage Row (Arrows removed to maximize celestial visuals across all devices) -->
            <div id="solar-stage-row" class="flex items-center justify-center w-full z-10">
                <div id="solar-stage-box" class="flex items-center justify-center relative">
                    <div id="solar-photo-container" class="w-full h-full flex flex-col items-center justify-center relative cursor-pointer squish-btn">
                        <div id="solar-svg-holder" class="w-full h-full rounded-3xl overflow-hidden border-4 border-indigo-300/40 shadow-xl bg-black flex items-center justify-center p-0" style="background-color: #000000;"></div>
                        <span id="solar-photo-credit" class="hidden absolute bottom-2 left-1/2 -translate-x-1/2 z-10 text-[10px] font-extrabold uppercase tracking-wider text-indigo-100 bg-slate-950/85 backdrop-blur-sm px-2.5 py-0.5 rounded-full border border-indigo-400/40 whitespace-nowrap pointer-events-none">
                            🔭 Space Telescope View
                        </span>
                    </div>

                    <div id="solar-canvas-container" class="hidden w-full h-full flex items-center justify-center cursor-grab active:cursor-grabbing"></div>
                </div>
            </div>

            <h1 id="solar-title" class="text-xl sm:text-2xl font-black text-white tracking-tight mt-0.5 leading-tight flex-shrink-0 text-center">The Sun</h1>
            <div id="solar-fact" class="mt-0.5 fact-badge px-3 py-1 rounded-2xl font-extrabold text-xs sm:text-sm text-center max-w-lg shadow-md cursor-pointer squish-btn flex-shrink-0 leading-snug">
                Our giant, glowing star! It keeps Earth warm and bright!
            </div>
        </div>

        <!-- Single-Row Horizontal Scrollable Tray (Upgrade 2) -->
        <div id="solar-controls-dock" class="controls-dock" style="background: #0f172a; border-top-color: #334155;">
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

                    <!-- iOS Silent Mode Bypass Active Badge -->
                    <div class="flex items-center gap-2 p-2 rounded-xl bg-indigo-50 border border-indigo-200 text-indigo-900 text-xs font-extrabold">
                        <span>🔔</span>
                        <span>iOS Silent Mode Bypass: Active (Sound effects & Gemini Voice play even if iPhone silent switch is on)</span>
                    </div>

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

                    <!-- Drag & Spin Speed (Upgrade 3) -->
                    <div class="flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 border border-slate-200 gap-2">
                        <div>
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🖐️</span><span>Drag & Spin Speed</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Press & hold (long-press) to drag items with 1 finger, or spin 3D</div>
                        </div>
                        <select id="opt-drag-speed" class="px-2.5 py-1.5 rounded-xl border-2 border-slate-300 font-bold text-xs bg-white text-slate-800 focus:border-indigo-500 focus:outline-none flex-shrink-0">
                            <option value="slow">🐢 Slow (0.55x)</option>
                            <option value="normal">🖐️ Normal (1.0x)</option>
                            <option value="fast">⚡ Fast (1.75x)</option>
                        </select>
                    </div>

                    <!-- 5. Counting Range -->
                    <div class="flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 border border-slate-200 gap-2">
                        <div>
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔢</span><span>Counting Range</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Tap &amp; Count, Number Blocks, and Quiz counting pool</div>
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

                    <!-- 10. Minimize Home Screen Title Banner -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🏠</span><span>Minimize Home Screen Title Banner</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Hide the top title banner to maximize card space</div>
                        </div>
                        <input id="opt-minimize-header" type="checkbox">
                        <div class="toggle-slider"></div>
                    </label>

                    <!-- 11. Show NASA Image Source Credits (Item 4) -->
                    <label class="toggle-switch flex items-center justify-between p-2.5 rounded-2xl bg-slate-50 hover:bg-slate-100 border border-slate-200 cursor-pointer">
                        <div class="pr-2">
                            <div class="text-xs font-black text-slate-800 flex items-center gap-1.5">
                                <span>🔭</span><span>Show NASA Image Source Credits</span>
                            </div>
                            <div class="text-[11px] font-bold text-slate-500 leading-tight">Display telescope & mission source badge on Solar System photos</div>
                        </div>
                        <input id="opt-solar-credits" type="checkbox">
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

                <!-- Pre-Cache Speed / API Tier Selector (Upgrade 1) -->
                <div class="flex flex-col gap-1">
                    <label class="text-xs font-black uppercase tracking-wider text-slate-700">Pre-Cache Speed / API Tier</label>
                    <select id="precache-tier-select" class="w-full px-3 py-2 rounded-xl border-2 border-slate-300 font-bold text-xs sm:text-sm bg-slate-50 focus:border-indigo-500 focus:outline-none">
                        <option value="tier2_turbo">🚀 Tier 2 Turbo (~90 RPM • 3x Parallel — Default)</option>
                        <option value="tier2_max">⚡ Tier 2 Max (~180 RPM • 5x Parallel)</option>
                        <option value="tier1_safe">🐢 Tier 1 Safe (~8 RPM • 1x Serial)</option>
                    </select>
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

                <div id="precache-progress-box" class="hidden flex flex-col gap-1.5 bg-amber-50 border border-amber-200 rounded-xl p-3 text-xs text-amber-900 font-bold">
                    <div class="flex justify-between items-center">
                        <span id="precache-progress-text">Pre-caching audio...</span>
                        <span id="precache-progress-num">0%</span>
                    </div>
                    <div class="w-full bg-amber-200 rounded-full h-2.5 overflow-hidden">
                        <div id="precache-progress-bar" class="bg-amber-600 h-full w-0 transition-all duration-150"></div>
                    </div>
                    <div class="flex items-center justify-between pt-1">
                        <span id="precache-tier-sub" class="text-[10px] text-amber-800 font-medium">Tier 2 Turbo (~90 RPM • 3x Parallel) • Runs in background</span>
                        <div class="flex items-center gap-1.5">
                            <button id="precache-modal-pause-btn" type="button" class="px-2.5 py-1 bg-amber-200 hover:bg-amber-300 text-amber-900 rounded-lg text-[11px] font-black squish-btn">⏸️ Pause</button>
                            <button id="precache-modal-cancel-btn" type="button" class="px-2.5 py-1 bg-slate-200 hover:bg-slate-300 text-slate-700 rounded-lg text-[11px] font-black squish-btn">Cancel</button>
                        </div>
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

const runtimeVoiceConfig = {
    apiKey: "",
    model: "",
    voice: ""
};

const safeGetStorage = (k) => {
    try { return localStorage.getItem(k) || ""; } catch (e) { return ""; }
};

const safeSetStorage = (k, v) => {
    try {
        if (v === null || v === undefined || v === "") localStorage.removeItem(k);
        else localStorage.setItem(k, v);
    } catch (e) {}
};

const getApiKey = () => {
    if (runtimeVoiceConfig.apiKey) return runtimeVoiceConfig.apiKey;
    const domInp = typeof document !== 'undefined' ? document.getElementById('gemini-api-key-input') : null;
    const domVal = domInp && domInp.value ? domInp.value.trim() : "";
    if (domVal && !domVal.includes('●●●●●●●●')) {
        runtimeVoiceConfig.apiKey = domVal;
        return domVal;
    }
    return safeGetStorage('tlh_isolated_v3_api_key') ||
           safeGetStorage('toddler_gemini_api_key') ||
           apiKey || "";
};

const getTtsModel = () => {
    if (runtimeVoiceConfig.model) return runtimeVoiceConfig.model;
    const domSel = typeof document !== 'undefined' ? document.getElementById('gemini-tts-model-select') : null;
    if (domSel && domSel.value) return domSel.value;
    return safeGetStorage('tlh_isolated_v3_tts_model') ||
           safeGetStorage('toddler_gemini_tts_model') ||
           'gemini-3.8-flash-tts';
};

const getTtsVoice = () => {
    if (runtimeVoiceConfig.voice) return runtimeVoiceConfig.voice;
    const domSel = typeof document !== 'undefined' ? document.getElementById('gemini-tts-voice-select') : null;
    if (domSel && domSel.value) return domSel.value;
    return safeGetStorage('tlh_isolated_v3_tts_voice') ||
           safeGetStorage('toddler_gemini_tts_voice') ||
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
    async getAllKeys() {
        const db = await this.init();
        if (!db) return [];
        return new Promise((resolve) => {
            try {
                const tx = db.transaction('audio_cache', 'readonly');
                const store = tx.objectStore('audio_cache');
                const req = store.getAllKeys();
                req.onsuccess = () => resolve(req.result || []);
                req.onerror = () => resolve([]);
            } catch (err) {
                resolve([]);
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
    decodedCache: new Map(),
    inFlight: new Map(),
    knownDbKeys: new Set(),
    activeSource: null,
    activeAudioEl: null,
    workingStrategy: safeGetStorage('tlh_isolated_v3_working_strat') || null,
    playReqId: 0,
    warmUpTimer: null,
    cooldownUntil: (() => {
        try {
            const cd = sessionStorage.getItem('tlh_tts_cooldown');
            return cd ? parseInt(cd, 10) : 0;
        } catch (e) { return 0; }
    })(),

    hasCached(cacheKey) {
        return this.memCache.has(cacheKey) ||
               this.decodedCache.has(cacheKey) ||
               this.knownDbKeys.has(cacheKey);
    },

    setCooldown(ms = 60000) {
        this.cooldownUntil = Date.now() + ms;
        try {
            sessionStorage.setItem('tlh_tts_cooldown', String(this.cooldownUntil));
        } catch (e) {}
    },

    isCoolingDown() {
        return Date.now() < (this.cooldownUntil || 0);
    },

    stop() {
        this.playReqId++;
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
            this.knownDbKeys.add(cacheKey);
            this.memCache.set(cacheKey, dbCached);
            if (soundFX.ctx && !this.decodedCache.has(cacheKey)) {
                soundFX.ctx.decodeAudioData(dbCached.slice(0))
                    .then(ab => this.decodedCache.set(cacheKey, ab))
                    .catch(() => {});
            }
            return dbCached;
        }

        // 3. De-duplicate identical in-flight network requests
        if (this.inFlight.has(cacheKey)) {
            return this.inFlight.get(cacheKey);
        }

        const fetchPromise = (async () => {
            // Multi-schema fallback chain for Gemini TTS (strictly verbatim text!)
            const strategies = [
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
                },
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
                const ctrl = new AbortController();
                const timeoutId = setTimeout(() => {
                    try { ctrl.abort(); } catch (e) {}
                }, 9000);

                try {
                    const url = `https://generativelanguage.googleapis.com/v1beta/models/${strat.model}:generateContent?key=${encodeURIComponent(key)}`;
                    const resp = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(strat.body),
                        signal: ctrl.signal
                    });
                    clearTimeout(timeoutId);

                    if (!resp.ok) {
                        const errData = await resp.json().catch(() => ({}));
                        const errMsg = errData?.error?.message || `HTTP ${resp.status}`;
                        if (resp.status === 429 || errMsg.includes('RESOURCE_EXHAUSTED')) {
                            const tierCooldown = (safeGetStorage('tlh_precache_tier') || 'tier2_turbo').startsWith('tier2') ? 25000 : 60000;
                            this.setCooldown(tierCooldown);
                            throw new Error("HTTP 429: Rate limit reached (RESOURCE_EXHAUSTED)");
                        }
                        throw new Error(errMsg);
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
                    try {
                        localStorage.setItem('tlh_isolated_v3_working_strat', strat.id);
                    } catch (e) {}

                    // Cache in memory and IndexedDB
                    this.memCache.set(cacheKey, wavBuffer);
                    await ttsDB.set(cacheKey, wavBuffer);
                    this.knownDbKeys.add(cacheKey);

                    // Pre-decode into AudioBuffer
                    if (soundFX.ctx) {
                        soundFX.ctx.decodeAudioData(wavBuffer.slice(0))
                            .then(ab => this.decodedCache.set(cacheKey, ab))
                            .catch(() => {});
                    }

                    return wavBuffer;
                } catch (err) {
                    clearTimeout(timeoutId);
                    lastErr = err;
                    if (err.message && (err.message.includes('429') || err.message.includes('RESOURCE_EXHAUSTED'))) {
                        const tierCooldown = (safeGetStorage('tlh_precache_tier') || 'tier2_turbo').startsWith('tier2') ? 25000 : 60000;
                        this.setCooldown(tierCooldown);
                        break; // Stop trying other strategies on 429
                    }
                }
            }

            throw lastErr || new Error("All Gemini TTS strategies failed");
        })();

        this.inFlight.set(cacheKey, fetchPromise);
        try {
            return await fetchPromise;
        } finally {
            this.inFlight.delete(cacheKey);
        }
    },

    async play(text, model = getTtsModel(), voice = getTtsVoice(), customKey = null, onPlayStart = null, onPlayEnd = null) {
        this.stop();
        const myReqId = ++this.playReqId;

        // CRITICAL FOR iOS SAFARI: synchronously initialize AudioContext and resume inside user gesture token BEFORE any await
        soundFX.init();
        if (soundFX.ctx && soundFX.ctx.state !== 'running') {
            try { soundFX.ctx.resume(); } catch (e) {}
        }

        // Cancel any active speechSynthesis so Device Voice and Gemini Voice never clash
        if ('speechSynthesis' in window && (window.speechSynthesis.speaking || window.speechSynthesis.pending)) {
            try { window.speechSynthesis.cancel(); } catch (e) {}
        }

        const cleanText = cleanSpokenText(text);
        if (!cleanText) return;

        if (typeof app !== 'undefined' && app.setSpeakingUI) {
            app.setSpeakingUI(true);
        }

        const cacheKey = `${model}:${voice}:${cleanText}`;

        const playAudioBuffer = async (audioBuf) => {
            if (myReqId !== this.playReqId) return;
            if (soundFX.ctx.state !== 'running') {
                try { await soundFX.ctx.resume(); } catch (e) {}
            }
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
                if (myReqId === this.playReqId) {
                    if (typeof onPlayEnd === 'function') {
                        try { onPlayEnd(); } catch (e) {}
                    }
                }
            };

            this.activeSource = src;
            const rateVal = (typeof app !== 'undefined' && app.getSpeechRateValue) ? app.getSpeechRateValue() : 1.0;
            const effectiveDur = audioBuf.duration / (rateVal || 1.0);
            if (typeof onPlayStart === 'function') {
                try { onPlayStart(effectiveDur); } catch (e) {}
            }
            src.start(0);
        };

        let wavBuf = null;
        try {
            // Fast-path: Pre-decoded AudioBuffer already available
            if (soundFX.ctx && this.decodedCache.has(cacheKey)) {
                await playAudioBuffer(this.decodedCache.get(cacheKey));
                return;
            }

            wavBuf = await this.fetchAudio(cleanText, model, voice, customKey);
            if (!wavBuf || myReqId !== this.playReqId) {
                if (myReqId === this.playReqId && typeof app !== 'undefined' && app.setSpeakingUI) {
                    app.setSpeakingUI(false);
                }
                return;
            }

            if (!soundFX.ctx) {
                throw new Error("No WebAudio context");
            }

            if (soundFX.ctx.state !== 'running') {
                try { await soundFX.ctx.resume(); } catch (e) {}
            }

            let audioBuf = this.decodedCache.get(cacheKey);
            if (!audioBuf) {
                audioBuf = await soundFX.ctx.decodeAudioData(wavBuf.slice(0));
                this.decodedCache.set(cacheKey, audioBuf);
            }
            await playAudioBuffer(audioBuf);
        } catch (decodeErr) {
            if (myReqId !== this.playReqId) return;
            if (wavBuf) {
                // Fallback to HTMLAudioElement with WAV Blob
                try {
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
                        if (myReqId === this.playReqId) {
                            if (typeof onPlayEnd === 'function') {
                                try { onPlayEnd(); } catch (e) {}
                            }
                        }
                    };
                    audio.onerror = () => {
                        URL.revokeObjectURL(blobUrl);
                        if (this.activeAudioEl === audio) {
                            this.activeAudioEl = null;
                            if (typeof app !== 'undefined' && app.setSpeakingUI) app.setSpeakingUI(false);
                        }
                    };
                    if (typeof onPlayStart === 'function') {
                        try { onPlayStart(); } catch (e) {}
                    }
                    await audio.play();
                    return;
                } catch (audioElErr) {}
            }
            if (myReqId === this.playReqId && typeof app !== 'undefined' && app.setSpeakingUI) {
                app.setSpeakingUI(false);
            }
            if (decodeErr.name === 'AbortError') return;
            throw decodeErr;
        }
    },

    warmUpView(viewName) {
        if (this.warmUpTimer) {
            clearTimeout(this.warmUpTimer);
            this.warmUpTimer = null;
        }
        if (typeof precacheManager !== 'undefined' && precacheManager.state === 'running') return;
        const key = getApiKey();
        if (!key || this.isCoolingDown()) return;

        const tier = safeGetStorage('tlh_precache_tier') || 'tier2_turbo';
        const delayMs = tier.startsWith('tier2') ? 600 : 3500;

        const phrases = [];
        if (typeof GAME_OPEN_TITLES !== 'undefined' && GAME_OPEN_TITLES[viewName]) {
            phrases.push(GAME_OPEN_TITLES[viewName]);
        }
        if (typeof GAMES !== 'undefined') {
            if (viewName === 'letters' && GAMES.phonics) {
                GAMES.phonics.slice(0, 5).forEach(p => phrases.push(`${p.letter}! ${p.cue} ${p.soundSpell}, ${p.words[0].w}!`));
            } else if (viewName === 'numbers' && GAMES.numbers) {
                GAMES.numbers.slice(0, 5).forEach(n => phrases.push(`${n.word}! Tap to count to ${n.num}!`));
            } else if (viewName === 'shapes' && GAMES.shapes) {
                GAMES.shapes.slice(0, 5).forEach(s => phrases.push(`${s.id}!`));
            } else if (viewName === 'shapes3d' && GAMES.shapes3d) {
                GAMES.shapes3d.slice(0, 5).forEach(s => phrases.push(`${s.id}! ${s.real}`));
            } else if (viewName === 'colors' && GAMES.colors) {
                GAMES.colors.slice(0, 5).forEach(c => phrases.push(c.id));
            } else if (viewName === 'animals' && GAMES.animals) {
                GAMES.animals.slice(0, 5).forEach(a => phrases.push(a.id));
            } else if (viewName === 'fruits' && GAMES.fruits) {
                GAMES.fruits.slice(0, 5).forEach(f => phrases.push(`${f.id}! ${f.desc}`));
            } else if (viewName === 'things' && GAMES.things) {
                GAMES.things.slice(0, 5).forEach(t => phrases.push(t.id));
            } else if (viewName === 'opposites' && GAMES.opposites) {
                GAMES.opposites.slice(0, 5).forEach(p => phrases.push(`${p.a.label}, and ${p.b.label}!`));
            } else if (viewName === 'solar' && GAMES.solar) {
                GAMES.solar.slice(0, 4).forEach(s => phrases.push(s.speech));
            } else if (viewName === 'blocks' && window.NumberBlocks && window.NumberBlocks.Data && window.NumberBlocks.Data.getWarmupPhrases) {
                (window.NumberBlocks.Data.getWarmupPhrases() || []).slice(0, 6).forEach(p => phrases.push(p));
            } else if (viewName === 'quiz' && typeof quizGame !== 'undefined' && quizGame.getPool) {
                quizGame.getPool().slice(0, 8).forEach(q => phrases.push(q.prompt));
            }
        }

        const model = getTtsModel();
        const voice = getTtsVoice();
        let idx = 0;

        const warmStep = async () => {
            if (app.currentView !== viewName || (typeof precacheManager !== 'undefined' && precacheManager.state === 'running')) return;
            if (idx >= phrases.length) return;
            const phrase = cleanSpokenText(phrases[idx++]);
            const cacheKey = `${model}:${voice}:${phrase}`;
            if (!this.hasCached(cacheKey) && !this.knownDbKeys.has(cacheKey)) {
                try {
                    await this.fetchAudio(phrase, model, voice, key);
                } catch (e) {}
            }
            this.warmUpTimer = setTimeout(warmStep, delayMs);
        };

        this.warmUpTimer = setTimeout(warmStep, delayMs);
    }
};

// High-Speed Multi-Tier Concurrent Background Pre-Cache Engine (Upgrade 1)
const precacheManager = {
    state: 'idle', // 'idle' | 'running' | 'paused' | 'cooling' | 'completed'
    allWords: [],
    uncachedQueue: [],
    cachedCount: 0,
    totalCount: 0,
    activeWorkers: 0,
    currentConcurrency: 3,
    backoffCount: 0,
    yieldUntil: 0,
    workerTimers: [],

    TIER_CONFIGS: {
        tier2_turbo: { id: 'tier2_turbo', label: 'Tier 2 Turbo (~90 RPM • 3x Parallel)', concurrency: 3, intervalMs: 1800, cooldownMs: 25000 },
        tier2_max: { id: 'tier2_max', label: 'Tier 2 Max (~180 RPM • 5x Parallel)', concurrency: 5, intervalMs: 1200, cooldownMs: 25000 },
        tier1_safe: { id: 'tier1_safe', label: 'Tier 1 Safe (~8 RPM • 1x Serial)', concurrency: 1, intervalMs: 7200, cooldownMs: 60000 }
    },

    getTierConfig() {
        const tierKey = safeGetStorage('tlh_precache_tier') || 'tier2_turbo';
        return this.TIER_CONFIGS[tierKey] || this.TIER_CONFIGS.tier2_turbo;
    },

    getCoreWordPool() {
        const list = [];
        const seen = new Set();
        const add = (txt) => {
            const c = cleanSpokenText(txt);
            if (c && !seen.has(c)) {
                seen.add(c);
                list.push(c);
            }
        };

        // Priority 1: Game opening announcements (both standalone and combined with default starting items)
        if (typeof GAME_OPEN_TITLES !== 'undefined') {
            Object.values(GAME_OPEN_TITLES).forEach(title => add(title));
        }
        add('ABC Phonics! A! A says ah! ah, Apple!');
        add('ABC Phonics! A! Apple!');
        add('Numbers and Counting! One! Tap to count to 1!');
        add('2D Shapes! Circle!');
        add('3D Shapes! Cube! 6 flat square faces — like a box or dice!');
        add('Colors and Paint! Red');
        add('Animal Friends! Lion');
        add('Yummy Foods! Strawberry! Sweet Red Berry!');
        add('Yummy Foods! Apple! Crunchy Red Apple!');
        add('Yummy Foods! Apple! Crispy, sweet red apple!');
        add('Vehicles and Things! Fire Truck');
        add('Opposites! Big, and Small!');
        if (typeof GAMES !== 'undefined' && GAMES.solar && GAMES.solar[0]) {
            add('Solar System! ' + GAMES.solar[0].speech);
        }

        if (typeof GAMES !== 'undefined') {
            // Priority 2: Core Game Selections across all 11 games
            // 1. Phonics / Letters
            if (GAMES.phonics) {
                GAMES.phonics.forEach(item => {
                    add(`${item.letter}! ${item.cue} ${item.soundSpell}, ${item.words[0].w}!`);
                    add(`${item.letter}! ${item.words[0].w}!`);
                    item.words.forEach(wObj => {
                        add(`${item.soundSpell}, ${item.soundSpell}, ${wObj.w}!`);
                        add(`${wObj.w}!`);
                    });
                    add(`Pop ${item.letter}! ${item.cue} ${item.words[0].w}!`);
                    add(`Yay! ${item.letter} says ${item.soundSpell}! ${item.words[0].w}!`);
                    add(`That is ${item.letter}. Find ${item.letter}!`);
                });
            }

            // 2. Numbers
            for (let i = 1; i <= 20; i++) {
                add(String(i));
            }
            if (GAMES.numbers) {
                GAMES.numbers.forEach(n => {
                    add(n.word);
                    add(`${n.word}! Tap to count to ${n.num}!`);
                    add(`${n.num}! Yay! ${n.word} ${n.item}!`);
                    add(n.item);
                });
            }

            // 3. 2D Shapes
            if (GAMES.shapes) {
                GAMES.shapes.forEach(s => {
                    add(`${s.id}!`);
                    add(s.id);
                });
            }

            // 4. 3D Shapes
            if (GAMES.shapes3d) {
                GAMES.shapes3d.forEach(s => {
                    add(`${s.id}! ${s.real}`);
                    add(s.id);
                    if (s.examples) {
                        s.examples.forEach(ex => {
                            if (ex.id !== 'pure') {
                                add(`${ex.label}! A 3D ${s.id}!`);
                                add(ex.label);
                            }
                        });
                    }
                });
            }

            // 5. Colors & Key Mixes
            if (GAMES.colors) {
                GAMES.colors.forEach(c => add(c.id));
            }
            const colorMixPairs = [
                ['Red', 'Yellow', 'Orange'],
                ['Blue', 'Yellow', 'Green'],
                ['Blue', 'Red', 'Purple'],
                ['Red', 'White', 'Pink'],
                ['Blue', 'White', 'Sky Blue'],
                ['White', 'Yellow', 'Cream Yellow'],
                ['Green', 'White', 'Mint Green'],
                ['Orange', 'White', 'Peach'],
                ['Purple', 'White', 'Lavender'],
                ['Pink', 'White', 'Light Pink'],
                ['Brown', 'White', 'Tan Khaki'],
                ['Black', 'White', 'Gray'],
                ['Black', 'Red', 'Burgundy Dark Red'],
                ['Black', 'Blue', 'Midnight Navy'],
                ['Black', 'Yellow', 'Olive Green'],
                ['Black', 'Green', 'Forest Green'],
                ['Black', 'Orange', 'Rust Brown'],
                ['Black', 'Purple', 'Deep Violet'],
                ['Black', 'Pink', 'Dusty Plum'],
                ['Black', 'Brown', 'Dark Chocolate'],
                ['Green', 'Red', 'Brown'],
                ['Blue', 'Orange', 'Warm Slate'],
                ['Purple', 'Yellow', 'Golden Bronze'],
                ['Green', 'Yellow', 'Lime Green'],
                ['Blue', 'Green', 'Teal Turquoise'],
                ['Orange', 'Red', 'Coral Red'],
                ['Pink', 'Purple', 'Magenta Rose'],
                ['Blue', 'Pink', 'Lilac Violet'],
                ['Brown', 'Orange', 'Caramel'],
                ['Brown', 'Red', 'Terracotta']
            ];
            colorMixPairs.forEach(([c1, c2, res]) => {
                add(`${c1} plus ${c2} makes ${res}!`);
                add(`${c2} plus ${c1} makes ${res}!`);
                add(res);
            });

            // 6. Animals
            if (GAMES.animals) {
                GAMES.animals.forEach(a => {
                    add(a.id);
                    add(a.sound);
                    add(a.speech);
                });
            }

            // 7. Yummy Foods
            if (GAMES.fruits) {
                GAMES.fruits.forEach(f => {
                    add(`${f.id}! ${f.desc}`);
                    add(f.id);
                    add(`All gone! Yummy ${f.id}! Delicious!`);
                });
                ['Crunch! Delicious!', 'Yum yum!', 'So tasty!', 'One more bite!'].forEach(ch => add(ch));
            }

            // 8. Vehicles and Things
            if (GAMES.things) {
                GAMES.things.forEach(t => {
                    add(t.id);
                    add(t.sound);
                    add(t.speech);
                });
            }

            // 9. Opposites
            if (GAMES.opposites) {
                GAMES.opposites.forEach(pair => {
                    add(`${pair.a.label}, and ${pair.b.label}!`);
                    add(pair.a.label);
                    add(pair.b.label);
                });
            }

            // 10. Solar System
            if (GAMES.solar) {
                GAMES.solar.forEach(s => {
                    add(s.id);
                    add(s.speech);
                });
                add('Zoom! Super fast planet orbits!');
                add("Back to today's planet positions!");
            }
        }

        // 12. Number Blocks
        if (window.NumberBlocks && window.NumberBlocks.Data && window.NumberBlocks.Data.getWarmupPhrases) {
            (window.NumberBlocks.Data.getWarmupPhrases() || []).forEach(p => add(p));
        }

        // Priority 3: Quiz Prompts, General Praises & UI Phrases
        if (typeof quizGame !== 'undefined' && quizGame.getPool) {
            const prevCat = quizGame.category;
            quizGame.category = 'all';
            quizGame.getPool().forEach(q => {
                add(q.prompt);
                add(`Look and Find! ${q.prompt}`);
                add(`You found it! ${q.label}!`);
                add(`Try to find ${q.label}!`);
            });
            quizGame.category = prevCat;
        }

        [
            'Great job!',
            'You found it!',
            'Yay!',
            'Try again!',
            "Options saved! Let's explore together!",
            'All core words are ready for instant play!'
        ].forEach(p => add(p));

        return list;
    },

    async start() {
        const key = getApiKey();
        if (!key) {
            alert("Please paste your Gemini API Key first to pre-cache Gemini natural voices!");
            return;
        }

        this.clearTimers();
        const cfg = this.getTierConfig();
        this.currentConcurrency = cfg.concurrency;
        this.backoffCount = 0;
        this.state = 'running';

        const model = getTtsModel();
        const voice = getTtsVoice();

        // 1. Pre-scan IndexedDB keys
        const dbKeys = await ttsDB.getAllKeys().catch(() => []);
        dbKeys.forEach(k => geminiTTS.knownDbKeys.add(k));

        // 2. Build full word pool and queue
        this.allWords = this.getCoreWordPool();
        this.totalCount = this.allWords.length;
        this.uncachedQueue = [];
        this.cachedCount = 0;

        for (const word of this.allWords) {
            const cacheKey = `${model}:${voice}:${word}`;
            if (geminiTTS.hasCached(cacheKey) || geminiTTS.knownDbKeys.has(cacheKey)) {
                this.cachedCount++;
            } else {
                this.uncachedQueue.push(word);
            }
        }

        if (this.uncachedQueue.length === 0) {
            this.state = 'completed';
            this.updateUI();
            if (typeof app !== 'undefined' && app.speak) {
                app.speak("All core words are ready for instant play!");
            }
            return;
        }

        this.updateUI();

        // 3. Launch concurrent workers
        this.activeWorkers = this.currentConcurrency;
        for (let w = 0; w < this.currentConcurrency; w++) {
            const t = setTimeout(() => this.runWorker(w), w * 450);
            this.workerTimers.push(t);
        }
    },

    clearTimers() {
        this.workerTimers.forEach(t => clearTimeout(t));
        this.workerTimers = [];
    },

    pause() {
        this.clearTimers();
        this.state = 'paused';
        this.updateUI();
    },

    resume() {
        if (this.state !== 'paused') return;
        this.state = 'running';
        this.updateUI();
        this.activeWorkers = this.currentConcurrency;
        for (let w = 0; w < this.currentConcurrency; w++) {
            const t = setTimeout(() => this.runWorker(w), w * 450);
            this.workerTimers.push(t);
        }
    },

    cancel() {
        this.clearTimers();
        this.state = 'idle';
        this.uncachedQueue = [];
        this.updateUI();
    },

    yieldForInteractive(extraMs = 8500) {
        this.yieldUntil = Math.max(this.yieldUntil, Date.now() + extraMs);
        if (this.state === 'running') {
            this.updateUI("Yielding to toddler speech tap...");
        }
    },

    async runWorker(workerId) {
        if (this.state !== 'running') return;
        if (workerId >= this.currentConcurrency) return;

        const now = Date.now();
        if (this.yieldUntil > now) {
            const waitMs = this.yieldUntil - now + 100;
            const t = setTimeout(() => this.runWorker(workerId), waitMs);
            this.workerTimers.push(t);
            return;
        }

        if (geminiTTS.isCoolingDown()) {
            const cdWait = Math.max(1000, (geminiTTS.cooldownUntil || 0) - now);
            this.state = 'cooling';
            this.updateUI(`Rate limit cooldown (${Math.ceil(cdWait / 1000)}s)...`);
            const t = setTimeout(() => {
                if (this.state === 'cooling') this.state = 'running';
                this.runWorker(workerId);
            }, cdWait);
            this.workerTimers.push(t);
            return;
        }

        if (this.uncachedQueue.length === 0) {
            this.activeWorkers--;
            if (this.activeWorkers <= 0) {
                this.state = 'completed';
                this.updateUI();
                if (typeof app !== 'undefined' && app.speak) {
                    app.speak("All core words are ready for instant play!");
                }
            }
            return;
        }

        const word = this.uncachedQueue.shift();
        const model = getTtsModel();
        const voice = getTtsVoice();
        const key = getApiKey();
        const cacheKey = `${model}:${voice}:${word}`;

        // Verify if cached while in queue
        if (geminiTTS.hasCached(cacheKey) || geminiTTS.knownDbKeys.has(cacheKey)) {
            this.cachedCount++;
            this.updateUI();
            const t = setTimeout(() => this.runWorker(workerId), 0);
            this.workerTimers.push(t);
            return;
        }

        const cfg = this.getTierConfig();
        this.updateUI(`Caching "${word}"...`);

        try {
            await geminiTTS.fetchAudio(word, model, voice, key);
            if (this.state !== 'running') {
                this.cachedCount++;
                this.updateUI();
                return;
            }
            this.cachedCount++;
            this.backoffCount = 0;
            this.updateUI();
            const t = setTimeout(() => this.runWorker(workerId), cfg.intervalMs);
            this.workerTimers.push(t);
        } catch (err) {
            const is429 = err.message && (err.message.includes('429') || err.message.includes('RESOURCE_EXHAUSTED'));
            if (is429) {
                // Return phrase to front of queue if not already present
                if (!this.uncachedQueue.includes(word)) {
                    this.uncachedQueue.unshift(word);
                }

                // If another parallel worker already triggered cooling, just return
                if (this.state === 'cooling') {
                    return;
                }

                this.backoffCount++;
                const isTier2 = cfg.id.startsWith('tier2');
                const waitMs = isTier2
                    ? (this.backoffCount === 1 ? 25000 : this.backoffCount === 2 ? 40000 : 60000)
                    : (this.backoffCount === 1 ? 60000 : this.backoffCount === 2 ? 90000 : 120000);

                geminiTTS.setCooldown(waitMs);
                this.state = 'cooling';

                // Automatically step down concurrency if on Tier 2
                if (this.currentConcurrency > 1) {
                    this.currentConcurrency--;
                }

                this.updateUI(`Rate limit reached — cooling down (${Math.ceil(waitMs / 1000)}s)...`);
                this.clearTimers();
                const t = setTimeout(() => {
                    if (this.state === 'cooling') this.state = 'running';
                    this.activeWorkers = this.currentConcurrency;
                    for (let w = 0; w < this.currentConcurrency; w++) {
                        const wt = setTimeout(() => this.runWorker(w), w * 450);
                        this.workerTimers.push(wt);
                    }
                }, waitMs);
                this.workerTimers.push(t);
            } else {
                // Non-429 error: skip phrase so queue doesn't stall
                if (this.state !== 'running') return;
                this.cachedCount++;
                this.updateUI();
                const t = setTimeout(() => this.runWorker(workerId), cfg.intervalMs);
                this.workerTimers.push(t);
            }
        }
    },

    updateUI(statusOverride = null) {
        const total = this.totalCount || (this.allWords && this.allWords.length) || this.getCoreWordPool().length;
        const current = this.cachedCount;
        const pct = total > 0 ? Math.round((current / total) * 100) : 0;
        const cfg = this.getTierConfig();

        // Modal Elements
        const precacheLabel = document.getElementById('voice-precache-label');
        const progressBox = document.getElementById('precache-progress-box');
        const progressBar = document.getElementById('precache-progress-bar');
        const progressNum = document.getElementById('precache-progress-num');
        const progressText = document.getElementById('precache-progress-text');
        const pauseModalBtn = document.getElementById('precache-modal-pause-btn');
        const tierSub = document.getElementById('precache-tier-sub');

        // Floating Pill Elements
        const pill = document.getElementById('precache-floating-pill');
        const pillTitle = document.getElementById('precache-pill-title');
        const pillSub = document.getElementById('precache-pill-sub');
        const pillPauseBtn = document.getElementById('precache-pill-pause-btn');

        if (progressBar) progressBar.style.width = `${pct}%`;
        if (progressNum) progressNum.textContent = `${pct}%`;
        if (tierSub) tierSub.textContent = `${cfg.label} • Runs in background`;

        if (this.state === 'running' || this.state === 'cooling') {
            if (progressBox) progressBox.classList.remove('hidden');
            if (pill) pill.classList.remove('hidden');
            if (precacheLabel) precacheLabel.textContent = `Caching (${pct}%)`;
            if (pauseModalBtn) pauseModalBtn.textContent = '⏸️ Pause';
            if (pillPauseBtn) pillPauseBtn.textContent = '⏸️';

            const defaultText = this.state === 'cooling' ? 'Cooling down...' : `Caching (${current}/${total})...`;
            const displayStatus = statusOverride || defaultText;
            if (progressText) progressText.textContent = displayStatus;
            if (pillTitle) pillTitle.textContent = `Caching: ${current}/${total} (${pct}%)`;
            if (pillSub) pillSub.textContent = statusOverride || cfg.label;
        } else if (this.state === 'paused') {
            if (progressBox) progressBox.classList.remove('hidden');
            if (pill) pill.classList.remove('hidden');
            if (precacheLabel) precacheLabel.textContent = 'Paused';
            if (pauseModalBtn) pauseModalBtn.textContent = '▶️ Resume';
            if (pillPauseBtn) pillPauseBtn.textContent = '▶️';
            if (progressText) progressText.textContent = `Paused at ${current}/${total} (${pct}%)`;
            if (pillTitle) pillTitle.textContent = `Paused (${pct}%)`;
            if (pillSub) pillSub.textContent = 'Tap to Resume';
        } else if (this.state === 'completed') {
            if (precacheLabel) precacheLabel.textContent = '⚡ Core Words Cached!';
            if (progressText) progressText.textContent = 'All core words successfully cached!';
            if (pillTitle) pillTitle.textContent = '✅ All Words Cached!';
            if (pillSub) pillSub.textContent = '100% Ready for Offline Play';
            setTimeout(() => {
                if (progressBox) progressBox.classList.add('hidden');
                if (pill) pill.classList.add('hidden');
            }, 4000);
        } else {
            // Idle
            if (precacheLabel) precacheLabel.textContent = 'Pre-cache Core Words';
            if (progressBox) progressBox.classList.add('hidden');
            if (pill) pill.classList.add('hidden');
            if (pillSub) pillSub.textContent = cfg.label;
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

// Real recorded vehicle & object sounds (Item 2b) & realistic crunch sounds (Item 6)
const REAL_THING_SFX = {
    "Fire Truck": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABBJtb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAADEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACpHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAADEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAkBtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAADEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB9m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABunN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAC3+AAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAADEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAUAAAABAAAAAQAAANhzdHN6AAAAAAAAAAAAAAAxAAAABAAAAGkAAAI/AAAA+AAAAPUAAAD2AAAA8QAAAPEAAADzAAAA9QAAAY0AAAGnAAABBwAAANQAAAC+AAAAwAAAAL0AAADKAAAA2wAAAOcAAADmAAAA2gAAANYAAADTAAAA1AAAANcAAADRAAAAwwAAALkAAADAAAAAzQAAAREAAAD4AAAA/AAAAPsAAAD2AAAA7QAAAPYAAADwAAAA9wAAAQYAAAEEAAABBgAAARcAAAD1AAAA/AAAAQEAAAEAAAABCgAAACRzdGNvAAAAAAAAAAUAABAAAAAcjQAAJpgAADETAAA89gAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMDQwIDAwMDAwMDAwMDAwMEJCODAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvKZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Police Car": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA/5tb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAAC0AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACkHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAAC0AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAixtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAAC0AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB4m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABpnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAADHCAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAC0AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAQAAAAJAAAAAQAAAMhzdHN6AAAAAAAAAAAAAAAtAAAABAAAAQoAAADAAAAA4AAAAOkAAADiAAAA5wAAAN8AAADqAAAA7AAAAOwAAADrAAAA8wAAAPMAAAESAAABFQAAARUAAAEbAAABFAAAARQAAAEVAAABGgAAAQsAAAEWAAABEAAAARgAAAEdAAABFAAAARgAAAERAAABHQAAARwAAAEfAAABGgAAARUAAAEWAAABCwAAARgAAAEMAAAA7gAAACMAAAANAAAACgAAAAQAAAAEAAAAIHN0Y28AAAAAAAAABAAAEAAAABnsAAAmoQAAM8AAAAD6dWR0YQAAAPJtZXRhAAAAAAAAACJoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAADEaWxzdAAAALwtLS0tAAAAHG1lYW4AAAAAY29tLmFwcGxlLmlUdW5lcwAAABRuYW1lAAAAAGlUdW5TTVBCAAAAhGRhdGEAAAABAAAAACAwMDAwMDAwMCAwMDAwMDg0MCAwMDAwMDMwMCAwMDAwMDAwMDAwMDBBOEMwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwAAAL3mZyZWUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Train": "data:audio/mp4;base64,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AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Rocket Ship": "data:audio/mp4;base64,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AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Airplane": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABBJtb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAADEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACpHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAADEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAkBtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAADEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB9m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABunN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAADASAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAADEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAUAAAABAAAAAQAAANhzdHN6AAAAAAAAAAAAAAAxAAAABAAAAlUAAAKdAAAA4gAAAOkAAADpAAAA9QAAAOgAAADhAAAA8QAAAOYAAAD0AAAA6AAAAO8AAADjAAAA6wAAAOoAAADhAAAA3QAAAOcAAADtAAAA2wAAAOsAAADzAAAA6QAAAPUAAADgAAAA6QAAAPUAAADoAAAA8AAAAOUAAADwAAAA7wAAAPEAAADvAAAA5AAAAOEAAADjAAAA5gAAARAAAADiAAAA3gAAAPkAAADgAAAA6AAAAOgAAADxAAAA2gAAACRzdGNvAAAAAAAAAAUAABAAAAAdMwAAKA0AADMlAAA+HQAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMDQwIDAwMDAwMDAwMDAwMEJCODAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvKZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Helicopter": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA8ptb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAACEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACXHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAACEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAfhtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAACEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABrm1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABcnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAC8iAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAACEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAMAAAAJAAAAAQAAAJhzdHN6AAAAAAAAAAAAAAAhAAAABAAAAAsAAAFSAAAChQAAAeAAAAF2AAABRwAAAQ4AAADqAAAA7wAAAOEAAADgAAAA3AAAAOYAAADkAAAA3wAAAOMAAADbAAAA4wAAAN4AAADaAAAA2AAAANYAAADeAAAA5gAAANMAAADaAAAA1gAAAOYAAADWAAAA5wAAAPAAAAA1AAAAHHN0Y28AAAAAAAAAAwAAEAAAAB0rAAAnlQAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMUUwIDAwMDAwMDAwMDAwMDc5RTAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAwSZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Tractor": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABBJtb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAADEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACpHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAADEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAkBtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAADEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB9m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABunN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAC+UAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAADEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAUAAAABAAAAAQAAANhzdHN6AAAAAAAAAAAAAAAxAAAABAAAAAwAAACdAAAA8QAAALsAAAEdAAABEwAAAQsAAAEJAAABEgAAAQ0AAAEQAAAA+wAAAQIAAAD/AAABBQAAAQwAAAEEAAABCQAAAQsAAAD3AAAA8gAAAPsAAAEQAAAA+wAAAQcAAAEhAAABGwAAAP8AAAD+AAABEQAAAPwAAAD+AAABAAAAARQAAAEKAAABEAAAAPsAAAD1AAAA9QAAAPQAAAEOAAABCAAAAQwAAAEQAAAA8gAAAQMAAAEGAAAA/wAAACRzdGNvAAAAAAAAAAUAABAAAAAZzAAAJeUAADJJAAA+XwAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMDQwIDAwMDAwMDAwMDAwMEJCODAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvKZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "School Bus": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA/5tb292AAAAbG12aGQAAAAA5v1+vOb9frwAAF3AAAC0AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACkHRyYWsAAABcdGtoZAAAAAfm/X685v1+vAAAAAEAAAAAAAC0AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAixtZGlhAAAAIG1kaGQAAAAA5v1+vOb9frwAAF3AAAC0AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB4m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABpnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAACrcAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAC0AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAQAAAAJAAAAAQAAAMhzdHN6AAAAAAAAAAAAAAAtAAAABAAAAMQAAACzAAABKgAAALgAAACXAAAAmQAAALsAAAEkAAAA+gAAAMUAAADfAAAA2AAAANkAAADlAAAA4wAAANUAAADhAAAA7gAAAOkAAADuAAAA9AAAAO0AAADwAAAA6AAAAPwAAAD2AAAA8QAAAPMAAAECAAAA8QAAAPUAAAD4AAAA6gAAAPcAAAECAAAA/wAAAPsAAAEEAAABCwAAAQcAAAECAAABBAAAAP8AAABKAAAAIHN0Y28AAAAAAAAABAAAEAAAABkKAAAjzwAAL1AAAAD6dWR0YQAAAPJtZXRhAAAAAAAAACJoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAADEaWxzdAAAALwtLS0tAAAAHG1lYW4AAAAAY29tLmFwcGxlLmlUdW5lcwAAABRuYW1lAAAAAGlUdW5TTVBCAAAAhGRhdGEAAAABAAAAACAwMDAwMDAwMCAwMDAwMDg0MCAwMDAwMDMwMCAwMDAwMDAwMDAwMDBBOEMwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwAAAL3mZyZWUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Sailboat": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABBJtb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAADEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACpHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAADEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAkBtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAADEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB9m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABunN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAC6mAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAADEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAUAAAABAAAAAQAAANhzdHN6AAAAAAAAAAAAAAAxAAAABAAAAP4AAAEbAAAA4gAAAOcAAADlAAAA8QAAAPIAAADtAAAA6gAAAPAAAADiAAAA6AAAAOYAAADqAAAA4QAAAN8AAADhAAABCgAAAQQAAAEQAAABAwAAAQcAAAELAAABBQAAAP4AAAEGAAABAQAAAQ4AAAEIAAABBAAAAQgAAAEGAAABBQAAAQEAAAD+AAABBAAAAP4AAAEGAAABAQAAAQcAAAECAAABDgAAAQQAAAECAAABBQAAAQgAAAD8AAAA8AAAACRzdGNvAAAAAAAAAAUAABAAAAAaVwAAJeMAADIZAAA+SAAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMDQwIDAwMDAwMDAwMDAwMEJCODAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvKZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Bicycle": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA5Jtb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAABQAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACJHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAABQAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAcBtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAABQAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABdm1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABOnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAABVmAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAABQAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAIAAAAIAAAAAQAAAGRzdHN6AAAAAAAAAAAAAAAUAAAABAAAAZoAAAG7AAABawAAAMwAAACbAAAAngAAAKUAAAFfAAABEgAAANQAAADrAAAA7QAAAO8AAAD0AAABAQAAANkAAADqAAAA6gAAAEcAAAAYc3RjbwAAAAAAAAACAAAQAAAAG54AAAD6dWR0YQAAAPJtZXRhAAAAAAAAACJoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAADEaWxzdAAAALwtLS0tAAAAHG1lYW4AAAAAY29tLmFwcGxlLmlUdW5lcwAAABRuYW1lAAAAAGlUdW5TTVBCAAAAhGRhdGEAAAABAAAAACAwMDAwMDAwMCAwMDAwMDg0MCAwMDAwMDE3MCAwMDAwMDAwMDAwMDA0NjUwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwAAAMSmZyZWUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Soccer Ball": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA8Jtb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAAB8AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACVHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAAB8AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAfBtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAAB8AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABpm1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABanN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAACqWAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAB8AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAMAAAAHAAAAAQAAAJBzdHN6AAAAAAAAAAAAAAAfAAAABAAAANcAAAFSAAABAAAAAPgAAADpAAABFwAAAN4AAAD3AAABZAAAAP0AAAESAAABAAAAAOQAAADhAAABKgAAAW8AAADrAAAA5wAAAOgAAADeAAAA6AAAAO4AAADrAAAA5gAAAOcAAADnAAAA/AAAARUAAAD1AAAADAAAABxzdGNvAAAAAAAAAAMAABAAAAAbbQAAJyQAAAD6dWR0YQAAAPJtZXRhAAAAAAAAACJoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAADEaWxzdAAAALwtLS0tAAAAHG1lYW4AAAAAY29tLmFwcGxlLmlUdW5lcwAAABRuYW1lAAAAAGlUdW5TTVBCAAAAhGRhdGEAAAABAAAAACAwMDAwMDAwMCAwMDAwMDg0MCAwMDAwMDM0MCAwMDAwMDAwMDAwMDA3MDgwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwAAAMGmZyZWUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Guitar": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA5Ztb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAABUAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACKHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAABUAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAcRtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAABUAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABem1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABPnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAABWqAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAABUAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAIAAAAJAAAAAQAAAGhzdHN6AAAAAAAAAAAAAAAVAAAABAAAABoAAAEuAAABlAAAAVwAAAFqAAAA1wAAAM0AAADRAAAA1AAAAOkAAAD9AAAA3QAAAOQAAADiAAAA7gAAAOkAAADfAAAA5gAAAQAAAAAzAAAAGHN0Y28AAAAAAAAAAgAAEAAAABrVAAAA+nVkdGEAAADybWV0YQAAAAAAAAAiaGRscgAAAAAAAAAAbWRpcmFwcGwAAAAAAAAAAAAAAAAAxGlsc3QAAAC8LS0tLQAAABxtZWFuAAAAAGNvbS5hcHBsZS5pVHVuZXMAAAAUbmFtZQAAAABpVHVuU01QQgAAAIRkYXRhAAAAAQAAAAAgMDAwMDAwMDAgMDAwMDA4NDAgMDAwMDAwQzAgMDAwMDAwMDAwMDAwNEIwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMAAADEZmcmVlAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "Drum": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABAZtb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAAC8AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACmHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAAC8AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAjRtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAAC8AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB6m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABrnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAADK8AAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAC8AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAQAAAALAAAAAQAAANBzdHN6AAAAAAAAAAAAAAAvAAAABAAAACIAAAC8AAAAuwAAAK8AAADfAAABAwAAAPUAAADoAAABuAAAAQEAAAEIAAABTQAAAPcAAAD9AAAA/wAAAPQAAAECAAABFQAAAQUAAAEWAAABEAAAAQwAAAEUAAABDwAAAKoAAAHuAAABGAAAARIAAAEUAAABEQAAAREAAAEYAAABDQAAAQ8AAAENAAABDAAAAQsAAAEKAAABAAAAAQAAAAEFAAAA+AAAAQQAAAD/AAABDwAAAPAAAAAgc3RjbwAAAAAAAAAEAAAQAAAAGcwAACZiAAAzqgAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMUEwIDAwMDAwMDAwMDAwMEIyMjAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvWZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAC7SbWRhdADQAAcBDheSIee06WWALcHUun/Xz8Z8AcAUHrYEAAAPbMOAUQ9+AQAXgDBkeSkCRhQ9nPthDFwbWBgjAFFBE1+tnl0xnPFA9Dkea04YwXYYvny3kBXpeeXDvEyLg7/IL+r6v1cueDMNkv1Jd8gqhLC2ITB3MnpWNDykKFkZJGEvk6PL0crqOgqP3BqaWj51/9igpXWPVd3k1TjJ1r1elbyKpvs4UfWFnu022rxdmHpnK19vKw7TnKLgYo86Rloq5mODH6NFiSteE7JRmlEJ0M2xH3Nc09a6m53fdpoAsAAAqHABHhegiSKojAL/HTVss3aAwCgFAKA4XzW2Y+TNFauSVgq5r0kmy6j5JpvifU0uHvkgXVwUFM/YOcsptFWy56bVzQje3u+/S3TN7DPtuNSE2dXAeiTthYrD7b1icyBiXTJQSmwsOJ0bfqVJWBDNFEsQapCyUYIOkzqTrVoWiAgdYmtP5PA7Pdnk3Gbahg7Aw0JzBn0zyv1/r3smP4gJYZMxk48hiapet86pKBIVj7LRMcFJq6+aUbIgyBcOARwXpOlSUKAC/w60BQiAMCgoKXige/eb3YQwrHVW425CiZvWUa8cYVng1yzi6GwaJ0aHap4UrrKqwMptbYy2xGcmqLEqj7q9QucnFMeHjYneT7CUrwtyczKRadFKx8WDrMB9wRqOlIvWG0hCcBGwGULmOl0eAjPpqB06IUlLhe+DF8Fd9uJaHBRduDkRaBZjv/aE9N49d0ds59icqsKOeRxySKcoTvlIQuWsWXABwAEgF6xMRIgFCqFCMIkiJ/zoi0xkKBmgN2UApQAX5ZG3jJe+qtXWG59xTmMDKPoXL+J6pClGRISmF6JdtC2yTLWTpCwJ9HBxNXj1QTsnL90ws1MQ5J1Uz6spqwOmWNo1PGBO9Is3cwvWCcgMiEweWHEgstBigCgz36f2x6XMFhIAoUIU6/bexndb4ORd1XdZ4d0hkitPR8zqRAmhDfUC13z1c0ToHKOSvOf2+U7NRjzxf3Y5V+EoXpKmY7G0milZ0KCUfTqCVnwOuMbjCw2zkxCtAAWo9SYz4zAKkwXABBwBHBeQVFRjCRJDQTBQkBUKDET7/hoGwWRhBVAQybgoDz3axHC5QM7LSRFNyIrhUxOfBgIT2wONzj5HH7rHSu64pO1bswxP3EgnlHSgQFtvpxz5/D9b9n+mfLKj9m27TeAwfi24sAQvJzJg/ueeJ4bDCUnte8wNC3qxVqt69HaJ1odCVgQHBon80AMsivANhjMdXo1ulYy5fkJ2fIvtPoWTHquFtFWJu0c9tk/RDCgOWAJcIVKTbkdx4F5eDEqGJmZaMp2Xcbmtt78v4qjaVxuG3zubCFPjRRET3uylfk16mOInKQfoOBJRuvlecHwPt4J7G5R3qUlekzWlGUbztcQAAFHAARwXrEySIw0mQ2EQxE/zHUojYsYEAMCk2iYDReo1buV09O/x1tW5q9VjhMNP2f/WEg9HypmOqZ5mzhJ64/DEuxMQRdN79SCpqw5vtnMh/B2B3sR4G+bCi3GyXV1eVaonKFwxBf1TvByxVoWaeW24LWAhILmDEJMM4nOqxp3IRGffPa9lm614nJapvD2wNDCq0m6CfrsiTn0AQ0TnDybE6AFCHPhIJOxGlBtXhb7a+7+ftVyPuiCEScTukOYza3yaf3oIDAiN75Btr6LdOmprny4uHgmfaWvwD6y10QER9E6Mg9WvQiYKDU37aJw6GG+6/VMEABwBHlesdJRxGQRFQgkfX6710xDmUa2jRmJkgogqigCCM3ngXedbj62b1suuMEkg0MSDogMMtuVmzyL7zzwZ1Bk8h41+EuEbuF20SN8b4hqHZ0I9vVeiA1kEOGQJGD7Vg3t8mSKnB0X7z9aC/9Wnbmu6hz0oYtTpOHC1Ywr6u2mrbtjnwBLYd8ygmgGpZTVxOP4yUVluM/awQ8XPjh1FuDFW4zfzSTo0MIEj5rRu0JgZWx05k9kIqsJ/C7GLhY1vnTiSTVQRqs0xUgow2YMvZv7306pfscTMvatV7E0rdmsgbprL4QEFCJU4AQqfFv6VfVNkJqxmZmk3KQTabpGJe+u/vtX1Zkz/x9vrn/P25n3WyP48HBcu7R/DFoM1IeKsmVTSHiWp/77qppAH0BNqiapZoxN88nQeuT/0v+JhXmfzC2y2ihOI/wbnGOdDT+w0AC7078yoH9BTVxT9QF2jM4ockNZJPdaDRaYMwiFIyyjcekogP9zrXEG2WIaYKfsPuCNO/epNZgOACGmHOL9FNh+uH4Lo2OpwtaMr4vo3oPPut/ZuHGYByeP8X02vlBX/lWNdxvSD0s5UbxKl8iPZ5bPKi9h/6lZbzCur5Dz+MmpdDpKzJrSJQtVlsgxU+12ZBoX7YQt9Z9Xx7BMoME0k8aphApKoia8d9HTcXH6lpdxoML546syzfZ4mObgFhrE/2ugG/Ge4/9PIzajCF1d7c7ZdnlxGavpUr37JlJ8s07LNE0UdpQSibzVeIIpYvFEB/zcQvdvFL53793W32jDR1O7fWW5jpitqDTmC1kjvlriV+ixxNPYdezGi/+8bNmrXjkfY6dTtMEyFJW60aejHMqOsooimvKAiQO5/hhGm7yCVnqbAms2Cj/IDw7ewy2wCw4ABRteslKZSDYqIIhiAKHzNXHaQMlKIUqUEBdgKujLGqbt5lqQaY05R0K9cUInfGnVzTElPQqWLzKHqb6xjbyPy6u2zRg8SUx/HkrZn6UvMZRTDtz13SoJzKV4S9ZI8YvljeqS5uIk0cLMepdQugi71U0GdIGvLNqDRzkKCZBYVxrHdgsFIZ2AV9c6cUyL8b/Yc0WWO8Wshb7FowycM7rI2D6lNNAgUTNUQlmm0bvXLbPZXPjyU2+XYm+e5YrkU0CX+9ApurVa9KtxNdE/iw83PPP+/clUmoTNkS6MQ+JA6TaRtQaDoNgA//c8TekitQxdPqvFzOhaVI12y8OLRiFRYBwE2V6y0hoINhIUhoERgEN9jNG7SA5RTKsZAkiARgDIneY35tRAy5S1mzY/MWBFLbrEbM87+0NJMTE7B0D9w4weH17sOCWP8+5cF5e19dn8dJ+4Q7psOTd2u7SlNsdlZB3YFAgjFKdGFT3dq2bGMI8hqgqF9FcsSQGO48HaDbu83AkWaMtVY/Cq8i+NnX2iz1sR4o53tRIIw8mDuBfRC4EE+015+gNt5TtWiStbPB9OzXzSioVVnuW66aBQVC1TVWySa6azsfSuLjQ9EDtozXHzrCwtY5Oh1BnX4GufP8ZmNtrUe7X1DXiXXJk8ZLG87YVp9t+LZjyfYUTl58HjY5U+0XwJFl7AA4AEkn6aTVISNV0yJiblRmjE2YbVGLestHjqYu3XzGoX2zU1x+WTnqbRxw/r5XNbE1daQ41YgADx98kfibs1o/ez3+6OdSw8A+Lh5Dxm5X98glntltW/lXNWNfLFb7774OFFpRX/y4zxGrSNFJvtPKtMZ+upqM0augGJf1KwdcGquji/X6642salBH9y2ux0urjMJ9kG6zilB+J978b63omr/Ju3YFItDS3MYyS/O2faPcDxtPZzkU0KMEuDdjxHF5EXODG4vHN8gJgmDvnhKezoUHPolcQoahZxF5kUfluf9Q4gTp4wngZHEuMd5aT0LFj7c/PPRZ2a3vFUt5NEnOYHsru1A2ZSByrij+zwQ+K4778jyof3tvfp0i8DZRD+ih0DyqP+JFjB9NIyUAUTa2vh7rSzFJkzIGO9yKf2n2aWBfw+uWLIxMSTbU84TDgFe16nMxEEZAkQQgFONEjSwAgEwguSIsENN+cMvvHd01e00ecuVcuVKsTdFk1HozMK/kKlLIy+Kl9l2AT/1svuWTOqcacJ5mw69VOpnp492eTtRKdlep+uFulWaQiho7Cris+lk5UROp9SwhtFWo+M/Vj2f4LQy1ZIqOOaLViI2aNZ6DxB4G0eWcqXkeNp1cX8WTfpKPiCGKRyrDP31/ep8fnNNO35ZHbRli6aJ88KOUCO9ern34JTy8Ug55yRxHU3o6tZzw0yOqgPCTHgpBb4c3O8Pr5xYjvfUNXRPSufBvrw+eIJQHNAb78VNgrAqTvAXz0IFwOABWheosLaCEJAiAKuuiRHUMIWGXM0yTEtYQI53oeesHm24W3abjCaqYbihbwvK1YLHJvlP/DreFZW706+0hgnypo8mYTeFKXzLeK5YYPZGA75K8JrrJweRD7u6V8aZEmNWmLuwdKwd2cGcArkJJOcTIM7YGglSggI4SNJViWFM/aFYzQdcmDNdZt8pWUrb/K3X2XkaJ68ygo9gB+R8aZ7741EuEiadvgmGHg7g6kmsm52nMN1CgdtyFoPxskhyNO8tKghNm7HJX5QuLD3DIvK2nFMKxo0Bwx88465vV3/cTJppd9PSEvR/INHuS4VGHPp74f8+jKYVkFBeVQBwAVoXouyUMRhEAXXWo1Jbdr21TVuV6QwQS4Sw7o+zVaX83BtNyrVH0U2u7H8GGpMhCXaTXop2aLBSx1ppvE01OEZpEPiTo4rJL68JLz9EkRYAER5AklCpP0VgBOCdUYkPQUkmaTVuxxUzwawrMza64WhA8IE5yl28aut8HZtuOTu9ctCUMc0PW9eYoUbJQfPgWuEjCoKKZZBdeyApK/rqf5LVRGbFRPdJ+iwqJMFY1vgrBkVFdPYA+hjHAISwzu6VqaM4czMjfbP1G/8tDmjkMc9pF5qzCibohh5gnRuhOn0+VYM7MY79Y+D0OrsChK7oeTwz/h4qK4FhfEfxLADgAVAXqa0EQSAEnTqcEi5IxXQVYCREaWCHtW/aP/ygZRS+/rlaz5VZoONOSLl8lUVtaKLLqg3UMzb1qbufQe6zy9RbaKab8fJIiXxj2UXHKEdrvF9JH17JRM5Ig5hBrZJJmGmi8Tu7TN1d0i/wrO9pneS2butR/fawKSC2eF0LmTqBWZLI6dY11y2UFQDaiYqaQHNSgqqaz5P8Ev6K1qSpdERUv4uhYkxXH8++TcMuYeonad/wPXukWK0BoGGZ/n95gdRzOICYRR8Ih4y6IIVsmgwtE+67Fsc1OY2YKTj654W0gRjnW1DAPbX6E+mkRLGcs4KzgAFEF6ms1FEVBCQnniGTjRUtbJYXKFNFrsmoHf3LKxe8lThZnCqvdvHdNpaQySjGYjgksZFu0EogCkV+yeMO18U8ZrfeHujloobfyyxO9r6FWQiH6Y5b3p81akKJWoHgNeo4txLvmzTWuUQWxzvvu2T/3ZStDvoTYpP+qiEPkWhOhv6SN4IC63VvZJtVFSTAODx2UUT2m5TUTVbddhFFkhcNHj6fK1h5/jMA1m5jNkxoc8x7Zh1DJQh6kxeOt9QOMmyDrJPnLfzGyaJNzpmQnC7jIip1oqYrNJnFVZXm8tFi9kiPwnWxuj+XXw3+ULRgN8K6EE6Rfa7FInxKITQhYuRRcAEuF62whmoYiiJFOuY+BZKuFW0xrCyyyWAxYIj4bMRAap1gT2IpR1JE+DPOFk20z7PboyjsPelXxHQMuxCMWTNF6VTpEtXSa3oZwmk0MKN6SSmi+UJPMKFhjsOcHZWKsolr7udclSPwhXkkYwYFgawgrjpxrMUVwrIRFjneZAhop5wloRe4ODIBteZlJAs+bIoQTMqOUVrJ4EZsg2LBrv6pq1Wdw7ABZCmZazsFmv4m/HzMJm1lreJalgUHRLyGp2V4Wmmqw7juKbAGz/BR4Vw3Vu4KKN4B8D5vHsx63xWE9lssKofSeWGRx1gDJlDJ2Tv2Cuapx8pr83ZHoQ3N0rEY7/RMM0bZJRSr2vWHQRq5wITY5hwBNhes0KZKFYKCYKEI4idGhcyNPIZ0gtKIjRUgAvjfMEw0UGtC+5JVkaj++GF3p9XrDZ6BCfHGjfjKjDoiEskZkbPsSTLjPJS1yvuesiosgwjFYQyASl1wtBs0cjO9affVoU0MrTmwgE/aovzF8GHcVC+3KyBLZ/dyAuJgNfow7UQpPrsjtaA9q10hnz0CLwNwA4Ky6c45izW1nBfdR9jwjbj/7HhAqN7oWyrwqnQ0XakWeLdGZfpL9oOXx/lUqO1xyVnKtxQBwDz0VlsVE3DJHe/6ISoAR13fLzZQZz86z0PvcPs6j6dtCYSNsL/dK4Dmap+CqWAYf/3UgXgBNvRugWuVgjwBOBescOZZhYSCUSHIJhIQhS7jPiyVwvoSwVbIRLIEwBHiNf4z35ITly9j+kQ4/CJ+tPSxfVj2+sIzD5wW3r6hTUlYEngVJdRP8jLowH74et9sNXYXOm5/B2rlfuY/NzxoKnA75ykobbZriasj6zQXrNFkrqV62g+huRKTAfG+3ceDyB0QZQJUawIylQdTYSFJUKNuHosX09KrfBGKysvGYBIaM85dlx2Ugrblpx9mULIh8w/o/EEIKXyO+Cu+YnyaULAQjEA0sua8keLCqjKjxye6ChgLxKopaYtxiRhmN4idQynIfhCTTODK0zrgvFbRcNt3e2Wup2Xwur0fsDDiskNoLQfIkiRhCkwOpLDqxoXuOrWqOAE2F6zwZqoUhoEhCJHkjScLXHFljFghECUBcOfo+rOJd6pnQazi2SGUk9hlFEdOd/XImk8sUmCzZwFeZlbTqSJZP1BgbYrz6Nxxu68z6XSwD4zTpziXBqe6RrKCglS/luRFOFrUlKFGdiUxkvR8FMSJ6yEg5aI2+b8uiN+xX5pTUDFK8hKCQmD0DMbgbmV7sZeBHYJtI1FmKZ6B3Qj+mFVf8KlLk+cVYthFDSNR65LdBhB5dc2Do5LfIvJHCnwApuyzBRN8V99Xj035YH/z4HQ53f3eyflrKUv7A2MQmALNiNlIE5DFmQQ+A3uZtj5qEAqqOff+4iMlq9im9FLSZjyxmX4z/Ebi16bgwlMMgopwAToXqa00CwUOYiEIkfVL6IODibuSRNZteXGSXhIgieQSZ/lO8xQzohvqBdvoFWuuLMtuNrpFxdeRVOkWhG6jWClN1e5wkRkelDMni4L83CJmXOO+nOx+imvQsmqi+U0RQMwILWi0W8q9//OzSZoKll5YUAOCV0TnwNScLyaopQRs+EQiIl+d/URHgEgWz9TCGRQRGRPgdcow9Yjt8tC2vMD9mHET6wD8Prhh9cIzllce6sR7ZF7MeAA3YL8s9Vgl8gAno84iwZeww274AGsPiM9luSFGhfrNxgxXN/z436R/yCxkbIk63WetPZhLOHwtC7vzEKHxH4wvG6RRDrcesqXIADduZb3q31PdwAEqF6kw5mqJAiFAkMRltRdrmeUuOdL76Ayxu4sIAXrjQv6H4urg5zF5pyvPaZWlU58NcvpMejWC6NSc8wYajC2wkQCa+Nhc2pBSSLWhGEJx4EhHgICXNGaoDJ7n2XAEYvOeehG0UX0zsGNqJXDSTMeOMj9tnmmScTQlASMYHbFAXRO8jvwKSUiRUeomMAQGmERI6evGhGI6aMAEgBaaSd9NMOoLMyAZ0s0O7k5Sk5maBbhNDFoTgQZ+rvxN4TEzLDKURYFBWlfVVxhIdxvwzxu0RcgJBVzZMezvig65a6kuZinK+tkgfXiSv7aPa4JWPBDj6vhaQfxHWuNAyaI/pktNFhtEglCakFOlAgqqb0UTDWvTgAEqV6ms5BsFDENAkJBCIV7EL6l3aQF0N6KRUkxYCNfJC+O4SWHx4Fl3G8vim0mIRxQpqBMQWPqbWlY75rKWwX7aLZuKtPJfZad4XBxmfnuq1u3Z/M8t9vOMn4MBVjNww1mQxEtgywFAC6tgeqByeQtOb+yeNaTBYU2ZdzS4JMNZqEzMV6Ba64bszG1eGIP6syaH50dzCKVcQjIzRs4ANTM6zRoYRCC3zOSlVNXGeTCdc8CMf0+6mf+7kYgre5mQyVBypeE3qluvVjCA3RlAPGE1M386nfM3cegOXn7yaNJ4qA7RWdOhgZVp+0AlxztMOOxglWhbPgub5yyPLSSEqLbPHt7Tpnapi2CsJM2yKnABEp/+kzSDQL483ChkoXvUdtdK4Tjlb7dScSv82NeLqxsjQ4s+Vlmp9xeYea/rICXZOnppuWYpY1t/vVe9NagVqblYjmCQZyINAoKOpMuqz4SK8Be6AiLZd/SbyF3gWictMK0Jn01srAOqik7Hb4RIMzb6s7ZFgiRupbThHn6lM0bl+m1DyVpz96eu7ZBS2ifim3YbxIigCwAaI2Vi6DToAQgsCKwAXCoABwEaniot93+b6jUmsFkjVVGylGZrlsZf720gE9/7/zXfnbs23Nb7e/xjJ6yba/XxvJMbzmbT/ZfpG/TDc/322U+aVp6HcEaz29E0ZqWPD9V9+b0+pzjT4F9svCOMR+bakLvW9eaEY8p/g+q1ApRbbkWInCqcwQePEYOWxyaT7X0PJedzXebdEnj9b7zwteIkOGlhHzX0mQI7HiOxcrlJqPWSfsP/PK4JbGQPAoAPo/+uzwbquwEw3WQmpUzidP8P1/Z7ayyTIwmoWXskYOLAx01mBsSP8PncHy8O+uZtyeOxwtWZ/9f3v1/sv7/9n4v9b1umaFgcMisZzVfacHYVDQyy9P/TutxHS+1raU4dEwZF03IcI5GbZN3H2ecjfmEpvzo1vhtCVaG8Q5UEEi8WM63OepVFbBKKNMaHutjz7X20bjUcFlwQaMoOkKXBGlRGgPq85DT3msw99iMw+utqKp/qJsXYawDHGcBk85qU5r3R86SxcUDa+kBLqh71pUH8H5MoCGkhlkq65xAlcPV99R9Ql3RL5HmFfwIX4RXOVtQPaL7s7lz8YmVtNAgL1F9Pa+sgHAerhHk5rbB7jY30XUj7PQKL+52giT0bSuRLYw3UKGQu5uy923oiiYhdCG5hLrxZshtshlv7ONscv2o4ASbXqmySEw4CoUGpxCAWW3TdN3hdO+/JjEwy2zI3KoCbZGzLDet+q455MgsWeIrW69o/78RoAh0dWblzvLQWLdQaTrSziAzQjNEaDMqcppUvWC3FCOAwVbZncRzM3xCTB8JLS4XgdtQuBELELAQP7pUcUX2aqqe7CEEE+7sOVwD4fRLj+ssyRKbBcaGAkLGB04+FRC7uYwsp7K3RDlieObQPLgmo10WDlb14Gr7++y6tDVcwLkCr3uI0ng01xJdx40FgCVF1EHdygN1lmoVnspU61qMbVyVsOE7pgcBgiKpM8pb7euenKKcZTqKDcQggvvZ5+72G5hIsuMa7o7NYXOE5cM4cEgCpYvZITJjF76ogCni4TA9A4AEoF62UhBQSSQFWmIAhrM25UIzBpzGbvZupgoUAK0NT1/zKww1KprG2tvVzs1PvW0zpHe/3AdmKH93SqsKqmFVCtVl2i/qQAlxIbkM4I7tSw7JmUiRBH1+IfsR+g+EEMKiG9ZCYcAUDHCZYt4k0Jv8++oZYZXz/Edj/R1p42AqLF4W6bKM5pyuVUEgVjiGMPG8PdMyOmVqx7Pq688mIisXj9EJvjePoz1dCc7uKLVpqYcMVzuddV83MULpso4g7s9k9XiCoi4uQCxcWVMhdcgKwSbTmp6pVkV0x64oX0hACrK1rjKyrm11SIr5QUd8Rcns6tlgYDlnFOWKBS+uO6+ytJtA1LDbSv73+vCUOqkInajgBKBepFkYtEc7CgLigKoMgBEVh8hnWYAVzo5OYG4KBFdAGrlDpS5eWdrzMez/lcFk+EjvJ5YFhVgOlb0t9Icd/dMXsOx/BhQQDCd9zhT/edtpweSNyz1SOE1kv4U3hc9R2GLLPLxtHciUxOgVGXrfcu5V3HF/QianJTnqYCShKQ7YIgYSeDs57Iv6SwmR5fWSrflJergJr2tl4VhAykmaXnqXSUKgRpHPgc9IBdLo1e/nyjEOcd8BNxGKNVfukq/LPw7cdoRVb4xEgS2TMDjjsCamAV4arJ1U6bj3QRKHZw+MbCxUrztdvC1bjXZd0Bcw56MnssOpvPWhIVeW8r9iDB9b6bLB+CHFrzHfSjvf3wQ7WQAcBLBesdNQNDgrlYUCVYhALiD3ZkhDlRGYwwyioyUsBDzjW4/kwjIEU9PkohFITiF3uyMDDCPlVt/CQfUF8PnEiX88vTm36akbQAd0hTjuPrPhg6goOuUY7gujh7FYFQCshsziwNyXhCNBGN1MsOu9hBWvxOo7NtnkSWobYNqMZFHZ1it/oMhTCtTTZCINuZnKPBBnTgJkuOozlI2KS4YAovhqd8+xPHlfAKubanWZnW173KoCr6efPmbEB6ezoZgFIuViA0RiRuMBGYEpvtXpHXLtvcwYsnFfymqggCLIXRfZ8++lhEYjkVDEmZnnIljftIsCIX3RzTi+ay84Rq7ISAmkwSDrg1lp2LmxKPvrAFBwBJBetVGINBYsDoRigKtEQBaL572vZimvmp1RHeDKKpeKiBc0wFxYTv/QDVZBjacZPbNqmsK67lwZVVrXf3nPZ06+y8MpqkZMZC8qkU6E+wZF5+iEd/19S6gR6hsU74T0UOomfxy5inPCeVOfcFQ4KIVBxDPPNBAQIicAoz4s8rWUI1/AULBVWsclfbHMA3fw058YuVfqiDO/74nW11FZie15a6a7b/zXPwXrsvQWtq2rXXtLZvUrQdXOxc32KK7q6JgCpnMosBsm5FTkXyvKhHHN1tHexwq+MK2Q1P71RUJFgDkI+G5WIpMbizUSXK+nCxuCJBKGO29zNR8YQYhvS+lVVYXhJBiS+/zBKP26QBIcBJheqCBocFcVBksBUqDMgBeRz4OYxAwbZdYbXtUTcpAAVBPvaq3pJkgEfXIhlNp693hVrcSl5tC60mZSNqTov0nQoT8oEWGNDg1BC/7mMu9l6wXhFKCkJJkwqUk7gJInAtNAu8y5UwEJ1ITnsXE5dn3sWPPt1HrABiXhOUNoRCpuqMdD0fW0Gfvujj3zotKjpkUupqV4arKoM0nBFyaxvU3LZ7ovNx5dGmO+4tbsjgbXDW8UqeqOYoTcfCVSlUqb+XKagHTw5JWuBGjKRUYKOqwhHfKX7L2FQL/csKe3YtxxsteF3zWJcP/cbJXsQ0Iuu8W3C2fW0aSuw5KD8fuc31vBGepvniy1hnbQ46zhuu4qTj77hBEOAASQXqcw6G44KgYEomCqjEARcds8RG1s2iI3jdJzcxeKkA4mDN1PiV4I4qNK4YvFN8zxDw9THDVNB+TNVRLYDk1LvnON8lFfmETSAlif1Q8LA0AJsNVDhsEJv29DOc4hkWa8Jac+8tYxFhUyQcZnLreatYgqfZ9uDSMEoOCepEMod9bawLUCi9GZK7dwLytyMSL/NFFfKISXwIJMe092axuVXVBXdcC5JzS4bpaZ3GFXW7Y64+UuauhQuktgcp4QkBG5c4kUhKZ1Qpy7+5W4jom5unI0K9864OwjaqmRaVegns8r4tRFOCc0nM5C5ipADKgiRPK4fN7oyKllFQAJ2kSR73ZaH7qBJu4JIgcABGBeqjGckBcipMQBMMx6FKYBkTdbbjLZLyogAW4DQnzo16RlOaC5sKzoPgtK8lmn4NI7eTPM/PH+lE5qiHHcLJnjuXALcmJE9wGcLjnxwjQDxr4Bwt2MxmS8vzKsEZBuDa13kcKs0UBnqE4b3sZyq9b3Hxejdrdpwkw06wZ6BXAA43Uihjw5CUDxtdJy7LcEGfZVaJVbU39ztjVzyw1ts10zF53nkExBG07ie1uJzWprVqr6vTu+Cm8RQ62DxBXbHKFiCl2UCS19F2Fax2s4iu+ieVyYGeb+83mywkWtfYaz8b5TcFwpukzYWcejJJIsgQIjqx0u6v2Ek53ETYATSjBJ77p7uIneh6bKIRmOAAR4XqXYYJIoExXQwVEwVOIgC3LOXZPFaKwKHNqw3pteCQApxpTLhIY40Pq3R4tnL2JzgY/r9Vmt98OS1UXicFNwWLfSKZDEk8YRqTXP/YQn0mIXnf6lyXCTCF5klV9Bg89unKUuYuMmeUOmCYzw9rNgvyeDjuz2Qxx1pXjn1ph1+dZxZ99+x4W3DueL6SNXorHOPVLK4EEXezDbOou8R3z/TQNwxYl1Ofc1M1go3UzGMRqpiUTSOY1EGLcuetmrObEAGZs6AOyeg4CDKjINyRSoBOd/AQ98KqCQhUeFWSgXsIheycZ3qYgcinCosEVNcNLISZ0UQIja51PynUjBFguAKROaX9UEBDjSALDgBGhetsIYrkgKigKoMgBa2jxyY53pc5yMsnNKGwumRYGOFRGRf+VIDCnJK53SNwWaX3i9P4kY0xektccbzhCnj9M9NLLaOcmSMylgiJhD9h8Vl0QVMUwUIqiAEFeAs4AM7ycqM/YLFQbgF4m2dXr/gTBfuOu/b1vLjOdo2kVGUXyK5NrOPS6GSNd1Jui3ePq7F+ijT9UqNfLthqYtzgRf8SX5KQhkpMvLKM6vgGrbYi8u/e6BSrzR/bXX0SyxyB34s6wX0OmbkA1DCA1SDlRYnOFxu/nFTWbEwlMf2xey9hYQORefm4TXYb7VV2dpt3Txe1BwWpRe/nVvzvfOPl9DUBAgmy8kRO/DMTEQ4AR4XrHTWFQ2LImFAVEwVKgVEZAC6yHvzisXQKZeFFc5AXiosFFpZiiHzu8lRwMDT1LwSShz/1JJKf1ET5BTz0hpzTgGczxQbTn1d2xKIjmIq/WvByWe7xuBE04ZSEwBUVkCzIe3mWX4xx84KVAXlG8UFGO/0CjH0bb9e8N3unSypGMAXN3ZPK3NDQQ0d66LY+7cP3yuia3f7oHV0gvp7KjAcLZd/pW2h4i6Z7s4XLgFYiGTDPTcrvDMoMVn5VgmbhRXaHUC6fKUgsmgBZdXkeNt0bTrXJb0ieJbVe/LEmhOwJWN+zRUUrgOHM8Y8Cm3xcwTUKy7Lve8sfA2sccPXBgIC3BIgempzTEQ4ARgXrLRrFR3PAWGomCpCEZgCVW6nqoGyYwgY5ApFIsHXetoWufwK5SME91J9bIodRtdA/w1Ei5BSn4kxRackGFxrj8t2oEmJWx5xyISJ4+uy0XjPaVuObw1NtxSsXnucbjjdG3rvtV4/AprwvFo7sJZY933pm5c7Wk5GMUwqQtCDroAS6OQsAFr9fvez1UW0RvgYwg8u2V4vf07nNFMG08OD14KJKt+XCldmBDGlqXbEaySsbxaPqZ/Y46uKUcfNB9oGNcVVANSKpAWw2CGgj5Fr87G6ssNXlfHd7k2Wboo05T/uOHRaLT2qLSpv+rrGDgbOVpe94e/u4RZuk/usQTsQSSxyECMwIhwBHhetkFsLIgSlgKoIJjALNE7Z6uMyb1sukTvDGtiSg0DUoyB45gq4pmmc/Rs5aZ6Qfs8PUDWARg4bJGpscVhrZL7eovIJrm4ZDwnLEgBl3wKdf1x6evBk0HOgEdt7wxAltUvoH5bAJqkNERkYYUvV/ADJ1h7CqMLhC7RMjOUPlqQf3x1/Plv3euq6RPSlXPBaa4bkLG5RfnLKlz24DKJc+iajCQzqTVTCOHwi0W3FSF1GtWu+6VH3yV9YHB8zOgvCZLiBhY6AEtEqqk3kMBnE0xEOQbFC5Kx8q74qFXJLRmfD+hTCBDn5nGlta9poux9S/C7eEJ1IBxASjxISiRDgARwXrZCXExICYWEqxIAWpG/HZHbF0RgVzreWJuxUlgBug+vXF7E7EbngLs3oNAlBrz829336ErStJVHWOHXk0s8Ypvox0lGShmmWExIFB8vvJp3HT0eiEVLeWit8vozeJWZQ6dXcAzOzAltxAIHv9rIIkPqnYiG6ieMJIhP8qxsAkfrui6q7OjScRMedg7drL9eu1EHbLv765c/Y1X05q/AvjnIdsyu1ksFd+1cK6Ks45j+EZ2+PljI+m01+4A7ABKMTeNgtEN3AEbIVrdMTUr61Eo05Rt1QjNjMwe0u+mNETlhdW8AyZL4RC1ci2e6lCMfFCIs0KBLXSKJRSSgBwAEcF6z0WC0RiOdUmUAlrZ+adxFmKMJumQpMu27lgM9rbHOaUOlRBJ4AqqHujJd6G5R7YspUYTfULrDW1EOVu+J99G/LMkkcKwnA+eklJTyvjTRkNCqgiANTT8HRmB+qvR+jl9DDMS0YZSyNXvbiKYfifo7vR7OSXUopzxV9jjkxVfz/NOjs1tbPmbdOa9btyzl7Wue3EzSaOzlXjjn4ax55uMeCKtsVGVuK4Z3yi18JjgJu/jx36YrhruuJHcTUgbxykANmUgWF7CEaitTXXOM1cSxQx2cPjlM5fHOrpKzcqei5dyd+yEob2lRel6rWmvJb8Bi7StYEFUk8ifi5OJAlCcwA4AEgF62QlxQIguSAqkzAF9bZyleoyiZWSA7GAabS5oAJCMWVNdxqzOBCpqkpuKUhGcMiaAx3JNx31//4t5nMBNi/ejYYhSUMQQVnIAuH5rw0LuKhETfgkm24Y2enyKAnrHqzTmDmfjTD4+Km8/uUTf1Os8+XX0uV6cMM+cvjViHH8FuVTMSFGKH20ju+6xfwlY+HZnGhDt1f58Oed7d/Y3wVqXaFWLnS959Etc+bXASpWE3tXcSd7WEArqrUl2CYN5ZEr2rtvklc4nuMnUvlUW9i8nzLJpRVaJ7u3deemTNneqiFxbN7GMyXFGkYcJB0oiFuIishYQAcASIXrhI4M4oCooCooCpzKAX4hvvbxJtkTmVEYbKoiJiyADHXziO44+GEPu7rJFPM4puTAd1NCM4oOn0xFywwqqKPWSox6gSgwGvAr9NisYT3v+FT4SWeX/oguCmt4zkVD+I7lLDgaUaaXRZMtZoyTExCY7H7k0OH5qbCLT5h1cEV5eC3u48Y1AxetsJJURSAQq+WDnzST9GLwX8+XNUSUqCPpmSETHXAoCuETOc4oXY7wt+grjUY4SFdV/PviYzGFybjOr8QVXf1wAXMhAoD2MCkb6FXCl4SEwVl3ykZRexVzxo6I1u1Wr3/U97hoV3xonpv6pmmdv3McKTAREulDCEiYBwBCheANTgjCcbCUTBVAkAKG2/W5SEbYqFbTZeTNLxJdisdDY/4Uphforfjmf3WG9XvO+ZJRSggYF4x+SXmB276w9eUe2FamWDuIY9QOe75Q/nUWzUe+6JsUK+MB3QnD4yDkuNAVNjbI1PzBkkd0HWgtNPL9wo0PRdTEVBOqpXTMZt95qirVi2fg7eBUVgmapj7iXd92Ar6evMQKjyT7Dhatdd1wXnsiPhdUGbm2zSr7C+vJkCueKKi9knLN8N9AHDu55iLkIBUALX6qJLqJmoy1c+xaouoGJokci6KpAky8UxQSXN9U0tWXHMLZMZTqtJX1e3AuSgBiH+TCSE5BQcBHhepthgzFIMCYVBYaDUSCUYhAT7uGVjsNyZzF7vdzbARUtli3D7JJBRIWJsa4rtwQzbcaRTb8wtew8qVUtdjckvjh/FP7joQqV6/bYQa69GRQUIYlCWH+zS8HlZ04g1BGmsLw6X+eglAqerd9LuFsqCz1wLojDSl+iuWSGJ6jeUqEiiChKmJt8oAVwqF8IrtzSM3UoJ7BIQqFwQyFVsydHZH81cEgikK9U3rmiSWwGa/uoHtTNmQ1UVej9MHiFcezqXfmY5x3jEZY66Z37IC3OkyUAWoJycG0njJTWyCuWeqfLKth04lfhorXm5gau0/VSABedUtmGuSr3FyAVDE5AqEWXQ777nFKgABT3hwAQAXgFUmNAiCwkKa3w2O42CRCRm52LZNBcstw8iEHgIE40iA2gayyoYTFUf/TjYLKlzpsPZVmSpmJFmh8SwV4kw5YqXRo8FA8ZPtNKK4yRoNqcyOMYCQlz/y2R70OZrvIttTAzErA6zKfJHwbCeTJm+TmeFk4E+RZ8s9uphxtfCkqY17O1PJZM1dVZp5c+LbZSmSlYVWovwSUFJHRSV3FO513q1ue7UNVDCqXawMOlll0nyonh7IDSZaQza0bYsQ7XCxT6JHrfSeTs7rDVKVZdbl9N6EDFl0TlRt2oFB1RWzNvcrSUAB1WkIgAAlEADg",
    "Clock": "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAABAZtb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAAC8AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACmHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAAC8AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAjRtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAAC8AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAAB6m1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABrnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAADGAAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAC8AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAQAAAALAAAAAQAAANBzdHN6AAAAAAAAAAAAAAAvAAAABAAAAA4AAADZAAAA6AAAAOYAAADiAAAA8QAAAPYAAADpAAAA8wAAAQoAAAD7AAAA9gAAAQAAAAEIAAAA+gAAAPQAAAGUAAABowAAAT4AAAD1AAAA5AAAAOcAAADhAAAA3wAAARwAAAEAAAAA6QAAAPsAAAEEAAAB3AAAAQcAAADoAAAA3wAAAOEAAADmAAAA5QAAATwAAAD8AAAA+AAAANUAAAEHAAABwQAAAQYAAADaAAAA7AAAAPoAAAAgc3RjbwAAAAAAAAAEAAAQAAAAGWMAACZlAAAyuQAAAPp1ZHRhAAAA8m1ldGEAAAAAAAAAImhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAAMRpbHN0AAAAvC0tLS0AAAAcbWVhbgAAAABjb20uYXBwbGUuaVR1bmVzAAAAFG5hbWUAAAAAaVR1blNNUEIAAACEZGF0YQAAAAEAAAAAIDAwMDAwMDAwIDAwMDAwODQwIDAwMDAwMUEwIDAwMDAwMDAwMDAwMEIyMjAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAgMDAwMDAwMDAAAAvWZnJlZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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"
};

const REAL_CRUNCH_SFX = [
    "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA4Ztb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAABEAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACGHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAABEAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAbRtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAABEAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABam1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABLnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAA4+AAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAABEAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAIAAAAFAAAAAQAAAFhzdHN6AAAAAAAAAAAAAAARAAAABAAAAP0AAAFBAAAA7gAAAPkAAAEKAAAA+QAAAPMAAAEJAAABVwAAATYAAAEWAAAA+QAAAOgAAADqAAAA7wAAADgAAAAYc3RjbwAAAAAAAAACAAAQAAAAG8sAAAD6dWR0YQAAAPJtZXRhAAAAAAAAACJoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAADEaWxzdAAAALwtLS0tAAAAHG1lYW4AAAAAY29tLmFwcGxlLmlUdW5lcwAAABRuYW1lAAAAAGlUdW5TTVBCAAAAhGRhdGEAAAABAAAAACAwMDAwMDAwMCAwMDAwMDg0MCAwMDAwMDM4MCAwMDAwMDAwMDAwMDAzODQwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwIDAwMDAwMDAwAAAMVmZyZWUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA4ptb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAABIAAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACHHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAABIAAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAbhtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAABIAAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABbm1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABMnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAABCiAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAABIAAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAIAAAAGAAAAAQAAAFxzdHN6AAAAAAAAAAAAAAASAAAABAAAATwAAAECAAAA8wAAAP8AAADxAAABTQAAAPIAAADtAAABLQAAAPgAAADsAAABKAAAARwAAADmAAABRwAAAQMAAAA2AAAAGHN0Y28AAAAAAAAAAgAAEAAAABtiAAAA+nVkdGEAAADybWV0YQAAAAAAAAAiaGRscgAAAAAAAAAAbWRpcmFwcGwAAAAAAAAAAAAAAAAAxGlsc3QAAAC8LS0tLQAAABxtZWFuAAAAAGNvbS5hcHBsZS5pVHVuZXMAAAAUbmFtZQAAAABpVHVuU01QQgAAAIRkYXRhAAAAAQAAAAAgMDAwMDAwMDAgMDAwMDA4NDAgMDAwMDAyRDAgMDAwMDAwMDAwMDAwM0NGMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMAAADFJmcmVlAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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",
    "data:audio/mp4;base64,AAAAHGZ0eXBNNEEgAAAAAE00QSBtcDQyaXNvbQAAA35tb292AAAAbG12aGQAAAAA5v1+veb9fr0AAF3AAAA8AAABAAABAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAACEHRyYWsAAABcdGtoZAAAAAfm/X695v1+vQAAAAEAAAAAAAA8AAAAAAAAAAAAAAAAAAEAAAAAAQAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAaxtZGlhAAAAIG1kaGQAAAAA5v1+veb9fr0AAF3AAAA8AAAAAAAAAAAiaGRscgAAAAAAAAAAc291bgAAAAAAAAAAAAAAAAAAAAABYm1pbmYAAAAQc21oZAAAAAAAAAAAAAAAJGRpbmYAAAAcZHJlZgAAAAAAAAABAAAADHVybCAAAAABAAABJnN0YmwAAAB2c3RzZAAAAAAAAAABAAAAZm1wNGEAAAAAAAAAAQAAAAAAAAAAAAIAEAAAAABdwAAAAAAAM2VzZHMAAAAAA4CAgCIAAAAEgICAFEAUABgAAAA4iAAAu4AFgICAAhMIBoCAgAECAAAAD3NidGQAAAAASTE2AAAAGHN0dHMAAAAAAAAAAQAAAA8AAAQAAAAAKHN0c2MAAAAAAAAAAgAAAAEAAAAMAAAAAQAAAAIAAAADAAAAAQAAAFBzdHN6AAAAAAAAAAAAAAAPAAAABAAAASgAAAFxAAABjQAAAaYAAAFBAAABkgAAAUkAAAFCAAABeAAAATQAAAGQAAABPAAAAW4AAADeAAAAGHN0Y28AAAAAAAAAAgAAEAAAAB9qAAAA+nVkdGEAAADybWV0YQAAAAAAAAAiaGRscgAAAAAAAAAAbWRpcmFwcGwAAAAAAAAAAAAAAAAAxGlsc3QAAAC8LS0tLQAAABxtZWFuAAAAAGNvbS5hcHBsZS5pVHVuZXMAAAAUbmFtZQAAAABpVHVuU01QQgAAAIRkYXRhAAAAAQAAAAAgMDAwMDAwMDAgMDAwMDA4NDAgMDAwMDAwMzAgMDAwMDAwMDAwMDAwMzM5MCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMCAwMDAwMDAwMAAADF5mcmVlAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA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"
];

// 0.1s Silent WAV Data URI for iOS AVAudioSessionCategoryPlayback silent mode unlock
const SILENT_AUDIO_WAV_URI = "data:audio/wav;base64,UklGRmQGAABXQVZFZm10IBAAAAABAAEAQB8AAIA+AAACABAAZGF0YUAGAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA";

// Procedural Multi-layered WebAudio Sound Effects Engine (100% offline, zero .ogg network files)
const soundFX = {
    ctx: null,
    noiseBuf: null,
    activeNodes: new Set(),
    activeTimers: new Set(),
    animalBuffers: new Map(),
    activeAudioElements: new Set(),
    munchBuffer: null,

    thingBuffers: new Map(),
    crunchBuffers: [],
    animalPreloadStarted: false,
    thingPreloadStarted: false,
    thingReqId: 0,
    silentAudioUnlocked: false,
    audioSessionConfigured: false,
    silentAudioEl: null,
    webAudioWarmedUp: false,

    unlockSilentMode() {
        // 1. W3C AudioSession API (iOS Safari 15+)
        if (!this.audioSessionConfigured && typeof navigator !== 'undefined' && 'audioSession' in navigator) {
            try {
                if (navigator.audioSession.type !== 'playback') {
                    navigator.audioSession.type = 'playback';
                }
                this.audioSessionConfigured = true;
            } catch (e) {}
        }

        if (this.silentAudioUnlocked && this.silentAudioEl && !this.silentAudioEl.paused) {
            return;
        }

        // 2. HTML5 Media Playback Session Unlocker (forces WebKit into AVAudioSessionCategoryPlayback)
        try {
            if (!this.silentAudioEl) {
                const el = document.createElement('audio');
                el.setAttribute('x-webkit-airplay', 'deny');
                el.setAttribute('playsinline', 'true');
                el.setAttribute('webkit-playsinline', 'true');
                el.loop = true;
                el.volume = 0.01;
                el.src = SILENT_AUDIO_WAV_URI;
                this.silentAudioEl = el;
            }
            if (!this.silentAudioUnlocked || this.silentAudioEl.paused) {
                const p = this.silentAudioEl.play();
                if (p && typeof p.then === 'function') {
                    p.then(() => {
                        this.silentAudioUnlocked = true;
                    }).catch(() => {});
                } else if (!this.silentAudioEl.paused) {
                    this.silentAudioUnlocked = true;
                }
            }
        } catch (e) {}
    },

    ensureRunning() {
        if (!this.ctx) {
            const AudioCtx = window.AudioContext || window.webkitAudioContext;
            if (AudioCtx) this.ctx = new AudioCtx();
        }
        if (this.ctx) {
            if (this.ctx.state !== 'running' && typeof this.ctx.resume === 'function') {
                try {
                    const rp = this.ctx.resume();
                    if (rp && rp.catch) rp.catch(() => {});
                } catch (e) {}
            }
            if (!this.webAudioWarmedUp) {
                try {
                    const buf = this.ctx.createBuffer(1, 1, 22050);
                    const src = this.ctx.createBufferSource();
                    src.buffer = buf;
                    src.connect(this.ctx.destination);
                    src.start(0);
                    this.webAudioWarmedUp = true;
                } catch (e) {}
            }
        }
        this.unlockSilentMode();
        return this.ctx;
    },

    init() {
        this.ensureRunning();
        if (this.ctx && !this.noiseBuf) {
            const sr = this.ctx.sampleRate;
            this.noiseBuf = this.ctx.createBuffer(1, sr * 2.0, sr);
            const data = this.noiseBuf.getChannelData(0);
            for (let i = 0; i < data.length; i++) data[i] = Math.random() * 2 - 1;
        }
        if (this.ctx && !this.munchBuffer) {
            this.buildMunchBuffer();
        }
        if (!this.animalPreloadStarted) {
            this.animalPreloadStarted = true;
            this.preloadAnimalSounds();
        }
        if (!this.thingPreloadStarted) {
            this.thingPreloadStarted = true;
            this.preloadThingAndCrunchSounds();
        }
    },

    preloadThingAndCrunchSounds() {
        if (!this.ctx || typeof REAL_THING_SFX === 'undefined') return;
        Object.entries(REAL_THING_SFX).forEach(([id, dataUri]) => {
            if (this.thingBuffers.has(id)) return;
            fetch(dataUri)
                .then(r => r.arrayBuffer())
                .then(ab => this.ctx.decodeAudioData(ab))
                .then(dec => this.thingBuffers.set(id, dec))
                .catch(() => {});
        });
        if (typeof REAL_CRUNCH_SFX !== 'undefined') {
            REAL_CRUNCH_SFX.forEach((dataUri, idx) => {
                fetch(dataUri)
                    .then(r => r.arrayBuffer())
                    .then(ab => this.ctx.decodeAudioData(ab))
                    .then(dec => { this.crunchBuffers[idx] = dec; })
                    .catch(() => {});
            });
        }
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

        this.thingReqId++;

        if (typeof animalGame !== 'undefined' && animalGame.speechTimer) {
            clearTimeout(animalGame.speechTimer);
            animalGame.speechTimer = null;
        }
        if (typeof thingsGame !== 'undefined' && thingsGame.speechTimer) {
            clearTimeout(thingsGame.speechTimer);
            thingsGame.speechTimer = null;
        }
        if (typeof foodGame !== 'undefined') {
            if (foodGame.cheerTimer) { clearTimeout(foodGame.cheerTimer); foodGame.cheerTimer = null; }
            if (foodGame.finalChimeTimer) { clearTimeout(foodGame.finalChimeTimer); foodGame.finalChimeTimer = null; }
            if (foodGame.finalSpeechTimer) { clearTimeout(foodGame.finalSpeechTimer); foodGame.finalSpeechTimer = null; }
        }
        if (typeof numberGame !== 'undefined' && numberGame.completionTimer) {
            clearTimeout(numberGame.completionTimer);
            numberGame.completionTimer = null;
        }
        if (typeof quizGame !== 'undefined' && quizGame.speechFollowupTimer) {
            clearTimeout(quizGame.speechFollowupTimer);
            quizGame.speechFollowupTimer = null;
        }
        if (typeof phonicsGame !== 'undefined' && phonicsGame.bubbleSpeechTimer) {
            clearTimeout(phonicsGame.bubbleSpeechTimer);
            phonicsGame.bubbleSpeechTimer = null;
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
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return 550;
        try {
            this.init();
            if (!this.ctx) return 550;

            const validBuffers = (this.crunchBuffers || []).filter(Boolean);
            if (validBuffers.length > 0) {
                const now = this.ctx.currentTime;
                const buf = validBuffers[Math.floor(Math.random() * validBuffers.length)];
                const src = this.ctx.createBufferSource();
                src.buffer = buf;
                const rate = 0.95 + Math.random() * 0.11; // 0.95 - 1.06
                src.playbackRate.value = rate;
                const gain = this.ctx.createGain();
                gain.gain.setValueAtTime(0.95, now);
                src.connect(gain);
                gain.connect(this.ctx.destination);
                this.trackNode(src);
                src.start(now);
                return Math.round((buf.duration / rate) * 1000);
            }

            if (this.munchBuffer) {
                const now = this.ctx.currentTime;
                const src = this.ctx.createBufferSource();
                src.buffer = this.munchBuffer;
                const gain = this.ctx.createGain();
                gain.gain.setValueAtTime(0.9, now);
                src.connect(gain);
                gain.connect(this.ctx.destination);
                this.trackNode(src);
                src.start(now);
                return 520;
            }
        } catch (e) {}
        return 520;
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
            gain1.gain.setValueAtTime(0.12, t0);
            gain1.gain.exponentialRampToValueAtTime(0.001, t0 + 0.24);
            osc1.connect(gain1);
            gain1.connect(this.ctx.destination);
            this.trackNode(osc1);
            osc1.start(t0);
            osc1.stop(t0 + 0.26);

            const osc2 = this.ctx.createOscillator();
            const gain2 = this.ctx.createGain();
            osc2.type = 'sine';
            osc2.frequency.setValueAtTime(baseFreq * 4, t0);
            gain2.gain.setValueAtTime(0.03, t0);
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
        if (typeof app !== 'undefined' && app.settings && !app.settings.sfxEnabled) return 800;
        this.init();
        if (!this.ctx) return 800;

        const reqToken = ++this.thingReqId;
        const buf = this.thingBuffers.get(id);

        if (buf) {
            try {
                const now = this.ctx.currentTime;
                const src = this.ctx.createBufferSource();
                src.buffer = buf;
                const gain = this.ctx.createGain();
                gain.gain.setValueAtTime(0.92, now);
                src.connect(gain);
                gain.connect(this.ctx.destination);
                this.trackNode(src);
                src.start(now);
                return Math.round(buf.duration * 1000);
            } catch (e) {}
        } else if (typeof REAL_THING_SFX !== 'undefined' && REAL_THING_SFX[id]) {
            fetch(REAL_THING_SFX[id])
                .then(r => r.arrayBuffer())
                .then(ab => this.ctx.decodeAudioData(ab))
                .then(dec => {
                    this.thingBuffers.set(id, dec);
                    if (reqToken === this.thingReqId && app.currentView === 'things') {
                        const now = this.ctx.currentTime;
                        const src = this.ctx.createBufferSource();
                        src.buffer = dec;
                        const gain = this.ctx.createGain();
                        gain.gain.setValueAtTime(0.92, now);
                        src.connect(gain);
                        gain.connect(this.ctx.destination);
                        this.trackNode(src);
                        src.start(now);
                    }
                })
                .catch(() => this.playThingSynth(id));
            return 1200;
        }

        return this.playThingSynth(id);
    },

    playThingSynth(id) {
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
    phonicsDetail: 'full',    // 'full' ("A! A says ah! ah, Apple!") or 'simple' ("A! Apple!")
    minimizeMenuHeader: false, // Minimize upper title banner on Main Menu to just show cards
    showSolarCredits: false,  // Display NASA telescope & mission source badge on Solar System photos
    dragSpeed: 'normal'       // 1-finger drag sensitivity for shapes, visuals & 3D models ('slow': 0.55x, 'normal': 1.0x, 'fast': 1.75x)
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
    solar: 'Solar System!',
    blocks: 'Number Blocks!'
};

const app = {
    currentView: 'menu',
    currentUtterance: null,
    speechTimeout: null,
    cachedVoice: null,
    speechToken: 0,
    _speechWarmedUp: false,
    settings: (() => {
        try {
            const saved = localStorage.getItem('tlh_isolated_v3_settings');
            if (saved) return Object.assign({}, DEFAULT_SETTINGS, JSON.parse(saved));
        } catch (e) {}
        return Object.assign({}, DEFAULT_SETTINGS);
    })(),
    isOpeningView: false,
    pendingGameIntro: null,

    getDragSpeedMultiplier() {
        const s = this.settings ? this.settings.dragSpeed : 'normal';
        if (s === 'slow') return 0.55;
        if (s === 'fast') return 1.75;
        return 1.0;
    },

    applySolarCreditsState() {
        const show = !!(this.settings && this.settings.showSolarCredits);
        const creditEl = document.getElementById('solar-photo-credit');
        if (creditEl) {
            creditEl.classList.toggle('hidden', !show);
        }
        const optCredits = document.getElementById('opt-solar-credits');
        if (optCredits) optCredits.checked = show;
    },

    applyMenuHeaderState() {
        const isMin = !!(this.settings && this.settings.minimizeMenuHeader);
        const banner = document.getElementById('menu-header-banner');
        if (banner) banner.classList.toggle('hidden', isMin);
        const topContainer = document.getElementById('menu-top-container');
        if (topContainer) {
            if (isMin) {
                topContainer.classList.remove('pt-5', 'pb-2', 'pt-4');
                topContainer.classList.add('pt-2', 'pb-1');
            } else {
                topContainer.classList.remove('pt-2', 'pb-1');
                topContainer.classList.add('pt-4', 'pb-2');
            }
        }
        const icon = document.getElementById('menu-minimize-icon');
        const label = document.getElementById('menu-minimize-label');
        if (icon) icon.textContent = isMin ? '🔽' : '🔼';
        if (label) label.textContent = isMin ? 'Show Title' : 'Minimize';
        const optToggle = document.getElementById('opt-minimize-header');
        if (optToggle) optToggle.checked = isMin;
    },

    saveSettings() {
        try {
            localStorage.setItem('tlh_isolated_v3_settings', JSON.stringify(this.settings));
        } catch (e) {}
        if (typeof this.applyMenuHeaderState === 'function') {
            this.applyMenuHeaderState();
        }
        if (typeof this.applySolarCreditsState === 'function') {
            this.applySolarCreditsState();
        }
        if (typeof numberGame !== 'undefined' && numberGame.applyMaxNumberSetting) {
            numberGame.applyMaxNumberSetting();
        }
        if (typeof updateVoiceStatusIndicator === 'function') {
            updateVoiceStatusIndicator();
        }
        if (window.NumberBlocks && window.NumberBlocks.Game && window.NumberBlocks.Game.applySettings) {
            window.NumberBlocks.Game.applySettings();
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

    updateViewportTheme(viewName) {
        let themeColor = '#bae6fd';
        if (viewName === 'solar') {
            themeColor = '#020617';
        } else if (viewName === 'shapes3d') {
            themeColor = '#090d16';
        } else if (viewName === 'blocks' || viewName === 'menu') {
            themeColor = '#bae6fd';
        } else {
            themeColor = '#e0f2fe';
        }
        const metaTheme = document.querySelector('meta[name="theme-color"]');
        if (metaTheme) metaTheme.setAttribute('content', themeColor);
        document.documentElement.style.backgroundColor = themeColor;
        document.body.style.backgroundColor = themeColor;
        if (viewName === 'solar' || viewName === 'shapes3d') {
            document.body.style.backgroundImage = 'none';
        } else {
            document.body.style.backgroundImage = '';
        }
    },

    goHome() {
        this.switchView('menu');
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

        if (typeof zoomController !== 'undefined') {
            zoomController.resetZoom();
        }

        this.speechToken++;
        geminiTTS.stop();
        soundFX.stopAll();
        document.querySelectorAll('.view-section').forEach(el => el.classList.remove('active-view'));
        if (this.currentView === 'letters' && typeof phonicsGame !== 'undefined') phonicsGame.stopBubbles();
        if (this.currentView === 'shapes3d' && typeof shapes3DGame !== 'undefined') shapes3DGame.stop();
        if (this.currentView === 'solar' && typeof solarGame !== 'undefined') solarGame.stop();
        if (this.currentView === 'numbers' && typeof numberGame !== 'undefined') numberGame.clearAutoTimers();
        if (this.currentView === 'blocks' && window.NumberBlocks && window.NumberBlocks.Game) window.NumberBlocks.Game.stop();

        const target = document.getElementById(`view-${viewName}`);
        if (target) target.classList.add('active-view');
        this.currentView = viewName;
        this.updateViewportTheme(viewName);

        if (viewName === 'menu') {
            this.pendingGameIntro = null;
            this.isOpeningView = false;
            this.applyMenuHeaderState();
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
        else if (viewName === 'blocks' && window.NumberBlocks && window.NumberBlocks.Game) window.NumberBlocks.Game.open();

        this.isOpeningView = false;
        this.pendingGameIntro = null;
        geminiTTS.warmUpView(viewName);
    },

    speak(text, onStartCallback = null, onEndCallback = null) {
        const token = ++this.speechToken;
        let endFired = false;
        let fallbackTimer = null;

        const fireEnd = () => {
            if (fallbackTimer) {
                clearTimeout(fallbackTimer);
                fallbackTimer = null;
            }
            if (endFired) return;
            if (token !== this.speechToken) return;
            endFired = true;
            if (typeof onEndCallback === 'function') {
                try { onEndCallback(); } catch (e) {}
            }
        };

        if (!this.settings.voiceEnabled || (this.isOpeningView && !this.settings.announceGameOnOpen)) {
            this.pendingGameIntro = null;
            setTimeout(fireEnd, 0);
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
        if (!clean) {
            setTimeout(fireEnd, 0);
            return;
        }

        geminiTTS.stop();
        if (this.speechTimeout) {
            clearTimeout(this.speechTimeout);
            this.speechTimeout = null;
        }

        const rate = this.getSpeechRateValue() || 1.0;
        const wordCount = clean.split(/\s+/).filter(Boolean).length;
        const estMs = Math.min(6000, 700 + Math.round((wordCount * 420) / rate));

        const key = getApiKey();
        const cacheKey = `${getTtsModel()}:${getTtsVoice()}:${clean}`;
        const isCached = key && geminiTTS.hasCached(cacheKey);
        const canUseGemini = key && (!geminiTTS.isCoolingDown() || isCached);

        // Priority yield: if toddler triggers live uncached speech, yield background pre-caching
        if (key && !isCached && typeof precacheManager !== 'undefined' && precacheManager.state === 'running') {
            precacheManager.yieldForInteractive(8500);
        }

        if (canUseGemini) {
            const onGeminiStart = (durSec) => {
                if (token !== this.speechToken) return;
                if (typeof onStartCallback === 'function') {
                    try { onStartCallback(); } catch (e) {}
                }
                const waitMs = (durSec && durSec > 0)
                    ? Math.round((durSec / rate) * 1000) + 250
                    : estMs;
                fallbackTimer = setTimeout(fireEnd, waitMs);
            };

            const onGeminiEnd = () => {
                fireEnd();
            };

            geminiTTS.play(clean, getTtsModel(), getTtsVoice(), key, onGeminiStart, onGeminiEnd).catch((err) => {
                console.warn('Gemini TTS fallback to Device Voice:', err);
                if (token === this.speechToken && !endFired) {
                    if (fallbackTimer) { clearTimeout(fallbackTimer); fallbackTimer = null; }
                    this.speakDeviceVoice(clean, onStartCallback, onEndCallback, token, fireEnd);
                }
            });
        } else {
            this.speakDeviceVoice(clean, onStartCallback, onEndCallback, token, fireEnd);
        }
    },

    speakDeviceVoice(cleanText, onStartCallback = null, onEndCallback = null, speechToken = null, existingFireEnd = null) {
        const token = speechToken !== null ? speechToken : ++this.speechToken;
        let endFired = false;
        let fallbackTimer = null;

        const fireEnd = existingFireEnd || (() => {
            if (fallbackTimer) {
                clearTimeout(fallbackTimer);
                fallbackTimer = null;
            }
            if (endFired) return;
            if (token !== this.speechToken) return;
            endFired = true;
            if (typeof onEndCallback === 'function') {
                try { onEndCallback(); } catch (e) {}
            }
        });

        try {
            if (!this.settings.voiceEnabled || !('speechSynthesis' in window)) {
                setTimeout(fireEnd, 0);
                return;
            }

            if (window.speechSynthesis.paused) {
                try { window.speechSynthesis.resume(); } catch (e) {}
            }
            if (window.speechSynthesis.speaking || window.speechSynthesis.pending) {
                try {
                    window.speechSynthesis.cancel();
                } catch(e){}
            }

            if (!this.cachedVoice) this.initVoices();

            const msg = new SpeechSynthesisUtterance(cleanText);
            const rate = this.getSpeechRateValue() || 1.0;
            msg.rate = rate;
            msg.pitch = 1.05;
            if (this.cachedVoice) msg.voice = this.cachedVoice;

            let started = false;
            const triggerStart = () => {
                if (token !== this.speechToken) return;
                if (!started) {
                    started = true;
                    if (typeof onStartCallback === 'function') {
                        try { onStartCallback(); } catch (e) {}
                    }
                }
            };

            const wordCount = cleanText.split(/\s+/).filter(Boolean).length;
            const estMs = Math.min(6000, 700 + Math.round((wordCount * 420) / rate));
            fallbackTimer = setTimeout(fireEnd, estMs);

            msg.onstart = () => {
                if (token !== this.speechToken) return;
                app.setSpeakingUI(true);
                triggerStart();
            };
            msg.onend = () => {
                app.setSpeakingUI(false);
                app.currentUtterance = null;
                fireEnd();
            };
            msg.onerror = (e) => {
                app.setSpeakingUI(false);
                app.currentUtterance = null;
                if (e && (e.error === 'canceled' || e.error === 'interrupted')) {
                    return;
                }
                fireEnd();
            };

            this.currentUtterance = msg;
            this._speechWarmedUp = true;
            window.speechSynthesis.speak(msg);
            setTimeout(triggerStart, 60);
        } catch (e) {
            app.setSpeakingUI(false);
            fireEnd();
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

const DEG2RAD = Math.PI / 180;
const RAD2DEG = 180 / Math.PI;

// JPL Table 1 Keplerian Elements (Valid 1800-2050 AD)
const JPL_KEPLER_TABLE = {
    Mercury: {
        a0: 0.38709927, aDot: 0.00000037,
        e0: 0.20563593, eDot: 0.00001906,
        I0: 7.00497902, IDot: -0.00594749,
        L0: 252.25032350, LDot: 149472.67411175,
        peri0: 77.45779628, periDot: 0.16047689,
        node0: 48.33076593, nodeDot: -0.12534081
    },
    Venus: {
        a0: 0.72333566, aDot: 0.00000390,
        e0: 0.00677672, eDot: -0.00004107,
        I0: 3.39467605, IDot: -0.00078890,
        L0: 181.97909950, LDot: 58517.81538729,
        peri0: 131.60246718, periDot: 0.00268329,
        node0: 76.67984255, nodeDot: -0.27769418
    },
    Earth: { // Earth/Moon Barycenter
        a0: 1.00000261, aDot: 0.00000562,
        e0: 0.01671123, eDot: -0.00004392,
        I0: -0.00001531, IDot: -0.01294668,
        L0: 100.46457166, LDot: 35999.37244981,
        peri0: 102.93768193, periDot: 0.32327364,
        node0: 0.0, nodeDot: 0.0
    },
    Mars: {
        a0: 1.52371034, aDot: 0.00001847,
        e0: 0.09339410, eDot: 0.00007882,
        I0: 1.84969142, IDot: -0.00813131,
        L0: -4.55343205, LDot: 19140.30268499,
        peri0: -23.94362959, periDot: 0.44441088,
        node0: 49.55953891, nodeDot: -0.29257343
    },
    Jupiter: {
        a0: 5.20288700, aDot: -0.00011607,
        e0: 0.04838624, eDot: -0.00013253,
        I0: 1.30439695, IDot: -0.00183714,
        L0: 34.39644051, LDot: 3034.74612775,
        peri0: 14.72847983, periDot: 0.21252668,
        node0: 100.47390909, nodeDot: 0.20469106
    },
    Saturn: {
        a0: 9.53667594, aDot: -0.00125060,
        e0: 0.05386179, eDot: -0.00050991,
        I0: 2.48599187, IDot: 0.00193609,
        L0: 49.95424423, LDot: 1222.49362201,
        peri0: 92.59887831, periDot: -0.41897216,
        node0: 113.66242448, nodeDot: -0.28867794
    },
    Uranus: {
        a0: 19.18916464, aDot: -0.00196176,
        e0: 0.04725744, eDot: -0.00004397,
        I0: 0.77263783, IDot: -0.00242939,
        L0: 313.23810451, LDot: 428.48202785,
        peri0: 170.95427630, periDot: 0.40805281,
        node0: 74.01692503, nodeDot: 0.04240589
    },
    Neptune: {
        a0: 30.06992276, aDot: 0.00026291,
        e0: 0.00859048, eDot: 0.00005105,
        I0: 1.77004347, IDot: 0.00035372,
        L0: -55.12002969, LDot: 218.45945325,
        peri0: 44.96476227, periDot: -0.32241464,
        node0: 131.78422574, nodeDot: -0.00508664
    },
    Pluto: {
        a0: 39.48168677, aDot: -0.00076912,
        e0: 0.24880766, eDot: 0.00006465,
        I0: 17.14175, IDot: 0.003075,
        L0: 238.92881, LDot: 145.20775,
        peri0: 224.06676, periDot: -0.03673611,
        node0: 110.30347, nodeDot: -0.01036944
    }
};

const solarEphemeris = {
    heliocentricLongitude(planetId, date) {
        const el = JPL_KEPLER_TABLE[planetId];
        if (!el) return 0;
        const d = (date instanceof Date) ? date : new Date(date);
        const jd = (d.getTime() / 86400000) + 2440587.5;
        const T = (jd - 2451545.0) / 36525.0;

        const a = el.a0 + el.aDot * T;
        const e = el.e0 + el.eDot * T;
        const I = (el.I0 + el.IDot * T) * DEG2RAD;
        const L = ((el.L0 + el.LDot * T) % 360 + 360) % 360;
        const peri = ((el.peri0 + el.periDot * T) % 360 + 360) % 360;
        const node = ((el.node0 + el.nodeDot * T) % 360 + 360) % 360;

        let M = (L - peri) % 360;
        if (M < -180) M += 360;
        if (M > 180) M -= 360;
        const M_rad = M * DEG2RAD;

        let E = M_rad + e * Math.sin(M_rad);
        for (let iter = 0; iter < 12; iter++) {
            const dM = M_rad - (E - e * Math.sin(E));
            const dE = dM / (1 - e * Math.cos(E));
            E += dE;
            if (Math.abs(dE) < 1e-9) break;
        }

        const x_prime = a * (Math.cos(E) - e);
        const y_prime = a * Math.sqrt(Math.max(0, 1 - e * e)) * Math.sin(E);

        const omega = (peri - node) * DEG2RAD;
        const node_rad = node * DEG2RAD;

        const cosNode = Math.cos(node_rad), sinNode = Math.sin(node_rad);
        const cosOmega = Math.cos(omega), sinOmega = Math.sin(omega);
        const cosI = Math.cos(I);

        const Px = cosOmega * cosNode - sinOmega * sinNode * cosI;
        const Py = cosOmega * sinNode + sinOmega * cosNode * cosI;
        const Qx = -sinOmega * cosNode - cosOmega * sinNode * cosI;
        const Qy = -sinOmega * sinNode + cosOmega * cosNode * cosI;

        const x = x_prime * Px + y_prime * Qx;
        const y = x_prime * Py + y_prime * Qy;

        let lambda = Math.atan2(y, x);
        if (lambda < 0) lambda += Math.PI * 2;
        return lambda;
    }
};

const solarGame = {
    mode: 'photo',
    current: GAMES.solar[0],
    scene: null, camera: null, renderer: null, rootGroup: null,
    orbitEntries: [], animId: null, isDragging: false,
    prevX: 0, prevY: 0, velX: 0.011, velY: 0.002, turboBoost: 1,
    textureCache: new Map(),
    simDate: new Date(),
    isPlaying: true,
    orbitSpeed: 1.0,
    earthMoonPivot: null,
    animatingDate: false,
    dateAnimStart: 0,
    dateAnimDuration: 900,
    dateAnimFrom: new Map(),
    dateAnimTo: new Map(),

    stepBody(delta) {
        const idx = GAMES.solar.findIndex(s => s.id === this.current.id);
        const nextIdx = (idx + delta + GAMES.solar.length) % GAMES.solar.length;
        this.select(GAMES.solar[nextIdx], true);
        const activeBtn = document.querySelector('#solar-controls .tray-btn.selected');
        if (activeBtn) {
            activeBtn.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
        }
    },

    setOrbitSpeed(mult) {
        const val = Math.max(0.25, Math.min(10, Math.round(mult * 100) / 100));
        this.orbitSpeed = val;
        const btn = document.getElementById('solar-speed-btn');
        if (btn) btn.textContent = `⚡ ${val}x`;
        const slider = document.getElementById('solar-speed-slider');
        if (slider) slider.value = String(val);
        const badge = document.getElementById('solar-orbit-summary-badge');
        if (badge) badge.textContent = `${val}x`;

        document.querySelectorAll('.solar-speed-preset').forEach(presetBtn => {
            const spd = parseFloat(presetBtn.dataset.speed);
            const isActive = Math.abs(spd - val) < 0.05;
            presetBtn.classList.toggle('bg-amber-400', isActive);
            presetBtn.classList.toggle('text-slate-950', isActive);
            presetBtn.classList.toggle('border-amber-300', isActive);
            presetBtn.classList.toggle('bg-slate-900/80', !isActive);
            presetBtn.classList.toggle('text-slate-200', !isActive);
            presetBtn.classList.toggle('border-slate-600/80', !isActive);
        });
    },

    open() {
        document.getElementById('solar-orbit-drawer')?.classList.add('hidden');
        document.getElementById('solar-date-popover')?.classList.add('hidden');
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
        this.camera.position.z = this.mode === 'orbit' ? 12.5 : 7.4;

        this.renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        this.renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
        const canvas = this.renderer.domElement;
        canvas.style.width = '100%';
        canvas.style.height = '100%';
        canvas.style.display = 'block';
        container.appendChild(canvas);

        const updateSize = () => {
            const w = container.clientWidth || 256;
            const h = container.clientHeight || 256;
            this.renderer.setSize(w, h, false);
            this.camera.aspect = w / h;
            this.camera.updateProjectionMatrix();
        };
        updateSize();

        if (window.ResizeObserver) {
            this.resizeObserver = new ResizeObserver(() => updateSize());
            this.resizeObserver.observe(container);
        }

        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);

        container.addEventListener('pointerdown', e => {
            if (this.mode === 'orbit') {
                document.getElementById('solar-orbit-drawer')?.classList.add('hidden');
                document.getElementById('solar-date-popover')?.classList.add('hidden');
            }
            if (typeof zoomController !== 'undefined' && (zoomController.isPinching || zoomController.isDragging1Finger)) return;
            this.isDragging = false;
            this.pointerDownX = e.clientX;
            this.pointerDownY = e.clientY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
        });

        container.addEventListener('pointermove', e => {
            if (typeof zoomController !== 'undefined' && (zoomController.isPinching || zoomController.isDragging1Finger || zoomController.isLongPressActive)) {
                this.isDragging = false;
                return;
            }
            const dist = Math.hypot(e.clientX - (this.pointerDownX || e.clientX), e.clientY - (this.pointerDownY || e.clientY));
            if (!this.isDragging) {
                if (dist > 8) {
                    this.isDragging = true;
                    try { container.setPointerCapture(e.pointerId); } catch (err) {}
                } else {
                    return;
                }
            }
            if (!this.rootGroup) return;
            const dx = e.clientX - this.prevX;
            const dy = e.clientY - this.prevY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            const dragMult = typeof app !== 'undefined' ? app.getDragSpeedMultiplier() : 1.0;
            this.velX = dx * 0.014 * dragMult;
            this.velY = dy * 0.014 * dragMult;
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
            // Rich realistic continent texture delegated from getEarthTexture with soft polar caps
            const tex = (typeof getEarthTexture === 'function') ? getEarthTexture() : new THREE.CanvasTexture(cvs);
            this.textureCache.set(id, tex);
            return tex;
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
            // Polar caps (soft natural elliptical ice caps with zero harsh rectangular white bars)
            ctx.fillStyle = 'rgba(255, 255, 255, 0.75)';
            ctx.beginPath(); ctx.ellipse(256, 4, 180, 7, 0, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.ellipse(256, 252, 180, 7, 0, 0, Math.PI * 2); ctx.fill();
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

        // Item 9e: Exclude Moon from Sun's orbits (attaches to Earth)
        const planets = GAMES.solar.filter(p => p.id !== 'The Sun' && p.id !== "Earth's Moon" && p.id !== 'Asteroid Belt' && p.id !== 'Comet' && p.id !== 'Galactic Swirl');
        const rScale = 0.55;
        this.earthMoonPivot = null;

        planets.forEach((p, idx) => {
            const radius = 1.0 + idx * 0.44;

            // Orbit ring line
            const ring = new THREE.Mesh(
                new THREE.RingGeometry(radius - 0.015, radius + 0.015, 64),
                new THREE.MeshBasicMaterial({ color: p.id === this.current.id ? '#facc15' : '#334155', side: THREE.DoubleSide })
            );
            ring.rotation.x = Math.PI / 2;
            group.add(ring);

            // Orbiting planet pivot
            const pivot = new THREE.Group();
            const initialLambda = solarEphemeris.heliocentricLongitude(p.id, this.simDate);
            pivot.rotation.y = initialLambda;
            const pSize = Math.max(0.12, p.orbitSize * rScale);
            const pMesh = new THREE.Mesh(new THREE.SphereGeometry(pSize, 18, 18), new THREE.MeshStandardMaterial({ color: p.color }));
            pMesh.position.x = radius;

            // Saturn mini-rings in orbit mode
            if (p.id === 'Saturn') {
                const sRing = new THREE.Mesh(new THREE.RingGeometry(pSize * 1.3, pSize * 2.1, 24), new THREE.MeshBasicMaterial({ color: 0xfef08a, side: THREE.DoubleSide, transparent: true, opacity: 0.8 }));
                sRing.rotation.x = Math.PI / 2.4;
                pMesh.add(sRing);
            }

            // Earth's Moon: attached directly to Earth's mesh (Item 9e)
            if (p.id === 'Earth') {
                const moonPivot = new THREE.Group();
                const moonMesh = new THREE.Mesh(
                    new THREE.SphereGeometry(Math.max(0.06, pSize * 0.35), 14, 14),
                    new THREE.MeshStandardMaterial({ color: '#e2e8f0', roughness: 0.6 })
                );
                moonMesh.position.x = pSize * 1.85;
                moonPivot.add(moonMesh);
                pMesh.add(moonPivot);
                this.earthMoonPivot = moonPivot;
            }

            pivot.add(pMesh);
            group.add(pivot);
            this.orbitEntries.push({ planetId: p.id, pivot, speed: p.orbitSpeed });
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
        document.getElementById('solar-orbit-drawer')?.classList.add('hidden');
        document.getElementById('solar-date-popover')?.classList.add('hidden');
        if (typeof zoomController !== 'undefined') {
            zoomController.resetZoom();
        }
        if (this.camera) {
            this.camera.position.z = newMode === 'orbit' ? 12.5 : 7.4;
            this.camera.updateProjectionMatrix();
        }
        const orbitControls = document.getElementById('solar-orbit-controls');
        if (orbitControls) orbitControls.classList.toggle('hidden', newMode !== 'orbit');
        const headerRow = document.getElementById('solar-header-row');
        if (headerRow) headerRow.classList.toggle('hidden', newMode === 'orbit');
        if (newMode === 'orbit') {
            this.simDate = new Date();
            this.isPlaying = true;
            this.updateOrbitDateUI();
            this.setOrbitSpeed(this.orbitSpeed || 1.0);
        }
        document.getElementById('solar-mode-photo').classList.toggle('active', newMode === 'photo');
        document.getElementById('solar-mode-planet').classList.toggle('active', newMode === 'planet');
        document.getElementById('solar-mode-orbit').classList.toggle('active', newMode === 'orbit');
        document.getElementById('solar-action-label').textContent = newMode === 'orbit' ? '🚀 Turbo Orbit!' : '🔊 Fun Fact!';
        this.select(this.current, false);
    },

    updateOrbitDateUI() {
        const d = this.simDate;
        const input = document.getElementById('solar-date-input');
        if (input) {
            const yr = d.getFullYear();
            const mo = String(d.getMonth() + 1).padStart(2, '0');
            const da = String(d.getDate()).padStart(2, '0');
            input.value = `${yr}-${mo}-${da}`;
        }
        const label = document.getElementById('solar-date-label');
        if (label) {
            label.textContent = d.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        }
        this.updatePlayPauseUI();
    },

    updatePlayPauseUI() {
        const icon = document.getElementById('solar-play-icon');
        const label = document.getElementById('solar-play-label');
        const qIcon = document.getElementById('solar-quick-play-icon');
        const qLabel = document.getElementById('solar-quick-play-label');
        if (this.isPlaying) {
            if (icon) icon.textContent = '⏸';
            if (label) label.textContent = 'Pause';
            if (qIcon) qIcon.textContent = '⏸';
            if (qLabel) qLabel.textContent = 'Playing';
        } else {
            if (icon) icon.textContent = '▶';
            if (label) label.textContent = 'Play';
            if (qIcon) qIcon.textContent = '▶';
            if (qLabel) qLabel.textContent = 'Paused';
        }
    },

    togglePlayPause() {
        this.isPlaying = !this.isPlaying;
        this.updatePlayPauseUI();
    },

    goToDate(targetDate, speakAnnouncement = true) {
        const d = (targetDate instanceof Date) ? targetDate : new Date(targetDate);
        if (isNaN(d.getTime())) return;
        this.isPlaying = false;
        this.simDate = d;
        this.updateOrbitDateUI();

        this.dateAnimFrom.clear();
        this.dateAnimTo.clear();
        this.orbitEntries.forEach(entry => {
            this.dateAnimFrom.set(entry.planetId, entry.pivot.rotation.y);
            const targetLambda = solarEphemeris.heliocentricLongitude(entry.planetId, d);
            this.dateAnimTo.set(entry.planetId, targetLambda);
        });
        this.dateAnimStart = performance.now();
        this.animatingDate = true;

        if (speakAnnouncement) {
            const dateStr = d.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
            const isFuture = d > new Date();
            app.speak(`Here is where the planets ${isFuture ? 'will be' : 'were'} on ${dateStr}!`);
        }
    },

    jumpToday() {
        this.goToDate(new Date(), false);
        this.isPlaying = true;
        this.updateOrbitDateUI();
        app.speak("Back to today's planet positions!");
    },

    select(item, speak = true) {
        this.current = item;
        document.getElementById('solar-order-badge').textContent = item.badge;
        document.getElementById('solar-title').textContent = item.id;
        document.getElementById('solar-fact').textContent = item.fact;

        document.querySelectorAll('#solar-controls .tray-btn').forEach(b => {
            const isSel = b.dataset.solarId === item.id;
            b.classList.toggle('selected', isSel);
            if (isSel) {
                b.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
            }
        });

        const photoContainer = document.getElementById('solar-photo-container');
        const canvasContainer = document.getElementById('solar-canvas-container');

        if (this.mode === 'photo') {
            this.stop();
            photoContainer.classList.remove('hidden');
            canvasContainer.classList.add('hidden');
            const holder = document.getElementById('solar-svg-holder');
            holder.innerHTML = '';
            const img = document.createElement('img');
            img.src = item.photoUrl;
            img.alt = item.id;
            const fitMode = (item.id === 'Saturn' || item.id === 'Comet') ? 'object-contain' : 'object-cover';
            img.className = `w-full h-full ${fitMode} rounded-2xl drop-shadow-xl transition-all duration-300`;
            img.addEventListener('error', () => {
                holder.innerHTML = getSolarSVG(item.id, 'fallback_stage');
            }, { once: true });
            holder.appendChild(img);
            document.getElementById('solar-photo-credit').textContent = item.credit;
            if (typeof app !== 'undefined' && app.applySolarCreditsState) {
                app.applySolarCreditsState();
            }
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
                    if (this.animatingDate) {
                        const now = performance.now();
                        const p = Math.min(1.0, (now - this.dateAnimStart) / this.dateAnimDuration);
                        const eased = p < 0.5 ? 4 * p * p * p : 1 - Math.pow(-2 * p + 2, 3) / 2;
                        this.orbitEntries.forEach(entry => {
                            const from = this.dateAnimFrom.get(entry.planetId) || 0;
                            const to = this.dateAnimTo.get(entry.planetId) || 0;
                            let diff = (to - from) % (Math.PI * 2);
                            if (diff < -Math.PI) diff += Math.PI * 2;
                            if (diff > Math.PI) diff -= Math.PI * 2;
                            entry.pivot.rotation.y = from + diff * eased;
                        });
                        if (p >= 1.0) {
                            this.animatingDate = false;
                        }
                    } else if (this.isPlaying) {
                        const advanceDays = 4 * (this.orbitSpeed || 1.0) * this.turboBoost;
                        this.simDate.setTime(this.simDate.getTime() + advanceDays * 86400000);
                        this.orbitEntries.forEach(entry => {
                            entry.pivot.rotation.y = solarEphemeris.heliocentricLongitude(entry.planetId, this.simDate);
                        });
                        const popover = document.getElementById('solar-date-popover');
                        if (popover && !popover.classList.contains('hidden')) {
                            this.updateOrbitDateUI();
                        }
                    }
                    if (this.earthMoonPivot) {
                        this.earthMoonPivot.rotation.y += 0.05 * (this.orbitSpeed || 1.0) * this.turboBoost;
                    }
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
        document.getElementById('solar-orbit-drawer')?.classList.add('hidden');
        document.getElementById('solar-date-popover')?.classList.add('hidden');
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
        if (typeof zoomController !== 'undefined') {
            zoomController.resetZoom();
        }
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

            wCard.innerHTML = `<span class="text-4xl sm:text-5xl mb-0.5">${wObj.e}</span><span class="font-black text-slate-800 text-xs sm:text-base truncate max-w-full text-center">${formattedWord}</span>`;
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
                    this.bubbleSpeechTimer = soundFX.registerTimer(setTimeout(() => {
                        app.speak(`Yay! ${pData.letter} says ${pData.soundSpell}! ${pData.words[0].w}!`);
                        this.bubbleSpeechTimer = null;
                    }, 350));
                    b.style.transform = 'scale(1.35)';
                    b.style.opacity = '0';
                    this.bubbleTimer = setTimeout(() => this.nextBubbleTarget(), 1250);
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
                    soundFX.playCheer();
                    this.completionTimer = soundFX.registerTimer(setTimeout(() => {
                        app.speak(`${myCount}! Yay! ${numData.word} ${numData.item}!`);
                        this.completionTimer = null;
                    }, 350));
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
            this.prefetchNumbers(numData.num);
        } else {
            instrEl.textContent = `Tap each ${numData.emoji} to count! (0/${numData.num})`;
            if (speakIntro) app.speak(`${numData.word}! Tap to count to ${numData.num}!`);
        }
    },

    autoSeqToken: 0,
    completionTimer: null,

    prefetchNumbers(maxN) {
        const key = getApiKey();
        if (!key || geminiTTS.isCoolingDown()) return;
        const model = getTtsModel();
        const voice = getTtsVoice();
        let i = 1;
        const loadNext = async () => {
            if (i > maxN || app.currentView !== 'numbers') return;
            const word = String(i);
            const cacheKey = `${model}:${voice}:${word}`;
            if (geminiTTS.hasCached(cacheKey) && !geminiTTS.memCache.has(cacheKey)) {
                try {
                    const buf = await ttsDB.get(cacheKey);
                    if (buf) {
                        geminiTTS.memCache.set(cacheKey, buf);
                        if (soundFX.ctx && !geminiTTS.decodedCache.has(cacheKey)) {
                            soundFX.ctx.decodeAudioData(buf.slice(0)).then(ab => geminiTTS.decodedCache.set(cacheKey, ab)).catch(() => {});
                        }
                    }
                } catch (e) {}
            }
            i++;
            setTimeout(loadNext, 40);
        };
        loadNext();
    },

    clearAutoTimers() {
        this.autoSeqToken++;
        this.autoTimers.forEach(t => clearTimeout(t));
        this.autoTimers = [];
        if (this.completionTimer) {
            clearTimeout(this.completionTimer);
            this.completionTimer = null;
        }
    },

    countAllSequentially() {
        this.clearAutoTimers();
        const curSeqToken = ++this.autoSeqToken;
        const numData = this.currentData;
        const items = Array.from(document.querySelectorAll('#number-items-grid .count-item-btn'));

        // Reset countedSoFar and remove any stale count state so restarting starts cleanly from 1
        this.countedSoFar = 0;
        items.forEach(btn => {
            btn.classList.remove('counted');
            const b = btn.querySelector('.count-badge');
            if (b) b.remove();
        });
        this.updateTenFrame(0, numData.num);

        let currentStep = 0;
        const isSmallBadge = numData.num >= 16;

        const step = () => {
            if (curSeqToken !== this.autoSeqToken || app.currentView !== 'numbers') return;
            if (currentStep >= numData.num || currentStep >= items.length) {
                const instrEl = document.getElementById('number-instruction');
                if (instrEl) instrEl.textContent = `🎉 You counted all ${numData.num} ${numData.item}!`;
                const centerEl = document.getElementById('number-items-grid');
                if (centerEl) {
                    const rect = centerEl.getBoundingClientRect();
                    app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
                }
                app.speak(`${numData.num}! Yay! ${numData.word} ${numData.item}!`, null, () => {
                    if (curSeqToken === this.autoSeqToken && app.currentView === 'numbers') {
                        soundFX.playCheer();
                    }
                });
                return;
            }

            const itemBtn = items[currentStep];
            const stepNum = currentStep + 1;
            currentStep++;
            this.countedSoFar = stepNum;

            itemBtn.classList.add('counted');
            let badge = itemBtn.querySelector('.count-badge');
            if (!badge) {
                badge = document.createElement('div');
                badge.className = 'count-badge';
                if (isSmallBadge) {
                    badge.style.width = '1.2rem';
                    badge.style.height = '1.2rem';
                    badge.style.fontSize = '0.7rem';
                    badge.style.top = '-5px';
                    badge.style.right = '-5px';
                }
                itemBtn.appendChild(badge);
            }
            badge.textContent = stepNum;
            badge.classList.remove('scale-0', 'opacity-0');
            badge.classList.add('scale-100', 'opacity-100');

            app.animatePop(itemBtn);
            this.updateTenFrame(stepNum, numData.num);
            const instrEl = document.getElementById('number-instruction');
            if (instrEl) instrEl.textContent = `Counting: ${stepNum} of ${numData.num}`;

            const startTime = Date.now();
            const minStepMs = 550;

            const next = () => {
                if (curSeqToken !== this.autoSeqToken || app.currentView !== 'numbers') return;
                const elapsed = Date.now() - startTime;
                const waitMs = Math.max(120, minStepMs - elapsed + 120);
                const t = setTimeout(step, waitMs);
                this.autoTimers.push(t);
            };

            app.speak(String(stepNum), null, next);
        };

        step();
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
    wrongAttempts: 0,
    nextTimer: null,
    speechFollowupTimer: null,

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
            cat: 'letters',
            label: `Letter ${p.letter}`,
            display: `${p.letter}${p.letter.toLowerCase()}`,
            sub: `${p.words[0].e} ${p.words[0].w}`,
            prompt: `Can you find the letter ${p.letter}?`
        }));
        const maxNum = (typeof app !== 'undefined' && app.settings && app.settings.maxNumber) ? app.settings.maxNumber : 20;
        const numbersPool = GAMES.numbers.filter(n => n.num <= maxNum).map(n => ({
            cat: 'numbers',
            label: `Number ${n.num}`,
            display: `${n.num}`,
            sub: `${n.emoji} ${n.word}`,
            prompt: `Where is the number ${n.num}?`
        }));
        const animalsPool = GAMES.animals.map(a => ({
            cat: 'animals',
            label: a.id,
            display: a.emoji,
            sub: a.id,
            prompt: `Can you find the ${a.id}?`
        }));
        const shapesPool = GAMES.shapes.map(s => ({
            cat: 'shapes',
            label: s.id,
            display: '',
            displayHtml: `<svg class="w-14 h-14 sm:w-16 sm:h-16 mx-auto drop-shadow-sm pointer-events-none" viewBox="0 0 100 100">${s.svg}</svg>`,
            sub: s.id,
            prompt: `Can you find the ${s.id}?`
        }));
        const solarPool = GAMES.solar.map((s, idx) => {
            const needsThe = (s.id === 'Asteroid Belt' || s.id === 'Comet' || s.id === 'Galactic Swirl');
            const spokenName = needsThe ? `the ${s.id}` : s.id;
            return {
                cat: 'solar',
                label: s.id,
                display: s.emoji,
                displayHtml: `<div class="w-14 h-14 sm:w-16 sm:h-16 mx-auto rounded-2xl overflow-hidden bg-slate-950 p-1 shadow-inner border border-indigo-200/40 flex items-center justify-center pointer-events-none">${getSolarSVG(s.id, 'qzsol_' + idx)}</div>`,
                sub: s.id,
                prompt: `Where is ${spokenName}?`
            };
        });

        const blocksPool = [];
        const nbData = (window.NumberBlocks && window.NumberBlocks.Data);
        const nbRenderer = (window.NumberBlocks && window.NumberBlocks.Renderer);
        for (let n = 1; n <= maxNum; n++) {
            const charDef = (nbData && nbData.getCharacter) ? nbData.getCharacter(n) : null;
            const charName = (charDef && charDef.name) ? charDef.name : String(n);
            const cardHtml = (nbRenderer && nbRenderer.getQuizCardHTML)
                ? nbRenderer.getQuizCardHTML(n)
                : `<div class="text-5xl font-black text-rose-500">${n}</div>`;
            blocksPool.push({
                cat: 'blocks',
                label: 'Numberblock ' + n,
                display: String(n),
                displayHtml: cardHtml,
                sub: charName + ' (' + n + ')',
                prompt: 'Can you find Numberblock ' + charName + '?'
            });
        }

        if (this.category === 'letters') return lettersPool;
        if (this.category === 'numbers') return numbersPool;
        if (this.category === 'blocks') return blocksPool;
        if (this.category === 'animals') return animalsPool;
        if (this.category === 'shapes') return shapesPool;
        if (this.category === 'solar') return solarPool;
        return [...lettersPool, ...numbersPool, ...blocksPool, ...animalsPool, ...shapesPool, ...solarPool];
    },

    nextQuestion(isOpening = false) {
        if (this.nextTimer) {
            clearTimeout(this.nextTimer);
            this.nextTimer = null;
        }
        if (this.speechFollowupTimer) {
            clearTimeout(this.speechFollowupTimer);
            this.speechFollowupTimer = null;
        }
        this.answered = false;
        this.wrongAttempts = 0;

        const pool = this.getPool();
        if (!pool || pool.length === 0) return;

        // 1. Avoid back-to-back duplicate questions
        const candidatePool = (pool.length > 1 && this.currentAnswer)
            ? pool.filter(p => p.label !== this.currentAnswer.label)
            : pool;
        const winner = candidatePool[Math.floor(Math.random() * candidatePool.length)];
        this.currentAnswer = winner;

        // 2. Pick 2 distractors from the SAME category as winner (prevents cross-category visual collisions)
        const distractors = pool
            .filter(p => p.cat === winner.cat && p.label !== winner.label)
            .sort(() => Math.random() - 0.5)
            .slice(0, 2);

        // Fallback if not enough in same category (should not occur since each category has >= 10 items)
        if (distractors.length < 2) {
            const others = pool
                .filter(p => p.label !== winner.label && !distractors.some(d => d.label === p.label))
                .sort(() => Math.random() - 0.5)
                .slice(0, 2 - distractors.length);
            distractors.push(...others);
        }

        const choices = [winner, ...distractors].sort(() => Math.random() - 0.5);

        document.getElementById('quiz-question-text').textContent = `Find: ${winner.label}!`;
        const shouldAnnounce = (typeof app !== 'undefined' && app.settings) ? app.settings.announceGameOnOpen : true;
        const spoken = (isOpening && shouldAnnounce) ? `Look and Find! ${winner.prompt}` : winner.prompt;
        app.speak(spoken);

        const grid = document.getElementById('quiz-choices-grid');
        grid.innerHTML = '';

        choices.forEach(item => {
            const card = document.createElement('div');
            card.className = 'bg-white rounded-3xl p-4 sm:p-6 shadow-md border-4 border-amber-200 flex flex-col items-center justify-center min-h-[145px] cursor-pointer squish-btn transition-all duration-200';
            card.dataset.quizLabel = item.label;

            const visualContent = item.displayHtml
                ? `<div class="mb-2 flex items-center justify-center">${item.displayHtml}</div>`
                : `<div class="text-5xl sm:text-6xl font-black text-slate-800 mb-2">${item.display}</div>`;

            card.innerHTML = `${visualContent}<div class="text-xs sm:text-sm font-extrabold text-slate-500 text-center">${item.sub}</div>`;

            card.addEventListener('click', () => {
                // Post-win click lock: Ignore all clicks once answered
                if (this.answered) return;

                const rect = card.getBoundingClientRect();
                if (item.label === winner.label) {
                    this.answered = true;
                    this.score++;
                    document.getElementById('quiz-score').textContent = this.score;
                    card.classList.replace('border-amber-200', 'border-emerald-500');
                    card.classList.add('bg-emerald-50');
                    soundFX.playCheer();
                    app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
                    this.speechFollowupTimer = soundFX.registerTimer(setTimeout(() => {
                        app.speak(`You found it! ${winner.label}!`);
                        this.speechFollowupTimer = null;
                    }, 350));
                    this.nextTimer = setTimeout(() => this.nextQuestion(false), 1350);
                } else {
                    this.wrongAttempts++;
                    soundFX.playNote(220, 0.15, 'sine');
                    card.classList.add('shake-anim', 'opacity-50');
                    app.speak(`Try to find ${winner.label}!`);
                    setTimeout(() => card.classList.remove('shake-anim'), 350);

                    // Scaffolding: if child tried wrong twice, highlight the winning card
                    if (this.wrongAttempts >= 2) {
                        grid.querySelectorAll('.squish-btn').forEach(btn => {
                            if (btn.dataset.quizLabel === winner.label) {
                                btn.classList.add('ring-4', 'ring-amber-400', 'border-amber-400', 'animate-pulse');
                            }
                        });
                    }
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
        this.camera.position.z = 6.2;

        this.renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        this.renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
        const canvas = this.renderer.domElement;
        canvas.style.width = '100%';
        canvas.style.height = '100%';
        canvas.style.display = 'block';
        container.appendChild(canvas);

        const updateSize = () => {
            const w = container.clientWidth || 256;
            const h = container.clientHeight || 256;
            this.renderer.setSize(w, h, false);
            this.camera.aspect = w / h;
            this.camera.updateProjectionMatrix();
        };
        updateSize();

        if (window.ResizeObserver) {
            this.resizeObserver = new ResizeObserver(() => updateSize());
            this.resizeObserver.observe(container);
        }

        const worldX = new THREE.Vector3(1, 0, 0);
        const worldY = new THREE.Vector3(0, 1, 0);

        container.addEventListener('pointerdown', e => {
            if (typeof zoomController !== 'undefined' && (zoomController.isPinching || zoomController.isDragging1Finger)) return;
            this.isDragging = false;
            this.pointerDownX = e.clientX;
            this.pointerDownY = e.clientY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
        });

        container.addEventListener('pointermove', e => {
            if (typeof zoomController !== 'undefined' && (zoomController.isPinching || zoomController.isDragging1Finger || zoomController.isLongPressActive)) {
                this.isDragging = false;
                return;
            }
            const dist = Math.hypot(e.clientX - (this.pointerDownX || e.clientX), e.clientY - (this.pointerDownY || e.clientY));
            if (!this.isDragging) {
                if (dist > 8) {
                    this.isDragging = true;
                    try { container.setPointerCapture(e.pointerId); } catch (err) {}
                } else {
                    return;
                }
            }
            if (!this.mesh) return;
            const dx = e.clientX - this.prevX;
            const dy = e.clientY - this.prevY;
            this.prevX = e.clientX;
            this.prevY = e.clientY;
            const dragMult = typeof app !== 'undefined' ? app.getDragSpeedMultiplier() : 1.0;
            this.velX = dx * 0.014 * dragMult;
            this.velY = dy * 0.014 * dragMult;
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

    getHexLuminance(hex) {
        if (!hex) return 0;
        let c = hex.replace('#', '');
        if (c.length === 3) c = c.split('').map(x => x + x).join('');
        const num = parseInt(c, 16);
        const r = (num >> 16) & 255;
        const g = (num >> 8) & 255;
        const b = num & 255;
        const [rs, gs, bs] = [r, g, b].map(v => {
            const s = v / 255;
            return s <= 0.03928 ? s / 12.92 : Math.pow((s + 0.055) / 1.055, 2.4);
        });
        return 0.2126 * rs + 0.7152 * gs + 0.0722 * bs;
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

        const lum = this.getHexLuminance(cData.hex);
        if (lum > 0.5) {
            txt.style.color = '#0f172a';
            txt.style.textShadow = 'none';
        } else {
            txt.style.color = '#ffffff';
            txt.style.textShadow = '0 2px 8px rgba(0, 0, 0, 0.45)';
        }

        if (lum > 0.8) {
            bg.style.boxShadow = 'inset 0 0 0 3px #cbd5e1';
            ex.style.border = '2px solid #e2e8f0';
        } else {
            bg.style.boxShadow = '';
            ex.style.border = '';
        }

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
        const mixBg = document.getElementById('color-bg-target');
        mixBg.style.backgroundColor = res.hex;
        const mixLum = this.getHexLuminance(res.hex);
        if (mixLum > 0.8) {
            mixBg.style.boxShadow = 'inset 0 0 0 3px #cbd5e1';
        } else {
            mixBg.style.boxShadow = '';
        }
        const mixResText = document.getElementById('mix-result-text');
        mixResText.textContent = `${c1} + ${c2} = ${res.name}!`;
        mixResText.style.color = '#0f172a';
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
        if (this.speechTimer) {
            clearTimeout(this.speechTimer);
            this.speechTimer = null;
        }
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
                app.speak(a.id, null, () => {
                    this.speechTimer = soundFX.registerTimer(setTimeout(() => {
                        soundFX.playAnimalSound(a.id);
                        this.speechTimer = null;
                    }, 180));
                });
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

    cheerTimer: null,
    finalChimeTimer: null,
    finalSpeechTimer: null,

    chomp(e) {
        if (this.cheerTimer) { clearTimeout(this.cheerTimer); this.cheerTimer = null; }
        if (this.finalChimeTimer) { clearTimeout(this.finalChimeTimer); this.finalChimeTimer = null; }
        if (this.finalSpeechTimer) { clearTimeout(this.finalSpeechTimer); this.finalSpeechTimer = null; }
        geminiTTS.stop();
        if ('speechSynthesis' in window && (window.speechSynthesis.speaking || window.speechSynthesis.pending)) {
            try { window.speechSynthesis.cancel(); } catch (e) {}
        }
        app.speechToken++;

        // ALWAYS play crisp physical bite crunch!
        const crunchDur = soundFX.playCrunch() || 550;

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
            this.cheerTimer = soundFX.registerTimer(setTimeout(() => {
                if (app.currentView === 'fruits') {
                    app.speak(cheers[idx % cheers.length]);
                }
                this.cheerTimer = null;
            }, crunchDur + 80));
        } else {
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            app.burstConfetti(rect.left + rect.width / 2, rect.top + rect.height / 2);
            document.getElementById('fruits-desc').textContent = `All gone! Getting another ${this.current.id}... 🎉`;

            this.finalChimeTimer = soundFX.registerTimer(setTimeout(() => {
                if (app.currentView !== 'fruits') return;
                soundFX.playCheer();
                this.finalSpeechTimer = soundFX.registerTimer(setTimeout(() => {
                    if (app.currentView === 'fruits') {
                        app.speak(`All gone! Yummy ${this.current.id}! Delicious!`);
                    }
                    this.finalSpeechTimer = null;
                }, 550));
                this.finalChimeTimer = null;
            }, crunchDur + 60));

            setTimeout(() => {
                if (app.currentView === 'fruits') {
                    this.biteList = [];
                    this.renderFoodCanvas();
                    document.getElementById('fruits-desc').textContent = `Fresh ${this.current.id}! Tap to take a bite!`;
                }
            }, 1200);
        }
    }
};

const thingsGame = {
    current: GAMES.things[0],
    speechTimer: null,
    select(item, speak = true, soundOnly = false) {
        this.current = item;
        soundFX.stopAll();
        if (this.speechTimer) {
            clearTimeout(this.speechTimer);
            this.speechTimer = null;
        }
        if (soundOnly || !speak) {
            geminiTTS.stop();
            if ('speechSynthesis' in window && (window.speechSynthesis.speaking || window.speechSynthesis.pending)) {
                try { window.speechSynthesis.cancel(); } catch (e) {}
            }
        }
        const t = document.getElementById('things-target');
        t.textContent = item.emoji;
        document.getElementById('things-text').textContent = item.id;
        document.getElementById('things-sound').textContent = `🔊 "${item.sound}"`;
        document.querySelectorAll('#things-controls .tray-btn').forEach(b => {
            b.classList.toggle('selected', b.dataset.thingId === item.id);
        });
        app.animatePop(t);
        if (soundOnly) {
            soundFX.playThingSound(item.id);
            return;
        }
        if (speak) {
            if (app.isOpeningView && !app.settings.announceGameOnOpen) {
                return;
            }
            app.speak(item.id, null, () => {
                this.speechTimer = soundFX.registerTimer(setTimeout(() => {
                    soundFX.playThingSound(item.id);
                    this.speechTimer = null;
                }, 180));
            });
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

    const storedKey = runtimeVoiceConfig.apiKey || safeGetStorage('tlh_isolated_v3_api_key') || safeGetStorage('toddler_gemini_api_key');
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

const zoomController = {
    scale: 1.0,
    panX: 0,
    panY: 0,
    isPinching: false,
    isDragging1Finger: false,
    isLongPressActive: false,
    suppressClick: false,

    showDragIndicator(stage) {
        const badge = stage.querySelector('.drag-hud-badge');
        if (badge) badge.classList.add('visible');
    },

    hideDragIndicator(stage) {
        const badge = stage.querySelector('.drag-hud-badge');
        if (badge) badge.classList.remove('visible');
    },

    init() {
        // Global click-suppression after drag
        window.addEventListener('click', (e) => {
            if (this.suppressClick) {
                e.stopPropagation();
                e.preventDefault();
            }
        }, true);

        const gameViews = [
            'letters', 'numbers', 'quiz', 'shapes', 'shapes3d',
            'colors', 'animals', 'fruits', 'things', 'opposites', 'solar'
        ];

        gameViews.forEach(vName => {
            const viewEl = document.getElementById(`view-${vName}`);
            if (!viewEl) return;
            const stages = viewEl.querySelectorAll('.main-stage');
            stages.forEach(stage => {
                if (stage.id === 'phonics-bubble-stage') return;
                this.setupStageZoom(stage, vName);
            });
        });
    },

    setupStageZoom(stage, viewName) {
        if (!stage || stage.querySelector('.zoom-hud-pill')) return;

        // Floating Draggable & Minimizable Zoom Pill (Upgrade 2)
        const pill = document.createElement('div');
        pill.className = 'zoom-hud-pill';
        pill.title = 'Drag to move • Tap to expand / pinch to zoom';

        // Minimized View Badge (🔍 100%)
        const minBadge = document.createElement('span');
        minBadge.className = 'zoom-min-badge';
        minBadge.innerHTML = '🔍 <span class="zoom-min-pct">100%</span>';

        // Expanded Controls Group
        const controlsGroup = document.createElement('div');
        controlsGroup.className = 'zoom-controls-group flex items-center gap-1';

        const outBtn = document.createElement('button');
        outBtn.type = 'button';
        outBtn.className = 'zoom-out-btn';
        outBtn.title = 'Zoom Out';
        outBtn.setAttribute('aria-label', 'Zoom Out');
        outBtn.textContent = '−';

        const resetBtn = document.createElement('button');
        resetBtn.type = 'button';
        resetBtn.className = 'zoom-reset-btn';
        resetBtn.title = 'Reset Zoom';
        resetBtn.setAttribute('aria-label', 'Reset Zoom');
        resetBtn.textContent = '100%';

        const inBtn = document.createElement('button');
        inBtn.type = 'button';
        inBtn.className = 'zoom-in-btn';
        inBtn.title = 'Zoom In';
        inBtn.setAttribute('aria-label', 'Zoom In');
        inBtn.textContent = '+';

        const closeBtn = document.createElement('button');
        closeBtn.type = 'button';
        closeBtn.className = 'zoom-close-btn text-slate-400 hover:text-slate-700 px-1';
        closeBtn.title = 'Minimize Magnifier';
        closeBtn.setAttribute('aria-label', 'Minimize Magnifier');
        closeBtn.textContent = '✕';

        controlsGroup.appendChild(outBtn);
        controlsGroup.appendChild(resetBtn);
        controlsGroup.appendChild(inBtn);
        controlsGroup.appendChild(closeBtn);

        pill.appendChild(minBadge);
        pill.appendChild(controlsGroup);
        stage.appendChild(pill);

        // Floating 1-Finger Drag Indicator Badge
        const dragBadge = document.createElement('div');
        dragBadge.className = 'drag-hud-badge';
        dragBadge.innerHTML = '<span>🖐️</span><span>Dragging</span>';
        stage.appendChild(dragBadge);

        // 1-Finger Dragging for the Zoom Pill
        let pillDragging = false;
        let pillStartX = 0, pillStartY = 0;
        let initialPillLeft = 0, initialPillTop = 0;
        let pillMovedDist = 0;

        pill.addEventListener('pointerdown', (e) => {
            e.stopPropagation();
            pillDragging = true;
            pillMovedDist = 0;
            pillStartX = e.clientX;
            pillStartY = e.clientY;
            const rect = pill.getBoundingClientRect();
            const stageRect = stage.getBoundingClientRect();
            initialPillLeft = rect.left - stageRect.left;
            initialPillTop = rect.top - stageRect.top;
            try { pill.setPointerCapture(e.pointerId); } catch(err) {}
        });

        pill.addEventListener('pointermove', (e) => {
            if (!pillDragging) return;
            e.stopPropagation();
            const dx = e.clientX - pillStartX;
            const dy = e.clientY - pillStartY;
            pillMovedDist = Math.hypot(dx, dy);
            if (pillMovedDist > 4) {
                const stageRect = stage.getBoundingClientRect();
                const pillW = pill.offsetWidth;
                const pillH = pill.offsetHeight;
                const newL = Math.max(4, Math.min(stageRect.width - pillW - 4, initialPillLeft + dx));
                const newT = Math.max(4, Math.min(stageRect.height - pillH - 4, initialPillTop + dy));
                pill.style.left = `${newL}px`;
                pill.style.top = `${newT}px`;
                pill.style.right = 'auto';
                pill.style.bottom = 'auto';
            }
        });

        const endPillDrag = (e) => {
            if (!pillDragging) return;
            e.stopPropagation();
            pillDragging = false;
            try { pill.releasePointerCapture(e.pointerId); } catch(err) {}
        };
        pill.addEventListener('pointerup', endPillDrag);
        pill.addEventListener('pointercancel', endPillDrag);

        // Toggle Minimize / Expand
        pill.addEventListener('click', (e) => {
            if (pillMovedDist > 6) {
                e.stopPropagation();
                return;
            }
            if (pill.classList.contains('minimized')) {
                e.stopPropagation();
                if (typeof soundFX !== 'undefined') soundFX.playPop();
                pill.classList.remove('minimized');
            }
        });
        closeBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            if (typeof soundFX !== 'undefined') soundFX.playPop();
            pill.classList.add('minimized');
        });

        outBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            this.zoomBy(-0.35);
        });
        resetBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            if (typeof soundFX !== 'undefined') soundFX.playPop();
            this.resetZoom();
        });
        inBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            this.zoomBy(0.35);
        });

        // 1-Finger Long-Press & Drag System across all games
        let longPressTimer = null;
        let isLongPressActive = false;
        let isDragging1Finger = false;
        let startPointerId = null;
        let startX = 0, startY = 0;
        let lastX = 0, lastY = 0;
        let lastTapTime = 0;
        let lastTapX = 0, lastTapY = 0;
        let dragTarget = null;

        stage.addEventListener('pointerdown', (e) => {
            if (this.isPinching) return;
            // Ignore touches on UI controls, buttons, drawers, tray, or hud pills
            if (e.target.closest('.zoom-hud-pill') || e.target.closest('#solar-orbit-controls') || e.target.closest('#solar-orbit-drawer') || e.target.closest('.home-btn') || e.target.closest('.options-quick-btn') || e.target.closest('.mode-switch') || e.target.closest('.controls-dock') || e.target.closest('.top-bar')) {
                return;
            }

            const now = Date.now();
            const tapDist = Math.hypot(e.clientX - lastTapX, e.clientY - lastTapY);
            if (now - lastTapTime < 320 && tapDist < 30) {
                // Double tap detected: reset zoom & pan to center!
                clearTimeout(longPressTimer);
                longPressTimer = null;
                isLongPressActive = false;
                isDragging1Finger = false;
                this.isDragging1Finger = false;
                this.isLongPressActive = false;
                if (typeof soundFX !== 'undefined') soundFX.playPop();
                this.resetZoom();
                lastTapTime = 0;
                return;
            }
            lastTapTime = now;
            lastTapX = e.clientX;
            lastTapY = e.clientY;

            // Prepare potential long-press drag
            clearTimeout(longPressTimer);
            isLongPressActive = false;
            isDragging1Finger = false;
            this.isDragging1Finger = false;
            this.isLongPressActive = false;
            startPointerId = e.pointerId;
            startX = e.clientX;
            startY = e.clientY;
            lastX = e.clientX;
            lastY = e.clientY;

            const curView = typeof app !== 'undefined' ? app.currentView : viewName;
            dragTarget = this.getTargetForView(curView);

            // Start Long-Press Timer (380ms)
            longPressTimer = setTimeout(() => {
                isLongPressActive = true;
                isDragging1Finger = true;
                this.isDragging1Finger = true;
                this.isLongPressActive = true;

                // Tactile & Audio feedback
                if (typeof soundFX !== 'undefined') soundFX.playPop();
                if (navigator.vibrate) {
                    try { navigator.vibrate([30, 25, 30]); } catch(err) {}
                }

                // If in 3D view, disengage 3D rotation so finger purely translates the model
                if (typeof shapes3DGame !== 'undefined') shapes3DGame.isDragging = false;
                if (typeof solarGame !== 'undefined') solarGame.isDragging = false;

                // Highlight target with lifted state
                if (dragTarget) {
                    dragTarget.classList.add('item-drag-active');
                }

                // Show floating drag badge
                this.showDragIndicator(stage);

                // Capture pointer to stage so movement is never lost even if moving fast
                try { stage.setPointerCapture(startPointerId); } catch(err) {}
            }, 380);
        });

        stage.addEventListener('pointermove', (e) => {
            if (this.isPinching) {
                clearTimeout(longPressTimer);
                longPressTimer = null;
                return;
            }

            if (!isLongPressActive) {
                // Check if finger moved before the 380ms long-press elapsed
                const dist = Math.hypot(e.clientX - startX, e.clientY - startY);
                if (dist > 8) {
                    // Canceled long-press because user moved/swiped/spun
                    clearTimeout(longPressTimer);
                    longPressTimer = null;
                }
                return;
            }

            // Long-press IS active: user is now 1-finger dragging the target!
            if (e.cancelable) e.preventDefault();

            const dx = e.clientX - lastX;
            const dy = e.clientY - lastY;
            lastX = e.clientX;
            lastY = e.clientY;

            const speedMult = typeof app !== 'undefined' ? app.getDragSpeedMultiplier() : 1.0;
            const newPanX = this.panX + dx * speedMult;
            const newPanY = this.panY + dy * speedMult;
            this.applyZoom(this.scale, newPanX, newPanY);
        });

        const endLongPressDrag = (e) => {
            clearTimeout(longPressTimer);
            longPressTimer = null;

            if (isLongPressActive || isDragging1Finger) {
                isLongPressActive = false;
                isDragging1Finger = false;
                this.isDragging1Finger = false;
                this.isLongPressActive = false;

                if (dragTarget) {
                    dragTarget.classList.remove('item-drag-active');
                }
                this.hideDragIndicator(stage);

                if (typeof soundFX !== 'undefined') soundFX.playPop();

                try { stage.releasePointerCapture(e.pointerId); } catch(err) {}

                // Suppress click event so releasing after a drag doesn't trigger tap action
                zoomController.suppressClick = true;
                setTimeout(() => {
                    zoomController.suppressClick = false;
                }, 320);
            }
        };

        stage.addEventListener('pointerup', endLongPressDrag);
        stage.addEventListener('pointercancel', endLongPressDrag);

        // Touch Pinch-to-Zoom & 2-Finger Pan Listeners
        let startDist = 0;
        let startScale = 1.0;
        let startMidX = 0, startMidY = 0;
        let startPanX = 0, startPanY = 0;

        stage.addEventListener('touchstart', (e) => {
            if (e.touches.length === 2) {
                this.isPinching = true;
                startDist = Math.hypot(
                    e.touches[0].clientX - e.touches[1].clientX,
                    e.touches[0].clientY - e.touches[1].clientY
                );
                startScale = this.scale;
                startMidX = (e.touches[0].clientX + e.touches[1].clientX) / 2;
                startMidY = (e.touches[0].clientY + e.touches[1].clientY) / 2;
                startPanX = this.panX;
                startPanY = this.panY;
            }
        }, { passive: false });

        stage.addEventListener('touchmove', (e) => {
            if (this.isPinching && e.touches.length === 2) {
                if (e.cancelable) e.preventDefault();
                const dist = Math.hypot(
                    e.touches[0].clientX - e.touches[1].clientX,
                    e.touches[0].clientY - e.touches[1].clientY
                );
                if (startDist > 0) {
                    const factor = dist / startDist;
                    const newScale = Math.max(0.6, Math.min(3.5, startScale * factor));
                    const midX = (e.touches[0].clientX + e.touches[1].clientX) / 2;
                    const midY = (e.touches[0].clientY + e.touches[1].clientY) / 2;
                    const newPanX = startPanX + (midX - startMidX);
                    const newPanY = startPanY + (midY - startMidY);
                    this.applyZoom(newScale, newPanX, newPanY);
                }
            }
        }, { passive: false });

        const endPinch = (e) => {
            if (e.touches.length < 2) {
                this.isPinching = false;
            }
        };
        stage.addEventListener('touchend', endPinch);
        stage.addEventListener('touchcancel', endPinch);

        // Desktop / Trackpad pinch (wheel with ctrlKey or metaKey)
        stage.addEventListener('wheel', (e) => {
            if (e.ctrlKey || e.metaKey) {
                if (e.cancelable) e.preventDefault();
                const delta = -e.deltaY * 0.01;
                this.zoomBy(delta, false);
            }
        }, { passive: false });
    },

    is3DView(viewName) {
        if (viewName === 'shapes3d') return true;
        if (viewName === 'solar' && typeof solarGame !== 'undefined' && solarGame.mode !== 'photo') return true;
        return false;
    },

    getTargetForView(viewName) {
        switch (viewName) {
            case 'letters':
                return document.getElementById('phonics-zoom-target') || document.getElementById('phonics-main-card');
            case 'numbers':
                return document.getElementById('number-items-grid');
            case 'quiz':
                return document.getElementById('quiz-choices-grid');
            case 'shapes':
                return document.getElementById('shape-target');
            case 'shapes3d':
                return document.getElementById('shape3d-target');
            case 'colors':
                return document.getElementById('color-explore-box') || document.getElementById('color-bg-target');
            case 'animals':
                return document.getElementById('animal-target');
            case 'fruits':
                return document.getElementById('fruits-target');
            case 'things':
                return document.getElementById('things-target');
            case 'opposites':
                return document.getElementById('opposites-cards-grid') || document.querySelector('#view-opposites .main-stage .grid');
            case 'solar':
                return document.getElementById('solar-stage-box') || document.getElementById('solar-photo-container') || document.getElementById('solar-svg-holder');
            default:
                return null;
        }
    },

    applyZoom(newScale, newPanX = this.panX, newPanY = this.panY) {
        this.scale = Math.max(0.6, Math.min(3.5, Math.round(newScale * 100) / 100));
        if (Math.abs(this.scale - 1.0) < 0.04) {
            this.scale = 1.0;
        }
        this.panX = Math.round(newPanX);
        this.panY = Math.round(newPanY);

        const curView = typeof app !== 'undefined' ? app.currentView : null;
        if (!curView || curView === 'menu') return;

        if (curView === 'shapes3d' && typeof shapes3DGame !== 'undefined' && shapes3DGame.camera) {
            shapes3DGame.camera.zoom = Math.max(0.55, Math.min(3.2, this.scale));
            shapes3DGame.camera.updateProjectionMatrix();
        } else if (curView === 'solar' && typeof solarGame !== 'undefined' && solarGame.camera && solarGame.mode !== 'photo') {
            solarGame.camera.zoom = Math.max(0.55, Math.min(3.2, this.scale));
            solarGame.camera.updateProjectionMatrix();
        }

        const target = this.getTargetForView(curView);
        if (target) {
            target.style.transformOrigin = 'center center';
            if (this.scale === 1.0 && this.panX === 0 && this.panY === 0) {
                target.style.transform = '';
                target.style.zIndex = '';
            } else {
                target.style.transform = `translate3d(${this.panX}px, ${this.panY}px, 0) scale(${this.scale})`;
                target.style.zIndex = (this.scale > 1.02 || Math.abs(this.panX) > 6 || Math.abs(this.panY) > 6) ? '25' : '';
            }
        }

        this.updateHUD();
    },

    zoomBy(delta, playSound = true) {
        if (playSound && typeof soundFX !== 'undefined') soundFX.playPop();
        const nextScale = Math.max(0.6, Math.min(3.5, this.scale + delta));
        const nextPanX = nextScale === 1.0 ? 0 : this.panX;
        const nextPanY = nextScale === 1.0 ? 0 : this.panY;
        this.applyZoom(nextScale, nextPanX, nextPanY);
    },

    resetZoom() {
        this.scale = 1.0;
        this.panX = 0;
        this.panY = 0;
        const curView = typeof app !== 'undefined' ? app.currentView : null;
        const gameViews = [
            'letters', 'numbers', 'quiz', 'shapes', 'shapes3d',
            'colors', 'animals', 'fruits', 'things', 'opposites', 'solar'
        ];
        gameViews.forEach(vName => {
            const target = this.getTargetForView(vName);
            if (target) {
                target.style.transform = '';
                target.style.zIndex = '';
                target.classList.remove('item-drag-active');
            }
        });
        if (typeof shapes3DGame !== 'undefined' && shapes3DGame.camera) {
            shapes3DGame.camera.zoom = 1.0;
            shapes3DGame.camera.updateProjectionMatrix();
        }
        if (typeof solarGame !== 'undefined' && solarGame.camera) {
            solarGame.camera.zoom = 1.0;
            solarGame.camera.updateProjectionMatrix();
        }
        this.updateHUD();
    },

    updateHUD() {
        const curView = typeof app !== 'undefined' ? app.currentView : null;
        if (!curView) return;
        const viewEl = document.getElementById(`view-${curView}`);
        if (!viewEl) return;
        const labels = viewEl.querySelectorAll('.zoom-reset-btn');
        labels.forEach(btn => {
            btn.textContent = `${Math.round(this.scale * 100)}%`;
        });
        const minLabels = viewEl.querySelectorAll('.zoom-min-pct');
        minLabels.forEach(span => {
            span.textContent = `${Math.round(this.scale * 100)}%`;
        });
    }
};

window.addEventListener('DOMContentLoaded', () => {
    app.updateViewportTheme(app.currentView || 'menu');
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

    const saveVoiceInputsToStorage = () => {
        if (inp) {
            const val = inp.value.trim();
            if (!val.includes('●●●●●●●●')) {
                runtimeVoiceConfig.apiKey = val;
                safeSetStorage('tlh_isolated_v3_api_key', val);
            }
        }
        if (modelSel && modelSel.value) {
            const prevModel = runtimeVoiceConfig.model || safeGetStorage('tlh_isolated_v3_tts_model');
            if (prevModel && prevModel !== modelSel.value) {
                safeSetStorage('tlh_isolated_v3_working_strat', '');
                geminiTTS.workingStrategy = null;
            }
            runtimeVoiceConfig.model = modelSel.value;
            safeSetStorage('tlh_isolated_v3_tts_model', modelSel.value);
        }
        if (voiceSel && voiceSel.value) {
            runtimeVoiceConfig.voice = voiceSel.value;
            safeSetStorage('tlh_isolated_v3_tts_voice', voiceSel.value);
        }
        updateVoiceStatusIndicator();
    };

    const syncSettingsToUI = () => {
        const s = app.settings;
        const tierSel = document.getElementById('precache-tier-select');
        if (tierSel) {
            tierSel.value = safeGetStorage('tlh_precache_tier') || 'tier2_turbo';
        }
        const optAnnounce = document.getElementById('opt-announce-open');
        if (optAnnounce) optAnnounce.checked = !!s.announceGameOnOpen;
        const optVoice = document.getElementById('opt-voice-enabled');
        if (optVoice) optVoice.checked = !!s.voiceEnabled;
        const optSfx = document.getElementById('opt-sfx-enabled');
        if (optSfx) optSfx.checked = !!s.sfxEnabled;
        const optSpeechRate = document.getElementById('opt-speech-rate');
        if (optSpeechRate) optSpeechRate.value = s.speechRate || 'normal';
        const optDragSpeed = document.getElementById('opt-drag-speed');
        if (optDragSpeed) optDragSpeed.value = s.dragSpeed || 'normal';
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
        const optMinHeader = document.getElementById('opt-minimize-header');
        if (optMinHeader) optMinHeader.checked = !!s.minimizeMenuHeader;
        const optSolarCredits = document.getElementById('opt-solar-credits');
        if (optSolarCredits) optSolarCredits.checked = !!s.showSolarCredits;
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
        saveVoiceInputsToStorage();
        if (voiceModal) voiceModal.classList.add('hidden');
    };

    document.getElementById('voice-settings-btn')?.addEventListener('click', openVoiceModal);
    document.querySelectorAll('.options-quick-btn').forEach(btn => {
        btn.addEventListener('click', openVoiceModal);
    });
    document.getElementById('voice-modal-close-x')?.addEventListener('click', closeVoiceModal);
    voiceModal?.addEventListener('click', (e) => {
        if (e.target === voiceModal) closeVoiceModal();
    });

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
    document.getElementById('opt-drag-speed')?.addEventListener('change', (e) => {
        app.settings.dragSpeed = e.target.value;
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
    document.getElementById('opt-minimize-header')?.addEventListener('change', (e) => {
        app.settings.minimizeMenuHeader = e.target.checked;
        app.saveSettings();
        app.applyMenuHeaderState();
    app.applySolarCreditsState();
    });
    document.getElementById('opt-solar-credits')?.addEventListener('change', (e) => {
        app.settings.showSolarCredits = e.target.checked;
        app.saveSettings();
        app.applySolarCreditsState();
    });

    document.getElementById('opt-reset-defaults-btn')?.addEventListener('click', () => {
        app.settings = Object.assign({}, DEFAULT_SETTINGS);
        app.saveSettings();
        syncSettingsToUI();
        app.applyMenuHeaderState();
        app.applySolarCreditsState();
        soundFX.playPop();
    });

    // Live input listeners so changes take effect immediately
    inp?.addEventListener('input', saveVoiceInputsToStorage);
    inp?.addEventListener('change', saveVoiceInputsToStorage);
    inp?.addEventListener('paste', () => setTimeout(saveVoiceInputsToStorage, 20));
    inp?.addEventListener('blur', saveVoiceInputsToStorage);
    modelSel?.addEventListener('change', saveVoiceInputsToStorage);
    voiceSel?.addEventListener('change', saveVoiceInputsToStorage);

    // Save & Done button
    document.getElementById('voice-modal-save-btn')?.addEventListener('click', () => {
        saveVoiceInputsToStorage();
        app.saveSettings();
        closeVoiceModal();
        if (app.settings.voiceEnabled) {
            app.speak("Options saved! Let's explore together!");
        }
    });

    // Live Test Voice Sample Button (tests live input values directly)
    document.getElementById('voice-test-btn')?.addEventListener('click', async () => {
        saveVoiceInputsToStorage();
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

    // Pre-populate known database cache keys for instant O(1) checks
    ttsDB.getAllKeys().then(keys => {
        if (keys && keys.length) {
            keys.forEach(k => geminiTTS.knownDbKeys.add(k));
        }
    }).catch(() => {});

    // Pre-cache Controls wired to background precacheManager
    document.getElementById('voice-precache-btn')?.addEventListener('click', () => {
        saveVoiceInputsToStorage();
        if (precacheManager.state === 'running') {
            precacheManager.pause();
        } else if (precacheManager.state === 'paused') {
            precacheManager.resume();
        } else {
            precacheManager.start();
        }
    });

    document.getElementById('precache-modal-pause-btn')?.addEventListener('click', () => {
        if (precacheManager.state === 'running') precacheManager.pause();
        else if (precacheManager.state === 'paused') precacheManager.resume();
    });

    document.getElementById('precache-modal-cancel-btn')?.addEventListener('click', () => {
        precacheManager.cancel();
    });

    document.getElementById('precache-pill-pause-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        if (precacheManager.state === 'running') precacheManager.pause();
        else if (precacheManager.state === 'paused') precacheManager.resume();
    });

    document.getElementById('precache-pill-settings-btn')?.addEventListener('click', () => {
        openVoiceModal();
    });

    // Wire Menu Header Minimize Button & initial state
    document.getElementById('menu-minimize-btn')?.addEventListener('click', () => {
        soundFX.playPop();
        app.settings.minimizeMenuHeader = !app.settings.minimizeMenuHeader;
        app.saveSettings();
        app.applyMenuHeaderState();
    });
    app.applyMenuHeaderState();

    // Setup Collapsible Bottom Trays across all docks
    document.querySelectorAll('.controls-dock').forEach(dock => {
        if (dock.querySelector('.dock-toggle-bar')) return;
        const bar = document.createElement('div');
        bar.className = 'dock-toggle-bar';
        const btn = document.createElement('button');
        btn.className = 'dock-toggle-btn';
        btn.type = 'button';
        btn.innerHTML = '<span>▼</span><span>Hide Selection Tray</span>';
        btn.setAttribute('aria-label', 'Toggle Selection Tray');
        btn.addEventListener('click', (e) => {
            e.stopPropagation();
            soundFX.playPop();
            const isCollapsed = dock.classList.toggle('dock-collapsed');
            btn.innerHTML = isCollapsed ? '<span>▲</span><span>Show Selection Tray</span>' : '<span>▼</span><span>Hide Selection Tray</span>';
        });
        dock.insertBefore(bar, dock.firstChild);
        bar.appendChild(btn);
    });

    // Initialize Universal Pinch-to-Zoom Controller
    zoomController.init();

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
    document.getElementById('number-open-blocks-btn')?.addEventListener('click', () => {
        soundFX.playPop();
        const n = (numberGame && numberGame.currentData && numberGame.currentData.num) ? numberGame.currentData.num : 1;
        app.switchView('blocks');
        if (window.NumberBlocks && window.NumberBlocks.Game && window.NumberBlocks.Game.openWithNumber) {
            window.NumberBlocks.Game.openWithNumber(n);
        }
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
    document.getElementById('fruits-target').addEventListener('click', e => foodGame.chomp(e));
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

    // 14. Solar System Setup with Fit-All 7x2 Planet Selection Tray
    const solarTray = document.getElementById('solar-controls');
    GAMES.solar.forEach((s, idx) => {
        const btn = document.createElement('button');
        btn.className = 'tray-btn';
        btn.dataset.solarId = s.id;
        const thumbWrap = document.createElement('div');
        thumbWrap.className = 'w-7 h-7 sm:w-8 sm:h-8 rounded-full overflow-hidden border border-slate-400 bg-slate-950 flex items-center justify-center flex-shrink-0';
        const thumbImg = document.createElement('img');
        thumbImg.src = s.photoUrl;
        thumbImg.alt = s.short;
        thumbImg.className = 'w-full h-full object-cover';
        thumbImg.addEventListener('error', () => {
            thumbWrap.innerHTML = getSolarSVG(s.id, 'tray_' + idx);
        }, { once: true });
        thumbWrap.appendChild(thumbImg);
        const labelSpan = document.createElement('span');
        labelSpan.className = 'text-[9.5px] sm:text-[10px] font-black text-slate-100 leading-none truncate max-w-full px-0.5 mt-0.5';
        labelSpan.textContent = s.short;
        btn.appendChild(thumbWrap);
        btn.appendChild(labelSpan);
        btn.addEventListener('click', () => solarGame.select(s, true));
        solarTray.appendChild(btn);
    });
    document.getElementById('solar-mode-photo').addEventListener('click', () => solarGame.setMode('photo'));
    document.getElementById('solar-mode-planet').addEventListener('click', () => solarGame.setMode('planet'));
    document.getElementById('solar-mode-orbit').addEventListener('click', () => solarGame.setMode('orbit'));
    // Wire Solar Orbit Drawer & Controls (Upgrade 2b)
    document.getElementById('solar-orbit-drawer-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        soundFX.playPop();
        const drawer = document.getElementById('solar-orbit-drawer');
        if (drawer) {
            drawer.classList.toggle('hidden');
        }
    });
    document.getElementById('solar-orbit-drawer-close')?.addEventListener('click', (e) => {
        e.stopPropagation();
        document.getElementById('solar-orbit-drawer')?.classList.add('hidden');
        document.getElementById('solar-date-popover')?.classList.add('hidden');
    });

    document.getElementById('solar-play-pause-quick-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        soundFX.playPop();
        solarGame.togglePlayPause();
    });
    document.getElementById('solar-play-pause-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        soundFX.playPop();
        solarGame.togglePlayPause();
    });
    document.getElementById('solar-turbo-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        solarGame.triggerAction();
    });

    // Speed Controls & Preset Pills (Upgrade 2b)
    document.getElementById('solar-speed-down-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        const cur = solarGame.orbitSpeed;
        const presets = [0.25, 0.5, 1, 2, 5, 10];
        const lower = presets.filter(p => p < cur - 0.05);
        const target = lower.length ? lower[lower.length - 1] : 0.25;
        solarGame.setOrbitSpeed(target);
    });
    document.getElementById('solar-speed-up-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        const cur = solarGame.orbitSpeed;
        const presets = [0.25, 0.5, 1, 2, 5, 10];
        const higher = presets.filter(p => p > cur + 0.05);
        const target = higher.length ? higher[0] : 10;
        solarGame.setOrbitSpeed(target);
    });
    document.getElementById('solar-speed-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        const presets = [0.25, 0.5, 1, 2, 5, 10];
        const cur = solarGame.orbitSpeed;
        let nextIdx = 0;
        for (let i = 0; i < presets.length; i++) {
            if (Math.abs(presets[i] - cur) < 0.1) {
                nextIdx = (i + 1) % presets.length;
                break;
            } else if (presets[i] > cur) {
                nextIdx = i;
                break;
            }
        }
        solarGame.setOrbitSpeed(presets[nextIdx]);
    });
    document.getElementById('solar-speed-slider')?.addEventListener('input', (e) => {
        solarGame.setOrbitSpeed(parseFloat(e.target.value));
    });
    document.querySelectorAll('.solar-speed-preset').forEach(btn => {
        btn.addEventListener('click', (e) => {
            e.stopPropagation();
            soundFX.playPop();
            const spd = parseFloat(btn.dataset.speed);
            if (!isNaN(spd)) solarGame.setOrbitSpeed(spd);
        });
    });

    // Date Popover inside Drawer (Upgrade 2b)
    document.getElementById('solar-date-toggle-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        const popover = document.getElementById('solar-date-popover');
        if (popover) {
            const isHidden = popover.classList.toggle('hidden');
            if (!isHidden) {
                solarGame.updateOrbitDateUI();
            }
        }
    });
    document.getElementById('solar-date-close-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        document.getElementById('solar-date-popover')?.classList.add('hidden');
    });
    document.getElementById('solar-date-input')?.addEventListener('change', e => {
        if (e.target.value) solarGame.goToDate(e.target.value + 'T12:00:00Z', true);
    });
    document.getElementById('solar-today-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        solarGame.jumpToday();
    });

    // Solar Navigation Arrows (Item 3)
    document.getElementById('solar-prev-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        soundFX.playPop();
        solarGame.stepBody(-1);
    });
    document.getElementById('solar-next-btn')?.addEventListener('click', (e) => {
        e.stopPropagation();
        soundFX.playPop();
        solarGame.stepBody(1);
    });

    // Pre-cache Tier Select listener (Upgrade 1)
    document.getElementById('precache-tier-select')?.addEventListener('change', (e) => {
        safeSetStorage('tlh_precache_tier', e.target.value);
        precacheManager.updateUI();
    });

    document.getElementById('solar-photo-container').addEventListener('click', () => solarGame.triggerAction());
    document.getElementById('solar-action-btn').addEventListener('click', () => solarGame.triggerAction());
    document.getElementById('solar-fact').addEventListener('click', () => solarGame.triggerAction());

    // 15. Cross-tab & Multi-app Audio Isolation & Silent Mode Session Resumption
    const pauseAllAudio = () => {
        soundFX.stopAll();
        geminiTTS.stop();
        if ('speechSynthesis' in window) {
            try { window.speechSynthesis.cancel(); } catch (e) {}
        }
    };
    document.addEventListener('visibilitychange', () => {
        if (document.hidden) {
            pauseAllAudio();
        } else if (document.visibilityState === 'visible') {
            if (soundFX.ctx && soundFX.ctx.state !== 'running') {
                try { soundFX.ctx.resume().catch(() => {}); } catch (e) {}
            }
            soundFX.audioSessionConfigured = false;
            soundFX.unlockSilentMode();
        }
    });
    window.addEventListener('pagehide', pauseAllAudio);
    window.addEventListener('beforeunload', pauseAllAudio);

    // Persistent lightweight touch/click/key unlock for WebAudio, iOS Silent Mode Bypass & speechSynthesis
    const unlockGestures = ['touchend', 'mouseup', 'click', 'keydown'];
    const handleAudioGestureUnlock = (evt) => {
        const needsAudioUnlock = !soundFX.ctx || soundFX.ctx.state !== 'running' || !soundFX.silentAudioUnlocked || (soundFX.silentAudioEl && soundFX.silentAudioEl.paused);
        if (needsAudioUnlock) {
            soundFX.init();
            soundFX.ensureRunning();
        }
        if (!app._speechWarmedUp && 'speechSynthesis' in window) {
            try {
                if (window.speechSynthesis.paused) window.speechSynthesis.resume();
                const isInteractiveTarget = evt && evt.target && typeof evt.target.closest === 'function' &&
                    Boolean(evt.target.closest('button, .menu-card, #nb-stage-canvas, .nb-dock-tile, [onclick]'));
                if (!isInteractiveTarget && !window.speechSynthesis.speaking && !window.speechSynthesis.pending) {
                    app._speechWarmedUp = true;
                    const u = new SpeechSynthesisUtterance(' ');
                    u.volume = 0;
                    u.rate = 2;
                    window.speechSynthesis.speak(u);
                }
            } catch (e) {}
        }
    };
    unlockGestures.forEach(evt => window.addEventListener(evt, handleAudioGestureUnlock, { capture: true, passive: true }));
});


window.ToddlerLearningHub = {
    app,
    soundFX,
    geminiTTS,
    zoomController,
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
    solarGame,
    precacheManager,
    get numberBlocks() { return window.NumberBlocks; },
    get blocksGame() { return window.NumberBlocks && window.NumberBlocks.Game; }
};
})();

    </script>

    <!-- FLOATING BACKGROUND PRE-CACHE STATUS PILL -->
    <div id="precache-floating-pill" class="hidden fixed bottom-3 right-3 sm:bottom-4 sm:right-4 z-40 bg-slate-900/95 text-white px-3.5 py-2 rounded-2xl shadow-xl backdrop-blur-md border border-slate-700/80 flex items-center gap-2.5 text-xs font-bold transition-all duration-300">
        <span class="text-amber-400 animate-pulse text-base">⚡</span>
        <div class="flex flex-col">
            <span id="precache-pill-title" class="font-black text-amber-300 text-[11px] leading-tight">Caching: 0/0 (0%)</span>
            <span id="precache-pill-sub" class="text-[10px] text-slate-300 leading-tight">Tier 2 Turbo (~90 RPM)</span>
        </div>
        <div class="flex items-center gap-1 ml-1">
            <button id="precache-pill-pause-btn" type="button" class="px-2 py-1 bg-slate-800 hover:bg-slate-700 text-slate-200 rounded-lg text-[10px] font-black border border-slate-600 squish-btn" title="Pause / Resume">⏸️</button>
            <button id="precache-pill-settings-btn" type="button" class="px-2 py-1 bg-slate-800 hover:bg-slate-700 text-slate-200 rounded-lg text-[10px] font-black border border-slate-600 squish-btn" title="Open Voice Options">⚙️</button>
        </div>
    </div>
    <script>
/**
 * Toddler Learning Hub — Number Blocks Module
 * nb-data-audio.js: Character Bible, Schemas, Challenges, and Woody Marimba Synth / Audio Engine
 *
 * Implements:
 *   window.NumberBlocks.Data:
 *     - STORAGE_KEYS: Local storage persistence keys
 *     - PALETTES: Pre-resolved 2.5D block palettes (light, base, deep, shadow, border, borderWidthScale)
 *     - getCharacter(n): Uniform schema for 1..20 (cells, face anchor, animations, lines, bonds)
 *     - CHALLENGES: 12 curated progressive challenges (merge & split)
 *     - getChallenges(maxCap): Filtered challenges based on player maxCap setting
 *     - getAdaptiveStepMs(sum): Adaptive block count-up duration
 *     - getWarmupPhrases(): Warmup dictionary for Gemini TTS / speech cache
 *     - Persistence helpers: getUnlocked(), isUnlocked(n), unlockCharacter(n), unlockAll(), getStars(), addStar(), resetData()
 *
 *   window.NumberBlocks.Audio:
 *     - SCALE_FREQS: 20-step C-major scale frequencies (C4 to A6)
 *     - unlock(): Initializes and unlocks Web Audio on user gesture
 *     - playMarimbaNote(step1Based, delaySec): 3-component woody marimba tone on TLH.soundFX.ctx
 *     - playCountNote(stepIndex, totalSteps): Alias/helper for sequential count-up
 *     - playPickup(): Crisp rising pop on block pickup / tray spawn
 *     - playSnapHover(): Soft celestial 5th shimmer with 380ms leading-edge throttle
 *     - playLand(n): Soft gravity drop slide + subtle marimba root
 *     - playMergeFanfare(sum): 4-beat rising triad arpeggio + rocket whoosh for 10/20
 *     - playSplitReady(): Bubbly double-blip when hold-to-split threshold reached
 *     - playSplitPop(partA, partB): Cork pop + double marimba chord
 *     - playUnlockJingle(): 5-note sparkling treasure arpeggio for new character discovery
 *     - playHighFiveBounce(): Supernova bounce fanfare when sum > maxCap
 *     - playLockedClueChime(): Gentle bell chime for silhouette clue
 *     - playChallengeWin(): Victory fanfare & 3 star chimes
 *     - speak(text, priority): TTS speech wrapper with 650ms leading tap debounce & blocks-view guard
 *     - speakOpenIntro(), speakMerge(a,b,sum), speakSplit(w,a,b), speakTap(n), speakSupernova(maxCap)
 */
(function () {
  'use strict';

  const NB = (window.NumberBlocks = window.NumberBlocks || {});

  // =========================================================================
  // 1. STORAGE KEYS & PERSISTENCE
  // =========================================================================

  const STORAGE_KEYS = Object.freeze({
    unlocked: 'tlh_isolated_v3_nb_unlocked',
    stars: 'tlh_isolated_v3_nb_stars'
  });

  function safeGetStorage(key) {
    try {
      if (typeof localStorage !== 'undefined') {
        return localStorage.getItem(key);
      }
    } catch (e) {}
    return null;
  }

  function safeSetStorage(key, value) {
    try {
      if (typeof localStorage !== 'undefined') {
        localStorage.setItem(key, value);
      }
    } catch (e) {}
  }

  function safeRemoveStorage(key) {
    try {
      if (typeof localStorage !== 'undefined') {
        localStorage.removeItem(key);
      }
    } catch (e) {}
  }

  // =========================================================================
  // 2. PALETTES (Resolved PaletteObj: light, base, deep, shadow, border, scale)
  // Drop-in replacement for index.html lines 10034-10572 inside NB.Data
  // =========================================================================

  const palViolet = Object.freeze({
    light: '#c084fc',
    base: '#9333ea',
    deep: '#7e22ce',
    shadow: '#581c87',
    border: '#6b21a8',
    borderWidthScale: 1.0
  });

  const palGreyMid = Object.freeze({
    light: '#cbd5e1',
    base: '#94a3b8',
    deep: '#64748b',
    shadow: '#334155',
    border: '#475569',
    borderWidthScale: 1.0
  });

  const PALETTES = Object.freeze({
    1: Object.freeze({
      light: '#f87171',
      base: '#ef4444',
      deep: '#dc2626',
      shadow: '#991b1b',
      border: '#b91c1c',
      borderWidthScale: 1.0
    }),
    2: Object.freeze({
      light: '#fbbf24',
      base: '#f97316',
      deep: '#ea580c',
      shadow: '#9a3412',
      border: '#c2410c',
      borderWidthScale: 1.0
    }),
    3: Object.freeze({
      light: '#fef08a',
      base: '#facc15',
      deep: '#eab308',
      shadow: '#a16207',
      border: '#ca8a04',
      borderWidthScale: 1.0
    }),
    4: Object.freeze({
      light: '#86efac',
      base: '#4ade80',
      deep: '#22c55e',
      shadow: '#14532d',
      border: '#15803d',
      borderWidthScale: 1.0
    }),
    5: Object.freeze({
      light: '#67e8f9',
      base: '#22d3ee',
      deep: '#06b6d4',
      shadow: '#0369a1',
      border: '#0284c7',
      borderWidthScale: 1.0
    }),
    6: Object.freeze({
      light: '#a5b4fc',
      base: '#6366f1',
      deep: '#4f46e5',
      shadow: '#3730a3',
      border: '#4c1d95',
      borderWidthScale: 1.0
    }),
    7: palViolet,
    green7: Object.freeze({
      light: '#86efac',
      base: '#22c55e',
      deep: '#16a34a',
      shadow: '#14532d',
      border: '#15803d',
      borderWidthScale: 1.0
    }),
    skyCyan: Object.freeze({
      light: '#7dd3fc',
      base: '#38bdf8',
      deep: '#0ea5e9',
      shadow: '#0369a1',
      border: '#0284c7',
      borderWidthScale: 1.0
    }),
    indigo: Object.freeze({
      light: '#818cf8',
      base: '#4f46e5',
      deep: '#4338ca',
      shadow: '#312e81',
      border: '#312e81',
      borderWidthScale: 1.0
    }),
    violet: palViolet,
    8: Object.freeze({
      light: '#f472b6',
      base: '#ec4899',
      deep: '#db2777',
      shadow: '#831843',
      border: '#9d174d',
      borderWidthScale: 1.0
    }),
    greyDark: Object.freeze({
      light: '#94a3b8',
      base: '#64748b',
      deep: '#475569',
      shadow: '#1e293b',
      border: '#334155',
      borderWidthScale: 1.0
    }),
    greyMid: palGreyMid,
    9: palGreyMid,
    greyLight: Object.freeze({
      light: '#e2e8f0',
      base: '#cbd5e1',
      deep: '#94a3b8',
      shadow: '#475569',
      border: '#64748b',
      borderWidthScale: 1.0
    }),
    10: Object.freeze({
      light: '#ffffff',
      base: '#ffffff',
      deep: '#e2e8f0',
      shadow: '#dc2626',
      border: '#ef4444',
      borderWidthScale: 1.35
    }),
    20: Object.freeze({
      light: '#ffedd5',
      base: '#fed7aa',
      deep: '#fdba74',
      shadow: '#c2410c',
      border: '#ea580c',
      borderWidthScale: 1.2
    })
  });

  // =========================================================================
  // 3. NUMBER NAMES & CORE CHARACTER SPECS (1..20)
  // =========================================================================

  const NUMBER_NAMES = Object.freeze({
    1: 'One',
    2: 'Two',
    3: 'Three',
    4: 'Four',
    5: 'Five',
    6: 'Six',
    7: 'Seven',
    8: 'Eight',
    9: 'Nine',
    10: 'Ten',
    11: 'Eleven',
    12: 'Twelve',
    13: 'Thirteen',
    14: 'Fourteen',
    15: 'Fifteen',
    16: 'Sixteen',
    17: 'Seventeen',
    18: 'Eighteen',
    19: 'Nineteen',
    20: 'Twenty'
  });

  const CHARACTER_CACHE = new Map();

  function buildCharacter(n) {
    if (n < 1 || n > 20) return null;

    if (n === 1) {
      return Object.freeze({
        n: 1,
        name: 'One',
        cols: 1,
        rows: 1,
        unitScale: 1.0,
        primaryColor: '#ef4444',
        cells: Object.freeze([
          Object.freeze({ col: 0, row: 0, palette: PALETTES[1], pip: false, starBtn: false })
        ]),
        face: Object.freeze({ type: 'cyclops', anchorCol: 0.5, anchorRow: 0.52 }),
        tapAnim: 'flip1',
        mergeLine: 'One!',
        tapLines: Object.freeze([
          'One! One wonderful block!',
          'Boing! I am One!',
          "One! Let's find a friend!"
        ]),
        splitBonds: Object.freeze([]),
        lockedHint: ''
      });
    }

    if (n === 2) {
      return Object.freeze({
        n: 2,
        name: 'Two',
        cols: 1,
        rows: 2,
        unitScale: 1.0,
        primaryColor: '#f97316',
        cells: Object.freeze([
          Object.freeze({ col: 0, row: 0, palette: PALETTES[2], pip: false, starBtn: false }),
          Object.freeze({ col: 0, row: 1, palette: PALETTES[2], pip: false, starBtn: false })
        ]),
        face: Object.freeze({ type: 'glasses', anchorCol: 0.5, anchorRow: 1.48 }),
        tapAnim: 'dance2',
        mergeLine: 'Two! One, two, dancing shoes!',
        tapLines: Object.freeze([
          "Two! Let's dance, one, two!",
          'Everything is better in twos!',
          'Tap, tap! I am Two!'
        ]),
        splitBonds: Object.freeze([[1, 1]]),
        lockedHint: ''
      });
    }

    if (n === 3) {
      return Object.freeze({
        n: 3,
        name: 'Three',
        cols: 1,
        rows: 3,
        unitScale: 1.0,
        primaryColor: '#facc15',
        cells: Object.freeze([
          Object.freeze({ col: 0, row: 0, palette: PALETTES[3], pip: false, starBtn: false }),
          Object.freeze({ col: 0, row: 1, palette: PALETTES[3], pip: false, starBtn: true }),
          Object.freeze({ col: 0, row: 2, palette: PALETTES[3], pip: false, starBtn: false })
        ]),
        face: Object.freeze({ type: 'crown', anchorCol: 0.5, anchorRow: 2.48 }),
        tapAnim: 'juggle3',
        mergeLine: 'Three! One, two, three, look at me!',
        tapLines: Object.freeze([
          'Three! Watch me juggle three balls!',
          'One, two, three, ta-da!',
          'Three is the magic number!'
        ]),
        splitBonds: Object.freeze([[2, 1]]),
        lockedHint: ''
      });
    }

    if (n === 4) {
      return Object.freeze({
        n: 4,
        name: 'Four',
        cols: 2,
        rows: 2,
        unitScale: 1.0,
        primaryColor: '#22c55e',
        cells: Object.freeze([
          Object.freeze({ col: 0, row: 0, palette: PALETTES[4], pip: false, starBtn: false }),
          Object.freeze({ col: 1, row: 0, palette: PALETTES[4], pip: false, starBtn: false }),
          Object.freeze({ col: 0, row: 1, palette: PALETTES[4], pip: false, starBtn: false }),
          Object.freeze({ col: 1, row: 1, palette: PALETTES[4], pip: false, starBtn: false })
        ]),
        face: Object.freeze({ type: 'square', anchorCol: 1.0, anchorRow: 1.48 }),
        tapAnim: 'square4',
        mergeLine: "Four! I'm a square!",
        tapLines: Object.freeze([
          'Four! Four sides and four corners!',
          'Two by two makes Square Four!',
          'I love being a strong green square!'
        ]),
        splitBonds: Object.freeze([[2, 2], [3, 1]]),
        lockedHint: ''
      });
    }

    if (n === 5) {
      const cells5 = [];
      for (let r = 0; r < 5; r++) {
        cells5.push(Object.freeze({ col: 0, row: r, palette: PALETTES[5], pip: false, starBtn: false }));
      }
      return Object.freeze({
        n: 5,
        name: 'Five',
        cols: 1,
        rows: 5,
        unitScale: 1.0,
        primaryColor: '#22d3ee',
        cells: Object.freeze(cells5),
        face: Object.freeze({ type: 'starLeft', anchorCol: 0.5, anchorRow: 4.48 }),
        tapAnim: 'highFive5',
        mergeLine: 'Five! High five!',
        tapLines: Object.freeze([
          'Up high, give me five!',
          'Five! One, two, three, four, five!',
          "Five! I'm a superstar!"
        ]),
        splitBonds: Object.freeze([[3, 2], [4, 1]]),
        lockedHint: ''
      });
    }

    if (n === 6) {
      const cells6 = [
        Object.freeze({ col: 0, row: 0, palette: PALETTES[6], pip: true, starBtn: false }),
        Object.freeze({ col: 1, row: 0, palette: PALETTES[6], pip: true, starBtn: false }),
        Object.freeze({ col: 0, row: 1, palette: PALETTES[6], pip: true, starBtn: false }),
        Object.freeze({ col: 1, row: 1, palette: PALETTES[6], pip: true, starBtn: false }),
        Object.freeze({ col: 0, row: 2, palette: PALETTES[6], pip: true, starBtn: false }),
        Object.freeze({ col: 1, row: 2, palette: PALETTES[6], pip: true, starBtn: false })
      ];
      return Object.freeze({
        n: 6,
        name: 'Six',
        cols: 2,
        rows: 3,
        unitScale: 1.0,
        primaryColor: '#6366f1',
        cells: Object.freeze(cells6),
        face: Object.freeze({ type: 'dice', anchorCol: 1.0, anchorRow: 2.48 }),
        tapAnim: 'dice6',
        mergeLine: "Six! Let's roll the dice!",
        tapLines: Object.freeze([
          'Six! Count my six spots!',
          "Roll the dice, it's Six!",
          'Six! Ready to play a game!'
        ]),
        splitBonds: Object.freeze([[3, 3], [4, 2], [5, 1]]),
        lockedHint: 'Can you make Six? Try Five plus One!'
      });
    }

    if (n === 7) {
      const rainbowPalettes = [
        PALETTES[1],
        PALETTES[2],
        PALETTES[3],
        PALETTES.green7,
        PALETTES.skyCyan,
        PALETTES.indigo,
        PALETTES.violet
      ];
      const cells7 = rainbowPalettes.map((pal, r) =>
        Object.freeze({ col: 0, row: r, palette: pal, pip: false, starBtn: false })
      );
      return Object.freeze({
        n: 7,
        name: 'Seven',
        cols: 1,
        rows: 7,
        unitScale: 0.86,
        primaryColor: '#9333ea',
        cells: Object.freeze(cells7),
        face: Object.freeze({ type: 'rainbow', anchorCol: 0.5, anchorRow: 6.48 }),
        tapAnim: 'rainbow7',
        mergeLine: 'Seven! Lucky rainbow Seven!',
        tapLines: Object.freeze([
          'Seven! Seven rainbow colors!',
          'How lucky! I am Seven!',
          'Count my rainbow, one to seven!'
        ]),
        splitBonds: Object.freeze([[4, 3], [5, 2], [6, 1]]),
        lockedHint: 'Can you make Rainbow Seven? Try Five plus Two!'
      });
    }

    if (n === 8) {
      const cells8 = [];
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 2; c++) {
          cells8.push(Object.freeze({ col: c, row: r, palette: PALETTES[8], pip: false, starBtn: false }));
        }
      }
      return Object.freeze({
        n: 8,
        name: 'Eight',
        cols: 2,
        rows: 4,
        unitScale: 1.0,
        primaryColor: '#ec4899',
        cells: Object.freeze(cells8),
        face: Object.freeze({ type: 'octoMask', anchorCol: 1.0, anchorRow: 3.48 }),
        tapAnim: 'octo8',
        mergeLine: 'Eight! Octoblock to the rescue!',
        tapLines: Object.freeze([
          'Eight! Wiggle all eight arms!',
          'Octoblock, strong and super!',
          'Two fours make super Eight!'
        ]),
        splitBonds: Object.freeze([[4, 4], [5, 3], [6, 2], [7, 1]]),
        lockedHint: 'Can you make Octoblock Eight? Try Four plus Four!'
      });
    }

    if (n === 9) {
      const rowPalettes9 = [PALETTES.greyDark, PALETTES.greyMid, PALETTES.greyLight];
      const cells9 = [];
      for (let r = 0; r < 3; r++) {
        for (let c = 0; c < 3; c++) {
          cells9.push(Object.freeze({ col: c, row: r, palette: rowPalettes9[r], pip: false, starBtn: false }));
        }
      }
      return Object.freeze({
        n: 9,
        name: 'Nine',
        cols: 3,
        rows: 3,
        unitScale: 1.0,
        primaryColor: '#64748b',
        cells: Object.freeze(cells9),
        face: Object.freeze({ type: 'squareSpecs', anchorCol: 1.5, anchorRow: 2.48 }),
        tapAnim: 'sneeze9',
        mergeLine: 'Nine! Three by three, a big square!',
        tapLines: Object.freeze([
          "Ah, ah, achoo! Haha, I'm Nine!",
          'Nine! Three rows of three!',
          "I'm a big proud square, Nine!"
        ]),
        // Explicit frozen order per blueprint #12 §3.2
        splitBonds: Object.freeze([[6, 3], [5, 4], [7, 2], [8, 1]]),
        lockedHint: 'Can you make Square Nine? Try Five plus Four!'
      });
    }

    if (n === 10) {
      const cells10 = [];
      for (let r = 0; r < 5; r++) {
        for (let c = 0; c < 2; c++) {
          cells10.push(Object.freeze({ col: c, row: r, palette: PALETTES[10], pip: false, starBtn: false }));
        }
      }
      return Object.freeze({
        n: 10,
        name: 'Ten',
        cols: 2,
        rows: 5,
        unitScale: 1.0,
        primaryColor: '#ef4444',
        cells: Object.freeze(cells10),
        face: Object.freeze({ type: 'starTwin', anchorCol: 1.0, anchorRow: 4.48 }),
        tapAnim: 'rocket10',
        mergeLine: 'Ten! Ten blocks, blast off!',
        tapLines: Object.freeze([
          "Three, two, one, blast off! I'm Ten!",
          'Ten! Two fives make a big Ten!',
          'Zoom to the stars! I am Ten!'
        ]),
        splitBonds: Object.freeze([[5, 5], [6, 4], [7, 3], [8, 2], [9, 1]]),
        lockedHint: 'Can you build Rocket Ten? Try Five plus Five!'
      });
    }

    // Twelve: Canonical 3x4 Super-Rectangle (10 white/red + 2 orange)
    if (n === 12) {
      const cells12 = [];
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 3; c++) {
          const isOrangeTwo = (c === 2 && r >= 2);
          cells12.push(Object.freeze({
            col: c,
            row: r,
            palette: isOrangeTwo ? PALETTES[2] : PALETTES[10],
            pip: false,
            starBtn: false
          }));
        }
      }
      return Object.freeze({
        n: 12,
        name: 'Twelve',
        cols: 3,
        rows: 4,
        unitScale: 0.86,
        primaryColor: '#f97316',
        cells: Object.freeze(cells12),
        face: Object.freeze({ type: 'superRect12', anchorCol: 1.5, anchorRow: 3.45 }),
        tapAnim: 'teenPulse',
        mergeLine: 'Twelve! Ten and Two make Twelve!',
        tapLines: Object.freeze([
          'Twelve! I am a Super Rectangle!',
          'Three by four makes Twelve!',
          'Ten and Two is Twelve!'
        ]),
        splitBonds: Object.freeze([[10, 2], [6, 6]]),
        lockedHint: ''
      });
    }

    // Procedural compound teens: 11, 13..19
    if (n >= 11 && n <= 19) {
      const unitN = n - 10;
      const unitChar = getCharacter(unitN);
      const name = NUMBER_NAMES[n];
      const unitWord = NUMBER_NAMES[unitN];

      const cols = 2 + unitChar.cols;
      const rows = Math.max(5, unitChar.rows);
      const unitScale = 0.78;
      const primaryColor = unitChar.primaryColor;

      const cells = [];
      // Ten column: cols 0..1, rows 0..4
      for (let r = 0; r < 5; r++) {
        for (let c = 0; c < 2; c++) {
          cells.push({ col: c, row: r, palette: PALETTES[10], pip: false, starBtn: false });
        }
      }
      // Unit columns: shifted by col + 2
      unitChar.cells.forEach(uc => {
        cells.push({
          col: uc.col + 2,
          row: uc.row,
          palette: uc.palette,
          pip: !!uc.pip,
          starBtn: !!uc.starBtn
        });
      });

      // Sort cells bottom-to-top: row ascending, then col ascending
      cells.sort((a, b) => (a.row === b.row ? a.col - b.col : a.row - b.row));

      return Object.freeze({
        n,
        name,
        cols,
        rows,
        unitScale,
        primaryColor,
        cells: Object.freeze(cells.map(c => Object.freeze(c))),
        face: Object.freeze({ type: 'teenCompound', unitN: unitN, anchorCol: 1.0, anchorRow: 4.48 }),
        tapAnim: 'teenPulse',
        mergeLine: `${name}! Ten and ${unitWord} make ${name}!`,
        tapLines: Object.freeze([
          `${name}! Ten and ${unitWord} make ${name}!`,
          `I am ${name}! One big Ten plus ${unitWord}!`,
          `Count with me, Ten and ${unitWord} is ${name}!`
        ]),
        splitBonds: Object.freeze([
          [10, unitN],
          [Math.ceil(n / 2), Math.floor(n / 2)]
        ]),
        lockedHint: ''
      });
    }

    // Big Twenty: 20 (4x5 double Ten in Warm Pale-Apricot)
    if (n === 20) {
      const cells20 = [];
      for (let r = 0; r < 5; r++) {
        for (let c = 0; c < 4; c++) {
          cells20.push(Object.freeze({ col: c, row: r, palette: PALETTES[20], pip: false, starBtn: false }));
        }
      }
      return Object.freeze({
        n: 20,
        name: 'Twenty',
        cols: 4,
        rows: 5,
        unitScale: 0.78,
        primaryColor: '#ea580c',
        cells: Object.freeze(cells20),
        face: Object.freeze({ type: 'twentyTopHat', anchorCol: 2.0, anchorRow: 4.48 }),
        tapAnim: 'dance20',
        mergeLine: 'Twenty! Two Tens make Twenty!',
        tapLines: Object.freeze([
          'Twenty! Two Tens make Twenty!',
          'Tip my hat, I am Big Twenty!',
          'Ten plus Ten equals Twenty!'
        ]),
        splitBonds: Object.freeze([[10, 10], [15, 5]]),
        lockedHint: ''
      });
    }

    return null;
  }

  function getCharacter(n) {
    const num = Math.round(Number(n));
    if (num < 1 || num > 20) return null;
    if (!CHARACTER_CACHE.has(num)) {
      const charObj = buildCharacter(num);
      if (charObj) CHARACTER_CACHE.set(num, charObj);
    }
    return CHARACTER_CACHE.get(num) || null;
  }

  // Pre-seed 1..20
  for (let i = 1; i <= 20; i++) {
    getCharacter(i);
  }

  // =========================================================================
  // 4. PROGRESSIVE TODDLER CHALLENGES (12 Curated Tasks)
  // =========================================================================

  const CHALLENGES = Object.freeze([
    Object.freeze({
      id: 1,
      type: 'merge',
      target: 2,
      splitParts: null,
      maxRequired: 2,
      spawn: Object.freeze([1, 1]),
      prompt: 'Put One and One together! Make Two!',
      hintText: 'Drag One onto One to make Two!'
    }),
    Object.freeze({
      id: 2,
      type: 'merge',
      target: 3,
      splitParts: null,
      maxRequired: 3,
      spawn: Object.freeze([2, 1]),
      prompt: 'Can you build Three, the juggler?',
      hintText: 'Put Two and One together to make Three!'
    }),
    Object.freeze({
      id: 3,
      type: 'merge',
      target: 4,
      splitParts: null,
      maxRequired: 4,
      spawn: Object.freeze([2, 2]),
      prompt: 'Make Square Four! Four green blocks!',
      hintText: 'Two plus Two makes Square Four!'
    }),
    Object.freeze({
      id: 4,
      type: 'merge',
      target: 5,
      splitParts: null,
      maxRequired: 5,
      spawn: Object.freeze([3, 2]),
      prompt: 'Build Five for a big High Five!',
      hintText: 'Stack Three and Two to make Five!'
    }),
    Object.freeze({
      id: 5,
      type: 'split',
      target: 4,
      splitParts: null,
      maxRequired: 4,
      spawn: Object.freeze([4]),
      prompt: 'Four wants to share! Split Four apart!',
      hintText: 'Tap the split button or stretch Four apart!'
    }),
    Object.freeze({
      id: 6,
      type: 'merge',
      target: 6,
      splitParts: null,
      maxRequired: 6,
      spawn: Object.freeze([3, 3]),
      prompt: 'Roll the dice! Can you build Six?',
      hintText: 'Put Three and Three together to make Six!'
    }),
    Object.freeze({
      id: 7,
      type: 'merge',
      target: 7,
      splitParts: null,
      maxRequired: 7,
      spawn: Object.freeze([5, 2]),
      prompt: 'Make Lucky Rainbow Seven!',
      hintText: 'Five plus Two makes Rainbow Seven!'
    }),
    Object.freeze({
      id: 8,
      type: 'split',
      target: 5,
      splitParts: Object.freeze([2, 3]),
      maxRequired: 5,
      spawn: Object.freeze([5]),
      prompt: 'Can you split Five into Two and Three?',
      hintText: 'Pull Five apart into Two and Three!'
    }),
    Object.freeze({
      id: 9,
      type: 'merge',
      target: 8,
      splitParts: null,
      maxRequired: 8,
      spawn: Object.freeze([4, 4]),
      prompt: 'Who has eight wiggly arms? Build Octoblock Eight!',
      hintText: 'Four plus Four makes Octoblock Eight!'
    }),
    Object.freeze({
      id: 10,
      type: 'merge',
      target: 9,
      splitParts: null,
      maxRequired: 9,
      spawn: Object.freeze([5, 4]),
      prompt: 'Make big Square Nine! Three by three!',
      hintText: 'Combine Five and Four to make Nine!'
    }),
    Object.freeze({
      id: 11,
      type: 'merge',
      target: 10,
      splitParts: null,
      maxRequired: 10,
      spawn: Object.freeze([5, 5]),
      prompt: 'Ready for blast off! Build Rocket Ten!',
      hintText: 'Put Five and Five together for Rocket Ten!'
    }),
    Object.freeze({
      id: 12,
      type: 'merge',
      target: 15,
      splitParts: null,
      maxRequired: 15,
      spawn: Object.freeze([10, 5]),
      prompt: 'Ten plus Five! Can you build Fifteen?',
      hintText: 'Drag Ten and Five together to make Fifteen!'
    })
  ]);

  function getChallenges(maxCap) {
    const cap = (typeof maxCap === 'number' && maxCap > 0) ? maxCap : 20;
    return CHALLENGES.filter(c => c.maxRequired <= cap);
  }

  function getAdaptiveStepMs(sum) {
    const s = Math.max(1, Math.round(Number(sum) || 1));
    return s <= 4 ? 120 : s <= 7 ? 90 : s <= 10 ? 68 : 44;
  }

  function getWarmupPhrases() {
    const phrases = [
      'Number Blocks!',
      "Number Blocks! Let's build and count!",
      'Yay! You did it!'
    ];
    for (let i = 1; i <= 10; i++) {
      const char = getCharacter(i);
      if (char && char.mergeLine) {
        phrases.push(char.mergeLine);
      }
    }
    return phrases;
  }

  // =========================================================================
  // 5. UNLOCK & STAR PERSISTENCE HELPERS
  // =========================================================================

  function getUnlocked() {
    const set = new Set([1, 2, 3, 4, 5]);
    const raw = safeGetStorage(STORAGE_KEYS.unlocked);
    if (raw) {
      try {
        const arr = JSON.parse(raw);
        if (Array.isArray(arr)) {
          arr.forEach(val => {
            const num = Number(val);
            if (num >= 1 && num <= 20) set.add(num);
          });
        }
      } catch (e) {}
    }
    return set;
  }

  function isUnlocked(n) {
    const num = Number(n);
    if (num <= 5) return true;
    return getUnlocked().has(num);
  }

  function unlockCharacter(n) {
    const num = Number(n);
    if (num < 1 || num > 20) return false;
    const current = getUnlocked();
    if (current.has(num)) return false;
    current.add(num);
    safeSetStorage(STORAGE_KEYS.unlocked, JSON.stringify(Array.from(current)));
    return true;
  }

  function unlockAll() {
    const all = [];
    for (let i = 1; i <= 20; i++) all.push(i);
    safeSetStorage(STORAGE_KEYS.unlocked, JSON.stringify(all));
  }

  function getStars() {
    const raw = safeGetStorage(STORAGE_KEYS.stars);
    const parsed = parseInt(raw, 10);
    return isNaN(parsed) || parsed < 0 ? 0 : parsed;
  }

  function addStar() {
    const next = getStars() + 1;
    safeSetStorage(STORAGE_KEYS.stars, String(next));
    return next;
  }

  function resetData() {
    safeRemoveStorage(STORAGE_KEYS.unlocked);
    safeRemoveStorage(STORAGE_KEYS.stars);
  }

  // Bind NB.Data namespace
  NB.Data = Object.freeze({
    STORAGE_KEYS,
    PALETTES,
    getCharacter,
    CHALLENGES,
    getChallenges,
    getAdaptiveStepMs,
    getWarmupPhrases,
    getUnlocked,
    isUnlocked,
    unlockCharacter,
    unlockAll,
    getStars,
    addStar,
    resetData
  });

  // =========================================================================
  // 6. AUDIO SYNTHESIS & SPEECH ENGINE (NB.Audio)
  // =========================================================================

  // 20-step C-Major Woody Marimba ladder (C4 to A6)
  const SCALE_FREQS = Object.freeze([
    261.63, 293.66, 329.63, 349.23, 392.00, 440.00, 493.88, 523.25,
    587.33, 659.25, 698.46, 783.99, 880.00, 987.77, 1046.50, 1174.66,
    1318.51, 1396.91, 1567.98, 1760.00
  ]);

  function getTLH() {
    return window.ToddlerLearningHub || null;
  }

  function getSoundFX() {
    const tlh = getTLH();
    return (tlh && tlh.soundFX) || (window.soundFX || null);
  }

  function isSfxEnabled() {
    const tlh = getTLH();
    if (tlh && tlh.app && tlh.app.settings && typeof tlh.app.settings.sfxEnabled !== 'undefined') {
      return !!tlh.app.settings.sfxEnabled;
    }
    if (typeof window.app !== 'undefined' && window.app && window.app.settings && typeof window.app.settings.sfxEnabled !== 'undefined') {
      return !!window.app.settings.sfxEnabled;
    }
    return true;
  }

  function isBlocksViewActive() {
    const tlh = getTLH();
    if (tlh && tlh.app && typeof tlh.app.currentView === 'string') {
      return tlh.app.currentView === 'blocks';
    }
    if (typeof window.app !== 'undefined' && window.app && typeof window.app.currentView === 'string') {
      return window.app.currentView === 'blocks';
    }
    return true;
  }

  let sharedCompressor = null;
  let sharedCompressorCtx = null;

  function ensureAudioCtx(sfx) {
    if (!sfx) return null;
    if (typeof sfx.ensureRunning === 'function') {
      try { sfx.ensureRunning(); } catch (e) {}
    } else if (typeof sfx.init === 'function') {
      try { sfx.init(); } catch (e) {}
    }
    return sfx.ctx || null;
  }

  function getOutputNode(ctx) {
    if (!ctx) return null;
    if (sharedCompressorCtx === ctx && sharedCompressor) {
      return sharedCompressor;
    }
    if (typeof ctx.createDynamicsCompressor === 'function') {
      try {
        const comp = ctx.createDynamicsCompressor();
        comp.threshold.setValueAtTime(-12, ctx.currentTime);
        comp.knee.setValueAtTime(12, ctx.currentTime);
        comp.ratio.setValueAtTime(4, ctx.currentTime);
        comp.attack.setValueAtTime(0.003, ctx.currentTime);
        comp.release.setValueAtTime(0.15, ctx.currentTime);
        comp.connect(ctx.destination);
        sharedCompressor = comp;
        sharedCompressorCtx = ctx;
        return comp;
      } catch (e) {}
    }
    return ctx.destination;
  }

  function unlock() {
    const sfx = getSoundFX();
    if (!sfx) return;
    if (typeof sfx.ensureRunning === 'function') {
      try { sfx.ensureRunning(); } catch (e) {}
    }
    if (typeof sfx.init === 'function') {
      try { sfx.init(); } catch (e) {}
    }
  }

  function trackNode(node) {
    const sfx = getSoundFX();
    if (sfx && typeof sfx.trackNode === 'function') {
      sfx.trackNode(node);
    }
  }

  // --- Woody Marimba Synth Bar ---
  function playMarimbaNote(step1Based, delaySec) {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    const step = Math.max(1, Math.min(20, Math.round(Number(step1Based) || 1)));
    const freq = SCALE_FREQS[step - 1] || 261.63;
    const t = ctx.currentTime + Math.max(0, Number(delaySec) || 0);

    try {
      // 1. Primary sine oscillator
      const oscPrimary = ctx.createOscillator();
      const gainPrimary = ctx.createGain();
      const primaryVol = step > 15 ? 0.30 : 0.42;

      oscPrimary.type = 'sine';
      oscPrimary.frequency.setValueAtTime(freq, t);

      gainPrimary.gain.setValueAtTime(0.0001, t);
      gainPrimary.gain.linearRampToValueAtTime(primaryVol, t + 0.004);
      gainPrimary.gain.exponentialRampToValueAtTime(0.0001, t + 0.214);

      oscPrimary.connect(gainPrimary);
      gainPrimary.connect(out);
      trackNode(oscPrimary);
      oscPrimary.start(t);
      oscPrimary.stop(t + 0.24);

      // 2. Harmonic sine oscillator (4x freq hollow rosewood bar resonance)
      const oscHarmonic = ctx.createOscillator();
      const gainHarmonic = ctx.createGain();

      oscHarmonic.type = 'sine';
      oscHarmonic.frequency.setValueAtTime(Math.min(22000, 4 * freq), t);

      gainHarmonic.gain.setValueAtTime(0.0001, t);
      gainHarmonic.gain.linearRampToValueAtTime(0.08, t + 0.002);
      gainHarmonic.gain.exponentialRampToValueAtTime(0.0001, t + 0.047);

      oscHarmonic.connect(gainHarmonic);
      gainHarmonic.connect(out);
      trackNode(oscHarmonic);
      oscHarmonic.start(t);
      oscHarmonic.stop(t + 0.06);

      // 3. Filtered mallet click transient (triangle at 6x freq)
      const oscClick = ctx.createOscillator();
      const gainClick = ctx.createGain();

      oscClick.type = 'triangle';
      oscClick.frequency.setValueAtTime(Math.min(22000, 6 * freq), t);

      gainClick.gain.setValueAtTime(0.0001, t);
      gainClick.gain.linearRampToValueAtTime(0.06, t + 0.001);
      gainClick.gain.exponentialRampToValueAtTime(0.0001, t + 0.013);

      oscClick.connect(gainClick);
      gainClick.connect(out);
      trackNode(oscClick);
      oscClick.start(t);
      oscClick.stop(t + 0.025);
    } catch (e) {}
  }

  function playCountNote(stepIndex, totalSteps) {
    const step = (stepIndex === 0) ? 1 : Math.max(1, Math.min(20, Math.round(Number(stepIndex) || 1)));
    playMarimbaNote(step, 0);
  }

  function playPickup() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    if (sfx && typeof sfx.playSlide === 'function') {
      sfx.playSlide(280, 520, 0.085, 'sine', 0.30);
    } else {
      playMarimbaNote(1, 0);
    }
  }

  function playTapBounce(n) {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    if (sfx && typeof sfx.playSlide === 'function') {
      sfx.playSlide(290, 560, 0.085, 'sine', 0.24);
    }
    const val = Math.max(1, Math.min(20, Math.round(Number(n) || 1)));
    playMarimbaNote(val, 0.015);
  }

  let lastSnapHoverAt = 0;
  function playSnapHover() {
    if (!isSfxEnabled()) return;
    const now = (typeof performance !== 'undefined' ? performance.now() : Date.now());
    if (now - lastSnapHoverAt < 380) return;
    lastSnapHoverAt = now;

    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime;
      const osc1 = ctx.createOscillator();
      const osc2 = ctx.createOscillator();
      const gain = ctx.createGain();

      // Celestial fifth shimmer: G5 (783.99 Hz) + D6 (1174.66 Hz)
      osc1.type = 'sine';
      osc1.frequency.setValueAtTime(783.99, t);
      osc2.type = 'sine';
      osc2.frequency.setValueAtTime(1174.66, t);

      gain.gain.setValueAtTime(0.0001, t);
      gain.gain.linearRampToValueAtTime(0.12, t + 0.01);
      gain.gain.exponentialRampToValueAtTime(0.0001, t + 0.16);

      osc1.connect(gain);
      osc2.connect(gain);
      gain.connect(out);

      trackNode(osc1);
      trackNode(osc2);
      osc1.start(t);
      osc2.start(t);
      osc1.stop(t + 0.18);
      osc2.stop(t + 0.18);
    } catch (e) {}
  }

  function playLand(n) {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    if (sfx && typeof sfx.playSlide === 'function') {
      sfx.playSlide(175, 92, 0.09, 'triangle', 0.26);
    }
    const val = Math.max(1, Math.min(20, Math.round(Number(n) || 1)));
    playMarimbaNote(val, 0.02);
  }

  function playMergeFanfare(sum) {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    const total = Math.max(1, Math.min(20, Math.round(Number(sum) || 1)));

    try {
      const t = ctx.currentTime;
      // Rising major triad arpeggio: C5 -> E5 -> G5 -> Chord [C5, E5, G5, C6]
      const notes = [
        { freq: 523.25, time: t, dur: 0.12, vol: 0.34 },
        { freq: 659.25, time: t + 0.055, dur: 0.12, vol: 0.34 },
        { freq: 783.99, time: t + 0.110, dur: 0.14, vol: 0.38 },
        // Chord
        { freq: 523.25, time: t + 0.165, dur: 0.32, vol: 0.28 },
        { freq: 659.25, time: t + 0.165, dur: 0.32, vol: 0.28 },
        { freq: 783.99, time: t + 0.165, dur: 0.32, vol: 0.30 },
        { freq: 1046.50, time: t + 0.165, dur: 0.35, vol: 0.34 }
      ];

      notes.forEach(n => {
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(n.freq, n.time);

        gain.gain.setValueAtTime(0.0001, n.time);
        gain.gain.linearRampToValueAtTime(n.vol, n.time + 0.008);
        gain.gain.exponentialRampToValueAtTime(0.0001, n.time + n.dur);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(n.time);
        osc.stop(n.time + n.dur + 0.03);
      });

      // Filtered rocket whoosh on 10 or 20
      if ((total === 10 || total === 20) && typeof sfx.playNoise === 'function') {
        sfx.playNoise(0.45, 'bandpass', 650, 1.5, 0.28, 0.16);
      }
    } catch (e) {}
  }

  function playSplitReady() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime;
      // Bubbly double-blip: E5 (659Hz) -> G5 (784Hz)
      const blips = [
        { freq: 659.25, time: t, dur: 0.045 },
        { freq: 783.99, time: t + 0.048, dur: 0.055 }
      ];

      blips.forEach(b => {
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(b.freq, b.time);

        gain.gain.setValueAtTime(0.0001, b.time);
        gain.gain.linearRampToValueAtTime(0.28, b.time + 0.006);
        gain.gain.exponentialRampToValueAtTime(0.0001, b.time + b.dur);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(b.time);
        osc.stop(b.time + b.dur + 0.02);
      });
    } catch (e) {}
  }

  function playSplitPop(partA, partB) {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    if (sfx && typeof sfx.playSlide === 'function') {
      // Playful cork-pop
      sfx.playSlide(680, 310, 0.11, 'sine', 0.36);
    }
    const a = Math.max(1, Math.min(20, Math.round(Number(partA) || 1)));
    const b = Math.max(1, Math.min(20, Math.round(Number(partB) || 1)));
    playMarimbaNote(a, 0.04);
    playMarimbaNote(b, 0.12);
  }

  function playUnlockJingle() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime;
      // Sparkling 5-note treasure arpeggio: C5 - E5 - G5 - B5 - C6
      const notes = [523.25, 659.25, 783.99, 987.77, 1046.50];
      notes.forEach((freq, idx) => {
        const noteTime = t + idx * 0.065;
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(freq, noteTime);

        gain.gain.setValueAtTime(0.0001, noteTime);
        gain.gain.linearRampToValueAtTime(0.28, noteTime + 0.008);
        gain.gain.exponentialRampToValueAtTime(0.0001, noteTime + 0.22);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(noteTime);
        osc.stop(noteTime + 0.25);
      });
    } catch (e) {}
  }

  function playHighFiveBounce() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    if (sfx && typeof sfx.playSlide === 'function') {
      sfx.playSlide(320, 640, 0.12, 'sine', 0.30);
    }
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime + 0.05;
      // Supernova high-five chord: [C5, G5, C6, E6]
      const chord = [523.25, 783.99, 1046.50, 1318.51];
      chord.forEach(freq => {
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(freq, t);

        gain.gain.setValueAtTime(0.0001, t);
        gain.gain.linearRampToValueAtTime(0.22, t + 0.01);
        gain.gain.exponentialRampToValueAtTime(0.0001, t + 0.32);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(t);
        osc.stop(t + 0.35);
      });
    } catch (e) {}
  }

  function playLockedClueChime() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime;
      // High pleasant bell chime: E6 -> G6
      const chimeNotes = [
        { freq: 1318.51, time: t, dur: 0.18 },
        { freq: 1567.98, time: t + 0.07, dur: 0.24 }
      ];

      chimeNotes.forEach(cn => {
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(cn.freq, cn.time);

        gain.gain.setValueAtTime(0.0001, cn.time);
        gain.gain.linearRampToValueAtTime(0.22, cn.time + 0.008);
        gain.gain.exponentialRampToValueAtTime(0.0001, cn.time + cn.dur);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(cn.time);
        osc.stop(cn.time + cn.dur + 0.03);
      });
    } catch (e) {}
  }

  function playChallengeWin() {
    if (!isSfxEnabled()) return;
    const sfx = getSoundFX();
    const ctx = ensureAudioCtx(sfx);
    if (!ctx) return;
    const out = getOutputNode(ctx);

    try {
      const t = ctx.currentTime;
      // Sparkling victory stars: G5 -> C6 -> E6 -> G6
      const winNotes = [783.99, 1046.50, 1318.51, 1567.98];
      winNotes.forEach((freq, idx) => {
        const noteTime = t + idx * 0.075;
        const osc = ctx.createOscillator();
        const gain = ctx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(freq, noteTime);

        gain.gain.setValueAtTime(0.0001, noteTime);
        gain.gain.linearRampToValueAtTime(0.28, noteTime + 0.008);
        gain.gain.exponentialRampToValueAtTime(0.0001, noteTime + 0.28);

        osc.connect(gain);
        gain.connect(out);
        trackNode(osc);
        osc.start(noteTime);
        osc.stop(noteTime + 0.32);
      });
    } catch (e) {}
  }

  // =========================================================================
  // 7. SPEECH ENGINE & TTS DISCIPLINE (TLH.app.speak integration)
  // =========================================================================

  let lastTapSpeakAt = 0;
  const tapIndexMap = Object.create(null);

  function speak(text, priority) {
    if (!text) return;
    if (!isBlocksViewActive()) return;

    const tlh = getTLH();
    const appObj = (tlh && tlh.app) || (typeof window.app !== 'undefined' ? window.app : null);
    if (!appObj || typeof appObj.speak !== 'function') return;

    const now = (typeof performance !== 'undefined' ? performance.now() : Date.now());
    const pri = priority || 'high';

    if (pri === 'tap') {
      // 0ms leading-edge 280ms cooldown on tap speech
      if (now - lastTapSpeakAt < 280) return;
      lastTapSpeakAt = now;
      appObj.speak(text);
    } else {
      // High priority: speak immediately
      lastTapSpeakAt = now;
      appObj.speak(text);
    }
  }

  function speakOpenIntro() {
    speak("Let's build and count!", 'high');
  }

  function speakMerge(a, b, sum, isFirstInSession) {
    const total = Math.max(1, Math.min(20, Math.round(Number(sum) || 1)));
    const char = getCharacter(total);
    const line = char ? char.mergeLine : (total + '!');
    speak(line, 'high');
  }

  function speakSplit(whole, partA, partB) {
    const w = Math.round(Number(whole) || 0);
    const a = Math.round(Number(partA) || 0);
    const b = Math.round(Number(partB) || 0);
    speak(`${w} is ${a} and ${b}!`, 'high');
  }

  function speakTap(n) {
    const num = Math.max(1, Math.min(20, Math.round(Number(n) || 1)));
    const char = getCharacter(num);
    if (!char || !char.tapLines || char.tapLines.length === 0) {
      speak(String(num), 'tap');
      return;
    }
    const idx = (tapIndexMap[num] || 0) % char.tapLines.length;
    tapIndexMap[num] = idx + 1;
    speak(char.tapLines[idx], 'tap');
  }

  function speakSupernova(maxCap) {
    if (maxCap === 10) {
      speak('Whoa, bigger than Ten! Fireworks!', 'high');
    } else {
      speak('Whoa, super big number! Twenty is our biggest rocket!', 'high');
    }
  }

  // Bind NB.Audio namespace
  NB.Audio = Object.freeze({
    SCALE_FREQS,
    unlock,
    playMarimbaNote,
    playCountNote,
    playPickup,
    playTapBounce,
    playSnapHover,
    playLand,
    playMergeFanfare,
    playSplitReady,
    playSplitPop,
    playUnlockJingle,
    playHighFiveBounce,
    playLockedClueChime,
    playChallengeWin,
    speak,
    speakOpenIntro,
    speakMerge,
    speakSplit,
    speakTap,
    speakSupernova
  });

})();

    </script>
    <script>
/* ==========================================================================
   nb-renderer.js - Number Blocks 60fps Retina CBeebies Character Stage Renderer
   Toddler Learning Hub - Scoped to window.NumberBlocks.Renderer
   Drop-in replacement for index.html lines 11319-13085
   ========================================================================== */

(function () {
  'use strict';

  const NB = (window.NumberBlocks = window.NumberBlocks || {});

  // --------------------------------------------------------------------------
  // Math & Path Primitives
  // --------------------------------------------------------------------------
  function clamp(val, min, max) {
    return Math.max(min, Math.min(max, val));
  }

  // Cross-browser roundRect with iOS 15 / older Safari arcTo fallback
  function drawRoundRect(ctx, x, y, w, h, r) {
    if (w <= 0 || h <= 0) return;
    const radius = Math.max(0, Math.min(r, w / 2, h / 2));
    if (ctx.roundRect) {
      ctx.beginPath();
      ctx.roundRect(x, y, w, h, radius);
      return;
    }
    ctx.beginPath();
    ctx.moveTo(x + radius, y);
    ctx.arcTo(x + w, y, x + w, y + h, radius);
    ctx.arcTo(x + w, y + h, x, y + h, radius);
    ctx.arcTo(x, y + h, x, y, radius);
    ctx.arcTo(x, y, x + w, y, radius);
    ctx.closePath();
  }

  function drawStar(ctx, cx, cy, spikes, outerR, innerR, fill, stroke, strokeW) {
    let rot = (Math.PI / 2) * 3;
    let x = cx;
    let y = cy;
    const step = Math.PI / spikes;

    ctx.beginPath();
    ctx.moveTo(cx, cy - outerR);
    for (let i = 0; i < spikes; i++) {
      x = cx + Math.cos(rot) * outerR;
      y = cy + Math.sin(rot) * outerR;
      ctx.lineTo(x, y);
      rot += step;

      x = cx + Math.cos(rot) * innerR;
      y = cy + Math.sin(rot) * innerR;
      ctx.lineTo(x, y);
      rot += step;
    }
    ctx.lineTo(cx, cy - outerR);
    ctx.closePath();

    if (fill) {
      ctx.fillStyle = fill;
      ctx.fill();
    }
    if (stroke) {
      ctx.strokeStyle = stroke;
      ctx.lineWidth = strokeW || 1.5;
      ctx.lineJoin = 'round';
      ctx.stroke();
    }
  }

  // Fast Hex to RGB and Palette Interpolation
  function parseHex(hex) {
    if (!hex || hex[0] !== '#') return [239, 68, 68];
    const clean = hex.slice(1);
    if (clean.length === 3) {
      const r = parseInt(clean[0] + clean[0], 16);
      const g = parseInt(clean[1] + clean[1], 16);
      const b = parseInt(clean[2] + clean[2], 16);
      return [r, g, b];
    }
    const num = parseInt(clean, 16);
    return [(num >> 16) & 255, (num >> 8) & 255, num & 255];
  }

  function lerpHex(hexA, hexB, t) {
    if (!hexA) return hexB || '#ef4444';
    if (!hexB) return hexA || '#ef4444';
    const [r1, g1, b1] = parseHex(hexA);
    const [r2, g2, b2] = parseHex(hexB);
    const r = Math.round(r1 + (r2 - r1) * t);
    const g = Math.round(g1 + (g2 - g1) * t);
    const b = Math.round(b1 + (b2 - b1) * t);
    return 'rgb(' + r + ',' + g + ',' + b + ')';
  }

  function lerpPalette(palA, palB, t) {
    if (!palA) return palB;
    if (!palB) return palA;
    if (t <= 0) return palA;
    if (t >= 1) return palB;
    return {
      light: lerpHex(palA.light, palB.light, t),
      base: lerpHex(palA.base, palB.base, t),
      deep: lerpHex(palA.deep, palB.deep, t),
      shadow: lerpHex(palA.shadow, palB.shadow, t),
      border: lerpHex(palA.border, palB.border, t),
      borderWidthScale: (palA.borderWidthScale || 1.0) + ((palB.borderWidthScale || 1.0) - (palA.borderWidthScale || 1.0)) * t
    };
  }

  // --------------------------------------------------------------------------
  // Canonical Palettes & Fallback Character Bible
  // --------------------------------------------------------------------------
  const PALETTES = {
    1: { light: '#f87171', base: '#ef4444', deep: '#dc2626', shadow: '#991b1b', border: '#b91c1c', borderWidthScale: 1.0 },
    2: { light: '#fbbf24', base: '#f97316', deep: '#ea580c', shadow: '#9a3412', border: '#c2410c', borderWidthScale: 1.0 },
    3: { light: '#fef08a', base: '#facc15', deep: '#eab308', shadow: '#a16207', border: '#ca8a04', borderWidthScale: 1.0 },
    4: { light: '#86efac', base: '#4ade80', deep: '#22c55e', shadow: '#14532d', border: '#15803d', borderWidthScale: 1.0 },
    5: { light: '#67e8f9', base: '#22d3ee', deep: '#06b6d4', shadow: '#0369a1', border: '#0284c7', borderWidthScale: 1.0 },
    6: { light: '#a5b4fc', base: '#6366f1', deep: '#4f46e5', shadow: '#3730a3', border: '#4c1d95', borderWidthScale: 1.0 },
    green7: { light: '#86efac', base: '#22c55e', deep: '#16a34a', shadow: '#14532d', border: '#15803d', borderWidthScale: 1.0 },
    skyCyan: { light: '#7dd3fc', base: '#38bdf8', deep: '#0ea5e9', shadow: '#0369a1', border: '#0284c7', borderWidthScale: 1.0 },
    indigo: { light: '#818cf8', base: '#4f46e5', deep: '#4338ca', shadow: '#312e81', border: '#312e81', borderWidthScale: 1.0 },
    violet: { light: '#c084fc', base: '#9333ea', deep: '#7e22ce', shadow: '#581c87', border: '#6b21a8', borderWidthScale: 1.0 },
    8: { light: '#f472b6', base: '#ec4899', deep: '#db2777', shadow: '#831843', border: '#9d174d', borderWidthScale: 1.0 },
    greyDark: { light: '#94a3b8', base: '#64748b', deep: '#475569', shadow: '#1e293b', border: '#334155', borderWidthScale: 1.0 },
    greyMid: { light: '#cbd5e1', base: '#94a3b8', deep: '#64748b', shadow: '#334155', border: '#475569', borderWidthScale: 1.0 },
    greyLight: { light: '#e2e8f0', base: '#cbd5e1', deep: '#94a3b8', shadow: '#475569', border: '#64748b', borderWidthScale: 1.0 },
    10: { light: '#ffffff', base: '#ffffff', deep: '#e2e8f0', shadow: '#dc2626', border: '#ef4444', borderWidthScale: 1.35 },
    20: { light: '#ffedd5', base: '#fed7aa', deep: '#fdba74', shadow: '#c2410c', border: '#ea580c', borderWidthScale: 1.2 }
  };

  function getFallbackCharacter(n) {
    const num = Math.max(1, Math.min(20, Math.floor(n) || 1));
    if (num === 1) {
      return {
        n: 1, name: 'One', cols: 1, rows: 1, unitScale: 1.0, primaryColor: '#ef4444',
        cells: [{ col: 0, row: 0, palette: PALETTES[1], pip: false, starBtn: false }],
        face: { type: 'cyclops', anchorCol: 0.5, anchorRow: 0.52 }, tapAnim: 'flip1'
      };
    }
    if (num === 2) {
      return {
        n: 2, name: 'Two', cols: 1, rows: 2, unitScale: 1.0, primaryColor: '#f97316',
        cells: [
          { col: 0, row: 0, palette: PALETTES[2], pip: false, starBtn: false },
          { col: 0, row: 1, palette: PALETTES[2], pip: false, starBtn: false }
        ],
        face: { type: 'glasses', anchorCol: 0.5, anchorRow: 1.48 }, tapAnim: 'dance2'
      };
    }
    if (num === 3) {
      return {
        n: 3, name: 'Three', cols: 1, rows: 3, unitScale: 1.0, primaryColor: '#facc15',
        cells: [
          { col: 0, row: 0, palette: PALETTES[3], pip: false, starBtn: false },
          { col: 0, row: 1, palette: PALETTES[3], pip: false, starBtn: true },
          { col: 0, row: 2, palette: PALETTES[3], pip: false, starBtn: false }
        ],
        face: { type: 'crown', anchorCol: 0.5, anchorRow: 2.48 }, tapAnim: 'juggle3'
      };
    }
    if (num === 4) {
      return {
        n: 4, name: 'Four', cols: 2, rows: 2, unitScale: 1.0, primaryColor: '#22c55e',
        cells: [
          { col: 0, row: 0, palette: PALETTES[4] }, { col: 1, row: 0, palette: PALETTES[4] },
          { col: 0, row: 1, palette: PALETTES[4] }, { col: 1, row: 1, palette: PALETTES[4] }
        ],
        face: { type: 'square', anchorCol: 1.0, anchorRow: 1.48 }, tapAnim: 'square4'
      };
    }
    if (num === 5) {
      const cells = [];
      for (let r = 0; r < 5; r++) cells.push({ col: 0, row: r, palette: PALETTES[5] });
      return {
        n: 5, name: 'Five', cols: 1, rows: 5, unitScale: 1.0, primaryColor: '#22d3ee',
        cells: cells,
        face: { type: 'starLeft', anchorCol: 0.5, anchorRow: 4.48 }, tapAnim: 'highFive5'
      };
    }
    if (num === 6) {
      const cells = [];
      for (let r = 0; r < 3; r++) {
        for (let c = 0; c < 2; c++) cells.push({ col: c, row: r, palette: PALETTES[6], pip: true });
      }
      return {
        n: 6, name: 'Six', cols: 2, rows: 3, unitScale: 1.0, primaryColor: '#6366f1',
        cells: cells,
        face: { type: 'dice', anchorCol: 1.0, anchorRow: 2.48 }, tapAnim: 'dice6'
      };
    }
    if (num === 7) {
      const rainbowPals = [PALETTES[1], PALETTES[2], PALETTES[3], PALETTES.green7, PALETTES.skyCyan, PALETTES.indigo, PALETTES.violet];
      const cells = [];
      for (let r = 0; r < 7; r++) cells.push({ col: 0, row: r, palette: rainbowPals[r] });
      return {
        n: 7, name: 'Seven', cols: 1, rows: 7, unitScale: 0.86, primaryColor: '#9333ea',
        cells: cells,
        face: { type: 'rainbow', anchorCol: 0.5, anchorRow: 6.48 }, tapAnim: 'rainbow7'
      };
    }
    if (num === 8) {
      const cells = [];
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 2; c++) cells.push({ col: c, row: r, palette: PALETTES[8] });
      }
      return {
        n: 8, name: 'Eight', cols: 2, rows: 4, unitScale: 1.0, primaryColor: '#ec4899',
        cells: cells,
        face: { type: 'octoMask', anchorCol: 1.0, anchorRow: 3.48 }, tapAnim: 'octo8'
      };
    }
    if (num === 9) {
      const greyPals = [PALETTES.greyDark, PALETTES.greyMid, PALETTES.greyLight];
      const cells = [];
      for (let r = 0; r < 3; r++) {
        for (let c = 0; c < 3; c++) cells.push({ col: c, row: r, palette: greyPals[r] });
      }
      return {
        n: 9, name: 'Nine', cols: 3, rows: 3, unitScale: 1.0, primaryColor: '#64748b',
        cells: cells,
        face: { type: 'squareSpecs', anchorCol: 1.5, anchorRow: 2.48 }, tapAnim: 'sneeze9'
      };
    }
    if (num === 10) {
      const cells = [];
      for (let r = 0; r < 5; r++) {
        for (let c = 0; c < 2; c++) cells.push({ col: c, row: r, palette: PALETTES[10] });
      }
      return {
        n: 10, name: 'Ten', cols: 2, rows: 5, unitScale: 1.0, primaryColor: '#ef4444',
        cells: cells,
        face: { type: 'starTwin', anchorCol: 1.0, anchorRow: 4.48 }, tapAnim: 'rocket10'
      };
    }
    if (num === 12) {
      const cells = [];
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 3; c++) {
          cells.push({ col: c, row: r, palette: (c === 2 && r >= 2) ? PALETTES[2] : PALETTES[10] });
        }
      }
      return {
        n: 12, name: 'Twelve', cols: 3, rows: 4, unitScale: 0.86, primaryColor: '#f97316',
        cells: cells,
        face: { type: 'superRect12', anchorCol: 1.5, anchorRow: 3.45 }, tapAnim: 'teenPulse'
      };
    }
    if (num >= 11 && num <= 19) {
      const unit = num - 10;
      const unitChar = getFallbackCharacter(unit);
      const cells = [];
      for (let r = 0; r < 5; r++) {
        for (let c = 0; c < 2; c++) cells.push({ col: c, row: r, palette: PALETTES[10] });
      }
      for (let i = 0; i < unitChar.cells.length; i++) {
        const uCell = unitChar.cells[i];
        cells.push({ col: uCell.col + 2, row: uCell.row, palette: uCell.palette, pip: uCell.pip, starBtn: uCell.starBtn });
      }
      const cols = 2 + unitChar.cols;
      const rows = Math.max(5, unitChar.rows);
      return {
        n: num, name: 'Teen' + num, cols: cols, rows: rows, unitScale: 0.78, primaryColor: unitChar.primaryColor,
        cells: cells,
        face: { type: 'teenCompound', unitN: unit, anchorCol: 1.0, anchorRow: 4.48 }, tapAnim: 'teenPulse'
      };
    }
    // 20 Big Twenty
    const cells = [];
    for (let r = 0; r < 5; r++) {
      for (let c = 0; c < 4; c++) cells.push({ col: c, row: r, palette: PALETTES[20] });
    }
    return {
      n: 20, name: 'Twenty', cols: 4, rows: 5, unitScale: 0.78, primaryColor: '#ea580c',
      cells: cells,
      face: { type: 'twentyTopHat', anchorCol: 2.0, anchorRow: 4.48 }, tapAnim: 'dance20'
    };
  }

  function getCharacter(n) {
    if (NB.Data && typeof NB.Data.getCharacter === 'function') {
      const char = NB.Data.getCharacter(n);
      if (char) return char;
    }
    return getFallbackCharacter(n);
  }

  // --------------------------------------------------------------------------
  // Character Layout & Limb Geometry Helpers
  // --------------------------------------------------------------------------
  function getLegHeight(u) {
    return u * 0.24;
  }

  function getHeadgearHeight(n, u) {
    if (n === 3) return u * 0.44;
    if (n === 6) return u * 0.24;
    if (n === 7) return u * 0.42;
    if (n === 20) return u * 0.68;
    return 0;
  }

  function getLimbStyle(n) {
    switch (n) {
      case 1: return { armColor: '#991b1b', legColor: '#991b1b', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 2: return { armColor: '#6b21a8', legColor: '#6b21a8', shoeStyle: 'twoToneOrange', gloveStyle: 'mitt' };
      case 3: return { armColor: '#9f1239', legColor: '#9f1239', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 4: return { armColor: '#14532d', legColor: '#14532d', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 5: return { armColor: '#1e3a8a', legColor: '#1e3a8a', shoeStyle: 'standard', gloveStyle: 'highFive5' };
      case 6: return { armColor: '#9d174d', legColor: '#9d174d', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 7: return { armColor: '#6b21a8', legColor: '#6b21a8', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 8: return { armColor: '#ec4899', legColor: '#ec4899', shoeStyle: 'tentacle8', gloveStyle: 'tentacle8' };
      case 9: return { armColor: '#334155', legColor: '#334155', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 10: return { armColor: '#dc2626', legColor: '#dc2626', shoeStyle: 'rocket10', gloveStyle: 'starWhite10' };
      case 11: return { armColor: '#dc2626', legColor: '#dc2626', shoeStyle: 'football11', gloveStyle: 'mitt' };
      case 12: return { armColor: '#ea580c', legColor: '#ea580c', shoeStyle: 'twoToneOrange', gloveStyle: 'mitt' };
      case 13: return { armColor: '#9f1239', legColor: '#9f1239', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 14: return { armColor: '#14532d', legColor: '#14532d', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 15: return { armColor: '#1e3a8a', legColor: '#1e3a8a', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 16: return { armColor: '#9d174d', legColor: '#9d174d', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 17: return { armColor: '#6b21a8', legColor: '#6b21a8', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 18: return { armColor: '#be185d', legColor: '#be185d', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 19: return { armColor: '#334155', legColor: '#334155', shoeStyle: 'standard', gloveStyle: 'mitt' };
      case 20: return { armColor: '#c2410c', legColor: '#c2410c', shoeStyle: 'twoToneOrange', gloveStyle: 'white20' };
      default: return { armColor: '#334155', legColor: '#334155', shoeStyle: 'standard', gloveStyle: 'mitt' };
    }
  }

  function findCellEdgeX(char, targetRow, isRight, u) {
    const startX = -(char.cols * u) / 2;
    let bestRow = 0;
    let bestDiff = Infinity;
    for (let i = 0; i < char.cells.length; i++) {
      const diff = Math.abs(char.cells[i].row - targetRow);
      if (diff < bestDiff) {
        bestDiff = diff;
        bestRow = char.cells[i].row;
      }
    }
    let extremeCol = isRight ? 0 : char.cols - 1;
    let found = false;
    for (let i = 0; i < char.cells.length; i++) {
      const c = char.cells[i];
      if (c.row === bestRow) {
        if (!found) {
          extremeCol = c.col;
          found = true;
        } else if (isRight && c.col > extremeCol) {
          extremeCol = c.col;
        } else if (!isRight && c.col < extremeCol) {
          extremeCol = c.col;
        }
      }
    }
    return isRight ? (startX + (extremeCol + 1) * u) : (startX + extremeCol * u);
  }

  // --------------------------------------------------------------------------
  // Pre-Allocated 120-Slot Particle Pool
  // --------------------------------------------------------------------------
  const PARTICLE_POOL_SIZE = 120;
  const particlePool = [];
  for (let i = 0; i < PARTICLE_POOL_SIZE; i++) {
    particlePool.push({
      active: false,
      x: 0,
      y: 0,
      vx: 0,
      vy: 0,
      size: 0,
      life: 0,
      maxLife: 1,
      color: '#ffffff',
      alpha: 1,
      shape: 'star', // 'star' | 'circle' | 'square' | 'smoke'
      rot: 0,
      vRot: 0,
      gravity: 0
    });
  }

  function activateParticle(x, y, vx, vy, size, maxLife, color, shape, gravity, vRot) {
    let p = null;
    for (let i = 0; i < PARTICLE_POOL_SIZE; i++) {
      if (!particlePool[i].active) {
        p = particlePool[i];
        break;
      }
    }
    if (!p) {
      let oldestIdx = 0;
      let oldestRatio = -1;
      for (let i = 0; i < PARTICLE_POOL_SIZE; i++) {
        const ratio = particlePool[i].life / particlePool[i].maxLife;
        if (ratio > oldestRatio) {
          oldestRatio = ratio;
          oldestIdx = i;
        }
      }
      p = particlePool[oldestIdx];
    }
    p.active = true;
    p.x = x;
    p.y = y;
    p.vx = vx;
    p.vy = vy;
    p.size = size;
    p.life = 0;
    p.maxLife = maxLife;
    p.color = color;
    p.alpha = 1;
    p.shape = shape || 'star';
    p.gravity = gravity || 0;
    p.rot = Math.random() * Math.PI * 2;
    p.vRot = vRot || (Math.random() - 0.5) * 6;
  }

  function updateAndDrawParticles(ctx, dt) {
    for (let i = 0; i < PARTICLE_POOL_SIZE; i++) {
      const p = particlePool[i];
      if (!p.active) continue;

      p.life += dt;
      if (p.life >= p.maxLife) {
        p.active = false;
        continue;
      }

      p.vy += p.gravity * dt;
      p.x += p.vx * dt;
      p.y += p.vy * dt;
      p.rot += p.vRot * dt;

      const progress = p.life / p.maxLife;
      p.alpha = Math.max(0, 1 - progress);

      ctx.save();
      ctx.translate(p.x, p.y);
      ctx.rotate(p.rot);
      ctx.globalAlpha = p.alpha;

      const sz = p.size * (1 - progress * 0.3);
      if (p.shape === 'star') {
        drawStar(ctx, 0, 0, 5, sz, sz * 0.45, p.color, null);
      } else if (p.shape === 'circle') {
        ctx.beginPath();
        ctx.arc(0, 0, sz, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
      } else if (p.shape === 'square') {
        ctx.fillStyle = p.color;
        ctx.fillRect(-sz / 2, -sz / 2, sz, sz);
      } else if (p.shape === 'smoke') {
        ctx.beginPath();
        ctx.arc(0, 0, sz * (1 + progress), 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
      }
      ctx.restore();
    }
  }

  // --------------------------------------------------------------------------
  // Drifting Clouds Parallax System
  // --------------------------------------------------------------------------
  const clouds = [
    { xRatio: 0.12, yRatio: 0.12, w: 120, h: 36, speed: 7 },
    { xRatio: 0.58, yRatio: 0.20, w: 90, h: 28, speed: 5 },
    { xRatio: 0.82, yRatio: 0.10, w: 110, h: 32, speed: 8 },
    { xRatio: 0.35, yRatio: 0.26, w: 80, h: 24, speed: 6 }
  ];

  function updateAndDrawClouds(ctx, width, height, dt) {
    ctx.save();
    ctx.fillStyle = 'rgba(255, 255, 255, 0.72)';
    for (let i = 0; i < clouds.length; i++) {
      const c = clouds[i];
      c.xRatio += (c.speed * dt) / width;
      if (c.xRatio * width > width + c.w) {
        c.xRatio = -c.w / width;
      }
      const cx = c.xRatio * width;
      const cy = c.yRatio * height;
      drawRoundRect(ctx, cx, cy, c.w, c.h, c.h / 2);
      ctx.fill();
    }
    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Universal Procedural Blink & Gaze Tracking
  // --------------------------------------------------------------------------
  const blinkStateMap = new Map();

  function getBlinkScaleY(entityId, now, isStatic) {
    if (isStatic) return 1.0;
    let state = blinkStateMap.get(entityId);
    if (!state) {
      state = {
        nextBlink: now + 2000 + Math.random() * 3500,
        isBlinking: false,
        blinkStart: 0,
        duration: 180,
        isDouble: Math.random() < 0.15,
        doneDouble: false
      };
      blinkStateMap.set(entityId, state);
    }

    if (!state.isBlinking) {
      if (now >= state.nextBlink) {
        state.isBlinking = true;
        state.blinkStart = now;
      } else {
        return 1.0;
      }
    }

    const elapsed = now - state.blinkStart;
    if (elapsed >= state.duration) {
      if (state.isDouble && !state.doneDouble) {
        state.doneDouble = true;
        state.blinkStart = now + 60;
        state.duration = 160;
        return 1.0;
      }
      state.isBlinking = false;
      state.isDouble = Math.random() < 0.15;
      state.doneDouble = false;
      state.nextBlink = now + 2400 + Math.random() * 3600;
      return 1.0;
    }

    const p = elapsed / state.duration;
    const dip = Math.sin(p * Math.PI);
    return Math.max(0.08, 1.0 - dip * 0.92);
  }

  // --------------------------------------------------------------------------
  // Flush Snap-Together Mathlink Cube Shading Recipe (CBeebies Style)
  // --------------------------------------------------------------------------
  function drawUnitBlock(ctx, x, y, size, palette, flashAlpha) {
    if (size <= 0) return;
    const pal = palette || PALETTES[1];
    const r = Math.min(size * 0.25, Math.max(1.5, size * 0.065));
    const bScale = pal.borderWidthScale || 1.0;
    const borderW = size < 14
      ? Math.max(1.0, size * 0.075 * bScale)
      : Math.max(1.8, size * 0.055 * bScale);

    // 1. Rich Base Color Fill (Full u x u grid cell, flush edge-to-edge)
    drawRoundRect(ctx, x, y, size, size, r);
    ctx.fillStyle = pal.base;
    ctx.fill();

    // 2. Clean Flat-Glossy Inner Bevels (zero ctx.clip for 60fps iOS Canvas2D)
    if (size > 6) {
      const ins = Math.max(borderW * 0.5, r * 0.35);
      const bx0 = x + ins;
      const by0 = y + ins;
      const bx1 = x + size - ins;
      const by1 = y + size - ins;
      const innerSpan = Math.max(0, bx1 - bx0);
      const bevel = Math.min(innerSpan * 0.25, Math.max(1.2, innerSpan * 0.11));

      if (bevel > 0.5 && innerSpan > bevel * 2) {
        // Subtle inner top & left light bevel
        ctx.fillStyle = 'rgba(255, 255, 255, 0.28)';
        ctx.beginPath();
        ctx.moveTo(bx0, by0);
        ctx.lineTo(bx1, by0);
        ctx.lineTo(bx1 - bevel, by0 + bevel);
        ctx.lineTo(bx0 + bevel, by0 + bevel);
        ctx.lineTo(bx0 + bevel, by1 - bevel);
        ctx.lineTo(bx0, by1);
        ctx.closePath();
        ctx.fill();

        // Subtle inner bottom & right shadow bevel (preserve parent globalAlpha)
        const prevAlpha = ctx.globalAlpha;
        ctx.fillStyle = pal.deep || pal.shadow;
        ctx.globalAlpha = prevAlpha * 0.55;
        ctx.beginPath();
        ctx.moveTo(bx1, by1);
        ctx.lineTo(bx0, by1);
        ctx.lineTo(bx0 + bevel, by1 - bevel);
        ctx.lineTo(bx1 - bevel, by1 - bevel);
        ctx.lineTo(bx1 - bevel, by0 + bevel);
        ctx.lineTo(bx1, by0);
        ctx.closePath();
        ctx.fill();
        ctx.globalAlpha = prevAlpha;
      }

      // Tiny crisp top-left corner highlight
      if (size >= 10) {
        ctx.fillStyle = 'rgba(255, 255, 255, 0.55)';
        drawRoundRect(ctx, x + size * 0.11, y + size * 0.11, size * 0.19, Math.max(1.5, size * 0.06), Math.max(1, size * 0.03));
        ctx.fill();
      }
    }

    // 3. Bold Colored Outer Border (seals bevel edges cleanly)
    ctx.lineWidth = borderW;
    ctx.strokeStyle = pal.border;
    drawRoundRect(ctx, x, y, size, size, r);
    ctx.stroke();

    // 4. Count-Up Flash Overlay
    if (flashAlpha && flashAlpha > 0.01) {
      ctx.fillStyle = 'rgba(255, 250, 205, ' + Math.min(1.0, flashAlpha) + ')';
      drawRoundRect(ctx, x, y, size, size, r);
      ctx.fill();
    }
  }

  // Draw cell-level canonical decorations (Six's dice pips & Three's 3 juggling buttons)
  function drawCellDecoration(ctx, cell, cx, cy, u) {
    if (cell.pip) {
      // Crisp light-lavender circular dice pip centered in block (clean CBeebies flat dot)
      const pipR = Math.max(1.5, u * 0.14);
      ctx.beginPath();
      ctx.arc(cx + u / 2, cy + u / 2, pipR, 0, Math.PI * 2);
      ctx.fillStyle = '#c4b5fd';
      ctx.fill();
    }
    if (cell.starBtn) {
      // Three's 3 bright red circular juggling buttons vertically stacked down the middle block
      const btnR = Math.max(1.3, u * 0.095);
      const spacing = u * 0.25;
      const midX = cx + u / 2;
      const midY = cy + u / 2;
      for (let b = -1; b <= 1; b++) {
        const by = midY + b * spacing;
        ctx.beginPath();
        ctx.arc(midX, by, btnR, 0, Math.PI * 2);
        ctx.fillStyle = '#dc2626';
        ctx.fill();
        if (u >= 14) {
          ctx.lineWidth = Math.max(1, u * 0.024);
          ctx.strokeStyle = '#991b1b';
          ctx.stroke();
          // Tiny glossy highlight
          ctx.beginPath();
          ctx.arc(midX - btnR * 0.28, by - btnR * 0.28, btnR * 0.28, 0, Math.PI * 2);
          ctx.fillStyle = 'rgba(255, 255, 255, 0.55)';
          ctx.fill();
        }
      }
    }
  }

  // --------------------------------------------------------------------------
  // Signature Cartoon Limbs: Arms/Hands & Legs/Shoes (1-20)
  // --------------------------------------------------------------------------
  function drawCartoonHand(ctx, x, y, angle, u, color, gloveStyle) {
    ctx.save();
    ctx.translate(x, y);
    ctx.rotate(angle);

    const palmR = u * 0.105;
    let fill = color;
    let stroke = null;

    if (gloveStyle === 'starWhite10' || gloveStyle === 'white20') {
      fill = '#ffffff';
      stroke = gloveStyle === 'starWhite10' ? '#dc2626' : '#c2410c';
    }

    // 3 rounded cartoon fingers fanning out along +x direction
    const fingerAngles = [-0.52, 0.0, 0.52];
    const fingerLen = u * 0.13;
    const fingerR = u * 0.046;

    ctx.fillStyle = fill;
    for (let i = 0; i < 3; i++) {
      const fa = fingerAngles[i];
      const fx = Math.cos(fa) * (palmR * 0.8 + fingerLen * 0.45);
      const fy = Math.sin(fa) * (palmR * 0.8 + fingerLen * 0.45);
      ctx.save();
      ctx.translate(fx, fy);
      ctx.rotate(fa);
      drawRoundRect(ctx, -fingerLen * 0.5, -fingerR, fingerLen, fingerR * 2, fingerR);
      ctx.fill();
      if (stroke) {
        ctx.lineWidth = Math.max(1, u * 0.025);
        ctx.strokeStyle = stroke;
        ctx.stroke();
      }
      ctx.restore();
    }

    // Rounded palm
    ctx.beginPath();
    ctx.arc(0, 0, palmR, 0, Math.PI * 2);
    ctx.fillStyle = fill;
    ctx.fill();
    if (stroke) {
      ctx.lineWidth = Math.max(1, u * 0.028);
      ctx.strokeStyle = stroke;
      ctx.stroke();
    }

    if (gloveStyle === 'starWhite10') {
      drawStar(ctx, 0, 0, 5, palmR * 0.65, palmR * 0.30, '#ef4444', null);
    }

    ctx.restore();
  }

  function drawHighFiveHand(ctx, x, y, angle, u) {
    ctx.save();
    ctx.translate(x, y);
    ctx.rotate(angle);

    const palmR = u * 0.24;
    const fill = '#1d4ed8';
    const outline = '#1e3a8a';

    // 5 distinct splayed fingers (thumb + 4 fingers)
    const fingerDefs = [
      { a: -1.15, len: u * 0.22, w: u * 0.095 },
      { a: -0.55, len: u * 0.26, w: u * 0.090 },
      { a: -0.10, len: u * 0.28, w: u * 0.092 },
      { a: 0.35, len: u * 0.26, w: u * 0.088 },
      { a: 0.82, len: u * 0.21, w: u * 0.082 }
    ];

    for (let i = 0; i < fingerDefs.length; i++) {
      const f = fingerDefs[i];
      ctx.save();
      ctx.rotate(f.a);
      drawRoundRect(ctx, palmR * 0.45, -f.w / 2, f.len, f.w, f.w / 2);
      ctx.fillStyle = fill;
      ctx.fill();
      ctx.lineWidth = Math.max(1.2, u * 0.028);
      ctx.strokeStyle = outline;
      ctx.stroke();
      ctx.restore();
    }

    // Main palm circle
    ctx.beginPath();
    ctx.arc(0, 0, palmR, 0, Math.PI * 2);
    ctx.fillStyle = fill;
    ctx.fill();
    ctx.lineWidth = Math.max(1.2, u * 0.03);
    ctx.strokeStyle = outline;
    ctx.stroke();

    // Light-cyan 5-pointed star on the palm
    drawStar(ctx, 0, 0, 5, palmR * 0.68, palmR * 0.31, '#67e8f9', '#0284c7', Math.max(1, u * 0.02));

    ctx.restore();
  }

  function drawCartoonShoe(ctx, legX, legTopY, u, dir, legColor, shoeStyle, tapLift) {
    const shoeRy = u * 0.11;
    const shoeRx = u * 0.205;
    const legW = Math.max(2.2, u * 0.13);
    const footY = -(tapLift || 0); // 0 rests directly on groundY

    ctx.save();

    // Short vertical leg from bottom of block (-legH - 2) down into shoe
    ctx.beginPath();
    ctx.moveTo(legX, legTopY);
    ctx.lineTo(legX, footY - shoeRy * 0.85);
    ctx.lineWidth = legW;
    ctx.lineCap = 'round';
    ctx.strokeStyle = legColor;
    ctx.stroke();

    // Outward-pointing rounded shoe resting flat on y = footY
    const shoeCx = legX + dir * (u * 0.09);
    const shoeCy = footY - shoeRy;

    if (shoeStyle === 'twoToneOrange') {
      // Main orange shoe body
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx, shoeRy, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#ea580c';
      ctx.fill();
      // Cream sole & toe cap (zero ctx.clip)
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx * 0.96, shoeRy * 0.96, 0, 0.08, Math.PI - 0.08);
      ctx.closePath();
      ctx.fillStyle = '#fed7aa';
      ctx.fill();
      ctx.beginPath();
      ctx.ellipse(shoeCx + dir * shoeRx * 0.45, shoeCy + shoeRy * 0.08, shoeRx * 0.48, shoeRy * 0.68, 0, 0, Math.PI * 2);
      ctx.fill();
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx, shoeRy, 0, 0, Math.PI * 2);
      ctx.lineWidth = Math.max(1, u * 0.025);
      ctx.strokeStyle = '#9a3412';
      ctx.stroke();
    } else if (shoeStyle === 'rocket10') {
      // Red rocket boot with bright yellow thruster cuff
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx * 1.05, shoeRy * 1.05, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#dc2626';
      ctx.fill();
      ctx.lineWidth = Math.max(1, u * 0.028);
      ctx.strokeStyle = '#991b1b';
      ctx.stroke();
      // Boot cuff
      drawRoundRect(ctx, legX - legW * 0.72, legTopY + u * 0.03, legW * 1.44, u * 0.07, u * 0.03);
      ctx.fillStyle = '#facc15';
      ctx.fill();
    } else if (shoeStyle === 'football11') {
      // Red football boot with crisp white stripe
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx * 1.04, shoeRy, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#dc2626';
      ctx.fill();
      ctx.fillStyle = '#ffffff';
      drawRoundRect(ctx, shoeCx - shoeRx * 0.3, shoeCy - shoeRy * 0.45, shoeRx * 0.6, shoeRy * 0.35, 2);
      ctx.fill();
    } else {
      // Canonical rounded cartoon shoe
      ctx.beginPath();
      ctx.ellipse(shoeCx, shoeCy, shoeRx, shoeRy, 0, 0, Math.PI * 2);
      ctx.fillStyle = legColor;
      ctx.fill();
      // Subtle top highlight
      ctx.beginPath();
      ctx.ellipse(shoeCx + dir * shoeRx * 0.18, shoeCy - shoeRy * 0.30, shoeRx * 0.45, shoeRy * 0.25, 0, 0, Math.PI * 2);
      ctx.fillStyle = 'rgba(255, 255, 255, 0.22)';
      ctx.fill();
    }

    ctx.restore();
  }

  function drawCharacterLimbsBack(ctx, entity, char, u, nowMs, isStatic) {
    const n = char.n;
    const legH = getLegHeight(u);
    const totalW = char.cols * u;
    const style = getLimbStyle(n);

    const tapP = (!isStatic && entity) ? (entity.tapProgress || 0) : 0;
    const isCel = (!isStatic && entity && entity.state === 'CELEBRATING');
    const entId = (entity && entity.id) ? entity.id : n;
    const idleWave = isStatic ? 0 : Math.sin(nowMs * 0.0036 + entId * 1.7);
    const tapBoost = (tapP > 0 || isCel) ? Math.sin((nowMs * 0.015) + tapP * 10) : 0;

    // -----------------------------------------------------------------------
    // Special Case 8: Octoblock's 8 Curved Pink Tentacles (6 Side + 2 Bottom)
    // -----------------------------------------------------------------------
    if (n === 8) {
      ctx.save();
      const tentW = Math.max(2.4, u * 0.13);
      ctx.lineWidth = tentW;
      ctx.lineCap = 'round';
      ctx.strokeStyle = '#ec4899';

      // 3 wavy tentacles on each side (rows 1, 2, 3)
      for (let t = 0; t < 3; t++) {
        const wave = isStatic ? 0 : Math.sin(nowMs * 0.005 + t * 1.1 + tapP * 8) * (u * 0.12);
        const anchorY = -legH - (1.1 + t * 0.95) * u;
        // Left tentacle
        ctx.beginPath();
        ctx.moveTo(-totalW / 2 + 2, anchorY);
        ctx.quadraticCurveTo(-totalW / 2 - u * 0.30, anchorY - u * 0.18 + wave, -totalW / 2 - u * 0.48, anchorY + u * 0.10 - wave);
        ctx.stroke();
        // Right tentacle
        ctx.beginPath();
        ctx.moveTo(totalW / 2 - 2, anchorY);
        ctx.quadraticCurveTo(totalW / 2 + u * 0.30, anchorY - u * 0.18 - wave, totalW / 2 + u * 0.48, anchorY + u * 0.10 + wave);
        ctx.stroke();
      }

      // 2 curled bottom tentacle legs resting flat at y = 0
      const footLiftL = isStatic ? 0 : Math.max(0, tapBoost) * u * 0.06;
      const footLiftR = isStatic ? 0 : Math.max(0, -tapBoost) * u * 0.06;
      const footLX = -u * 0.46;
      const footRX = u * 0.46;
      const curlR = tentW * 0.5;

      // Left bottom tentacle + curled foot tip
      ctx.beginPath();
      ctx.moveTo(footLX, -legH - 2);
      ctx.quadraticCurveTo(footLX - u * 0.02, -legH * 0.25, footLX - u * 0.24, -curlR - footLiftL);
      ctx.quadraticCurveTo(footLX - u * 0.34, -curlR - u * 0.06 - footLiftL, footLX - u * 0.28, -curlR - u * 0.11 - footLiftL);
      ctx.stroke();
      // Right bottom tentacle + curled foot tip
      ctx.beginPath();
      ctx.moveTo(footRX, -legH - 2);
      ctx.quadraticCurveTo(footRX + u * 0.02, -legH * 0.25, footRX + u * 0.24, -curlR - footLiftR);
      ctx.quadraticCurveTo(footRX + u * 0.34, -curlR - u * 0.06 - footLiftR, footRX + u * 0.28, -curlR - u * 0.11 - footLiftR);
      ctx.stroke();

      ctx.restore();
      return;
    }

    // -----------------------------------------------------------------------
    // 1. Two Short Legs & Shoes (resting right at y = 0)
    // -----------------------------------------------------------------------
    const legTopY = -legH - 2;
    const legSpan = char.cols === 1 ? u * 0.22 : Math.min(totalW * 0.26, u * 0.56);
    const liftL = isStatic ? 0 : Math.max(0, tapBoost) * u * 0.07;
    const liftR = isStatic ? 0 : Math.max(0, -tapBoost) * u * 0.07;

    drawCartoonShoe(ctx, -legSpan, legTopY, u, -1, style.legColor, style.shoeStyle, liftL);
    drawCartoonShoe(ctx, legSpan, legTopY, u, 1, style.legColor, style.shoeStyle, liftR);

    // -----------------------------------------------------------------------
    // 2. Curved Arms & 3-Fingered Cartoon Mitts
    // -----------------------------------------------------------------------
    let shoulderRow = char.rows >= 4 ? char.rows - 1.55 : (char.rows >= 2 ? char.rows * 0.55 : 0.48);
    if (n === 1) shoulderRow = 0.48;
    if (n === 2) shoulderRow = 1.05;
    if (n === 3) shoulderRow = 1.55;
    if (n === 4) shoulderRow = 0.95;
    if (n === 5) shoulderRow = 3.35;
    if (n === 6) shoulderRow = 1.65;
    if (n === 7) shoulderRow = 5.35;
    if (n >= 11 && n <= 19 && n !== 12) shoulderRow = 3.15;
    if (n === 12) shoulderRow = 2.15;
    if (n === 20) shoulderRow = 3.15;

    const armW = Math.max(2.2, u * 0.13);

    // Left Arm
    const leftEdgeX = findCellEdgeX(char, shoulderRow, false, u) + 2;
    const leftShoulderY = -legH - shoulderRow * u;
    let leftUpFactor = (n === 1 || n === 6 || n === 7 || n === 3 || n === 10 || n === 20) ? -1 : 0.35;
    if (n === 7) leftUpFactor = -1.35;
    if (n === 1) leftUpFactor = -0.85;
    const waveL = idleWave * (u * 0.09) + tapBoost * (u * 0.14);
    const armReachL = (n === 10 || n === 20) ? 0.42 : (n === 7 ? 0.38 : 0.36);
    const leftHandX = leftEdgeX - u * armReachL;
    const leftHandY = leftShoulderY + leftUpFactor * (u * 0.32) + waveL;
    const leftCtrlX = leftEdgeX - u * 0.24;
    const leftCtrlY = leftShoulderY + (leftUpFactor < 0 ? u * 0.08 : -u * 0.05) + waveL * 0.5;

    ctx.save();
    ctx.beginPath();
    ctx.moveTo(leftEdgeX, leftShoulderY);
    ctx.quadraticCurveTo(leftCtrlX, leftCtrlY, leftHandX, leftHandY);
    ctx.lineWidth = armW;
    ctx.lineCap = 'round';
    ctx.strokeStyle = style.armColor;
    ctx.stroke();
    const leftHandAngle = Math.atan2(leftHandY - leftCtrlY, leftHandX - leftCtrlX);
    drawCartoonHand(ctx, leftHandX, leftHandY, leftHandAngle, u, style.armColor, style.gloveStyle);
    ctx.restore();

    // Right Arm (Note: for n === 5, Five's High-Five arm & giant star hand render in Front pass or arm behind + hand in front)
    const rightRow = (n >= 11 && n <= 19 && n !== 12 && (n - 10) < 4) ? Math.min(shoulderRow, (n - 10) * 0.55) : shoulderRow;
    const rightEdgeX = findCellEdgeX(char, rightRow, true, u) - 2;
    const rightShoulderY = -legH - rightRow * u;

    if (n !== 5) {
      let rightUpFactor = (n === 1 || n === 6 || n === 7 || n === 3 || n === 10 || n === 20) ? -1 : 0.35;
      if (n === 7) rightUpFactor = -1.35;
      if (n === 1) rightUpFactor = -0.35;
      const waveR = -idleWave * (u * 0.09) - tapBoost * (u * 0.14);
      const armReachR = (n === 10 || n === 20) ? 0.42 : (n === 7 ? 0.38 : 0.36);
      const rightHandX = rightEdgeX + u * armReachR;
      const rightHandY = rightShoulderY + rightUpFactor * (u * 0.32) + waveR;
      const rightCtrlX = rightEdgeX + u * 0.24;
      const rightCtrlY = rightShoulderY + (rightUpFactor < 0 ? u * 0.08 : -u * 0.05) + waveR * 0.5;

      ctx.save();
      ctx.beginPath();
      ctx.moveTo(rightEdgeX, rightShoulderY);
      ctx.quadraticCurveTo(rightCtrlX, rightCtrlY, rightHandX, rightHandY);
      ctx.lineWidth = armW;
      ctx.lineCap = 'round';
      ctx.strokeStyle = style.armColor;
      ctx.stroke();
      const rightHandAngle = Math.atan2(rightHandY - rightCtrlY, rightHandX - rightCtrlX);
      drawCartoonHand(ctx, rightHandX, rightHandY, rightHandAngle, u, style.armColor, style.gloveStyle);
      ctx.restore();
    } else {
      // Five's right arm reaching out and up from behind the block; giant star hand drawn in front pass
      const wave5 = isStatic ? 0 : Math.sin(nowMs * 0.006 + tapP * 8) * (u * 0.08);
      const handX = rightEdgeX + u * 0.44;
      const handY = -legH - 4.30 * u + wave5;
      const ctrlX = rightEdgeX + u * 0.26;
      const ctrlY = rightShoulderY + u * 0.05;

      ctx.save();
      ctx.beginPath();
      ctx.moveTo(rightEdgeX, rightShoulderY);
      ctx.quadraticCurveTo(ctrlX, ctrlY, handX, handY);
      ctx.lineWidth = armW;
      ctx.lineCap = 'round';
      ctx.strokeStyle = style.armColor;
      ctx.stroke();
      ctx.restore();
    }
  }

  function drawCharacterLimbsFront(ctx, entity, char, u, nowMs, isStatic) {
    if (char.n !== 5) return;
    const legH = getLegHeight(u);
    const totalW = char.cols * u;
    const rightEdgeX = totalW / 2 - 2;
    const tapP = (!isStatic && entity) ? (entity.tapProgress || 0) : 0;
    const wave5 = isStatic ? 0 : Math.sin(nowMs * 0.006 + tapP * 8) * (u * 0.08);
    const handX = rightEdgeX + u * 0.48;
    const handY = -legH - 4.35 * u + wave5;
    const rot = -0.35 + (isStatic ? 0 : Math.sin(nowMs * 0.006 + tapP * 8) * 0.18);
    drawHighFiveHand(ctx, handX, handY, rot, u);
  }

  // --------------------------------------------------------------------------
  // Pupil & Face Rendering
  // --------------------------------------------------------------------------
  function drawPupilEye(ctx, cx, cy, eyeR, blinkScaleY, pupilOffsetX, pupilOffsetY, irisColor, isAnticipating, strokeScale) {
    ctx.save();
    ctx.translate(cx, cy);
    ctx.scale(isAnticipating ? 1.12 : 1.0, blinkScaleY * (isAnticipating ? 1.12 : 1.0));

    // Eye Sclera (White)
    ctx.beginPath();
    ctx.arc(0, 0, eyeR, 0, Math.PI * 2);
    ctx.fillStyle = '#ffffff';
    ctx.fill();
    ctx.lineWidth = Math.max(1.3, eyeR * (strokeScale || 0.22));
    ctx.strokeStyle = irisColor || '#0f172a';
    ctx.stroke();

    if (blinkScaleY > 0.25) {
      const maxOff = eyeR * 0.30;
      const ox = clamp(pupilOffsetX, -maxOff, maxOff);
      const oy = clamp(pupilOffsetY, -maxOff, maxOff);
      const pupilR = eyeR * 0.50;

      ctx.beginPath();
      ctx.arc(ox, oy, pupilR, 0, Math.PI * 2);
      ctx.fillStyle = '#0f172a';
      ctx.fill();

      // Dual Specular Glints
      ctx.beginPath();
      ctx.arc(ox - pupilR * 0.32, oy - pupilR * 0.32, pupilR * 0.34, 0, Math.PI * 2);
      ctx.fillStyle = '#ffffff';
      ctx.fill();

      ctx.beginPath();
      ctx.arc(ox + pupilR * 0.28, oy + pupilR * 0.28, pupilR * 0.18, 0, Math.PI * 2);
      ctx.fillStyle = '#ffffff';
      ctx.fill();
    }
    ctx.restore();
  }

  function drawOpenSmile(ctx, cx, cy, width, lipColor, isAnticipating) {
    ctx.save();
    if (isAnticipating) {
      ctx.beginPath();
      ctx.ellipse(cx, cy, width * 0.32, width * 0.42, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#1e1b4b';
      ctx.fill();
      ctx.lineWidth = Math.max(1.2, width * 0.10);
      ctx.strokeStyle = lipColor || '#0f172a';
      ctx.stroke();
      ctx.beginPath();
      ctx.ellipse(cx, cy + width * 0.15, width * 0.20, width * 0.16, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#fb7185';
      ctx.fill();
    } else {
      // CBeebies D-shaped happy open smile with dark interior, pink tongue & bold colored lip
      const rx = width * 0.48;
      const ry = width * 0.42;
      const topY = cy - ry * 0.32;

      ctx.beginPath();
      ctx.moveTo(cx - rx, topY);
      ctx.quadraticCurveTo(cx, topY + ry * 0.18, cx + rx, topY);
      ctx.bezierCurveTo(cx + rx, topY + ry * 1.35, cx - rx, topY + ry * 1.35, cx - rx, topY);
      ctx.closePath();

      ctx.fillStyle = '#450a0a';
      ctx.fill();

      // Pink Tongue inside lower half (zero ctx.clip)
      ctx.beginPath();
      ctx.ellipse(cx, topY + ry * 0.76, rx * 0.50, ry * 0.23, 0, 0, Math.PI * 2);
      ctx.fillStyle = '#fb7185';
      ctx.fill();

      // Lip Outline
      ctx.beginPath();
      ctx.moveTo(cx - rx, topY);
      ctx.quadraticCurveTo(cx, topY + ry * 0.18, cx + rx, topY);
      ctx.bezierCurveTo(cx + rx, topY + ry * 1.35, cx - rx, topY + ry * 1.35, cx - rx, topY);
      ctx.closePath();
      ctx.lineWidth = Math.max(1.3, width * 0.12);
      ctx.strokeStyle = lipColor || '#be123c';
      ctx.lineJoin = 'round';
      ctx.stroke();
    }
    ctx.restore();
  }

  function drawCurvedSmile(ctx, cx, cy, width, lipColor, isAnticipating) {
    if (isAnticipating) {
      drawOpenSmile(ctx, cx, cy, width, lipColor, true);
      return;
    }
    ctx.save();
    ctx.beginPath();
    ctx.arc(cx, cy - width * 0.14, width * 0.42, 0.18 * Math.PI, 0.82 * Math.PI, false);
    ctx.lineWidth = Math.max(1.5, width * 0.14);
    ctx.strokeStyle = lipColor || '#991b1b';
    ctx.lineCap = 'round';
    ctx.stroke();
    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Signature Character Faces & Props (1-20)
  // --------------------------------------------------------------------------
  function drawCharacterFaceAndProps(ctx, entity, char, u, metrics, nowMs, isStatic) {
    const tapP = (!isStatic && entity) ? (entity.tapProgress || 0) : 0;
    const isAnticipating = (!isStatic && entity && entity.expression === 'anticipation');
    const entId = (entity && entity.id) ? entity.id : char.n;
    const blinkY = getBlinkScaleY(entId, nowMs, isStatic);
    const legH = getLegHeight(u);

    // Live Pupil Tracking calculation
    let pOffsetX = 0;
    let pOffsetY = 0;
    if (!isStatic && entity && entity.lookTarget) {
      const dx = entity.lookTarget.x - entity.x;
      const dy = entity.lookTarget.y - (entity.y - legH - (char.rows * u) / 2);
      const dist = Math.hypot(dx, dy);
      if (dist > 1) {
        const factor = Math.min(1.0, dist / 150) * (u * 0.12);
        pOffsetX = (dx / dist) * factor;
        pOffsetY = (dy / dist) * factor;
      }
    }

    const faceDef = char.face || { type: 'cyclops', anchorCol: 0.5, anchorRow: 0.52 };
    const faceX = (faceDef.anchorCol - char.cols / 2) * u;
    const faceY = -legH - (faceDef.anchorRow) * u;

    ctx.save();
    ctx.translate(faceX, faceY);

    // 1: Cyclops Eye (NO eyebrow, thick #991b1b rim) & Curved Smile
    if (faceDef.type === 'cyclops') {
      const eyeR = u * 0.25;
      drawPupilEye(ctx, 0, -u * 0.04, eyeR, blinkY, pOffsetX, pOffsetY, '#991b1b', isAnticipating, 0.28);
      drawCurvedSmile(ctx, 0, eyeR + u * 0.08, u * 0.36, '#991b1b', isAnticipating);
    }

    // 2: Bold Rounded-Rectangle Purple Glasses with White Inner Trim & Coral Smile
    else if (faceDef.type === 'glasses') {
      const eyeR = u * 0.165;
      const eyeSpacing = u * 0.255;
      const gColor = '#9333ea';

      const frameW = u * 0.44;
      const frameH = u * 0.42;
      const frameR = Math.max(2, u * 0.11);

      // Bridge Bar
      ctx.beginPath();
      ctx.moveTo(-eyeSpacing + frameW / 2 - 1, -u * 0.02);
      ctx.lineTo(eyeSpacing - frameW / 2 + 1, -u * 0.02);
      ctx.lineWidth = Math.max(2, u * 0.085);
      ctx.strokeStyle = gColor;
      ctx.stroke();

      // Left & Right Purple Outer Frames + Crisp White Inner Lens Trim
      const xCenters = [-eyeSpacing, eyeSpacing];
      for (let i = 0; i < 2; i++) {
        const lx = xCenters[i];
        drawRoundRect(ctx, lx - frameW / 2, -frameH / 2 - u * 0.02, frameW, frameH, frameR);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.lineWidth = Math.max(2, u * 0.085);
        ctx.strokeStyle = gColor;
        ctx.stroke();

        // Crisp #ffffff inner lens trim inside the purple rim
        const pad = Math.max(1.2, u * 0.035);
        drawRoundRect(ctx, lx - frameW / 2 + pad, -frameH / 2 - u * 0.02 + pad, frameW - pad * 2, frameH - pad * 2, Math.max(1, frameR * 0.7));
        ctx.lineWidth = Math.max(0.8, u * 0.02);
        ctx.strokeStyle = '#ffffff';
        ctx.stroke();
      }

      drawPupilEye(ctx, -eyeSpacing, -u * 0.02, eyeR, blinkY, pOffsetX, pOffsetY, '#ffffff', isAnticipating, 0.05);
      drawPupilEye(ctx, eyeSpacing, -u * 0.02, eyeR, blinkY, pOffsetX, pOffsetY, '#ffffff', isAnticipating, 0.05);
      drawCurvedSmile(ctx, 0, u * 0.30, u * 0.38, '#e11d48', isAnticipating);
    }

    // 3: 3 Red Jester Cap Spikes with Yellow Pom-Poms, Amber Eye Rims, Open Red Mouth
    else if (faceDef.type === 'crown') {
      const eyeR = u * 0.165;
      const eyeSpacing = u * 0.24;

      // 3 Red Triangular Jester Cap Spikes on Top of Row 2
      ctx.save();
      ctx.translate(0, -u * 0.52);
      const spikes = [
        { baseX: -u * 0.25, tipX: -u * 0.44, tipY: -u * 0.30, halfW: u * 0.145 },
        { baseX: 0, tipX: 0, tipY: -u * 0.38, halfW: u * 0.15 },
        { baseX: u * 0.25, tipX: u * 0.44, tipY: -u * 0.30, halfW: u * 0.145 }
      ];
      for (let s = 0; s < spikes.length; s++) {
        const sp = spikes[s];
        ctx.beginPath();
        ctx.moveTo(sp.baseX - sp.halfW, 1);
        ctx.lineTo(sp.tipX, sp.tipY);
        ctx.lineTo(sp.baseX + sp.halfW, 1);
        ctx.closePath();
        ctx.fillStyle = '#ef4444';
        ctx.fill();
        ctx.lineWidth = Math.max(1, u * 0.028);
        ctx.strokeStyle = '#b91c1c';
        ctx.lineJoin = 'round';
        ctx.stroke();

        // Tiny #facc15 pom-pom dot at tip
        ctx.beginPath();
        ctx.arc(sp.tipX, sp.tipY, Math.max(1.5, u * 0.055), 0, Math.PI * 2);
        ctx.fillStyle = '#facc15';
        ctx.fill();
        ctx.lineWidth = Math.max(0.8, u * 0.02);
        ctx.strokeStyle = '#ca8a04';
        ctx.stroke();
      }
      ctx.restore();

      drawPupilEye(ctx, -eyeSpacing, -u * 0.04, eyeR, blinkY, pOffsetX, pOffsetY, '#d97706', isAnticipating, 0.24);
      drawPupilEye(ctx, eyeSpacing, -u * 0.04, eyeR, blinkY, pOffsetX, pOffsetY, '#d97706', isAnticipating, 0.24);
      drawOpenSmile(ctx, 0, u * 0.24, u * 0.36, '#be123c', isAnticipating);

      // Orbiting 3 Red Juggling Balls on Tap / Celebrate
      if (!isStatic && (tapP > 0 || (entity && entity.state === 'CELEBRATING'))) {
        const jugglePhase = (nowMs * 0.005 + tapP * 3);
        const ballR = u * 0.13;
        for (let b = 0; b < 3; b++) {
          const bAngle = jugglePhase + (b * Math.PI * 2) / 3;
          const bx = Math.sin(bAngle) * (u * 0.65);
          const by = -u * 0.90 + Math.cos(bAngle * 2) * (u * 0.30);
          ctx.beginPath();
          ctx.arc(bx, by, ballR, 0, Math.PI * 2);
          ctx.fillStyle = '#ef4444';
          ctx.fill();
          ctx.lineWidth = 2;
          ctx.strokeStyle = '#b91c1c';
          ctx.stroke();
          ctx.beginPath();
          ctx.arc(bx - ballR * 0.3, by - ballR * 0.3, ballR * 0.3, 0, Math.PI * 2);
          ctx.fillStyle = '#ffffff';
          ctx.fill();
        }
      }
    }

    // 4: Square White Eyes, Square Pupils, Thick #14532d Brows, Open Green Smile
    else if (faceDef.type === 'square') {
      const eyeW = u * 0.31;
      const eyeSpacing = u * 0.34;
      const eyeY = -u * 0.06;

      // Dark-Green Rectangular Eyebrows
      const browW = eyeW * 1.15;
      const browH = Math.max(2, u * 0.085);
      ctx.fillStyle = '#14532d';
      drawRoundRect(ctx, -eyeSpacing - browW / 2, eyeY - eyeW / 2 - browH - u * 0.05, browW, browH, browH * 0.3);
      ctx.fill();
      drawRoundRect(ctx, eyeSpacing - browW / 2, eyeY - eyeW / 2 - browH - u * 0.05, browW, browH, browH * 0.3);
      ctx.fill();

      // Square Eyes (with blink scaling)
      const sqOffsets = [-eyeSpacing, eyeSpacing];
      for (let i = 0; i < 2; i++) {
        ctx.save();
        ctx.translate(sqOffsets[i], eyeY);
        ctx.scale(1, blinkY);
        drawRoundRect(ctx, -eyeW / 2, -eyeW / 2, eyeW, eyeW, Math.max(1.5, u * 0.055));
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.lineWidth = Math.max(1.3, u * 0.045);
        ctx.strokeStyle = '#14532d';
        ctx.stroke();

        if (blinkY > 0.25) {
          const pOff = clamp(pOffsetX, -eyeW * 0.22, eyeW * 0.22);
          const pOffY = clamp(pOffsetY, -eyeW * 0.22, eyeW * 0.22);
          const pupSize = eyeW * 0.46;
          drawRoundRect(ctx, -pupSize / 2 + pOff, -pupSize / 2 + pOffY, pupSize, pupSize, Math.max(1, pupSize * 0.16));
          ctx.fillStyle = '#0f172a';
          ctx.fill();
          ctx.fillStyle = '#ffffff';
          ctx.fillRect(-pupSize * 0.32 + pOff, -pupSize * 0.32 + pOffY, pupSize * 0.28, pupSize * 0.28);
        }
        ctx.restore();
      }

      drawOpenSmile(ctx, 0, eyeY + eyeW / 2 + u * 0.18, u * 0.44, '#14532d', isAnticipating);
    }

    // 5: Royal-Blue 5-Pointed Star Mask around Left Eye, Round Blue Rim Right Eye, Pink Open Smile
    else if (faceDef.type === 'starLeft') {
      const eyeR = u * 0.16;
      const eyeSpacing = u * 0.23;

      // Big 5-pointed royal-blue star mask around left eye
      drawStar(ctx, -eyeSpacing, -u * 0.04, 5, eyeR * 2.45, eyeR * 1.1, '#1d4ed8', '#1e3a8a', Math.max(1.2, u * 0.03));

      drawPupilEye(ctx, -eyeSpacing, -u * 0.04, eyeR, blinkY, pOffsetX, pOffsetY, '#1d4ed8', isAnticipating, 0.20);
      drawPupilEye(ctx, eyeSpacing, -u * 0.04, eyeR, blinkY, pOffsetX, pOffsetY, '#0284c7', isAnticipating, 0.24);
      drawOpenSmile(ctx, 0, u * 0.25, u * 0.38, '#db2777', isAnticipating);
    }

    // 6: Eyes at Top Edge of Row 2 with Coral-Red Rims + 3 Outer Eyelashes Each; Wide Pink Open Smile Across Row 1/2 Seam
    else if (faceDef.type === 'dice') {
      const eyeR = u * 0.155;
      const eyeSpacing = u * 0.56;
      const eyeY = -u * 0.36; // sits near top edge of row 2, keeping all 6 pips 100% visible

      // 3 distinct outer eyelashes on EACH eye (6 eyelashes total)
      const sides = [-1, 1];
      for (let s = 0; s < 2; s++) {
        const dir = sides[s];
        const ex = dir * eyeSpacing;
        const lashAngles = [-0.95, -0.55, -0.15];
        ctx.save();
        ctx.lineWidth = Math.max(1.3, u * 0.038);
        ctx.strokeStyle = '#dc2626';
        ctx.lineCap = 'round';
        for (let l = 0; l < 3; l++) {
          const a = dir < 0 ? Math.PI - lashAngles[l] : lashAngles[l];
          ctx.beginPath();
          ctx.moveTo(ex + Math.cos(a) * eyeR * 0.95, eyeY + Math.sin(a) * eyeR * 0.95);
          ctx.lineTo(ex + Math.cos(a) * eyeR * 1.65, eyeY + Math.sin(a) * eyeR * 1.65);
          ctx.stroke();
        }
        ctx.restore();
      }

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#dc2626', isAnticipating, 0.25);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#dc2626', isAnticipating, 0.25);

      // Wide pink-rimmed open smile across row 1/2 seam (y = +0.46u from anchorRow 2.48 => row 2.02)
      drawOpenSmile(ctx, 0, u * 0.45, u * 0.58, '#ec4899', isAnticipating);
    }

    // 7: 7 Bold Flat-Topped Rainbow Hair Bars, Connected Yellow Goggles, Yellow-Rimmed Open Smile
    else if (faceDef.type === 'rainbow') {
      const eyeR = u * 0.16;
      const eyeSpacing = u * 0.22;
      const eyeY = -u * 0.06;

      // 7 bold flat-topped vertical/fanning rainbow hair bars across top of row 6
      ctx.save();
      ctx.translate(0, -u * 0.52);
      const rainbowColors = ['#ef4444', '#f97316', '#facc15', '#22c55e', '#38bdf8', '#4f46e5', '#9333ea'];
      const barW = u * 0.105;
      for (let i = 0; i < 7; i++) {
        const offsetIdx = i - 3;
        const bx = offsetIdx * (u * 0.115);
        const angle = offsetIdx * 0.11;
        const bh = u * (0.33 - Math.abs(offsetIdx) * 0.015);
        ctx.save();
        ctx.translate(bx, 2);
        ctx.rotate(angle);
        drawRoundRect(ctx, -barW / 2, -bh, barW, bh, barW * 0.18);
        ctx.fillStyle = rainbowColors[i];
        ctx.fill();
        ctx.restore();
      }
      ctx.restore();

      // Connected Yellow-Gold Rounded Goggles
      const gogW = u * 0.44;
      const gogH = u * 0.36;
      ctx.save();
      // Bridge
      ctx.beginPath();
      ctx.moveTo(-eyeSpacing + gogW * 0.45, eyeY);
      ctx.lineTo(eyeSpacing - gogW * 0.45, eyeY);
      ctx.lineWidth = Math.max(2, u * 0.08);
      ctx.strokeStyle = '#ca8a04';
      ctx.stroke();
      ctx.lineWidth = Math.max(1.4, u * 0.05);
      ctx.strokeStyle = '#facc15';
      ctx.stroke();

      for (let g = 0; g < 2; g++) {
        const gx = g === 0 ? -eyeSpacing : eyeSpacing;
        drawRoundRect(ctx, gx - gogW / 2, eyeY - gogH / 2, gogW, gogH, gogH * 0.45);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.lineWidth = Math.max(1.8, u * 0.075);
        ctx.strokeStyle = '#facc15';
        ctx.stroke();
        ctx.lineWidth = Math.max(0.8, u * 0.022);
        ctx.strokeStyle = '#ca8a04';
        ctx.stroke();
      }
      ctx.restore();

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR * 0.88, blinkY, pOffsetX, pOffsetY, '#ca8a04', isAnticipating, 0.08);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR * 0.88, blinkY, pOffsetX, pOffsetY, '#ca8a04', isAnticipating, 0.08);
      drawOpenSmile(ctx, 0, u * 0.25, u * 0.42, '#facc15', isAnticipating);
    }

    // 8: Pale-Pink Pointed Superhero Mask Visor + Happy Open Smile
    else if (faceDef.type === 'octoMask') {
      const eyeR = u * 0.165;
      const eyeSpacing = u * 0.32;
      const eyeY = -u * 0.04;

      // Pale-pink (#fbcfe8, stroke #db2777) pointed superhero mask visor
      ctx.save();
      ctx.beginPath();
      ctx.moveTo(-eyeSpacing * 1.9, eyeY - eyeR * 1.55);
      ctx.quadraticCurveTo(0, eyeY - eyeR * 0.65, eyeSpacing * 1.9, eyeY - eyeR * 1.55);
      ctx.quadraticCurveTo(eyeSpacing * 1.65, eyeY + eyeR * 1.45, eyeSpacing * 0.85, eyeY + eyeR * 1.25);
      ctx.quadraticCurveTo(0, eyeY + eyeR * 0.55, -eyeSpacing * 0.85, eyeY + eyeR * 1.25);
      ctx.quadraticCurveTo(-eyeSpacing * 1.65, eyeY + eyeR * 1.45, -eyeSpacing * 1.9, eyeY - eyeR * 1.55);
      ctx.closePath();
      ctx.fillStyle = '#fbcfe8';
      ctx.fill();
      ctx.lineWidth = Math.max(1.4, u * 0.045);
      ctx.strokeStyle = '#db2777';
      ctx.lineJoin = 'round';
      ctx.stroke();
      ctx.restore();

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9d174d', isAnticipating, 0.22);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9d174d', isAnticipating, 0.22);
      drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.16, u * 0.46, '#9d174d', isAnticipating);
    }

    // 9: Square Eyes with Teal/Slate Square Frames, Thick #334155 Rectangular Brows, Open Smile
    else if (faceDef.type === 'squareSpecs') {
      const eyeW = u * 0.32;
      const eyeSpacing = u * 0.42;
      const eyeY = -u * 0.05;

      // Thick #334155 rectangular eyebrows
      const browW = eyeW * 1.15;
      const browH = Math.max(2, u * 0.085);
      ctx.fillStyle = '#334155';
      drawRoundRect(ctx, -eyeSpacing - browW / 2, eyeY - eyeW / 2 - browH - u * 0.05, browW, browH, browH * 0.25);
      ctx.fill();
      drawRoundRect(ctx, eyeSpacing - browW / 2, eyeY - eyeW / 2 - browH - u * 0.05, browW, browH, browH * 0.25);
      ctx.fill();

      const sqOffsets = [-eyeSpacing, eyeSpacing];
      for (let i = 0; i < 2; i++) {
        ctx.save();
        ctx.translate(sqOffsets[i], eyeY);
        ctx.scale(1, blinkY);
        drawRoundRect(ctx, -eyeW / 2, -eyeW / 2, eyeW, eyeW, Math.max(1.5, u * 0.055));
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.lineWidth = Math.max(1.4, u * 0.05);
        ctx.strokeStyle = '#334155';
        ctx.stroke();

        if (blinkY > 0.25) {
          const pOff = clamp(pOffsetX, -eyeW * 0.22, eyeW * 0.22);
          const pOffY = clamp(pOffsetY, -eyeW * 0.22, eyeW * 0.22);
          const pupSize = eyeW * 0.46;
          drawRoundRect(ctx, -pupSize / 2 + pOff, -pupSize / 2 + pOffY, pupSize, pupSize, Math.max(1, pupSize * 0.16));
          ctx.fillStyle = '#0f172a';
          ctx.fill();
          ctx.fillStyle = '#ffffff';
          ctx.fillRect(-pupSize * 0.32 + pOff, -pupSize * 0.32 + pOffY, pupSize * 0.28, pupSize * 0.28);
        }
        ctx.restore();
      }

      drawOpenSmile(ctx, 0, eyeY + eyeW / 2 + u * 0.18, u * 0.48, '#334155', isAnticipating);
    }

    // 10: Twin Bright-Red 5-Pointed Star Borders on Both Eyes + Joyful Red-Lipped Smile + Rocket Flames
    else if (faceDef.type === 'starTwin') {
      const eyeR = u * 0.165;
      const eyeSpacing = u * 0.36;
      const eyeY = -u * 0.04;

      drawStar(ctx, -eyeSpacing, eyeY, 5, eyeR * 2.1, eyeR * 0.95, '#ef4444', '#b91c1c', Math.max(1.2, u * 0.03));
      drawStar(ctx, eyeSpacing, eyeY, 5, eyeR * 2.1, eyeR * 0.95, '#ef4444', '#b91c1c', Math.max(1.2, u * 0.03));

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#991b1b', isAnticipating, 0.20);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#991b1b', isAnticipating, 0.20);
      drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.18, u * 0.48, '#dc2626', isAnticipating);

      // Flickering Rocket Flames under Boots on Jump / Tap / Celebrate
      const flameActive = (!isStatic && entity && (tapP > 0 || entity.state === 'CELEBRATING' || entity.vy < -50));
      if (flameActive) {
        ctx.save();
        ctx.translate(0, -faceY); // local groundY (0) right under boots
        const flicker = 1.0 + Math.sin(nowMs * 0.03) * 0.25;
        const fH = u * 0.85 * flicker;
        const bootOffsets = [-u * 0.55, u * 0.55];
        for (let b = 0; b < 2; b++) {
          const bx = bootOffsets[b];
          ctx.beginPath();
          ctx.moveTo(bx - u * 0.24, 0);
          ctx.quadraticCurveTo(bx, fH * 1.30, bx + u * 0.24, 0);
          ctx.fillStyle = '#ef4444';
          ctx.fill();

          ctx.beginPath();
          ctx.moveTo(bx - u * 0.16, 0);
          ctx.quadraticCurveTo(bx, fH * 0.95, bx + u * 0.16, 0);
          ctx.fillStyle = '#f97316';
          ctx.fill();

          ctx.beginPath();
          ctx.moveTo(bx - u * 0.08, 0);
          ctx.quadraticCurveTo(bx, fH * 0.60, bx + u * 0.08, 0);
          ctx.fillStyle = '#fef08a';
          ctx.fill();
        }
        ctx.restore();
      }
    }

    // 12: Super-Rectangle Twelve (Centered across 3x4 top, Orange Array Visor Glasses)
    else if (faceDef.type === 'superRect12') {
      const eyeR = u * 0.17;
      const eyeSpacing = u * 0.44;
      const eyeY = -u * 0.04;

      // Signature orange/white rectangular meditation visor frames
      const frameW = u * 0.52;
      const frameH = u * 0.40;
      drawRoundRect(ctx, -eyeSpacing - frameW / 2, eyeY - frameH / 2, frameW, frameH, u * 0.09);
      ctx.fillStyle = '#ffffff';
      ctx.fill();
      ctx.lineWidth = Math.max(1.8, u * 0.065);
      ctx.strokeStyle = '#ea580c';
      ctx.stroke();

      drawRoundRect(ctx, eyeSpacing - frameW / 2, eyeY - frameH / 2, frameW, frameH, u * 0.09);
      ctx.fillStyle = '#ffffff';
      ctx.fill();
      ctx.stroke();

      ctx.beginPath();
      ctx.moveTo(-eyeSpacing + frameW / 2, eyeY);
      ctx.lineTo(eyeSpacing - frameW / 2, eyeY);
      ctx.stroke();

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR * 0.85, blinkY, pOffsetX, pOffsetY, '#ea580c', isAnticipating, 0.12);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR * 0.85, blinkY, pOffsetX, pOffsetY, '#ea580c', isAnticipating, 0.12);
      drawOpenSmile(ctx, 0, eyeY + u * 0.34, u * 0.48, '#ea580c', isAnticipating);
    }

    // 11, 13-19: Compound Teen Friends with Signature Facial Accents
    else if (faceDef.type === 'teenCompound') {
      const unitN = faceDef.unitN || (char.n - 10);
      const eyeR = u * 0.165;
      const eyeSpacing = u * 0.34;
      const eyeY = -u * 0.04;

      if (unitN === 1) {
        // 11: Asymmetric football eyes! Left eye red-rimmed, right eye soccer/football style
        drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR * 0.95, blinkY, pOffsetX, pOffsetY, '#dc2626', isAnticipating, 0.24);
        // Larger football eye on right
        ctx.save();
        ctx.translate(eyeSpacing, eyeY);
        ctx.scale(1, blinkY);
        const fR = eyeR * 1.25;
        ctx.beginPath();
        ctx.arc(0, 0, fR, 0, Math.PI * 2);
        ctx.fillStyle = '#ffffff';
        ctx.fill();
        ctx.lineWidth = Math.max(1.4, fR * 0.18);
        ctx.strokeStyle = '#0f172a';
        ctx.stroke();
        if (blinkY > 0.25) {
          // Football pentagon pupil + seam lines
          drawStar(ctx, pOffsetX * 0.5, pOffsetY * 0.5, 5, fR * 0.46, fR * 0.36, '#0f172a', null);
          ctx.beginPath();
          ctx.arc(pOffsetX * 0.5 - fR * 0.15, pOffsetY * 0.5 - fR * 0.15, fR * 0.14, 0, Math.PI * 2);
          ctx.fillStyle = '#ffffff';
          ctx.fill();
        }
        ctx.restore();
        drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.16, u * 0.44, '#dc2626', isAnticipating);
      } else if (unitN === 5) {
        // 15: Step-Squad Cyan Star Eye Mask
        drawStar(ctx, -eyeSpacing, eyeY, 5, eyeR * 2.0, eyeR * 0.95, '#0284c7', '#1e3a8a', Math.max(1.2, u * 0.03));
        drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#1e3a8a', isAnticipating, 0.22);
        drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#0284c7', isAnticipating, 0.22);
        drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.16, u * 0.44, '#db2777', isAnticipating);
      } else if (unitN === 8) {
        // 18: Speed-Ray Pink Visor
        drawRoundRect(ctx, -eyeSpacing * 1.75, eyeY - eyeR * 1.2, eyeSpacing * 3.5, eyeR * 2.4, eyeR);
        ctx.fillStyle = '#fbcfe8';
        ctx.fill();
        ctx.lineWidth = Math.max(1.4, u * 0.045);
        ctx.strokeStyle = '#db2777';
        ctx.stroke();
        drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9d174d', isAnticipating, 0.22);
        drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9d174d', isAnticipating, 0.22);
        drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.16, u * 0.44, '#be185d', isAnticipating);
      } else {
        const accentMap = {
          3: '#ca8a04',
          4: '#15803d',
          6: '#6366f1',
          7: '#9333ea',
          9: '#475569'
        };
        const rim = accentMap[unitN] || '#dc2626';
        drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, rim, isAnticipating, 0.24);
        drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, rim, isAnticipating, 0.24);
        drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.16, u * 0.44, rim, isAnticipating);
      }
    }

    // 20: Big Twenty Classy Top Hat, Twin Orange Stars, Bow Tie
    else if (faceDef.type === 'twentyTopHat') {
      const eyeR = u * 0.18;
      const eyeSpacing = u * 0.48;
      const eyeY = -u * 0.04;

      // Classy Top Hat sitting cleanly on top of row 4
      ctx.save();
      ctx.translate(0, -u * 0.52);
      if (tapP > 0) {
        ctx.rotate(Math.sin(tapP * Math.PI) * -0.28);
      }
      // Brim
      drawRoundRect(ctx, -u * 0.85, -u * 0.08, u * 1.7, u * 0.13, u * 0.06);
      ctx.fillStyle = '#1e293b';
      ctx.fill();
      // Crown
      drawRoundRect(ctx, -u * 0.52, -u * 0.66, u * 1.04, u * 0.60, u * 0.08);
      ctx.fillStyle = '#0f172a';
      ctx.fill();
      // Gold Hat Band
      drawRoundRect(ctx, -u * 0.52, -u * 0.24, u * 1.04, u * 0.14, 2);
      ctx.fillStyle = '#facc15';
      ctx.fill();
      ctx.restore();

      // Twin Orange Stars
      drawStar(ctx, -eyeSpacing, eyeY, 5, eyeR * 2.0, eyeR * 0.92, '#f97316', '#c2410c', Math.max(1.2, u * 0.03));
      drawStar(ctx, eyeSpacing, eyeY, 5, eyeR * 2.0, eyeR * 0.92, '#f97316', '#c2410c', Math.max(1.2, u * 0.03));

      drawPupilEye(ctx, -eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9a3412', isAnticipating, 0.22);
      drawPupilEye(ctx, eyeSpacing, eyeY, eyeR, blinkY, pOffsetX, pOffsetY, '#9a3412', isAnticipating, 0.22);
      drawOpenSmile(ctx, 0, eyeY + eyeR + u * 0.18, u * 0.52, '#c2410c', isAnticipating);

      // Dapper Orange-Red Bow Tie below smile
      const bowY = eyeY + eyeR + u * 0.62;
      ctx.save();
      ctx.translate(0, bowY);
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.lineTo(-u * 0.28, -u * 0.14);
      ctx.lineTo(-u * 0.28, u * 0.14);
      ctx.closePath();
      ctx.moveTo(0, 0);
      ctx.lineTo(u * 0.28, -u * 0.14);
      ctx.lineTo(u * 0.28, u * 0.14);
      ctx.closePath();
      ctx.fillStyle = '#ea580c';
      ctx.fill();
      ctx.lineWidth = Math.max(1, u * 0.025);
      ctx.strokeStyle = '#9a3412';
      ctx.stroke();
      ctx.beginPath();
      ctx.arc(0, 0, u * 0.08, 0, Math.PI * 2);
      ctx.fillStyle = '#facc15';
      ctx.fill();
      ctx.stroke();
      ctx.restore();
    }

    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Floating Fredoka Numberling (positioned cleanly above headgear)
  // --------------------------------------------------------------------------
  function drawNumberling(ctx, entity, char, u, nowMs) {
    const legH = getLegHeight(u);
    const headgearH = getHeadgearHeight(char.n, u);
    const totalH = char.rows * u;
    const bob = Math.sin(nowMs * 0.0032 + entity.id * 1.5) * 3.5;
    const numY = -legH - totalH - headgearH - (u * 0.44) + bob;

    ctx.save();
    ctx.font = '700 ' + Math.round(u * 0.60) + "px 'Fredoka', 'Nunito', sans-serif";
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';

    const text = String(entity.n);

    // Crisp White Sticker Stroke
    ctx.lineWidth = 6;
    ctx.lineJoin = 'round';
    ctx.strokeStyle = '#ffffff';
    ctx.strokeText(text, 0, numY);

    // Bold Slate Fill
    ctx.fillStyle = '#0f172a';
    ctx.fillText(text, 0, numY);
    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Split Badge [<>] & Taffy-Stretch Tether
  // --------------------------------------------------------------------------
  function drawSplitBadge(ctx, badgeRect, alpha) {
    if (alpha <= 0.01) return;
    ctx.save();
    ctx.globalAlpha = alpha;

    const { cx, cy, r } = badgeRect;

    // Soft offset halo instead of GPU-stalling shadowBlur
    ctx.beginPath();
    ctx.arc(cx, cy + 2.5, r + 1.5, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(37, 99, 235, 0.18)';
    ctx.fill();

    ctx.beginPath();
    ctx.arc(cx, cy, r, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.96)';
    ctx.fill();

    ctx.lineWidth = 2.5;
    ctx.strokeStyle = '#3b82f6';
    ctx.stroke();

    ctx.fillStyle = '#2563eb';
    ctx.beginPath();
    ctx.moveTo(cx - 10, cy);
    ctx.lineTo(cx - 3, cy - 6);
    ctx.lineTo(cx - 3, cy + 6);
    ctx.closePath();
    ctx.fill();

    ctx.beginPath();
    ctx.arc(cx, cy, 2, 0, Math.PI * 2);
    ctx.fill();

    ctx.beginPath();
    ctx.moveTo(cx + 10, cy);
    ctx.lineTo(cx + 3, cy - 6);
    ctx.lineTo(cx + 3, cy + 6);
    ctx.closePath();
    ctx.fill();

    ctx.restore();
  }

  function drawTaffyStretch(ctx, stretchInfo, metrics) {
    if (!stretchInfo) return;
    const { anchorX, anchorY, pullX, pullY, ratio, partB } = stretchInfo;
    const dist = Math.hypot(pullX - anchorX, pullY - anchorY);
    if (dist < 4) return;

    ctx.save();

    const thickness = Math.max(6, 26 * (1.0 - Math.min(ratio, 0.85)));
    const angle = Math.atan2(pullY - anchorY, pullX - anchorX);
    const perp = angle + Math.PI / 2;

    const ax1 = anchorX + Math.cos(perp) * (thickness * 1.2);
    const ay1 = anchorY + Math.sin(perp) * (thickness * 1.2);
    const ax2 = anchorX - Math.cos(perp) * (thickness * 1.2);
    const ay2 = anchorY - Math.sin(perp) * (thickness * 1.2);

    const px1 = pullX + Math.cos(perp) * (thickness * 0.8);
    const py1 = pullY + Math.sin(perp) * (thickness * 0.8);
    const px2 = pullX - Math.cos(perp) * (thickness * 0.8);
    const py2 = pullY - Math.sin(perp) * (thickness * 0.8);

    const midX = (anchorX + pullX) / 2;
    const midY = (anchorY + pullY) / 2;

    ctx.beginPath();
    ctx.moveTo(ax1, ay1);
    ctx.quadraticCurveTo(midX, midY, px1, py1);
    ctx.lineTo(px2, py2);
    ctx.quadraticCurveTo(midX, midY, ax2, ay2);
    ctx.closePath();

    ctx.fillStyle = ratio >= 1.0 ? 'rgba(250, 204, 21, 0.85)' : 'rgba(147, 197, 253, 0.75)';
    ctx.fill();
    ctx.lineWidth = 2.5;
    ctx.strokeStyle = ratio >= 1.0 ? '#ca8a04' : '#3b82f6';
    ctx.stroke();

    ctx.beginPath();
    ctx.arc(pullX, pullY, Math.max(16, metrics.unitSize * 0.42), 0, Math.PI * 2);
    ctx.fillStyle = '#ffffff';
    ctx.fill();
    ctx.lineWidth = 3;
    ctx.strokeStyle = ratio >= 1.0 ? '#f59e0b' : '#3b82f6';
    ctx.stroke();

    ctx.font = "700 16px 'Fredoka', 'Nunito', sans-serif";
    ctx.fillStyle = '#1e293b';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText(String(partB), pullX, pullY + 1);

    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Floating Equation Pill
  // --------------------------------------------------------------------------
  function drawEquationPill(ctx, pill, metrics) {
    if (!pill || pill.alpha <= 0.01) return;

    ctx.save();
    ctx.globalAlpha = pill.alpha;

    const scale = pill.scale || 1.0;
    const clampedY = Math.max(metrics.topSafeY + 24, pill.y);

    ctx.translate(pill.x, clampedY);
    ctx.scale(scale, scale);

    let textStr = '';
    if (pill.mode === 'preview') {
      textStr = pill.leftN + ' + ' + pill.rightN + ' = ✨ ?';
    } else if (pill.mode === 'merge') {
      textStr = pill.leftN + ' + ' + pill.rightN + ' = ' + pill.sumN + '!';
    } else if (pill.mode === 'split') {
      textStr = pill.leftN + ' = ' + pill.rightN + ' + ' + pill.sumN + '!';
    } else if (pill.mode === 'boom') {
      textStr = pill.leftN + ' + ' + pill.rightN + ' = 💥 BOOM!';
    } else {
      textStr = pill.leftN + ' + ' + pill.rightN + ' = ' + (pill.sumN || '?');
    }

    ctx.font = "700 17px 'Fredoka', 'Nunito', sans-serif";
    const textW = ctx.measureText(textStr).width;
    const pillW = textW + 36;
    const pillH = 38;

    // Soft offset backing pill instead of GPU-stalling shadowBlur
    drawRoundRect(ctx, -pillW / 2, -pillH / 2 + 4, pillW, pillH, pillH / 2);
    ctx.fillStyle = 'rgba(15, 23, 42, 0.12)';
    ctx.fill();

    drawRoundRect(ctx, -pillW / 2, -pillH / 2, pillW, pillH, pillH / 2);
    ctx.fillStyle = 'rgba(255, 255, 255, 0.97)';
    ctx.fill();

    ctx.lineWidth = 2;
    ctx.strokeStyle = '#e2e8f0';
    ctx.stroke();

    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillStyle = '#1e293b';
    ctx.fillText(textStr, 0, 1);

    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Magnetic Snap Preview Aura & Ghost
  // --------------------------------------------------------------------------
  function drawSnapPreview(ctx, snap, metrics) {
    if (!snap) return;
    ctx.save();

    const u = metrics.unitSize;
    const pulse = snap.pulse || 0;
    const auraR = u * (1.1 + 0.18 * Math.sin(pulse * Math.PI * 2));
    const auraColor = snap.exceedsCap ? 'rgba(236, 72, 153, 0.75)' : 'rgba(250, 204, 21, 0.75)';

    ctx.beginPath();
    ctx.arc(snap.x, snap.y - u * 1.2, auraR, 0, Math.PI * 2);
    ctx.lineWidth = 3;
    ctx.setLineDash([8, 6]);
    ctx.strokeStyle = auraColor;
    ctx.stroke();
    ctx.setLineDash([]);

    const targetChar = getCharacter(snap.sum);
    if (targetChar) {
      const gU = (targetChar.unitScale || 1.0) * u;
      const gLegH = getLegHeight(gU);
      const totalW = targetChar.cols * gU;
      const startX = snap.x - totalW / 2;
      const startY = snap.y;

      ctx.globalAlpha = 0.28;
      for (let i = 0; i < targetChar.cells.length; i++) {
        const c = targetChar.cells[i];
        const cx = startX + c.col * gU;
        const cy = startY - gLegH - (c.row + 1) * gU;
        drawRoundRect(ctx, cx, cy, gU, gU, Math.max(2, gU * 0.065));
        ctx.fillStyle = c.palette ? c.palette.base : '#facc15';
        ctx.fill();
        ctx.lineWidth = 1.5;
        ctx.strokeStyle = '#ffffff';
        ctx.stroke();
      }
    }

    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Onboarding Arc
  // --------------------------------------------------------------------------
  function drawOnboardingArc(ctx, arc) {
    if (!arc || arc.alpha <= 0.01) return;
    ctx.save();
    ctx.globalAlpha = arc.alpha;

    const { fromX, fromY, toX, toY, phase } = arc;
    const midX = (fromX + toX) / 2;
    const midY = Math.min(fromY, toY) - 55;

    ctx.beginPath();
    ctx.moveTo(fromX, fromY);
    ctx.quadraticCurveTo(midX, midY, toX, toY);
    ctx.lineWidth = 3.5;
    ctx.setLineDash([8, 8]);
    ctx.strokeStyle = '#3b82f6';
    ctx.stroke();
    ctx.setLineDash([]);

    const t = phase;
    const px = (1 - t) * (1 - t) * fromX + 2 * (1 - t) * t * midX + t * t * toX;
    const py = (1 - t) * (1 - t) * fromY + 2 * (1 - t) * t * midY + t * t * toY;

    ctx.font = '28px sans-serif';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText('👆', px, py);

    ctx.restore();
  }

  // --------------------------------------------------------------------------
  // Renderer Instance State & Public API Implementation
  // --------------------------------------------------------------------------
  let canvas = null;
  let hudOverlay = null;
  let ctx2d = null;
  let cachedSkyGrad = null;
  let cachedTurfGrad = null;
  let cachedGradGroundY = -1;
  let cachedGradHeight = -1;
  const sortedEntitiesBuf = [];
  let cachedMetrics = {
    width: 0,
    height: 0,
    dpr: 1,
    unitSize: 48,
    topSafeY: 12,
    groundY: 400
  };
  let lastTimeMs = performance.now();

  function rebuildBackgroundGradients(groundY, height) {
    if (!ctx2d || height <= 0) return;
    if (cachedSkyGrad && cachedTurfGrad && cachedGradGroundY === groundY && cachedGradHeight === height) {
      return;
    }
    const skyGrad = ctx2d.createLinearGradient(0, 0, 0, Math.max(1, groundY));
    skyGrad.addColorStop(0, '#bae6fd');
    skyGrad.addColorStop(0.48, '#e0f2fe');
    skyGrad.addColorStop(0.78, '#fef9c3');
    skyGrad.addColorStop(1.0, '#dcfce7');
    cachedSkyGrad = skyGrad;

    const turfGrad = ctx2d.createLinearGradient(0, groundY, 0, Math.max(groundY + 1, height));
    turfGrad.addColorStop(0, '#4ade80');
    turfGrad.addColorStop(1, '#22c55e');
    cachedTurfGrad = turfGrad;

    cachedGradGroundY = groundY;
    cachedGradHeight = height;
  }

  function resize() {
    if (!canvas) return cachedMetrics;
    const rect = canvas.getBoundingClientRect();
    if (rect.width === 0 || rect.height === 0) return cachedMetrics;

    const dpr = Math.min(window.devicePixelRatio || 1, 3);
    const targetW = Math.round(rect.width * dpr);
    const targetH = Math.round(rect.height * dpr);
    if (canvas.width !== targetW || canvas.height !== targetH) {
      canvas.width = targetW;
      canvas.height = targetH;
      cachedSkyGrad = null;
      cachedTurfGrad = null;
    }

    let topSafe = 12;
    if (hudOverlay && hudOverlay.children) {
      for (let i = 0; i < hudOverlay.children.length; i++) {
        const child = hudOverlay.children[i];
        if (child.classList.contains('hidden') || child.offsetParent === null) continue;
        const cRect = child.getBoundingClientRect();
        if (cRect.height > 0) {
          const bottomY = cRect.bottom - rect.top + 8;
          topSafe = Math.max(topSafe, bottomY);
        }
      }
    }

    const ground = Math.round(rect.height - 18);
    const playH = Math.max(100, ground - topSafe - 24);
    const unitSize = Math.round(clamp(28, Math.min(rect.width / 8.2, playH / 8.2), 64));

    cachedMetrics = {
      width: rect.width,
      height: rect.height,
      dpr: dpr,
      unitSize: unitSize,
      topSafeY: topSafe,
      groundY: ground
    };

    rebuildBackgroundGradients(ground, rect.height);

    return cachedMetrics;
  }

  function getMetrics() {
    return cachedMetrics;
  }

  function getEntityBounds(entity, metrics) {
    if (!entity) return null;
    const m = metrics || cachedMetrics;
    const char = getCharacter(entity.n || 1);
    const unitScale = (char && char.unitScale) ? char.unitScale : 1.0;
    const u = unitScale * (m ? m.unitSize : 48);

    const cols = char ? char.cols : 1;
    const rows = char ? char.rows : 1;
    const legH = getLegHeight(u);
    const headgearH = getHeadgearHeight(char ? char.n : 1, u);

    const width = cols * u;
    const height = rows * u + legH + headgearH;
    const left = entity.x - width / 2;
    const right = left + width;
    const bottom = entity.y;
    const top = entity.y - height;

    return {
      x: entity.x,
      y: entity.y,
      u: u,
      cols: cols,
      rows: rows,
      legH: legH,
      headgearH: headgearH,
      width: width,
      height: height,
      left: left,
      right: right,
      top: top,
      bottom: bottom,
      centerX: entity.x,
      centerY: entity.y - height / 2
    };
  }

  function getSplitBadgeRect(entity, metrics) {
    const m = metrics || cachedMetrics;
    const bounds = getEntityBounds(entity, m);
    if (!bounds) return { cx: 0, cy: 0, r: 24 };

    return {
      cx: Math.min(m.width - 28, bounds.right + 16),
      cy: Math.max(m.topSafeY + 26, bounds.top + 8),
      r: 24
    };
  }

  function spawnBurst(x, y, presetOrColors, maybeCount, maybeKind) {
    const tlh = window.ToddlerLearningHub;
    const settings = (tlh && tlh.app && tlh.app.settings) || (typeof app !== 'undefined' && app.settings);
    if (settings && settings.confettiEnabled === false) return;

    let preset = typeof presetOrColors === 'string' ? presetOrColors : (maybeKind || 'mergeStarburst');
    let customColor = typeof maybeCount === 'string' ? maybeCount : null;

    if (preset === 'mergeStarburst') {
      const colors = ['#facc15', '#fef08a', '#ef4444', '#3b82f6', '#22c55e', '#a855f7'];
      const count = typeof maybeCount === 'number' ? maybeCount : 28;
      for (let i = 0; i < count; i++) {
        const angle = (i * Math.PI * 2) / count + (Math.random() - 0.5) * 0.4;
        const speed = 120 + Math.random() * 260;
        const color = customColor || colors[i % colors.length];
        const shape = i % 2 === 0 ? 'star' : 'circle';
        activateParticle(x, y, Math.cos(angle) * speed, Math.sin(angle) * speed, 6 + Math.random() * 7, 0.65 + Math.random() * 0.4, color, shape, 320, 0);
      }
    } else if (preset === 'splitPop') {
      const count = typeof maybeCount === 'number' ? maybeCount : 16;
      for (let i = 0; i < count; i++) {
        const vx = (Math.random() - 0.5) * 280;
        const vy = -120 - Math.random() * 200;
        activateParticle(x, y, vx, vy, 5 + Math.random() * 5, 0.55 + Math.random() * 0.35, '#38bdf8', 'circle', 420, 0);
      }
    } else if (preset === 'highFive') {
      const colors = ['#f43f5e', '#f97316', '#eab308', '#22c55e', '#06b6d4', '#8b5cf6'];
      const count = typeof maybeCount === 'number' ? maybeCount : 32;
      for (let i = 0; i < count; i++) {
        const angle = Math.random() * Math.PI * 2;
        const speed = 150 + Math.random() * 320;
        activateParticle(x, y, Math.cos(angle) * speed, Math.sin(angle) * speed, 7 + Math.random() * 8, 0.75 + Math.random() * 0.4, colors[i % colors.length], 'star', 300, 0);
      }
    } else if (preset === 'rocketPuff') {
      const colors = ['#ef4444', '#f97316', '#fef08a', '#ffffff'];
      for (let i = 0; i < 16; i++) {
        const vx = (Math.random() - 0.5) * 120;
        const vy = 60 + Math.random() * 180;
        activateParticle(x, y, vx, vy, 4 + Math.random() * 6, 0.45 + Math.random() * 0.3, colors[i % colors.length], 'smoke', 40, 0);
      }
    } else if (preset === 'sneezeStars') {
      const colors = ['#cbd5e1', '#94a3b8', '#64748b', '#ffffff'];
      for (let i = 0; i < 14; i++) {
        const vx = (Math.random() - 0.5) * 240;
        const vy = -60 - Math.random() * 180;
        activateParticle(x, y, vx, vy, 4 + Math.random() * 5, 0.5 + Math.random() * 0.3, colors[i % colors.length], 'star', 360, 0);
      }
    } else if (preset === 'poofOut') {
      for (let i = 0; i < 16; i++) {
        const angle = (i * Math.PI * 2) / 16;
        const speed = 40 + Math.random() * 80;
        activateParticle(x, y, Math.cos(angle) * speed, Math.sin(angle) * speed - 30, 8 + Math.random() * 8, 0.5 + Math.random() * 0.3, 'rgba(255, 255, 255, 0.85)', 'smoke', -20, 0);
      }
    } else if (preset === 'tapSparkle') {
      for (let i = 0; i < 8; i++) {
        const vx = (Math.random() - 0.5) * 140;
        const vy = -80 - Math.random() * 140;
        activateParticle(x, y, vx, vy, 5 + Math.random() * 4, 0.4 + Math.random() * 0.3, '#facc15', 'star', 200, 0);
      }
    }
  }

  // --------------------------------------------------------------------------
  // Full Mini-Character Dock Icons & High-Res Quiz Cards
  // --------------------------------------------------------------------------
  function renderDockIcon(canvasEl, n, isUnlocked, cssPx) {
    if (!canvasEl) return;
    const px = cssPx || 40;
    const dpr = Math.min(window.devicePixelRatio || 1, 3);

    canvasEl.width = Math.round(px * dpr);
    canvasEl.height = Math.round(px * dpr);
    canvasEl.style.width = px + 'px';
    canvasEl.style.height = px + 'px';

    const ictx = canvasEl.getContext('2d');
    if (!ictx) return;

    ictx.save();
    ictx.scale(dpr, dpr);
    ictx.clearRect(0, 0, px, px);

    if (!isUnlocked) {
      drawRoundRect(ictx, 4, 4, px - 8, px - 8, 8);
      ictx.fillStyle = '#cbd5e1';
      ictx.fill();
      ictx.lineWidth = 2;
      ictx.strokeStyle = '#94a3b8';
      ictx.stroke();

      ictx.font = "700 " + Math.round(px * 0.50) + "px 'Fredoka', 'Nunito', sans-serif";
      ictx.fillStyle = '#64748b';
      ictx.textAlign = 'center';
      ictx.textBaseline = 'middle';
      ictx.fillText('?', px / 2, px / 2 + 1);
      ictx.restore();
      return;
    }

    const char = getCharacter(n);
    if (!char) {
      ictx.restore();
      return;
    }

    // Compute full visual extent (blocks + arms/hands/tentacles + legs/shoes + headgear)
    const leftReach = char.n === 8 ? 0.58 : 0.48;
    const rightReach = char.n === 5 ? 0.85 : (char.n === 8 ? 0.58 : 0.48);
    let topReach = 0.08;
    if (char.n === 3) topReach = 0.46;
    else if (char.n === 6) topReach = 0.28;
    else if (char.n === 7) topReach = 0.44;
    else if (char.n === 20) topReach = 0.70;
    const bottomReach = 0.24; // legH

    const spanW = char.cols + leftReach + rightReach;
    const spanH = char.rows + topReach + bottomReach;
    const avail = px * 0.86;
    const u = Math.min(avail / spanW, avail / spanH);

    // Center the full character bounding box inside px x px
    const originX = px / 2 + ((leftReach - rightReach) / 2) * u;
    const originY = px / 2 + (spanH * u) / 2;

    const syntheticEnt = {
      id: char.n,
      n: char.n,
      x: 0,
      y: 0,
      state: 'IDLE',
      expression: 'happy',
      tapProgress: 0
    };

    ictx.save();
    ictx.translate(originX, originY);

    // 1. Limbs behind block grid
    drawCharacterLimbsBack(ictx, syntheticEnt, char, u, 0, true);

    // 2. Flush Snap-Together Blocks + Cell Decorations
    const legH = getLegHeight(u);
    const startX = -(char.cols * u) / 2;
    for (let i = 0; i < char.cells.length; i++) {
      const c = char.cells[i];
      const cx = startX + c.col * u;
      const cy = -legH - (c.row + 1) * u;
      drawUnitBlock(ictx, cx, cy, u, c.palette, 0);
      drawCellDecoration(ictx, c, cx, cy, u);
    }

    // 3. Front limbs (5's High-Five star hand) & Canonical Face + Headgear
    drawCharacterLimbsFront(ictx, syntheticEnt, char, u, 0, true);
    drawCharacterFaceAndProps(ictx, syntheticEnt, char, u, null, 0, true);

    ictx.restore();
    ictx.restore();
  }

  const quizCardCache = new Map();

  function getQuizCardHTML(n) {
    n = Math.max(1, Math.min(20, Math.round(Number(n) || 1)));
    if (quizCardCache.has(n)) {
      return quizCardCache.get(n);
    }
    if (typeof document === 'undefined') {
      const fallback = `<div class="w-14 h-14 sm:w-16 sm:h-16 mx-auto flex items-center justify-center font-black text-3xl text-rose-500">${n}</div>`;
      quizCardCache.set(n, fallback);
      return fallback;
    }
    try {
      const offscreen = document.createElement('canvas');
      renderDockIcon(offscreen, n, true, 144);
      const dataUrl = offscreen.toDataURL('image/png');
      const html = `<img src="${dataUrl}" alt="Numberblock ${n}" class="w-14 h-14 sm:w-16 sm:h-16 mx-auto drop-shadow-sm pointer-events-none object-contain" width="144" height="144">`;
      quizCardCache.set(n, html);
      return html;
    } catch (err) {
      const fallback = `<div class="w-14 h-14 sm:w-16 sm:h-16 mx-auto flex items-center justify-center font-black text-3xl text-rose-500">${n}</div>`;
      quizCardCache.set(n, fallback);
      return fallback;
    }
  }

  // --------------------------------------------------------------------------
  // Main Frame Rendering Pass (60fps)
  // --------------------------------------------------------------------------
  function renderFrame(renderState, dtOrNow) {
    if (!ctx2d || !canvas) return;
    const nowMs = performance.now();
    let dt = 0.016;
    if (typeof dtOrNow === 'number') {
      if (dtOrNow < 10) {
        dt = clamp(dtOrNow, 0.001, 0.05);
      } else {
        dt = clamp((dtOrNow - lastTimeMs) / 1000, 0.001, 0.05);
        lastTimeMs = dtOrNow;
      }
    } else {
      dt = clamp((nowMs - lastTimeMs) / 1000, 0.001, 0.05);
      lastTimeMs = nowMs;
    }

    const metrics = (renderState && renderState.metrics) ? renderState.metrics : cachedMetrics;
    const dpr = metrics.dpr || 1;
    const w = metrics.width;
    const h = metrics.height;

    ctx2d.save();
    ctx2d.scale(dpr, dpr);
    ctx2d.clearRect(0, 0, w, h);

    // 1. Sunlit Parallax Sky Gradient (cached)
    rebuildBackgroundGradients(metrics.groundY, h);
    ctx2d.fillStyle = cachedSkyGrad || '#e0f2fe';
    ctx2d.fillRect(0, 0, w, h);

    // 2. Pill Clouds
    updateAndDrawClouds(ctx2d, w, h, dt);

    // 3. Rolling Pastel Hills
    ctx2d.beginPath();
    ctx2d.moveTo(0, metrics.groundY - 30);
    ctx2d.quadraticCurveTo(w * 0.35, metrics.groundY - 110, w * 0.70, metrics.groundY - 45);
    ctx2d.quadraticCurveTo(w * 0.88, metrics.groundY - 15, w, metrics.groundY - 35);
    ctx2d.lineTo(w, metrics.groundY);
    ctx2d.lineTo(0, metrics.groundY);
    ctx2d.closePath();
    ctx2d.fillStyle = '#bbf7d0';
    ctx2d.fill();

    ctx2d.beginPath();
    ctx2d.moveTo(0, metrics.groundY - 10);
    ctx2d.quadraticCurveTo(w * 0.25, metrics.groundY - 70, w * 0.55, metrics.groundY - 20);
    ctx2d.quadraticCurveTo(w * 0.78, metrics.groundY - 80, w, metrics.groundY - 15);
    ctx2d.lineTo(w, metrics.groundY);
    ctx2d.lineTo(0, metrics.groundY);
    ctx2d.closePath();
    ctx2d.fillStyle = '#86efac';
    ctx2d.fill();

    // 4. Play Floor & Turf Strip (cached)
    ctx2d.fillStyle = cachedTurfGrad || '#4ade80';
    ctx2d.fillRect(0, metrics.groundY, w, h - metrics.groundY);

    ctx2d.fillStyle = '#bef264';
    ctx2d.fillRect(0, metrics.groundY - 3, w, 3);

    // 5. Onboarding Arc (if active)
    if (renderState && renderState.onboardingArc) {
      drawOnboardingArc(ctx2d, renderState.onboardingArc);
    }

    // 6. Ground Contact Shadows
    const entities = (renderState && renderState.entities) ? renderState.entities : [];
    for (let i = 0; i < entities.length; i++) {
      const ent = entities[i];
      if (ent.state === 'POOFING_OUT' && (ent.poofProgress || 0) >= 0.95) continue;
      const b = getEntityBounds(ent, metrics);
      if (!b) continue;

      const distOffGround = Math.max(0, metrics.groundY - ent.y);
      const liftFactor = clamp(1.0 - distOffGround / 280, 0.25, 1.0);
      const rx = b.width * 0.48 * clamp(1.0 - distOffGround / 320, 0.32, 1.0);
      const ry = clamp(metrics.unitSize * 0.13, 5, 10) * liftFactor;

      ctx2d.beginPath();
      ctx2d.ellipse(ent.x, metrics.groundY, rx, ry, 0, 0, Math.PI * 2);
      ctx2d.fillStyle = 'rgba(15, 55, 30, ' + (0.22 * liftFactor) + ')';
      ctx2d.fill();
    }

    // 7. Snap Preview Aura & Ghost
    if (renderState && renderState.snapPreview) {
      drawSnapPreview(ctx2d, renderState.snapPreview, metrics);
    }

    // 8. Entities Sorted by zOrder (preallocated buffer)
    sortedEntitiesBuf.length = entities.length;
    for (let i = 0; i < entities.length; i++) {
      sortedEntitiesBuf[i] = entities[i];
    }
    sortedEntitiesBuf.sort(function (a, b) {
      return (a.zOrder || 0) - (b.zOrder || 0);
    });

    for (let i = 0; i < sortedEntitiesBuf.length; i++) {
      const ent = sortedEntitiesBuf[i];
      const char = getCharacter(ent.n);
      if (!char) continue;

      const u = (char.unitScale || 1.0) * metrics.unitSize;
      const legH = getLegHeight(u);
      const headgearH = getHeadgearHeight(char.n, u);
      const poofP = ent.poofProgress || 0;
      const poofScale = 1.0 - poofP;
      const poofAlpha = clamp(1.0 - poofP, 0, 1);

      ctx2d.save();
      ctx2d.translate(ent.x, ent.y);
      ctx2d.rotate(ent.tilt || 0);
      ctx2d.scale((ent.scaleX || 1.0) * poofScale, (ent.scaleY || 1.0) * poofScale);
      ctx2d.globalAlpha = poofAlpha;

      // Golden Pulsing Hint Ring (layered translucent halo instead of shadowBlur)
      if (ent.hintGlow) {
        const ringPulse = 1.0 + Math.sin(nowMs * 0.008) * 0.08;
        const totalW = char.cols * u * ringPulse;
        const totalH = (char.rows * u + legH + headgearH) * ringPulse;
        drawRoundRect(ctx2d, -totalW / 2 - 6, -totalH - 6, totalW + 12, totalH + 12, 14);
        ctx2d.lineWidth = 9;
        ctx2d.strokeStyle = 'rgba(250, 204, 21, 0.35)';
        ctx2d.stroke();
        ctx2d.lineWidth = 3.5;
        ctx2d.strokeStyle = '#facc15';
        ctx2d.stroke();
      }

      // Morphing vs Standard Block Drawing
      if (ent.state === 'MORPHING' && ent.morphInfo) {
        const mInfo = ent.morphInfo;
        const p = mInfo.progress || 0;
        const cubes = mInfo.cubes || [];

        if (mInfo.phase === 'reveal') {
          const revPop = mInfo.revealPop !== undefined ? mInfo.revealPop : 1.0;
          const revAlpha = clamp(mInfo.revealAlpha !== undefined ? mInfo.revealAlpha : 1.0, 0, 1);
          const pivotY = -legH - (char.rows * u) * 0.5;
          const totalW = char.cols * u;
          const startX = -totalW / 2;

          ctx2d.save();
          ctx2d.translate(0, pivotY);
          ctx2d.scale(revPop, revPop);
          ctx2d.translate(0, -pivotY);

          ctx2d.globalAlpha = poofAlpha * revAlpha;
          drawCharacterLimbsBack(ctx2d, ent, char, u, nowMs, false);

          ctx2d.globalAlpha = poofAlpha;
          for (let cIdx = 0; cIdx < char.cells.length; cIdx++) {
            const c = char.cells[cIdx];
            const cx = startX + c.col * u;
            const cy = -legH - (c.row + 1) * u;
            drawUnitBlock(ctx2d, cx, cy, u, c.palette, 0);
            if (revAlpha > 0.02) {
              ctx2d.globalAlpha = poofAlpha * revAlpha;
              drawCellDecoration(ctx2d, c, cx, cy, u);
              ctx2d.globalAlpha = poofAlpha;
            }
          }

          ctx2d.globalAlpha = poofAlpha * revAlpha;
          drawCharacterLimbsFront(ctx2d, ent, char, u, nowMs, false);
          drawCharacterFaceAndProps(ctx2d, ent, char, u, metrics, nowMs, false);
          drawNumberling(ctx2d, ent, char, u, nowMs);
          ctx2d.restore();
        } else {
          for (let cIdx = 0; cIdx < cubes.length; cIdx++) {
            const cube = cubes[cIdx];
            const curX = (1 - p) * cube.fromX + p * cube.toX + 4 * p * (1 - p) * (cube.arcX || 0);
            const curY = (1 - p) * cube.fromY + p * cube.toY + 4 * p * (1 - p) * (cube.arcY || 0);
            const curSize = (1 - p) * cube.fromSize + p * cube.toSize;
            const curPal = lerpPalette(cube.fromPalette, cube.toPalette, p);
            const isLit = (mInfo.litCount || 0) > cIdx;
            const isActiveStep = (mInfo.phase === 'cubes' && mInfo.activeStepIndex === cIdx);
            const flashA = isActiveStep ? 0.85 : (isLit ? 0.55 : 0);

            // Align morph cubes smoothly to lifted block stack (-legH)
            const localX = curX - ent.x;
            const localY = curY - ent.y - getLegHeight(curSize);
            if (isActiveStep) {
              const cMidX = localX + curSize * 0.5;
              const cMidY = localY + curSize * 0.5;
              ctx2d.save();
              ctx2d.translate(cMidX, cMidY);
              ctx2d.scale(1.06, 1.06);
              drawUnitBlock(ctx2d, -curSize * 0.5, -curSize * 0.5, curSize, curPal, flashA);
              ctx2d.restore();
            } else {
              drawUnitBlock(ctx2d, localX, localY, curSize, curPal, flashA);
            }
          }
        }
      } else {
        // 1. Limbs BEHIND Block Grid
        drawCharacterLimbsBack(ctx2d, ent, char, u, nowMs, false);

        // 2. Flush Snap-Together Character Blocks + Pips/Buttons
        const totalW = char.cols * u;
        const startX = -totalW / 2;

        for (let cIdx = 0; cIdx < char.cells.length; cIdx++) {
          const c = char.cells[cIdx];
          const cx = startX + c.col * u;
          const cy = -legH - (c.row + 1) * u;
          drawUnitBlock(ctx2d, cx, cy, u, c.palette, 0);
          drawCellDecoration(ctx2d, c, cx, cy, u);
        }

        // 3. Front Limbs (5's High-Five hand), Face/Props & Numberling
        drawCharacterLimbsFront(ctx2d, ent, char, u, nowMs, false);
        drawCharacterFaceAndProps(ctx2d, ent, char, u, metrics, nowMs, false);
        drawNumberling(ctx2d, ent, char, u, nowMs);
      }

      ctx2d.restore();

      // Elastic Taffy Tether (if in STRETCH_SPLIT)
      if (ent.stretchInfo) {
        drawTaffyStretch(ctx2d, ent.stretchInfo, metrics);
      }

      // Contextual Split Badge
      if (ent.n >= 2 && ent.splitBadgeAlpha && ent.splitBadgeAlpha > 0.01) {
        const badgeRect = getSplitBadgeRect(ent, metrics);
        drawSplitBadge(ctx2d, badgeRect, ent.splitBadgeAlpha);
      }
    }

    // 9. 120-Slot Pooled Particle Engine Update & Draw
    updateAndDrawParticles(ctx2d, dt);

    // 10. Floating Equation Pill
    if (renderState && renderState.equationPill) {
      drawEquationPill(ctx2d, renderState.equationPill, metrics);
    }

    ctx2d.restore();
  }

  // --------------------------------------------------------------------------
  // Initialization & Module Export
  // --------------------------------------------------------------------------
  function init(canvasEl, hudOverlayEl) {
    canvas = canvasEl;
    hudOverlay = hudOverlayEl;
    quizCardCache.clear();
    if (canvas) {
      ctx2d = canvas.getContext('2d');
    }
    resize();

    return {
      resize: resize,
      getMetrics: getMetrics,
      getLayoutMetrics: getMetrics
    };
  }

  // Export NB.Renderer
  NB.Renderer = {
    init: init,
    resize: resize,
    getMetrics: getMetrics,
    getLayoutMetrics: getMetrics,
    getEntityBounds: getEntityBounds,
    getSplitBadgeRect: getSplitBadgeRect,
    renderFrame: renderFrame,
    spawnBurst: spawnBurst,
    renderDockIcon: renderDockIcon,
    getQuizCardHTML: getQuizCardHTML,
    lerpPalette: lerpPalette
  };

})();

    </script>
    <script>
(function () {
  'use strict';

  const NB = (window.NumberBlocks = window.NumberBlocks || {});

  // ---------------------------------------------------------------------------
  // CONSTANTS & CONFIGURATION
  // ---------------------------------------------------------------------------
  const STORAGE_KEYS = {
    unlocked: 'tlh_isolated_v3_nb_unlocked',
    stars: 'tlh_isolated_v3_nb_stars'
  };

  const DEFAULT_UNLOCKED = [1, 2, 3, 4, 5];
  const MAX_STAGE_ACTORS = 8;

  // Spring & Physics Constants (Harmonized with Visual Tech Lead Spec)
  const GRAVITY = 1650;          // px/s^2
  const DRAG_STIFFNESS = 420;    // spring stiffness for drag follow
  const DRAG_DAMPING = 28;       // spring damping for drag follow
  const TILT_STIFFNESS = 260;    // spring stiffness for velocity tilt
  const TILT_DAMPING = 22;       // spring damping for velocity tilt
  const SQUASH_STIFFNESS = 380;  // spring stiffness for landing squash recovery
  const SQUASH_DAMPING = 28;     // near-critically damped squash recovery (eliminates jelly wobble)

  // Fallback split bonds for 1..10 in case NB.Data is loading asynchronously
  const FALLBACK_BONDS = {
    2: [[1, 1]],
    3: [[2, 1]],
    4: [[2, 2], [3, 1]],
    5: [[3, 2], [4, 1]],
    6: [[3, 3], [4, 2], [5, 1]],
    7: [[4, 3], [5, 2], [6, 1]],
    8: [[4, 4], [5, 3], [6, 2], [7, 1]],
    9: [[6, 3], [5, 4], [7, 2], [8, 1]],
    10: [[5, 5], [6, 4], [7, 3], [8, 2], [9, 1]]
  };

  // Fallback 12 progressive challenges matching #12 §3.2
  const FALLBACK_CHALLENGES = [
    { id: 1, type: 'merge', target: 2, splitParts: null, maxRequired: 2, spawn: [1, 1], prompt: 'Put One and One together! Make Two!', hintText: 'Drag One onto One to make Two!' },
    { id: 2, type: 'merge', target: 3, splitParts: null, maxRequired: 3, spawn: [2, 1], prompt: 'Can you build Three, the juggler?', hintText: 'Combine Two and One to make Three!' },
    { id: 3, type: 'merge', target: 4, splitParts: null, maxRequired: 4, spawn: [2, 2], prompt: 'Make Square Four! Four green blocks!', hintText: 'Put Two and Two together to make Four!' },
    { id: 4, type: 'merge', target: 5, splitParts: null, maxRequired: 5, spawn: [3, 2], prompt: 'Build Five for a big High Five!', hintText: 'Combine Three and Two to make Five!' },
    { id: 5, type: 'split', target: 4, splitParts: null, maxRequired: 4, spawn: [4], prompt: 'Four wants to share! Split Four apart!', hintText: 'Tap or pull the split badge on Four!' },
    { id: 6, type: 'merge', target: 6, splitParts: null, maxRequired: 6, spawn: [3, 3], prompt: 'Roll the dice! Can you build Six?', hintText: 'Put Three and Three together to make Six!' },
    { id: 7, type: 'merge', target: 7, splitParts: null, maxRequired: 7, spawn: [5, 2], prompt: 'Make Lucky Rainbow Seven!', hintText: 'Add Five and Two together to make Seven!' },
    { id: 8, type: 'split', target: 5, splitParts: [2, 3], maxRequired: 5, spawn: [5], prompt: 'Can you split Five into Two and Three?', hintText: 'Split Five apart into Two and Three!' },
    { id: 9, type: 'merge', target: 8, splitParts: null, maxRequired: 8, spawn: [4, 4], prompt: 'Who has eight wiggly arms? Build Octoblock Eight!', hintText: 'Combine Four and Four to make Eight!' },
    { id: 10, type: 'merge', target: 9, splitParts: null, maxRequired: 9, spawn: [5, 4], prompt: 'Make big Square Nine! Three by three!', hintText: 'Add Five and Four to make Square Nine!' },
    { id: 11, type: 'merge', target: 10, splitParts: null, maxRequired: 10, spawn: [5, 5], prompt: 'Ready for blast off! Build Rocket Ten!', hintText: 'Put Five and Five together to make Rocket Ten!' },
    { id: 12, type: 'merge', target: 15, splitParts: null, maxRequired: 15, spawn: [10, 5], prompt: 'Ten plus Five! Can you build Fifteen?', hintText: 'Combine Ten and Five to make Fifteen!' }
  ];

  // ---------------------------------------------------------------------------
  // MODULE-LEVEL STATE
  // ---------------------------------------------------------------------------
  let initialized = false;
  let isOpen = false;

  let canvasEl = null;
  let stageWrapEl = null;
  let hudOverlayEl = null;
  let dockEl = null;
  let dockFriendsEl = null;

  // HUD Elements
  let modePlayBtn = null;
  let modeChallengeBtn = null;
  let challengeBarEl = null;
  let challengeSpeakBtn = null;
  let challengeIconCanvas = null;
  let challengeTextEl = null;
  let challengeStarsEl = null;
  let challengeHintBtn = null;
  let challengeSkipBtn = null;
  let toolSplitBtn = null;
  let toolUnlockBtn = null;
  let toolResetBtn = null;
  let toolCountBtn = null;
  let lastInteractedEntityId = null;

  let renderer = null;
  let metrics = null;

  let entities = [];
  let nextEntityId = 1;

  let unlockedFriends = [...DEFAULT_UNLOCKED];
  let challengeStars = 0;
  let splitToolActive = false;
  let currentMode = 'play'; // 'play' | 'challenge'
  let activeChallengeIndex = 0;
  let challengeGoalReached = false;
  let challengeIdleTimer = 0;

  let onboardingArc = null;
  let onboardingTimer = 0;

  let snapTarget = null;
  let activeEquationPill = null;

  const splitBondCycleMap = new Map();
  const firstMergeSessionMap = new Set();
  const trackedTimers = new Set();

  let rAFId = null;
  let lastTime = 0;
  let maxCap = 20;

  // Pointer Tracking
  const primaryPointer = {
    id: null,
    type: 'touch',
    startClientX: 0,
    startClientY: 0,
    startX: 0,
    startY: 0,
    currentX: 0,
    currentY: 0,
    grabOffsetX: 0,
    grabOffsetY: 0,
    startTime: 0,
    targetEntityId: null,
    isSplitBadgeHit: false,
    isFromDock: false,
    dockN: 0,
    draggedEntity: null,
    hasMoved: false
  };

  const secondPointer = {
    id: null,
    startX: 0,
    startY: 0,
    currentX: 0,
    currentY: 0,
    targetEntityId: null,
    initialSpread: 0
  };

  // ---------------------------------------------------------------------------
  // SPRING HELPER
  // ---------------------------------------------------------------------------
  function stepSpring(val, vel, target, stiffness, damping, dt) {
    const force = -stiffness * (val - target) - damping * vel;
    vel += force * dt;
    val += vel * dt;
    return [val, vel];
  }

  // ---------------------------------------------------------------------------
  // PERSISTENCE (TRY/CATCH WRAPPED)
  // ---------------------------------------------------------------------------
  function loadUnlocked() {
    try {
      if (typeof window !== 'undefined' && window.localStorage) {
        const raw = window.localStorage.getItem(STORAGE_KEYS.unlocked);
        if (raw) {
          const arr = JSON.parse(raw);
          if (Array.isArray(arr)) {
            const set = new Set([...DEFAULT_UNLOCKED, ...arr.map(Number).filter(n => n >= 1 && n <= 10)]);
            return Array.from(set).sort((a, b) => a - b);
          }
        }
      }
    } catch (e) {
      console.warn('[NB.Game] loadUnlocked error:', e);
    }
    return [...DEFAULT_UNLOCKED];
  }

  function saveUnlocked(arr) {
    try {
      if (typeof window !== 'undefined' && window.localStorage) {
        window.localStorage.setItem(STORAGE_KEYS.unlocked, JSON.stringify(arr));
      }
    } catch (e) {
      console.warn('[NB.Game] saveUnlocked error:', e);
    }
  }

  function isUnlocked(n) {
    return unlockedFriends.indexOf(n) !== -1;
  }

  function unlockFriend(n) {
    if (!isUnlocked(n)) {
      unlockedFriends.push(n);
      unlockedFriends.sort((a, b) => a - b);
      saveUnlocked(unlockedFriends);
    }
  }

  function loadStars() {
    try {
      if (typeof window !== 'undefined' && window.localStorage) {
        const raw = window.localStorage.getItem(STORAGE_KEYS.stars);
        if (raw !== null) {
          const parsed = parseInt(raw, 10);
          return isNaN(parsed) ? 0 : parsed;
        }
      }
    } catch (e) {
      console.warn('[NB.Game] loadStars error:', e);
    }
    return 0;
  }

  function saveStars(count) {
    try {
      if (typeof window !== 'undefined' && window.localStorage) {
        window.localStorage.setItem(STORAGE_KEYS.stars, String(count));
      }
    } catch (e) {
      console.warn('[NB.Game] saveStars error:', e);
    }
  }

  // ---------------------------------------------------------------------------
  // TIMER & ENVIRONMENT GUARDS
  // ---------------------------------------------------------------------------
  function nowMs() {
    if (typeof window !== 'undefined' && window.performance && typeof window.performance.now === 'function') {
      return window.performance.now();
    }
    return Date.now();
  }

  function requestFrame(cb) {
    if (typeof window !== 'undefined' && typeof window.requestAnimationFrame === 'function') {
      return window.requestAnimationFrame(cb);
    }
    return setTimeout(() => cb(nowMs()), 16);
  }

  function cancelFrame(id) {
    if (typeof window !== 'undefined' && typeof window.cancelAnimationFrame === 'function') {
      return window.cancelAnimationFrame(id);
    }
    clearTimeout(id);
  }

  function getTLH() {
    if (typeof window !== 'undefined') {
      return window.ToddlerLearningHub || window.TLH || null;
    }
    return null;
  }

  function isBlocksActive() {
    const tlh = getTLH();
    return isOpen && tlh && tlh.app && tlh.app.currentView === 'blocks';
  }

  function addTimer(fn, delayMs) {
    if (!isOpen) return null;
    const id = setTimeout(() => {
      trackedTimers.delete(id);
      if (isOpen && isBlocksActive()) {
        fn();
      }
    }, delayMs);
    trackedTimers.add(id);
    const tlh = getTLH();
    if (tlh && tlh.soundFX && typeof tlh.soundFX.registerTimer === 'function') {
      try { tlh.soundFX.registerTimer(id); } catch (e) {}
    }
    return id;
  }

  function clearAllTimers() {
    for (const id of trackedTimers) {
      clearTimeout(id);
    }
    trackedTimers.clear();
  }

  function getMaxCap() {
    const tlh = getTLH();
    if (tlh && tlh.app && tlh.app.settings && tlh.app.settings.maxNumber === 10) {
      return 10;
    }
    return 20;
  }

  function getHighestZOrder() {
    let maxZ = 1;
    for (let i = 0; i < entities.length; i++) {
      if (entities[i].zOrder > maxZ) maxZ = entities[i].zOrder;
    }
    return maxZ;
  }

  function findEntity(id) {
    if (id === null || id === undefined) return null;
    for (let i = 0; i < entities.length; i++) {
      if (entities[i].id === id) return entities[i];
    }
    return null;
  }

  function getEntityBounds(entity) {
    if (NB.Renderer && NB.Renderer.getEntityBounds && metrics) {
      return NB.Renderer.getEntityBounds(entity, metrics);
    }
    const char = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(entity.n) : { rows: 1, cols: 1, unitScale: 1.0 };
    const u = (char.unitScale || 1.0) * (metrics ? metrics.unitSize : 48);
    const w = char.cols * u;
    const h = char.rows * u;
    return {
      x: entity.x,
      y: entity.y,
      u: u,
      cols: char.cols,
      rows: char.rows,
      width: w,
      height: h,
      left: entity.x - w / 2,
      right: entity.x + w / 2,
      top: entity.y - h,
      bottom: entity.y,
      centerX: entity.x,
      centerY: entity.y - h / 2
    };
  }

  function getSplitBadgeRect(entity) {
    if (NB.Renderer && NB.Renderer.getSplitBadgeRect && metrics) {
      return NB.Renderer.getSplitBadgeRect(entity, metrics);
    }
    const b = getEntityBounds(entity);
    const topSafe = metrics ? metrics.topSafeY : 20;
    const stageWidth = metrics ? metrics.width : 400;
    return {
      cx: Math.min(stageWidth - 28, b.right + 16),
      cy: Math.max(topSafe + 26, b.top + 8),
      r: 24
    };
  }

  // ---------------------------------------------------------------------------
  // ENTITY MANAGEMENT & RECYCLING
  // ---------------------------------------------------------------------------
  function createEntity(n, x, y, state) {
    state = state || 'IDLE';
    const char = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(n) : { rows: 1, cols: 1, unitScale: 1.0 };
    const u = (char.unitScale || 1.0) * (metrics ? metrics.unitSize : 48);
    const b = getEntityBounds({ n: n, x: x, y: y });
    const boundsHeight = b ? b.height : (char.rows * u);
    const halfWidth = b ? (b.width / 2) : ((char.cols * u) / 2);

    const topSafe = metrics ? metrics.topSafeY : 20;
    const ground = metrics ? metrics.groundY : 350;
    const stageWidth = metrics ? metrics.width : 400;
    const numberlingPad = metrics ? metrics.unitSize * 0.65 : 30;
    const minAllowedY = topSafe + boundsHeight + numberlingPad;

    const clampedY = Math.min(ground, Math.max(minAllowedY, y));
    const clampedX = Math.max(halfWidth + 12, Math.min(stageWidth - halfWidth - 12, x));

    return {
      id: nextEntityId++,
      n: n,
      x: clampedX,
      y: clampedY,
      vx: 0,
      vy: 0,
      scaleX: 1.0,
      scaleY: 1.0,
      scaleYVel: 0,
      tilt: 0,
      tiltVel: 0,
      zOrder: 1,
      state: state,
      tapProgress: 0,
      splitBadgeAlpha: 0,
      splitBadgeTimer: 0,
      poofProgress: 0,
      hintGlow: false,
      lookTarget: null,
      expression: 'happy',
      morphInfo: null,
      stretchInfo: null
    };
  }

  function enforceStageCapacity() {
    const active = entities.filter(e => e.state !== 'POOFING_OUT');
    if (active.length < MAX_STAGE_ACTORS) return;

    // Count occurrences of each number to find duplicates
    const counts = {};
    for (let i = 0; i < active.length; i++) {
      counts[active[i].n] = (counts[active[i].n] || 0) + 1;
    }

    let candidate = null;
    // Prefer oldest IDLE duplicate
    for (let i = 0; i < active.length; i++) {
      const e = active[i];
      if (e.state === 'IDLE' && counts[e.n] > 1) {
        if (!candidate || e.id < candidate.id) {
          candidate = e;
        }
      }
    }

    // Fallback: oldest IDLE entity
    if (!candidate) {
      for (let i = 0; i < active.length; i++) {
        const e = active[i];
        if (e.state === 'IDLE') {
          if (!candidate || e.id < candidate.id) {
            candidate = e;
          }
        }
      }
    }

    if (candidate) {
      candidate.state = 'POOFING_OUT';
      candidate.poofProgress = 0.001;
      const b = getEntityBounds(candidate);
      if (NB.Renderer && NB.Renderer.spawnBurst) {
        NB.Renderer.spawnBurst(candidate.x, candidate.y - b.height / 2, 'poofOut', null);
      }
    }
  }

  // ---------------------------------------------------------------------------
  // DOCK GENERATION & UPDATING
  // ---------------------------------------------------------------------------
  function initDock() {
    if (!dockFriendsEl) return;
    dockFriendsEl.innerHTML = '';

    const isShortLandscape = metrics ? (metrics.height < 500) : false;
    const iconSize = isShortLandscape ? 32 : 40;

    for (let n = 1; n <= 10; n++) {
      const btn = document.createElement('button');
      btn.type = 'button';
      btn.className = 'nb-dock-tile squish-btn';
      btn.dataset.n = String(n);
      if (n === 1) {
        btn.classList.add('is-hero');
      }

      const canvas = document.createElement('canvas');
      canvas.className = 'nb-dock-canvas';
      btn.appendChild(canvas);

      const label = document.createElement('span');
      label.className = 'nb-dock-num';
      btn.appendChild(label);

      dockFriendsEl.appendChild(btn);
    }

    updateDock();
  }

  function updateDock() {
    if (!dockFriendsEl) return;
    const isShortLandscape = metrics ? (metrics.height < 500) : false;
    const iconSize = isShortLandscape ? 32 : 40;
    const dprKey = Math.round(Math.min(window.devicePixelRatio || 1, 3) * 100);

    const tiles = dockFriendsEl.querySelectorAll('.nb-dock-tile');
    tiles.forEach(tile => {
      const n = parseInt(tile.dataset.n, 10);
      const unlocked = isUnlocked(n);
      const canvas = tile.querySelector('.nb-dock-canvas');
      const label = tile.querySelector('.nb-dock-num');

      if (unlocked) {
        tile.classList.remove('is-locked');
        if (label) label.textContent = String(n);
      } else {
        tile.classList.add('is-locked');
        if (label) label.textContent = '?';
      }

      const stateKey = (unlocked ? '1' : '0') + ':' + iconSize + ':' + dprKey;
      if (canvas && NB.Renderer && NB.Renderer.renderDockIcon && tile.dataset.renderKey !== stateKey) {
        NB.Renderer.renderDockIcon(canvas, n, unlocked, iconSize);
        tile.dataset.renderKey = stateKey;
      }
    });
  }

  // ---------------------------------------------------------------------------
  // SPLITTING MECHANICS (CYCLES SPLIT BONDS, E.G. NINE'S 4 BONDS)
  // ---------------------------------------------------------------------------
  function getNextSplitBond(n) {
    const char = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(n) : null;
    const bonds = (char && char.splitBonds && char.splitBonds.length > 0) ? char.splitBonds : FALLBACK_BONDS[n];
    if (!bonds || bonds.length === 0) {
      const half = Math.floor(n / 2);
      return [n - half, Math.max(1, half)];
    }
    const idx = splitBondCycleMap.get(n) || 0;
    const bond = bonds[idx % bonds.length];
    splitBondCycleMap.set(n, (idx + 1) % bonds.length);
    return [bond[0], bond[1]];
  }

  function performSplit(entity, partA, partB) {
    if (!entity) return;
    const parentN = entity.n;
    const parentX = entity.x;
    const parentY = entity.y;
    const bounds = getEntityBounds(entity);
    const boundsHeight = bounds.height;

    // Remove parent
    const pIdx = entities.findIndex(e => e.id === entity.id);
    if (pIdx !== -1) entities.splice(pIdx, 1);

    // Enforce capacity for 2 children
    enforceStageCapacity();
    enforceStageCapacity();

    const stageWidth = metrics ? metrics.width : 400;
    const offset = Math.max(36, (metrics ? metrics.unitSize : 48) * 0.9);
    const clampedXA = Math.max(48, Math.min(stageWidth - 48, parentX - offset));
    const clampedXB = Math.max(48, Math.min(stageWidth - 48, parentX + offset));

    const entityA = createEntity(partA, clampedXA, parentY, 'IDLE');
    entityA.vx = -150;
    entityA.vy = -340;
    entityA.scaleX = 1.15;
    entityA.scaleY = 0.87;
    entityA.zOrder = getHighestZOrder() + 1;

    const entityB = createEntity(partB, clampedXB, parentY, 'IDLE');
    entityB.vx = 150;
    entityB.vy = -340;
    entityB.scaleX = 1.15;
    entityB.scaleY = 0.87;
    entityB.zOrder = getHighestZOrder() + 2;

    entities.push(entityA, entityB);
    lastInteractedEntityId = entityA.id;

    // Visual burst & sound
    if (NB.Renderer && NB.Renderer.spawnBurst) {
      NB.Renderer.spawnBurst(parentX, parentY - boundsHeight / 2, 'splitPop', null);
    }
    if (NB.Audio && isBlocksActive()) {
      if (NB.Audio.playSplitPop) NB.Audio.playSplitPop(partA, partB);
      if (NB.Audio.speakSplit) NB.Audio.speakSplit(parentN, partA, partB);
    }

    // Equation pill
    const topSafe = metrics ? metrics.topSafeY : 20;
    activeEquationPill = {
      x: parentX,
      y: Math.max(topSafe + 24, parentY - boundsHeight - 24),
      mode: 'split',
      leftN: parentN,
      rightN: partA,
      sumN: partB,
      alpha: 1.0,
      scale: 1.0,
      timer: 1.6
    };

    // Challenge check
    checkChallengeGoal('split', { whole: parentN, partA: partA, partB: partB });
  }

  // ---------------------------------------------------------------------------
  // 4-BEAT MERGE & SUPERNOVA BOUNCE
  // ---------------------------------------------------------------------------
  function performMerge(entityA, entityB) {
    const sum = entityA.n + entityB.n;
    const targetX = entityB.x;
    const ground = metrics ? metrics.groundY : 350;

    // Remove source entities
    const idxA = entities.findIndex(e => e.id === entityA.id);
    if (idxA !== -1) entities.splice(idxA, 1);
    const idxB = entities.findIndex(e => e.id === entityB.id);
    if (idxB !== -1) entities.splice(idxB, 1);

    // Create resulting entity in MORPHING state
    const entityC = createEntity(sum, targetX, ground, 'MORPHING');
    entityC.zOrder = getHighestZOrder() + 10;

    const charA = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(entityA.n) : { cells: [], unitScale: 1.0 };
    const charB = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(entityB.n) : { cells: [], unitScale: 1.0 };
    const charC = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(sum) : { cells: [], unitScale: 1.0 };

    const u = metrics ? metrics.unitSize : 48;
    const uA = (charA.unitScale || 1.0) * u;
    const uB = (charB.unitScale || 1.0) * u;
    const uC = (charC.unitScale || 1.0) * u;

    const boundsA = getEntityBounds(entityA);
    const boundsB = getEntityBounds(entityB);
    const boundsC = getEntityBounds(entityC);

    const sourceCells = [];
    if (charA.cells) {
      charA.cells.forEach(cell => {
        sourceCells.push({
          x: boundsA.left + cell.col * uA,
          y: boundsA.bottom - (cell.row + 1) * uA,
          size: uA,
          palette: cell.palette
        });
      });
    }
    if (charB.cells) {
      charB.cells.forEach(cell => {
        sourceCells.push({
          x: boundsB.left + cell.col * uB,
          y: boundsB.bottom - (cell.row + 1) * uB,
          size: uB,
          palette: cell.palette
        });
      });
    }

    const cubes = [];
    if (charC.cells && charC.cells.length > 0) {
      charC.cells.forEach((cell, idx) => {
        const toX = boundsC.left + cell.col * uC;
        const toY = boundsC.bottom - (cell.row + 1) * uC;
        const src = sourceCells[idx] || sourceCells[sourceCells.length - 1] || { x: boundsC.centerX, y: boundsC.centerY, size: uC, palette: cell.palette };
        cubes.push({
          fromX: src.x,
          fromY: src.y,
          fromSize: src.size,
          toX: toX,
          toY: toY,
          toSize: uC,
          fromPalette: src.palette,
          toPalette: cell.palette,
          arcX: (Math.random() - 0.5) * 28,
          arcY: -14 - Math.random() * 12
        });
      });
    }

    const stepMs = (NB.Data && NB.Data.getAdaptiveStepMs) ? NB.Data.getAdaptiveStepMs(sum) : 70;
    const phase1Duration = 130;
    const phase2Duration = sum * stepMs;
    const phase3Duration = 180;
    const phase4Duration = 220;

    entityC.morphInfo = {
      startTime: nowMs(),
      phase: 'dock',
      progress: 0,
      litCount: 0,
      activeStepIndex: -1,
      revealAlpha: 0,
      revealPop: 0.86,
      revealScale: 0.86,
      cubes: cubes,
      stepMs: stepMs,
      p1End: phase1Duration,
      p2End: phase1Duration + phase2Duration,
      p3End: phase1Duration + phase2Duration + phase3Duration,
      totalDuration: phase1Duration + phase2Duration + phase3Duration + phase4Duration,
      sum: sum,
      sourceA: entityA.n,
      sourceB: entityB.n,
      starburstTriggered: false
    };

    entities.push(entityC);
    lastInteractedEntityId = entityC.id;

    const topSafe = metrics ? metrics.topSafeY : 20;
    activeEquationPill = {
      x: targetX,
      y: Math.max(topSafe + 24, boundsC.top - 28),
      mode: 'merge',
      leftN: entityA.n,
      rightN: entityB.n,
      sumN: sum,
      alpha: 1.0,
      scale: 1.0,
      timer: (entityC.morphInfo.totalDuration / 1000) + 1.2
    };

    snapTarget = null;
  }

  function performSupernovaBounce(entityA, entityB) {
    const midX = (entityA.x + entityB.x) / 2;
    const midY = (entityA.y + entityB.y) / 2 - 40;

    if (NB.Renderer && NB.Renderer.spawnBurst) {
      NB.Renderer.spawnBurst(midX, midY, 'highFive', null);
    }
    const tlh = getTLH();
    if (tlh && tlh.app && tlh.app.burstConfetti && isBlocksActive() && tlh.app.settings && tlh.app.settings.confettiEnabled !== false) {
      tlh.app.burstConfetti(midX, midY);
    }
    if (NB.Audio && isBlocksActive()) {
      if (NB.Audio.playHighFiveBounce) NB.Audio.playHighFiveBounce();
      if (maxCap === 10) {
        NB.Audio.speak("Whoa, bigger than Ten! Fireworks!", 'high');
      } else {
        NB.Audio.speak("Whoa, super big number! Twenty is our biggest rocket!", 'high');
      }
    }

    entityA.state = 'IDLE';
    entityA.vx = -160;
    entityA.vy = -360;
    entityA.scaleX = 1.18;
    entityA.scaleY = 0.82;
    entityA.expression = 'happy';

    entityB.state = 'IDLE';
    entityB.vx = 160;
    entityB.vy = -360;
    entityB.scaleX = 1.18;
    entityB.scaleY = 0.82;
    entityB.expression = 'happy';

    const topSafe = metrics ? metrics.topSafeY : 20;
    activeEquationPill = {
      x: midX,
      y: Math.max(topSafe + 24, midY - 30),
      mode: 'boom',
      leftN: entityA.n,
      rightN: entityB.n,
      sumN: entityA.n + entityB.n,
      alpha: 1.0,
      scale: 1.0,
      timer: 1.5
    };

    snapTarget = null;
  }

  // ---------------------------------------------------------------------------
  // CHALLENGES CONTROLLER
  // ---------------------------------------------------------------------------
  function getAvailableChallenges() {
    const pool = (NB.Data && NB.Data.CHALLENGES && NB.Data.CHALLENGES.length > 0) ? NB.Data.CHALLENGES : FALLBACK_CHALLENGES;
    return pool.filter(c => c.maxRequired <= maxCap);
  }

  function getCurrentChallenge() {
    const list = getAvailableChallenges();
    if (list.length === 0) return null;
    return list[activeChallengeIndex % list.length];
  }

  function loadChallenge(challenge) {
    if (!challenge) return;
    challengeGoalReached = false;
    challengeIdleTimer = 8.0;

    // Clear stage entities
    entities = [];

    // Spawn required blocks spaced nicely across floor
    const count = challenge.spawn.length;
    const stageWidth = metrics ? metrics.width : 400;
    const ground = metrics ? metrics.groundY : 350;

    challenge.spawn.forEach((n, idx) => {
      const posX = stageWidth * ((idx + 1) / (count + 1));
      const ent = createEntity(n, posX, ground, 'IDLE');
      ent.vy = -380;
      entities.push(ent);
    });

    updateChallengeUI();

    if (NB.Audio && NB.Audio.speak && isBlocksActive()) {
      NB.Audio.speak(challenge.prompt, 'high');
    }
  }

  function updateChallengeUI() {
    const challenge = getCurrentChallenge();
    if (!challenge) return;

    if (challengeTextEl) {
      challengeTextEl.textContent = challenge.prompt;
    }
    if (challengeStarsEl) {
      challengeStarsEl.textContent = '⭐ ' + challengeStars;
    }
    if (challengeIconCanvas && NB.Renderer && NB.Renderer.renderDockIcon) {
      NB.Renderer.renderDockIcon(challengeIconCanvas, challenge.target, true, 40);
    }
  }

  function triggerChallengeHint() {
    const challenge = getCurrentChallenge();
    if (!challenge) return;

    if (NB.Audio && NB.Audio.speak && isBlocksActive()) {
      NB.Audio.speak(challenge.hintText, 'high');
    }

    if (challenge.type === 'merge') {
      entities.forEach(e => {
        if (challenge.spawn.indexOf(e.n) !== -1 || e.n === challenge.target) {
          e.hintGlow = true;
        }
      });
    } else if (challenge.type === 'split') {
      entities.forEach(e => {
        if (e.n === challenge.target) {
          e.hintGlow = true;
          e.splitBadgeAlpha = 1.0;
          e.splitBadgeTimer = 5.0;
        }
      });
    }

    // Also highlight relevant dock tile
    if (dockFriendsEl) {
      const tiles = dockFriendsEl.querySelectorAll('.nb-dock-tile');
      tiles.forEach(tile => {
        const n = parseInt(tile.dataset.n, 10);
        if (challenge.spawn.indexOf(n) !== -1 || n === challenge.target) {
          tile.classList.add('is-hint');
          addTimer(() => { tile.classList.remove('is-hint'); }, 4000);
        }
      });
    }
  }

  function checkChallengeGoal(actionType, data) {
    if (currentMode !== 'challenge' || challengeGoalReached) return;
    const challenge = getCurrentChallenge();
    if (!challenge) return;

    let matched = false;
    if (challenge.type === 'merge' && actionType === 'merge') {
      if (data.target === challenge.target) {
        matched = true;
      }
    } else if (challenge.type === 'split' && actionType === 'split') {
      if (data.whole === challenge.target) {
        if (!challenge.splitParts) {
          matched = true;
        } else if (Array.isArray(challenge.splitParts) && challenge.splitParts.length === 2) {
          const p1 = challenge.splitParts[0];
          const p2 = challenge.splitParts[1];
          if ((data.partA === p1 && data.partB === p2) || (data.partA === p2 && data.partB === p1)) {
            matched = true;
          }
        }
      }
    }

    if (matched) {
      challengeGoalReached = true;
      challengeStars++;
      saveStars(challengeStars);
      updateChallengeUI();

      if (NB.Audio && isBlocksActive()) {
        if (NB.Audio.playChallengeWin) NB.Audio.playChallengeWin();
        if (NB.Audio.speak) NB.Audio.speak('Yay! You did it!', 'high');
      }
      const tlh = getTLH();
      if (tlh && tlh.app && tlh.app.burstConfetti && isBlocksActive() && metrics) {
        tlh.app.burstConfetti(metrics.width / 2, metrics.height / 3);
      }

      addTimer(() => {
        advanceChallenge();
      }, 2300);
    }
  }

  function advanceChallenge() {
    const list = getAvailableChallenges();
    if (list.length === 0) return;
    activeChallengeIndex = (activeChallengeIndex + 1) % list.length;
    loadChallenge(list[activeChallengeIndex]);
  }

  function switchMode(newMode) {
    if (currentMode === newMode) return;
    currentMode = newMode;

    if (modePlayBtn) {
      modePlayBtn.classList.toggle('active', currentMode === 'play');
    }
    if (modeChallengeBtn) {
      modeChallengeBtn.classList.toggle('active', currentMode === 'challenge');
    }

    if (challengeBarEl) {
      challengeBarEl.classList.toggle('hidden', currentMode !== 'challenge');
    }

    if (currentMode === 'challenge') {
      const challenge = getCurrentChallenge();
      loadChallenge(challenge);
    } else {
      // Return to Free Play: reset stage if empty
      if (entities.length === 0) {
        spawnStarterFriends();
      }
    }
  }

  function spawnStarterFriends() {
    if (!metrics) return;
    entities = [];
    const one = createEntity(1, metrics.width * 0.38, metrics.groundY, 'IDLE');
    const two = createEntity(2, metrics.width * 0.62, metrics.groundY, 'IDLE');
    entities.push(one, two);

    onboardingArc = {
      fromX: one.x,
      fromY: metrics.groundY - 30,
      toX: two.x,
      toY: metrics.groundY - 30,
      alpha: 1.0,
      phase: 0.0
    };
    onboardingTimer = 3.0;
  }

  // ---------------------------------------------------------------------------
  // POINTER EVENT HANDLERS (SEAMLESS DOCK-TO-STAGE DRAG & ZERO-ACCIDENT GESTURES)
  // ---------------------------------------------------------------------------
  function getCanvasCoords(clientX, clientY) {
    if (!canvasEl) return { x: 0, y: 0 };
    const rect = canvasEl.getBoundingClientRect();
    return {
      x: clientX - rect.left,
      y: clientY - rect.top
    };
  }

  function findSnapTarget(draggedEnt, atX, atY) {
    if (!draggedEnt) return null;
    const bDragged = getEntityBounds(draggedEnt);
    const dragCenterX = (atX !== undefined) ? atX : bDragged.centerX;
    const dragCenterY = (atY !== undefined) ? atY : bDragged.centerY;

    let closest = null;
    let minEdgeDist = Infinity;
    const u = metrics ? metrics.unitSize : 48;
    const snapEnterDist = Math.max(68, 1.35 * u);

    for (let i = 0; i < entities.length; i++) {
      const other = entities[i];
      if (other.id === draggedEnt.id || other.state !== 'IDLE') continue;
      const bOther = getEntityBounds(other);
      const edgeDist = Math.max(0, Math.hypot(dragCenterX - bOther.centerX, dragCenterY - bOther.centerY) - (bDragged.width + bOther.width) / 2);
      if (edgeDist < minEdgeDist && edgeDist <= snapEnterDist) {
        minEdgeDist = edgeDist;
        closest = other;
      }
    }
    return closest;
  }

  function onDockPointerDown(e) {
    const tile = e.target.closest('.nb-dock-tile');
    if (!tile) return;
    const n = parseInt(tile.dataset.n, 10);
    if (isNaN(n)) return;

    if (NB.Audio && NB.Audio.unlock) {
      NB.Audio.unlock();
    }

    if (!isUnlocked(n)) {
      tile.classList.add('is-wiggling');
      addTimer(() => { tile.classList.remove('is-wiggling'); }, 400);
      if (NB.Audio && isBlocksActive()) {
        if (NB.Audio.playLockedClueChime) NB.Audio.playLockedClueChime();
        const char = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(n) : null;
        if (char && char.lockedHint && NB.Audio.speak) {
          NB.Audio.speak(char.lockedHint, 'high');
        }
      }
      return;
    }

    // Unlocked tile: initiate potential continuous dock-to-stage drag
    const coords = getCanvasCoords(e.clientX, e.clientY);
    primaryPointer.id = e.pointerId;
    primaryPointer.type = e.pointerType || 'touch';
    primaryPointer.startClientX = e.clientX;
    primaryPointer.startClientY = e.clientY;
    primaryPointer.startX = coords.x;
    primaryPointer.startY = coords.y;
    primaryPointer.currentX = coords.x;
    primaryPointer.currentY = coords.y;
    primaryPointer.grabOffsetX = 0;
    primaryPointer.grabOffsetY = 0;
    primaryPointer.startTime = nowMs();
    primaryPointer.isFromDock = true;
    primaryPointer.dockN = n;
    primaryPointer.draggedEntity = null;
    primaryPointer.hasMoved = false;
    primaryPointer.isSplitBadgeHit = false;
    primaryPointer.targetEntityId = null;

    try {
      tile.setPointerCapture(e.pointerId);
    } catch (err) {}
  }

  function onCanvasPointerDown(e) {
    if (NB.Audio && NB.Audio.unlock) {
      NB.Audio.unlock();
    }

    const coords = getCanvasCoords(e.clientX, e.clientY);
    const px = coords.x;
    const py = coords.y;

    if (primaryPointer.id === null) {
      // 1. Check Split Badge hit first (only for n >= 2 with splitBadgeAlpha > 0.1)
      for (let i = entities.length - 1; i >= 0; i--) {
        const ent = entities[i];
        if (ent.n >= 2 && ent.splitBadgeAlpha > 0.1) {
          const badge = getSplitBadgeRect(ent);
          const dist = Math.hypot(px - badge.cx, py - badge.cy);
          if (dist <= badge.r + 14) {
            primaryPointer.id = e.pointerId;
            primaryPointer.type = e.pointerType || 'touch';
            primaryPointer.startClientX = e.clientX;
            primaryPointer.startClientY = e.clientY;
            primaryPointer.startX = px;
            primaryPointer.startY = py;
            primaryPointer.currentX = px;
            primaryPointer.currentY = py;
            primaryPointer.grabOffsetX = 0;
            primaryPointer.grabOffsetY = 0;
            primaryPointer.startTime = nowMs();
            primaryPointer.targetEntityId = ent.id;
            lastInteractedEntityId = ent.id;
            primaryPointer.isSplitBadgeHit = true;
            primaryPointer.isFromDock = false;
            primaryPointer.hasMoved = false;
            primaryPointer.draggedEntity = null;
            try { canvasEl.setPointerCapture(e.pointerId); } catch (err) {}
            return;
          }
        }
      }

      // 2. Check Entity Body hit (with +22px padding and min 76x76 hit target)
      // Sort entities descending by zOrder
      const sorted = [...entities].sort((a, b) => b.zOrder - a.zOrder);
      for (let i = 0; i < sorted.length; i++) {
        const ent = sorted[i];
        if (ent.state === 'POOFING_OUT' || ent.state === 'MORPHING') continue;
        const b = getEntityBounds(ent);
        const halo = 22;
        const minHalf = 38;
        const left = Math.min(b.left - halo, b.centerX - minHalf);
        const right = Math.max(b.right + halo, b.centerX + minHalf);
        const top = Math.min(b.top - halo, b.centerY - minHalf);
        const bottom = Math.max(b.bottom + halo, b.centerY + minHalf);

        if (px >= left && px <= right && py >= top && py <= bottom) {
          primaryPointer.id = e.pointerId;
          primaryPointer.type = e.pointerType || 'touch';
          primaryPointer.startClientX = e.clientX;
          primaryPointer.startClientY = e.clientY;
          primaryPointer.startX = px;
          primaryPointer.startY = py;
          primaryPointer.currentX = px;
          primaryPointer.currentY = py;
          primaryPointer.grabOffsetX = ent.x - px;
          primaryPointer.grabOffsetY = ent.y - py;
          primaryPointer.startTime = nowMs();
          primaryPointer.targetEntityId = ent.id;
          lastInteractedEntityId = ent.id;
          primaryPointer.isSplitBadgeHit = false;
          primaryPointer.isFromDock = false;
          primaryPointer.hasMoved = false;
          primaryPointer.draggedEntity = null;
          try { canvasEl.setPointerCapture(e.pointerId); } catch (err) {}
          return;
        }
      }
    } else if (secondPointer.id === null && e.pointerId !== primaryPointer.id) {
      // Secondary pointer for 2-finger pinch/spread split
      if (primaryPointer.targetEntityId !== null) {
        const ent = findEntity(primaryPointer.targetEntityId);
        if (ent && ent.n >= 2) {
          secondPointer.id = e.pointerId;
          secondPointer.startX = px;
          secondPointer.startY = py;
          secondPointer.currentX = px;
          secondPointer.currentY = py;
          secondPointer.targetEntityId = ent.id;
          secondPointer.initialSpread = Math.hypot(px - primaryPointer.currentX, py - primaryPointer.currentY);
        }
      }
    }
  }

  function onWindowPointerMove(e) {
    // Secondary pointer spread tracking
    if (secondPointer.id === e.pointerId) {
      const coords = getCanvasCoords(e.clientX, e.clientY);
      secondPointer.currentX = coords.x;
      secondPointer.currentY = coords.y;

      const ent = findEntity(secondPointer.targetEntityId);
      if (ent && ent.n >= 2) {
        const currentSpread = Math.hypot(secondPointer.currentX - primaryPointer.currentX, secondPointer.currentY - primaryPointer.currentY);
        if (currentSpread - secondPointer.initialSpread >= 40) {
          // Intentional 2-finger spread split!
          secondPointer.id = null;
          primaryPointer.id = null;
          const [pA, pB] = getNextSplitBond(ent.n);
          performSplit(ent, pA, pB);
          return;
        }
      }
    }

    if (primaryPointer.id !== e.pointerId) return;

    // Handle Dock Drag Spawn
    if (primaryPointer.isFromDock) {
      const travel = Math.hypot(e.clientX - primaryPointer.startClientX, e.clientY - primaryPointer.startClientY);
      if (travel >= 10 && !primaryPointer.draggedEntity) {
        // Pointer moved >= 10px: spawn block immediately in DRAGGING state right under finger!
        enforceStageCapacity();
        const coords = getCanvasCoords(e.clientX, e.clientY);
        const ground = metrics ? metrics.groundY : 350;
        const tempBounds = getEntityBounds({ n: primaryPointer.dockN, x: coords.x, y: ground });
        const grabOffY = Math.min(32, (tempBounds ? tempBounds.height : 48) * 0.35);
        const ent = createEntity(primaryPointer.dockN, coords.x, Math.min(ground, coords.y + grabOffY), 'DRAGGING');
        ent.zOrder = getHighestZOrder() + 1;
        entities.push(ent);
        primaryPointer.draggedEntity = ent;
        primaryPointer.targetEntityId = ent.id;
        primaryPointer.grabOffsetX = 0;
        primaryPointer.grabOffsetY = grabOffY;
        lastInteractedEntityId = ent.id;
        primaryPointer.hasMoved = true;
        onboardingArc = null;

        if (NB.Audio && NB.Audio.playPickup && isBlocksActive()) {
          NB.Audio.playPickup();
        }
      }
    }

    const coords = getCanvasCoords(e.clientX, e.clientY);
    primaryPointer.currentX = coords.x;
    primaryPointer.currentY = coords.y;

    // Handle Split Badge Stretch
    if (primaryPointer.isSplitBadgeHit) {
      const ent = findEntity(primaryPointer.targetEntityId);
      if (ent && ent.n >= 2) {
        const travel = Math.hypot(coords.x - primaryPointer.startX, coords.y - primaryPointer.startY);
        if (travel >= 12) {
          if (ent.state !== 'STRETCH_SPLIT') {
            ent.state = 'STRETCH_SPLIT';
            const [pA, pB] = getNextSplitBond(ent.n);
            const badge = getSplitBadgeRect(ent);
            ent.stretchInfo = {
              anchorX: badge.cx,
              anchorY: badge.cy,
              pullX: coords.x,
              pullY: coords.y,
              ratio: 0,
              partA: pA,
              partB: pB
            };
            if (NB.Audio && NB.Audio.playSplitReady && isBlocksActive()) {
              NB.Audio.playSplitReady();
            }
          }

          if (ent.stretchInfo) {
            const pullDist = Math.hypot(coords.x - ent.stretchInfo.anchorX, coords.y - ent.stretchInfo.anchorY);
            ent.stretchInfo.pullX = coords.x;
            ent.stretchInfo.pullY = coords.y;
            ent.stretchInfo.ratio = Math.min(1.0, pullDist / 44);

            const topSafe = metrics ? metrics.topSafeY : 20;
            activeEquationPill = {
              x: ent.x,
              y: Math.max(topSafe + 24, ent.y - (metrics ? metrics.unitSize * 2 : 80)),
              mode: 'split',
              leftN: ent.n,
              rightN: ent.stretchInfo.partA,
              sumN: ent.stretchInfo.partB,
              alpha: 1.0,
              scale: 1.0,
              timer: 0.8
            };

            if (pullDist >= 44) {
              // Pulled past 44px: pops apart!
              const partA = ent.stretchInfo.partA;
              const partB = ent.stretchInfo.partB;
              primaryPointer.id = null;
              performSplit(ent, partA, partB);
              return;
            }
          }
        }
      }
      return;
    }

    // Normal Entity Dragging
    const ent = findEntity(primaryPointer.targetEntityId);
    if (!ent) return;

    const travel = Math.hypot(coords.x - primaryPointer.startX, coords.y - primaryPointer.startY);
    if (travel >= 12 && !primaryPointer.hasMoved) {
      primaryPointer.hasMoved = true;
      ent.state = 'DRAGGING';
      ent.zOrder = getHighestZOrder() + 1;
      ent.splitBadgeAlpha = 0;
      onboardingArc = null;

      if (NB.Audio && NB.Audio.playPickup && isBlocksActive()) {
        NB.Audio.playPickup();
      }
    }

    if (ent.state === 'DRAGGING') {
      // Live pupil tracking for surrounding characters
      const bounds = getEntityBounds(ent);
      for (let i = 0; i < entities.length; i++) {
        if (entities[i].id !== ent.id) {
          entities[i].lookTarget = { x: ent.x, y: ent.y - bounds.height / 2 };
        }
      }

      // Magnetic Snap Detection (uses ent's actual bounds center so preview, pill, and drop match)
      const u = metrics ? metrics.unitSize : 48;
      const snapExitDist = Math.max(82, 1.60 * u);

      if (snapTarget) {
        // Check hysteresis exit
        const bSnap = getEntityBounds(snapTarget);
        const curDist = Math.max(0, Math.hypot(bounds.centerX - bSnap.centerX, bounds.centerY - bSnap.centerY) - (bounds.width + bSnap.width) / 2);
        if (curDist > snapExitDist) {
          snapTarget.expression = 'happy';
          snapTarget = null;
          activeEquationPill = null;
        }
      }

      if (!snapTarget) {
        const candidate = findSnapTarget(ent);
        if (candidate) {
          snapTarget = candidate;
          snapTarget.expression = 'anticipation';
          if (NB.Audio && NB.Audio.playSnapHover && isBlocksActive()) {
            NB.Audio.playSnapHover();
          }
        }
      }

      if (snapTarget) {
        const sum = ent.n + snapTarget.n;
        const bOther = getEntityBounds(snapTarget);
        const topSafe = metrics ? metrics.topSafeY : 20;

        activeEquationPill = {
          x: (bounds.centerX + bOther.centerX) / 2,
          y: Math.max(topSafe + 24, Math.min(bounds.top, bOther.top) - 28),
          mode: sum > maxCap ? 'boom' : 'preview',
          leftN: ent.n,
          rightN: snapTarget.n,
          sumN: sum,
          alpha: 1.0,
          scale: 1.0,
          timer: 0.5
        };
      }
    }
  }

  function onWindowPointerUp(e) {
    if (NB.Audio && NB.Audio.unlock) {
      NB.Audio.unlock();
    }

    if (secondPointer.id === e.pointerId) {
      secondPointer.id = null;
    }

    if (primaryPointer.id !== e.pointerId) return;
    const coords = getCanvasCoords(e.clientX, e.clientY);
    const isFromDock = primaryPointer.isFromDock;
    const dockN = primaryPointer.dockN;
    const wasMoved = primaryPointer.hasMoved;
    const isBadgeHit = primaryPointer.isSplitBadgeHit;
    const targetId = primaryPointer.targetEntityId;

    // Reset primary pointer
    primaryPointer.id = null;
    primaryPointer.isFromDock = false;
    primaryPointer.draggedEntity = null;

    // Clear look targets when dragging stops
    for (let i = 0; i < entities.length; i++) {
      entities[i].lookTarget = null;
    }

    // 1. Dock tap without drag (released < 10px): spawn block hopping on floor!
    if (isFromDock && !wasMoved) {
      enforceStageCapacity();
      const stageWidth = metrics ? metrics.width : 400;
      const ground = metrics ? metrics.groundY : 350;

      // Find open spot
      const spawnX = stageWidth * (0.25 + Math.random() * 0.5);
      const ent = createEntity(dockN, spawnX, ground, 'IDLE');
      ent.vy = -420;
      ent.scaleY = 1.18;
      ent.scaleX = 0.85;
      ent.zOrder = getHighestZOrder() + 1;
      entities.push(ent);
      lastInteractedEntityId = ent.id;
      onboardingArc = null;

      if (NB.Audio && isBlocksActive()) {
        if (NB.Audio.playPickup) NB.Audio.playPickup();
        if (NB.Audio.speakTap) NB.Audio.speakTap(dockN);
      }
      return;
    }

    // 2. Split badge tap or release
    if (isBadgeHit) {
      const ent = findEntity(targetId);
      if (ent && ent.n >= 2) {
        if (ent.state === 'STRETCH_SPLIT') {
          // Released below 44px threshold: snap back harmlessly!
          ent.state = 'IDLE';
          ent.stretchInfo = null;
          ent.scaleX = 1.12;
          ent.scaleY = 0.90;
          ent.splitBadgeAlpha = 1.0;
          ent.splitBadgeTimer = 5.0;
          activeEquationPill = null;
        } else if (!wasMoved) {
          // Tap on [↔] badge: 1-Tap Split!
          const [pA, pB] = getNextSplitBond(ent.n);
          performSplit(ent, pA, pB);
        }
      }
      return;
    }

    // 3. Body tap or drag release
    const ent = findEntity(targetId);
    if (!ent) return;

    if (!wasMoved) {
      // It was a tap on character body!
      if (splitToolActive && ent.n >= 2) {
        // Split tool is active: 1-Tap Split!
        const [pA, pB] = getNextSplitBond(ent.n);
        performSplit(ent, pA, pB);
      } else {
        // Normal Tap -> Joy Tap! NEVER accidentally splits!
        ent.vy = -480;
        ent.scaleY = 1.20;
        ent.scaleX = 0.84;
        ent.tapProgress = 0.001;
        ent.expression = 'excited';

        if (NB.Audio && isBlocksActive()) {
          if (NB.Audio.playTapBounce) NB.Audio.playTapBounce(ent.n);
          if (NB.Audio.speakTap) NB.Audio.speakTap(ent.n);
        }
        const b = getEntityBounds(ent);
        if (NB.Renderer && NB.Renderer.spawnBurst) {
          NB.Renderer.spawnBurst(ent.x, ent.y - b.height / 2, 'tapSparkle', null);
        }

        // Reveal contextual [↔] Split Badge for 5.0s on characters >= 2
        if (ent.n >= 2) {
          ent.splitBadgeAlpha = 1.0;
          ent.splitBadgeTimer = 5.0;
        }
      }
    } else if (ent.state === 'DRAGGING') {
      // Drag release
      if (!snapTarget) {
        snapTarget = findSnapTarget(ent);
      }
      if (snapTarget) {
        const sum = ent.n + snapTarget.n;
        if (sum > maxCap) {
          performSupernovaBounce(ent, snapTarget);
        } else {
          performMerge(ent, snapTarget);
        }
      } else {
        ent.state = 'IDLE';
        activeEquationPill = null;
        if (snapTarget) {
          snapTarget.expression = 'happy';
          snapTarget = null;
        }
      }
    }
  }

  function onWindowPointerCancel(e) {
    if (secondPointer.id === e.pointerId) {
      secondPointer.id = null;
    }
    if (primaryPointer.id !== e.pointerId) return;

    const targetId = primaryPointer.targetEntityId;
    primaryPointer.id = null;
    primaryPointer.isFromDock = false;
    primaryPointer.draggedEntity = null;
    primaryPointer.grabOffsetX = 0;
    primaryPointer.grabOffsetY = 0;

    for (let i = 0; i < entities.length; i++) {
      entities[i].lookTarget = null;
    }

    if (snapTarget) {
      snapTarget.expression = 'happy';
      snapTarget = null;
    }
    activeEquationPill = null;

    const ent = findEntity(targetId);
    if (ent && (ent.state === 'DRAGGING' || ent.state === 'STRETCH_SPLIT')) {
      ent.state = 'IDLE';
      ent.stretchInfo = null;
    }
  }

  // ---------------------------------------------------------------------------
  // MAIN ANIMATION LOOP (RAF-DRIVEN)
  // ---------------------------------------------------------------------------
  function gameLoop(now) {
    if (!isOpen || !isBlocksActive()) {
      if (isOpen) stop();
      return;
    }

    const dt = Math.min((now - lastTime) / 1000, 0.033);
    lastTime = now;

    // Update challenge idle timer (for 8s auto-hint)
    if (currentMode === 'challenge' && !challengeGoalReached) {
      challengeIdleTimer -= dt;
      if (challengeIdleTimer <= 0) {
        challengeIdleTimer = 16.0;
        triggerChallengeHint();
      }
    }

    // Update onboarding arc
    if (onboardingArc) {
      onboardingTimer -= dt;
      onboardingArc.phase = (onboardingArc.phase + dt * 0.8) % 1.0;
      if (onboardingTimer <= 0) {
        onboardingArc.alpha = Math.max(0, onboardingArc.alpha - dt * 2);
        if (onboardingArc.alpha <= 0) onboardingArc = null;
      }
    }

    // Update equation pill timer
    if (activeEquationPill && activeEquationPill.timer !== undefined) {
      activeEquationPill.timer -= dt;
      if (activeEquationPill.timer <= 0) {
        activeEquationPill.alpha = Math.max(0, activeEquationPill.alpha - dt * 3);
        if (activeEquationPill.alpha <= 0) activeEquationPill = null;
      }
    }

    // Step physics & animation for all entities
    const stageWidth = metrics ? metrics.width : 400;
    const topSafe = metrics ? metrics.topSafeY : 20;
    const ground = metrics ? metrics.groundY : 350;

    for (let i = entities.length - 1; i >= 0; i--) {
      const e = entities[i];
      const bounds = getEntityBounds(e);

      // Fade split badge timer
      if (e.splitBadgeTimer > 0) {
        e.splitBadgeTimer -= dt;
        if (e.splitBadgeTimer <= 0) {
          e.splitBadgeAlpha = Math.max(0, e.splitBadgeAlpha - dt * 2.5);
        }
      } else if (e.splitBadgeAlpha > 0) {
        e.splitBadgeAlpha = Math.max(0, e.splitBadgeAlpha - dt * 2.5);
      }

      // Tap animation progress
      if (e.tapProgress > 0) {
        e.tapProgress += dt / 0.75;
        if (e.tapProgress >= 1) {
          e.tapProgress = 0;
          e.expression = 'happy';
        }
      }

      // Poof out animation
      if (e.state === 'POOFING_OUT') {
        e.poofProgress += dt / 0.25;
        if (e.poofProgress >= 1) {
          entities.splice(i, 1);
          continue;
        }
      }

      // 4-Beat Merge Clock
      if ((e.state === 'MORPHING' || e.state === 'CELEBRATING') && e.morphInfo) {
        const elapsed = now - e.morphInfo.startTime;

        if (elapsed < e.morphInfo.p1End) {
          // Beat 1: Dock (0..130ms) with smooth easeOutCubic
          e.morphInfo.phase = 'dock';
          const raw = Math.max(0, Math.min(1, elapsed / e.morphInfo.p1End));
          e.morphInfo.progress = 1 - Math.pow(1 - raw, 3);
        } else if (elapsed < e.morphInfo.p2End) {
          // Beat 2: Cubes count-up (130ms .. p2End) — keep docked at progress=1.0
          e.morphInfo.phase = 'cubes';
          e.morphInfo.progress = 1.0;
          const p2Elapsed = elapsed - e.morphInfo.p1End;

          const step = Math.min(e.morphInfo.sum, Math.floor(p2Elapsed / e.morphInfo.stepMs) + 1);
          e.morphInfo.activeStepIndex = step - 1;
          if (step > e.morphInfo.litCount) {
            for (let k = e.morphInfo.litCount + 1; k <= step; k++) {
              if (NB.Audio && isBlocksActive()) {
                if (NB.Audio.playCountNote) NB.Audio.playCountNote(k, e.morphInfo.sum);
                else if (NB.Audio.playMarimbaNote) NB.Audio.playMarimbaNote(k);
              }
            }
            e.morphInfo.litCount = step;
          }
        } else if (elapsed < e.morphInfo.p3End) {
          // Beat 3: Reveal (p2End .. p3End)
          e.morphInfo.phase = 'reveal';
          e.morphInfo.progress = 1.0;
          e.morphInfo.litCount = 0;
          e.morphInfo.activeStepIndex = -1;
          const p3Elapsed = elapsed - e.morphInfo.p2End;
          const p3Total = e.morphInfo.p3End - e.morphInfo.p2End;
          const t = Math.min(1.0, p3Elapsed / p3Total);
          e.morphInfo.revealAlpha = Math.min(1.0, t / 0.45);
          e.morphInfo.revealPop = t < 0.55
            ? (0.86 + 0.22 * (t / 0.55))
            : (1.08 - 0.08 * ((t - 0.55) / 0.45));
          e.morphInfo.revealScale = e.morphInfo.revealPop;

          if (!e.morphInfo.starburstTriggered) {
            e.morphInfo.starburstTriggered = true;
            const char = (NB.Data && NB.Data.getCharacter) ? NB.Data.getCharacter(e.n) : { primaryColor: '#facc15' };
            if (NB.Renderer && NB.Renderer.spawnBurst) {
              NB.Renderer.spawnBurst(e.x, e.y - bounds.height / 2, 'mergeStarburst', char.primaryColor);
            }
            const tlh = getTLH();
            if (tlh && tlh.app && tlh.app.burstConfetti && isBlocksActive() && tlh.app.settings && tlh.app.settings.confettiEnabled !== false) {
              tlh.app.burstConfetti(e.x, e.y - bounds.height / 2);
            }
            if (NB.Audio && NB.Audio.playMergeFanfare && isBlocksActive()) {
              NB.Audio.playMergeFanfare(e.n);
            }

            // Unlock friend in dock if 6..10
            if (e.n >= 6 && e.n <= 10 && !isUnlocked(e.n)) {
              unlockFriend(e.n);
              if (NB.Audio && NB.Audio.playUnlockJingle && isBlocksActive()) {
                NB.Audio.playUnlockJingle();
              }
              updateDock();
            }
          }
        } else if (elapsed < e.morphInfo.totalDuration) {
          // Beat 4: Celebrate / Idle (upward launch stretch)
          if (e.state === 'MORPHING') {
            e.state = 'CELEBRATING';
            e.vy = -420;
            e.scaleY = 1.16;
            e.scaleX = 1 / 1.16;

            const isFirstInSession = !firstMergeSessionMap.has(e.n);
            firstMergeSessionMap.add(e.n);
            if (NB.Audio && NB.Audio.speakMerge && isBlocksActive()) {
              NB.Audio.speakMerge(e.morphInfo.sourceA, e.morphInfo.sourceB, e.n, isFirstInSession);
            }

            checkChallengeGoal('merge', { target: e.n });
          }
        } else {
          e.state = 'IDLE';
          e.morphInfo = null;
        }
      }

      // State: DRAGGING
      if (e.state === 'DRAGGING') {
        const liftY = (primaryPointer.type === 'touch') ? -10 : -4;
        const targetX = primaryPointer.currentX + (primaryPointer.grabOffsetX || 0);
        const targetY = Math.min(ground, primaryPointer.currentY + (primaryPointer.grabOffsetY || 0) + liftY);

        // Drag follow spring
        const [nextX, nextVx] = stepSpring(e.x, e.vx, targetX, DRAG_STIFFNESS, DRAG_DAMPING, dt);
        const [nextY, nextVy] = stepSpring(e.y, e.vy, targetY, DRAG_STIFFNESS, DRAG_DAMPING, dt);
        e.x = nextX; e.vx = nextVx;
        e.y = nextY; e.vy = nextVy;

        // Velocity tilt
        const targetTilt = Math.max(-0.22, Math.min(0.22, e.vx * 0.00045));
        const [nextTilt, nextTiltVel] = stepSpring(e.tilt, e.tiltVel, targetTilt, TILT_STIFFNESS, TILT_DAMPING, dt);
        e.tilt = nextTilt; e.tiltVel = nextTiltVel;

        // Ceiling clamp: prevent Numberlings from clipping above topSafeY
        const numberlingPad = metrics ? metrics.unitSize * 0.65 : 30;
        const minAllowedY = topSafe + bounds.height + numberlingPad;
        if (e.y < minAllowedY) {
          e.y = minAllowedY;
          e.vy = 0;
        }

        // Stage walls clamp
        const halfW = bounds.width / 2;
        if (e.x < halfW + 12) { e.x = halfW + 12; e.vx = 0; }
        if (e.x > stageWidth - halfW - 12) { e.x = stageWidth - halfW - 12; e.vx = 0; }
      }

      // State: IDLE or CELEBRATING (free physical body)
      if (e.state === 'IDLE' || e.state === 'CELEBRATING') {
        // Gravity
        e.vy += GRAVITY * dt;
        e.y += e.vy * dt;
        e.x += e.vx * dt;
        e.vx *= Math.pow(0.85, dt * 60);

        // Ceiling clamp during high jump apex
        const numberlingPad = metrics ? metrics.unitSize * 0.65 : 30;
        const minAllowedY = topSafe + bounds.height + numberlingPad;
        if (e.y < minAllowedY) {
          e.y = minAllowedY;
          e.vy = Math.max(0, e.vy);
        }

        // Ground Collision
        if (e.y >= ground) {
          e.y = ground;
          if (e.vy > 60) {
            e.scaleY = Math.max(0.74, Math.min(0.92, 1 - e.vy / 1500));
            e.scaleX = 1 / e.scaleY;
            if (NB.Audio && NB.Audio.playLand && isBlocksActive()) {
              NB.Audio.playLand(e.n);
            }
          }
          e.vy = 0;
          e.vx = 0;

          if (e.state === 'CELEBRATING' && (!e.morphInfo || now - e.morphInfo.startTime >= e.morphInfo.totalDuration)) {
            e.state = 'IDLE';
            e.morphInfo = null;
          }
        }

        // Squash-and-stretch spring back to 1.0 (area-preserving)
        const [nextScaleY, nextScaleYVel] = stepSpring(e.scaleY, e.scaleYVel, 1.0, SQUASH_STIFFNESS, SQUASH_DAMPING, dt);
        e.scaleY = Math.max(0.74, Math.min(1.26, nextScaleY));
        e.scaleYVel = nextScaleYVel;
        e.scaleX = 1 / e.scaleY;

        // Tilt recovery back to 0
        const [nextTilt, nextTiltVel] = stepSpring(e.tilt, e.tiltVel, 0, TILT_STIFFNESS, TILT_DAMPING, dt);
        e.tilt = nextTilt;
        e.tiltVel = nextTiltVel;

        // Wall clamps
        const halfW = bounds.width / 2;
        if (e.x < halfW + 12) { e.x = halfW + 12; e.vx = 0; }
        if (e.x > stageWidth - halfW - 12) { e.x = stageWidth - halfW - 12; e.vx = 0; }
      }
    }

    // Render Frame
    if (renderer && NB.Renderer && NB.Renderer.renderFrame) {
      let snapPreviewObj = null;
      if (snapTarget) {
        const dragged = findEntity(primaryPointer.targetEntityId);
        if (dragged) {
          const sum = dragged.n + snapTarget.n;
          snapPreviewObj = {
            sourceId: dragged.id,
            targetId: snapTarget.id,
            x: snapTarget.x,
            y: snapTarget.y,
            sum: sum,
            exceedsCap: sum > maxCap,
            pulse: (now % 1000) / 1000
          };
        }
      }

      const renderState = {
        entities: entities,
        metrics: metrics,
        splitModeActive: splitToolActive,
        onboardingArc: onboardingArc,
        snapPreview: snapPreviewObj,
        equationPill: activeEquationPill
      };

      NB.Renderer.renderFrame(renderState, now);
    }

    rAFId = requestFrame(gameLoop);
  }

  // ---------------------------------------------------------------------------
  // PUBLIC API: INIT, OPEN, STOP, APPLYSETTINGS, SPAWNFROMDOCK
  // ---------------------------------------------------------------------------
  function init() {
    if (initialized) return;
    initialized = true;

    canvasEl = document.getElementById('nb-stage-canvas');
    stageWrapEl = document.getElementById('nb-stage-wrap');
    hudOverlayEl = document.getElementById('nb-hud-overlay');
    dockEl = document.getElementById('nb-dock');
    dockFriendsEl = document.getElementById('nb-dock-friends');

    modePlayBtn = document.getElementById('nb-mode-play');
    modeChallengeBtn = document.getElementById('nb-mode-challenge');
    challengeBarEl = document.getElementById('nb-challenge-bar');
    challengeSpeakBtn = document.getElementById('nb-challenge-speak-btn');
    challengeIconCanvas = document.getElementById('nb-challenge-icon');
    challengeTextEl = document.getElementById('nb-challenge-text');
    challengeStarsEl = document.getElementById('nb-challenge-stars');
    challengeHintBtn = document.getElementById('nb-challenge-hint-btn');
    challengeSkipBtn = document.getElementById('nb-challenge-skip-btn');
    toolSplitBtn = document.getElementById('nb-tool-split');
    toolUnlockBtn = document.getElementById('nb-tool-unlock');
    toolResetBtn = document.getElementById('nb-tool-reset');
    toolCountBtn = document.getElementById('nb-tool-count');

    if (canvasEl && hudOverlayEl && NB.Renderer && NB.Renderer.init) {
      renderer = NB.Renderer.init(canvasEl, hudOverlayEl);
      metrics = renderer.getMetrics();
    }

    unlockedFriends = loadUnlocked();
    challengeStars = loadStars();

    initDock();

    // Mode Switches
    if (modePlayBtn) {
      modePlayBtn.addEventListener('click', () => switchMode('play'));
    }
    if (modeChallengeBtn) {
      modeChallengeBtn.addEventListener('click', () => switchMode('challenge'));
    }

    // Challenge Actions
    if (challengeSpeakBtn) {
      challengeSpeakBtn.addEventListener('click', () => {
        const c = getCurrentChallenge();
        if (c && NB.Audio && NB.Audio.speak && isBlocksActive()) {
          NB.Audio.speak(c.prompt, 'high');
        }
      });
    }
    if (challengeHintBtn) {
      challengeHintBtn.addEventListener('click', () => {
        triggerChallengeHint();
      });
    }
    if (challengeSkipBtn) {
      challengeSkipBtn.addEventListener('click', () => {
        advanceChallenge();
      });
    }

    // Stage Tools
    if (toolSplitBtn) {
      toolSplitBtn.addEventListener('click', () => {
        splitToolActive = !splitToolActive;
        toolSplitBtn.classList.toggle('is-active', splitToolActive);
        toolSplitBtn.setAttribute('aria-pressed', String(splitToolActive));
        if (NB.Audio && NB.Audio.unlock) NB.Audio.unlock();
      });
    }

    if (toolUnlockBtn) {
      toolUnlockBtn.addEventListener('click', () => {
        const allUnlocked = unlockedFriends.length >= 10;
        if (allUnlocked) {
          unlockedFriends = [...DEFAULT_UNLOCKED];
        } else {
          unlockedFriends = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
        }
        saveUnlocked(unlockedFriends);
        updateDock();
        if (NB.Audio && NB.Audio.playUnlockJingle && isBlocksActive()) {
          NB.Audio.playUnlockJingle();
        }
      });
    }

    if (toolResetBtn) {
      toolResetBtn.addEventListener('click', () => {
        if (NB.Audio && NB.Audio.playPickup && isBlocksActive()) {
          NB.Audio.playPickup();
        }
        // Poof out all entities
        entities.forEach(e => {
          e.state = 'POOFING_OUT';
          e.poofProgress = 0.001;
          const b = getEntityBounds(e);
          if (NB.Renderer && NB.Renderer.spawnBurst) {
            NB.Renderer.spawnBurst(e.x, e.y - b.height / 2, 'poofOut', null);
          }
        });

        addTimer(() => {
          entities = [];
          if (currentMode === 'challenge') {
            const c = getCurrentChallenge();
            loadChallenge(c);
          } else {
            spawnStarterFriends();
          }
        }, 260);
      });
    }

    if (toolCountBtn) {
      toolCountBtn.addEventListener('click', () => {
        const targetN = getTargetNumberForCount();
        const tlh = getTLH();
        const games = (tlh && tlh.GAMES) || (typeof GAMES !== 'undefined' ? GAMES : null);
        const numberGameObj = (tlh && tlh.numberGame) || (typeof numberGame !== 'undefined' ? numberGame : null);
        const appObj = (tlh && tlh.app) || (typeof app !== 'undefined' ? app : null);

        if (games && games.numbers && numberGameObj) {
          numberGameObj.currentData = games.numbers.find(item => item.num === targetN) || games.numbers[0];
        }
        if (appObj && appObj.switchView) {
          appObj.switchView('numbers');
        }
      });
    }

    // Attach Pointer Events
    if (dockFriendsEl) {
      dockFriendsEl.addEventListener('pointerdown', onDockPointerDown);
    }
    if (canvasEl) {
      canvasEl.addEventListener('pointerdown', onCanvasPointerDown);
    }

    window.addEventListener('pointermove', onWindowPointerMove, { passive: false });
    window.addEventListener('pointerup', onWindowPointerUp, { passive: false });
    window.addEventListener('pointercancel', onWindowPointerCancel, { passive: true });

    // Window Resize / Layout Handling
    const handleResize = () => {
      if (!isOpen || !renderer) return;
      renderer.resize();
      metrics = renderer.getMetrics();
      const ground = metrics.groundY;
      entities.forEach(e => {
        if (e.state === 'IDLE') {
          e.y = ground;
        }
        const b = getEntityBounds(e);
        const halfW = b.width / 2;
        e.x = Math.max(halfW + 12, Math.min(metrics.width - halfW - 12, e.x));
      });
      updateDock();
    };

    window.addEventListener('resize', handleResize);
    if (typeof window !== 'undefined' && window.ResizeObserver && stageWrapEl) {
      const ro = new window.ResizeObserver(() => handleResize());
      ro.observe(stageWrapEl);
    }

    // Visibility Change: Pauses rAF to eliminate idle battery drain
    document.addEventListener('visibilitychange', () => {
      if (document.hidden) {
        if (rAFId) {
          cancelFrame(rAFId);
          rAFId = null;
        }
      } else {
        if (isOpen && isBlocksActive() && !rAFId) {
          lastTime = nowMs();
          rAFId = requestFrame(gameLoop);
        }
      }
    });
  }

  function open() {
    init();
    isOpen = true;
    maxCap = getMaxCap();

    if (renderer) {
      renderer.resize();
      metrics = renderer.getMetrics();
    }

    if (typeof requestAnimationFrame === 'function') {
      requestAnimationFrame(() => {
        if (isOpen && renderer) {
          renderer.resize();
          metrics = renderer.getMetrics();
          updateDock();
        }
      });
    }

    applySettings();

    // Spawns starter blocks 1 and 2 if stage is completely empty
    if (entities.length === 0) {
      if (currentMode === 'challenge') {
        const c = getCurrentChallenge();
        loadChallenge(c);
      } else {
        spawnStarterFriends();
      }
    }

    // Paint one immediate frame synchronously to prevent blank flash on open
    if (NB.Renderer && NB.Renderer.renderFrame) {
      NB.Renderer.renderFrame({
        entities: entities,
        metrics: metrics,
        splitModeActive: splitToolActive,
        onboardingArc: onboardingArc,
        snapPreview: null,
        equationPill: activeEquationPill
      }, nowMs());
    }

    // Start rAF loop
    if (!rAFId) {
      lastTime = nowMs();
      rAFId = requestFrame(gameLoop);
    }

    // Synchronously call speakOpenIntro so switchView prepends game intro when enabled
    if (NB.Audio && NB.Audio.speakOpenIntro) {
      NB.Audio.speakOpenIntro();
    }
  }

  function getTargetNumberForCount() {
    maxCap = getMaxCap();
    const liveEntities = entities.filter(e => e.state !== 'POOFING_OUT');
    if (liveEntities.length === 0) return 1;

    let candidate = null;
    if (lastInteractedEntityId) {
      candidate = liveEntities.find(e => e.id === lastInteractedEntityId);
    }
    if (!candidate) {
      // Find largest Numberblock currently on stage
      candidate = liveEntities.reduce((best, curr) => (curr.n > best.n ? curr : best), liveEntities[0]);
    }
    let targetN = candidate ? candidate.n : 1;
    targetN = Math.max(1, Math.min(maxCap, targetN));
    return targetN;
  }

  function openWithNumber(n) {
    n = parseInt(n, 10);
    if (isNaN(n) || n < 1) n = 1;
    init();
    isOpen = true;
    maxCap = getMaxCap();
    if (n > maxCap) n = maxCap;

    if (renderer) {
      renderer.resize();
      metrics = renderer.getMetrics();
    }

    if (typeof requestAnimationFrame === 'function') {
      requestAnimationFrame(() => {
        if (isOpen && renderer) {
          renderer.resize();
          metrics = renderer.getMetrics();
          updateDock();
        }
      });
    }

    applySettings();

    // Unlock n if <= 10
    if (n <= 10 && !unlockedFriends.includes(n)) {
      unlockedFriends.push(n);
      unlockedFriends.sort((a, b) => a - b);
      saveUnlocked(unlockedFriends);
      if (NB.Data && NB.Data.unlockCharacter) {
        NB.Data.unlockCharacter(n);
      }
      updateDock();
    }

    // Switch to free play mode if in challenge mode
    if (currentMode !== 'play') {
      currentMode = 'play';
      if (modePlayBtn && modeChallengeBtn) {
        modePlayBtn.classList.add('active');
        modeChallengeBtn.classList.remove('active');
      }
      if (challengeBarEl) challengeBarEl.classList.add('hidden');
    }

    // Clear stage and setup Numberblock n center-stage
    clearAllTimers();
    entities = [];
    onboardingArc = null;
    onboardingTimer = 0;
    snapTarget = null;
    activeEquationPill = null;
    splitToolActive = false;
    if (toolSplitBtn) {
      toolSplitBtn.classList.remove('is-active');
      toolSplitBtn.setAttribute('aria-pressed', 'false');
    }

    const stageWidth = metrics ? metrics.width : 400;
    const ground = metrics ? metrics.groundY : 350;
    const spawnX = stageWidth * 0.5;

    const ent = createEntity(n, spawnX, ground, 'IDLE');
    ent.vy = -480; // Joyful celebration bounce!
    ent.scaleY = 1.25;
    ent.scaleX = 0.8;
    ent.zOrder = 1;
    entities.push(ent);
    lastInteractedEntityId = ent.id;

    // Paint one immediate frame synchronously to prevent blank flash on open
    if (NB.Renderer && NB.Renderer.renderFrame) {
      NB.Renderer.renderFrame({
        entities: entities,
        metrics: metrics,
        splitModeActive: splitToolActive,
        onboardingArc: onboardingArc,
        snapPreview: null,
        equationPill: activeEquationPill
      }, nowMs());
    }

    // Start rAF loop if not running
    if (!rAFId) {
      lastTime = nowMs();
      rAFId = requestFrame(gameLoop);
    }

    // Celebration burst & intro speech
    const char = NB.Data ? NB.Data.getCharacter(n) : null;
    if (NB.Renderer && NB.Renderer.spawnBurst) {
      const b = getEntityBounds(ent);
      const topY = b ? (ground - b.height * 0.5) : (ground - 60);
      NB.Renderer.spawnBurst(spawnX, topY, 'mergeStarburst', char ? char.primaryColor : null);
    }

    if (NB.Audio) {
      if (NB.Audio.playUnlockJingle) NB.Audio.playUnlockJingle();
      else if (NB.Audio.playPickup) NB.Audio.playPickup();

      const line = (char && char.tapLines && char.tapLines.length > 0)
        ? char.tapLines[0]
        : (char && char.name ? `I am ${char.name}!` : `Numberblock ${n}!`);
      if (NB.Audio.speak) {
        NB.Audio.speak(line, 'high');
      }
    }
  }

  function stop() {
    isOpen = false;
    if (rAFId) {
      cancelFrame(rAFId);
      rAFId = null;
    }

    clearAllTimers();

    // Reset pointers
    primaryPointer.id = null;
    primaryPointer.isFromDock = false;
    primaryPointer.draggedEntity = null;
    primaryPointer.grabOffsetX = 0;
    primaryPointer.grabOffsetY = 0;
    secondPointer.id = null;

    // Settle all active dragging/morphing entities cleanly to IDLE on ground
    entities.forEach(e => {
      if (e.state === 'DRAGGING' || e.state === 'MORPHING' || e.state === 'STRETCH_SPLIT' || e.state === 'CELEBRATING') {
        e.state = 'IDLE';
        e.morphInfo = null;
        e.stretchInfo = null;
        if (metrics) e.y = metrics.groundY;
        e.vy = 0;
        e.vx = 0;
      }
      e.scaleX = 1.0;
      e.scaleY = 1.0;
      e.scaleYVel = 0;
      e.tilt = 0;
      e.tiltVel = 0;
      e.expression = 'happy';
      e.lookTarget = null;
      e.hintGlow = false;
    });

    snapTarget = null;
    activeEquationPill = null;
    splitToolActive = false;
    if (toolSplitBtn) {
      toolSplitBtn.classList.remove('is-active');
      toolSplitBtn.setAttribute('aria-pressed', 'false');
    }
  }

  function applySettings() {
    maxCap = getMaxCap();

    if (maxCap === 10) {
      // Downgraded 20 -> 10 while entities n > 10 are on stage:
      // immediately split them live into 10 and n - 10!
      const highEntities = entities.filter(e => e.n > 10 && e.state !== 'POOFING_OUT');
      highEntities.forEach(ent => {
        performSplit(ent, 10, ent.n - 10);
      });

      if (currentMode === 'challenge') {
        const c = getCurrentChallenge();
        if (c && c.maxRequired > 10) {
          advanceChallenge();
        }
      }
    }

    updateDock();
  }

  function spawnFromDock(n, pointerEvent) {
    if (pointerEvent && pointerEvent.clientX !== undefined) {
      onDockPointerDown(pointerEvent);
    } else {
      enforceStageCapacity();
      const stageWidth = metrics ? metrics.width : 400;
      const ground = metrics ? metrics.groundY : 350;
      const spawnX = stageWidth * (0.25 + Math.random() * 0.5);
      const ent = createEntity(n, spawnX, ground, 'IDLE');
      ent.vy = -420;
      ent.scaleY = 1.18;
      ent.scaleX = 0.85;
      ent.zOrder = getHighestZOrder() + 1;
      entities.push(ent);
      lastInteractedEntityId = ent.id;
      onboardingArc = null;

      if (NB.Audio && isBlocksActive()) {
        if (NB.Audio.playPickup) NB.Audio.playPickup();
        if (NB.Audio.speakTap) NB.Audio.speakTap(n);
      }
    }
  }

  // ---------------------------------------------------------------------------
  // EXPORT TO WINDOW.NUMBERBLOCKS
  // ---------------------------------------------------------------------------
  NB.Game = {
    init: init,
    open: open,
    openWithNumber: openWithNumber,
    stop: stop,
    applySettings: applySettings,
    spawnFromDock: spawnFromDock
  };

  if (typeof document !== 'undefined') {
    if (document.readyState === 'loading') {
      window.addEventListener('DOMContentLoaded', () => init());
    } else {
      init();
    }
  }

})();

    </script>
</body>
</html>
