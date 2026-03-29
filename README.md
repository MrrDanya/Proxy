<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Telegram Прокси</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}

body{
    min-height:100vh;
    background:linear-gradient(135deg,#052e16,#064e3b);
    display:flex;
    align-items:center;
    justify-content:center;
    font-family:system-ui;
    color:#fff;
    padding:20px;
}

.container{max-width:500px;width:100%}

.info{
    background:rgba(255,255,255,.08);
    border:1px solid rgba(34,197,94,.3);
    padding:16px;
    border-radius:18px;
    text-align:center;
    margin-bottom:20px;
}

/* ===== TOGGLE ===== */

.toggle{
    width:100%;
    height:50px;
    background:#022c22;
    border-radius:30px;
    position:relative;
    margin-bottom:20px;
    cursor:pointer;
}

.toggle-circle{
    width:50%;
    height:100%;
    background:#22c55e;
    border-radius:30px;
    position:absolute;
    top:0;
    left:0;
    transition:.3s;
}

.toggle.active .toggle-circle{
    left:50%;
}

.toggle-labels{
    position:absolute;
    width:100%;
    height:100%;
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:0 20px;
    font-weight:600;
    pointer-events:none;
}

/* ===== GRID ===== */

.grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:10px;
    margin-bottom:20px;
}

button.proxy{
    background:#16a34a;
    border:none;
    padding:12px;
    border-radius:12px;
    color:#fff;
    font-weight:600;
    cursor:pointer;
    transition:.2s;
}

button.proxy:hover{
    background:#22c55e;
    transform:scale(1.03);
}

/* ===== SHARE ===== */

.share-btn{
    width:100%;
    background:#22c55e;
    border:none;
    padding:14px;
    border-radius:14px;
    font-size:16px;
    font-weight:600;
    color:#fff;
    cursor:pointer;
    transition:.2s;
}

.share-btn:hover{
    background:#4ade80;
    transform:scale(1.02);
}

</style>
</head>

<body>
<div class="container">

<div class="info">
🔐 Выберите прокси<br>
💡 Если не работает — попробуйте другой
</div>

<!-- TOGGLE -->
<div class="toggle" id="toggle" onclick="switchPage()">
    <div class="toggle-circle"></div>
    <div class="toggle-labels">
        <span>1</span>
        <span>2</span>
    </div>
</div>

<div class="grid" id="grid"></div>

<button class="share-btn" onclick="share()">📤 Поделиться сайтом</button>

</div>

<script>

// =================== ПРОКСИ ===================

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
"tg://proxy?server=he.108.mtproto.ru&port=443&secret=ee2111222233334444555566667777888862726f777365722e79616e6465782e636f6d",

"tg://proxy?server=nl2.mtproxy.me.mtproto.ru&port=443&secret=ee3f354f86e59e2c166c83031772d92d6379612e7275",
"tg://proxy?server=a4.ru.nuvira.cc.mtproto.ru&port=443&secret=ee470cb2b8b29aeadfbdf8a2f7bee5ca3b62726f777365722e79616e6465782e636f6d",
"tg://proxy?server=c3.ru.nuvira.cc.mtproto.ru&port=443&secret=ee470cb2b8b29aeadfbdf8a2f7bee5ca3b62726f777365722e79616e6465782e636f6d",
"tg://proxy?server=random.1.mtproto.ru&port=443&secret=ee4628a25fc4e5296ba73238298c93fc756d61782e7275",
"tg://proxy?server=ab.x5retail.org.mtproto.ru&port=443&secret=eee67e7cc2d997b34bc1cd2a4b8f3fc07e6c6b2e78352e7275",
"tg://proxy?server=nl.mtproxy.me.mtproto.ru&port=443&secret=ee3f354f86e59e2c166c83031772d92d6379612e7275",
"tg://proxy?server=ru4.mtproxy.me.mtproto.ru&port=443&secret=ee3f354f86e59e2c166c83031772d92d6379612e7275",
"tg://proxy?server=a1.ru.nuvira.cc.mtproto.ru&port=443&secret=ee470cb2b8b29aeadfbdf8a2f7bee5ca3b62726f777365722e79616e6465782e636f6d",
"tg://proxy?server=c1.ru.nuvira.cc.mtproto.ru&port=443&secret=ee470cb2b8b29aeadfbdf8a2f7bee5ca3b62726f777365722.79616e6465782e636f6d",
"tg://proxy?server=de.mtproxy.me.mtproto.ru&port=443&secret=ee3f354f86e59e2c166c83031772d92d6379612e7275"
];

// =================== ЛОГИКА ===================

let page = 1;
const perPage = 10;

function render(){
    const grid=document.getElementById('grid');
    grid.innerHTML='';

    const start=(page-1)*perPage;
    const items=proxies.slice(start,start+perPage);

    items.forEach((p,i)=>{
        const btn=document.createElement('button');
        btn.className='proxy';
        btn.textContent='Прокси '+(start+i+1);
        btn.onclick=()=>location.href=p;
        grid.appendChild(btn);
    });
}

function switchPage(){
    const toggle=document.getElementById('toggle');
    toggle.classList.toggle('active');

    page = page === 1 ? 2 : 1;
    render();
}

render();

// =================== SHARE ===================

function share(){
    const url="https://mrrdanya.github.io/Proxy/";

    if(navigator.share){
        navigator.share({
            title:'Telegram Прокси',
            text:'Рабочие прокси для Telegram',
            url
        });
    }else{
        navigator.clipboard.writeText(url);
        alert("Ссылка скопирована");
    }
}

</script>

</body>
</html>
