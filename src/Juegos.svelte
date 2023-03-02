<script>
    import { getContext } from "svelte";
    import { jsonData } from "./store.js";
    import { onMount } from "svelte";
    import Buscar from "./Buscar.svelte";
    import Juego from "./Juego.svelte";
    import Boton from "./Boton.svelte";

    let busqueda = "";
    let juego = {};
    const URL = getContext("URL");

    onMount(async () => {
        const response = await fetch(URL.juegos);
        const data = await response.json();
        $jsonData = data;
    });
    $: datos = $jsonData.filter((item) =>
        RegExp(busqueda, "i").test(item.nombre)
    );
</script>

<h1>Juegos</h1>
<Buscar bind:busqueda />

<hr />

<Juego bind:juego>
    <Boton documento={juego} tipo="insertar" coleccion="juegos">Insertar</Boton>
</Juego>
<br />
<br />

<div class="row">
    {#each datos as juego}
        <div id="juegobox" class="col-md-3 mt-4 ms-2">
            <Juego bind:juego>
                <Boton tipo="modificar" documento={juego} coleccion="juegos">Modificar</Boton>
                <Boton tipo="eliminar" documento={juego} coleccion="juegos">Eliminar</Boton>
            </Juego>
        </div>
    {/each}
</div>

<style>
    #juegobox{
        
    background-color: lightgreen
        
    }
</style>
