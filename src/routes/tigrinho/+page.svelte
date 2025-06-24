<script>
    import Roleta from '$lib/component/Roleta.svelte';
    import PremioLista from '$lib/component/PremioLista.svelte';
  
    let escolha = 'par'; // aposta do jogador
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
  </script>
  
  <style>
    main {
      max-width: 600px;
      margin: auto;
      padding: 2rem;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #1e3c72, #2a5298);
      color: #fff;
      border-radius: 20px;
      box-shadow: 0 0 20px #0008;
    }
  
    h1 {
      text-align: center;
      font-size: 2.2rem;
      margin-bottom: 1rem;
    }
  
    .creditos {
      text-align: center;
      font-size: 1.3rem;
      margin: 1rem 0;
    }
  
    .aposta {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 1rem;
    }
  
    .aposta button {
      background-color: #ffd700;
      border: none;
      padding: 0.8rem 1.5rem;
      border-radius: 10px;
      font-weight: bold;
      cursor: pointer;
      color: #222;
      transition: 0.3s;
    }
  
    .aposta button.active {
      background-color: #00ff88;
      color: #000;
    }
  
    button#girar {
      display: block;
      margin: 1rem auto;
      background-color: #00cfff;
      color: #000;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 10px;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      transition: transform 0.2s;
    }
  
    button#girar:hover {
      transform: scale(1.05);
    }
  
    ul {
      list-style: none;
      padding: 0;
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
    <h1>🎰 Tigrinho do PAL</h1>
  
    <div class="creditos">
      Créditos: <strong>{creditos}</strong>
    </div>
  
    <div class="aposta">
      <button
        class:active={escolha === 'par'}
        on:click={() => escolha = 'par'}
      >Par</button>
      <button
        class:active={escolha === 'impar'}
        on:click={() => escolha = 'impar'}
      >Ímpar</button>
    </div>
  
    <button id="girar" on:click={jogar} disabled={creditos <= 0}>
      Girar Roleta
    </button>
  
    <Roleta {resultado} {escolha} />
  
    {#if resultado !== null}
      <p class={((escolha === 'par' && resultado % 2 === 0) || (escolha === 'impar' && resultado % 2 !== 0)) ? 'ganhou' : 'perdeu'}>
        Resultado: <strong>{resultado}</strong> — 
        {resultado % 2 === 0 ? 'Par' : 'Ímpar'} —
        {((escolha === 'par' && resultado % 2 === 0) || (escolha === 'impar' && resultado % 2 !== 0)) 
          ? '🎉 Acertou!' 
          : '😢 Errou...'}
      </p>
    {/if}
  
    <PremioLista />
  
    <h3 style="margin-top: 1.5rem;">📜 Histórico:</h3>
    <ul>
      {#each historico.slice(0, 10) as h}
        <li>
          Número: {h.numero} | {h.numero % 2 === 0 ? 'Par' : 'Ímpar'} | 
          <span class={h.acertou ? 'ganhou' : 'perdeu'}>
            {h.acertou ? 'Ganhou' : 'Perdeu'}
          </span> | Saldo: {h.saldo}
        </li>
      {/each}
    </ul>
  </main>
  