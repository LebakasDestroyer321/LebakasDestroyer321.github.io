<script>
  import FavoriteList from '$lib/FavoriteList.svelte';

  let favorites = $state([]);

  $effect(() => {
    const saved = localStorage.getItem('favorites');
    if (saved) {
      favorites = JSON.parse(saved);
    }
  });

  function selectCity(city) {
    alert(`Lade Wetter für ${city}`);
  }
</script>

<h1 class="title">Deine Favoriten</h1>

<FavoriteList {favorites} {selectCity} />
