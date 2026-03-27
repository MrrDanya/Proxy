<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Telegram Proxy</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background: #0f172a;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        button {
            background: #3b82f6;
            border: none;
            padding: 16px 48px;
            font-size: 18px;
            font-weight: 600;
            color: white;
            border-radius: 12px;
            cursor: pointer;
            transition: 0.2s;
            font-family: system-ui, sans-serif;
        }

        button:hover {
            background: #2563eb;
            transform: scale(1.02);
        }
    </style>
</head>
<body>
    <button id="connectBtn">Подключить</button>

    <script>
        const PROXY_URL = "tg://proxy?server=77.221.140.46&port=8443&secret=7lGCP4KcxEDl19RqQ4-5fxR2a3ZkMzMxLm9rY2RuLnJ1";

        document.getElementById('connectBtn').addEventListener('click', () => {
            window.location.href = PROXY_URL;
            
            // Если не открылось через 2 секунды, показываем подсказку
            setTimeout(() => {
                if (document.hidden === false) {
                    alert('Если Telegram не открылся автоматически, скопируйте ссылку и вставьте в Telegram:\n\n' + PROXY_URL);
                }
            }, 2000);
        });
    </script>
</body>
</html>
