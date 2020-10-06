<script lang="ts">
  import Nav from "../components/Nav.svelte";

  export let segment: string;
</script>

<svelte:head>
  <style lang="sass">
    @import '../styles/global'
  </style>
</svelte:head>

{#if segment}
  <Nav {segment} />
{/if}
<slot />
