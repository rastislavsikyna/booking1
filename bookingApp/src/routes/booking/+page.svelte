<script lang="ts">
	import Timer from '$lib/components/Timer.svelte';
	import HomeLink from '$lib/components/HomeLink.svelte';
	import type { PageProps } from './$types';

	let { data }: PageProps = $props();
	let infoModal = $state('');
	let infoModal2 = $state('');

	// ONEWAY STATE
	let isOneWayCalendar = $state(false);
	let OneWayDateTime = $state<string>('');
	let oneWayList = $state<string[]>([]);

	// RETURN STATE
	let returnFlight = $state<string[]>([]);
	let ReturnFlightDateTime = $state<string>();
	let ReturnFlightDateTime2 = $state<string>();
	let isReturnFlightCalendar = $state(false);

	//  LOGIC ONEWAY
	function handleOneWayBook() {
		if (OneWayDateTime) {
			oneWayList.pop();
			oneWayList.push(OneWayDateTime);
			localStorage.setItem('Oneway', oneWayList.toString());

			infoModal = 'Thank you for choosing your Date. Modal closing...';
			setTimeout(() => {
				isOneWayCalendar = false;
				infoModal = '';
			}, 3000);
		} else {
			infoModal = 'Please fill Flight Date';
		}
	}

	// LOGIC RETURN
	function handleReturnBook() {
		if (ReturnFlightDateTime && ReturnFlightDateTime2) {
			returnFlight.slice(0, returnFlight.length);
			localStorage.setItem('Return', ReturnList.toString());

			infoModal2 = 'Thank you for choosing your Date. Modal closing...';
			setTimeout(() => {
				isReturnFlightCalendar = false;
				infoModal2 = '';
			}, 3000);
		} else {
			infoModal2 = 'Please fill Flight Date';
		}
	}

	$effect(() => {
		let getLc = localStorage.getItem('oneWay');
		let getReturnLc = localStorage.getItem('returnFlight');
		oneWayList = getLc ? [getLc] : [];
		returnFlight = getReturnLc ? returnFlight : [];
	});

	// $inspect(ReturnList, ReturnList2);
</script>

<main class="relative items-center justify-center text-center">
	<h1>Actual Time</h1>
	<Timer />
	<HomeLink name={'Home'} url={'/'} />

	<div>
		<div class=" items-center justify-center text-center">
			<section class="group mt-60 flex items-start justify-center">
				<button
					onclick={() => {
						isReturnFlightCalendar = false;
						isOneWayCalendar = true;
					}}
					class="  rounded-t-4xl cursor-pointer border bg-gray-300 p-20 pb-3 pl-20 pt-3 text-3xl hover:bg-gray-400"
					>One-way Flight</button
				>
			</section>
			<section>
				<button
					onclick={() => {
						isReturnFlightCalendar = true;
						isOneWayCalendar = false;
					}}
					class=" rounded-b-4xl cursor-pointer border bg-gray-300 pb-3 pl-24 pr-24 pt-3 text-3xl hover:bg-gray-400"
					>Return Flight</button
				>
			</section>
		</div>
	</div>

	<!-- Oneway -->
	{#if isOneWayCalendar}
		<section
			class="absolute left-0 top-0 h-full min-h-screen w-full bg-gray-500/10 backdrop-blur-sm"
		>
			<div
				class="w-lg relative mx-auto flex flex-col rounded-3xl border border-black shadow-2xl lg:mt-44"
			>
				<h1 class="text-2xl">One-Way Flight</h1>

				<!-- INPUTCALENDAR -->
				<input type="datetime-local" bind:value={OneWayDateTime} class="w-3xs mx-auto" />
				<p class=" font-bold text-purple-600">{infoModal}</p>
				<div class="m-4 mt-10 flex justify-center gap-10">
					<!-- SUMBIT -->
					<button
						class="cursor-pointer rounded-2xl border p-3 hover:bg-green-200"
						onclick={() => {
							handleOneWayBook();
						}}>Submit</button
					>

					<!-- CLOSE -->
					<button
						class="cursor-pointer rounded-2xl border p-3 hover:bg-red-200"
						onclick={() => {
							isOneWayCalendar = false;
						}}>Close</button
					>
				</div>
			</div>
		</section>
	{/if}

	<!-- Return -->

	{#if isReturnFlightCalendar}
		<section
			class="absolute left-0 top-0 h-full min-h-screen w-full bg-gray-500/10 backdrop-blur-sm"
		>
			<div
				class="w-lg relative mx-auto flex flex-col rounded-3xl border border-black shadow-2xl lg:mt-44"
			>
				<h1 class="text-2xl">Return Flight</h1>

				<!-- INPUT RETURN -->
				<input type="datetime-local" bind:value={ReturnFlightDateTime} class="w-3xs mx-auto" />

				<div class="m-4 mt-10 flex justify-center gap-10">
					<div>
						<!-- RETURN2 -->
						<input type="datetime-local" bind:value={ReturnFlightDateTime2} class="w-3xs mx-auto" />
						<p class=" font-bold text-purple-600">{infoModal2}</p>
						<div class="m-4 mt-10 flex justify-center gap-10"></div>

						<!-- SUBMIT -->
						<div class="mt-6 flex justify-center gap-10">
							<button
								class="cursor-pointer rounded-2xl border p-3 hover:bg-green-200"
								onclick={() => {
									handleReturnBook();
								}}>Submit</button
							>

							<!-- CLOSE -->

							<button
								class="cursor-pointer rounded-2xl border p-3 hover:bg-red-200"
								onclick={() => {
									isReturnFlightCalendar = false;
								}}>Close</button
							>
						</div>
					</div>
				</div>
			</div>
		</section>
	{/if}

	<!-- ONEWAY -->
	<article>
		{#each oneWayList as item}
			<div class=" mt-10 flex flex-col justify-center gap-5">
				<p class=" text-2xl font-bold">Booked Succesfully</p>
				<p>{item}</p>

				<button
					class=" cursor-pointer font-bold text-red-500"
					onclick={() => {
						oneWayList = [];
					}}>Delete</button
				>
			</div>
		{/each}
	</article>

	<!-- RETURN -->

	<article>
		{#each ReturnList2 as item}
			<div class=" mt-10 flex flex-col justify-center gap-5">
				<p class=" text-2xl font-bold">Booked Succesfully</p>
				<p>{item}</p>

				<button
					class=" cursor-pointer font-bold text-red-500"
					onclick={() => {
						ReturnList = [];
						ReturnList2 = [];
					}}>Delete</button
				>
			</div>
		{/each}
	</article>
</main>
