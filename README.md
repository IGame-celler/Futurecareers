# Futurecareers.gov
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title> Neuro-Surgon</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4e2c8;
        text-align: center;
        margin: 0;
        padding: 20px;
    }

    h1 { margin-bottom: 10px; }

    #cookie {
        width: 200px;
        cursor: pointer;
        transition: transform 0.1s;
    }

    #cookie:active {
        transform: scale(0.95);
    }

    .panel {
        margin-top: 20px;
        background: #fff8e6;
        padding: 20px;
        border-radius: 10px;
        display: inline-block;
        min-width: 260px;
        box-shadow: 0 3px 6px rgba(0,0,0,.15);
    }

    button {
        width: 100%;
        padding: 10px;
        margin-top: 10px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        background: #d3a15d;
        color: white;
        font-size: 16px;
        transition: background 0.2s;
    }

    button:hover {
        background: #c28f4e;
    }

    button:disabled {
        background: #9a815f;
        cursor: not-allowed;
    }
</style>
</head>

<body>
<h1> Neuro-Surgon</h1>
<h2>Cookies: <span id="count">0</span></h2>

<img id="cookie" src="https://upload.wikimedia.org/wikipedia/commons/7/70/Cookie.png">

<div class="panel">
    <h3>Upgrades</h3>
    <button id="cursorBtn">Buy Cursor (10) — +1 CPS</button>
    <button id="grandmaBtn">Buy Grandma (100) — +5 CPS</button>
    <button id="factoryBtn">Buy Factory (1000) — +25 CPS</button>

    <p style="margin-top:15px;">CPS: <span id="cps">0</span></p>
</div>

<script>
let cookies = 0;
let cps = 0;

// Upgrade definitions
const upgrades = {
    cursor: { cost: 10, cps: 1, count: 0 },
    grandma: { cost: 100, cps: 5, count: 0 },
    factory: { cost: 1000, cps: 25, count: 0 }
};

// UI elements
const cookieEl = document.getElementById("cookie");
const countEl = document.getElementById("count");
const cpsEl = document.getElementById("cps");
const cursorBtn = document.getElementById("cursorBtn");
const grandmaBtn = document.getElementById("grandmaBtn");
const factoryBtn = document.getElementById("factoryBtn");

// Click to gain cookies
cookieEl.addEventListener("click", () => {
    cookies++;
    updateDisplay();
});

// Handle buying upgrades
cursorBtn.onclick = () => buyUpgrade("cursor", cursorBtn);
grandmaBtn.onclick = () => buyUpgrade("grandma", grandmaBtn);
factoryBtn.onclick = () => buyUpgrade("factory", factoryBtn);

function buyUpgrade(type, button) {
    const u = upgrades[type];
    if (cookies >= u.cost) {
        cookies -= u.cost;
        u.count++;
        cps += u.cps;

        // Increase cost slightly
        u.cost = Math.floor(u.cost * 1.15);

        // Update button text
        button.textContent = `Buy ${capitalize(type)} (${u.cost}) — +${u.cps} CPS`;
        updateDisplay();
    }
}

function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}

// Add cookies automatically
setInterval(() => {
    cookies += cps / 10; // smooth 10-times-per-second increase
    updateDisplay(false);
}, 100);

function updateDisplay(round = true) {
    countEl.textContent = round ? Math.floor(cookies) : cookies.toFixed(1);
    cpsEl.textContent = cps;
}
</script>
</body>
</html>
