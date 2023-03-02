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

<h1>Clientes</h1>
<Buscar bind:busqueda />

<hr />

<Cliente bind:cliente>
    <Boton documento={cliente} tipo="insertar" coleccion="clientes" >Insertar</Boton>
</Cliente>
<br />

<div class="row-cols-3">
    {#each datos as cliente}
        <div class="col-md-4 mx-2">
            <Cliente {cliente}>
                <Boton tipo="modificar" documento={cliente} coleccion="clientes" > Modificar </Boton>
                <Boton tipo="eliminar" documento={cliente} coleccion="clientes" > Eliminar </Boton>
            </Cliente>
        </div>
    {/each}
</div>

