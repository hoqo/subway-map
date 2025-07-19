<script>
    import Map from '$lib/components/Map/Map.svelte';
    import Legend from '$lib/components/Legend/Legend.svelte';
</script>

<div class="app-container">
    <header>
        <h1>Kyiv Rapid Transit Map</h1>
    </header>

    <main>
        <Map />
    </main>

    <footer>
        <Legend />
    </footer>
</div>

<style>
    .app-container {
        display: grid;
        /*make the header with auto height*/
        grid-template-rows: 82px 747px calc(100vh - 82px - 747px);
        place-content: stretch;
    }

    header {
        text-align: center;
    }
</style>
