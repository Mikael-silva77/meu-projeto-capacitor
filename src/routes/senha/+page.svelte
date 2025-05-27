<script>  
  let quantidade = 12; 
  let qtdSenhas = 1;
  let senhas = [];
  let incluirMaiusculas = true;
  let incluirMinusculas = true;
  let incluirNumeros = true;
  let incluirSimbolos = false;

  function gerarSenha() {
    const caracteresMaiusculos = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    const caracteresMinusculos = 'abcdefghijklmnopqrstuvwxyz';
    const numeros = '0123456789';
    const simbolos = '!@#$%^&*()-_=+[]{}|;:,.<>?';

    let caracteres = '';
    if (incluirMaiusculas) caracteres += caracteresMaiusculos;
    if (incluirMinusculas) caracteres += caracteresMinusculos;
    if (incluirNumeros) caracteres += numeros;
    if (incluirSimbolos) caracteres += simbolos;

    let senhaGerada = '';
    for (let i = 0; i < quantidade; i++) {
      senhaGerada += caracteres.charAt(Math.floor(Math.random() * caracteres.length));
    }
    return senhaGerada;
  }

  function gerarMultiplaSenha() {
    const novasSenhas = [];
    for (let i = 0; i < qtdSenhas; i++) {
      novasSenhas.push(gerarSenha());
    }
    senhas = novasSenhas;
  }

  function copiarSenha(senha) {
    navigator.clipboard.writeText(senha).then(() => {
      alert("Senha copiada para a área de transferência!");
    }).catch(err => {
      console.error("Erro ao copiar a senha: ", err);
    });
  }
</script>

<main class="main">
  <div class="content">
    <h1>Gerador de Senha</h1>

    <div class="options">
      <div class="slider-container">
        <label for="quantidadeSlider">Tamanho da Senha:</label>
        <input
          type="range"
          id="quantidadeSlider"
          min="4"
          max="20"
          bind:value={quantidade}
        />
        <span>{quantidade}</span>
      </div>

      <div class="input-container">
        <label for="quantidade">Número de Senhas:</label>
        <input type="number" bind:value={qtdSenhas} min="1" max="10" />
      </div>

      <div class="checkboxes">
        <label><input type="checkbox" checked={incluirMaiusculas} on:change={() => incluirMaiusculas = !incluirMaiusculas} /> Letras Maiúsculas</label>
        <label><input type="checkbox" checked={incluirMinusculas} on:change={() => incluirMinusculas = !incluirMinusculas} /> Letras Minúsculas</label>
        <label><input type="checkbox" checked={incluirNumeros} on:change={() => incluirNumeros = !incluirNumeros} /> Dígitos</label>
        <label><input type="checkbox" checked={incluirSimbolos} on:change={() => incluirSimbolos = !incluirSimbolos} /> Símbolos</label>
      </div>

      <button on:click={gerarMultiplaSenha}>Gerar Senhas</button>

      <div class="senha-container">
        {#if senhas.length === 0}
          <div class="senha-item">
            <span class="senha">{gerarSenha()}</span>
            <button on:click={() => copiarSenha(gerarSenha())}>Copiar</button>
          </div>
        {:else}
          <div>
            {#each senhas as senha}
              <div class="senha-item">
                <span class="senha">{senha}</span>
                <button on:click={() => copiarSenha(senha)}>Copiar</button>
              </div>
            {/each}
          </div>
        {/if}
      </div>
    </div>
  </div>
</main>

<style>
  .main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .content {
    text-align: center;
    background: linear-gradient(135deg, #f9c6d2 0%, #a7c7e7 100%);
    padding: 30px 40px;
    border-radius: 15px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    width: 380px;
    max-width: 100%;
    transition: all 0.3s ease;
  }

  h1 {
    color: #4b4b4b;
    font-size: 28px;
    margin-bottom: 25px;
    font-weight: 600;
    letter-spacing: 1px;
  }

  .options {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .slider-container {
    display: flex;
    justify-content: space-between;
    width: 100%;
    margin-bottom: 20px;
  }

  .slider-container input {
    width: 75%;
  }

  .slider-container span {
    font-size: 18px;
    color: #4b4b4b;
  }

  .input-container {
    width: 100%;
    margin-bottom: 20px;
  }

  .input-container label {
    display: block;
    font-size: 14px;
    color: #777;
    margin-bottom: 5px;
  }

  .input-container input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 8px;
    border: 1px solid #e0e0e0;
    text-align: center;
    background-color: #f0f0f0;
    transition: all 0.3s ease;
  }

  .input-container input:focus {
    border-color: #9fd2f4;
    background-color: #fff;
    box-shadow: 0 0 5px rgba(37, 117, 252, 0.4);
  }

  .checkboxes {
    width: 100%;
    text-align: left;
    margin-bottom: 20px;
  }

  .checkboxes label {
    display: block;
    font-size: 14px;
    color: #555;
    margin-top: 8px;
  }

  .senha-container {
    margin-top: 30px;
  }

  .senha-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
  }

  .senha {
    font-weight: bold;
    font-size: 18px;
    color: #4b4b4b;
    margin-right: 10px;
    word-wrap: break-word;
    padding: 10px;
    background-color: #f0f8ff;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease, transform 0.2s;
    max-width: 220px; 
    word-break: break-all; 
  }

  .senha:hover {
    background-color: #e1f5fe;
    transform: scale(1.05);
  }

  button {
    padding: 10px 15px;
    font-size: 14px;
    background-color: #384f81;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s;
    width: 80px;
  }

  button:hover {
    background-color: #8ab8d6;
  }

  button:active {
    transform: scale(0.98);
  }

  button:focus {
    outline: none;
  }

 
  @media (max-width: 480px) {
    .content {
      padding: 25px 20px;
      width: 90%;
    }

    .slider-container {
      flex-direction: column;
      align-items: stretch;
    }

    .slider-container input {
      width: 100%;
    }

    .input-container input {
      width: 100%;
    }
  }
</style>
