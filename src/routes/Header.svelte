<script lang="ts">

    let { 
        name, 
        fake_name = null
    }: {
        name: string
        fake_name? : string | null
    } = $props();

</script>

<h1>Hello {name}</h1>
<h2>{fake_name}</h2>

<style>


</style>