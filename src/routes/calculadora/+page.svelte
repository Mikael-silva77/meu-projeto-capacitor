<script>
    let display = '0';
    let memory = 0;
  
    function append(value) {
      if (display === '0' || display === 'Erro') {
        display = value;
      } else {
        display += value;
      }
    }
  
    function clear() {
      display = '0';
    }
  
    function clearEntry() {
      display = '0';
    }
  
    function backspace() {
      display = display.length > 1 ? display.slice(0, -1) : '0';
    }
  
    function calculate() {
      try {
        display = eval(display.replace('×', '*').replace('÷', '/').replace(',', '.')).toString().replace('.', ',');
      } catch {
        display = 'Erro';
      }
    }
  
    function square() {
      try {
        display = (Math.pow(parseFloat(display.replace(',', '.')), 2)).toString().replace('.', ',');
      } catch {
        display = 'Erro';
      }
    }
  
    function sqrt() {
      try {
        display = (Math.sqrt(parseFloat(display.replace(',', '.')))).toString().replace('.', ',');
      } catch {
        display = 'Erro';
      }
    }
  
    function inverse() {
      try {
        display = (1 / parseFloat(display.replace(',', '.'))).toString().replace('.', ',');
      } catch {
        display = 'Erro';
      }
    }
  
    function toggleSign() {
      try {
        display = (parseFloat(display.replace(',', '.')) * -1).toString().replace('.', ',');
      } catch {
        display = 'Erro';
      }
    }
  
    // Memória
    function memoryClear() {
      memory = 0;
    }
  
    function memoryRecall() {
      display = memory.toString().replace('.', ',');
    }
  
    function memoryStore() {
      memory = parseFloat(display.replace(',', '.'));
    }
  
    function memoryAdd() {
      memory += parseFloat(display.replace(',', '.'));
    }
  
    function memorySubtract() {
      memory -= parseFloat(display.replace(',', '.'));
    }
  </script>
  
  <style>
    .calculator {
      width: 100%;
      max-width: 400px;
      margin: auto;
      margin-top: 2rem;
      padding: 1rem;
      border-radius: 1rem;
      background: #f3f6fb;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.15);
      font-family: system-ui, sans-serif;
    }
  
    .display {
      font-size: 2.5rem;
      text-align: right;
      padding: 1rem;
      background: white;
      border-radius: 0.75rem;
      margin-bottom: 1rem;
      border: 1px solid #ccc;
      overflow-x: auto;
    }
  
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 0.5rem;
    }
  
    button {
      font-size: 1.2rem;
      padding: 1.2rem;
      border: none;
      border-radius: 0.75rem;
      background: #ffffff;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      color: #000;
      transition: background 0.2s;
      width: 100%;
      height: 100%;
    }
  
    button:active {
      background: #d0d0d0;
    }
  
    .operator {
      background: #e3e8f0;
      color: #0078d7;
      font-weight: bold;
    }
  
    .equals {
      background: #0078d7;
      color: white;
      font-weight: bold;
    }
  
    @media (max-width: 480px) {
      .calculator {
        padding: 0.5rem;
      }
  
      .display {
        font-size: 2rem;
        padding: 0.75rem;
      }
  
      button {
        font-size: 1rem;
        padding: 1rem;
      }
    }
  </style>
  
  <div class="calculator">
    <div class="display">{display}</div>
    <div class="buttons">
      <button on:click={memoryClear}>MC</button>
      <button on:click={memoryRecall}>MR</button>
      <button on:click={memoryAdd}>M+</button>
      <button on:click={memorySubtract}>M−</button>
  
      <button on:click={memoryStore}>MS</button>
      <button on:click={clearEntry}>CE</button>
      <button on:click={clear}>C</button>
      <button on:click={backspace}>⌫</button>
  
      <button on:click={inverse}>1/x</button>
      <button on:click={square}>x²</button>
      <button on:click={sqrt}>√x</button>
      <button class="operator" on:click={() => append('÷')}>÷</button>
  
      <button on:click={() => append('7')}>7</button>
      <button on:click={() => append('8')}>8</button>
      <button on:click={() => append('9')}>9</button>
      <button class="operator" on:click={() => append('×')}>×</button>
  
      <button on:click={() => append('4')}>4</button>
      <button on:click={() => append('5')}>5</button>
      <button on:click={() => append('6')}>6</button>
      <button class="operator" on:click={() => append('-')}>−</button>
  
      <button on:click={() => append('1')}>1</button>
      <button on:click={() => append('2')}>2</button>
      <button on:click={() => append('3')}>3</button>
      <button class="operator" on:click={() => append('+')}>+</button>
  
      <button on:click={toggleSign}>±</button>
      <button on:click={() => append('0')}>0</button>
      <button on:click={() => append(',')}>,</button>
      <button class="equals" on:click={calculate}>=</button>
    </div>
  </div>
  