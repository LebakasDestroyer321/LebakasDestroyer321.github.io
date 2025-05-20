<script>
  let { data } = $props();

  function formatDateTime(dateStr) {
    const d = new Date(dateStr);
    return d.toLocaleString('de-DE', { 
      weekday: 'long', 
      day: 'numeric', 
      month: 'long', 
      hour: '2-digit', 
      minute: '2-digit' 
    });
  }
</script>

<h1>Wetter in {data.name}, {data.country}</h1>

<p>Temperatur: {data.current.temperature_2m}°C</p>
<p>Wind: {data.current.wind_speed_10m} km/h</p>
<p>Luftfeuchtigkeit: {data.current.relative_humidity_2m}%</p>
<p>Messzeit: {formatDateTime(data.current.time)}</p>

<h2>3-Tage-Vorhersage</h2>
<ul>
  {#each data.daily.time.slice(1,4) as day, i}
    <li>
      {new Date(day).toLocaleDateString('de-DE', { weekday: 'long' })}:
      {data.daily.temperature_2m_min[i+1]}°C – {data.daily.temperature_2m_max[i+1]}°C,
      Regen: {data.daily.precipitation_sum[i+1]} mm
    </li>
  {/each}
</ul>
