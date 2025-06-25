<script>
  import { goto } from '$app/navigation';

</script>

<main>
  <h1>Tigrinho do PAL</h1>

  <button on:click={() => goto('tigrinho/par-impar')}>🔢 Par ou Ímpar</button>
  <button on:click={() => goto('tigrinho/sequencia')}>🎯 Jogo da Sequência</button>
  <button on:click={() => goto('tigrinho/dado')}>🎲 Girar o Dado</button>
</main>


<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(135deg, #6a11cb, #2575fc);
    min-height: 100vh;
    color: white;
  }
                                                                                                                                                                                                                                                                                 

  h1 {
    margin-bottom: 2rem;
    font-size: 2.5rem;
    color:#fffdfd;
  }

  button {
    padding: 1.2rem 2rem;
    font-size: 1.2rem;
    background: #ffd700;
    border: none;
    border-radius: 10px;
    font-weight: bold;
    color: #222;
    cursor: pointer;
    transition: 0.3s;
    margin-bottom: 1rem;
    width: 220px;
  }

  button:hover {
    background: #00ff88;
    color: #000;
  }
</style>
