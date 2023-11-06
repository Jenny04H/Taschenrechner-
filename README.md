<!DOCTYPE html>
<html>
<head>
    <title>Options</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 5;
            display: grid;
            grid-template-columns: 1fr;
            grid-template-rows: min-content 1fr auto;
        }
        .header {
            max-width: 600px;
            margin: 5 auto;
            border: 1px solid #ccc;
            border-radius: 10px;
            padding: 5px;
            background-color: #333;
            color: white;
            text-align: center;
            position: relative;
            cursor: pointer;
        }
        .content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        .calculator {
            max-width: 100%;
            border: 1px solid #ccc;
            border-radius: 10px;
            padding: 10px;
            background-color: #fff;
            position: relative; /* Hinzugefügt: relative Positionierung */
        }
        .additional-field {
            max-width: 31%;
            border: 1px solid #ccc;
            border-radius: 6px;
            padding: 11px;
            background-color: #fff;
            display: none;
        }
        .toggle-button {
            position: absolute;
            left: 15px;
            top: 15px;
        }
        /* Rest deines CSS-Codes für den Taschenrechner bleibt unverändert */
    </style>
</head>
<body>
    <div class="header" onclick="toggleAdditionalField()">
        <span class="toggle-button">≡</span><h1>Options</h1>
    </div>
    <div class="content">
        <div class="calculator" id="calculator">
            <!-- Dein Taschenrechner-HTML-Code bleibt unverändert -->
        </div>
    </div>
    <div class="additional-field" id="additionalField">
        <!-- Inhalt deines zusätzlichen Feldes -->
    </div>

    <script>
        // JavaScript-Code für den Taschenrechner
        // ...

        function toggleAdditionalField() {
            const additionalField = document.getElementById("additionalField");
            if (additionalField.style.display === "block") {
                additionalField.style.display = "none";
            } else {
                additionalField.style.display = "block";
            }
        }

        // JavaScript-Code für das Verschieben des Taschenrechners
        const calculator = document.getElementById("calculator");
        let isDragging = false;
        let offsetX, offsetY;

        calculator.addEventListener("mousedown", (e) => {
            isDragging = true;
            offsetX = e.clientX - calculator.getBoundingClientRect().left;
            offsetY = e.clientY - calculator.getBoundingClientRect().top;
        });

        document.addEventListener("mousemove", (e) => {
            if (isDragging) {
                calculator.style.left = e.clientX - offsetX + "px";
                calculator.style.top = e.clientY - offsetY + "px";
            }
        });

        document.addEventListener("mouseup", () => {
            isDragging = false;
        });
    </script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <title>Taschenrechner</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .calculator {
            max-width: 300px;
            margin: 0 auto;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 10px;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
        }
        input[type="text"] {
            grid-column: span 4;
            padding: 10px;
            font-size: 18px;
            text-align: right;
            background-color: #696969; /* Schwarz */
       	    color: white; /* Weiße Textfarbe */
	}
        button {
            width: 50px;
            height: 50px;
            font-size: 20px;
            background-color: #696969; /* Schwarz */
            color: #333; /* Dunkelgrau */
            border: 1px solid #ccc;
        }
        .symbol {
            background-color: black;
            border: 4px solid black;
            color: white;
        }
        .equals {
            background-color: #696969; /* Schwarz */
            border: 4px #00BFFF;
            color: white;
        }
	.equals <=> {
	    background-color: #00BFFF; /* Hellblau */ 
	    border: 2px #00BFFF; 
	    color: white;
	}
	button[class="symbol"][onclick="appendToDisplay('=')"] {
   	   background-color: #696969; /* Dunkelgrau */
   	   border: 4px solid #00BFFF;
   	   color: white;
	}
	.result-button {
            background-color: #00BFFF;
            border: 2px solid #00BFFF;
            color: white;
	}
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <button class="symbol" onclick="calculatePercentage()">%</button>
        <button class="symbol" onclick="clearEntry()">CE</button>
        <button class="symbol" onclick="clearAll()">C</button>
        <button class="symbol" onclick="backspace()">⌫</button>
        <button class="symbol" onclick="appendToDisplay('1/')">1/x</button>
        <button class="symbol" onclick="appendToDisplay('**2')">x²</button>
        <button class="symbol" onclick="calculateSquareRoot()">√x</button>
        <button class="symbol" onclick="appendToDisplay('÷')">÷</button>
        <button onclick="appendToDisplay('7')">7</button>
        <button onclick="appendToDisplay('8')">8</button>
        <button onclick="appendToDisplay('9')">9</button>
        <button class="symbol" onclick="appendToDisplay('*')">*</button>
        <button onclick="appendToDisplay('4')">4</button>
        <button onclick="appendToDisplay('5')">5</button>
        <button onclick="appendToDisplay('6')">6</button>
        <button class="symbol" onclick="appendToDisplay('-')">-</button>
        <button onclick="appendToDisplay('1')">1</button>
        <button onclick="appendToDisplay('2')">2</button>
        <button onclick="appendToDisplay('3')">3</button>
        <button class="symbol" onclick="appendToDisplay('+')">+</button>
        <button class="symbol" onclick="toggleSign()">±</button>
        <button onclick="appendToDisplay('0')">0</button>
        <button class="symbol" onclick="appendToDisplay(',')">,</button>
        <button class="result-button" onclick="calculateResult()">=</button>
    </div>

    <script>
        let currentInput = "";
        let result = 0;

        function clearAll() {
            currentInput = "";
            document.getElementById("display").value = "";
        }

        function clearEntry() {
            currentInput = currentInput.slice(0, -1);
            document.getElementById("display").value = currentInput;
        }

        function toggleSign() {
            if (currentInput[0] === '-') {
                currentInput = currentInput.substring(1);
            } else {
                currentInput = '-' + currentInput;
            }
            document.getElementById("display").value = currentInput;
        }

        function appendToDisplay(value) {
            if (value === '**2') {
                currentInput += '**2';
                document.getElementById("display").value = currentInput;
            } else {
                currentInput += value;
                document.getElementById("display").value = currentInput;
            }
        }

        function backspace() {
            currentInput = currentInput.slice(0, -1);
            document.getElementById("display").value = currentInput;
        }

        function calculateResult() {
            try {
                result = eval(currentInput);
                document.getElementById("display").value = result;
            } catch (error) {
                document.getElementById("display").value = "Error";
            }
        }

        function calculateSquareRoot() {
            try {
                result = Math.sqrt(parseFloat(currentInput));
                document.getElementById("display").value = result;
            } catch (error) {
                document.getElementById("display").value = "Error";
            }
            currentInput = "";
        }

        function calculatePercentage() {
            try {
                result = eval(currentInput) / 100;
                document.getElementById("display").value = result;
            } catch (error) {
                document.getElementById("display").value = "Error";
            }
        }

    </script>
</body>
</html>

