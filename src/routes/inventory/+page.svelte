<script lang="ts">
  import { base } from '$app/paths';
  const inventoryByVehicle = [
    {
      id: 'LFA',
      name: 'Löschfahrzeug mit Allrad',
      items: [
        { name: 'Hooligan-Tool', status: 'AUSSTEHEND', info: 'Prüfung fällig: Sept 2024' },
        { name: 'Standrohr', status: 'AUSSTEHEND', info: 'Prüfung fällig: Aug 2024' },
        { name: 'Strahlrohre (C/B)', status: 'BEREIT', info: 'In 14 Tagen fällig' },
      ]
    },
    {
      id: 'TLF-A 3000',
      name: 'Tanklöschfahrzeug mit Allrad',
      items: [
        { name: 'Schlauchmaterial', status: 'FEHLER', info: 'Prüfung ÜBERFÄLLIG!' },
        { name: 'Wasserwerfer', status: 'BEREIT', info: 'Prüfung Nov 2024' },
        { name: 'Atemschutzgeräte', status: 'BEREIT', info: 'Prüfung März 2025' },
      ]
    },
    {
      id: 'VRF-A',
      name: 'Vorausrüstfahrzeug mit Allrad',
      items: [
        { name: 'Hydraulischer Rettungssatz', status: 'BEREIT', info: 'Prüfung Okt 2024' },
        { name: 'Stabilisierungssystem', status: 'BEREIT', info: 'Prüfung Dez 2024' },
        { name: 'Hebekissen', status: 'BEREIT', info: 'Prüfung Jan 2025' },
      ]
    },
    {
      id: 'MTF',
      name: 'Mannschaftstransportfahrzeug',
      items: [
        { name: 'Absicherungsmaterial', status: 'BEREIT', info: 'Prüfung Jan 2025' },
        { name: 'Funkgeräte', status: 'BEREIT', info: 'Prüfung Feb 2025' },
        { name: 'Erste-Hilfe-Rucksack', status: 'BEREIT', info: 'Prüfung März 2025' },
      ]
    }
  ];

  const getStatusColor = (status: string) => {
    switch (status) {
      case 'BEREIT': return 'var(--color-success)';
      case 'AUSSTEHEND': return 'var(--color-warning)';
      case 'FEHLER': return 'var(--color-error)';
      default: return 'var(--color-on-surface-variant)';
    }
  };
</script>

<div class="space-y-10">
  <header>
    <h2 class="text-3xl font-bold tracking-tight text-[var(--color-on-surface)] uppercase">Fahrzeug-Inventar</h2>
    <p class="text-[var(--color-on-surface-variant)] font-medium">Status & Bestandsliste der Einsatzfahrzeuge</p>
  </header>

  <div class="space-y-12">
    {#each inventoryByVehicle as vehicle}
      <section class="space-y-4">
        <div class="flex items-center gap-4">
          <h3 class="text-xl font-bold uppercase tracking-tight text-[var(--color-primary)]">{vehicle.id}</h3>
          <div class="h-px flex-1 bg-[var(--color-outline-variant)]/20"></div>
          <span class="text-[10px] font-bold text-[var(--color-on-surface-variant)] uppercase tracking-widest">{vehicle.name}</span>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
          {#each vehicle.items as item}
            <div class="bg-[var(--color-surface-container-lowest)] p-5 rounded-[var(--radius-md)] relative pl-8 border border-[var(--color-outline-variant)]/10 shadow-sm group">
              <div class="absolute left-0 top-0 w-1 h-full rounded-l-[var(--radius-md)]" style="background-color: {getStatusColor(item.status)}"></div>
              
              <div class="flex justify-between items-start mb-2">
                <h4 class="font-bold text-sm">{item.name}</h4>
                <div class="w-1.5 h-1.5 rounded-full" style="background-color: {getStatusColor(item.status)}"></div>
              </div>
              
              <p class="text-xs text-[var(--color-on-surface-variant)] font-medium mb-4">
                {item.info}
              </p>

              <div class="flex items-center justify-between mt-auto">
                <span class="text-[9px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] opacity-60">Status: {item.status}</span>
                <a href="{base}/inventory/{vehicle.id}" class="text-[9px] font-bold text-[var(--color-primary)] uppercase tracking-widest hover:underline transition-all">Details ➔</a>
              </div>
            </div>
          {/each}
        </div>
      </section>
    {/each}
  </div>

  <footer class="pt-10 border-t border-[var(--color-outline-variant)]/10 flex justify-between items-center">
    <p class="text-xs text-[var(--color-on-surface-variant)] font-medium italic">Letzte Aktualisierung: Heute, 07:15 durch OBI Musterer</p>
    <a href="{base}/" class="bg-[var(--color-primary)] text-white px-6 py-3 rounded-[var(--radius-md)] font-bold uppercase tracking-wide text-xs">
      Prüfbericht Exportieren
    </a>
  </footer>
</div>
