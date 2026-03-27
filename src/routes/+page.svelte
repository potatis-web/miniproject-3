<script>
  const POINT_CONFIG = {
    min: 0,
    max: 5000,
  };

  // Image URLs
  const IMAGES = {
    earth: "https://upload.wikimedia.org/wikipedia/commons/7/74/Mercator-projection.jpg",
    fire: "https://www.techadvisor.com/wp-content/uploads/2025/09/pigeon_people_google_street_view.jpg?quality=50&strip=all",
    cat: "https://external-preview.redd.it/this-cat-in-google-street-view-v0-qMcPyXnMJV25J4z41JRu-6nIWdVYxCR1BR1UGqPL9BQ.jpg?width=640&crop=smart&auto=webp&s=70ae447799801f5fef59f1548ee1c5f4fa36f780",
    obama: "https://www.slashgear.com/img/gallery/the-10-best-google-maps-street-view-photos-of-all-time/horseman-1654627123.jpg",
    alien: "https://www.slashgear.com/img/gallery/the-10-best-google-maps-street-view-photos-of-all-time/the-stig-1654627123.jpg",
    spiderman: "https://i1.wp.com/www.weirdgoogleearth.com/wp-content/uploads/2020/10/spiderman-goes-international.jpg?fit=1024%2C629&ssl=1",
  };

  const imageArray = [IMAGES.cat, IMAGES.fire, IMAGES.spiderman, IMAGES.obama, IMAGES.alien];

  let data = {
    points: Math.floor(Math.random() * POINT_CONFIG.max),
    maphover: false,
    total: 0,
  };

  let currentImage = $state(IMAGES.cat);

  function gulp() {
    data.points = Math.floor(Math.random() * POINT_CONFIG.max);
    data.total += data.points;
    currentImage = imageArray[Math.floor(Math.random() * imageArray.length)];
  }
</script>

<main>
  <h1 class="test">{data.points} Poäng</h1>
  <div class="button-row">
    <button class="container">
      <img class="image-wrapper" src={currentImage} alt="Random Street View">
    </button>
    <button id="map" class="container" onclick={gulp}>
      <img class="image-wrapper" src={IMAGES.earth} alt="World map">
    </button>
  </div>
  <h1 class="test">Total Poäng: {data.total}</h1>
</main>

<style>
  * {
    transition: all 0.2s;
    font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  }

  :global(body) {
    background-color: aliceblue;
  }

  #map {
    cursor: url("Untitled.png"), auto;
  }

  .test {
    text-align: center;
  }

  .button-row {
    display: flex;
    justify-content: center;
    gap: 16px;
    flex-wrap: wrap;
    margin-top: 1rem;
  }

  .image-wrapper {
    border-radius: 20px;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .container {
    width: 39vw;
    height: 30vw;
    display: flex;
    background-color: #4a412a;
    border-radius: 20px;
    overflow: hidden;
  }
</style>