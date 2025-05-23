<script>
  import SearchBar from '$lib/SearchBar.svelte';
  import CurrentWeather from '$lib/CurrentWeather.svelte';
  import ForecastList from '$lib/ForecastList.svelte';
  import FavoriteList from '$lib/FavoriteList.svelte';

  let city = $state('');
  let temperature = $state(null);
  let forecast = $state(null);
  let currentIcon = $state('');
  let error = $state('');
  let favorites = $state([]);
  let isFavorite = $derived(favorites.includes(city));
  let nearby = $state([]);

  // Beim ersten Rendern: Favoriten laden,
  // wenn keine, Geolocation-Fallback ausführen
  $effect(() => {
    const saved = localStorage.getItem('favorites');
    if (saved) {
      favorites = JSON.parse(saved);
    } else if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(
        async pos => {
          const { latitude, longitude } = pos.coords;
          const geo = await fetch(
            `https://geocoding-api.open-meteo.com/v1/search?` +
            `latitude=${latitude}&longitude=${longitude}&count=5`
          ).then(r => r.json());
          nearby = geo.results?.map(r => r.name) ?? [];
        },
        () => {
          nearby = [];
        }
      );
    }
  });

  function updateCity(val) {
    city = val;
  }

  function toggleFavorite() {
    let newFavs = favorites.includes(city)
      ? favorites.filter(c => c !== city)
      : [...favorites, city];

    favorites = newFavs;
    localStorage.setItem('favorites', JSON.stringify(favorites));
  }

  async function getWeather() {
    error = '';
    temperature = null;
    forecast = null;
    currentIcon = '';

    try {
      const geo = await fetch(
        `https://geocoding-api.open-meteo.com/v1/search?name=${city}&count=1`
      ).then(r => r.json());
      if (!geo.results?.length) throw 'Ort nicht gefunden';
      const { latitude, longitude } = geo.results[0];

      const w = await fetch(
        `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}` +
        `&current=temperature_2m` +
        `&daily=temperature_2m_max,temperature_2m_min,precipitation_sum` +
        `&timezone=auto`
      ).then(r => r.json());

      temperature = w.current.temperature_2m;
      forecast = {
        days: w.daily.time.slice(1, 4),
        max:  w.daily.temperature_2m_max.slice(1, 4),
        min:  w.daily.temperature_2m_min.slice(1, 4),
        rain: w.daily.precipitation_sum.slice(1, 4)
      };
      // Icon nach heutiger Regenmenge
      const todayRain = w.daily.precipitation_sum[0];
      currentIcon = todayRain > 0 ? '🌧️' : '☀️';
    } catch (e) {
      error = typeof e === 'string' ? e : 'Fehler beim Abrufen';
    }
  }

  function selectCity(c) {
    city = c;
    getWeather();
  }
</script>

<main class="space-y-6">
  <h1 class="text-3xl font-bold text-center text-white">Wetter App</h1>

  <SearchBar {city} updateCity={updateCity} search={getWeather} />

  {#if error}
    <p class="text-red-600 text-center">{error}</p>
  {/if}

  <CurrentWeather
    city={city}
    temperature={temperature}
    icon={currentIcon}
    isFavorite={isFavorite}
    toggleFavorite={toggleFavorite}
  />

  <ForecastList {forecast} />

  {#if favorites.length > 0}
    <FavoriteList {favorites} selectCity={selectCity} />
  {:else if nearby.length > 0}
    <h2 class="text-xl font-semibold text-white">In deiner Nähe</h2>
    <ul class="space-y-2">
      {#each nearby as place}
        <li>
          <button
            class="w-full text-left bg-white/60 px-4 py-2 rounded-full hover:bg-white transition"
            onclick={() => selectCity(place)}
          >
            {place}
          </button>
        </li>
      {/each}
    </ul>
  {:else}
    <p class="text-white/80 italic text-center">Keine Favoriten gespeichert.</p>
  {/if}
</main>
