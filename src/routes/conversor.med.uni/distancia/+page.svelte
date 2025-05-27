<script>
  let distanciaEntrada = 0;
  let unidadeEntrada = 'm';
  let unidadeSaida = 'km';
  let resultado = 0;

  const unidadesDistancia = ['m', 'km', 'cm', 'mm'];

  function converterDistancia() {
      if (unidadeEntrada === 'm' && unidadeSaida === 'km') {
          resultado = distanciaEntrada / 1000;
      } else if (unidadeEntrada === 'm' && unidadeSaida === 'cm') {
          resultado = distanciaEntrada * 100;
      } else if (unidadeEntrada === 'm' && unidadeSaida === 'mm') {
          resultado = distanciaEntrada * 1000;
      } else if (unidadeEntrada === 'km' && unidadeSaida === 'm') {
          resultado = distanciaEntrada * 1000;
      } else if (unidadeEntrada === 'km' && unidadeSaida === 'cm') {
          resultado = distanciaEntrada * 100000;
      } else if (unidadeEntrada === 'km' && unidadeSaida === 'mm') {
          resultado = distanciaEntrada * 1000000;
      }
  }
</script>

<main>
  <h1>Conversor de Distância</h1>
  <div class="input-container">
      <label for="distanciaEntrada">Distância:</label>
      <input type="number" id="distanciaEntrada" bind:value={distanciaEntrada} placeholder="Digite a distância" />
  </div>
  <div class="select-container">
      <label for="unidadeEntrada">De:</label>
      <select id="unidadeEntrada" bind:value={unidadeEntrada}>
          {#each unidadesDistancia as unidade}
              <option value={unidade}>{unidade}</option>
          {/each}
      </select>
  </div>
  <div class="select-container">
      <label for="unidadeSaida">Para:</label>
      <select id="unidadeSaida" bind:value={unidadeSaida}>
          {#each unidadesDistancia as unidade}
              <option value={unidade}>{unidade}</option>
          {/each}
      </select>
  </div>
  <button class="converter-btn" on:click={converterDistancia}>Converter</button>
  {#if resultado}
      <p class="resultado">Resultado: {resultado}</p>
  {/if}
</main>

<style>

  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }



  main {
      text-align: center;
      padding: 2rem;
      background-color: #ffffff;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      width: 100%;
      max-width: 400px;
  }

  h1 {
      font-size: 2rem;
      margin-bottom: 1.5rem;
      color: #0056b3;
  }

  .input-container, .select-container {
      margin: 1rem 0;
      display: flex;
      justify-content: center;
      align-items: center;
  }

  label {
      font-size: 1.1rem;
      margin-right: 1rem;
      color: #555;
  }

  input, select {
      padding: 0.5rem;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      outline: none;
  }

  input:focus, select:focus {
      border-color: #0056b3;
  }

  .converter-btn {
      background-color: #0056b3;
      color: #fff;
      padding: 0.7rem 2rem;
      font-size: 1.1rem;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      transition: background-color 0.3s ease;
  }

  .converter-btn:hover {
      background-color: #003d7a;
  }

  .resultado {
      margin-top: 1.5rem;
      font-size: 1.2rem;
      font-weight: bold;
      color: #28a745;
  }
</style>
