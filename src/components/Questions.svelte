<script lang="ts">
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
  on:submit|preventDefault={(e) => {
    console.log(e);
  }}>
  <textarea type="text" name="bio" id="bio" placeholder="Bio" required />
  <textarea
    type="text"
    name="bestPart"
    id="best-part"
    placeholder="What is the best part of the day?"
    required />
  <input
    type="text"
    name="contactInfo"
    id="contact-info"
    placeholder="What is your contact info?"
    required />
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
</form>
