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
"Agonie la Déterrée",
"Akadémie des Gobs",
"Antichambre des Gloursons",
"Antre de Crocabulia",
"Antre de la Reine Nyée",
"Antre du Blop Multicolore Royal",
"Antre du Dragon Cochon",
"Antre du Korriandre",
"Antre du Kralamoure Géant",
"Aquadôme de Merkator",
"Arbre de Moon",
"Arbre de mort",
"Atelier du Tanukouï San",
"Autel de la Déchireuse",
"Bambusaie de Damadrya",
"Bastion des Marteaux-Aigris",
"Bataille de l'Aurore Pourpre",
"Bateau du Chouque",
"Belvédère d'Ilyzaelle",
"Bibliothèque du Maître Corbac",
"Boyau du Père Ver",
"Brasserie du roi Dazak",
"Breuil du Vénérable",
"Bworks",
"Cache de Kankreblath",
"Cale de l'Arche d'Otomaï",
"Camp du Comte Razof",
"Canopée du Kimbo",
"Cave du Toxoliath",
"Caverne d'El Piko",
"Caverne de Cire Momore",
"Caverne de Nowel",
"Caverne des Bulbes",
"Caverne du Koulosse",
"Cavernes du Kolosso",
"Centre du Labyrinthe du Minotoror",
"Chambre de Tal Kasha",
"Chambre des maléfices",
"Chapiteau des Magik Riktus",
"Château du Wa Wabbit",
"Château Ensablé",
"Cimetière des mastodontes",
"Clairière du Chêne Mou",
"Clos des Blops",
"Comte Harebourg",
"Corbeau Noir",
"Cour du Bouftou Royal",
"Croquanterie",
"Crypte de Kardorim",
"Dark Vlad",
"Dathura",
"Demeure des Esprits",
"Dojo du Vent",
"Domaine Ancestral",
"Draguisla Bonita",
"Défi du Chaloeil",
"Epave du Grolandais violent",
"Excavation du Mansot Royal",
"Fabrique de foux d'artifice",
"Fabrique de Malléfisk",
"Fers de la Tyrannie",
"Firefoux",
"Fonderie des Waddicts",
"Forgefroide de Missiz Frizz",
"Forgerons",
"Galerie du Phossile",
"Garde-manger du Rat Blanc",
"Gelaxième dimension",
"Goulet du Rasboul",
"Grange du Tournesol Affamé",
"Grotte de Kanigroula",
"Grotte du Bworker",
"Grotte Hesque",
"Grozilla et Grasmera",
"Horologium de XLII",
"Hypogée de l'Obsidiantre",
"Julith",
"Kitsounes",
"Laboratoire de Brumen Tinctorias",
"Laboratoire de Nileza",
"Laboratoire du Tynril",
"Larve de Rushu",
"Larves",
"Léorictus le Roi Grimaçant",
"Maison du Papa Nowel",
"Maison Fantôme",
"Malice",
"Manoir des Katrepat",
"Miausolée du Pounicheur",
"Mine de Sakaï",
"Minotot",
"Mégalithe de Fraktale",
"Mémoire d'Orukam",
"Nid du Kwakwa",
"Nowel",
"Noximilien l'Horloger",
"Palais de Dantinéa",
"Palais du roi Nidas",
"Percimol",
"Pitons Rocheux des Craqueleurs",
"Plateau de Ush",
"Poste de contrôle du Supervizœuf",
"Potager d'Halouine",
"Pyramide d'Ombre",
"Qilby",
"Rats de Bonta",
"Rats de Brakmar",
"Refuge Sylvestre",
"Repaire de Daïgoro",
"Repaire de Skeunk",
"Repaire de Sphincter Cell",
"Repaire des Pandikazes",
"Repaire du Kharnozor",
"Ring du Capitaine Ekarlatte",
"Rituel de Kabahal",
"Salons privés de Klime",
"Sanctuaire de Torkélonia",
"Sanctuaire des Familiers",
"Scarafeuilles",
"Sentence de la Balance",
"Serre du Royalmouth",
"Shuccube",
"Sousouricière du Rat Noir",
"Souvenir d'Imagiro",
"Squelettes",
"Tanière du Meulou",
"Tanière Givrefoux",
"Temple de Gargandyas",
"Temple de Koutoulou",
"Temple du dieu Kao",
"Temple du Grand Ougah",
"Tempête de l'Eliocalypse",
"Terrier du Wa Wabbit",
"Tertre du long sommeil",
"Théâtre de Dramak",
"Tofulailler Royal",
"Tofus",
"Tombe du Shogun Tofugawa",
"Tour de Bethel",
"Tour de Solar",
"Transporteur de Sylargh",
"Trône de la Cour Sombre",
"Trône de sang",
"Vaisseau du Capitaine Meno",
"Vallée de la Dame des eaux",
"Ventre de la baleine",
"Village Kanniboul",
"Volière de la Haute Truche",
"Épreuve de Draegnerys",
"Œil de Vortex"
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
