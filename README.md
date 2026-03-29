<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>10 Telegram Прокси</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: system-ui, -apple-system, sans-serif;
            padding: 20px;
        }

        .container {
            display: flex;
            flex-direction: column;
            width: 100%;
            max-width: 400px;
        }

        .info-text {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 16px;
            margin-bottom: 20px;
            text-align: center;
            color: white;
            border: 1px solid rgba(255,255,255,0.2);
        }

        .info-text p {
            margin: 8px 0;
            font-size: 14px;
            line-height: 1.4;
        }

        .info-text p:first-child {
            font-weight: bold;
            font-size: 16px;
            margin-bottom: 12px;
        }

        .info-text p:last-child {
            color: #fbbf24;
            font-size: 13px;
        }

        .buttons-wrapper {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 16px;
            width: 100%;
        }

        .column {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        button {
            background: #3b82f6;
            border: none;
            padding: 14px 0;
            font-size: 16px;
            font-weight: 600;
            color: white;
            border-radius: 12px;
            cursor: pointer;
            transition: 0.2s;
            font-family: system-ui, sans-serif;
            width: 100%;
            text-align: center;
        }

        button:hover {
            background: #2563eb;
            transform: scale(1.02);
        }

        button:active {
            transform: scale(0.98);
        }

        .qr-section {
            margin-top: 24px;
            text-align: center;
        }

        .qr-container {
            background: white;
            padding: 16px;
            border-radius: 20px;
            display: inline-block;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .qr-container canvas {
            display: block;
            margin: 0 auto;
            border-radius: 12px;
        }

        .qr-text {
            margin-top: 12px;
            color: #94a3b8;
            font-size: 12px;
            word-break: break-all;
        }

        .qr-text a {
            color: #60a5fa;
            text-decoration: none;
        }

        .qr-text a:hover {
            text-decoration: underline;
        }

        .share-btn {
            margin-top: 12px;
            background: #22c55e;
            border: none;
            padding: 10px 20px;
            font-size: 14px;
            font-weight: 600;
            color: white;
            border-radius: 40px;
            cursor: pointer;
            transition: 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .share-btn:hover {
            background: #16a34a;
            transform: scale(1.02);
        }

        @media (max-width: 480px) {
            .buttons-wrapper {
                gap: 12px;
            }
            .column {
                gap: 10px;
            }
            button {
                padding: 12px 0;
                font-size: 14px;
            }
            .info-text {
                padding: 12px;
                margin-bottom: 16px;
            }
            .info-text p {
                font-size: 12px;
            }
            .info-text p:first-child {
                font-size: 14px;
            }
            .qr-container {
                padding: 12px;
            }
            .qr-container canvas {
                width: 140px;
                height: 140px;
            }
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js"></script>
</head>
<body>
    <div class="container">
        <div class="info-text">
            <p>Выберите один из прокси-серверов</p>
            <p>Если один не работает, попробуйте другой</p>
        </div>
        <div class="buttons-wrapper">
            <div class="column" id="leftColumn"></div>
            <div class="column" id="rightColumn"></div>
        </div>

        <div class="qr-section">
            <div class="qr-container">
                <div id="qrcode"></div>
            </div>
            <div class="qr-text">
                <p>тсканируйте QR-код, чтобы поделиться сайтом с другом</p>
                <p><a href="https://mrrdanya.github.io/Proxy/" target="_blank">https://mrrdanya.github.io/Proxy/</a></p>
            </div>
            <button class="share-btn" id="shareBtn">
                скопировать ссылку
            </button>
        </div>
    </div>

    <script>
        // Ссылка на сайт
        const siteUrl = "https://mrrdanya.github.io/Proxy/";
        
        // Генерация QR-кода
        new QRCode(document.getElementById("qrcode"), {
            text: siteUrl,
            width: 160,
            height: 160,
            colorDark: "#000000",
            colorLight: "#ffffff",
            correctLevel: QRCode.CorrectLevel.H
        });

        // Кнопка "Поделиться"
        document.getElementById('shareBtn').addEventListener('click', async () => {
            if (navigator.share) {
                try {
                    await navigator.share({
                        title: 'Telegram Прокси',
                        text: 'Прокси для Telegram, если один не работает -- попробуй другой',
                        url: siteUrl
                    });
                } catch (err) {
                    console.log('Отменено или ошибка:', err);
                }
            } else {
                // Если Web Share API не поддерживается, копируем в буфер
                try {
                    await navigator.clipboard.writeText(siteUrl);
                    const btn = document.getElementById('shareBtn');
                    const originalText = btn.innerHTML;
                    btn.innerHTML = '✅ Ссылка скопирована!';
                    setTimeout(() => {
                        btn.innerHTML = originalText;
                    }, 2000);
                } catch (err) {
                    alert('Не удалось скопировать ссылку. Скопируйте вручную: ' + siteUrl);
                }
            }
        });

        // ============================================
        // ВАШИ 10 ПРОКСИ
        // ============================================
        const proxies = [
            "tg://proxy?server=77.221.140.46&port=8443&secret=7lGCP4KcxEDl19RqQ4-5fxR2a3ZkMzMxLm9rY2RuLnJ1",
            "tg://proxy?server=213.219.212.245&port=443&secret=9f3c7a8d2e4b1c6f5a7d8e9b0c2f4a1d",
            "tg://proxy?server=37.139.34.153&port=443&secret=9f3c7a8d2e4b1c6f5a7d8e9b0c2f4a1d",
            "tg://proxy?server=37.139.32.18&port=443&secret=9f3c7a8d2e4b1c6f5a7d8e9b0c2f4a1d",
            "tg://proxy?server=146.185.242.117&port=443&secret=9f3c7a8d2e4b1c6f5a7d8e9b0c2f4a1d",
            "tg://proxy?server=146.185.209.244&port=443&secret=9f3c7a8d2e4b1c6f5a7d8e9b0c2f4a1d",
            "tg://proxy?server=he.65.mtproto.ru&port=443&secret=ee2111222233334444555566667777888862726f777365722e79616e6465782e636f6d",
            "tg://proxy?server=he.17.mtproto.ru&port=443&secret=ee2111222233334444555566667777888862726f777365722e79616e6465782e636f6d",
            "tg://proxy?server=he.17.mtproto.ru&port=443&secret=ee2111222233334444555566667777888862726f777365722e79616e6465782e636f6d",
            "tg://proxy?server=he.108.mtproto.ru&port=443&secret=ee2111222233334444555566667777888862726f777365722e79616e6465782e636f6d"
        ];

        const leftColumn = document.getElementById('leftColumn');
        const rightColumn = document.getElementById('rightColumn');

        proxies.forEach((proxy, index) => {
            const button = document.createElement('button');
            button.textContent = `Прокси ${index + 1}`;
            button.addEventListener('click', () => {
                window.location.href = proxy;
                console.log(`Прокси ${index + 1} активирована:`, proxy);
            });
            
            if (index < 5) {
                leftColumn.appendChild(button);
            } else {
                rightColumn.appendChild(button);
            }
        });
    </script>
</body>
</html>
