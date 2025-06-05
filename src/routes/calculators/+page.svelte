<script lang="js">
    import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
    import Navbar from '../component/Navbar.svelte';

    const divStyle = "w-[30%] border border-gray-300 rounded-lg flex flex-col pl-5 shadow-xl px-10 mx-auto";
    const h1Style = "text-3xl font-bold mt-5 mb-1 ml-5";
    const pStyle = "ml-5 mb-5";
</script>

<Navbar />
<div class="w-full flex flex-col items-start justify-center">

    <h1 class="text-3xl font-bold my-10 ml-20">Drug Calculation Tools</h1>
    <p class="text-xl text-gray-600 ml-20 mb-5">Select a calculator to perform accurate medication calculations for your clinical practice.</p>
    <div class={divStyle}>
        <h1 class={h1Style}>Dosage Calculator</h1>
        <p class={`${pStyle} text-sm text-gray-600`}>Calculate medication dosages based on patient weight</p>
        <FontAwesomeIcon icon="flask" class="text-5xl text-sky-800 my-5" />
        <p class={pStyle}>Calculate dosages using the formula:<br>Dose = Weight × Dose per kg</p>
        <button>Calculate Dosage</button>
    </div>
</div>