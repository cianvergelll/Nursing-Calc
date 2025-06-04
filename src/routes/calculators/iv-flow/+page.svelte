<script lang="js">
    let activeTab = $state('mlhr');
    let volume = $state('');
    let infusionTime = $state('');
    let submitted = $state(false);
    let volumeInMl = $state('');

    let selectedTimeUnit = $state('hr');
    let timeOptions = [
        { value: 'hr', label: 'hours' },
        { value: 'min', label: 'minutes' }
    ];

    function convertTime() {
      if (selectedTimeUnit === 'min') {
        return parseFloat(infusionTime) / 60;
      }
    }
    
    function calculateIVFlowRate() {
        submitted = true;
        let timeInHours = convertTime();
        volumeInMl = parseFloat(volume) / timeInHours;
    }

    const inputStyle = "border p-2 rounded mb-2";
</script>

<div class="w-[50%] flex flex-col mx-auto">
  <p class="font-bold text-3xl mt-8 ml-5">Dosage Calculator</p>
    <div class="w-full my-5 border border-gray-300 py-4 rounded-xl shadow-lg">
        <p class="text-lg mx-5 font-medium">Important</p>
        <p class="mx-5">This calculator is for educational purposes. Always verify calculations and follow your institution's protocols.</p>
    </div>

    <div class="flex w-full bg-gray-100 rounded-lg overflow-hidden">
      <button
        class="w-1/2 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
        class:bg-white={activeTab === 'mlhr'}
        class:text-black={activeTab === 'mlhr'}
        class:text-gray-400={activeTab !== 'mlhr'}
        onclick={() => activeTab = 'mlhr'}
      >
        mL/hr Calculator
      </button>

      <button
        class="w-1/2 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
        class:bg-white={activeTab === 'drip'}
        class:text-black={activeTab === 'drip'}
        class:text-gray-400={activeTab !== 'drip'}
        onclick={() => activeTab = 'drip'}
      >
        Drip Rate Calculator
      </button>
    </div>

  <!-- Content area -->
  {#if activeTab === 'mlhr'}
    <div class="w-full border border-gray-300 py-4 rounded-xl px-7 shadow-xl my-5">
        <p class="text-2xl font-bold flex flex-col">IV Flow Rate Calculator (mL/hr)</p>
        <p class="text-sm mb-5 text-gray-500">Calculate the flow rate in mL/hr using the formula: Flow Rate = Volume ÷ Time</p>
        
        <div class="flex flex-col mb-5">
          <label for="patient-weight" class="text-m mb-2 text-left">Total Volume (mL)</label>
          <input type="number" bind:value={volumeInMl} placeholder="Enter volume in mL" />
        </div>

        <div class="flex  mb-5">
          <label for="patient-weight" class="text-m mb-2 text-left">Infusion Time</label>
          <input type="number" bind:value={infusionTime} placeholder="Enter time" class={`${inputStyle} w-[60%]`}/>
          <select bind:value={selectedTimeUnit} class={`${inputStyle} w-[35%]`}>
            {#each timeOptions as option}
                <option value={option.value}>{option.label}</option>
            {/each}
        </select>
        </div>
    </div>
  {:else}
    <div class="w-full border border-gray-300 py-4 rounded-xl px-7 shadow-xl my-5">
        <p class="text-2xl font-bold flex flex-col">Drip Rate Calculator (drops/min)</p>
        <p class="text-sm mb-5 text-gray-500">Calculate the drip rate in drops per minute using the formula: Drip Rate = (Flow Rate × Drop Factor) ÷ 60</p>
        
        <label for="patient-weight" class="text-m mb-2 text-left">Flow Rate (mL/hr)</label>
        <div class="flex justify-between mb-5">
        </div>
    </div>
  {/if}

</div>