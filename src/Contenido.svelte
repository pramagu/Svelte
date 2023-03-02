<script>
    import {Route} from "svelte-routing";
    import Juegos from "./Juegos.svelte";
    import Clientes from "./Clientes.svelte";
    import Inicio from "./Inicio.svelte";
</script>


<main>
    <Route path="/" component="{Inicio}"></Route>
    <Route path="/juegos" component="{Juegos}"></Route>
    <Route path="/clientes" component="{Clientes}"></Route>
</main>