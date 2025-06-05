<script lang="js">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import Navbar from "../../component/Navbar.svelte";

    let activeTab = $state('bsa');
    let height = $state('');
    let weight = $state('');
    let bsaSubmitted = $state(false);
    let pdcSubmitted = $state(false);
    let bsaResult = $state(0);
    let adultDose = $state('');
    let patientBSA = $state('');
    let PediatricDose = $state(0);

    let selectedAdultDose = $state('mg');
    let adultDoseOption = [
        { value: 'mg', label: 'mg' },
        { value: 'mcg', label: 'mcg' },
        { value: 'g', label: 'g' }
    ];

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

    function calculatePediatricDose() {
        pdcSubmitted = true;

        PediatricDose = ((patientBSA / 1.73) * adultDose).toFixed(2);
    }
    
    const pStyle = "my-2 ml-5";
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
    {:else if activeTab === 'pdc'}
        <div class="w-full border border-gray-300 py-4 rounded-xl px-7 shadow-lg my-5">
            <p class="text-2xl font-bold flex flex-col">Pediatric Dosage Calculator</p>
            <p class="text-sm mb-5 text-gray-500">Calculate pediatric dosages based on (BSA m² / 1.73) x Adult Dose</p>
            
            <div class="flex flex-col mb-5">
            <label for="patient-weight" class="text-m mb-2 text-left">Body Surface Area:</label>
            <input type="number" bind:value={patientBSA} placeholder="Enter Body Surface Area" />
            </div>

            <label for="patient-weight" class="text-m text-left">Adult Dose:</label>
                <div class="flex justify-between mb-5">
                    <input type="number" bind:value={adultDose} placeholder="Enter adult dose" class={`${inputStyle} w-[60%]`}/>
                    <select bind:value={selectedAdultDose} class={`${inputStyle} w-[35%] pl-5`}>
                    {#each adultDoseOption as option}
                        <option value={option.value}>{option.label}</option>
                    {/each}
                    </select>
                </div>

                {#if pdcSubmitted && (!adultDose || !patientBSA)}
            <p class="text-red-500 mb-4">Please enter adult dose and patient BSA</p>
        {:else if pdcSubmitted && adultDose && patientBSA}
            <div class="w-full mb-5 bg-sky-100 p-4 rounded">
                <label for="Calculated Dose" class="text-lg">Calculated Dose:</label>
                <p class="font-bold text-3xl my-1">{`${PediatricDose} ${selectedAdultDose}`}</p>
                <p>{`Based on (${patientBSA} m² / 1.73) x ${adultDose}`}</p>
            </div>
        {/if}

        <button onclick={calculatePediatricDose} class="py-2 mb-4 bg-sky-600 text-white px-10 rounded-lg w-full hover:bg-blue-700 transition hover:scale-100">Calculate Pediatric Dose</button>
        </div>
    {/if}

    <div class="w-full">
        <p class="font-bold my-5 ml-5 text-2xl">How to Use This Calculator</p>
         <p class="text-lg ml-5">Body Surface Area (BSA) Calculator:</p>
        <p class={pStyle}>1.  Enter the weight of the patient</p>
        <p class={pStyle}>2.  Enter the height of the patient</p>
        <p class={pStyle}>3.  Click "Calculate Body Surface Area (BSA)" to determine the BSA</p>

         <p class="text-lg ml-5 mt-5">Pediatric Dosage Calculator:</p>
        <p class={pStyle}>1.  Enter the Body Surface Area (BSA)</p>
        <p class={pStyle}>2.  Select the appropriate unit for the adult dose (g, mg, mcg)</p>
        <p class={pStyle}>3.  Click "Calculate Pediatric Dose" to determine the Pediatric Dose based on the BSA of the patient</p>
  </div>

  <div class="bg-sky-100 p-4 rounded-lg mt-5 mb-10">
        <p class="font-bold text-xl">Formula Used:</p>
        <p class="my-2 text-lg">Body Surface Area (m²) = √(Height (cm) × Weight (kg) ÷ 3600)</p>
        <p class="my-2 text-lg">Pediatric Dose = (BSA m² / 1.73) x Adult Dose</p>
  </div>
</div>

