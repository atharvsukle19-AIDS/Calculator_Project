<!doctype html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Colorful Calculator</title>
  <style>
    body {
      background: linear-gradient(135deg, #1E1E1E, #2E2E2E);
      font-family: 'Poppins', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .calculator {
      background: #222;
      border-radius: 20px;
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.6);
      width: 320px;
      padding: 20px;
    }

    .display {
      background: #111;
      color: #00FFAA;
      font-size: 2em;
      padding: 20px;
      border-radius: 12px;
      text-align: right;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
      margin-top: 20px;
    }

    button {
      border: none;
      border-radius: 12px;
      padding: 20px;
      font-size: 1.2em;
      font-weight: bold;
      color: white;
      cursor: pointer;
      transition: all 0.15s ease;
    }

    /* Colorful buttons */
    .num {
      background-color: #333;
    }

    .op {
      background-color: #00BFFF;
    }

    .eq {
      background-color: #FF6347;
      grid-column: span 2;
    }

    .clr {
      background-color: #4CAF50;
      grid-column: span 2;
    }

    /* Hover and active effects */
    button:hover {
      filter: brightness(1.2);
    }

    button:active {
      transform: scale(0.95);
      filter: brightness(1.4);
    }

    @media (max-width: 400px) {
      .calculator {
        width: 90%;
      }

      .display {
        font-size: 1.6em;
      }
    }
  </style>
</head>

<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clr" onclick="playClick(); clearDisplay()">C</button>
      <button class="op" onclick="playClick(); inputValue('/')">÷</button>
      <button class="op" onclick="playClick(); inputValue('*')">×</button>
      <button class="num" onclick="playClick(); inputValue('7')">7</button>
      <button class="num" onclick="playClick(); inputValue('8')">8</button>
      <button class="num" onclick="playClick(); inputValue('9')">9</button>
      <button class="op" onclick="playClick(); inputValue('-')">−</button>
      <button class="num" onclick="playClick(); inputValue('4')">4</button>
      <button class="num" onclick="playClick(); inputValue('5')">5</button>
      <button class="num" onclick="playClick(); inputValue('6')">6</button>
      <button class="op" onclick="playClick(); inputValue('+')">+</button>
      <button class="num" onclick="playClick(); inputValue('1')">1</button>
      <button class="num" onclick="playClick(); inputValue('2')">2</button>
      <button class="num" onclick="playClick(); inputValue('3')">3</button>
      <button class="eq" onclick="playClick(); calculate()">=</button>
      <button class="num" onclick="playClick(); inputValue('0')">0</button>
      <button class="num" onclick="playClick(); inputValue('.')">.</button>
    </div>
  </div>

  <!-- Button click sound -->
  <audio id="clickSound"
    src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_eecc38acb6.mp3?filename=click-button-140881.mp3"></audio>

  <script>
    const display = document.getElementById('display');
    const clickSound = document.getElementById('clickSound');
    let expression = '';
    const operators = ['+', '-', '*', '/'];

    function playClick() {
      try { clickSound.currentTime = 0; clickSound.play(); } catch (e) { /* ignore autoplay issues */ }
    }

    function inputValue(value) {
      const last = expression.slice(-1);

      if (operators.includes(value)) {
        // Don't allow starting expression with an operator except minus
        if (expression === '' && value !== '-') return;
        // Replace last operator if user enters two operators in a row
        if (operators.includes(last)) {
          expression = expression.slice(0, -1) + value;
        } else {
          expression += value;
        }
      } else if (value === '.') {
        // Prevent multiple decimals in the current number
        const parts = expression.split(/[-+*/]/);
        const current = parts[parts.length - 1];
        if (current.includes('.')) return;
        if (current === '') expression += '0.'; else expression += '.';
      } else {
        // digits
        expression += value;
      }

      display.textContent = expression || '0';
    }

    function clearDisplay() {
      expression = '';
      display.textContent = '0';
    }

    function calculate() {
      try {
        if (expression === '') return;
        // Basic validation: allow only digits, operators, parentheses, dot and spaces
        if (!/^[0-9+\-*/().\s]+$/.test(expression)) throw new Error('Invalid expression');
        // If expression ends with operator, strip it
        if (operators.includes(expression.slice(-1))) expression = expression.slice(0, -1);
        // Use Function to evaluate in a safer controlled way than raw eval
        const result = Function('"use strict"; return (' + expression + ')')();
        if (!Number.isFinite(result)) throw new Error('Math error');
        expression = result.toString();
        display.textContent = expression;
      } catch (e) {
        display.textContent = 'Error';
        expression = '';
      }
    }

    // Keyboard support
    window.addEventListener('keydown', (e) => {
      if ((e.key >= '0' && e.key <= '9') || operators.includes(e.key) || e.key === '.') {
        e.preventDefault();
        inputValue(e.key === '/' ? '/' : e.key);
      } else if (e.key === 'Enter') {
        e.preventDefault();
        calculate();
      } else if (e.key === 'Backspace') {
        e.preventDefault();
        expression = expression.slice(0, -1);
        display.textContent = expression || '0';
      } else if (e.key === 'Escape') {
        e.preventDefault();
        clearDisplay();
      }
    });
  </script>
</body>

</html>
