<script module lang="ts">
	export type CoverflowItem = {
		src: string;
		alt?: string;
		title?: string;
		subtitle?: string;
		href?: string;
	};
</script>

<script lang="ts">
	import '$lib/coverflow.css';
	type Props = {
		items: CoverflowItem[];
		size?: string;
		rotation?: string;
		overlap?: number;
		reflection?: boolean;
		label?: string;
		wheel?: boolean;
		class?: string;
	};

	let {
		items,
		size,
		rotation,
		overlap,
		reflection = true,
		label = 'Covers',
		wheel = true,
		class: className = ''
	}: Props = $props();

	let track: HTMLUListElement;

	const slotWidth = () =>
		track.querySelector<HTMLElement>('.cf-item')?.getBoundingClientRect().width ?? 0;

	function step(direction: number) {
		track.scrollBy({ left: direction * slotWidth(), behavior: 'smooth' });
	}

	function centre(item: Element) {
		item.scrollIntoView({ behavior: 'smooth', inline: 'center', block: 'nearest' });
	}

	function offsetFromCentre(item: Element) {
		const port = track.getBoundingClientRect();
		const box = item.getBoundingClientRect();
		return box.left + box.width / 2 - (port.left + port.width / 2);
	}

	$effect(() => {
		if (!wheel) return;
		let acc = 0;

		function onwheel(event: WheelEvent) {
			const delta = Math.abs(event.deltaX) > Math.abs(event.deltaY) ? event.deltaX : event.deltaY;
			if (!delta) return;
			event.preventDefault();

			if (Math.sign(delta) !== Math.sign(acc)) acc = 0;
			acc += delta;
			if (Math.abs(acc) < 40) return;

			acc = 0;
			step(Math.sign(delta));
		}

		track.addEventListener('wheel', onwheel, { passive: false });
		return () => track.removeEventListener('wheel', onwheel);
	});

	function onclick(event: MouseEvent) {
		// Leave new-tab and new-window clicks to the browser.
		if (event.metaKey || event.ctrlKey || event.shiftKey || event.altKey) return;

		const item = (event.currentTarget as HTMLElement).closest('.cf-item');
		if (!item) return;

		if (Math.abs(offsetFromCentre(item)) > 8) {
			event.preventDefault();
			centre(item);
		}
	}
</script>

{#snippet face(item: CoverflowItem, mirror: boolean)}
	<span class="cf-face">
		<img src={item.src} alt={mirror ? '' : (item.alt ?? item.title ?? '')} draggable="false" />
		<span class="cf-gloss"></span>
		<span class="cf-shade"></span>
		{#if !mirror}<span class="cf-edge"></span>{/if}
	</span>
{/snippet}

{#snippet cover(item: CoverflowItem)}
	{@render face(item, false)}

	{#if reflection}
		<span class="cf-mirror" aria-hidden="true">
			{@render face(item, true)}
		</span>
	{/if}
{/snippet}

<div
	class="coverflow {className}"
	class:cf-flat={!reflection}
	style:--cf-size={size}
	style:--cf-rot={rotation}
	style:--cf-overlap={overlap}
>
	<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
	<ul class="cf-track" bind:this={track} role="list" aria-label={label}>
		{#each items as item, i (i)}
			<li class="cf-item">
				{#if item.href}
					<!-- eslint-disable-next-line svelte/no-navigation-without-resolve -- hrefs come from the caller, already resolved -->
					<a class="cf-cover" href={item.href} {onclick}>
						{@render cover(item)}
					</a>
				{:else}
					<a class="cf-cover unavailable" aria-disabled="true">
						{@render cover(item)}
					</a>
				{/if}
				<span class="cf-caption" aria-hidden="true">
					<h2>{item.title}</h2>
					<h3>{item.subtitle}</h3>
				</span>
			</li>
		{/each}
	</ul>
</div>
