<script>

    let valorEntrada = 1;
    let unidadeEntrada = 'h';
    let unidadeSaida = 'min';
    let valorSaida = 60;

   
    const conversoes = {
        h: { min: 60, s: 3600, dia: 1 / 24, ano: 1 / 8760 },
        min: { h: 1 / 60, s: 60, dia: 1 / 1440, ano: 1 / 525600 },
        s: { h: 1 / 3600, min: 1 / 60, dia: 1 / 86400, ano: 1 / 31536000 },
        dia: { h: 24, min: 1440, s: 86400, ano: 1 / 365 },
        ano: { h: 8760, min: 525600, s: 31536000, dia: 365 }
    };

   
    function converter() {
        if (unidadeEntrada === unidadeSaida) {
            valorSaida = valorEntrada;
        } else {
            valorSaida = valorEntrada * conversoes[unidadeEntrada][unidadeSaida];
        }
    }
</script>

<main>
    <div class="conversor">
        <h2>Conversor de Tempo</h2>
        <div class="grupo-entrada">
            <input type="number" bind:value={valorEntrada} on:input={converter} />
            <select bind:value={unidadeEntrada} on:change={converter}>
                <option value="h">Horas</option>
                <option value="min">Minutos</option>
                <option value="s">Segundos</option>
                <option value="dia">Dias</option>
                <option value="ano">Anos</option>
            </select>
        </div>
        <span class="igual">=</span>
        <div class="grupo-entrada">
            <input type="number" bind:value={valorSaida} readonly />
            <select bind:value={unidadeSaida} on:change={converter}>
                <option value="h">Horas</option>
                <option value="min">Minutos</option>
                <option value="s">Segundos</option>
                <option value="dia">Dias</option>
                <option value="ano">Anos</option>
            </select>
        </div>
    </div>
</main>

<style>
  
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    main {
        font-family: 'Arial', sans-serif;
        background-color: #f4f6f9;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    .conversor {
        background: #ffffff;
        padding: 30px;
        border-radius: 15px;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
        text-align: center;
        width: 350px;
        max-width: 100%;
    }

    h2 {
        margin-bottom: 20px;
        font-size: 1.8rem;
        color: #333;
    }

    .grupo-entrada {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 15px;
        margin-bottom: 20px;
    }

    input {
        width: 80px;
        padding: 10px;
        font-size: 1rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        text-align: center;
        background-color: #fafafa;
        transition: border 0.3s;
    }

    input:focus {
        border-color: #3a8dff;
        outline: none;
    }

    select {
        padding: 10px;
        font-size: 1rem;
        border-radius: 8px;
        border: 1px solid #ddd;
        background-color: #fafafa;
        cursor: pointer;
        transition: border 0.3s;
    }

    select:focus {
        border-color: #3a8dff;
        outline: none;
    }

    .igual {
        font-size: 2rem;
        font-weight: bold;
        color: #555;
        margin-top: 10px;
    }


    .grupo-entrada select:hover,
    .grupo-entrada input:hover {
        border-color: #3a8dff;
    }

    .grupo-entrada input:disabled {
        background-color: #e9e9e9;
    }
</style>
