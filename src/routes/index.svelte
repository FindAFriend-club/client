<style lang="sass">
  \:global(html)
    height: 100vh
    background: #fff
  
    &::before 
      content: ""
      position: fixed
      left: calc(50% - 0.25 * 850px)
      width: 100vw
      height: 2000px
      background: hsl(220, 100%, 60%)
      background: linear-gradient(hsl(220, 100%, 70%), #05f)
      transform: skew(-25deg)
      transform-origin: left
      z-index: -1

  \:global(body)
    background: none

  main
    padding: 0 2rem
    margin-top: 5rem
    justify-content: space-between

    .info
      h1.headline
        font-size: 2.5rem
        font-weight: bolder
        text-align: center

    .login
      width: 100%
      max-width: 30rem
      padding: 1rem 1.5rem
      background: #fff
      border-radius: 1rem
      box-shadow: rgba(0, 0, 0, 0.125) 0 0 0.5rem
      flex: 1 1 0

      form button 
        display: block
        color: #fff
        background: hsl(220, 100%, 55%)
        border: 0
        margin: 1rem 0
        padding: 1rem 1.5rem
        font-size: 17px
        border-radius: 2rem
        width: 100%

  @media (min-width: 768px)
    main 
      display: flex

      .info 
        max-width: 50%
      
        h1.headline 
          text-align: left
      
      .login 
        margin: 0 0 0 2rem
</style>

<svelte:head>
  <title>Find A Friend</title>
</svelte:head>

<main class="container">
  <section class="info">
    <h1 class="headline">Find new friends who share your interests</h1>
  </section>

  <section class="login">
    <form action="/login" method="post">
      <input type="text" name="email" id="email" placeholder="Email" />
      <input
        type="password"
        name="password"
        id="password"
        placeholder="Password" />
      <button name="login">Log In</button>
      <a href="/recover">Forgot your password?</a>
      <p>
        Don't have an account yet?
        <strong><a href="/register">Sign up</a></strong>
      </p>
    </form>
  </section>
</main>
