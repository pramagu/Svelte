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
  $: datos = $jsonData.filter ( item => RegExp(busqueda, "i").test(item.nombre)) 

</script>

<h1>Juegos</h1>
<Buscar bind:busqueda />

<hr />

<Juego bind:juego>
    <Boton documento={juego} tipo="insertar" coleccion="juegos" />
</Juego>
<br />

{#each datos as juego}
    <br />
    <Juego bind:juego={juego}>
        <Boton tipo="modificar" documento={juego} coleccion="juegos" />
        <Boton tipo="eliminar" documento={juego} coleccion="juegos" />
    </Juego>
    <br />
    <br />
{/each}
