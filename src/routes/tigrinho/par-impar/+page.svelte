<script>
    import { goto } from '$app/navigation';
    import Roleta from '$lib/component/Roleta.svelte';
    import PremioLista from '$lib/component/PremioLista.svelte';
  
    let escolha = 'par';
    let resultado = null;
    let creditos = 100;
    let historico = [];
  
    function jogar() {
      const numero = Math.floor(Math.random() * 100) + 1;
      resultado = numero;
  
      const acertou =
        (escolha === 'par' && numero % 2 === 0) ||
        (escolha === 'impar' && numero % 2 !== 0);
  
      creditos += acertou ? 10 : -10;
  
      historico.unshift({
        numero,
        acertou,
        saldo: creditos
      });
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
      font-size: 2.4rem;
      margin-bottom: 1.5rem;
    }
  
    p {
      font-size: 1.3rem;
      margin: 1rem 0;
    }
  
    .aposta {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 1.5rem;
    }
  
    .aposta button {
      background-color: #ffd700;
      border: none;
      padding: 0.8rem 1.5rem;
      border-radius: 10px;
      font-weight: bold;
      cursor: pointer;
      color: #222;
      transition: background-color 0.3s;
      font-size: 1.1rem;
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
    }
  
    .aposta button.active {
      background-color: #00ff88;
      color: #000;
    }
  
    button#girar {
      background-color: #00cfff;
      color: #000;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 10px;
      font-size: 1.2rem;
      font-weight: bold;
      cursor: pointer;
      margin-bottom: 1.5rem;
      transition: transform 0.2s, background-color 0.3s;
    }
  
    button#girar:hover:not(:disabled) {
      transform: scale(1.05);
      background-color: #00a0cc;
    }
  
    button#girar:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  
    button#voltar {
      background-color: #ff5555;
      color: #fff;
      border: none;
      padding: 0.6rem 1.5rem;
      border-radius: 10px;
      font-weight: bold;
      cursor: pointer;
      font-size: 1rem;
      transition: background-color 0.3s;
    }
  
    button#voltar:hover {
      background-color: #cc4444;
    }
  
    ul {
      list-style: none;
      padding: 0;
      max-height: 220px;
      overflow-y: auto;
      margin-top: 1.5rem;
      text-align: left;
    }
  
    li {
      padding: 0.3rem 0;
      border-bottom: 1px solid #ffffff33;
    }
  
    .ganhou {
      color: #00ff88;
      font-weight: bold;
    }
  
    .perdeu {
      color: #ff5555;
      font-weight: bold;
    }
  </style>
  
  <main>
    <h1> Tigrinho do PAL 🎰 </h1>
    <h1>Par ou Ímpar</h1>
    <p>Créditos: <strong>{creditos}</strong></p>
  
    <div class="aposta">
      <button
        class:active={escolha === 'par'}
        on:click={() => (escolha = 'par')}
      >Par</button>
      <button
        class:active={escolha === 'impar'}
        on:click={() => (escolha = 'impar')}
      >Ímpar</button>
    </div>
  
    <button id="girar" on:click={jogar} disabled={creditos <= 0}>
      Girar Roleta
    </button>
  
    <Roleta {resultado} {escolha} />
  
    {#if resultado !== null}
      <p class={historico[0].acertou ? 'ganhou' : 'perdeu'}>
        Resultado: <strong>{resultado}</strong> — 
        {resultado % 2 === 0 ? 'Par' : 'Ímpar'} — 
        {historico[0].acertou ? '🎉 Acertou!' : '😢 Errou...'}
      </p>
    {/if}
  
    <PremioLista />
  
    
  
    <button class="ganho" on:click={voltar}> Voltar</button>
  
  </main>
  