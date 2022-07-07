<script>
    // only thing in svelte that doesn't make sense
    var inp = '';
    var error1 = '';
    var data = '';
    var success = '';
    var error2 = '';

    async function checkSong(id) {
        success.innerHTML = '';
        error2.innerHTML = '';
        var response = await fetch(`https://gdbrowser.com/api/song/${id}`).catch(err => {
            var newInnerHtml = `<p>${inp} is not whitelisted</p>`;
            error2.innerHTML = newInnerHtml;
        }).then(res => {
            // @ts-ignore
            return res.json();
        });

        if (response === true) {
            var newInnerHtml = `<p>${inp} is whitelisted!</p>`;
            success.innerHTML = newInnerHtml;
        }
    }
</script>

<main class="main">
    <div class="inputBox">
        <h1>
            GD Song Checker
        </h1>
        <input type="text" name="a" id="" bind:value={inp} class="" label='SongID'>
    </div>
    <div class="btn">
        <input type="submit" value="Check!" on:click="{checkSong(inp)}">
    </div>
    <div class="error">
        {#if inp.length == 0}
            <p>Please enter a valid ID (example: 99641)</p>
        {/if}
    </div>

    <div class="success" bind:this={success}>
    </div>

    <div class="error2" bind:this={error2}>
    </div>

    <div class="footer">
        <p>
          Made by Brisolo32 in 🇧🇷
        </p>
    </div>
</main>


<style>
    .inputBox {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
        size: 10px;
    }

    .success {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;

        font-size: 20px;
        font-weight: bold;

        font-family: 'Courier New', Courier, monospace;
        color: #02d422;
    }

    .error2 {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;

        font-size: 20px;
        font-weight: bold;

        font-family: 'Courier New', Courier, monospace;
        color: red;
    }

    .inputBox h1 {
        font-size: 40px;
        font-weight: bold;

        font-family: 'Courier New', Courier, monospace;
        color: #fff;
    }

    input[type=text] {
        width: 20%;
        height: 100%;
        border: none;
        border-bottom: 1px solid #000;
        font-size: 30px;
        padding: 10px;
        margin: 10px;
    }

    input[type=submit] {
        font-family: 'Courier New', Courier, monospace;
        width: 10%;
        height: 100%;
        border: none;
        border-bottom: 1px solid #000;
        font-size: 15px;
        padding: 10px;
        margin: 10px;
    }

    input[type=submit]:hover {
        background-color: rgb(198, 198, 198);
        color: #000;
    }

    .btn {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
    }

    .error {
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 13%;
        justify-content: center;
        width: 100%;
        color: rgb(255, 255, 255);
        font-size: 30px;
        font-family: 'Courier New', Courier, monospace;

        float: left;
        position: fixed;
        bottom: 0;
    }

    .footer {
        font-family: 'Consolas', 'Monaco', 'Bitstream Vera Sans Mono', monospace;
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 45px;
        background-color: #333;
        color: #fff;
        text-align: left;
        padding-left: 15px;
        line-height: 20px;
    }

</style>
