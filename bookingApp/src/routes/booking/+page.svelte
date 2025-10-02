<script lang="ts">
    import Timer from '$lib/components/Timer.svelte';
	import HomeLink from '$lib/components/HomeLink.svelte';
    import type { PageProps } from './$types';
    


    let { data }: PageProps = $props();
</script>
<main class="justify-center items-center text-center">
	<h1>Actual Time</h1>
	<Timer />
    <HomeLink name={'Home'} url={'/'}/>

    <div>
    <div class=" justify-center items-center text-center ">
        

  <section class="group flex items-start justify-center mt-60">
  <button class="  border rounded-t-4xl pl-20 pr-20 pb-3 pt-3 text-3xl bg-gray-300 hover:bg-gray-400 cursor-pointer ">One-way Flight</button> 

   
  </section>
  <section>
     <button class=" border rounded-b-4xl pl-24 pr-24 pt-3 pb-3 bg-gray-300 text-3xl hover:bg-gray-400 cursor-pointer">Return Flight</button> 
  </section>

    </div>
</div>
</main>




