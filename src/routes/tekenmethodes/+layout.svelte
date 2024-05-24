<script>
	import { setContext } from 'svelte'
	import { writable } from 'svelte/store'

	export let data

	const methodsPage = writable()
	$: methodsPage.set(data)

	setContext('methodsPage', methodsPage)
</script>

<slot />