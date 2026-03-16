<script>
  import { error } from "@sveltejs/kit";


    let points = $state(0);
    let totalpoints = $state(0);
    let clicked = $state(false);

    const apiendpoint="http://openstreetcam.org/";

    let earth="https://upload.wikimedia.org/wikipedia/commons/7/74/Mercator-projection.jpg";

    function click(){
      clicked =! clicked;
    }

    function generateLatLng() {
      const baseLat = Math.random();
      const lat = baseLat > 0.5 ? baseLat * 90 : baseLat * -90;
      
      const baseLng = Math.random();
      const lng = baseLng > 0.5 ? baseLng * 180 : baseLng * -180;

      return {
        lat: format(lat),
        lng: format(lng)
      }
    }
    function format(value) {
      return value.toFixed(4)
    }
    async function request() {
      const request = new Request(`https://api.openstreetcam.org/2.0/photo/?lat=${coords.lat}&lng=${coords.lng}&radius=50`, {
        method: "GET"
      })
      const response = await fetch(request);

      if (response.status != 200) {
        throw error(response.status, {message: response.statusText});
      }
      let data = await response.json();
      console.log(data)
      return data;
    }

    async function getValidRequest() {
      let validated = false;
      while (!validated) {
        
      }
    }
    const min = 0;
    const max = 5000;

    let coords = $state(generateLatLng());
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
    <button onclick={request}>Request</button>
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