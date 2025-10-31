# Simple-Calculator
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #062054 0%, #ac8dcb 100%);
        }
        
        .calculator {
            background: #c4dde7f1;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgb(13, 28, 42);
            padding: 20px;
            width: 320px;
        }
        
        .display {
            background: linear-gradient(135deg, #2e2438 0%, #062054 100%);
            ;
            color: #fff;
            font-size: 2.5rem;
            text-align: right;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            min-height: 80px;
            word-wrap: break-word;
            word-break: break-all;
        }
        
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        
        button {
            padding: 20px;
            font-size: 1.5rem;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
        }
        
        button:hover {
            transform: scale(1.05);
        }
        
        button:active {
            transform: scale(0.95);
        }
        
        .num,
        .decimal {
            background: #f0f0f0;
            color: #333;
        }
        
        .num:hover,
        .decimal:hover {
            background: #e0e0e0;
        }
        
        .operator {
            background: #5a41ae;
            color: #fff;
        }
        
        .operator:hover {
            background: #e68600;
        }
        
        .equals {
            background: #1ce362;
            color: #fff;
            grid-column: span 2;
        }
        
        .equals:hover {
            background: #1cbbe3;
        }
        
        .clear {
            background: #e74b4bc9;
            color: #fff;
            grid-column: span 2;
        }
        
        .clear:hover {
            background: #e6342a;
        }
    </style>
</head>

<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="clear" onclick="clearDisplay()">C</button>
            <button class="operator" onclick="appendOperator('/')">÷</button>
            <button class="operator" onclick="appendOperator('*')">×</button>

            <button class="num" onclick="appendNumber('7')">7</button>
            <button class="num" onclick="appendNumber('8')">8</button>
            <button class="num" onclick="appendNumber('9')">9</button>
            <button class="operator" onclick="appendOperator('-')">−</button>

            <button class="num" onclick="appendNumber('4')">4</button>
            <button class="num" onclick="appendNumber('5')">5</button>
            <button class="num" onclick="appendNumber('6')">6</button>
            <button class="operator" onclick="appendOperator('+')">+</button>

            <button class="num" onclick="appendNumber('1')">1</button>
            <button class="num" onclick="appendNumber('2')">2</button>
            <button class="num" onclick="appendNumber('3')">3</button>
            <button class="operator" onclick="deleteLastChar()">⌫</button>

            <button class="num" onclick="appendNumber('0')">0</button>
            <button class="decimal" onclick="appendDecimal()">.</button>
            <button class="equals" onclick="calculate()">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentValue = '0';
        let previousValue = '';
        let operation = '';
        let shouldResetDisplay = false;

        function updateDisplay() {
            display.textContent = currentValue;
        }

        function clearDisplay() {
            currentValue = '0';
            previousValue = '';
            operation = '';
            shouldResetDisplay = false;
            updateDisplay();
        }

        function appendNumber(num) {
            if (shouldResetDisplay) {
                currentValue = num;
                shouldResetDisplay = false;
            } else {
                currentValue = currentValue === '0' ? num : currentValue + num;
            }
            updateDisplay();
        }

        function appendDecimal() {
            if (shouldResetDisplay) {
                currentValue = '0.';
                shouldResetDisplay = false;
            } else if (!currentValue.includes('.')) {
                currentValue += '.';
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operation && !shouldResetDisplay) {
                calculate();
            }
            previousValue = currentValue;
            operation = op;
            shouldResetDisplay = true;
        }

        function deleteLastChar() {
            if (currentValue.length > 1) {
                currentValue = currentValue.slice(0, -1);
            } else {
                currentValue = '0';
            }
            updateDisplay();
        }

        function calculate() {
            if (!operation || !previousValue) return;

            const prev = parseFloat(previousValue);
            const curr = parseFloat(currentValue);
            let result;

            switch (operation) {
                case '+':
                    result = prev + curr;
                    break;
                case '-':
                    result = prev - curr;
                    break;
                case '*':
                    result = prev * curr;
                    break;
                case '/':
                    result = curr !== 0 ? prev / curr : 'Error';
                    break;
                default:
                    return;
            }

            currentValue = result.toString();
            operation = '';
            previousValue = '';
            shouldResetDisplay = true;
            updateDisplay();
        }
    </script>
</body>

</html>
