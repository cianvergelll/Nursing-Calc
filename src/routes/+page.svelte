<script lang="js">
	import { goto } from "$app/navigation";
    import Navbar from "./component/Navbar.svelte";
    import '../icons';
    import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';

    function handleDosageCalc() {
        goto('/calculators/dosage');
    }

    function handleIVFlowCalc() {
        goto('/calculators/iv-flow');
    }

    function handlePDosageCalc() {
        goto('/calculators/pediatric-dosage');
    }

    const divStyle ="w-[30%] border border-gray-300 rounded-lg flex flex-col pl-5 shadow-xl";
    const divStyle_h1 = "font-bold text-3xl mt-7 ml-5";
    const divStyle_p = "text-s ml-5 text-gray-600 mb-5";
    const divStyle_h2 = "text-lg px-5";
    const divStyle_button = "py-3 bg-gradient-to-r from-sky-500 to-sky-800 w-[40%] rounded-lg text-white font-bold my-10 ml-5 hover:from-sky-800 hover:to-sky-500 transition hover:scale-105 transition-colors duration-300";
</script>

<div class="w-full flex flex-col items-center justify-start overflow-x-hidden">
    <Navbar />
    <h1 class="text-5xl font-bold mt-10 mb-5">Nursing Drug Calculations</h1>
    <p class="text-xl mb-10">Accurate and reliable drug calculation tools for nursing professionals and students.</p>

    <div class="w-full h-[40%] flex flex-row justify-center items-center">
        <div class= {`${divStyle} mx-auto`}>
            <h1 class={divStyle_h1}>Dosage Calculator</h1>
            <p class={divStyle_p}>Calculate medication dosage from patient data</p>
            <h2 class={divStyle_h2}>Access tools for calculating dosages based on weight, body surface area, and other factors.</h2>
            <button class={divStyle_button} on:click={handleDosageCalc}>Get Started<FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
        </div>

        <div class={`${divStyle} mx-auto`}>
            <h1 class={divStyle_h1}>IV Flow Rate</h1>
            <p class={divStyle_p}>Calculate drip rates and infusion times</p>
            <h2 class={divStyle_h2}>Tools for calculating IV flow rates, drip factors, and infusion durations.</h2>
            <button class={divStyle_button} on:click={handleIVFlowCalc}>Calculate Now<FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
        </div>

        <div class={`${divStyle} mx-auto`}>
            <h1 class={divStyle_h1}>Pediatric Calculations</h1>
            <p class={divStyle_p}>Specialized calculations for pediatric patients</p>
            <h2 class={divStyle_h2}>Age and weight-based dosing calculators specifically designed for pediatric care.</h2>
            <button class={divStyle_button} on:click={handlePDosageCalc}>Explore Now<FontAwesomeIcon icon="arrow-right" class="inline ml-2" /></button>
        </div>
    </div>

    <div class="bg-sky-100 w-[95%] my-10 rounded-xl shadow-xl flex flex-col">
        <h1 class={divStyle_h1}>Why Use NurseCalc?</h1>
        <div class="flex flex-row justify-between px-5 py-5 my-5">
            <div class="flex flex-col items-center">
                <h1 class="text-2xl font-bold">Accurate Calculations</h1>
                <FontAwesomeIcon icon="calculator" class="text-5xl text-sky-800 my-5" />
                <h2 class={divStyle_h2}>Validated formulas based on current clinical standards</h2>
            </div>
            <div class="flex flex-col items-center">
                <h1 class="text-2xl font-bold">Educational Resources</h1>
                <FontAwesomeIcon icon="book" class="text-5xl text-sky-800 my-5" />
                <h2 class={divStyle_h2}>Learn the principles behind drug calculations</h2>
            </div>
            <div class="flex flex-col items-center">
                <h1 class="text-2xl font-bold">Reference Materials</h1>
                <FontAwesomeIcon icon="exclamation-circle" class="text-5xl text-sky-800 my-5" />
                <h2 class={divStyle_h2}>Quick access to formulas and conversion factors</h2>
            </div>
        </div>
    </div>
</div>