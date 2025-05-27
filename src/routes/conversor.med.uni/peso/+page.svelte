<script>
  let pesoEntrada = 0;
  let unidadeEntrada = 'kg';
  let unidadeSaida = 'lb';
  let resultado = 0;

  const unidadesPeso = ['kg', 'lb', 'g', 'oz'];

  function converterPeso() {
      if (unidadeEntrada === 'kg' && unidadeSaida === 'lb') {
          resultado = pesoEntrada * 2.20462;
      } else if (unidadeEntrada === 'kg' && unidadeSaida === 'g') {
          resultado = pesoEntrada * 1000;
      } else if (unidadeEntrada === 'lb' && unidadeSaida === 'kg') {
          resultado = pesoEntrada / 2.20462;
      } else if (unidadeEntrada === 'lb' && unidadeSaida === 'g') {
          resultado = (pesoEntrada / 2.20462) * 1000;
      }
  }
</script>

<main>
  <div class="conversor">
      <h1>Conversor de Peso</h1>
      <div class="grupo-entrada">
          <input type="number" id="pesoEntrada" bind:value={pesoEntrada} placeholder="Digite o peso" on:input={converterPeso} />
          <select id="unidadeEntrada" bind:value={unidadeEntrada} on:change={converterPeso}>
              {#each unidadesPeso as unidade}
                  <option value={unidade}>{unidade}</option>
              {/each}
          </select>
      </div>
      <span class="igual">=</span>
      <div class="grupo-entrada">
          <input type="number" id="resultado" bind:value={resultado} readonly placeholder="Resultado" />
          <select id="unidadeSaida" bind:value={unidadeSaida} on:change={converterPeso}>
              {#each unidadesPeso as unidade}
                  <option value={unidade}>{unidade}</option>
              {/each}
          </select>
      </div>
      {#if resultado}
          <p class="resultado">Resultado: {resultado.toFixed(3)}</p>
      {/if}
  </div>
</main>

<style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }

main {
      height: 100%;
      font-family: 'Arial', sans-serif;
      background-color: #f4f4f9;
      display: flex;
      justify-content: center;
      align-items: center;
      color: #333;
  }

  main {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      width: 100%;
  }

  .conversor {
      background: #fff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 350px;
      transition: transform 0.3s ease;
  }

  .conversor:hover {
      transform: scale(1.05);
  }

  h1 {
      color: #333;
      margin-bottom: 20px;
      font-size: 1.8rem;
      font-weight: bold;
  }

  .grupo-entrada {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 15px;
      margin: 15px 0;
  }

  input,
  select {
      padding: 12px;
      border-radius: 8px;
      border: 2px solid #ccc;
      font-size: 1.1rem;
      text-align: center;
      background-color: #f9f9f9;
      outline: none;
      transition: border-color 0.3s;
      width: 120px; 
  }

  input:focus,
  select:focus {
      border-color: #4CAF50;
  }

  .igual {
      font-size: 2rem;
      font-weight: bold;
      color: #333;
  }

  .resultado {
      margin-top: 20px;
      font-size: 1.2rem;
      font-weight: bold;
      color: #4CAF50;
  }

  select {
      cursor: pointer;
  }

 
  @media (max-width: 600px) {
      .conversor {
          width: 90%;
          padding: 20px;
      }

      h1 {
          font-size: 1.5rem;
      }

      .grupo-entrada {
          flex-direction: column;
          gap: 10px;
      }

      input, select {
          width: 100%; 
      }

      .igual {
          font-size: 1.5rem;
      }

      .resultado {
          font-size: 1rem;
      }
  }
</style>
