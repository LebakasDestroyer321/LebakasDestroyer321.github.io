<script>
  // importiere einmalig dein Tailwind-CSS
  import '../app.css';
</script>

<!--
  Hier definierst du die "Rahmenbedingungen" für alle Pages.
  Füge direkt hier deinen Hintergrund-Gradient und den Full-Screen Wrapper hinzu.
-->
<div class="min-h-screen w-full bg-gradient-to-br from-purple-500 via-pink-400 to-orange-300 flex items-center justify-center p-4">
  <main class="w-full sm:w-11/12 md:w-3/4 lg:w-2/3 xl:w-1/2 bg-white/40 backdrop-blur-md border border-white/30 rounded-3xl shadow-lg p-6">
    <slot />
  </main>
</div>
