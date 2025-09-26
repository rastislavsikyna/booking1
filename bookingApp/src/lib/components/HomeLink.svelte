
<script lang="ts">
  import { goto } from '$app/navigation';

 let {
  name, url
 }=$props()

  function goHome(url:string) {
    goto(url);
  }
</script>

<main class="flex min-h-screen w-full items-center justify-center">

  <section class="group flex items-start ">
  <button class="home-button  text-4xl ; " onclick={()=>goHome(url)} >{name}</button>

  <span class="text-sm group-hover:ml-10 text-purple-700 group-hover:translate-x-2,5 
    font font-semibold transition-all duration-500 ease-linear group-hover:bounce "
    >Click</span>

  </section>

  </main>

