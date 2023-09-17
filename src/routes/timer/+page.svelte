<script>
    let timerMode = "edit"
    let editValues = []
    let hours = 0
    let minutes = 0
    let seconds = 0
    let intervalRef = null

    function showDisplay() {
        timerMode = "display"
        
        editValues.push(Number(hours), Number(minutes), Number(seconds))

        if (hours <= 9) {
            hours = `0${hours}`
        }

        if (minutes <= 9) {
            minutes = `0${minutes}`
        }

        if (seconds <= 9) {
            seconds = `0${seconds}`
        }

        intervalRef = setInterval(() => {
            let numberHours = Number(hours)
            let numberMinutes = Number(minutes)
            let numberSeconds = Number(seconds)

            if (numberMinutes + numberSeconds === 0) {             
                if (numberHours === 0) {
                    return clearInterval(intervalRef)
                } else if (numberHours === 1) {
                    hours = "00"
                } else {
                    numberHours--
                    hours = numberHours > 9 ? `${numberHours}` : `0${numberHours}`
                }

                minutes = "59"
                seconds = "59"
            } else {
                if (numberSeconds === 0) {
                    numberMinutes--
                    minutes = numberMinutes > 9 ? `${numberMinutes}` : `0${numberMinutes}`

                    seconds = "59"
                } else {
                    numberSeconds--
                    seconds = numberSeconds > 9 ? `${numberSeconds}` : `0${numberSeconds}`
                }
            }
        }, 1000);
    }

    function showEdit() {
        clearInterval(intervalRef)

        timerMode = "edit"

        hours = editValues[0]
        minutes = editValues[1]
        seconds = editValues[2]
    }
</script>

<div id="main">
    <h1>Timer</h1>

    <div id="timer-container">
        {#if timerMode === "edit"}
            <form on:submit|preventDefault={showDisplay}>
                <div>
                    <input type="number" max="99" min="0" bind:value={hours}>
                    <input type="number" max="59" min="0" bind:value={minutes}>
                    <input type="number" max="59" min="0" bind:value={seconds}>
                </div>
                <button type="submit" disabled={hours + minutes + seconds === 0}>Display</button>
            </form>
        {/if}
        {#if timerMode === "display"}
            <div id="edit-mode-container">
                <p>{hours}:{minutes}:{seconds}</p>
                <button type="button" on:click={showEdit}>Edit</button>
            </div>
        {/if}
    </div>

    <nav>
        <a href="/stopwatch">Stopwatch</a>
        <a href="/clock">Clock</a>
        <a href="/">Home</a>
    </nav>
</div>

<style>
    #timer-container {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        background-color: lightgray;
        padding: 0.5rem;
        height: 100px;
        border-radius: 10%;
    }

    form, #edit-mode-container {
        display: flex;
        flex-direction: column;
    }

    #timer-container input {
        font-size: 3rem;
        width: 4rem;
    }
    
    #timer-container p {
        font-size: 3rem;
        margin: 0;
    }
</style>
