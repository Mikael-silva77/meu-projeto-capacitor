<script>
  import { dicionario, palavras, getRandomWord } from '$lib/dicio/data.js';
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  let termo = '';
  let filtro = '';
  let palavraDoDia = '';
  let filtradas = [];

  onMount(() => {
    palavraDoDia = getRandomWord();
    aplicarFiltro();
  });

  function aplicarFiltro() {
    filtradas = palavras.filter(p => p.startsWith(filtro.toLowerCase()));
  }

  function buscar() {
    const palavra = termo.toLowerCase();
    if (palavra in dicionario) {
      goto(`/dicionario/${palavra}`);
    }
  }

  function irPara(p) {
    goto(`/dicionario/${p}`);
  }
</script>

<style>
 main {
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background: linear-gradient(to bottom right, #d0f0ff, #e0fff5);
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  font-family: 'Segoe UI', sans-serif;
  color: #2d3436;
}
  main {
    max-width: 800px;
    margin: 2rem auto;
    padding: 2rem;
    background: #ffffff;
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  }

  h1 {
    font-size: 2.5rem;
    color: #2d3436;
    margin-bottom: 1rem;
    text-align: center;
  }

  h2, h3 {
    color: #0984e3;
    margin-top: 1.5rem;
  }

  section {
    margin-bottom: 2rem;
  }

  input {
    padding: 0.6rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    margin-right: 0.5rem;
    font-size: 1rem;
    width: 250px;
    transition: box-shadow 0.2s;
  }

  input:focus {
    outline: none;
    border-color: #00cec9;
    box-shadow: 0 0 5px #00cec9aa;
  }

  button {
    background: linear-gradient(to right, #00b894, #0984e3);
    color: white;
    border: none;
    padding: 0.6rem 1.2rem;
    font-size: 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: opacity 0.3s;
  }

  button:hover {
    opacity: 0.9;
  }

  a {
    color: #0984e3;
    cursor: pointer;
    text-decoration: underline;
    font-weight: 500;
  }

  a:hover {
    color: #00cec9;
  }

  ul {
    list-style: none;
    padding-left: 0;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    gap: 0.5rem;
  }

  li {
    background: #ecf0f1;
    padding: 0.5rem 1rem;
    border-radius: 8px;
    text-align: center;
    transition: background 0.2s;
  }

  li:hover {
    background: #dfe6e9;
  }
</style>

<main>
  <h1>Dicionário</h1>
  

  <section>
    <h2>
      Palavra do Dia: 
      <a on:click={() => irPara(palavraDoDia)}>{palavraDoDia}</a>
    </h2>
  </section>

  <section>
    <input bind:value={termo} placeholder="Digite uma palavra..." />
    <button on:click={buscar}>Buscar</button>

    <br /><br />

    <input
      bind:value={filtro}
      placeholder="Filtro por prefixo (ex: ab)"
      on:input={aplicarFiltro}
    />
  </section>

  <section>
    <h3>Palavras Encontradas ({filtradas.length})</h3>
    <ul>
      {#each filtradas as p}
        <li><a on:click={() => irPara(p)}>{p}</a></li>
      {/each}
    </ul>
  </section>
</main>
