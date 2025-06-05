<script lang="js">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import Navbar from "../component/Navbar.svelte";

    let activeTab = $state('cf');
</script>

<Navbar />

<h1 class="text-3xl font-bold my-5 ml-10">Drug Calculation References</h1>
    <p class="text-xl text-gray-600 ml-10 mb-5">Essential formulas, conversion factors, and reference tables for nursing drug calculations.</p>

<div class="w-full">
    <div class="flex bg-gray-100 rounded-lg overflow-hidden w-[95%] mx-auto">
        <button
            class="w-1/3 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
            class:bg-white={activeTab === 'cf'}
            class:text-black={activeTab === 'cf'}
            class:text-gray-400={activeTab !== 'cf'}
            onclick={() => activeTab = 'cf'}
        >
            Common Formulas
        </button>

        <button
            class="w-1/3 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
            class:bg-white={activeTab === 'cfa'}
            class:text-black={activeTab === 'cfa'}
            class:text-gray-400={activeTab !== 'cfa'}
            onclick={() => activeTab = 'cfa'}
        >
            Conversion Factors
        </button>

        <button
            class="w-1/3 py-1 text-center font-medium rounded-md transition-all duration-300 m-1"
            class:bg-white={activeTab === 'abbr'}
            class:text-black={activeTab === 'abbr'}
            class:text-gray-400={activeTab !== 'abbr'}
            onclick={() => activeTab = 'abbr'}
        >
            Medical Abbreviations
        </button>
    </div>

    {#if activeTab === 'cf'}
        <div class="w-[95%] mt-5 mx-auto border border-gray-300 rounded-lg">
            asdas
        </div>
    {:else if activeTab === 'cfa'}

    {:else if activeTab === 'abbr'}

    {/if}
</div>