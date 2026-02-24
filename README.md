<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Roulette des Donjons Dofus</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #1e1e1e;
        color: white;
        text-align: center;
        padding-top: 30px;
    }

    canvas {
        margin-top: 20px;
    }

    button {
        margin-top: 30px;
        padding: 15px 30px;
        font-size: 18px;
        cursor: pointer;
        border: none;
        border-radius: 8px;
        background: #ffcc00;
        color: #000;
        font-weight: bold;
    }

    /* Modal */
    #modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.8);
        display: none;
        justify-content: center;
        align-items: center;
    }

    #modal-content {
        background: #fff;
        color: #000;
        padding: 40px;
        border-radius: 10px;
        font-size: 32px;
        font-weight: bold;
    }
</style>
</head>
<body>

<h1>🎡 Roulette des Donjons Dofus</h1>

<canvas id="wheel" width="500" height="500"></canvas>

<button onclick="spin()">🎲 Lancer la roue</button>

<div id="modal" onclick="closeModal()">
    <div id="modal-content"></div>
</div>

<script>
const donjons = [
    "Donjon des Bouftous",
    "Donjon des Champs",
    "Donjon des Forgerons",
    "Donjon des Scarafeuilles",
    "Donjon des Blops",
    "Donjon Kwakwa",
    "Donjon Tofu",
    "Donjon Craqueleur",
    "Donjon Dragon Cochon",
    "Donjon Minotoror",
    "Donjon Minotot",
    "Donjon Kimbo",
    "Donjon Bworker",
    "Donjon Ben le Ripate",
    "Donjon Obsidiantre",
    "Donjon Tengu Givrefoux",
    "Donjon Korriandre",
    "Donjon Kolosso",
    "Donjon Glourséleste",
    "Donjon Royalmouth",
    "Donjon Mansot Royal",
    "Donjon Chêne Mou",
    "Donjon Péki Péki",
    "Donjon Sphincter Cell",
    "Donjon Kralamoure Géant",
    "Donjon Ombre",
    "Donjon Merkator",
    "Donjon Sylargh",
    "Donjon Nileza",
    "Donjon Klime",
    "Donjon Comte Harebourg",
    "Donjon Reine des Voleurs",
    "Donjon Vortex",
    "Donjon Protozorreur",
    "Donjon Chalœil",
    "Donjon Tal Kasha",
    "Donjon Dazak Martegel",
    "Donjon Solar",
    "Donjon Bethel Akarna",
    "Donjon Ilyzaelle",
    "Donjon Imagiro",
    "Donjon Koutoulou",
    "Donjon Dantinéa",
    "Donjon Ush",
    "Donjon Meno",
    "Donjon Capitaine Meno",
    "Donjon Père Ver",
    "Donjon Kanniboul Ebil",
    "Donjon Kanniboul Jav",
    "Donjon Kanniboul Sarbak",
    "Donjon Kanniboul Archer",
    "Donjon Pandala Feu",
    "Donjon Pandala Terre",
    "Donjon Pandala Eau",
    "Donjon Pandala Air",
    "Donjon Tanukouï San",
    "Donjon Fuji Givrefoux",
    "Donjon Kanigroula",
    "Donjon Tour des Voyageurs",
    "Donjon Tour des Défis"
];

const canvas = document.getElementById("wheel");
const ctx = canvas.getContext("2d");
let angle = 0;

function drawWheel() {
    const nb = donjons.length;
    const arc = 2 * Math.PI / nb;

    for (let i = 0; i < nb; i++) {
        ctx.beginPath();
        ctx.fillStyle = `hsl(${i * (360 / nb)}, 80%, 50%)`;
        ctx.moveTo(250, 250);
        ctx.arc(250, 250, 250, arc * i, arc * (i + 1));
        ctx.fill();

        ctx.save();
        ctx.translate(250, 250);
        ctx.rotate(arc * i + arc / 2);
        ctx.textAlign = "right";
        ctx.fillStyle = "black";
        ctx.font = "14px Arial";
        ctx.fillText(donjons[i], 230, 5);
        ctx.restore();
    }
}

drawWheel();

function spin() {
    const spinAngle = Math.random() * 2000 + 2000;
    const duration = 4000;
    const start = performance.now();

    function animate(now) {
        const progress = (now - start) / duration;
        if (progress < 1) {
            angle = spinAngle * easeOut(progress);
            canvas.style.transform = `rotate(${angle}deg)`;
            requestAnimationFrame(animate);
        } else {
            const finalAngle = angle % 360;
            const arc = 360 / donjons.length;
            const index = Math.floor((360 - finalAngle) / arc) % donjons.length;
            showModal(donjons[index]);
        }
    }

    requestAnimationFrame(animate);
}

function easeOut(t) {
    return 1 - Math.pow(1 - t, 3);
}

function showModal(text) {
    document.getElementById("modal-content").innerText = text;
    document.getElementById("modal").style.display = "flex";
}

function closeModal() {
    document.getElementById("modal").style.display = "none";
}
</script>

</body>
</html>
