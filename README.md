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
        /* Dark blue overlay */
        body::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(5, 15, 30, 0.88);
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
            color: #cce7ff;
            opacity: 0.7;
        }
        @keyframes fall {
            0% { transform: translateY(-10px) translateX(0); }
            100% { transform: translateY(105vh) translateX(15px); }
        }

        /* Rotating Disc Header in Center */
        .header-container {
            position: relative;
            width: 170px;
            height: 170px;
            margin: 25px auto 10px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }
        .vinyl-disc {
            position: absolute;
            width: 170px;
            height: 170px;
            background: #111;
            border-radius: 50%;
            box-shadow: 0 0 30px rgba(0, 150, 255, 0.7);
            animation: rotateDisk 4s linear infinite;
            border: 3px solid #00bcd4;
            background-image: repeating-radial-gradient(#111, #111 4px, #1a2a3a 5px, #111 6px);
        }
        @keyframes rotateDisk {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .kingdom-center-logo {
            position: relative;
            z-index: 2;
            width: 95px;
            height: 95px;
            object-fit: contain;
            filter: drop-shadow(0 0 8px rgba(0, 210, 255, 0.8));
            border-radius: 50%;
        }
        .music-info {
            font-size: 12px;
            color: #8ab4f8;
            margin-bottom: 25px;
            text-align: center;
            font-weight: bold;
        }

        /* Links Container */
        .links-container {
            width: 100%;
            max-width: 400px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            z-index: 2;
            margin-bottom: 20px;
        }
        .link-card {
            background: rgba(15, 30, 55, 0.65);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(0, 188, 212, 0.3);
            padding: 12px 16px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            text-decoration: none;
            color: #fff;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }
        .link-card:hover {
            background: rgba(0, 188, 212, 0.15);
            transform: translateY(-3px);
            border-color: #00bcd4;
            box-shadow: 0 6px 20px rgba(0, 188, 212, 0.4);
        }
        .link-content {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
            font-size: 15px;
        }
        .link-content i {
            font-size: 22px;
            width: 28px;
            text-align: center;
        }
        
        /* App Colors */
        .fa-discord { color: #5865F2; }
        .fa-instagram { color: #E1306C; }
        .fa-snapchat { color: #FFFC00; }
        .fa-tiktok { color: #00f2fe; }

        .btn-visit {
            background: #00bcd4;
            color: #050f1e;
            padding: 5px 12px;
            border-radius: 8px;
            font-size: 12px;
            font-weight: bold;
            transition: all 0.2s;
        }
        .link-card:hover .btn-visit {
            background: #fff;
            color: #00bcd4;
        }

        /* Warning Message Box */
        .warning-box {
            background: rgba(255, 165, 0, 0.12);
            border: 1px solid rgba(255, 165, 0, 0.4);
            color: #ffb703;
            padding: 10px 14px;
            border-radius: 12px;
            text-align: center;
            font-size: 13px;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            margin: 5px 0;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
        }
    </style>
</head>
<body>

    <!-- Audio Elements -->
    <audio id="bg-music" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mp3">
    </audio>
    <audio id="click-sound" src="https://assets.mixkit.co/active_storage/sfx/2571/2571-preview.mp3"></audio>

    <!-- Header Rotating Disk with Kingdom Logo Inside -->
    <div class="header-container" onclick="toggleAudio()">
        <div class="vinyl-disc"></div>
        <!-- Logo li sifti f tswira -->
        <img src="https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=400&auto=format&fit=crop" alt="KINGDOM" class="kingdom-center-logo" id="logo-img">
    </div>
    
    <div class="music-info">🎵 اضغط على القرص لتشغيل الموسيقى الخلفية</div>

    <!-- Links List -->
    <div class="links-container">
        
        <!-- Discord -->
        <a href="https://discord.com" class="link-card" target="_blank" onclick="playClickSound()">
            <div class="link-content">
                <i class="fa-brands fa-discord"></i>
                <span>KINGDOM Official Discord</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Instagram Main -->
        <a href="https://instagram.com" class="link-card" target="_blank" onclick="playClickSound()">
            <div class="link-content">
                <i class="fa-brands fa-instagram"></i>
                <span>KINGDOM Instagram (Main)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Instagram Community Group -->
        <a href="https://instagram.com" class="link-card" target="_blank" onclick="playClickSound()">
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
        <a href="https://instagram.com" class="link-card" target="_blank" onclick="playClickSound()">
            <div class="link-content">
                <i class="fa-brands fa-instagram"></i>
                <span>Hassan's Personal Account (الحساب الشخصي)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- Snapchat -->
        <a href="https://snapchat.com" class="link-card" target="_blank" onclick="playClickSound()">
            <div class="link-content">
                <i class="fa-brands fa-snapchat"></i>
                <span>Hassan's Snapchat (سناب شات)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

        <!-- TikTok -->
        <a href="https://tiktok.com" class="link-card" target="_blank" onclick="playClickSound()">
            <div class="link-content">
                <i class="fa-brands fa-tiktok"></i>
                <span>Hassan's TikTok (تيك توك)</span>
            </div>
            <div class="btn-visit">Visit</div>
        </a>

    </div>

    <script>
        // Snow Effect
        function createSnowflake() {
            const snow = document.createElement('div');
            snow.classList.add('snowflake');
            snow.innerHTML = '❄';
            snow.style.left = Math.random() * window.innerWidth + 'px';
            snow.style.top = '-20px';
            snow.style.fontSize = (Math.random() * 8 + 8) + 'px';
            snow.style.animationDuration = (Math.random() * 3 + 2) + 's';
            snow.style.opacity = Math.random() * 0.7 + 0.3;
            document.body.appendChild(snow);

            setTimeout(() => { snow.remove(); }, 5000);
        }
        setInterval(createSnowflake, 180);

        // Music Toggle
        let musicPlaying = false;
        function toggleAudio() {
            const music = document.getElementById('bg-music');
            if (!musicPlaying) {
                music.play();
                musicPlaying = true;
                document.querySelector('.music-info').innerText = "🎵 الموسيقى شغالة (اضغط للإيقاف)";
            } else {
                music.pause();
                musicPlaying = false;
                document.querySelector('.music-info').innerText = "🎵 اضغط على القرص لتشغيل الموسيقى الخلفية";
            }
        }

        // Click Sound Effect for Links
        function playClickSound() {
            const clickAudio = document.getElementById('click-sound');
            clickAudio.currentTime = 0;
            clickAudio.play().catch(e => console.log(e));
        }
    </script>
</body>
</html>
