<script lang="ts">
	import { goto } from "$app/navigation"

	function gotoAbout() {
		goto('/about');
	}
</script>

<nav class='flex justify-center w-full'>
	<a class='mx-4 text-lg' href='/'>Home</a>
	<button class='mx-4 text-lg' on:click={gotoAbout}>About</button>
</nav>
