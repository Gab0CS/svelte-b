<script lang="ts">
    import type { Snippet } from "svelte";
    import { createState, GaboState } from "./sate.svelte";
    let { 
        name, 
    }: {
        name: string
    } = $props();

    const myState = createState();
    const myState2 = new GaboState();

</script>

<div>
   <h1>
        {name ? name : 'User'}'s form
   </h1>
   <button onclick={myState.up}>{myState.value}</button>
   <button onclick={() => myState2.up()}>{myState2.value}</button>
</div>


<style>

</style>