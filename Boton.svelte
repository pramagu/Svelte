<script>
    import { onMount } from "svelte";
    import { jsonData } from "./store.js";
    import { getContext } from "svelte";
    export let tipo = "insertar";
    export let coleccion = "juegos";
    export let documento = {};

    let handler = () => {};
    let clases = "";
    let url = "";
    const URL = getContext("URL");

    onMount(() => {
        switch (tipo) {
            case "insertar":
                handler = insertar;
                clases = "btn btn-insertar bg-secondary";
                break;
            case "modificar":
                handler = modificar;
                clases = "btn btn-modificar bg-secondary";
                break;
            case "eliminar":
                handler = eliminar;
                clases = "btn btn-eliminar bg-secondary";
                break;
            default:
        }
        switch (coleccion) {
            case "juegos":
                url = URL.juegos;
                break;
            case "clientes":
                url = URL.clientes;
                break;
            default:
        }
    });
    function insertar() {
        if (
            Object.keys(documento).length > 1 &&
            Object.values(documento).every((x) => x !== undefined && x != "")
        ) {
            let opciones = {
                method: "POST",
                headers: { "Content-Type": "application/json", "Access-Control-Allow-Origin" : "*" },
                body: JSON.stringify(documento),
            };
            fetch(url, opciones)
                .then((res) => res.json())
                .then((data) => {
                    $jsonData = [...$jsonData, data];
                    console.log("Todo Correcto");
                })
                .catch((err) => console.log("Fallo en insertar"));
        }
    }
    function modificar() {
        let opciones = {
            method: "PUT",
            headers: { "Content-Type": "application/json", "Access-Control-Allow-Origin" : "*"  },
            body: JSON.stringify(documento),
        };
        fetch(url + documento._id, opciones)
            .then((res) => res.json())
            .then((data) => console.log("Todo Correcto"))
            .catch((err) => console.log("Fallo en modificar"));
    }
    function eliminar() {
        let opciones = { method: "DELETE" };
        fetch(url + documento._id, opciones)
            .then((res) => res.json())
            .then((data) => {
                $jsonData = $jsonData.filter((x) => x._id !== data._id);
                console.log("Todo Correcto");
            })
            .catch((err) => console.log("Fallo en eliminar"));
    }
</script>

<button class="{clases}" on:click={handler}>{tipo}</button>
