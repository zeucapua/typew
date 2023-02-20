<script lang="ts">
  import { getContext, onMount } from "svelte";
  export let content : string;
  const add : Function = getContext("add");

  onMount(() => {
    add("text", {content: content});
  });

</script>


