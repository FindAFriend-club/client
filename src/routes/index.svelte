<script lang="ts">
  import { flip } from "svelte/animate";
  import { fade } from "svelte/transition";
  import { circOut } from "svelte/easing";

  import FlipBox from "../components/FlipBox.svelte";
  import LoginForm from "../components/LoginForm.svelte";
  import Questions from "../components/Questions.svelte";
  import SignUpForm from "../components/SignUpForm.svelte";

  import { isFormFlipped, isFullscreen } from "../stores";

  let formHeight: number;

  function resizeCenter(node, { duration = 500 }) {
    let height = +getComputedStyle(node)["height"].match(/(\d+)px/)[1];

    return {
      delay: 0,
      duration,
      css: (t) => {
        return `
          height: ${formHeight}px;
          margin: calc(${circOut(t) * ((height - formHeight) / 2)}px) 0;
          transform: translateY(-${(height - formHeight) / 2}px);
          opacity: ${t};
        `;
      },
    };
  }
</script>

<style lang="sass">
  \:global(html)
    height: 100%

  \:global(body)
    display: flex
    height: 100%
    background: none
    align-items: center
    justify-content: center

  main
    position: relative
    height: 100%
    padding: 5rem 0.5rem 0
    justify-content: space-between

    &::before
      content: ""
      position: fixed
      width: 100vw
      height: 100vh
      background: $primary
      background: linear-gradient(lighten($primary, 10%), $primary)
      top: 0
      left: calc(100% + 5rem)
      transform: skew(-25deg)
      transform-origin: top left
      transition: all 1s
    
    &.fullscreen
      &::before
        width: 500vw
        left: 0
      
      .form-outer
        transform: translateY(-10rem)

    .info
      position: absolute
      left: 0
      right: 0
      z-index: -1

      h1.headline
        font-size: 2.5rem
        font-weight: bolder
        text-align: center

    .form-outer
      margin-top: 10rem
      width: 100%
      max-width: 30rem
      flex: 1 1 0
      transition: transform 1s

      .form
        display: grid
        width: 100%
        padding: 1rem 1.5rem
        background: #fff
        border-radius: 1rem
        box-shadow: rgba(0, 0, 0, 0.125) 0 0 0.5rem
        align-items: center
        overflow: hidden
        
        div
          grid-column: 1
          grid-row: 1

  @media (min-width: 768px)
    main
      display: flex
      padding: 0 2rem 0
      justify-content: flex-end
      align-items: center

      &::before
        left: calc(50% + 20rem)

      &.fullscreen
        .form-outer
          position: absolute
          margin: 0
          left: 50%
          transform: translateX(-50%)

      .info
        max-width: 50%
        top: 20rem
        right: unset
        transform: translateY(-50%)

        h1.headline
          text-align: left

      .form-outer
        margin: 0 0 0 2rem
        transition: transform 1s
</style>

<svelte:head>
  <title>Find A Friend</title>
</svelte:head>

<main class="container" class:fullscreen={$isFullscreen}>
  <section class="info">
    <h1 class="headline">Find new friends who share your interests</h1>
  </section>
  
  {#each [0] as form (form)}
    <section class="form-outer" animate:flip>
      <FlipBox bind:isFlipped={$isFormFlipped}>
        <div class="form" slot="front">
          <LoginForm />
        </div>
        <div class="form" slot="back">
          {#if !$isFullscreen}
            <div
              class="signup"
              bind:offsetHeight={formHeight}
              out:fade={{ duration: 500 }}>
              <SignUpForm />
            </div>
          {:else}
            <div class="questions" in:resizeCenter>
              <Questions />
            </div>
          {/if}
        </div>
      </FlipBox>
    </section>
  {/each}
</main>
