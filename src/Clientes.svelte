<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store.js";
    import Buscar from "./Buscar.svelte";
    import Cliente from "./Cliente.svelte";
    import Boton from "./Boton.svelte";

    const URL = getContext("URL");
    let busqueda = "";
    let cliente = {};

    onMount(async () => {
        const response = await fetch(URL.clientes);
        const data = await response.json();
        $jsonData = data;
    });
    $: regex = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regex.test(item.nombre))
        : $jsonData;
</script>

<div class="text-center">
<h1>Clientes</h1>
<Buscar bind:busqueda />
</div>

<hr />
<div class="text-center">
<Cliente bind:cliente>
    <Boton documento={cliente} tipo="insertar" coleccion="clientes">Insertar</Boton>
</Cliente>
</div>
<br />

<div class="row">
    {#each datos as cliente}
        <div id="clientebox" class="col-md-3 mt-4 ms-2 pt-2 pb-2">
            <Cliente {cliente}>
                <Boton tipo="modificar" documento={cliente} coleccion="clientes" > Modificar </Boton>
                <Boton tipo="eliminar" documento={cliente} coleccion="clientes" > Eliminar </Boton>
            </Cliente>
        </div>
    {/each}
</div>

<style>
    #clientebox{
        
    background-color: aquamarine
        
    }
</style>

