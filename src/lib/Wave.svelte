<script lang="ts">
	type Props = {
		text: string | undefined;
	};
	let { text }: Props = $props();
</script>

{#each text as char, index (index)}
	<span class="wavy" style={`--i: ${index}`}>{char}</span>
{/each}
