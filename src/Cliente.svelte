<script>
    export let cliente = {nombre: "", apellido: ""};
</script>

<input id="nombre" type="text" placeholder="Nombre" bind:value={cliente.nombre}/><br />
<input id="precio" type="text" placeholder="Apellido" bind:value={cliente.apellido}/>

<slot />