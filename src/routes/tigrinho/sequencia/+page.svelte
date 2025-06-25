<script>
	import { goto } from "$app/navigation";

    let min = 1,
      max = 100;
    let inicio = 1,
      fim = 5;
    let resultado = null;
    let creditos = 100;
    let historico = [];
  
    function jogar() {
      const numero = Math.floor(Math.random() * (max - min + 1)) + min;
      resultado = numero;
  
      const acertou = numero >= inicio && numero <= fim;
      creditos += acertou ? 10 : -10;
  
      historico.unshift({ numero, acertou, saldo: creditos, intervalo: [inicio, fim] });
    }

 function voltar() {
    if (history.lenght > 1 ){
        history.back();
    }else{
        goto('/tigrinho')
    }
    }
 
  </script>
  
  <style>
    main {
      max-width: 600px;
      margin: 2rem auto;
      padding: 2rem;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #6a11cb, #2575fc);
      color: #fff;
      border-radius: 20px;
      box-shadow: 0 0 20px #0008;
      text-align: center;
    }
  
    h1 {
      font-size: 2.4rem;
      margin-bottom: 1.5rem;
    }
  
    p {
      font-size: 1.3rem;
      margin: 1rem 0;
    }
  
    div {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 0.6rem;
      margin-bottom: 1.2rem;
    }
  
    input[type='number'] {
      width: 80px;
      padding: 0.5rem 0.8rem;
      font-size: 1.1rem;
      border-radius: 8px;
      border: none;
      text-align: center;
      outline: none;
      box-shadow: inset 0 0 5px #00000088;
      transition: box-shadow 0.3s;
    }
  
    input[type='number']:focus {
      box-shadow: inset 0 0 8px #00ff88cc;
    }

    .ganho {
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
  
    .perdo {
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
  
    button:hover:not(:disabled) {
      background-color: #00ff88;
    }
  
    button:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  
    .ganhou {
      color: #00ff88;
      font-weight: bold;
      margin-top: 1rem;
      font-size: 1.4rem;
    }
  
    .perdeu {
      color: #ff5555;
      font-weight: bold;
      margin-top: 1rem;
      font-size: 1.4rem;
    }
  
    ul {
      list-style: none;
      padding: 0;
      margin-top: 1.5rem;
      max-height: 220px;
      overflow-y: auto;
      text-align: left;
    }
  
    li {
      padding: 0.3rem 0;
      border-bottom: 1px solid #ffffff33;
    }
  </style>
  



  <main>
    <h1>Tigrinho do PAL 🎰</h1>
    <h1>🎯 Jogo da Sequência</h1>
  
    <p>Créditos: <strong>{creditos}</strong></p>
  
    <p>Escolha intervalo (máx 5 números):</p>
    <div>
      <input
        type="number"
        min={min}
        max={max}
        bind:value={inicio}
        aria-label="Número inicial do intervalo"
      />
      até
      <input
        type="number"
        min={min}
        max={max}
        bind:value={fim}
        aria-label="Número final do intervalo"
      />
    </div>
  
    <button class="perdo" on:click={jogar} disabled={creditos <= 0 || fim - inicio > 4 || inicio > fim}>
      Jogar
    </button>
  
    {#if resultado !== null}
      <p class={(resultado >= inicio && resultado <= fim) ? 'ganhou' : 'perdeu'}>
        Número sorteado: <strong>{resultado}</strong> — 
        {(resultado >= inicio && resultado <= fim) ? '🎉 Acertou!' : '😢 Errou...'}
      </p>
    {/if}
   
    <center><button class="ganho" on:click={voltar}> Voltar</button></center>

  
  </main>

  