<script>
    console.log("works!")

    let count = 0

    function addOne() {
        count++
    }
</script>

<style>
    button {
        padding: 1rem;
        font-size: 1rem;
    }
</style>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->

<button on:click={addOne}>Clicked {count} Times</button>
