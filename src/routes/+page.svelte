<script>
    let points=$state(0)
    let totalpoints=$state(0)
    let clicked=$state(false)

    const apiendpoint="http://openstreetcam.org/"

    let earth="https://upload.wikimedia.org/wikipedia/commons/7/74/Mercator-projection.jpg"

    function click(){
        clicked=!clicked
    }

    const min=0
    const max=5000 
</script>

<main>
    <h1 class="test"> {points} Poäng</h1>
    <h1 class="test"> Total Poäng: {points}</h1>
    <button class="container" onclick={() => click()}> 
        <img class="image-wrapper" src={earth} alt="Flexbox egenskaper">
    </button>
    {#if clicked}
        <h1>im gorking it</h1>
    {/if}
</main>

<style>
    .test {
        text-align: center;
    }

    .image-wrapper{ 
        border-radius: 20px;
        display: flex;
    }
    
    .container{
        width: 39vw;
        height: 30vw;
        display: flex;
        margin-left: 50%;
        background-color: #4a412a;
        border-radius: 20px;

        overflow: hidden;
    }
</style>