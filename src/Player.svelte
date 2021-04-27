<script>
    import {createEventDispatcher} from "svelte";
  export let name;
  export let points;
  let showControls = false;
  const dispatch = createEventDispatcher();
  
  const toggleControls = () => {showControls = !showControls}

  let isDisabled = true;
  const addPoint = () => {
      points += 1;
      isDisabled = false;
    };
  const removePoint = () => {
      points -= 1;
      isDisabled = false;
    };
  const onDelete = () => dispatch("removeplayer", name)
</script>


<div class="card">
    <h1>Player: {name}</h1>

    {#if showControls}
    <button class={showControls === false ? "blue" : ""} on:click={toggleControls} disabled={isDisabled}>Done</button>
    {:else}
        <button class="blue" on:click={toggleControls}>Add points</button>
    {/if}

    <button class="red" on:click={onDelete}>Delete</button>
    <h3>Points: {points}</h3>
    {#if showControls}
        <button class="btn" on:click={addPoint}>+1</button>
        <button class="btn btn-dark" on:click={removePoint}>-1</button><br>
        <input type="number" bind:value={points}>
    {/if}
</div>


<style lang="scss">
    .card {
        border: 1px solid gray;
        padding: 20px;
        margin-bottom: 20px;

        .blue{
            background-color: aliceblue;
        }

        .red{
            background-color: indianred;
        }
        h3{
            margin-bottom: 10px;
        }
    }
</style>
