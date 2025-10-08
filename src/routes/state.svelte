<script lang="ts">
    import Header from "./Header.svelte";

    let name = $state("Gabo");

    let status: 'OPEN' | 'CLOSED' = $state('OPEN');

    function onclick() {
        status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
    }

    let fullName = $derived(name + " " + "sex");

</script>

<Header {name} fake_name="Poncho"/>
<h2>{fullName}</h2>
<input type="text" bind:value={name} />


<p>The store is now {status}</p>
<button {onclick}>Toggle status</button>
