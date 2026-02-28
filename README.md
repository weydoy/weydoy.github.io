[Amy.html](https://github.com/user-attachments/files/25620217/Amy.html)
<!DOCTYPE html>
<html>
<head>
    <title>Young Mi's Quarter of a Century</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            background: linear-gradient(to bottom, #dff6ff, #f4fff4);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            overflow-x: hidden;
        }

        h1 {
            margin-bottom: 10px;
        }

        #countdown {
            font-size: 36px;
            margin-bottom: 20px;
        }

        #hiddenContent {
            display: none;
            font-size: 26px;
            color: #2e7d32;
            margin-top: 20px;
        }

        /* Frog bottom left */
        .frog-container {
            position: fixed;
            bottom: 0;
            left: 20px;
        }

        /* Mouse bottom right */
        .mouse-container {
            position: fixed;
            bottom: 0;
            right: 20px;
        }

        /* Balloon floating */
        @keyframes float {
            0%   { transform: translateY(0px); }
            50%  { transform: translateY(-12px); }
            100% { transform: translateY(0px); }
        }

        .balloon {
            animation: float 3s ease-in-out infinite;
            transform-origin: center;
        }

        /* Blinking */
        @keyframes blink {
            0%, 90%, 100% { transform: scaleY(1); }
            95% { transform: scaleY(0.1); }
        }

        .eye {
            transform-origin: center;
            animation: blink 4s infinite;
        }

        /* Mouse nibble animation */
        @keyframes nibble {
            0%, 100% { transform: rotate(0deg); }
            50% { transform: rotate(-5deg); }
        }

        .mouse-head {
            transform-origin: 60% 60%;
            animation: nibble 1.5s infinite ease-in-out;
        }

    </style>
</head>
<body>

    <h1>Young Mi's Quarter of a Century</h1>
    <div id="countdown"></div>

    <div id="hiddenContent">
        🎉 It's 10AM AEST on March 2! Surprise unlocked!
    </div>

    <!-- Frog -->
    <div class="frog-container">
        <svg width="220" height="300" viewBox="0 0 220 300">

            <g class="balloon">
                <line x1="150" y1="60" x2="150" y2="160" stroke="#555" stroke-width="2"/>
                <ellipse cx="150" cy="40" rx="35" ry="45" fill="#ff6b81"/>
                <polygon points="145,85 155,85 150,95" fill="#ff6b81"/>
            </g>

            <ellipse cx="110" cy="200" rx="70" ry="60" fill="#66bb6a"/>
            <ellipse cx="110" cy="215" rx="40" ry="35" fill="#a5d6a7"/>

            <circle cx="80" cy="130" r="20" fill="#66bb6a"/>
            <circle cx="140" cy="130" r="20" fill="#66bb6a"/>

            <g class="eye">
                <circle cx="80" cy="130" r="10" fill="white"/>
                <circle cx="80" cy="130" r="5" fill="black"/>
            </g>

            <g class="eye">
                <circle cx="140" cy="130" r="10" fill="white"/>
                <circle cx="140" cy="130" r="5" fill="black"/>
            </g>

            <path d="M75 165 Q110 190 145 165"
                  stroke="#2e7d32"
                  stroke-width="4"
                  fill="transparent"/>

            <path d="M150 190 Q170 170 150 160"
                  stroke="#66bb6a"
                  stroke-width="10"
                  fill="transparent"
                  stroke-linecap="round"/>
        </svg>
    </div>

    <!-- Mouse -->
    <div class="mouse-container">
        <svg width="220" height="200" viewBox="0 0 220 200">

            <!-- Cheese -->
            <polygon points="120,140 190,120 190,170 120,170"
                     fill="#ffd54f"/>
            <circle cx="150" cy="150" r="8" fill="#fbc02d"/>
            <circle cx="170" cy="160" r="6" fill="#fbc02d"/>

            <!-- Mouse body -->
            <ellipse cx="80" cy="150" rx="50" ry="35" fill="#b0bec5"/>

            <!-- Tail -->
            <path d="M30 155 Q10 140 25 120"
                  stroke="#90a4ae"
                  stroke-width="4"
                  fill="transparent"/>

            <!-- Head (animated) -->
            <g class="mouse-head">
                <ellipse cx="110" cy="140" rx="30" ry="25" fill="#b0bec5"/>
                <circle cx="120" cy="135" r="4" fill="black"/>
                <circle cx="95" cy="120" r="12" fill="#cfd8dc"/>
                <circle cx="115" cy="120" r="12" fill="#cfd8dc"/>
            </g>

        </svg>
    </div>

    <script>
        const targetDate = new Date("March 2, 2026 10:00:00 GMT+10:00").getTime();

        const countdownElement = document.getElementById("countdown");
        const hiddenContent = document.getElementById("hiddenContent");

        const timer = setInterval(function() {
            const now = new Date().getTime();
            const distance = targetDate - now;

            if (distance <= 0) {
                clearInterval(timer);
                countdownElement.style.display = "none";
                hiddenContent.style.display = "block";
                return;
            }

            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            countdownElement.innerHTML =
                days + "d " +
                hours + "h " +
                minutes + "m " +
                seconds + "s ";
        }, 1000);
    </script>

</body>
</html>
