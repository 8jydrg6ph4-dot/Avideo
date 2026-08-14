# Avideo
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Avideo — Liquid Glass</title>
    <style>
        /* ===== БАЗОВЫЙ СБРОС И ШРИФТ ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0a0a0f;
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Helvetica Neue", Helvetica, Arial, sans-serif;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 2rem;
            color: #1d1d1f;
            position: relative;
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        /* ===== ГРАДИЕНТНЫЙ ФОН (ГЛУБИНА ДЛЯ СТЕКЛА) ===== */
        .gradient-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            background: radial-gradient(circle at 20% 20%, #aac9ff 0%, #7aa2f7 25%, #5f7af2 50%, #3b3f6e 75%, #1a1a2e 100%);
            background-size: 200% 200%;
            animation: gradientShift 12s ease-in-out infinite alternate;
            pointer-events: none;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 0%; }
            100% { background-position: 100% 100%; }
        }

        /* ===== ОБЩАЯ ОБОЛОЧКА ===== */
        .glass-wrapper {
            position: relative;
            z-index: 2;
            width: 100%;
            max-width: 1200px;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        /* ===== ЗАГОЛОВОК ===== */
        .header-logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            backdrop-filter: blur(30px) saturate(180%);
            -webkit-backdrop-filter: blur(30px) saturate(180%);
            background: rgba(255, 255, 255, 0.25);
            border-radius: 3rem;
            padding: 1rem 2rem;
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2), inset 0 1px 1px rgba(255, 255, 255, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.4);
            transition: transform 0.3s cubic-bezier(0.2, 0.8, 0.2, 1);
            animation: floatIn 0.8s ease-out;
        }

        .header-logo:hover {
            transform: scale(1.02);
        }

        .logo-icon {
            font-size: 2.5rem;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
        }

        .logo-text {
            font-size: 2.2rem;
            font-weight: 700;
            letter-spacing: -0.03em;
            background: linear-gradient(to right, #1a1a2e, #2d2d44);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 1px 2px rgba(255, 255, 255, 0.6);
        }

        .logo-sub {
            font-size: 0.9rem;
            font-weight: 500;
            letter-spacing: 0.3em;
            text-transform: uppercase;
            color: rgba(30, 30, 50, 0.7);
            margin-left: auto;
        }

        /* ===== ОСНОВНАЯ СЕТКА КАРТОЧЕК ===== */
        .video-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            perspective: 1200px;
        }

        /* ===== КАРТОЧКА ВИДЕО (LIQUID GLASS) ===== */
        .video-card {
            backdrop-filter: blur(35px) saturate(200%);
            -webkit-backdrop-filter: blur(35px) saturate(200%);
            background: rgba(255, 255, 255, 0.35);
            border-radius: 3rem;
            padding: 2rem 1.5rem 1.5rem;
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.3),
                inset 0 1px 2px rgba(255, 255, 255, 0.7),
                inset 0 -1px 2px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.6);
            transition: all 0.4s cubic-bezier(0.2, 0.8, 0.2, 1);
            transform-style: preserve-3d;
            animation: cardAppear 0.7s ease-out forwards;
            opacity: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .video-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle at 30% 20%, rgba(255, 255, 255, 0.8) 0%, rgba(255, 255, 255, 0) 60%);
            opacity: 0;
            transition: opacity 0.6s;
            pointer-events: none;
            z-index: 2;
        }

        .video-card:hover::before {
            opacity: 0.35;
        }

        .video-card:hover {
            transform: translateY(-10px) rotateX(3deg) rotateY(2deg);
            box-shadow: 
                0 30px 60px rgba(0, 0, 0, 0.4),
                inset 0 1px 3px rgba(255, 255, 255, 0.9);
            background: rgba(255, 255, 255, 0.45);
        }

        .video-card:nth-child(1) { animation-delay: 0.1s; }
        .video-card:nth-child(2) { animation-delay: 0.2s; }
        .video-card:nth-child(3) { animation-delay: 0.3s; }
        .video-card:nth-child(4) { animation-delay: 0.4s; }

        @keyframes cardAppear {
            0% { opacity: 0; transform: translateY(40px) scale(0.9); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }

        @keyframes floatIn {
            0% { opacity: 0; transform: translateY(-20px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        /* ===== ИКОНКА / ПРЕВЬЮ ===== */
        .thumbnail {
            width: 100%;
            aspect-ratio: 16 / 9;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 1.8rem;
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.5), 0 10px 20px rgba(0, 0, 0, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            margin-bottom: 1.5rem;
            transition: transform 0.3s ease;
            background-image: linear-gradient(135deg, rgba(255,255,255,0.4) 0%, rgba(200,200,240,0.2) 100%);
            border: 1px solid rgba(255, 255, 255, 0.7);
            position: relative;
            overflow: hidden;
        }

        .video-card:hover .thumbnail {
            transform: scale(1.02);
        }

        .thumbnail span {
            filter: drop-shadow(0 4px 6px rgba(0,0,0,0.3));
        }

        .play-overlay {
            position: absolute;
            inset: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0, 0, 0, 0.1);
            border-radius: inherit;
            transition: background 0.3s;
        }

        .play-button {
            width: 60px;
            height: 60px;
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(10px);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: #1a1a2e;
            box-shadow: 0 8px 16px rgba(0,0,0,0.3), inset 0 1px 1px rgba(255,255,255,0.8);
            transition: all 0.2s;
            cursor: pointer;
        }

        .video-card:hover .play-button {
            background: rgba(255, 255, 255, 0.9);
            transform: scale(1.1);
        }

        /* ===== ТЕКСТОВАЯ ИНФОРМАЦИЯ ===== */
        .video-title {
            font-size: 1.5rem;
            font-weight: 650;
            letter-spacing: -0.02em;
            color: #1a1a2e;
            margin-bottom: 0.4rem;
        }

        .video-desc {
            font-size: 0.95rem;
            color: rgba(30, 30, 50, 0.75);
            margin-bottom: 1.5rem;
            font-weight: 450;
            line-height: 1.4;
        }

        .meta-info {
            display: flex;
            justify-content: space-between;
            width: 100%;
            font-size: 0.8rem;
            color: rgba(20, 20, 40, 0.6);
            border-top: 1px solid rgba(255, 255, 255, 0.4);
            padding-top: 0.8rem;
            letter-spacing: 0.02em;
        }

        /* ===== АНИМАЦИЯ ПУЛЬСА ДЛЯ СТЕКЛА (ДОПОЛНИТЕЛЬНАЯ) ===== */
        .pulse-layer {
            position: fixed;
            bottom: 5%;
            right: 5%;
            width: 200px;
            height: 200px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 50%;
            z-index: 1;
            animation: pulse 4s ease-in-out infinite;
            pointer-events: none;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.3; }
            50% { transform: scale(1.3); opacity: 0.6; }
        }

        /* ===== МЕДИАЗАПРОСЫ ДЛЯ ТЕЛЕФОНОВ ===== */
        @media (max-width: 600px) {
            body {
                padding: 1rem;
            }
            .header-logo {
                flex-wrap: wrap;
                justify-content: center;
                text-align: center;
            }
            .logo-sub {
                margin-left: 0;
                width: 100%;
                margin-top: 0.4rem;
            }
        }
    </style>
</head>
<body>
    <!-- Живой градиентный фон -->
    <div class="gradient-bg"></div>
    <!-- Дополнительный пульсирующий элемент -->
    <div class="pulse-layer"></div>

    <div class="glass-wrapper">
        <!-- Шапка в стиле Liquid Glass -->
        <header class="header-logo">
            <div class="logo-icon">▶</div>
            <div class="logo-text">Avideo</div>
            <div class="logo-sub">Liquid Glass</div>
        </header>

        <!-- Сетка видеокарточек -->
        <main class="video-grid">
            <!-- Карточка 1 -->
            <div class="video-card">
                <div class="thumbnail">
                    <span>🎬</span>
                    <div class="play-overlay">
                        <div class="play-button">▶</div>
                    </div>
                </div>
                <h3 class="video-title">Синематика в стекле</h3>
                <p class="video-desc">Эффект Liquid Glass с плавными анимациями и глубиной.</p>
                <div class="meta-info">
                    <span>4K · 60fps</span>
                    <span>12:42</span>
                </div>
            </div>

            <!-- Карточка 2 -->
            <div class="video-card">
                <div class="thumbnail">
                    <span>🌌</span>
                    <div class="play-overlay">
                        <div class="play-button">▶</div>
                    </div>
                </div>
                <h3 class="video-title">Ночной город</h3>
                <p class="video-desc">Градиентные переливы и стеклянные отражения.</p>
                <div class="meta-info">
                    <span>8K · 120fps</span>
                    <span>08:17</span>
                </div>
            </div>

            <!-- Карточка 3 -->
            <div class="video-card">
                <div class="thumbnail">
                    <span>🎧</span>
                    <div class="play-overlay">
                        <div class="play-button">▶</div>
                    </div>
                </div>
                <h3 class="video-title">Аудио визуализация</h3>
                <p class="video-desc">Жидкое стекло реагирует на каждый бит.</p>
                <div class="meta-info">
                    <span>4K · 30fps</span>
                    <span>15:03</span>
                </div>
            </div>

            <!-- Карточка 4 -->
            <div class="video-card">
                <div class="thumbnail">
                    <span>🍃</span>
                    <div class="play-overlay">
                        <div class="play-button">▶</div>
                    </div>
                </div>
                <h3 class="video-title">Природа в потоке</h3>
                <p class="video-desc">Органические формы сквозь матовое стекло.</p>
                <div class="meta-info">
                    <span>6K · 60fps</span>
                    <span>21:55</span>
                </div>
            </div>
        </main>
    </div>
</body>
</html>
