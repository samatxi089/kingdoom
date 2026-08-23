<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KINGDOOM</title>
    <!-- FontAwesome icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            background: url('https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=1920&auto=format&fit=crop') no-repeat center center fixed;
            background-size: cover;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #fff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding: 20px;
            overflow-x: hidden;
            position: relative;
        }
        /* Overlay to darken background */
        body::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(10, 25, 47, 0.75);
            z-index: -1;
        }

        /* Snow effect */
        .snowflake {
            position: fixed;
            top: -10px;
            z-index: 9999;
            user-select: none;
            cursor: default;
            animation: fall linear infinite;
            color: #fff;
            opacity: 0.8;
        }
        @keyframes fall {
            0% { transform: translateY(-10px) translateX(0); }
            100% { transform: translateY(105vh) translateX(20px); }
        }

        /* Rotating Disc Header */
        .header-container {
            position: relative;
            width: 160px;
            height: 160px;
            margin-top: 20px;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .vinyl-disc {
            position: absolute;
            width: 160px;
            height: 160px;
            background: #111;
            border-radius: 50%;
            box-shadow: 0 0 20px rgba(0, 150, 255, 0.4);
            animation: rotateDisk 4s linear infinite;
            border: 4px solid #222;
            background-image: repeating-radial-gradient(#111, #111 4px, #222 5px, #111 6px);
        }
        .vinyl-disc::after {
            content: '';
            position: absolute;
            top: 60px; left: 60px;
            width: 40px; height: 40px;
            background: #00bcd4;
            border-radius: 50%;
            border: 3px solid #fff;
        }
        @keyframes rotateDisk {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .kingdom-logo {
            position: relative;
            z-index: 2;
            width: 120px;
            filter: drop-shadow(0 0 10px rgba(0, 188, 212, 0.8));
        }

        /* Links Container */
        .links-container {
            width: 100%;
            max-width: 420px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            z-index: 2;
            margin-bottom: 30px;
        }
        .link-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            padding: 12px 18px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            text-decoration: none;
            color: #fff;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }
        .link-card:hover {
            background: rgba(255, 255, 255, 0.18);
            transform: translateY(-3px);
            border-color: #00bcd4;
            box-shadow: 0 6px 20px rgba(0, 188, 212, 0.3);
        }
        .link-content {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: bold;
            font-size: 16px;
        }
        .link-content i {
            font-size: 24px;
            width: 30px;
            text-align: center;
        }
        /* Specific app colors */
        .fa-discord { color: #5865F2; }
        .fa-instagram { color: #E1306C; }
        .fa-snapchat { color: #FFFC00; }
        .fa-tiktok { color: #ff0050; }

        .btn-visit {
            background: #00bcd4;
            color: #0a192f;
            padding: 6px 14px;
            border-radius: 8px;
            font-size: 13px;
            font-weight: bold;
            transition: background 0.2s;
        }
        .link-card:hover .btn-visit {
            background: #fff;
        }

        /* Warning Message */
        .warning-box {
            background: rgba(255, 193, 7, 0.15);
            border: 1px solid rgba(255, 193, 7, 0.4);
            color: #ffc107;
            padding: 12px;
            border-radius: 10px;
            text-align: center;
            font-size: 14px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-class: center;
            gap: 8px;
            justify-content: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        /* Music player background audio trigger info */
        .music-info {
            font-size: 12px;
            color: #aaa;
            margin-top: 10px;
            text-align: center;
        }
    </style>
</head>
<body>

    <!-- Background Audio (Replace source with your music link if needed) -->
    <audio id="bg-music" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mp3">
    </audio>

    <!-- Click sound effect -->
    <audio id="click-sound" src="https://assets.mixkit.co/active_storage/sfx/2571/2571-preview.mp3"></audio>

    <!-- Rotating Vinyl Disc + Kingdom Logo -->
    <div class="header-container" onclick="toggleAudio()">
        <div class="vinyl-disc"></div>
        <img src="https://api.iconify.design/fluent-emoji-flat:crown.svg" alt="KINGDOOM" class="keyword-icon kingdom-logo" style="width: 80px;">
    </div>
    <div class="music-info">🎵 Click the crown/disc to play background music</div>
    <br>

    <!-- Links List -->
    <div class="links-container">
        
        <!-- Discord -->
        <a href="https://discord.com" class="link-card" target="_blank" onclick="playClickSound(event, this)">
            <div class="link-content">
                <i class="fa-brands fa-discord"></i>
                <span>KINGDOM Official Discord</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Instagram Community Group -->
        <a href="https://instagram.com" class="link-card" target="_blank" onclick="playClickSound(event, this)">
            <div class="link-content">
                <i class="fa-brands fa-instagram"></i>
                <span>KINGDOM Community Group</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Warning Box -->
        <div class="warning-box">
            <i class="fa-solid fa-triangle-exclamation"></i>
            <span>WARNING: إذا مamadmech اللينك، صيفطو في الكومنتيرات أو خاص للحساب!</span>
        </div>

        <!-- Personal Account -->
        <a href="https://instagram.com" class="link-card" target="_blank" onclick="playClickSound(event, this)">
            <div class="link-content">
                <i class="fa-brands fa-instagram"></i>
                <span>Hassan's Personal Account (الحساب الشخصي)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Snapchat -->
        <a href="https://snapchat.com" class="link-card" target="_blank" onclick="playClickSound(event, this)">
            <div class="link-content">
                <i class="fa-brands fa-snapchat"></i>
                <span>Hassan's Snapchat (سناب شات)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- TikTok -->
        <a href="https://tiktok.com" class="link-card" target="_blank" onclick="playClickSound(event, this)">
            <div class="link-content">
                <i class="fa-brands fa-tiktok"></i>
                <span>Hassan's TikTok (تيك توك)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

    </div>

    <script>
        // Snow Effect Generation
        function createSnowflake() {
            const snow = document.createElement('div');
            snow.classList.add('snowflake');
            snow.innerHTML = '❄';
            snow.style.left = Math.random() * window.innerWidth + 'px';
            snow.style.top = '-20px';
            snow.style.fontSize = (Math.random() * 10 + 10) + 'px';
            snow.style.animationDuration = (Math.random() * 3 + 2) + 's';
            snow.style.opacity = Math.random();
            document.body.appendChild(snow);

            setTimeout(() => {
                snow.remove();
            }, 5000);
        }
        setInterval(createSnowflake, 150);

        // Audio Toggle & Click Sound
        let musicPlaying = false;
        function toggleAudio() {
            const music = document.getElementById('bg-music');
            if (!musicPlaying) {
                music.play();
                musicPlaying = true;
                document.querySelector('.music-info').innerText = "🎵 Music Playing (Click to pause)";
            } else {
                music.pause();
                musicPlaying = false;
                document.querySelector('.music-info').innerText = "🎵 Click the crown/disc to play background music";
            }
        }

        function playClickSound(event, element) {
            const clickAudio = document.getElementById('click-sound');
            clickAudio.currentTime = 0;
            clickAudio.play().catch(e => console.log(e));
        }
    </script>
</body>
</html>
