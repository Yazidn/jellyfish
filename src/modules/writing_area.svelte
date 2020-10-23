<script>
    let is_fs = false;

    let text_area_value = '';
    let text_size = 16;

    let tw = new Audio('/tw.wav');
    let is_tw_mute = false;
    tw.volume = 0.2;



    function mute_typewriter() {
        if (!is_tw_mute) {
            tw.volume = 0;
            is_tw_mute = true;
        }
        else {
            tw.volume = 0.2;
            is_tw_mute = false;
        }
    }

    function on_write_sound() {
        tw.currentTime = 0;
        tw.play();
    }


    function download(content, fileName, contentType) {
        let a = document.createElement("a");
        let file = new Blob([content], { type: contentType });
        a.href = URL.createObjectURL(file);
        a.download = fileName;
        a.click();
    }

    let background_url = '/bg.png';
    async function change_background() {
        const req = await fetch('https://picsum.photos/1920/1080');
        background_url = req.url;
    }

    function increase_text() {
        text_size += 2;
    }

    function decrease_text() {
        text_size -= 2;
    }

</script>
<main style="background-image: url({background_url})">
    <div class="container">
        <div class="panel">
            <button title="Toggle fullscreen mode." on:click={() => is_fs = !is_fs}><i class="fas fa-expand"></i></button>
            <button title="Make text bigger." on:click={increase_text}><i class="fas fa-heading"></i></button>
            <button title="Make text smaller." on:click={decrease_text}><i class="fas fa-font"></i></button>
            <button title="Use a random background image." on:click={change_background}><i class="fas fa-image"></i></button>
            <button title="Toggle typewriter button click sound." on:click={mute_typewriter}><i class="fas fa-volume-mute"></i></button>
            <button title="Save as text file." on:click={() => download(text_area_value, `jellyfish - ${new Date().toLocaleString()}.txt`, 'text/plain')}><i class="fas fa-file-export"></i></button>
            <!-- <button title="Change your preferences." ><i class="fas fa-cog"></i></button> -->
        </div>
        <textarea style='font-size: {text_size}px' bind:value={text_area_value} on:input={on_write_sound} class:isfs={is_fs}></textarea>
    </div>
</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Special+Elite&display=swap');

    main {
        height: 100vh;
        width: 100vw;
        background: rgb(238, 238, 238);
        /* background-image: url("/bg.png"); */
        background-size: cover;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    textarea {
        border-radius: 10px;
        border: none;
        box-shadow: 0px 30px 45px rgba(0, 0, 0, .05);

        padding: 40px;
        padding-right: 80px;

        background: rgba(255, 255, 255, .95);

        /* background-image: url('/opq.png'); */
        /* background-repeat: repeat; */

        font-family: 'Special Elite', cursive;
        /* font-size: 16px; */


        min-height: 300px;
        min-width: 300px;

        height: 80vh;
        width: 32vw;

        /* max-height: 95vh;
        max-width: 97vw; */
    }

    div.container {
        padding: 5px;
        position: relative;
    }

    div.panel {
        display: none;
        position: absolute;
        right: 20px;
        top: 20px;
    }

    div.panel button{
        margin: 10px;
        padding: 5px;
        cursor: pointer;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, .1);

        border:none;
        border-radius: 5px;

        /* background: linear-gradient(45deg, #2557c2, #671da0); */
        /* color: white; */
    }

    div.container:hover >  div.panel{
        display: flex;
        flex-direction: column;
        padding: 5px;
    }

    .isfs {
        /* height: 95vh; */
        /* width: 97vw; */

        height: 100vh;
        width: 100vw;

        text-align: center;
        padding-left: 20vw;
        padding-right: 20vw;

        border-radius: 0;
    }
</style>