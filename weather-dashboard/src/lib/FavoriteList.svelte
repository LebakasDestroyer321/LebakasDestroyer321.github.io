<script>
  let { favorites = [], selectCity } = $props();
</script>

{#if favorites.length > 0}
  <h2 class="mt-6 text-xl font-semibold text-indigo-800">Favoriten</h2>
  <ul class="grid grid-cols-1 sm:grid-cols-2 gap-2 mt-2">
    {#each favorites as fav}
      <li>
        <button
          class="w-full text-left bg-white/70 backdrop-blur-sm rounded-lg px-4 py-2 hover:bg-white transition"
          onclick={() => selectCity(fav)}
        >
          {fav}
        </button>
      </li>
    {/each}
  </ul>
{:else}
  <p class="mt-4 italic text-gray-500">Keine Favoriten gespeichert.</p>
{/if}
