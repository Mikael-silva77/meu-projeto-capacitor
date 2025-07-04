<script lang="ts">
	let borda= Array(9).fill('');
	let currentPlayer = 'X';
	let occupiedIndex: number | null = null;

	function play(index: number) {
		if (borda[index] !== '') {
			occupiedIndex = index;
			setTimeout(() => occupiedIndex = null, 500);
			return;
		}
		borda[index] = currentPlayer;
		currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
	}

	function reset() {
		borda = Array(9).fill('');
		currentPlayer = 'X';
		occupiedIndex = null;
	}
</script>

<main>
	<h1>Jogo da Velha</h1>
	<div class="grid">
		{#each borda as cell, i}
			<div
				class="cell {cell !== '' ? 'filled' : ''} {occupiedIndex === i ? 'shake' : ''}"
				on:click={() => play(i)}>
				{cell}
			</div>
		{/each}
	</div>
	<button on:click={reset}>Reiniciar</button>
</main>

<style>
	main {
		font-family: sans-serif;
		text-align: center;
		padding: 2rem;
	}

	h1 {
		margin-bottom: 1rem;
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(3, 100px);
		grid-gap: 10px;
		justify-content: center;
		margin-bottom: 1rem;
	}

	.cell {
		width: 100px;
		height: 100px;
		font-size: 2.5rem;
		display: flex;
		align-items: center;
		justify-content: center;
		border: 2px solid #353535;
		cursor: pointer;
		transition: background 0.3s;                       
	}

	.cell:hover {
		background: #aa0581;
	}

	.filled {           
		background-color:#c55cab;
		pointer-events: none;
	}

	.shake {
		animation: shake 0.3s;
		background-color: rgb(168, 136, 255);
	}


	button {
		padding: 10px 20px;
		font-size: 1rem;
		border: none;
		border-radius: 8px;
		background-color: #333;
		color: white;
		cursor: pointer;
	}

	button:hover {
		background-color: #aa0581;
	}
</style>