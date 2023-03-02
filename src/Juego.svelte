<script>
    export let juego = {nombre: "", precio: 0};
</script>

<input id="nombre" type="text" placeholder="Nombre" bind:value={juego.nombre}/><br />
<input id="precio" type="number" placeholder="Precio" bind:value={juego.precio}/>

<slot />