<script>
  import { error } from "@sveltejs/kit";


    let points = $state(0);
    let totalpoints = $state(0);
    let clicked = $state(false);
    let timeElapsed = $state(0);
    let timerId;
    let timerStart = 0;
    let coords = $state(generateLatLng())
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

    function startTimer() {
      stopTimer();
      timeElapsed = 0;
      timerStart = performance.now();
      timerId = setInterval(() => {
        timeElapsed = (performance.now() - timerStart) / 1000;
      }, 100);
    }

    function stopTimer() {
      if (timerId) {
        clearInterval(timerId);
        timerId = undefined;
      }

      // Keep a final high-resolution elapsed time when stopping.
      if (timerStart) {
        timeElapsed = (performance.now() - timerStart) / 1000;
      }
    }

    async function request() {
      const request = new Request(`https://api.openstreetcam.org/2.0/photo/?lat=${coords.lat}&lng=${coords.lng}&radius=500000`, {
        method: "GET"
      })
      const response = await fetch(request);

      if (response.status != 200) {
        stopTimer();
        throw error(response.status, {message: response.statusText});
        
      }
      let data = await response.json();
      console.log(data)
      return data;
    }

    async function getValidRequest() {
      startTimer();

      let validated = false;
      while (!validated) {
        const data = await request();

        if (data.status.apiCode === 601) {
          console.warn(data.status.apiMessage)
          coords = generateLatLng()
          continue;
        }

        console.log("Success!")
        validated = true;
      }

      stopTimer();
    }


    const min = 0;
    const max = 5000;
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
    <p>{timeElapsed.toFixed(2)}s</p>
    <p>Latitide: {coords.lat}</p>
    <p>Longitude: {coords.lng}</p>
    <button onclick={getValidRequest}>Request</button>
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