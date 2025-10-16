<script lang="ts">
    import Timer from '$lib/components/Timer.svelte';
	import HomeLink from '$lib/components/HomeLink.svelte';
    import type { PageProps } from './$types';
    


    let { data }: PageProps = $props();
    let infoModal = $state('')
    let infoModal2 = $state('')
    
// ONEWAY STATE
    let isOneWayCalendar = $state(false);
    let OneWayDateTime = $state <string>('');
    let oneWayList = $state<string[]>([]);

// RETURN STATE
    let ReturnFlightDateTime = $state <string>();
    let ReturnFlightDateTime2 = $state <string>();
    let isReturnFlightCalendar = $state(false);
    let ReturnList = $state<string[]>([]);
    let ReturnList2 = $state<string[]>([]);

 //  LOGIC ONEWAY
    function handleOneWayBook() {
      if (OneWayDateTime) {
      oneWayList.pop();
      oneWayList.push(OneWayDateTime)
      localStorage.setItem('Oneway', oneWayList.toString())

      infoModal = 'Thank you for choosing your Date. Modal closing...'
      setTimeout(() =>{
        isOneWayCalendar = false
        infoModal= ''
      }, 3000);
     
    }else{
      infoModal = 'Please fill Flight Date'

    } } 
   $effect(() =>{
    let getLc = localStorage.getItem('oneWay');
    oneWayList = getLc ? [getLc] : [];
   })

  // LOGIC RETURN
   function handleReturnBook() {
      if (ReturnFlightDateTime) {
      ReturnList.pop();
      ReturnList.push(ReturnFlightDateTime)
      localStorage.setItem('Return', ReturnList.toString())

      infoModal2 = 'Thank you for choosing your Date. Modal closing...'
      setTimeout(() =>{
        isReturnFlightCalendar = false
        infoModal2= ''
      }, 3000);
     
    }else{
      infoModal2 = 'Please fill Flight Date'

    } } 
   $effect(() =>{
    let getLc = localStorage.getItem('Return');
    ReturnList = getLc ? [getLc] : [];
   })
   
  // LOGIC RETURN 2
  function handleReturnBook2() {
      if (ReturnFlightDateTime) {
      ReturnList2.pop();
      ReturnList2.push(ReturnFlightDateTime)
      localStorage.setItem('Return', ReturnList.toString())

      infoModal = 'Thank you for choosing your Date. Modal closing...'
      setTimeout(() =>{
        isReturnFlightCalendar = false
        infoModal2= ''
      }, 3000);
     
    }else{
      infoModal2 = 'Please fill Flight Date'

    } } 
   $effect(() =>{
    let getLc = localStorage.getItem('Return');
    ReturnList2 = getLc ? [getLc] : [];
   })
    
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
   class="  border rounded-t-4xl pl-20 p-20 pb-3 pt-3 text-3xl bg-gray-300 hover:bg-gray-400 cursor-pointer ">One-way Flight</button> 

   
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



<!-- INPUTCALENDAR -->
   <input type="datetime-local" bind:value={OneWayDateTime} class="w-3xs mx-auto"> 
     <p class=" font-bold text-purple-600">{infoModal}</p>
<div class="flex gap-10 justify-center mt-10 m-4"> 



   <!-- SUMBIT -->
  <button class="border rounded-2xl p-3 cursor-pointer hover:bg-green-200"
    
        onclick={() => {
          handleOneWayBook();
        }} >Submit</button>

  
   <!-- CLOSE -->
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

 <!-- INPUT RETURN -->
<input type="datetime-local" bind:value={ReturnFlightDateTime} class="w-3xs mx-auto"> 
      
    <div class="flex gap-10 justify-center mt-10 m-4"> <div>

<!-- RETURN2 -->
<input type="datetime-local" bind:value={ReturnFlightDateTime2} class="w-3xs mx-auto"> 
    <p class=" font-bold text-purple-600">{infoModal2}</p>
   <div class="flex justify-center gap-10 mt-10 m-4 "></div>


<!-- SUBMIT -->
<div class="flex justify-center gap-10 mt-6">
  <button class="border rounded-2xl p-3 cursor-pointer hover:bg-green-200"
    onclick={() => {
          handleReturnBook();
          handleReturnBook2();
        }} >Submit</button>

  <!-- CLOSE -->

    <button class="border rounded-2xl p-3  cursor-pointer hover:bg-red-200 "
    onclick={() => {
        isReturnFlightCalendar= false
    }}
    >Close</button>
    </div>
      </div>
       </div>
       </div>
</section>
 {/if}

<!-- ONEWAY -->
<article>
  {#each oneWayList as item}
  <div class=" mt-10 flex justify-center gap-5 flex-col">
    <p class=" font-bold text-2xl ">Booked Succesfully</p>
   <p>{item}</p> 

  <button
  class=" text-red-500  font-bold cursor-pointer"
   onclick={() =>{
    oneWayList = [];
  }} >Delete</button>

 
  </div>
 {/each}
</article>

<!-- RETURN -->

<article>
  {#each ReturnList2 as item}
  <div class=" mt-10 flex justify-center gap-5 flex-col">
    <p class=" font-bold text-2xl ">Booked Succesfully</p>
   <p>{item}</p> 

  <button
  class=" text-red-500  font-bold cursor-pointer"
   onclick={() =>{
    ReturnList = [];
    ReturnList2 = [];
  }} >Delete</button>

 
  </div>
 {/each}
</article>

</main>




