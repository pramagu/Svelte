<script>
    export let cliente = {nombre: "", apellido: ""};
</script>
<div class="px-5">
<input id="nombre" type="text" placeholder="Nombre" bind:value={cliente.nombre}/><br />
<input id="precio" type="text" placeholder="Apellido" bind:value={cliente.apellido}/>
</div>

<slot />
