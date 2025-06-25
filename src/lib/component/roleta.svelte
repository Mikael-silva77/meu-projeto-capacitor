<script>
  export let resultado;
</script>

<style>
  .roleta-box {
    text-align: center;
    margin: 1rem 0;
    padding: 1rem;
    background: #ffffff22;
    border-radius: 12px;
  }
  .roleta-box span {
    font-size: 2rem;
    font-weight: bold;
    color: #fff;
  }
</style>

{#if resultado !== null}
  <div class="roleta-box">
    <span>🎲 {resultado}</span>
  </div>
{/if}
