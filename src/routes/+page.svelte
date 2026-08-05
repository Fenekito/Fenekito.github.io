<script lang="ts">
	import { resolve } from '$app/paths';
	import { Coverflow, type CoverflowItem } from '$lib';
	import Aurora from '$lib/assets/Aurora.png';
	import Fenekito from '$lib/assets/Fenekito.png';
	import Slide from '$lib/assets/SlideCover.png';
	import misc from '$lib/assets/imageNebo.png';

	const items: CoverflowItem[] = [
		{ title: 'About', subtitle: 'Know more about me', href: resolve('/about'), src: Fenekito },
		{
			title: 'The Beckoning of Aurora',
			subtitle: "About The current game I'm working on",
			src: Aurora
		},
		{ title: 'Slide!', subtitle: 'About Slide!', src: Slide },
		{ title: 'Misc', subtitle: 'Some other cool stuff!', src: misc }
	].map((item) => ({ ...item, alt: `${item.title} — ${item.subtitle}` }));
</script>

<svelte:head>
	<title>Fenekito</title>
</svelte:head>

<main>
	<h1 style="position: fixed; top: 0%; left: 35%;">THIS IS STILL A WORK IN PROGRESS</h1>
	<h2 style="position: fixed; top: 5%; left: 40%;">SOME LINKS ARE NOT ACCESSIBLE!</h2>
	<header>
		<h3>Navigate using your mouse wheel or by clicking on the covers!</h3>
		<button command="show-modal" commandfor="info">Not seeing animations?</button>
	</header>
	<Coverflow {items} label="Sections" />
	<dialog id="info">
		<p>
			If you're in firefox and not seeing the coverflow animations, scroll-driven animations may be
			disabled. You can turn these on by going to about:config and changing <strong
				>layout.css.scroll-driven-animations.enabled</strong
			> from false to true.
		</p>
		<button commandfor="info" command="close">Close</button>
	</dialog>
</main>
