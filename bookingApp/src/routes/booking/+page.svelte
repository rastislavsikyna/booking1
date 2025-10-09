<script lang="ts">
    import Timer from '$lib/components/Timer.svelte';
	import HomeLink from '$lib/components/HomeLink.svelte';
    import type { PageProps } from './$types';
    


    let { data }: PageProps = $props();

    let isOneWayCalendar = $state(false);
    let isReturnFlightCalendar = $state(false);
    let OneWayDateTime = $state <Date>();
    $inspect(OneWayDateTime)

    let ReturnFlightDateTime = $state <Date>();
    $inspect(ReturnFlightDateTime)

    let ReturnFlightDateTime2 = $state <Date>();
    $inspect(ReturnFlightDateTime2)
</script>


<main class="justify-center items-center text-center relative">
	<h1>Actual Time</h1>
	<Timer />
    <HomeLink name={'Home'} url={'/'}/>

    <div>
    <div class=" justify-center items-center text-center ">
        

  <section class="group flex items-start justify-center mt-60">
  <button onclick={() =>{
    isReturnFlightCalendar = false
    isOneWayCalendar= true  }
}
   class="  border rounded-t-4xl pl-20 pr-20 pb-3 pt-3 text-3xl bg-gray-300 hover:bg-gray-400 cursor-pointer ">One-way Flight</button> 

   
  </section>
  <section>
     <button onclick={() =>{
    isReturnFlightCalendar = true
    isOneWayCalendar= false  }
} class=" border rounded-b-4xl pl-24 pr-24 pt-3 pb-3 bg-gray-300 text-3xl hover:bg-gray-400 cursor-pointer">Return Flight</button> 
  </section>

    </div>
</div>


<!-- Oneway -->
 {#if isOneWayCalendar}
 <section class="bg-gray-500/10 backdrop-blur-sm h-full w-full absolute left-0 top-0 min-h-screen ">
  <div class="relative flex w-lg flex-col  border border-black mx-auto lg:mt-44 rounded-3xl shadow-2xl  ">
   <h1 class="text-2xl">One-Way Flight</h1>

   <input type="datetime-local" bind:value={OneWayDateTime} class="w-3xs mx-auto"> 
<div class="flex gap-10 justify-center mt-10 m-4"> 
   
  <button class="border rounded-2xl p-3 cursor-pointer hover:bg-green-200"
    onclick={() => {
        isOneWayCalendar= false
    }}
    >Submit</button>

  

    <button class="border rounded-2xl p-3  cursor-pointer hover:bg-red-200"
    onclick={() => {
        isOneWayCalendar= false
    }}
    >Close</button>
    </div>


 </section>
 {/if}

 <!-- Return -->

   {#if isReturnFlightCalendar}
 <section class="bg-gray-500/10 backdrop-blur-sm h-full w-full absolute left-0 top-0 min-h-screen ">
  <div class="relative flex w-lg flex-col  border border-black mx-auto lg:mt-44 rounded-3xl shadow-2xl  ">
   <h1 class="text-2xl">Return Flight</h1>

<input type="datetime-local" bind:value={ReturnFlightDateTime} class="w-3xs mx-auto"> 
    <div class="flex gap-10 justify-center mt-10 m-4"> <div>

<input type="datetime-local" bind:value={ReturnFlightDateTime2} class="w-3xs mx-auto"> 
   <div class="flex justify-center gap-10 mt-10 m-4 "></div>



<div class="flex justify-center gap-10 mt-6">
  <button class="border rounded-2xl p-3 cursor-pointer hover:bg-green-200"
    onclick={() => {
        isReturnFlightCalendar= false
    }}
    >Submit</button>

  

    <button class="border rounded-2xl p-3  cursor-pointer hover:bg-red-200 "
    onclick={() => {
        isReturnFlightCalendar= false
    }}
    >Close</button>
    </div>
      </div>
       </div>
       </div>
"</section>
 {/if}




</main>




