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
            padding-top: 50px;
        }

        #wheel {
            width: 300px;
            height: 300px;
            border-radius: 50%;
            border: 10px solid #fff;
            margin: 0 auto;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 22px;
            font-weight: bold;
            background: linear-gradient(45deg, #ffcc00, #ff6600);
            transition: transform 4s cubic-bezier(.17,.67,.83,.67);
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

    <div id="wheel">Clique pour tourner</div>

    <button onclick="spin()">🎲 Lancer la roue</button>

    <!-- Modal -->
    <div id="modal" onclick="closeModal()">
        <div id="modal-content"></div>
    </div>

    <script>
        const donjons = [
            "Donjon Bouftou",
            "Donjon des Champs",
            "Donjon des Forgerons",
            "Donjon des Scarafeuilles",
            "Donjon Blop",
            "Donjon Kwakwa",
            "Donjon Bworker",
            "Donjon Tofu",
            "Donjon Craqueleur",
            "Donjon Dragon Cochon",
            "Donjon Minotoror",
            "Donjon Kimbo",
            "Donjon Ben le Ripate",
            "Donjon Obsidiantre",
            "Donjon Korriandre",
            "Donjon Kolosso",
            "Donjon Glourséleste"
        ];

        function spin() {
            const wheel = document.getElementById("wheel");
            const randomIndex = Math.floor(Math.random() * donjons.length);
            const selected = donjons[randomIndex];

            const rotation = 360 * 5 + Math.random() * 360;
            wheel.style.transform = `rotate(${rotation}deg)`;

            setTimeout(() => {
                showModal(selected);
            }, 4000);
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
