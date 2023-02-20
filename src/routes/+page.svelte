<script>
  import {
    Typewriter,
    Text,
    Set,
    Wait
  } from "$lib";
</script>

<main>

<Typewriter autoplay loop>
  <Text content="Hello" />
  <Wait duration={1000} />
  <Text content="World" />
</Typewriter>

</main>

<style>
  main {
    font-family: monospace;
  }
</style>
