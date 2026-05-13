<script lang="ts">
	import { base } from '$app/paths';
	import { page } from '$app/state';
	import './layout.css';
	let { children } = $props();

	const navItems = [
		{ href: `${base}/`, label: 'Status', icon: '📊' },
		{ href: `${base}/inventory`, label: 'Fahrzeuge', icon: '🚒' },
		{ href: `${base}/stock`, label: 'Lager', icon: '📦' },
		{ href: `${base}/checklists`, label: 'Setup', icon: '⚙️' }
	];
</script>

<svelte:head>
	<title>FD Inventory Tracker - FW Pfarrwerfen</title>
</svelte:head>

<div class="min-h-screen flex flex-col md:flex-row bg-[var(--color-surface)]">
	<!-- Tactical Sidebar (Monolith) -->
	<nav class="w-full md:w-64 bg-[var(--color-surface-container-high)] flex flex-col border-r border-[var(--color-outline-variant)]/10">
		<div class="p-6 mb-4">
			<h1 class="text-xl font-bold tracking-tight text-[var(--color-primary)] uppercase">FW Pfarrwerfen</h1>
			<p class="text-[10px] text-[var(--color-on-surface-variant)] font-bold uppercase tracking-widest mt-1">Salzburg Org. Nr. 3.04.01</p>
		</div>
		
		<div class="flex-1 px-3 space-y-1">
			{#each navItems as item}
				<a 
					href={item.href} 
					class="flex items-center px-4 py-3 text-sm font-medium rounded-[var(--radius-md)] transition-all {page.url.pathname === item.href ? 'bg-[var(--color-surface-container-lowest)] text-[var(--color-primary)] shadow-sm font-semibold' : 'text-[var(--color-on-surface-variant)] hover:bg-[var(--color-surface-container-highest)]'}"
				>
					<span class="mr-3">{item.icon}</span> {item.label}
				</a>
			{/each}
		</div>

		<div class="p-4 mt-auto">
			<div class="bg-[var(--color-surface-container-low)] p-4 rounded-[var(--radius-md)] border border-[var(--color-outline-variant)]/10">
				<div class="flex items-center justify-between mb-2">
					<span class="text-[10px] font-bold uppercase tracking-widest text-[var(--color-on-surface-variant)]">System</span>
					<div class="w-2 h-2 bg-[var(--color-success)] rounded-full"></div>
				</div>
				<p class="text-[10px] text-[var(--color-on-surface-variant)] font-medium">Betriebsbereit</p>
			</div>
		</div>
	</nav>

	<!-- Main Content Area (Tactical Monolith) -->
	<main class="flex-1 overflow-y-auto">
		<div class="max-w-6xl mx-auto p-6 md:p-12">
			{@render children()}
		</div>
	</main>
</div>
