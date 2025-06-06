<script>
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import Navbar from '../../component/Navbar.svelte';

	let submitted = $state(false);
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

	function calculateConcentration() {
		submitted = true;

		concentration = (amount / volume).toFixed(2);
	}

	const inputStyle = 'border p-2 rounded mb-2';
	const pStyle = 'my-2 ml-5';
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
				bind:value={volume}
				placeholder="Enter volume"
				class={`${inputStyle} w-[60%]`}
			/>
			<select bind:value={selectedvolumeOptions} class={`${inputStyle} w-[35%] pl-5`}>
				{#each volumeOptions as option}
					<option value={option.value}>{option.label}</option>
				{/each}
			</select>
		</div>

		{#if submitted && (!amount || !volume)}
			<p class="mb-4 text-red-500">Please enter weight and dose</p>
		{:else if submitted && amount && volume}
			<div class="mb-5 w-full rounded bg-sky-100 p-4">
				<label for="Calculated Dilution" class="text-lg">Calculated Dilution:</label>
				<p class="my-1 text-3xl font-bold">
					{concentration}
					{selectedamountOptions}/{selectedvolumeOptions}
				</p>
				<p>{`Based on ${amount} ${selectedamountOptions} ÷ ${volume} ${selectedvolumeOptions}`}</p>
			</div>
		{/if}

		<button
			onclick={calculateConcentration}
			class="my-5 w-full rounded-lg bg-sky-600 px-10 py-2 text-white transition hover:scale-100 hover:bg-blue-700"
			>Calculate Pediatric Dose</button
		>
	</div>

	<div class="w-full">
		<p class="my-5 ml-5 text-2xl font-bold">How to Use This Calculator</p>
		<p class={pStyle}>1. Enter the amount of drug</p>
		<p class={pStyle}>2. Enter the volume in</p>
		<p class={pStyle}>3. Select the appropriate units for weight and dose</p>
		<p class={pStyle}>4. Click "Calculate Dilution" to determine the Drug Dilution</p>
	</div>

	<div class="mt-5 mb-10 rounded-lg bg-sky-100 p-4">
		<p class="text-xl font-bold">Formula Used:</p>
		<p class="my-2 text-lg">Concentration = Amount of drug (mg, g, mL) ÷ Volume (mL, L)</p>
		<p class="text-sm">
			There will no base unit so unit of dilution depends on the selected unit for each the volume
			and amount of dose.
		</p>
	</div>
</div>
