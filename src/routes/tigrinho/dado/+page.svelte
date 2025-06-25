<script>
    let escolha = 1;
    let resultado = null;
    let creditos = 100;
    let historico = [];
  
    function girarDado() {
      const numero = Math.floor(Math.random() * 6) + 1;
      resultado = numero;
  
      const acertou = numero === escolha;
      creditos += acertou ? 20 : -5;
  
      historico.unshift({
        numero,
        acertou,
        saldo: creditos,
        escolha
      });
    }

    function voltar() {
    if (history.lenght >= 0 ){
        goto('/tigrinho');
    }else{
        history.back();

    }
    }
 
  </script>
  
  <style>
    main {
      max-width: 600px;
      margin: auto;
      padding: 2rem;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #6a11cb, #2575fc);
      color: #fff;
      border-radius: 20px;
      box-shadow: 0 0 20px #0008;
      text-align: center;
    }
  
    h1 {
      font-size: 2.2rem;
      margin-bottom: 1rem;
    }
  
    select {
      font-size: 1.1rem;
      padding: 0.5rem 1rem;
      border-radius: 8px;
      border: none;
      margin-bottom: 1rem;
      cursor: pointer;
    }

    .pedro{
      background-color: #ffd700;
      color: #000;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 10px;
      font-size: 1.2rem;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
    }
  
    .paulo{
      background-color: #ffd700;
      color: #000;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 10px;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
    }
  
    button:hover:not(:disabled) {
      background-color: #00ff88;
    }
  
    button:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }
  
    .resultado {
      margin-top: 1rem;
      font-size: 1.5rem;
      font-weight: bold;
    }

    .pedro {
      background-color: #ff1e00;
      color: #000;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 10px;
      font-size: 1.2rem;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-top: 15px;
    }
  
    .ganhou {
      color: #00ff88;
    }
  
    .perdeu {
      color: #ff5555;
    }
  
    ul {
      list-style: none;
      padding: 0;
      margin-top: 1.5rem;
      max-height: 200px;
      overflow-y: auto;
    }
  
    li {
      padding: 0.3rem 0;
      border-bottom: 1px solid #ffffff33;
    }
  </style>
  
  <main>
    <h1>Tigrinho do PAL</h1>
    <h1>🎲 Escolha o Número e Gire o Dado</h1>
  
    <p>Créditos: <strong>{creditos}</strong></p>
  
    <label for="escolha">Escolha um número de 1 a 6:</label><br />
    <select id="escolha" bind:value={escolha}>
      {#each Array(6) as _, i}
        <option value={i + 1}>{i + 1}</option>
      {/each}
    </select>
  
    <br />
  
    <button class="paulo" on:click={girarDado} disabled={creditos <= 0}>
      Girar Dado
    </button>
  
    {#if resultado !== null}
      <p class="resultado {resultado === escolha ? 'ganhou' : 'perdeu'}">
        Resultado: <strong>{resultado}</strong> — 
        {resultado === escolha ? '🎉 Você ganhou +20 créditos!' : '😢 Você perdeu 5 créditos.'}
      </p>
    {/if}
  
      <center> <button class='pedro' on:click={voltar}> Voltar</button></center>

  </main>

  