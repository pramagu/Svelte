<script>
	import { setContext } from "svelte";
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";
	import { Router } from "svelte-routing";

	const URL = {
		juegos: "https://tiendajuegos.herokuapp.com/api/juegos/",
		clientes: "https://tiendajuegos.herokuapp.com/api/clientes/"
	};

	setContext("URL", URL);
</script>

<Router>
	<Nav />
	<Contenido />
</Router>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
	}

	:global(*) {
		margin: 0;
		padding: 0;
	}
</style>
