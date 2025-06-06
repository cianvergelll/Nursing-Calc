<script lang="js">
	import Navbar from '../../component/Navbar.svelte';
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';

	const inputStyle = 'border p-2 rounded mb-2';
	const pStyle = 'my-2 ml-5';
	let totalDose = $state(0);
	let weight = $state('');
	let dosePerKg = $state('');
	let submitted = $state(false);
	let selectedWeightUnit = $state('kg');
	let weightOptions = [
		{ value: 'kg', label: 'kg' },
		{ value: 'lbs', label: 'lbs' }
	];

	let selectedDosageUnit = $state('mg');
	let dosageUnits = [
		{ value: 'mg', label: 'mg' },
		{ value: 'mcg', label: 'mcg' },
		{ value: 'g', label: 'g' }
	];

	function convertWeight() {
		if (selectedWeightUnit === 'lbs') {
			return parseFloat(weight) * 0.45359237;
		}
		return parseFloat(weight);
	}

	function convertDosage() {
		if (selectedDosageUnit === 'mcg') {
			return parseFloat(dosePerKg) / 1000;
		} else if (selectedDosageUnit === 'g') {
			return parseFloat(dosePerKg) * 1;
		}
		return parseFloat(dosePerKg);
	}

	let weightInKg = $state(0);

	function calculateDosage() {
		submitted = true;

		weightInKg = convertWeight();
		let dosePerKgValue = convertDosage();
		totalDose = (weightInKg * dosePerKgValue).toFixed(2);
	}
</script>

<Navbar />
<div class="mx-auto flex w-[50%] flex-col">
	<p class="mt-8 ml-5 text-3xl font-bold">Dosage Calculator</p>
	<div class="my-5 w-full rounded-xl border border-gray-300 py-4 shadow-lg">
		<p class="mx-5 text-lg">Important</p>
		<p class="mx-5">
			This calculator is for educational purposes. Always verify calculations and follow your
			institution's protocols.
		</p>
	</div>

	<div class="w-full rounded-xl border border-gray-300 px-7 py-4 shadow-lg">
		<p class="flex flex-col text-2xl font-bold">Weight Based Calculator</p>
		<p class="mb-5 text-sm text-gray-500">
			Calculate medication dosage based on patient weight using the formula: Dose = Weight × Dose
			per kilogram (kg)
		</p>

		<label for="patient-weight" class="text-m mb-2 text-left">Patient Weight:</label>
		<div class="mb-5 flex justify-between">
			<input
				type="number"
				bind:value={weight}
				placeholder="Enter weight"
				class={`${inputStyle} w-[60%]`}
			/>
			<select bind:value={selectedWeightUnit} class={`${inputStyle} w-[35%] pl-5`}>
				{#each weightOptions as option}
					<option value={option.value}>{option.label}</option>
				{/each}
			</select>
		</div>

		<label for="dosage-per-kg" class="text-m mb-2 text-left">Dose Per kg:</label>
		<div class="mb-5 flex justify-between">
			<input
				type="number"
				bind:value={dosePerKg}
				placeholder="Enter dosage"
				class={`${inputStyle} w-[60%]`}
			/>
			<select bind:value={selectedDosageUnit} class={`${inputStyle} w-[35%] pl-5`}>
				{#each dosageUnits as unit}
					<option value={unit.value}>{unit.label}</option>
				{/each}
			</select>
		</div>

		{#if submitted && (!weight || !dosePerKg)}
			<p class="mb-4 text-red-500">Please enter weight and dose</p>
		{:else if submitted && weight && dosePerKg}
			<div class="mb-5 w-full rounded bg-sky-100 p-4">
				<label for="Calculated Dose" class="text-lg">Calculated Dose:</label>
				<p class="my-1 text-3xl font-bold">{totalDose}{selectedDosageUnit}</p>
				<p>{`Based on ${weightInKg} kg × ${dosePerKg} ${selectedDosageUnit}/kg`}</p>
			</div>
		{/if}

		<button
			onclick={calculateDosage}
			class="mb-4 w-full rounded-lg bg-sky-600 px-10 py-2 text-white transition hover:scale-100 hover:bg-blue-700"
			>Calculate Dose</button
		>
	</div>

	<div class="w-full">
		<p class="my-5 ml-5 text-2xl font-bold">How to Use This Calculator</p>
		<p class={pStyle}>1. Enter the patient's weight in the specified unit (kg or lb)</p>
		<p class={pStyle}>2. Enter the prescribed dose per kg</p>
		<p class={pStyle}>3. Select the appropriate units for weight and dose</p>
		<p class={pStyle}>4. Click "Calculate Dose" to determine the total dose</p>
	</div>

	<div class="mt-5 mb-10 rounded-lg bg-sky-100 p-4">
		<p class="text-xl font-bold">Formula Used:</p>
		<p class="my-2 text-lg">Total Dose = Patient Weight (kg) × Dose per kg</p>
		<p class="text-sm">
			If weight is entered in pounds (lb), it is first converted to kilograms (kg) using the
			conversion factor 1 lb = 0.45359237 kg.
		</p>
	</div>
</div>
