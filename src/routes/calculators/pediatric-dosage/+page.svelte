<script lang="js">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import Navbar from "../../component/Navbar.svelte";

    let activeTab = $state('bsa');
    let height = $state('');
    let weight = $state('');
    let bsaSubmitted = $state(false);
    let pdcSubmitted = $state(false);
    let bsaResult = $state(0);

    let selectedWeightOption = $state('kg');
    let weightOptions = [
        { value:'kg', label: 'kg' },
        { value:'lbs', label: 'lbs' }
    ]

    let selectedHeightOption = $state('cm');
    let heightOptions = [
        { value:'m', label: 'm' },
        { value:'cm', label: 'cm' },
        { value:'in', label: 'in' }
    ]

    function convertHeight() {
    if (!height) return 0;
    if (selectedHeightOption === 'm') {
        return parseFloat(height) * 100;
    } else if (selectedHeightOption === 'in') {
        return parseFloat(height) * 2.54;
    } 
    return parseFloat(height);
}

function convertWeight() {
    if (!weight) return 0;
    if (selectedWeightOption === 'lbs') {
        return parseFloat(weight) * 0.45359237;
    }
    return parseFloat(weight);
}

     function calculateBSA() {
        bsaSubmitted = true;
        
        const heightInCm = convertHeight();
        const weightInKg = convertWeight();

        bsaResult = Math.sqrt((heightInCm * weightInKg) / 3600).toFixed(2);
    }

    const inputStyle = "border p-2 rounded mb-2";
 </script>

<Navbar />
<div class="w-[50%] flex flex-col mx-auto">
    <p class="font-bold text-3xl mt-8 ml-5">Pediatric Dosage Calculator</p>
    <div class="w-full my-5 border border-gray-300 py-4 rounded-xl shadow-lg">
        <p class="text-lg mx-5">Important</p>
        <p class="mx-5">This calculator is for educational purposes. Always verify calculations and follow your institution's protocols.</p>
    </div>

    <div class="flex w-full bg-gray-100 rounded-lg overflow-hidden">
      <button
        class="w-1/2 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
        class:bg-white={activeTab === 'bsa'}
        class:text-black={activeTab === 'bsa'}
        class:text-gray-400={activeTab !== 'bsa'}
        onclick={() => activeTab = 'bsa'}
      >
        BSA Calculator
      </button>

      <button
        class="w-1/2 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
        class:bg-white={activeTab === 'pdc'}
        class:text-black={activeTab === 'pdc'}
        class:text-gray-400={activeTab !== 'pdc'}
        onclick={() => activeTab = 'pdc'}
      >
        Pediatric Dosage Calculator
      </button>
    </div>

    {#if activeTab === 'bsa'}
        <div class="w-full border border-gray-300 py-4 rounded-xl px-7 shadow-lg mt-5">
        <p class="text-2xl font-bold flex flex-col">Pediatric Dosage Calculator</p>
        <p class="text-sm mb-5 text-gray-500">Calculate pediatric dosages using weight or BSA. BSA (m²) = √(Height (cm) × Weight (kg) ÷ 3600)</p>
        
        <label for="patient-weight" class="text-m mb-2 text-left">Patient Weight:</label>
        <div class="flex justify-between mb-5">
        <input type="number" bind:value={weight} placeholder="Enter weight" class={`${inputStyle} w-[60%]`} />
        <select bind:value={selectedWeightOption} class={`${inputStyle} w-[35%] pl-5`}>
            {#each weightOptions as option}
                <option value={option.value}>{option.label}</option>
            {/each}
        </select>
        </div>

        <label for="dosage-per-kg" class="text-m mb-2 text-left">Patient Height:</label>
        <div class="flex justify-between mb-5">
        <input type="number" bind:value={height} placeholder= "Enter height"  class={`${inputStyle} w-[60%]`} />
        <select bind:value={selectedHeightOption} class={`${inputStyle} w-[35%] pl-5`}>
            {#each heightOptions as unit}
                <option value={unit.value}>{unit.label}</option>
            {/each}
        </select>
        </div>

        {#if bsaSubmitted && (!weight || !height)}
            <p class="text-red-500 mb-4">Please enter height and weight</p>
        {:else if bsaSubmitted && weight && height}
            <div class="w-full mb-5 bg-sky-100 p-4 rounded">
                <label for="Calculated Dose" class="text-lg">Calculated Dose:</label>
                <p class="font-bold text-3xl my-1">{`${bsaResult} m²`}</p>
                <p>{`Based on √(${convertHeight()} (cm) × ${convertWeight()} (kg) ÷ 3600)`}</p>
            </div>
        {/if}

        <button onclick={calculateBSA} class="py-2 mb-4 bg-sky-600 text-white px-10 rounded-lg w-full hover:bg-blue-700 transition hover:scale-100">Calculate Body Surface Area (BSA)</button>
    </div>
        
    {/if}
</div>

