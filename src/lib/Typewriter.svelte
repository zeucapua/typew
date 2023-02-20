<script lang="ts">
  import { onMount, setContext } from "svelte";
  import { writable } from "svelte/store";

  // typewriter props
  export let loop : boolean = false;
  export let autoplay : boolean = false;
  export let playing : boolean = false;
  export let speed : number = 10;

  // current text value
  let current_text = "";

  // all children inside the slot
  const contents = writable<Map<string, object>[]>([]);
  let addContent = (type : string, values : object) => { 
    contents.update( c => [...c, new Map([[type, values]])] );
  }
  
  // let child pass values to this parent
  setContext("add", addContent);

  onMount(() => {
    if (autoplay) play();
  });

  async function play() {
    for (const content of $contents) {
      const entry = content.entries().next().value;
      const type = entry[0];
      const values = entry[1];
      switch (type) {
        case "text": await display(values.content); break;
        case "wait": await sleep(values.duration); break;
      }
    }
    if (loop) play();
  }

  // utils 
  async function display(value : string) {
    current_text = "";
    for (let i = 0; i < value.length; i++) {
      const char = value[i];
      current_text += char;
      await sleep(speed * 10);
    }
  }
  const sleep = (ms : number) => new Promise(resolve => setTimeout(resolve, ms));

  $: if (playing) play();
</script>

<p>{current_text}</p>
<slot />
