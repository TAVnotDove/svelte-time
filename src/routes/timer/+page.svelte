<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<script>
    let timerStyle = "Default"
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

    function changeStyle() {
        timerStyle = timerStyle === "Default" ? "Hourglass" : "Default"
    }
</script>

<div id="main">
    <h1 on:click={changeStyle}>Timer {timerStyle}</h1>

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
            {#if timerStyle === "Default"}
                <div id="edit-mode-container">
                    <p>{hours}:{minutes}:{seconds}</p>
                    <button type="button" on:click={showEdit}>Edit</button>
                </div>
            {/if}
            {#if timerStyle === "Hourglass"}
                <!-- Created with Inkscape (http://www.inkscape.org/) -->
                <svg
                version="1.1"
                id="svg9241"
                width="75"
                height="100"
                viewBox="0 0 75 100"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:svg="http://www.w3.org/2000/svg">
                <path
                    style="fill:lightgray;fill-opacity:1;stroke-width:2;paint-order:fill markers stroke"
                    d="M 0.76033018,55.842009 H 74.427845 V 98.927372 L 73.429998,86.623228 68.077907,73.313793 60.878666,64.87494 50.347183,57.841823 38.043597,55.895569 27.081811,57.982273 16.53749,63.380789 7.8546714,72.211282 1.7979006,86.053259 0.76033018,98.927372 Z" />
                <path
                    style="fill:lightgray;fill-opacity:1;stroke-width:2;paint-order:fill markers stroke"
                    d="m 74.370791,44.136654 -73.66745517,0.09389 -0.05491,-43.0853271 1.01352797,12.3028611 5.3690489,13.302604 7.2099903,8.42967 10.540438,7.01969 12.306057,1.930571 10.959117,-2.100672 10.537433,-5.41195 8.671557,-8.841552 6.039125,-13.849685 1.021161,-12.8754241 z" />
                <path
                    style="display:inline;fill:#111111;stroke:none"
                    d="M 0,0 C 0,12.1437 3.6723,24.9486 12.1667,34 17.1744,39.3361 27.868,42.0721 27,51 26.2768,58.4388 17.5663,60.4337 13,65 3.93963,74.0604 0,87.5184 0,100 H 75 C 75,87.6605 71.119,75.3723 62.8333,66 57.9549,60.4817 47.1289,57.96 48,49 48.7117,41.6794 57.4591,39.5409 62,35 71.0134,25.9866 75,12.4079 75,0 H 0 M 73,2 C 73,8.82333 71.7763,15.7678 68.8333,22 59.8881,40.9429 35.6186,50.1253 18,36.6667 7.19962,28.4164 2,15.2891 2,2 h 71 m 0,96 H 2 C 2,91.1767 3.22369,84.2322 6.16667,78 15.1119,59.0571 39.3814,49.8747 57,63.3333 67.8004,71.5836 73,84.7109 73,98 Z" />
                </svg>
                <!-- default: top: 10px; height: 41px; empty: top: 51px; height: 0px;-->
                <div style="top: 10px; height: 41px" class="top-sand"></div>
                <!-- default: top: 106px; height: 0px; full: top: 65px; height: 41px;-->
                <div style="top: 106px; height: 0px" class="bottom-sand"></div>
            {/if}
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
        border: 1px solid black;
        position: relative;
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

    h1 {
        cursor: pointer;
        user-select: none;
    }

    svg {
        z-index: 1;
    }

    .top-sand, .bottom-sand {
        width: 71px;
        background-color: beige;
        position: absolute;
        left: 10px;
    }
</style>
