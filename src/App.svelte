<script>
	import Navbar from "./Navbar.svelte";
	import Player from "./Player.svelte";
	import AddPlayer from "./AddPlayer.svelte";

	let players = [
		{
			name: "Ruth",
			points: 43
		},
		{
			name: "Daniel",
			points: 12
		},
		{
			name: "Elin",
			points: 67
		}
	];

	const addPlayer = (e) => {
		const newPlayer = e.detail;
		// Add the newPlayer to the array. Array will be updated.
		players = [...players, newPlayer];
	}

	const removePlayer = (e) => {
		players = players.filter(player => player.name !== e.detail)
	}
</script>

<div class="main">
	<Navbar/>
	<div class="container">
		<AddPlayer on:addplayer={addPlayer}/>
		{#if players.length === 0}
			<p>No players</p>
		{:else}
			{#each players as player}
				<Player name={player.name} points={player.points} on:removeplayer={removePlayer}/>
			{/each}
		{/if}
	</div>
</div>


<style lang="scss">
	.main{
		display: flex; 
		margin: 0 auto;
		flex-direction: column;
		width: 60%;
	}
</style>
