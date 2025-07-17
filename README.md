<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Detailed Dice Roller</title>
    <link href="https://fonts.googleapis.com/css2?family=Luckiest+Guy&display=swap" rel="stylesheet">
    <style>
    * {
  -webkit-tap-highlight-color: transparent; /* Removes the blue box on tap */
}

        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #a5ceff;
            color: black;
            padding: 20px;
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .wrapper {
            width: 20cm;
            height: auto;
            border: 5px solid white; /* White border */
            background-color: #5ba7ff;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            border-radius: 20px;
            position: relative;
        }

        .title {
            font-family: 'Luckiest Guy', cursive;
            font-size: 36px;
            font-weight: bold;
            color: white;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 1px;
            text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
        }

        button {
            background: linear-gradient(to bottom, #ffeb3b, #ffc107);
            color: white;
            font-family: 'Luckiest Guy', cursive;
            padding: 10px 250px;
            font-size: 28px;
            font-weight: bold;
            text-transform: uppercase;
            border: 3px solid white;
            border-radius: 6px;
            cursor: pointer;
            box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2), 0px -3px 6px rgba(255, 255, 255, 0.6);
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
            display: inline-block;
            text-align: center;
            height: 50px;
            -webkit-text-stroke: 0.2px #ca8a00; /* Added text outline color */
            font-weight: bold; /* Ensuring bold text */
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0px 10px 12px rgba(0, 0, 0, 0.3), 0px -4px 8px rgba(255, 255, 255, 0.5);
        }

        button:active {
            transform: scale(0.98);
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.4), 0px -2px 4px rgba(255, 255, 255, 0.4);
        }

        .dice-result {
            margin: 10px auto;
            padding: 10px;
            width: 100%;
            max-width: 600px;
            display: flex;
            justify-content: center;
            gap: 10px;
        }

        .color-block {
            display: inline-block;
            width: 75px;
            height: 75px;
            position: relative;
            border: 9px solid #fff;
            box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.25), -4px -4px 10px rgba(255, 255, 255, 0.8);
            background-color: grey;
            border-radius: 12px;
            animation: shake-dice 0.2s infinite, freeze-dice 0.5s 1s forwards, color-change 0.5s 1.5s forwards;
            transition: background-color 0.2s ease-in-out; /* Fade effect */
        }

        .coin {
            display: inline-block;
            width: 100px; /* Increased width */
            height: 100px; /* Increased height */
            position: relative;
            border: 5px solid #fff; /* Smaller white border */
            box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.25), -4px -4px 10px rgba(255, 255, 255, 0.8);
            background-color: grey;
            border-radius: 50%; /* Make it a circle */
            transition: background-color 0.2s ease-in-out, transform 0.5s ease-in-out; /* Fade effect and smooth stop */
            flex-shrink: 0; /* Prevent stretching */
        }

        .dot {
            width: 14px;
            height: 14px;
            background-color: white;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        @keyframes shake-dice {
            0%, 100% {
                transform: translate(0, 0);
            }
            25% {
                transform: translate(-3px, 3px);
            }
            50% {
                transform: translate(3px, -3px);
            }
            75% {
                transform: translate(-3px, -3px);
            }
        }

        @keyframes freeze-dice {
            0% {
                transform: translate(0, 0);
            }
            100% {
                transform: translate(0, 0); /* No movement */
            }
        }

        @keyframes toss-coin {
            0% {
                transform: translateY(0) rotateX(0deg);
            }
            25% {
                transform: translateY(-100px) rotateX(180deg);
            }
            50% {
                transform: translateY(-200px) rotateX(360deg);
            }
            75% {
                transform: translateY(-100px) rotateX(540deg);
            }
            100% {
                transform: translateY(0) rotateX(720deg);
            }
        }

        @keyframes flip-button {
            0% {
                transform: scale(1) rotateX(0deg);
            }
            25% {
                transform: scale(1.2) rotateX(180deg);
            }
            50% {
                transform: scale(1) rotateX(360deg);
            }
            75% {
                transform: scale(1.2) rotateX(540deg);
            }
            100% {
                transform: scale(1) rotateX(720deg);
            }
        }

        .flipping {
            animation: flip-button 1.6s ease-in-out;
        }

        @keyframes flip-coin {
            0% {
                transform: scale(1) rotateX(0deg);
            }
            25% {
                transform: scale(1.2) rotateX(180deg);
            }
            50% {
                transform: scale(1) rotateX(360deg);
            }
            75% {
                transform: scale(1.2) rotateX(540deg);
            }
            100% {
                transform: scale(1) rotateX(720deg);
            }
        }

        .flipping {
            animation: flip-coin 1.6s ease-in-out;
        }

        .coin img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
            backface-visibility: hidden; /* Prevent flipping upside down */
        }

        .color-info {
            margin-top: 30px;
            font-size: 16px;
            font-weight: bold;
            font-style: normal;
            color: white;
            text-transform: none;
        }

        .color-info span.red {
            color: red;
        }
        .color-info span.orange {
            color: orange;
        }
        .color-info span.yellow {
            color: gold;
        }
        .color-info span.green {
            color: green;
        }
        .color-info span.blue {
            color: blue;
        }
        .color-info span.purple {
            color: purple;
        }

        .color-container {
            width: 18cm;
            height: 30px;
            background-color: #2d98ff;
            margin-top: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 6px;
        }

        .color-container .color-info {
            margin: 0;
            line-height: normal;
        }

        .dropdown-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        select {
            font-family: 'Luckiest Guy', cursive;
            font-size: 24px;  /* Increased font size */
            padding: 10px 20px;
            border: 3px solid #0088ff; /* Border color */
            border-radius: 6px;
            background-color: white; /* Background color */
            color: #0088ff; /* Text color updated */
            text-transform: uppercase;
            text-align: left; /* Left align the text */
            box-shadow: 0px 6px 8px rgba(0, 0, 0, 0.2);
            cursor: pointer;
            width: 310px;
            outline: none; /* Remove the outline from dropdown */
            -webkit-text-stroke: none; /* Removed text outline from dropdown */
        }

        .exclude-container {
            position: absolute;
            top: 20px;
            right: 20px;
            display: none;
            flex-direction: column;
            align-items: flex-start;
            background-color: #5ba7ff;
            border: 5px solid white;
            border-radius: 12px;
            padding: 15px;
        }

        .exclude-container label {
            font-size: 16px;
            margin-bottom: 5px;
            font-weight: bold;
        }

        .exclude-container .red { color: red; }
        .exclude-container .orange { color: orange; }
        .exclude-container .gold { color: gold; }
        .exclude-container .green { color: green; }
        .exclude-container .blue { color: blue; }
        .exclude-container .purple { color: purple; }



    </style>
</head>
<body>
    <div class="wrapper">
    <div class="title">MONYUN DICE </div>
    <div class="dropdown-container">
        <select id="numDice">
            <option value="1">1 Dice</option>
            <option value="2">2 Dice</option>
            <option value="3">3 Dice</option>
            <option value="4">4 Dice</option>
	    <option value="5">5 Dice</option>
	    <option value="6">6 Dice</option>
        </select>
        <select id="colorDice">
    <option value="color">Color Dice</option>
    <option value="headsOrTails">Heads or Tails</option>
</select>
    </div>
    <div id="result" class="dice-result"></div>
    <button id="rollButton" disabled>ROLL AGAIN !</button>
    <div class="color-container">
        <div class="color-info" id="colorInfo">
    Possible colors are: 
    <span class="red" data-color="red">Red</span>, 
    <span class="orange" data-color="orange">Orange</span>, 
    <span class="yellow" data-color="gold">Yellow</span>, 
    <span class="green" data-color="green">Green</span>, 
    <span class="blue" data-color="blue">Blue</span>, 
    <span class="purple" data-color="purple">Purple</span>.
</div>

<audio id="rollSound" src="roll-sound.mp3" preload="auto"></audio>

    <script>
        document.querySelectorAll("#colorInfo span").forEach(span => {
    span.style.cursor = "pointer";
    span.addEventListener("click", function () {
        const color = this.getAttribute("data-color");
        const isExcluded = excludedColors.includes(color);

        if (isExcluded) {
            excludedColors = excludedColors.filter(c => c !== color);
        } else {
            excludedColors.push(color);
        }
    });
});


        let numDice = 1;
        const validColors = ["red", "orange", "gold", "green", "blue", "purple"];
        let excludedColors = [];

        const rollSound = new Audio('roll-sound.mp3');
        let isMuted = false;

        function toggleMute() {
            isMuted = !isMuted;
            document.getElementById("muteButtonImg").src = isMuted ? "mute.png" : "sound.png";
        }

        function playRollSound() {
            if (!isMuted) {
                rollSound.play();
            }
        }

        function getRandomColor() {
    const availableColors = validColors.filter(color => !excludedColors.includes(color));
    if (availableColors.length === 0) return "grey"; // fallback if all are excluded
    const randomIndex = Math.floor(Math.random() * availableColors.length);
    return availableColors[randomIndex];
   }

        function rollDice() {
            const resultDiv = document.getElementById("result");
            const rollButton = document.getElementById("rollButton");
            resultDiv.innerHTML = "";

            rollButton.disabled = true;

            const rollDuration = 1600;
            const rollingColor = "#eaf5ff"; 
            const soundDuration = 2800; 

            playRollSound();

            for (let i = 0; i < numDice; i++) {
                const colorBlock = document.createElement("div");
                colorBlock.className = "color-block";
                colorBlock.style.backgroundColor = rollingColor;

                const dot = document.createElement("div");
                dot.className = "dot";
                colorBlock.appendChild(dot);

                let animationInterval = setInterval(() => {
                    colorBlock.style.backgroundColor = rollingColor;
                }, 100);

                setTimeout(() => {
                    clearInterval(animationInterval);
                    let finalColor;
                    do {
                        finalColor = getRandomColor(true);
                    } while (excludedColors.includes(finalColor));

                    colorBlock.style.backgroundColor = finalColor;
                }, rollDuration);

                resultDiv.appendChild(colorBlock);
            }

            setTimeout(() => {
                rollButton.disabled = false;
                resetExcludedColors();
            }, soundDuration);
        }

        function resetExcludedColors() {
            excludedColors = [];
            document.querySelectorAll(".exclude-container input[type='checkbox']").forEach(checkbox => {
                checkbox.checked = false;
            });
        }

        function flipCoin() {
            const resultDiv = document.getElementById("result");
            const rollButton = document.getElementById("rollButton");
            resultDiv.innerHTML = "";

            rollButton.disabled = true;

            const rollDuration = 1600;
            const rollingColor = "#eaf5ff"; 
            const soundDuration = 2800; 

            playRollSound();

            for (let i = 0; i < numDice; i++) {
                const colorBlock = document.createElement("div");
                colorBlock.className = "coin flipping";
                colorBlock.style.backgroundColor = rollingColor;

                let switchInterval = setInterval(() => {
                    colorBlock.style.backgroundColor = rollingColor;
                }, 100);

                setTimeout(() => {
                    clearInterval(switchInterval);
                    let finalImage;
                    do {
                        finalImage = Math.random() < 0.5 ? "heads.png" : "tails.png";
                    } while (excludedColors.includes(finalImage === "heads.png" ? "heads" : "tails"));

                    colorBlock.innerHTML = `<img src="${finalImage}" alt="Coin Face" class="fade-in">`;
                    colorBlock.classList.remove("flipping");
                    colorBlock.style.backgroundColor = "transparent"; // Remove background color after flip
                }, rollDuration);

                resultDiv.appendChild(colorBlock);
            }

            setTimeout(() => {
                rollButton.disabled = false;
                resetExcludedColors();
            }, soundDuration);
        }

        document.getElementById("colorDice").addEventListener("change", function () {
            const numDiceSelect = document.getElementById("numDice");
            const rollButton = document.getElementById("rollButton");
            const colorInfo = document.getElementById("colorInfo");
            const excludeContainer = document.querySelector(".exclude-container");
            if (this.value === "headsOrTails") {
                updateNumDiceOptions("coin");
                rollButton.textContent = "FLIP AGAIN !";
                colorInfo.innerHTML = 'Possible coins are: <span style="color: green;">Heads</span> and <span style="color: orange;">Tails</span>.';
                excludeContainer.innerHTML = `
                    <label style="color: green;"><input type="checkbox" id="excludeHeads"> Heads</label>
                    <label style="color: orange;"><input type="checkbox" id="excludeTails"> Tails</label>
                `;
                document.getElementById("excludeHeads").addEventListener("change", function () {
                    toggleExcludedColor("heads", this.checked);
                });
                document.getElementById("excludeTails").addEventListener("change", function () {
                    toggleExcludedColor("tails", this.checked);
                });
                rollButton.removeEventListener("click", rollDice);
                rollButton.addEventListener("click", flipCoin);
            } else {
                updateNumDiceOptions("dice");
                rollButton.textContent = "ROLL AGAIN !";
                colorInfo.innerHTML = 'Possible colors are: <span class="red">Red</span>, <span class="orange">Orange</span>, <span class="yellow">Yellow</span>, <span class="green">Green</span>, <span class="blue">Blue</span>, and <span class="purple">Purple</span>.';
                excludeContainer.innerHTML = `
                    <label class="red"><input type="checkbox" id="excludeRed"> Red</label>
                    <label class="orange"><input type="checkbox" id="excludeOrange"> Orange</label>
                    <label class="gold"><input type="checkbox" id="excludeGold"> Gold</label>
                    <label class="green"><input type="checkbox" id="excludeGreen"> Green</label>
                    <label class="blue"><input type="checkbox" id="excludeBlue"> Blue</label>
                    <label class="purple"><input type="checkbox" id="excludePurple"> Purple</label>
                `;
                document.getElementById("excludeRed").addEventListener("change", function () {
                    toggleExcludedColor("red", this.checked);
                });
                document.getElementById("excludeOrange").addEventListener("change", function () {
                    toggleExcludedColor("orange", this.checked);
                });
                document.getElementById("excludeGold").addEventListener("change", function () {
                    toggleExcludedColor("gold", this.checked);
                });
                document.getElementById("excludeGreen").addEventListener("change", function () {
                    toggleExcludedColor("green", this.checked);
                });
                document.getElementById("excludeBlue").addEventListener("change", function () {
                    toggleExcludedColor("blue", this.checked);
                });
                document.getElementById("excludePurple").addEventListener("change", function () {
                    toggleExcludedColor("purple", this.checked);
                });
                rollButton.removeEventListener("click", flipCoin);
                rollButton.addEventListener("click", rollDice);
            }
        });

        function updateNumDiceOptions(type) {
            const numDiceSelect = document.getElementById("numDice");
            numDiceSelect.innerHTML = "";
            for (let i = 1; i <= 6; i++) {
                const option = document.createElement("option");
                option.value = i;
                option.text = `${i} ${type}${i > 1 ? 's' : ''}`;
                numDiceSelect.appendChild(option);
            }
        }

        window.onload = function () {
            setTimeout(() => rollDice(), 500);
            updateNumDiceOptions("dice"); // Initialize with "dice" options
        };

        document.getElementById("rollButton").addEventListener("click", rollDice);
        document.getElementById("numDice").addEventListener("change", function () {
            numDice = parseInt(this.value);
        });
