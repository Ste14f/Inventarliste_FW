<script lang="ts">
  import { base } from '$app/paths';
  const stockCategories = [
    { name: 'Atemschutz', count: 24, status: 'BEREIT', info: 'Nächste Prüfung: Okt 2024' },
    { name: 'Schläuche', count: 42, status: 'BEREIT', info: 'B-Schläuche geprüft' },
    { name: 'Geräte', count: 18, status: 'FEHLER', info: 'Stromerzeuger ÜBERFÄLLIG' },
  ];

  const consumables = [
    { name: 'Bindemittel (Sack)', location: 'R1-S4', amount: 15, unit: 'Stk', min: 10 },
    { name: 'Erste Hilfe Kits (Typ A)', location: 'M2-S1', amount: 8, unit: 'Stk', min: 5 },
  ];
</script>

<div class="space-y-10">
  <header class="flex flex-col md:flex-row md:items-end justify-between gap-6">
    <div>
      <h2 class="text-3xl font-bold tracking-tight text-[var(--color-on-surface)] uppercase">Lager Bestandslage</h2>
      <p class="text-[var(--color-on-surface-variant)] font-medium">Feuerwehrhaus Pfarrwerfen</p>
    </div>
    <a href="{base}/stock" class="bg-[var(--color-primary)] text-white px-6 py-3 rounded-[var(--radius-md)] font-bold uppercase tracking-wide text-xs shadow-lg">
      Bestellung Erstellen
    </a>
  </header>

  <!-- High-Level Categories -->
  <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
    {#each stockCategories as cat}
      <div class="bg-[var(--color-surface-container-low)] p-6 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10 relative overflow-hidden group">
        <div class="absolute left-0 top-0 w-1 h-full" style="background-color: {cat.status === 'ERROR' ? 'var(--color-error)' : 'var(--color-primary)'}"></div>
        <div class="flex justify-between items-start mb-4">
          <p class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)]">{cat.name}</p>
          <span class="text-2xl font-bold">{cat.count}</span>
        </div>
        <p class="text-xs font-medium {cat.status === 'ERROR' ? 'text-[var(--color-error)]' : 'text-[var(--color-on-surface-variant)]'} uppercase tracking-wide">
          {cat.info}
        </p>
      </div>
    {/each}
  </div>

  <!-- Consumables Table (Tactical Monolith) -->
  <section class="bg-[var(--color-surface-container-lowest)] rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10 overflow-hidden shadow-sm">
    <div class="p-6 border-b border-[var(--color-outline-variant)]/10 flex justify-between items-center bg-[var(--color-surface-container-low)]/30">
      <h3 class="text-sm font-bold uppercase tracking-widest">Verbrauchsmaterial</h3>
      <a href="{base}/stock" class="text-xs font-bold text-[var(--color-primary)] uppercase tracking-widest">Bestandsaufnahme ➔</a>
    </div>
    
    <div class="overflow-x-auto">
      <table class="w-full text-left text-sm">
        <thead class="bg-[var(--color-surface-container-low)] text-[var(--color-on-surface-variant)] uppercase text-[10px] font-bold tracking-widest">
          <tr>
            <th class="px-6 py-4">Artikel</th>
            <th class="px-6 py-4">Lagerplatz</th>
            <th class="px-6 py-4">Menge</th>
            <th class="px-6 py-4 text-right">Status</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-[var(--color-outline-variant)]/5">
          {#each consumables as item}
            <tr class="hover:bg-[var(--color-surface-container-low)]/50 transition-colors">
              <td class="px-6 py-5 font-bold uppercase tracking-tight">{item.name}</td>
              <td class="px-6 py-5 text-[var(--color-on-surface-variant)] font-medium">{item.location}</td>
              <td class="px-6 py-5">
                <span class="font-bold">{item.amount}</span> {item.unit}
              </td>
              <td class="px-6 py-5 text-right">
                {#if item.amount <= item.min}
                  <span class="text-[var(--color-warning)] text-[10px] font-bold uppercase tracking-widest">Nachbestellen</span>
                {:else}
                  <span class="text-[var(--color-success)] text-[10px] font-bold uppercase tracking-widest">Lager OK</span>
                {/if}
              </td>
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </section>

  <div class="p-6 bg-[var(--color-surface-container-high)]/30 rounded-[var(--radius-md)] border border-dashed border-[var(--color-outline-variant)]/20 text-center">
    <p class="text-xs font-bold text-[var(--color-on-surface-variant)] uppercase tracking-widest">Inventar geprüft von: OBI Musterer (Heute, 07:15)</p>
  </div>
</div>
