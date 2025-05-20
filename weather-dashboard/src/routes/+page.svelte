<script>
  let city = $state('');
  let temperature = $state(null);
  let forecast = $state(null);
  let error = $state('');
  let favorites = $state([]);
  let isFavorite = $derived(favorites.includes(city));

  $effect(() => {
    const saved = localStorage.getItem('favorites');
    if (saved) {
      favorites = JSON.parse(saved);
    }
  });

  function toggleFavorite() {
    let newFavorites;
    if (favorites.includes(city)) {
      newFavorites = favorites.filter(c => c !== city);
    } else {
      newFavorites = [...favorites, city];
    }
    favorites = newFavorites;
    localStorage.setItem('favorites', JSON.stringify(favorites));
  }

  async function getWeather() {
    error = '';
    temperature = null;
    forecast = null;

    try {
      const geoRes = await fetch(`https://geocoding-api.open-meteo.com/v1/search?name=${city}&count=1`);
      const geoData = await geoRes.json();

      if (!geoData.results || geoData.results.length === 0) {
        error = 'Ort nicht gefunden';
        return;
      }

      const { latitude, longitude } = geoData.results[0];

      const weatherRes = await fetch(
        `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}` +
        `&current=temperature_2m` +
        `&daily=temperature_2m_max,temperature_2m_min,precipitation_sum` +
        `&timezone=auto`
      );
      const weatherData = await weatherRes.json();

      temperature = weatherData.current.temperature_2m;

      forecast = {
        days: weatherData.daily.time.slice(1, 4),
        max: weatherData.daily.temperature_2m_max.slice(1, 4),
        min: weatherData.daily.temperature_2m_min.slice(1, 4),
        rain: weatherData.daily.precipitation_sum.slice(1, 4)
      };
    } catch {
      error = 'Fehler beim Abrufen';
    }
  }
</script>

<div class="min-h-screen bg-gradient-to-br from-indigo-100 via-white to-indigo-100 flex items-center justify-center px-4 py-10 font-sans">
  <div class="max-w-md w-full bg-white/70 backdrop-blur-md rounded-3xl shadow-lg p-8 space-y-8 text-center text-gray-900">
    <h1 class="text-4xl font-extrabold tracking-tight">Deine Wetter App</h1>

    <div class="flex space-x-4">
      <input
        bind:value={city}
        placeholder="Stadt eingeben"
        class="flex-grow rounded-xl border border-gray-300 bg-white/50 px-4 py-3 text-lg placeholder-gray-400 focus:outline-none focus:ring-4 focus:ring-indigo-300"
      />
      <button
        onclick={getWeather}
        class="rounded-xl bg-indigo-600 px-6 py-3 text-lg font-semibold text-white shadow-md transition hover:bg-indigo-700"
      >
        Suchen
      </button>
    </div>

    {#if error}
      <p class="text-red-600 font-medium">{error}</p>
    {/if}

    {#if temperature !== null}
      <div class="space-y-3">
        <p class="text-xl font-semibold">Temperatur in <span class="font-bold">{city}</span></p>
        <p class="text-7xl font-black tracking-tight">{temperature}°</p>
        <button
          onclick={toggleFavorite}
          class="rounded-full bg-indigo-500 px-8 py-2 font-semibold text-white shadow-md transition hover:bg-indigo-600"
        >
          {isFavorite ? 'Favorit entfernen' : 'Als Favorit speichern'}
        </button>
      </div>
    {/if}

    {#if forecast}
      <h2 class="text-2xl font-semibold tracking-wide">3-Tage-Vorhersage</h2>
      <div class="grid grid-cols-3 gap-6">
        {#each forecast.days as day, i}
          <div class="rounded-2xl bg-white/80 p-5 shadow-md backdrop-blur-sm">
            <p class="mb-1 font-semibold text-indigo-700">
              {new Date(day).toLocaleDateString('de-DE', { weekday: 'short' })}
            </p>
            <p class="text-lg">{forecast.min[i]}° – {forecast.max[i]}°</p>
            <p class="text-sm text-indigo-500">Regen: {forecast.rain[i]} mm</p>
          </div>
        {/each}
      </div>
    {/if}

    {#if favorites.length > 0}
      <h2 class="mt-10 text-2xl font-semibold tracking-wide">Favoriten</h2>
      <ul class="space-y-3">
        {#each favorites as fav}
          <li>
            <button
              onclick={() => {
                city = fav;
                getWeather();
              }}
              class="text-indigo-600 hover:underline">
              {fav}
            </button>
          </li>
        {/each}
      </ul>
    {:else}
      <p class="mt-4 italic text-indigo-400">Keine Favoriten gespeichert.</p>
    {/if}
  </div>
</div>
