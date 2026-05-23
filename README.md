<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gully Cricket Scorer</title>
    <style>
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            text-align: center; 
            background-color: #e9ecef; 
            margin: 0; 
            padding: 20px; 
        }
        .score-board { 
            background: #212529; 
            color: #fff; 
            padding: 30px; 
            border-radius: 15px; 
            margin-bottom: 30px; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        h1 { font-size: 4em; margin: 10px 0; color: #0d6efd; }
        h2 { font-size: 1.5em; color: #ced4da; margin: 0; }
        .btn-grid { 
            display: grid; 
            grid-template-columns: repeat(3, 1fr); 
            gap: 15px; 
            max-width: 450px; 
            margin: auto; 
        }
        button { 
            padding: 15px; 
            font-size: 1.2em; 
            font-weight: bold;
            border: none; 
            border-radius: 8px; 
            cursor: pointer; 
            background: #0d6efd; 
            color: white; 
            transition: 0.2s;
        }
        button:hover { background: #0b5ed7; }
        button:active { transform: scale(0.95); }
        button.wicket { background: #dc3545; }
        button.wicket:hover { background: #bb2d3b; }
        button.extra { background: #ffc107; color: #000; }
        button.extra:hover { background: #ffca2c; }
        button.reset { background: #6c757d; grid-column: span 3; }
        button.reset:hover { background: #5c636a; }
    </style>
</head>
<body>

    <div class="score-board">
        <h2>Live Score</h2>
        <h1 id="scoreDisplay">0 / 0</h1>
        <h2>Overs: <span id="overDisplay">0.0</span></h2>
    </div>

    <div class="btn-grid">
        <button onclick="addRuns(0)">Dot (0)</button>
        <button onclick="addRuns(1)">1 Run</button>
        <button onclick="addRuns(2)">2 Runs</button>
        <button onclick="addRuns(3)">3 Runs</button>
        <button onclick="addRuns(4)">4 Runs</button>
        <button onclick="addRuns(6)">6 Runs</button>
        <button class="extra" onclick="addExtra()">Wide / NB</button>
        <button class="wicket" onclick="addWicket()">Wicket</button>
        <button class="reset" onclick="resetScore()">Reset Match</button>
    </div>

    <script>
        // Variables to store match data
        let runs = 0;
        let wickets = 0;
        let balls = 0;

        // Function to update the screen
        function updateUI() {
            document.getElementById('scoreDisplay').innerText = runs + " / " + wickets;
            
            // Calculate overs and balls (e.g., 7 balls = 1.1 overs)
            let overCount = Math.floor(balls / 6);
            let ballCount = balls % 6;
            document.getElementById('overDisplay').innerText = overCount + "." + ballCount;
        }

        // Function to add runs for a legal delivery
        function addRuns(r) {
            if (wickets >= 10) return alert("All out bhai! Nayi innings shuru karo.");
            runs += r;
            balls++;
            updateUI();
        }

        // Function to add a wicket
        function addWicket() {
            if (wickets >= 10) return alert("All out bhai!");
            wickets++;
            balls++; // Wicket delivery counts as a legal ball
            updateUI();
        }

        // Function to add extra runs (Wide / No Ball)
        function addExtra() {
            if (wickets >= 10) return alert("All out bhai!");
            runs++; 
            // Extras don't count as a legal ball, so 'balls' is not increased
            updateUI();
        }

        // Function to reset the game
        function resetScore() {
            if(confirm("Pakka score reset karna hai?")) {
                runs = 0; 
                wickets = 0; 
                balls = 0;
                updateUI();
            }
        }
    </script>
</body>
</html>
