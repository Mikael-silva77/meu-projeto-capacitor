<script>
  let temperaturaEntrada = 0;
  let unidadeEntrada = 'C';
  let unidadeSaida = 'F';
  let resultado = 0;

  const unidadesTemperatura = ['C', 'F', 'K'];

  function converterTemperatura() {
    if (unidadeEntrada === 'C' && unidadeSaida === 'F') {
      resultado = (temperaturaEntrada * 9/5) + 32;
    } else if (unidadeEntrada === 'C' && unidadeSaida === 'K') {
      resultado = temperaturaEntrada + 273.15;
    } else if (unidadeEntrada === 'F' && unidadeSaida === 'C') {
      resultado = (temperaturaEntrada - 32) * 5/9;
    } else if (unidadeEntrada === 'F' && unidadeSaida === 'K') {
      resultado = (temperaturaEntrada - 32) * 5/9 + 273.15;
    } else if (unidadeEntrada === 'K' && unidadeSaida === 'C') {
      resultado = temperaturaEntrada - 273.15;
    } else if (unidadeEntrada === 'K' && unidadeSaida === 'F') {
      resultado = (temperaturaEntrada - 273.15) * 9/5 + 32;
    }
  }
</script>

<main>
  <h1>Conversor de Temperatura</h1>
  <div>
    <label for="temperaturaEntrada">Temperatura:</label>
    <input type="number" id="temperaturaEntrada" bind:value={temperaturaEntrada} />
  </div>
  <div>
    <label for="unidadeEntrada">De:</label>
    <select id="unidadeEntrada" bind:value={unidadeEntrada}>
      {#each unidadesTemperatura as unidade}
        <option value={unidade}>{unidade}</option>
      {/each}
    </select>
  </div>
  <div>
    <label for="unidadeSaida">Para:</label>
    <select id="unidadeSaida" bind:value={unidadeSaida}>
      {#each unidadesTemperatura as unidade}
        <option value={unidade}>{unidade}</option>
      {/each}
    </select>
  </div>
  <button on:click={converterTemperatura}>Converter</button>

  {#if resultado}
    <p>Resultado: {resultado} {unidadeSaida}</p>
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 2rem;
  }

  div {
    margin: 1rem 0;
  }

  input, select {
    margin-left: 1rem;
  }

  button {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #45a049;
  }
</style>
