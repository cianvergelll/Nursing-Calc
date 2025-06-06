<script>
	import Navbar from '../../component/Navbar.svelte';
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';

	let activeTab = $state('solid');
	let unitVolume = $state('');
	let unitMass = $state('');

	let resultMassUnit = $state(0);

	let selectedBaseUnit = $state('mg');
	let BaseUnitOption = [
		{ label: 'mg', value: 'mg' },
		{ label: 'g', value: 'g' },
		{ label: 'kg', value: 'kg' },
		{ label: 'mcg', value: 'mcg' }
	];

	let selectedResultUnit = $state('mg');
	let ResultUnitOption = [
		{ label: 'milligrams', value: 'mg' },
		{ label: 'grams', value: 'g' },
		{ label: 'kilograms', value: 'kg' },
		{ label: 'micrograms', value: 'mcg' }
	];

	let selectedBaseVolumeUnit = $state('mL');
	let BaseVolumeUnitOption = [
		{ label: 'mL', value: 'mL' },
		{ label: 'L', value: 'L' }
	];

	let selectedResultVolumeUnit = $state('mL');
	let ResultVolumeUnitOption = [
		{ label: 'milliliters', value: 'mL' },
		{ label: 'liters', value: 'L' }
	];

	const inputStyle = 'border p-2 rounded mb-2';
	const pStyle = 'my-2 ml-5';

	function calculateMassUnit() {}
</script>

<Navbar />
<div class="mx-auto flex w-[50%] flex-col">
	<p class="mt-8 ml-5 text-3xl font-bold">Unit Converter</p>
	<div class="my-5 w-full rounded-xl border border-gray-300 py-4 shadow-lg">
		<p class="mx-5 text-lg font-medium">Important</p>
		<p class="mx-5">
			This calculator is for educational purposes. Always verify calculations and follow your
			institution's protocols.
		</p>
	</div>

	<div class="flex w-full overflow-hidden rounded-lg bg-gray-100">
		<button
			class="m-1 w-1/2 rounded-md py-1 text-center font-medium transition-all duration-300"
			class:bg-white={activeTab === 'solid'}
			class:text-black={activeTab === 'solid'}
			class:text-gray-400={activeTab !== 'solid'}
			onclick={() => (activeTab = 'solid')}
		>
			Mass Units
		</button>

		<button
			class="m-1 w-1/2 rounded-md py-1 text-center font-medium transition-all duration-300"
			class:bg-white={activeTab === 'liquid'}
			class:text-black={activeTab === 'liquid'}
			class:text-gray-400={activeTab !== 'liquid'}
			onclick={() => (activeTab = 'liquid')}
		>
			Volume Units
		</button>
	</div>

	{#if activeTab === 'solid'}
		<div class="mt-5 w-full rounded-xl border border-gray-300 px-7 py-4 shadow-xl">
			<p class="flex flex-col text-2xl font-bold">Mass (Weight) Units</p>
			<p class="mb-5 text-sm text-gray-500">
				Convert common mass unit conversions used in medication calculations
			</p>

			<label for="Unit" class="text-m text-left">Base unit</label>
			<div class="mb-5 flex justify-between">
				<input
					type="number"
					bind:value={unitMass}
					placeholder="Enter value"
					class={`${inputStyle} w-[60%]`}
				/>

				<select bind:value={selectedBaseUnit} class={`${inputStyle} w-[35%] pl-5`}>
					{#each BaseUnitOption as option}
						<option value={option.value}>{option.label}</option>
					{/each}
				</select>
			</div>

			<label for="UnitResult" class="text-m text-left">Convert to</label>
			<div class="mb-5 flex justify-between">
				<select bind:value={selectedResultUnit} class={`${inputStyle} w-full pl-5`}>
					{#each ResultUnitOption as option}
						<option value={option.value}>{option.label}</option>
					{/each}
				</select>
			</div>

			<button
				onclick={calculateConcentration}
				class="my-5 w-full rounded-lg bg-sky-600 px-10 py-2 text-white transition hover:scale-100 hover:bg-blue-700"
				>Convert Unit</button
			>
		</div>
	{:else}
		<div class="mt-5 w-full rounded-xl border border-gray-300 px-7 py-4 shadow-xl">
			<p class="flex flex-col text-2xl font-bold">Volume Units</p>
			<p class="mb-5 text-sm text-gray-500">
				Convert common volume unit conversions used in medication calculations
			</p>

			<label for="Unit" class="text-m text-left">Base unit</label>
			<div class="mb-5 flex justify-between">
				<input
					type="number"
					bind:value={unitVolume}
					placeholder="Enter value"
					class={`${inputStyle} w-[60%]`}
				/>

				<select bind:value={selectedBaseVolumeUnit} class={`${inputStyle} w-[35%] pl-5`}>
					{#each BaseVolumeUnitOption as option}
						<option value={option.value}>{option.label}</option>
					{/each}
				</select>
			</div>

			<label for="UnitResult" class="text-m text-left">Convert to</label>
			<div class="mb-5 flex justify-between">
				<select bind:value={selectedResultVolumeUnit} class={`${inputStyle} w-full pl-5`}>
					{#each ResultVolumeUnitOption as option}
						<option value={option.value}>{option.label}</option>
					{/each}
				</select>
			</div>

			<button
				onclick={calculateConcentration}
				class="my-5 w-full rounded-lg bg-sky-600 px-10 py-2 text-white transition hover:scale-100 hover:bg-blue-700"
				>Convert Unit</button
			>
		</div>
	{/if}

	<div class="w-full">
		<p class="my-5 ml-5 text-2xl font-bold">How to Use This Calculator</p>
		<p class="ml-5 text-lg">Mass (Weight) Calcaulator</p>
		<p class={pStyle}>1. Enter the value and select the base unit</p>
		<p class={pStyle}>2. Select the appropriate value to convert into</p>
		<p class={pStyle}>3. Click "convert Unit" to determine the resulting unit value</p>

		<p class="mt-5 ml-5 text-lg">Volume Calculator</p>
		<p class={pStyle}>1. Enter the value and select the base unit</p>
		<p class={pStyle}>2. Select the appropriate value to convert into</p>
		<p class={pStyle}>3. Click "convert Unit" to determine the resulting unit value</p>
	</div>

	<div class="mt-5 mb-10 rounded-lg bg-sky-100 p-4">
		<p class="text-xl font-bold">Formula Used:</p>
		<p class="my-2 text-lg">Flow Rate (mL/hr) = Volume (mL) ÷ Time (hours)</p>
		<p class="my-2 text-lg">
			Drip Rate (drops/min) = (Flow Rate (mL/hr) × Drop Factor (drops/mL)) ÷ 60
		</p>
		<p class="text-sm">
			If time is entered in minutes, it is first converted to hours using the conversion factor 1
			hour = 60 minutes.
		</p>
	</div>
</div>
