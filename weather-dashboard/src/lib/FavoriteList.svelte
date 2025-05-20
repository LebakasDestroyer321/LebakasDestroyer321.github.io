<ul class="space-y-2">
  {#each favorites as city}
    <li>
      <button
        onclick={() => selectCity(city)}
        class="w-full text-left p-3 rounded bg-blue-100 hover:bg-blue-200 transition">
        {city}
      </button>
    </li>
  {/each}
</ul>
