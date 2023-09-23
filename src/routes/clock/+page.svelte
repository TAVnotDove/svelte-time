<script>
    let hours = stringFormat(new Date().getHours())
    let minutes = stringFormat(new Date().getMinutes())
    let clockMode = "24-hour"
    let twelveM = null

    function stringFormat(number) {
        return number > 9 ? number : `0${number}`
    }

    function changeClockMode() {
        if (clockMode === "12-hour") {
            clockMode = "24-hour"

            hours = stringFormat(new Date().getHours())
            minutes = new Date().getMinutes()
        } else {
            clockMode = "12-hour"
            
            minutes = new Date().getMinutes()
            
            if (hours > 12) {
                twelveM = "PM"
                hours = stringFormat(hours - 12)
            } else {
                twelveM = "AM"
            }
        }
    }
</script>

<div id="main">
    <h1>Clock</h1>

    <div id="clock-container">
        {#if clockMode === "12-hour"}
            <p>{hours}:{minutes}{twelveM}</p>
        {/if}
        {#if clockMode === "24-hour"}
            <p>{hours}:{minutes}</p>
        {/if}
        <button on:click={changeClockMode}>{clockMode}</button>
    </div>

    <nav>
        <a href="/stopwatch">Stopwatch</a>
        <a href="/">Home</a>
        <a href="/timer">Timer</a>
    </nav>
</div>

<style>
    #clock-container {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        background-color: lightgray;
        padding: 0.5rem;
        height: 100px;
        border-radius: 10%;
        border: 1px solid black;
    }

    #clock-container p {
        font-size: 3rem;
        margin: 0;
    }
</style>
