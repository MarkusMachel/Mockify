<script>
	import '../app.pcss';
	import { DarkMode } from 'flowbite-svelte';
</script>

<div class="md:container md:mx-auto">
	<DarkMode />
	<slot />
</div>

