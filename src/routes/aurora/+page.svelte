<script lang="ts">
	import Aurora from '$lib/assets/Aurora.png';
	import Hallway from '$lib/assets/HallwayDark.png';
	import Save from '$lib/assets/save.png';
	import MaintLight from '$lib/assets/MaintLight.png';
</script>

<main>
	<h1>NOBODY HERE YET!</h1>
</main>

<style>
	.carousel {
		/* How many slides sit in the scrollport at once. Fractional on purpose:
		   the leftover part-slide is what tells you the strip keeps going, and
		   it guarantees the content overflows the port no matter how wide the
		   card gets — no overflow would mean no scroll travel, and no scroll
		   travel means the view timeline never advances and nothing pans. */
		--visible: 2.5;
		--gap: 1.5rem;
		--slide-height: clamp(18rem, 46vh, 32rem);

		flex-basis: 100%;
	}
	/* 
				The Beckoning of Aurora takes place in an alternate universe where a second space race
				happened, being dubbed as the Silver Age Space Race with the previous one being renamed as
				the Gold Space Race, this time however it was primarily driven by corporations in 2038, with
				humanity taking it's first steps in colonizing Earth's neighboring planets, and by 2048 were
				able to venture out of the Solar system unto it's neighbors to push their colonization work
				by that point in time only 8 companies remaining active on this effort, forming the
				Humanitarian Space Consortium (HSC) to better push and standardize their space faring
				activities. This rapid expansion as well as population booms made it so approximately 38% of
				humanity worked for one of those companies or their subsidiares, with things remaining
				relatively prosperous for the next decade. In 2060 however one of the biggest events in
				human history happened, as contact was lost on a colony ship and it's escort was lost 2
				hours after confirmed landing, it was then after a fleet was sent to investigate that
				humanity had confirmed their contact with a sapient extraterrestiral species, known as
				Kaanins a species which shared a few similarities with Earth's canines. A war broke out
				between both species with humanity having won due to huge technological gap between them.
				The following years were of great hostility, with the Kaanins essentialy working by force to
				the HSC with few rights, leading to at some point in 2074 after years of not only diplomacy
				but the also from the UN deciding to not only intervene and act upon humanitie's space
				activities after decades of neglecting these, made it so Kaanins were fully integrated in
				human society, as well as forcing the HSC to be rebranded as the Human Kaanin Consortium,
				due to deciding that with the integration of both species, that the interest of both should
				be united and explored rather than having a fully humanity first approach. In 2080 in order
				to show the friendlyness between both species, the ship Dawn of the New Aurora was revealed
				as a joint effort between both, being an enormous research vessel that could house the best
				scientists of both sides for long term research, and in 2101 after being auctioned by the
				HKC to the Interstellar Travel Group, which will lead to a series of events that start The
				Beckoning of Aurora. There is much more to the universe than that which I'm always happy to
				share, with this serving as a much more condensed version of it.
	*/

	.slides {
		width: 100%;
		padding: 0;
		list-style: none;
		white-space: nowrap;
		background: #000;
		outline: 1px solid #333;
		border-radius: 0.5rem;
		overflow-x: auto;
		overflow-y: hidden;
		overscroll-behavior-x: contain;
		scroll-snap-type: x mandatory;
		touch-action: pan-x;
	}

	.slide {
		display: inline-block;
		position: relative;
		/* Percentages here resolve against the scrollport, not the strip. */
		width: calc((100% - (var(--visible) - 1) * var(--gap)) / var(--visible));
		height: var(--slide-height);
		margin: 0;
		padding: 0;
		vertical-align: top;
		list-style: none;
		scroll-snap-align: center;
		/* Use clip, not hidden: `hidden` would make each slide its own scroll
		   container and steal the view timeline from the carousel. */
		overflow: clip;
	}

	.slide + .slide {
		margin-left: var(--gap);
	}

	.slide > img {
		display: block;
		width: 100%;
		height: 100%;
		/* Stick 'm to the right of their frame. */
		position: absolute;
		right: 0;
	}

	@media screen and (max-width: 600px) {
		.carousel {
			/* 2.5 across a phone leaves slivers; show one and a peek instead. */
			--visible: 1.25;
			--gap: 1rem;
		}
	}
</style>
