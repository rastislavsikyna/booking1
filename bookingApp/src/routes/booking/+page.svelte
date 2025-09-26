<script lang="ts">
    import Timer from '$lib/components/Timer.svelte';
	import HomeLink from '$lib/components/HomeLink.svelte';
    import type { PageProps } from './$types';
    


    let { data }: PageProps = $props();
</script>
<main>
	<h1>Actual Time</h1>
	<Timer />
</main>

<HomeLink name={'Home'} url={'/'}/>

