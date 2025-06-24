<script>
    export let resultado;
    export let escolha;
  </script>
  
  <style>
    .roleta {
      text-align: center;
      font-size: 1.5rem;
      margin-top: 1rem;
      background: #ffffff22;
      padding: 1rem;
      border-radius: 12px;
    }
  </style>
  
  {#if resultado !== null}
    <div class="roleta">
      🎯 Roleta girou... Número sorteado: <strong>{resultado}</strong><br />
      {resultado % 2 === 0 ? 'Par' : 'Ímpar'}
    </div>
  {:else}
    <div class="roleta">
      🎲 Girando a roleta... Faça sua aposta!
    </div>
  {/if}
  