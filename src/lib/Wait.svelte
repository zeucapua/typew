<script lang="ts">
  import { onMount, getContext } from "svelte";
  export let duration : number;
  const add : Function = getContext("add");

  onMount(() => {
    add("wait", {duration: duration});
  });
</script>

