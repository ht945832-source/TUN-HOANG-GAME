<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>HOANGDZ TUN - PREMUM SLIDER</title>
    <style>
        :root {
            --red: #ff0000;
            --black: #000000;
            --glass: rgba(20, 20, 20, 0.9);
        }

        * {
            box-sizing: border-box;
            touch-action: manipulation;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--black);
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            font-family: 'Courier New', Courier, monospace;
        }

        /* Nền hiệu ứng */
        #bg {
            position: fixed;
            width: 100%; height: 100%;
            background: linear-gradient(135deg, #1a0000 0%, #000 100%);
            z-index: -1;
        }

        /* Panel chính */
        .panel {
            width: 360px;
            height: 600px;
            background: var(--glass);
            border: 2px solid var(--red);
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            box-shadow: 0 0 40px rgba(255, 0, 0, 0.4);
            position: relative;
            backdrop-filter: blur(10px);
        }

        .header {
            padding: 15px;
            text-align: center;
            border-bottom: 2px solid var(--red);
            text-shadow: 0 0 10px var(--red);
        }

        h1 { margin: 0; color: #fff; font-size: 22px; letter-spacing: 3px; }

        /* Vùng cuộn mượt */
        .scroll-area {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
        }

        .scroll-area::-webkit-scrollbar { width: 0px; }

        /* Block chức năng */
        .card {
            background: rgba(40, 40, 40, 0.5);
            margin-bottom: 15px;
            padding: 15px;
            border-radius: 12px;
            border-left: 5px solid var(--red);
        }

        .row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        /* Thanh trượt Slider cực chất */
        .slider-container { margin-top: 10px; }
        
        .slider {
            -webkit-appearance: none;
            width: 100%;
            height: 6px;
            background: #333;
            border-radius: 5px;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 18px;
            height: 18px;
            background: var(--red);
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 0 10px var(--red);
        }

        .val-display {
            color: var(--red);
            font-weight: bold;
            font-size: 14px;
        }

        /* Toggle Button */
        .toggle {
            width: 44px; height: 22px;
            background: #444;
            border-radius: 20px;
            position: relative;
            transition: 0.3s;
        }

        .toggle::after {
            content: '';
            position: absolute;
            width: 16px; height: 16px;
            background: #fff;
            border-radius: 50%;
            top: 3px; left: 3px;
            transition: 0.3s;
        }

        .on { background: var(--red); box-shadow: 0 0 10px var(--red); }
        .on::after { left: 25px; }

        /* Thông báo */
        .toast {
            position: fixed;
            top: 10%;
            background: #fff;
            color: #000;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            box-shadow: 0 0 20px var(--red);
            z-index: 100;
            animation: slideDown 0.4s ease;
        }

        @keyframes slideDown {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .footer {
            padding: 10px;
            font-size: 10px;
            color: #777;
            text-align: center;
            border-top: 1px solid #333;
        }
    </style>
</head>
<body>

<div id="bg"></div>

<div class="panel">
    <div class="header">
        <h1>HOANGDZ TUN 🎯</h1>
    </div>

    <div class="scroll-area">
        <div class="card">
            <div class="row">
                <span>ĐỘ NHẠY TỔNG 🚀</span>
                <span class="val-display" id="v1">50%</span>
            </div>
            <input type="range" class="slider" oninput="updateVal('v1', this.value)" value="50">
        </div>

        <div class="card">
            <div class="row">
                <span>GIA TỐC ẢO ⚡</span>
                <span class="val-display" id="v2">80%</span>
            </div>
            <input type="range" class="slider" oninput="updateVal('v2', this.value)" value="80">
        </div>

        <div class="card" onclick="toggleBtn(this, 'Nhẹ Tâm')">
            <div class="row">
                <span>NHẸ TÂM 🎯</span>
                <div class="toggle"></div>
            </div>
        </div>

        <div class="card" onclick="toggleBtn(this, 'Đầm Tâm')">
            <div class="row">
                <span>ĐẦM TÂM 🎯</span>
                <div class="toggle"></div>
            </div>
        </div>

        <div class="card" onclick="toggleBtn(this, 'Aimlock Pro')">
            <div class="row">
                <span>AIMLOCK PRO 🔒</span>
                <div class="toggle"></div>
            </div>
        </div>

        <div class="card" onclick="toggleBtn(this, 'Bypass System')">
            <div class="row">
                <span>BYPASS SYSTEM 🛠️</span>
                <div class="toggle"></div>
            </div>
        </div>

        <div class="card" onclick="toggleBtn(this, 'Antiban VIP')">
            <div class="row">
                <span>ANTIBAN VIP 🛡️</span>
                <div class="toggle"></div>
            </div>
        </div>
    </div>

    <div class="footer">
        PHÁT TRIỂN BỞI HOANGDZ TUN <br>
        PHIÊN BẢN CỰC VIP - KHÔNG PHÓNG TO
    </div>
</div>

<audio id="tingSound" src="https://www.soundjay.com/buttons/sounds/button-10.mp3"></audio>

<script>
    // Hiệu ứng hạt rơi (Tuyết & Icon)
    function createSnow() {
        const icons = ['❄️', '🎯', '🔥', '💎'];
        const el = document.createElement('div');
        el.innerText = icons[Math.floor(Math.random() * icons.length)];
        el.style.position = 'fixed';
        el.style.top = '-20px';
        el.style.left = Math.random() * 100 + 'vw';
        el.style.fontSize = '15px';
        el.style.color = 'rgba(255,0,0,0.5)';
        el.style.transition = 'transform 4s linear, opacity 4s';
        document.body.appendChild(el);

        setTimeout(() => {
            el.style.transform = `translateY(${window.innerHeight + 20}px) rotate(360deg)`;
            el.style.opacity = '0';
        }, 100);
        setTimeout(() => el.remove(), 4500);
    }
    setInterval(createSnow, 400);

    // Cập nhật giá trị Slider
    function updateVal(id, val) {
        document.getElementById(id).innerText = val + '%';
    }

    // Bật tắt nút
    function toggleBtn(card, name) {
        const t = card.querySelector('.toggle');
        const audio = document.getElementById('tingSound');
        
        t.classList.toggle('on');
        
        if(t.classList.contains('on')) {
            audio.currentTime = 0;
            audio.play();
            showToast("KÍCH HOẠT: " + name);
            if(navigator.vibrate) navigator.vibrate(50);
        }
    }

    function showToast(msg) {
        const toast = document.createElement('div');
        toast.className = 'toast';
        toast.innerText = msg;
        document.body.appendChild(toast);
        setTimeout(() => {
            toast.style.opacity = '0';
            setTimeout(() => toast.remove(), 500);
        }, 1500);
    }

    // Chặn zoom 
    document.addEventListener('touchstart', (e) => {
        if (e.touches.length > 1) e.preventDefault();
    }, {passive: false});
</script>

</body>
</html>
