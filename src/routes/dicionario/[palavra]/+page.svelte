<script>
  export let data;
  import { goto } from '$app/navigation';
  import { dicionario as baseDicionario } from '$lib/dicio/data.js';

  let partes = [];

  if (data.definicao) {
    partes = data.definicao.split(/(\b[\wçÇáéíóúãõâêîôûàèìòùü]+\b)/);
  }

  function clicarPalavra(p) {
    const termo = p.toLowerCase();
    if (termo in baseDicionario) {
      goto(`/dicionario/${termo}`);
    }
  }

  function voltar() {
    if (history.length > 1) {
      history.back();
    } else {
      goto('/dicionario');
    }
  }
</script>

<style>
  main {
    max-width: 700px;
    margin: 2rem auto;
    padding: 2rem;
    background: linear-gradient(to bottom right, #e0f7fa, #ffffff);
    border-radius: 16px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
    font-family: 'Segoe UI', sans-serif;
  }

  .voltar {
    margin-bottom: 1.5rem;
    padding: 0.6rem 1.2rem;
    background: linear-gradient(to right, #00b894, #0984e3);
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1rem;
    transition: opacity 0.3s;
  }

  .voltar:hover {
    opacity: 0.85;
  }

  h1 {
    font-size: 2.4rem;
    color: #2d3436;
    margin-bottom: 1rem;
    text-align: center;
  }

  .definicao {
    font-size: 1.2rem;
    line-height: 1.7;
    color: #34495e;
    background: #ecf0f1;
    padding: 1rem;
    border-radius: 12px;
  }

  .definicao a {
    color: #0984e3;
    cursor: pointer;
    text-decoration: underline;
    font-weight: 600;
    transition: color 0.2s;
  }

  .definicao a:hover {
    color: #00cec9;
  }

  .mensagem-erro {
    font-size: 1.1rem;
    color: #c0392b;
    background: #fbeee6;
    padding: 1rem;
    border-radius: 12px;
    text-align: center;
  }
</style>

<main>
  <button on:click={voltar} class="voltar">⟵ Voltar</button>

  <h1>{data.termo}</h1>

  {#if data.definicao}
    <p class="definicao">
      {#each partes as parte}
        {#if baseDicionario[parte.toLowerCase().replace(/[^\wçÇáéíóúãõâêîôûàèìòùü]/gi, '')]}
          <a on:click={() => clicarPalavra(parte)}>{parte}</a>
        {:else}
          {parte}
        {/if}
      {/each}
    </p>
  {:else}
    <p class="mensagem-erro">Palavra não encontrada no dicionário.</p>
  {/if}
</main>
