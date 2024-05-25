<script>
  import Breadcrumb from "$lib/atoms/breadcrumb.svelte"
  import Introduction from "$lib/molecules/introduction.svelte"
  import Filter from "$lib/molecules/filter.svelte"
  import Methods from "$lib/organisms/methods.svelte"

  import { getContext } from "svelte"

  const methodsPage = getContext('methodsPage')

  const {page, methods, categories} = $methodsPage
</script>

<Breadcrumb titel="Tekenmethodes" bgc="var(--vtYellow)" />
<Introduction {page}/>

<Filter {categories} />
<Methods {methods} /> 
