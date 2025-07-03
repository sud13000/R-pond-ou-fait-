<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Dis ou Engage</title>
  <style>
    body { font-family: Arial; text-align: center; background: #f4f4f4; padding: 20px; }
    #game { display: none; }
    button {
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      background: #007bff;
      color: white;
    }
    button:hover { background: #0056b3; }
    textarea {
      padding: 10px;
      margin: 5px;
      border-radius: 5px;
      width: 80%;
      max-width: 400px;
    }
    #challenge {
      color: darkred;
      font-weight: bold;
      margin-top: 20px;
      min-height: 40px;
    }
  </style>
</head>
<body>

  <h1>🎉 Dis ou Engage 🎉</h1>

  <div id="setup">
    <p>Entre les prénoms des joueurs (1 par ligne) :</p>
    <textarea id="playersInput" rows="6" placeholder="Ex: Alice&#10;Bob&#10;Charlie"></textarea><br>
    <button onclick="startGame()">Lancer la partie</button>
  </div>

  <div id="game">
    <h2 id="playerTurn"></h2>
    <p id="question"></p>
    <button onclick="respond()">Je réponds</button>
    <button onclick="refuse()">Je refuse</button>
    <p id="challenge"></p>
  </div>

  <script>
    const questions = [
      "Quel est ton dernier mensonge ?",
      "As-tu déjà stalké un ex ?",
      "Quel joueur ici t’intrigue le plus ?",
      "Quel est ton fantasme le plus bizarre ?",
      "As-tu déjà été attiré(e) par quelqu’un ici ?"
    ];

    const challenges = [
      "Fais une imitation d’un animal.",
      "Chante une chanson connue.",
      "Fais une grimace pendant 10 secondes.",
      "Parle avec une voix bizarre pendant 2 tours.",
      "Danse sans musique 15 secondes."
    ];

    let players = [];
    let currentPlayer = 0;
    let refuseMode = false;

    function startGame() {
      const input = document.getElementById("playersInput").value.trim();
      players = input.split("\n").map(p => p.trim()).filter(p => p !== "");
      if (players.length < 2) return alert("Ajoute au moins 2 joueurs !");
      document.getElementById("setup").style.display = "none";
      document.getElementById("game").style.display = "block";
      nextTurn();
    }

    function nextTurn() {
      document.getElementById("challenge").innerText = "";
      refuseMode = false;
      const player = players[currentPlayer];
      document.getElementById("playerTurn").innerText = "👉 À " + player + " de jouer !";
      document.getElementById("question").innerText = questions[Math.floor(Math.random() * questions.length)];
    }

    function respond() {
      currentPlayer = (currentPlayer + 1) % players.length;
      nextTurn();
    }

    function refuse() {
      const gage = challenges[Math.floor(Math.random() * challenges.length)];
      document.getElementById("challenge").innerText = "🔥 Gage : " + gage;
      document.getElementById("question").innerText = "✅ Clique sur 'Je réponds' pour continuer.";
    }
  </script>

</body>
</html>
