<script>
    let velocidadeEntrada = 0;
    let unidadeEntrada = 'km/h';
    let unidadeSaida = 'm/s';
    let resultado = 0;
  
    const unidadesVelocidade = ['km/h', 'm/s', 'mi/h', 'ft/s'];
  
    function converterVelocidade() {
      if (unidadeEntrada === 'km/h' && unidadeSaida === 'm/s') {
        resultado = velocidadeEntrada / 3.6;
      } else if (unidadeEntrada === 'km/h' && unidadeSaida === 'mi/h') {
        resultado = velocidadeEntrada / 1.60934;
      } else if (unidadeEntrada === 'm/s' && unidadeSaida === 'km/h') {
        resultado = velocidadeEntrada * 3.6;
      } else if (unidadeEntrada === 'm/s' && unidadeSaida === 'mi/h') {
        resultado = velocidadeEntrada * 2.23694;
      }
    }
  </script>
  
  <main>
    <h1>Conversor de Velocidade</h1>
    <div>
      <label for="velocidadeEntrada">Velocidade:</label>
      <input type="number" id="velocidadeEntrada" bind:value={velocidadeEntrada} />
    </div>
    <div>
      <label for="unidadeEntrada">De:</label>
      <select id="unidadeEntrada" bind:value={unidadeEntrada}>
        {#each unidadesVelocidade as unidade}
          <option value={unidade}>{unidade}</option>
        {/each}
      </select>
    </div>
    <div>
      <label for="unidadeSaida">Para:</label>
      <select id="unidadeSaida" bind:value={unidadeSaida}>
        {#each unidadesVelocidade as unidade}
          <option value={unidade}>{unidade}</option>
        {/each}
      </select>
    </div>
    <button on:click={converterVelocidade}>Converter</button>
    {#if resultado}
      <p>Resultado: {resultado}</p>
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
  </style>