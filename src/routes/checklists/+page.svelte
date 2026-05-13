<script lang="ts">
  const checklists = [
    { title: 'Wöchentliche Fahrzeugprüfung', desc: 'Standardüberprüfung aller Systeme und Geräte.', vehicle: 'Alle Fahrzeuge', time: '15 min' },
    { title: 'Monatsprüfung Tragkraftspritzen', desc: 'Probelauf und Funktionsprüfung der TS.', vehicle: 'LFA, TLF-A 3000', time: '30 min' },
    { title: 'Atemschutz Jahresprüfung', desc: 'Detaillierte Prüfung der AS-Geräte und Masken.', vehicle: 'TLF-A 3000, LFA', time: '45 min' },
  ];
</script>

<div class="space-y-10">
  <header>
    <h2 class="text-3xl font-bold tracking-tight text-[var(--color-on-surface)] uppercase">Setup & Checklisten</h2>
    <p class="text-[var(--color-on-surface-variant)] font-medium">Standardisierte Abläufe für die Instandhaltung</p>
  </header>

  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
    {#each checklists as list}
      <div class="bg-[var(--color-surface-container-low)] p-6 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10 relative overflow-hidden group hover:border-[var(--color-primary)]/30 transition-all">
        <div class="absolute left-0 top-0 w-1 h-full bg-[var(--color-primary)] opacity-20"></div>
        
        <div class="flex justify-between items-start mb-6">
          <div class="text-2xl">📋</div>
          <span class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)] bg-[var(--color-surface-container-high)] px-2 py-1 rounded">
            {list.time}
          </span>
        </div>
        
        <h3 class="text-lg font-bold mb-2 uppercase tracking-tight group-hover:text-[var(--color-primary)] transition-colors">{list.title}</h3>
        <p class="text-xs text-[var(--color-on-surface-variant)] font-medium mb-8 leading-relaxed">{list.desc}</p>
        
        <div class="flex items-center justify-between mt-auto pt-4 border-t border-[var(--color-outline-variant)]/10">
          <span class="text-[10px] font-bold text-[var(--color-on-surface-variant)] uppercase tracking-widest opacity-60">{list.vehicle}</span>
          <button class="text-[10px] font-bold text-[var(--color-primary)] uppercase tracking-widest hover:underline transition-all">
            Starten ➔
          </button>
        </div>
      </div>
    {/each}

    <!-- Add New Template (Monolith Style) -->
    <div class="border-2 border-dashed border-[var(--color-outline-variant)]/20 rounded-[var(--radius-md)] p-6 flex flex-col items-center justify-center text-center hover:bg-[var(--color-surface-container-low)] transition-colors cursor-pointer min-h-[220px]">
      <span class="text-3xl mb-3 text-[var(--color-on-surface-variant)] opacity-40">➕</span>
      <p class="font-bold uppercase text-[10px] tracking-widest text-[var(--color-on-surface-variant)] opacity-60">Neue Prüfvorlage Erstellen</p>
    </div>
  </div>
</div>
