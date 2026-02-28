# Young Mi's Quarter century.
[index.html](https://github.com/user-attachments/files/25620074/index.html)
<!DOCTYPE html>
<html>
<head>
    <title>Countdown to March 2 - 10AM AEST</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 100px;
            background-color: #f4f4f4;
        }

        #countdown {
            font-size: 40px;
            margin-bottom: 30px;
        }

        #hiddenContent {
            display: none;
            font-size: 28px;
            color: green;
        }
    </style>
</head>
<body>

    <h1>Countdown</h1>
    <div id="countdown"></div>

    <div id="hiddenContent">
        🎉 It's 10AM AEST on March 2! Your content is now live!
    </div>

    <script>
        // March 2 at 10:00 AM AEST (UTC+10)
        // Change the year if needed
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
