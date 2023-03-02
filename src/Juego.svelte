<script>
    export let juego = {nombre: "", precio: 0};
</script>

<div class="px-5">
<input id="nombre" type="text" placeholder="Nombre" bind:value={juego.nombre}/><br />
<input id="precio" type="number" placeholder="Precio" bind:value={juego.precio}/>
</div>

<slot />
