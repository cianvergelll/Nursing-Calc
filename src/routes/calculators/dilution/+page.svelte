<script>
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import Navbar from '../../component/Navbar.svelte';

	let volume = $state('');
	let amount = $state('');
	let concentration = $state(0);

	let selectedvolumeOptions = $state('mL');
	let volumeOptions = [
		{ label: 'mL', value: 'mL' },
		{ label: 'L', value: 'L' }
	];

	let selectedamountOptions = $state('mg');
	let amountOptions = [
		{ label: 'mg', value: 'mg' },
		{ label: 'g', value: 'g' },
		{ label: 'mL', value: 'mL' }
	];

	const inputStyle = 'border p-2 rounded mb-2';
</script>

<Navbar />

<div class="mx-auto flex w-[50%] flex-col">
	<p class="mt-8 ml-5 text-3xl font-bold">Dilution Calculator</p>
	<div class="my-5 w-full rounded-xl border border-gray-300 py-4 shadow-lg">
		<p class="mx-5 text-lg font-medium">Important</p>
		<p class="mx-5">
			This calculator is for educational purposes. Always verify calculations and follow your
			institution's protocols.
		</p>
	</div>

	<div class="w-full rounded-xl border border-gray-300 px-7 py-4 shadow-xl">
		<p class="flex flex-col text-2xl font-bold">Dilution Calculator</p>
		<p class="mb-5 text-sm text-gray-500">
			Calculate dilutions using Concentration = Amount of drug ÷ Volume
		</p>

		<label for="patient-weight" class="text-m text-left">Amount of Drug</label>
		<div class="mb-5 flex justify-between">
			<input
				type="number"
				bind:value={amount}
				placeholder="Enter adult dose"
				class={`${inputStyle} w-[60%]`}
			/>
			<select bind:value={selectedamountOptions} class={`${inputStyle} w-[35%] pl-5`}>
				{#each amountOptions as option}
					<option value={option.value}>{option.label}</option>
				{/each}
			</select>
		</div>

		<label for="patient-weight" class="text-m text-left">Volume</label>
		<div class="flex justify-between">
			<input
				type="number"
				bind:value={amount}
				placeholder="Enter volume"
				class={`${inputStyle} w-[60%]`}
			/>
			<select bind:value={selectedvolumeOptions} class={`${inputStyle} w-[35%] pl-5`}>
				{#each volumeOptions as option}
					<option value={option.value}>{option.label}</option>
				{/each}
			</select>
		</div>
	</div>
</div>
