<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Simple Calculator</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #f2f2f2;
      font-family: Arial, sans-serif;
    }
    .calculator {
      background: #ffffff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
      width: 260px;
    }
    .display {
      width: 100%;
      height: 50px;
      margin-bottom: 10px;
      text-align: right;
      padding: 10px;
      font-size: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }
    button {
      padding: 15px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background: #e0e0e0;
    }
    button.operator {
      background: #ff9500;
      color: white;
    }
    button.equal {
      background: #34c759;
      color: white;
      grid-column: span 2;
    }
    button.clear {
      background: #ff3b30;
      color: white;
    }
  </style>
</head>
<body>
  <div class="calculator">
    <input type="text" id="display" class="display" disabled />
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">C</button>
      <button onclick="appendValue('/')">/</button>
      <button onclick="appendValue('*')">*</button>
      <button class="operator" onclick="appendValue('-')">-</button>

      <button onclick="appendValue('7')">7</button>
      <button onclick="appendValue('8')">8</button>
      <button onclick="appendValue('9')">9</button>
      <button class="operator" onclick="appendValue('+')">+</button>

      <button onclick="appendValue('4')">4</button>
      <button onclick="appendValue('5')">5</button>
      <button onclick="appendValue('6')">6</button>
      <button onclick="appendValue('.')">.</button>

      <button onclick="appendValue('1')">1</button>
      <button onclick="appendValue('2')">2</button>
      <button onclick="appendValue('3')">3</button>
      <button class="equal" onclick="calculate()">=</button>

      <button onclick="appendValue('0')">0</button>
    </div>
  </div>

  <script>
    const display = document.getElementById('display');

    function appendValue(value) {
      display.value += value;
    }

    function clearDisplay() {
      display.value = '';
    }

    function calculate() {
      try {
        display.value = eval(display.value);
      } catch (error) {
        display.value = 'Error';
      }
    }
  

    // Keyboard support
    document.addEventListener('keydown', function (event) {
      const key = event.key;

      if (!isNaN(key) || key === '.') {
        appendValue(key);
      } else if (key === '+' || key === '-' || key === '*' || key === '/') {
        
        appendValue(key);
      } else if (key === 'Enter' || key === '=') {
        event.preventDefault();
        calculate();
      } else if (key === 'Backspace') {
        display.value = display.value.slice(0, -1);
      } else if (key === 'Escape') {
        clearDisplay();
      }
    });
  </script>
</body>
</html>
