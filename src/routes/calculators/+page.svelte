<script lang="js">
    import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
    import Navbar from '../component/Navbar.svelte';
	import { goto } from '$app/navigation';

    function Dosage() {
        goto ('/calculators/dosage');
    }

    function IVFlow() {
        goto ('/calculators/iv-flow');
    }

    const divStyle_button = "py-3 bg-gradient-to-r from-sky-500 to-sky-800 rounded-lg text-white font-bold mt-5 mb-10 ml-5 hover:from-sky-800 hover:to-sky-500 transition-colors duration-300";
    const divStyle2_button = "py-3 bg-gradient-to-r from-sky-500 to-sky-800 rounded-lg text-white font-bold mt-11 mb-10 ml-5 hover:from-sky-800 hover:to-sky-500 transition-colors duration-300";
    const divStyle = "w-[30%] border border-gray-300 rounded-lg flex flex-col pl-5 shadow-xl px-10";
    const h1Style = "text-2xl font-bold mt-5 mb-1 ml-5";
    const pStyle = "ml-5";
</script>

<Navbar />

<h1 class="text-3xl font-bold my-10 ml-10">Drug Calculation Tools</h1>
    <p class="text-xl text-gray-600 ml-10 mb-5">Select a calculator to perform accurate medication calculations for your clinical practice.</p>
<div class="w-full flex flex-wrap items-start justify-center pb-10 gap-10">
    <div class={divStyle}>
        <h1 class={h1Style}>Dosage Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate medication dosages based on patient weight</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate dosages using the formula:<br>Dose = Weight × Dose per kg</p>
        <button onclick={Dosage} class={divStyle_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>

    <div class={divStyle}>
        <h1 class={h1Style}>IV Flow Rate Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate drip rates and infusion times</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate flow rates using the formula:<br>Flow Rate (mL/hr) = (Volume × Drip Factor) ÷ Time</p>
        <button onclick={IVFlow} class={divStyle_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>

    <div class={divStyle}>
        <h1 class={h1Style}>Pediatric Dosage Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate pediatric dosages based on weight or BSA</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate pediatric dosages using weight or BSA.<br>BSA (m²) = √(Height (cm) × Weight (kg) ÷ 3600)</p>
        <button class={divStyle_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>

    <div class={divStyle}>
        <h1 class={h1Style}>Dilution Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate medication dilutions and concentrations</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate dilutions using the formula:<br>Concentration = Amount of drug ÷ Volume</p>
        <button class={divStyle2_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>

    <div class={divStyle}>
        <h1 class={h1Style}>Unit Conversion</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Convert between different units of measurement</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Convert between common units used in medication:<br>mg ↔ mcg ↔ g ↔ kg, mL ↔ L</p>
        <button class={divStyle2_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>

    <div class={divStyle}>
        <h1 class={h1Style}>Infusion Rate Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate medication infusion rates</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate infusion rates using the formula:<br>Rate (mL/hr) = (Dose × Weight × 60) ÷ Concentration</p>
        <button class={divStyle_button}>Calculate Dosage <FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
    </div>
</div>