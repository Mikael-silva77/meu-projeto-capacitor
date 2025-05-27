<script>
  const links = [
    { href: '/conversor.med.uni', label: 'Inicio', color: '#FF5733' },
    { href: '/conversor.med.uni/moeda', label: 'Moeda', color: '#636363' },
    { href: '/conversor.med.uni/peso', label: 'Peso', color: '#636363' },
    { href: '/conversor.med.uni/distancia', label: 'Distância', color: '#636363' },
    { href: '/conversor.med.uni/temperatura', label: 'Temperatura', color: '#636363' },
    { href: '/conversor.med.uni/velocidade', label: 'Velocidade', color: '#636363' },
    { href: '/conversor.med.uni/tempo', label: 'Tempo', color: '#636363' },
  ];
</script>

<nav class="navbar">
  <ul>
    {#each links as { href, label, color }}
      <li>
        <a href={href} style="background-color: {color}">{label}</a>
      </li>
    {/each}
  </ul>
</nav>

<main>
  <slot />
</main>

<style>
  .navbar {
    background: #333;
    padding: 1rem;
    width: 100%;
    overflow-x: auto; 
    border-radius: 20px; 
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); 
  }

  

  .navbar ul {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
    width: fit-content; 
  }

  .navbar li {
    margin-right: 1rem; 
  }

  .navbar a {
    color: white;
    text-decoration: none;
    font-weight: bold;
    padding: 0.5rem 1rem;
    text-align: center;
    border-radius: 10px; 
    transition: background-color 0.3s ease, transform 0.3s ease; 
  }

  .navbar a:hover {
    background-color: rgba(255, 255, 255, 0.2);
    transform: scale(1.05);
  }
</style>
