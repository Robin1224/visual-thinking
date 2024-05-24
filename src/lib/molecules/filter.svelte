<script>
  import { page } from "$app/stores"
  import { goto } from "$app/navigation"

  export let categories
  let form
  let filter = $page.url.searchParams.getAll("categorie") || []

  function applyFilter(event) {
      event.preventDefault()
      const form = event.target
      const url = new URL(form.action)

      const formData = new FormData(form)
      const categorie = formData.getAll("categorie")

      url.searchParams.delete("categorie")
      categorie.forEach((slug) => url.searchParams.append("categorie", slug))

      console.log('CLIENT',url)

      goto('/').then(() => goto(url, { replaceState: true, keepFocus: true, noScroll: true }))
  }

</script>

<section>
  <h2 id="methodes">Filter op categorie</h2>

  <form method="GET" action="/tekenmethodes#methodes" bind:this={form} on:submit|preventDefault={applyFilter}>
    {#each categories as category}
      <label for={category.slug}>
        <input
          type="checkbox"
          id={category.slug}
          value={category.slug}
          checked={filter.includes(category.slug)}  
          name="categorie"
          tabindex="0"
        />
        {category.title}
      </label>
    {/each}
    <button type="submit">
      Pas filters toe
    </button>
  </form>
</section>

<style>
  h2 {
    font-size: 1em;
  }

#methodes {
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

section form {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

 label {
  display: flex;
  align-items: center;
  margin: 5px 0;
}

section input[type="checkbox"] {
  margin-right: 8px;
}

section button {
  background-color: var(--vtYellow);
  color: black;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
}

section button:hover {
  background-color: var(--vtYellow-80);
}

</style>

<!-- https://github.com/sveltejs/kit/discussions/8499 -->
<!-- https://github.com/sveltejs/kit/issues/7895 -->
<!-- +page.js: export const csr = false -->