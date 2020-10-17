<script>
    // Booleans
    let is_writer_fs = false;
    let mute = false;

    let text_area_value = '';

    let text_size = 16;

    // Sound
    let bgm = new Audio('/bgm.mp3');
    let tw = new Audio('/tw.wav');

    tw.volume = 0.2;
    bgm.volume = 0.05;

    bgm.currentTime = 0;
    bgm.play();

    function on_write_sound() {
        tw.currentTime = 0;
        tw.play();
    }


    // Save to file
    // TRIGGER DOWNLOAD
    function download(content, fileName, contentType) {
        let a = document.createElement("a");
        let file = new Blob([content], { type: contentType });
        a.href = URL.createObjectURL(file);
        a.download = fileName;
        a.click();
    }

</script>
<main>
    <div class="container">
        <div class="panel">
            <button title="Fullscreen" on:click={() => is_writer_fs = !is_writer_fs}><i class="fas fa-expand"></i></button>
            <button title="Increase Text Size" on:click={() => text_size += 2}><i class="fas fa-text-height"></i></button>
            <button title="Background" disabled><i class="fas fa-image"></i></button>
            <button title="Music" disabled><i class="fas fa-headphones-alt"></i></button>
            <button title="Mute" on:click={() => bgm.pause()}><i class="fas fa-volume-mute"></i></button>

            <!-- <button title="Copy"><i class="fas fa-copy"></i></button> -->
            <button title="Save to Device" on:click={() => download(text_area_value, `jellyfish - ${new Date().toLocaleString()}.txt`, 'text/plain')}><i class="fas fa-file-export"></i></button>
        </div>
        <textarea style='font-size: {text_size}px' bind:value={text_area_value} on:input={on_write_sound} class:iswriterfs={is_writer_fs} autofocus></textarea>
    </div>
</main>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Special+Elite&display=swap');

    main {
        height: 100vh;
        width: 100vw;
        background: rgb(238, 238, 238);
        background-image: url("/bg.png");
        background-size: cover;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    textarea {
        border-radius: 20px;
        border: none;
        box-shadow: 0px 20px 35px rgba(0, 0, 0, .15);

        padding: 20px;
        padding-right: 80px;

        background: rgba(255, 255, 255, .8);

        /* background-image: url('/opq.png'); */
        /* background-repeat: repeat; */

        font-family: 'Special Elite', cursive;
        /* font-size: 16px; */


        min-height: 300px;
        min-width: 300px;

        height: 80vh;
        width: 50vw;

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
        margin: 5px;
        padding: 10px;
        cursor: pointer;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, .2);

        border:none;
        border-radius: 50%;

        background: linear-gradient(45deg, #2557c2, #671da0);
        color: white;
    }

    div.container:hover >  div.panel{
        display: flex;
        flex-direction: column;
        padding: 5px;
    }

    .iswriterfs {
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