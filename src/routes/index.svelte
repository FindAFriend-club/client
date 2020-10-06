<script>
  import FlipBox from "../components/FlipBox.svelte";
  import LoginForm from "../components/LoginForm.svelte";
  import SignUpForm from "../components/SignUpForm.svelte";

  import { isFormFlipped } from "../stores";
</script>

<style lang="sass">
  \:global(html)
    height: 100%
    background: #fff

    &::before
      content: ""
      position: fixed
      left: calc(100% + 5rem)
      width: 100vw
      height: 100vh
      background: $primary
      background: linear-gradient(lighten($primary, 10%), $primary)
      transform: skew(-25deg)
      transform-origin: top left
      z-index: -1

  \:global(body)
    display: flex
    height: 100%
    background: none
    align-items: center
    justify-content: center

  main
    padding: 0 2rem
    margin-top: 3rem
    justify-content: space-between

    .info
      h1.headline
        font-size: 2.5rem
        font-weight: bolder
        text-align: center

    .form-outer
      width: 100%
      max-width: 30rem
      flex: 1 1 0

      .form
        padding: 1rem 1.5rem
        background: #fff
        border-radius: 1rem
        box-shadow: rgba(0, 0, 0, 0.125) 0 0 0.5rem

  @media (min-width: 768px)
    \:global(html)
      &::before
        left: calc(50% + 20rem)

    main
      display: flex
      margin-top: 5rem

      .info
        max-width: 50%

        h1.headline
          text-align: left

      .form-outer
        margin: 0 0 0 2rem
</style>

<svelte:head>
  <title>Find A Friend</title>
</svelte:head>

<main class="container">
  <section class="info">
    <h1 class="headline">Find new friends who share your interests</h1>
  </section>

  <section class="form-outer">
    <FlipBox bind:isFlipped={$isFormFlipped}>
      <div class="form" slot="front">
        <LoginForm />
      </div>
      <div class="form" slot="back">
        <SignUpForm />
      </div>
    </FlipBox>
  </section>
</main>
