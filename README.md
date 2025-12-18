# Genlayer-role-checker-
With your discord username your discord rank and role is visible 
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GenLayer Tracker</title>
    <style>
        body { font-family: sans-serif; background: #0d1117; color: white; text-align: center; padding: 20px; }
        .card { background: #161b22; padding: 20px; border-radius: 12px; border: 1px solid #30363d; max-width: 400px; margin: auto; }
        input { width: 80%; padding: 12px; margin: 10px 0; border-radius: 8px; border: 1px solid #30363d; background: #010409; color: white; }
        button { background: #5865F2; color: white; border: none; padding: 12px; width: 85%; border-radius: 8px; font-weight: bold; cursor: pointer; }
        #res { margin-top: 20px; padding: 15px; background: #0d1117; border-radius: 8px; display: none; text-align: left; }
        .role { color: #f1c40f; font-weight: bold; }
    </style>
</head>
<body>

    <div class="card">
        <h2>🧬 GenLayer Evolution</h2>
        <p style="font-size: 12px; color: gray;">Lvl 1-6 Molecule | 7-17 Neuron | 18-35 Synapse | 36-53 Brain | 54+ Singularity</p>
        
        <input type="text" id="userInput" placeholder="Type Discord Username...">
        <button onclick="check()">Search My Rank</button>

        <div id="res">
            <p>Level: <span id="rLvl"></span></p>
            <p>Rank: <span id="rRnk"></span></p>
            <p>Form: <span id="rRol" class="role"></span></p>
            <button onclick="copyStats()" style="background:#238636; font-size: 12px; padding: 5px;">📋 Copy for Discord</button>
        </div>
    </div>

    <script>
        let players = [];
        async function load() {
            const url = `https://api.allorigins.win/get?url=${encodeURIComponent('https://mee6.xyz/api/plugins/levels/leaderboard/1237055789441487021')}`;
            const res = await fetch(url);
            const data = await res.json();
            players = JSON.parse(data.contents).players;
        }

        function check() {
            const name = document.getElementById('userInput').value.toLowerCase().trim();
            const p = players.find(x => x.username.toLowerCase() === name);
            if(p) {
                const lvl = p.level;
                let role = "Molecule";
                if(lvl >= 54) role = "Singularity";
                else if(lvl >= 36) role = "Brain";
                else if(lvl >= 18) role = "Synapse";
                else if(lvl >= 7) role = "Neuron";

                document.getElementById('rLvl').innerText = lvl;
                document.getElementById('rRnk').innerText = "#" + (players.indexOf(p) + 1);
                document.getElementById('rRol').innerText = role;
                document.getElementById('res').style.display = "block";
            } else { alert("User not found in Top 100!"); }
        }

        function copyStats() {
            const name = document.getElementById('userInput').value;
            const lvl = document.getElementById('rLvl').innerText;
            const rnk = document.getElementById('rRnk').innerText;
            const rol = document.getElementById('rRol').innerText;
            const text = `🧬 GenLayer Evolution\n👤 User: ${name}\n🏆 Rank: ${rnk} | Level: ${lvl}\n✨ Form: ${rol}\nCheck yours: ${window.location.href}`;
            navigator.clipboard.writeText(text);
            alert("Copied! Paste in Discord!");
        }
        load();
    </script>
</body>
</html>
