<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Valentine Surprise</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            min-height: 100vh;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Romantic Pink Heart Background */
        .heart-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 80%, rgba(255, 182, 193, 0.4) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(255, 105, 180, 0.4) 0%, transparent 50%),
                radial-gradient(circle at 40% 40%, rgba(255, 192, 203, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 60% 60%, rgba(219, 112, 147, 0.3) 0%, transparent 50%),
                linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fad0c4 100%);
            z-index: -2;
            animation: heartPulse 8s ease-in-out infinite;
        }

        .heart-bg::before {
            content: '';
            position: absolute;
            top: 10%;
            left: 10%;
            width: 100px;
            height: 90px;
            background: rgba(255, 105, 180, 0.2);
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            animation: floatHeart 15s linear infinite;
        }

        .heart-bg::after {
            content: '';
            position: absolute;
            bottom: 20%;
            right: 15%;
            width: 80px;
            height: 72px;
            background: rgba(255, 182, 193, 0.25);
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            animation: floatHeart 20s linear infinite reverse;
        }

        .container {
            text-align: center;
            animation: fadeInUp 1s ease-out;
            position: relative;
            z-index: 1;
        }

        h1 {
            font-size: 2.8rem;
            color: #fff;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            margin-bottom: 2rem;
            animation: glow 2s ease-in-out infinite alternate;
            line-height: 1.3;
            max-width: 90vw;
            z-index: 2;
        }

        .buttons {
            display: flex;
            gap: 2rem;
            justify-content: center;
            flex-wrap: wrap;
            position: relative;
            z-index: 2;
        }

        .btn {
            padding: 1.2rem 2.5rem;
            font-size: 1.3rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
        }

        .btn-yes {
            background: linear-gradient(45deg, #ff6b9d, #ff8fab);
            color: white;
        }

        .btn-no {
            background: linear-gradient(45deg, #feca57, #ff9ff3);
            color: #333;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 30px rgba(0,0,0,0.3);
        }

        .hearts-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1000;
        }

        .heart {
            position: absolute;
            font-size: 2rem;
            color: #ff69b4;
            pointer-events: none;
            animation: float 3s ease-out forwards;
        }

        .secret-page {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 20%, rgba(255, 182, 193, 0.5) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(255, 105, 180, 0.5) 0%, transparent 50%),
                radial-gradient(circle at 50% 50%, rgba(255, 192, 203, 0.4) 0%, transparent 50%),
                linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 0;
            visibility: hidden;
            transition: all 1s ease;
            z-index: 10;
        }

        .secret-page.active {
            opacity: 1;
            visibility: visible;
        }

        .secret-page .heart-bg {
            z-index: -1;
        }

        .secret-message {
            font-size: 1.8rem;
            color: white;
            text-align: center;
            line-height: 1.6;
            max-width: 600px;
            animation: slideInUp 1s ease-out 0.5s both;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .emoji {
            font-size: 3rem;
            animation: bounce 2s infinite;
            margin-bottom: 1rem;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes glow {
            from { text-shadow: 2px 2px 4px rgba(0,0,0,0.3), 0 0 10px #fff; }
            to { text-shadow: 2px 2px 4px rgba(0,0,0,0.3), 0 0 20px #ff69b4; }
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }

        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-20px); }
            60% { transform: translateY(-10px); }
        }

        @keyframes heartPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes floatHeart {
            0% { transform: translateY(0px) rotate(0deg); }
            100% { transform: translateY(-100vh) rotate(360deg); }
        }

        @media (max-width: 768px) {
            h1 { font-size: 1.8rem; line-height: 1.2; }
            .secret-message { font-size: 1.2rem; }
            .btn { padding: 1rem 2rem; font-size: 1.1rem; }
        }
    </style>
</head>
<body>
    <!-- Romantic Pink Heart Background -->
    <div class="heart-bg"></div>
    
    <div class="container" id="mainPage">
        <div class="emoji">💕</div>
        <h1>If I Will Give U All Of My Time<br>Will U Become My Valantine🥰❤💕</h1>
        <div class="buttons">
            <button class="btn btn-yes" onclick="showHeartsAndSecret()">Yes🥰</button>
            <button class="btn btn-no" id="noBtn" onclick="moveNoButton()">No 😢</button>
        </div>
    </div>

    <div class="hearts-container" id="hearts"></div>

    <div class="secret-page" id="secretPage">
        <div class="heart-bg"></div>
        <div class="emoji">💖✨💖</div>
        <div class="secret-message">
            Tum Jab Kahogi 'Hum Tab Milenge<br>
            Lekin Ek Shart Par,<br>
            Naa ghadi Tum Pehenogi,<br>
            Na Waqt Hum Dekhnege ❤💕❤
        </div>
    </div>

    <script>
        function moveNoButton() {
            const noBtn = document.getElementById('noBtn');
            const maxX = window.innerWidth - noBtn.offsetWidth;
            const maxY = window.innerHeight - noBtn.offsetHeight;
            
            const newX = Math.random() * maxX;
            const newY = Math.random() * maxY;
            
            noBtn.style.position = 'fixed';
            noBtn.style.left = newX + 'px';
            noBtn.style.top = newY + 'px';
            noBtn.style.transform = 'translate(-50%, -50%)';
            noBtn.style.zIndex = '100';
            
            const moves = noBtn.getAttribute('data-moves') || 0;
            if (moves > 2) {
                noBtn.style.opacity = '0';
                noBtn.style.pointerEvents = 'none';
            } else {
                noBtn.setAttribute('data-moves', parseInt(moves) + 1);
            }
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = ['💖', '💕', '💗', '❤️', '💝'][Math.floor(Math.random() * 5)];
            heart.style.left = Math.random() * 100 + '%';
            heart.style.animationDuration = (Math.random() * 2 + 2) + 's';
            document.getElementById('hearts').appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 5000);
        }

        function showHeartsAndSecret() {
            document.getElementById('mainPage').style.opacity = '0';
            document.getElementById('mainPage').style.transform = 'scale(0.8)';
            
            for (let i = 0; i < 30; i++) {
                setTimeout(createHeart, i * 100);
            }
            
            setTimeout(() => {
                document.getElementById('secretPage').classList.add('active');
                document.body.style.overflow = 'auto';
            }, 2000);
        }

        document.addEventListener('contextmenu', e => e.preventDefault());
        document.addEventListener('keydown', e => {
            if (e.key === 'F12' || (e.ctrlKey && e.shiftKey && e.key === 'I')) {
                e.preventDefault();
            }
        });
    </script>
</body>
</html>
