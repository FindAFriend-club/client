<script context="module" lang="ts">
  export async function preload({ params }) {
    // the `slug` parameter is available because
    // this file is called [slug].svelte
    const res = await this.fetch(`blog/${params.slug}.json`);
    const data = await res.json();

    if (res.status === 200) {
      return { post: data };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script lang="ts">
  export let post: { slug: string; title: string; html: any };
</script>

<style lang="sass">
	.content 
		\:global(h2)
			font-size: 1.4em
			font-weight: 500

		\:global(pre)
			background-color: #f9f9f9
			box-shadow: inset 1px 1px 5px rgba(0, 0, 0, 0.05)
			padding: 0.5em
			border-radius: 2px
			overflow-x: auto

		\:global(code)
			background-color: transparent
			padding: 0

		\:global(ul)
			line-height: 1.5

			\:global(li)
				margin: 0 0 0.5em 0
</style>

<svelte:head>
  <title>{post.title}</title>
</svelte:head>

<h1>{post.title}</h1>

<div class="content">
  {@html post.html}
</div>
