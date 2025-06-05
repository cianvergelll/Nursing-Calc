<script lang="js">
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import Navbar from "../component/Navbar.svelte";

    let activeTab = $state('cf');

    const tdStyle = "pl-2 py-4";
    const trStyle = "border-b-1 border-gray-200";
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
        <div class="w-[95%] mt-5 mx-auto border border-gray-300 rounded-lg shadow-xl mb-15">
            <h1 class="text-2xl font-medium mt-10 ml-10">Essential Drug Calculation Formulas</h1>
            <p class="text-s text-gray-400 ml-10">Reference guide for commonly used formulas in medication administration</p>

            <h1 class="text-xl font-bold mt-5 ml-10">Basic Dosage Calculations</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[25%] mx-auto">Calculation Type</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Formula</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Example</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Weight-Based Dosing</td>
                        <td class={tdStyle}>Dose = Weight × Dose per kg</td>
                        <td class={tdStyle}>50 kg × 2 mg/kg = 100 mg</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>BSA-Based Dosing</td>
                        <td class={tdStyle}>Dose = BSA × Dose per m²</td>
                        <td class={tdStyle}>1.73 m² × 100 mg/m² = 173 mg</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Desired/Have Method</td>
                        <td class={tdStyle}>(Desired Dose ÷ Have Dose) × Vehicle Volume</td>
                        <td class={tdStyle}>(25 mg ÷ 50 mg) × 2 mL = 1 mL</td>
                    </tr>
                </tbody>
            </table>
            
            <h1 class="text-xl font-bold mt-10 ml-10">IV Calculations</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[25%] mx-auto">Calculation Type</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Formula</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Example</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Flow Rate</td>
                        <td class={tdStyle}>Flow Rate (mL/hr) = Volume (mL) ÷ Time (hr)</td>
                        <td class={tdStyle}>1000 mL ÷ 8 hr = 125 mL/hr</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Drip Rate</td>
                        <td class={tdStyle}>Drip Rate (drops/min) = (Flow Rate × Drop Factor) ÷ 60</td>
                        <td class={tdStyle}>(125 mL/hr × 20 drops/mL) ÷ 60 = 42 drops/min</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Infusion Time</td>
                        <td class={tdStyle}>Time (hr) = Volume (mL) ÷ Flow Rate (mL/hr)</td>
                        <td class={tdStyle}>1000 mL ÷ 125 mL/hr = 8 hr</td>
                    </tr>
                </tbody>
            </table>

            <h1 class="text-xl font-bold mt-10 ml-10">Concentration & Dilution</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto mb-10">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[25%] mx-auto">Calculation Type</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Formula</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Example</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Concentration</td>
                        <td class={tdStyle}>Concentration = Amount of Drug ÷ Volume</td>
                        <td class={tdStyle}>50 mg ÷ 250 mL = 0.2 mg/mL</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Dilution</td>
                        <td class={tdStyle}>C₁V₁ = C₂V₂</td>
                        <td class={tdStyle}>(10 mg/mL)(x mL) = (2 mg/mL)(50 mL); x = 10 mL</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Infusion Rate (mcg/kg/min)</td>
                        <td class={tdStyle}>Rate (mL/hr) = (Dose × Weight × 60) ÷ Concentration</td>
                        <td class={tdStyle}>(5 mcg/kg/min × 70 kg × 60) ÷ 400 mcg/mL = 52.5 mL/hr</td>
                    </tr>
                </tbody>
            </table>
        </div>
    {:else if activeTab === 'cfa'}
        <div class="w-[95%] mt-5 mx-auto border border-gray-300 rounded-lg shadow-xl mb-15">
            <h1 class="text-2xl font-medium mt-10 ml-10">Conversion Factors</h1>
            <p class="text-s text-gray-400 ml-10">Common unit conversions used in medication calculations</p>

            <h1 class="text-xl font-bold mt-5 ml-10">Weight Conversions</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[35%] mx-auto">From</th>
                        <th class="p-2 text-left w-[35%] mx-auto">To</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Multiplied By</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Kilograms (kg)</td>
                        <td class={tdStyle}>Pounds (lb)</td>
                        <td class={tdStyle}>2.2</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Pounds (lb)</td>
                        <td class={tdStyle}>Kilograms (kg)</td>
                        <td class={tdStyle}>0.45</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Grams (g)</td>
                        <td class={tdStyle}>Milligrams (mg)</td>
                        <td class={tdStyle}>1,000</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Milligrams (mg)</td>
                        <td class={tdStyle}>Micrograms (mcg)</td>
                        <td class={tdStyle}>1,000</td>
                    </tr>
                </tbody>
            </table>
            
            <h1 class="text-xl font-bold mt-10 ml-10">Volume Conversions</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[35%] mx-auto">From</th>
                        <th class="p-2 text-left w-[35%] mx-auto">To</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Multiplied By</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Liters (L)</td>
                        <td class={tdStyle}>Milliliters (mL)</td>
                        <td class={tdStyle}>1,000</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Milliliters (mL)</td>
                        <td class={tdStyle}>Liters (L)</td>
                        <td class={tdStyle}>0.001</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Tablespoons</td>
                        <td class={tdStyle}>Milliliters (mL)</td>
                        <td class={tdStyle}>15</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Teaspoons</td>
                        <td class={tdStyle}>Milliliters (mL)</td>
                        <td class={tdStyle}>5</td>
                    </tr>
                </tbody>
            </table>

            <h1 class="text-xl font-bold mt-10 ml-10">Temperature Conversions</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto mb-10">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[35%] mx-auto">From</th>
                        <th class="p-2 text-left w-[35%] mx-auto">To</th>
                        <th class="p-2 text-left w-[30%] mx-auto">Multiplied By</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Celsius (°C)</td>
                        <td class={tdStyle}>Fahrenheit (°F)</td>
                        <td class={tdStyle}>(°C × 9/5) + 32</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Fahrenheit (°F)</td>
                        <td class={tdStyle}>Celsius (°C)</td>
                        <td class={tdStyle}>(°F - 32) × 5/9</td>
                    </tr>
                </tbody>
            </table>
        </div>
    {:else if activeTab === 'abbr'}
        <div class="w-[95%] mt-5 mx-auto border border-gray-300 rounded-lg shadow-xl mb-15">
            <h1 class="text-2xl font-medium mt-10 ml-10">Medical Abbreviations</h1>
            <p class="text-s text-gray-400 ml-10">Common abbreviations used in medication orders and administration</p>

            <h1 class="text-xl font-bold mt-5 ml-10">Route Abbreviations</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[30%] mx-auto">Abbreviation</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Meaning</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>PO</td>
                        <td class={tdStyle}>By mouth (per os)</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>IV</td>
                        <td class={tdStyle}>Intravenous</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>IM</td>
                        <td class={tdStyle}>Intramuscular</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>SC or SQ</td>
                        <td class={tdStyle}>Subcutaneous</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>PR</td>
                        <td class={tdStyle}>Per rectum</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>SL</td>
                        <td class={tdStyle}>Sublingual</td>
                    </tr>
                </tbody>
            </table>
            
            <h1 class="text-xl font-bold mt-5 ml-10">Frequency Abbreviations</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[30%] mx-auto">Abbreviation</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Meaning</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>QD</td>
                        <td class={tdStyle}>Once daily</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>BID</td>
                        <td class={tdStyle}>Twice daily</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>TID</td>
                        <td class={tdStyle}>Three times daily</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>QID</td>
                        <td class={tdStyle}>Four times daily</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>Q4H</td>
                        <td class={tdStyle}>Every 4 hours</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>PRN</td>
                        <td class={tdStyle}>As needed</td>
                    </tr>
                </tbody>
            </table>

            <h1 class="text-xl font-bold mt-5 ml-10">Measurement Abbreviations</h1>
            <table class="w-[90%] h-2 mt-5 mx-auto">
                <thead>
                    <tr class="text-gray-500 font-light border-b-1 border-gray-200">
                        <th class="p-2 text-left w-[30%] mx-auto">Abbreviation</th>
                        <th class="p-2 text-left w-[35%] mx-auto">Meaning</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class={trStyle}>
                        <td class={tdStyle}>mg</td>
                        <td class={tdStyle}>Milligram</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>mcg or μg</td>
                        <td class={tdStyle}>Microgram</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>g</td>
                        <td class={tdStyle}>Gram</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>mL</td>
                        <td class={tdStyle}>Milliliter</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>L</td>
                        <td class={tdStyle}>Liter</td>
                    </tr>
                    <tr class={trStyle}>
                        <td class={tdStyle}>mEq</td>
                        <td class={tdStyle}>Milliequivalent</td>
                    </tr>
                </tbody>
            </table>
        </div>
    {/if}
</div>