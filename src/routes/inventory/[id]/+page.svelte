<script lang="ts">
  import { base } from '$app/paths';
  import { page } from '$app/state';

  const vehicles = {
    'TLF-A 3000': {
      name: 'Tanklöschfahrzeug mit Allrad',
      desc: 'Der Allrounder der Feuerwehr Pfarrwerfen für Brand- und technische Einsätze.',
      tech: [
        { label: 'Taktische Bezeichnung', value: 'TLFA 3000/100' },
        { label: 'Funkrufname', value: 'Tank Pfarrwerfen' },
        { label: 'Besatzung', value: '1:8' },
        { label: 'Baujahr', value: '2017' },
        { label: 'Wasser', value: '3.000 Liter' },
        { label: 'Schaum', value: '140 Liter' }
      ],
      features: [
        'Permanenter Allradantrieb',
        'Einbaupumpe 3.000 l/min',
        'Einbauseilwinde 5,5 t',
        'LED-Lichtmast'
      ],
      equipment: [
        '3 Atemschutzgeräte (TwinPack)',
        'Wärmebildkamera',
        'Rettungsplattform',
        'Korbschleiftrage',
        'Stromerzeuger 14 kVA'
      ]
    },
    'LFA': {
      name: 'Löschfahrzeug mit Allrad',
      desc: 'Sicherstellung der Wasserversorgung und flexibler Einsatz durch Rollcontainer-System.',
      tech: [
        { label: 'Taktische Bezeichnung', value: 'LFA' },
        { label: 'Funkrufname', value: 'Pumpe Pfarrwerfen' },
        { label: 'Besatzung', value: '1:8' },
        { label: 'Baujahr', value: '2024' },
        { label: 'Schlauch', value: '1.000m B-Schlauch' }
      ],
      features: [
        'Rollcontainer-Wechselsystem',
        'Ladebordwand am Heck',
        'Schlauchverlegevorrichtung',
        'LED-Umfeldbeleuchtung'
      ],
      equipment: [
        '2 Tragkraftspritzen (Fox 4)',
        '3 Pressluftatmer',
        'Greifzug',
        'Stromerzeuger 9 kVA',
        'Schmutzwasserpumpe'
      ]
    },
    'VRF-A': {
      name: 'Vorausrüstfahrzeug mit Allrad',
      desc: 'Stützpunktgerät des LFV Salzburg für schnelle technische Hilfeleistung.',
      tech: [
        { label: 'Taktische Bezeichnung', value: 'VRFA' },
        { label: 'Funkrufname', value: 'Voraus Pfarrwerfen' },
        { label: 'Besatzung', value: '1:2' }
      ],
      features: [
        'Schnelle Einsatzbereitschaft',
        'Stützpunktfahrzeug'
      ],
      equipment: [
        'Hydraulisches Rettungsgerät',
        'Beleuchtungseinheiten'
      ]
    },
    'MTF': {
      name: 'Mannschaftstransportfahrzeug',
      desc: 'Transport von Mannschaft und Gerät zur Einsatzstelle.',
      tech: [
        { label: 'Taktische Bezeichnung', value: 'MTF' },
        { label: 'Funkrufname', value: 'Bus Pfarrwerfen' },
        { label: 'Besatzung', value: '1:8' }
      ],
      features: [
        'Mannschaftstransport',
        'Einsatzleitung'
      ],
      equipment: [
        'Funkgeräte',
        'Absicherungsmaterial',
        'Erste Hilfe Ausrüstung'
      ]
    }
  };

  const id = decodeURIComponent(page.params.id ?? '');
  const vehicle = vehicles[id as keyof typeof vehicles];
</script>

{#if vehicle}
  <div class="space-y-10">
    <header class="flex items-start justify-between gap-6">
      <div>
        <h2 class="text-3xl font-bold tracking-tight text-[var(--color-on-surface)] uppercase">{id}</h2>
        <p class="text-[var(--color-on-surface-variant)] font-medium">{vehicle.name}</p>
      </div>
      <a href="{base}/inventory" class="text-xs font-bold text-[var(--color-on-surface-variant)] uppercase tracking-widest border border-[var(--color-outline-variant)]/20 px-4 py-2 rounded-[var(--radius-md)] hover:bg-[var(--color-surface-container-low)] transition-colors">
        Zurück 
      </a>
    </header>

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
      <!-- Info Column -->
      <div class="lg:col-span-2 space-y-8">
        <section class="bg-[var(--color-surface-container-low)] p-8 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10">
          <h3 class="text-sm font-bold uppercase tracking-widest text-[var(--color-primary)] mb-4">Beschreibung</h3>
          <p class="text-lg leading-relaxed">{vehicle.desc}</p>
        </section>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <section class="bg-[var(--color-surface-container-lowest)] p-6 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10 shadow-sm">
            <h3 class="text-sm font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] mb-4 border-b border-[var(--color-outline-variant)]/10 pb-2">Ausstattung</h3>
            <ul class="space-y-3">
              {#each vehicle.features as feature}
                <li class="flex items-center gap-3 text-sm font-medium">
                  <span class="w-1.5 h-1.5 bg-[var(--color-primary)] rounded-full"></span>
                  {feature}
                </li>
              {/each}
            </ul>
          </section>

          <section class="bg-[var(--color-surface-container-lowest)] p-6 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10 shadow-sm">
            <h3 class="text-sm font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] mb-4 border-b border-[var(--color-outline-variant)]/10 pb-2">Beladung</h3>
            <ul class="space-y-3">
              {#each vehicle.equipment as item}
                <li class="flex items-center gap-3 text-sm font-medium">
                  <span class="text-[var(--color-primary)]">➔</span>
                  {item}
                </li>
              {/each}
            </ul>
          </section>
        </div>
      </div>

      <!-- Tech Specs Sidebar -->
      <aside class="space-y-6">
        <div class="bg-[var(--color-surface-container-high)] p-6 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10">
          <h3 class="text-xs font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] mb-6">Technische Daten</h3>
          <div class="space-y-4">
            {#each vehicle.tech as spec}
              <div>
                <p class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] opacity-60 mb-1">{spec.label}</p>
                <p class="font-bold text-sm">{spec.value}</p>
              </div>
            {/each}
          </div>
        </div>

        <div class="p-6 border border-dashed border-[var(--color-outline-variant)]/20 rounded-[var(--radius-md)]">
          <p class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] opacity-60 mb-2">Letzte Prüfung</p>
          <p class="text-xs font-bold uppercase tracking-tight text-[var(--color-success)]">OK - GESTERN, 14:30</p>
        </div>
      </aside>
    </div>
  </div>
{:else}
  <div class="p-20 text-center">
    <p class="text-[var(--color-on-surface-variant)] font-bold uppercase tracking-widest">Fahrzeug nicht gefunden</p>
    <a href="{base}/inventory" class="mt-4 inline-block text-[var(--color-primary)] font-bold uppercase text-xs tracking-widest">Zurück zur Übersicht</a>
  </div>
{/if}
