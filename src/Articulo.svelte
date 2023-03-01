<script>
    export let articulo = {nombre: "", precio: 0};
</script>

<input id="nombre" type="text" placeholder="Nombre" bind:value={articulo.nombre}/><br />
<input id="precio" type="number" placeholder="Precio" bind:value={articulo.precio}/>

<slot />