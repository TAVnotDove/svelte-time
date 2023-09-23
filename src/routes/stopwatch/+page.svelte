<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<script>
    let isPaused = true
    let intervalRef = null

    let hours = "00"
    let minutes = "00"
    let seconds = "00"

    function useStopwatch() {
        if (isPaused) {
            isPaused = false

            intervalRef = setInterval(() => {
                let numberHours = Number(hours)
                let numberMinutes = Number(minutes)
                let numberSeconds = Number(seconds)

                if (numberSeconds === 59) {
                    seconds = "00"

                    numberMinutes++ 
                } else {
                    numberSeconds++

                    if (numberSeconds > 9) {
                        seconds = `${numberSeconds}`
                    } else {
                        seconds = `0${numberSeconds}`
                    }
                }

                if (numberMinutes > 59) {
                    minutes = "00"
                    
                    numberHours++
                } else {
                    if (numberMinutes > 9) {
                        minutes = `${numberMinutes}`
                    } else {
                        minutes = `0${numberMinutes}`
                    }
                }

                if (numberHours > 9) {
                    hours = `${numberHours}`
                } else {
                    hours = `0${numberHours}`
                }
            }, 1000);
        } else {
            isPaused = true

            clearInterval(intervalRef)
        }

    }

    function resetStopwatch() {
        clearInterval(intervalRef)

        hours = "00"
        minutes = "00"
        seconds = "00"
    }

</script>

<div id="main">
    <h1>Stopwatch</h1>

    <div id="stopwatch-container">
        <p on:click={useStopwatch}>{hours}:{minutes}:{seconds}</p>
        <button
            on:click={resetStopwatch}
            disabled={hours + minutes + seconds === "000000"}>
            Reset
        </button>
    </div>

    <nav>
        <a href="/">Home</a>
        <a href="/clock">Clock</a>
        <a href="/timer">Timer</a>
    </nav>
</div>

<style>
    #stopwatch-container {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        background-color: lightgray;
        padding: 0.5rem;
        height: 100px;
        border-radius: 10%;
        border: 1px solid black;
    }

    p {
        font-size: 3rem;
        margin: 0;
        user-select: none;
        cursor: pointer;
    }
</style>
