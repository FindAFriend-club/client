<script lang="ts">
  import { isFormFlipped, isFullscreen } from "../stores";
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

<form
  on:submit|preventDefault={() => {
    $isFullscreen = true;
  }}>
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
    autocomplete="new-password"
    required />
  <input
    type="password"
    name="confirmPassword"
    id="password"
    placeholder="Confirm the password"
    autocomplete="new-password"
    required />
  <button type="submit" name="signup">Create an account</button>
  <p>
    Already have an account?
    <strong><a
        href="/"
        on:click|preventDefault={() => ($isFormFlipped = false)}>Log in</a></strong>
  </p>
</form>
