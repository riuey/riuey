<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple CAPTCHA</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }

        .captcha-container {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }

        .captcha-text {
            font-size: 24px;
            letter-spacing: 3px;
            background-color: #000000;
            color: #ffffff;
            display: inline-block;
            padding: 10px 20px;
            border-radius: 5px;
            user-select: none;
            margin-bottom: 20px;
        }

        .captcha-input {
            font-size: 16px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            width: 80%;
        }

        .captcha-button {
            background-color: #28a745;
            color: #ffffff;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }

        .captcha-button:hover {
            background-color: #218838;
        }

        .captcha-message {
            margin-top: 20px;
            font-size: 16px;
            color: #d9534f;
        }
    </style>
</head>
<body>
    <div class="captcha-container">
        <div id="captcha" class="captcha-text"></div>
        <input type="text" id="captcha-input" class="captcha-input" placeholder="Enter CAPTCHA" />
        <button class="captcha-button" onclick="validateCaptcha()">Submit</button>
        <div id="captcha-message" class="captcha-message"></div>
    </div>

    <script>
        let captchaCode;

        function generateCaptcha() {
            captchaCode = '';
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            for (let i = 0; i < 6; i++) {
                captchaCode += characters.charAt(Math.floor(Math.random() * characters.length));
            }
            document.getElementById('captcha').innerText = captchaCode;
        }

        function validateCaptcha() {
            const userCaptcha = document.getElementById('captcha-input').value;
            const messageElement = document.getElementById('captcha-message');

            if (userCaptcha === captchaCode) {
                messageElement.style.color = 'green';
                messageElement.innerText = 'CAPTCHA Verified!';
            } else {
                messageElement.style.color = 'red';
                messageElement.innerText = 'Incorrect CAPTCHA. Please try again.';
                generateCaptcha(); // Regenerate CAPTCHA for new attempt
                document.getElementById('captcha-input').value = '';
            }
        }

        // Generate CAPTCHA when page loads
        window.onload = generateCaptcha;
    </script>
</body>
</html>
