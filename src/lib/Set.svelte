<script lang="ts">
  import { getContext, onMount } from "svelte";
  export let speed : number;
  export let delay : number;
  const add : Function = getContext("add");

  onMount(() => {
    add("set", {speed: speed, delay: delay});
  });
</script>
