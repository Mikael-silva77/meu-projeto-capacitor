

<script>
  
</script>

<main class="welcome-page">
  <h1>Bem-vindo ao Conversor de Unidades!</h1>
  <p>Escolha uma das opções abaixo para começar a usar o conversor de unidades:</p>
  <div class="links">
    <a href="/conversor.med.uni/moeda">Conversão de Moeda</a>
    <a href="/conversor.med.uni/peso">Conversão de Peso</a>
    <a href="/conversor.med.uni/distancia">Conversão de Distância</a>
    <a href="/conversor.med.uni/temperatura">Conversão de Temperatura</a>
    <a href="/conversor.med.uni/velocidade">Conversão de Velocidade</a>
    <a href="/conversor.med.uni/tempo">Conversão de Tempo</a>
  </div>
</main>

<style>
  .welcome-page {
    text-align: center;
    padding: 2rem;
    background-color: #e8e9e4;
    min-height: 100vh;
    border-radius: 15px;
  }

  h1 {
    font-size: 2.5rem;
    color: #000000;
    margin-bottom: 1rem;
    border-radius: 10px; 
  }

  p {
    font-size: 1.2rem;
    color: #333;
    margin-bottom: 2rem;
    border-radius: 10px; 
  }

  .links {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: center;
  }

  .links a {
    padding: 1rem 2rem;
    background-color: #56565c;
    color: white;
    text-decoration: none;
    border-radius: 15px; 
    font-weight: bold;
    transition: background-color 0.3s ease, transform 0.3s ease;
  }

  .links a:hover {
    background-color: #e44e29;
    transform: scale(1.05);
  }
</style>
