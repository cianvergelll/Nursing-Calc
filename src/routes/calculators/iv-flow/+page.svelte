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

    let selecteddripFactor = $state('20');
    let dropFactorOptions = [
      { value: '10', label: '10 drops/mL (Macrodrip)' },
      { value: '15', label: '15 drops/mL (Macrodrip)' },
      { value: '20', label: '20 drops/mL (Macrodrip)' },
      { value: '60', label: '60 drops/mL (Microdrip)' }
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
     const pStyle = "my-2 ml-5";
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

        <label for="patient-weight" class="text-m mb-5 text-left">Infusion Time</label>
        <div class="flex justify-between mb-5">
          <input type="number" bind:value={infusionTime} placeholder="Enter time" class={`${inputStyle} w-[60%]`}/>
          <select bind:value={selectedTimeUnit} class={`${inputStyle} w-[35%] pl-5`}>
            {#each timeOptions as option}
                <option value={option.value}>{option.label}</option>
            {/each}
        </select>
        </div>
        <button onclick={calculateIVFlowRate} class="py-2 mb-4 bg-sky-600 text-white px-10 rounded-lg w-full hover:bg-blue-700 transition hover:scale-100">Calculate Flow Rate</button>
    </div>
  {:else}
    <div class="w-full border border-gray-300 py-4 rounded-xl px-7 shadow-xl my-5">
        <p class="text-2xl font-bold flex flex-col">Drip Rate Calculator (drops/min)</p>
        <p class="text-sm mb-5 text-gray-500">Calculate the drip rate in drops per minute using the formula: Drip Rate = (Flow Rate × Drop Factor) ÷ 60</p>
        
        <div class="flex flex-col mb-5">
          <label for="patient-weight" class="text-m mb-2 text-left">Flow Rate (mL/hr)</label>
          <input type="number" bind:value={volumeInMl} placeholder="Enter flow rate in mL/hr" />
        </div>

        <div class="flex flex-col mb-5">
          <label for="patient-weight" class="text-m mb-2 text-left">Drop Factor (drops/mL)</label>
          <select bind:value={selecteddripFactor} class={`${inputStyle} pl-5`}>
              {#each dropFactorOptions as option}
                  <option value={option.value}>{option.label}</option>
              {/each}
          </select>
        </div>
        <button onclick={calculateIVFlowRate} class="py-2 mb-4 bg-sky-600 text-white px-10 rounded-lg w-full hover:bg-blue-700 transition hover:scale-100">Calculate Drip Rate</button>
    </div>

  {/if}

  <div class="w-full">
        <p class="font-bold my-5 ml-5 text-2xl">How to Use This Calculator</p>
         <p class="text-lg ml-5">mL/hr Calculator:</p>
        <p class={pStyle}>1.  Enter the total volume to be infused in milliliters (mL)</p>
        <p class={pStyle}>2.  Enter the infusion time in hours or minutes</p>
        <p class={pStyle}>3.  Click "Calculate Flow Rate" to determine the flow rate in mL/hr</p>

         <p class="text-lg ml-5 mt-5">Drip Rate Calculator:</p>
        <p class={pStyle}>1.  Enter the flow rate in mL/hr</p>
        <p class={pStyle}>2.  Select the appropriate drop factor based on your IV tubing (10, 15, 20, or 60 drops/mL)</p>
        <p class={pStyle}>3.  Click "Calculate Drip Rate" to determine the drip rate in drops/min</p>
  </div>

  <div class="bg-sky-100 p-4 rounded-lg mt-5 mb-10">
        <p class="font-bold text-xl">Formula Used:</p>
        <p class="my-2 text-lg">Flow Rate (mL/hr) = Volume (mL) ÷ Time (hours)</p>
        <p class="my-2 text-lg">Drip Rate (drops/min) = (Flow Rate (mL/hr) × Drop Factor (drops/mL)) ÷ 60</p>
        <p class="text-sm">If time is entered in minutes, it is first converted to hours using the conversion factor 1 hour = 60 minutes.</p>
  </div>

</div>