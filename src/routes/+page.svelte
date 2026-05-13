<script lang="ts">
  import { base } from '$app/paths';
  const vehicles = [
    { id: 'LFA', status: 'BEREIT', readiness: 100, color: 'var(--color-success)' },
    { id: 'TLF-A 3000', status: 'BEREIT', readiness: 95, color: 'var(--color-success)' },
    { id: 'VRF-A', status: 'BEREIT', readiness: 100, color: 'var(--color-success)' },
    { id: 'MTF', status: 'WARTUNG', readiness: 75, color: 'var(--color-warning)' },
  ];

  const stats = [
    { label: 'Fahrzeuge außer Dienst', value: '00', sub: 'Einsatzbereit' },
    { label: 'Überfällig', value: '03', sub: 'Prüfungen' },
    { label: 'In 14 Tagen', value: '12', sub: 'Fällig' },
  ];
</script>

<div class="space-y-10">
  <header>
    <h2 class="text-3xl font-bold tracking-tight text-[var(--color-on-surface)] uppercase">Dashboard Status</h2>
    <p class="text-[var(--color-on-surface-variant)] font-medium">Salzburg Org. Nr. 3.04.01</p>
  </header>

  <!-- Mission Alert -->
  <div class="bg-[var(--color-primary)] text-white p-6 rounded-[var(--radius-md)] flex items-center justify-between shadow-lg">
    <div class="flex items-center gap-4">
      <span class="text-2xl">⚠️</span>
      <div>
        <p class="font-bold uppercase tracking-wide">Monatsprüfung Erforderlich</p>
        <p class="text-sm opacity-90">Tragkraftspritzen (TS) jetzt durchführen.</p>
      </div>
    </div>
    <a href="{base}/checklists" class="bg-white/20 hover:bg-white/30 px-4 py-2 rounded-[var(--radius-md)] text-xs font-bold uppercase transition-colors">
      Starten
    </a>
  </div>

  <!-- Stats Tonal Grid -->
  <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
    {#each stats as stat}
      <div class="bg-[var(--color-surface-container-low)] p-8 rounded-[var(--radius-md)] relative overflow-hidden group">
        <div class="absolute left-0 top-0 w-1 h-full bg-[var(--color-primary)] opacity-20"></div>
        <p class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] mb-1">{stat.label}</p>
        <p class="text-4xl font-bold tracking-tight">{stat.value}</p>
        <p class="text-[10px] font-medium text-[var(--color-on-surface-variant)] uppercase">{stat.sub}</p>
      </div>
    {/each}
  </div>

  <!-- Vehicle Readiness (Monolith Style) -->
  <section class="space-y-6">
    <div class="flex items-center justify-between mb-6">
      <h3 class="text-sm font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)]">Fahrzeugbereitschaft</h3>
      <a href="{base}/inventory" class="text-[10px] font-bold text-[var(--color-primary)] uppercase tracking-widest hover:underline">Alle Fahrzeuge anzeigen</a>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
      {#each vehicles as vehicle}
        <div class="bg-[var(--color-surface-container-lowest)] p-6 rounded-[var(--radius-md)] relative pl-10 border border-[var(--color-outline-variant)]/5 shadow-sm">
          <div class="absolute left-0 top-0 w-1.5 h-full" style="background-color: {vehicle.color}"></div>
          <div class="flex justify-between items-start mb-4">
            <div>
              <h4 class="font-bold text-lg">{vehicle.id}</h4>
              <p class="text-xs font-medium text-[var(--color-on-surface-variant)] uppercase tracking-wider">{vehicle.status}</p>
            </div>
            <span class="text-xl font-bold">{vehicle.readiness}%</span>
          </div>
          <div class="w-full h-2 bg-[var(--color-surface-container-low)] rounded-full overflow-hidden">
            <div class="h-full transition-all duration-1000" style="width: {vehicle.readiness}%; background-color: {vehicle.color}"></div>
          </div>
        </div>
      {/each}
    </div>
  </section>

  <!-- Quick Actions -->
  <div class="flex flex-wrap gap-4 pt-4">
    <a href="{base}/inventory" class="bg-[var(--color-primary)] text-white px-8 py-4 rounded-[var(--radius-md)] font-bold uppercase tracking-wide shadow-md hover:translate-y-[-1px] transition-all">
      Inventar Erfassen
    </a>
    <a href="{base}/stock" class="bg-[var(--color-surface-container-highest)] text-[var(--color-on-surface)] px-8 py-4 rounded-[var(--radius-md)] font-bold uppercase tracking-wide hover:bg-[var(--color-surface-container-high)] transition-colors">
      Bestandsliste
    </a>
  </div>
</div>
