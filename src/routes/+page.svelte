<script>
    let theme = 'light';

    /** @type {import('./$types').Snapshot<string>} */
    export const snapshot = {
        capture: () => {theme},
        restore: (newTheme) => theme = newTheme
    };

    console.log("works!")

    let count = 0

    function addOne() {
        count++
    }
</script>

<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->

<div id="main">
    <h1>Home</h1>
    <button on:click={addOne}>Clicked {count} Times</button>
    <nav>
        <a href="/stopwatch">Stopwatch</a>
        <a href="/clock">Clock</a>
        <a href="/timer">Timer</a>
    </nav>
</div>

<style>
    button {
        padding: 1rem;
        font-size: 1rem;
    }
</style>
