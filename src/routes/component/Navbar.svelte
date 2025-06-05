<script lang="js">
    import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
    import { faHome, faCalculator, faBook, faExclamationCircle } from '@fortawesome/free-solid-svg-icons';
    const navButton = "px-5 py-3 mx-2 rounded-md hover:bg-sky-500 transition-colors duration-300 border-b-3 border-white";
</script>

<div class="w-full py-5 flex flex-row items-center bg-gradient-to-r from-sky-600 to-sky-700">
    <h1 class="text-white text-3xl font-bold ml-10 text">Nursing Calc</h1>
    <ul class="flex flex-row ml-auto mr-10 text-white text-lg space-between-x-4">
        <li><a href="/" class={navButton}><FontAwesomeIcon icon="home" class="inline mr-2" />Home</a></li>
        <li><a href="/calculators" class={navButton}><FontAwesomeIcon icon="calculator" class="inline mr-2" />Calculators</a></li>
        <li><a href="/references" class={navButton}><FontAwesomeIcon icon="book" class="inline mr-2" />References</a></li>
        <li><a href="/about" class={navButton}><FontAwesomeIcon icon="exclamation-circle" class="inline mr-2" />About</a></li>
    </ul>
</div>