<script lang="ts">
  import { isFormFlipped } from "../stores";
</script>

<style lang="sass">
  form button 
    display: block
    color: #fff
    background: $primary
    border: 0
    margin: 1rem 0
    padding: 1rem 1.5rem
    font-size: 17px
    border-radius: 2rem
    width: 100%
</style>

<form action="/login" method="post">
  <input
    type="email"
    name="email"
    id="email"
    placeholder="Email"
    autocomplete="username"
    required />
  <input
    type="password"
    name="password"
    id="password"
    placeholder="Password"
    autocomplete="current-password"
    required />
  <button name="login">Log In</button>
  <a href="/recover">Forgot your password?</a>
  <p>
    Don't have an account yet?
    <strong><a
        href="/register"
        on:click|preventDefault={() => ($isFormFlipped = true)}>Sign up</a></strong>
  </p>
</form>
