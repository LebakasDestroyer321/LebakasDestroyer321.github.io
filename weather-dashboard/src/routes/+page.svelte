<script>
  let city = $state("");
  let temperature = $state(null);
  let forecast = $state(null);
  let errorMsg = $state("");
  let favorites = $state([]);
  let isFavorite = $derived(favorites.includes(city));

  async function getWeather() {
    errorMsg = "";
    temperature = null;
    forecast = null;

    function toggleFavorite() {
      let updated;
      if (favorites.includes(city)) {
        updated = favorites.filter((c) => c !== city);
      } else {
        updated = [...favorites, city];
      }
      favorites = updated;
      localStorage.setItem("favorites", JSON.stringify(favorites));
    }
  }
</script>
