<script lang="ts">
	import { resolve } from '$app/paths';
	type routes = '/' | '/aurora' | '/misc' | '/slide';
	type Props = {
		text: string;
		href: routes;
		description: string | undefined;
	};
	let { text, href, description }: Props = $props();
</script>

<a href={resolve(href)}><button aria-label={description}>{text}</button></a>
