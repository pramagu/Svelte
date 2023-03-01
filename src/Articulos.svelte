<script>
    import { getContext } from "svelte";
    import { data } from "./store.js";
    import { onMount } from "svelte";
    import Buscar from "./Buscar.svelte";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";

    let articuloInsertar = {};

    let datosFiltrados = [];
    let patron = "";

    const URL = getContext("URL");

    let getArticulos = async () => {
        const response = await fetch(URL.articulos);
        $data = await response.json();
    };

    onMount(getArticulos);

    $: datosFiltrados = $data.filter((articulo) =>
        RegExp(patron, "i").test(articulo.nombre)
    );
</script>

<Buscar bind:busqueda={patron} />

<hr />

<Articulo bind:articulo={articuloInsertar}>
    <Boton documento={articuloInsertar} />
</Articulo>
<br />

{#each datosFiltrados as articulo}
    <br />
    <Articulo bind:articulo={articulo}>
        <Boton tipo="modificar" documento={articulo} />
        <Boton tipo="eliminar" documento={articulo} />
    </Articulo>
    <br />
    <br />
{/each}
