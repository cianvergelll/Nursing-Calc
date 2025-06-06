<script>
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import Navbar from '../../component/Navbar.svelte';

	let submitted = $state(false);
</script>

<Navbar />

<div class="mx-auto flex w-[50%] flex-col">
	<p class="mt-8 ml-5 text-3xl font-bold">Dilution Calculator</p>
	<div class="my-5 w-full rounded-xl border border-gray-300 py-4 shadow-lg">
		<p class="mx-5 text-lg font-medium">Important</p>
		<p class="mx-5">
			This calculator is for educational purposes. Always verify calculations and follow your
			institution's protocols.
		</p>
	</div>
</div>
