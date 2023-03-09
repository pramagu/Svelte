# FRONTEND (con Svelte)
## ¿Qué es **svelte**?

En términos simples, Svelte es un compilador que genera código Javascript altamente optimizado y de reducido tamaño. Entre sus características encontramos:

- Convierte el codigo escrito por el desarrollador/a en build time
- Su escritura comprende los elementos sintácticos de JavaScript, HTML y CSS.
- Es una solución al problema de construcción de interfaces interactivas (desde el punto de vista de la experiencia de usuario)
- Es aún prematuro. Sin embargo, varias encuestas lo proyectan como una herramienta que será muy usada y aceptada

## Inicio de un proyecto de svelte

Lo primero que necesitamos es tener instalado Node.js (un runtime de Javascript que nos permite ejecutar código escrito en éste lenguaje pero por fuera del navegador) Una vez cumplido éste requisito, se procede a installar npx (un ejecutador de código) con el siguiente comando (npm viene incluido con Node.js) que debe escribirse en consola 

```console
npm i -g npx 
```

Y listo, ya podemos crear nuestro primer proyecto de Svelte. Para hacerlo, escribimos el siguiente comando en consola (posicionándonos en el directorio d preferencia) 

```console
npx degit sveltejs/template nombre-de-la-app 
```

> Nota: Como comparación frente a otros frameworks ...
>
> - **Vue**
>   - ```npx  @vue/cli  create  nombre-proyecto   # Unos 100MB aprox.```
> - **React**
>   - ```npx  create-react-app  nombre-proyecto   # Unos 200MB aprox.```
> - **Angular**
>   - ```npx  @angular/cli new  nombre-proyecto   # Unos 300MB aprox.```

A diferencia de estos, svelte solo pesa **unos pocos mb**.

## Examinar el proyecto creado

Entramos en el directorio del proyecto, ejecutando:

```console
cd   nombre-de-la-app  &&  ls 
```

Para ver todo el contenido podemos ejecutar el comando `tree`:

```
├── package.json
├── public
│   ├── favicon.png
│   ├── global.css
│   └── index.html
├── README.md
├── rollup.config.js
└── src
    ├── App.svelte
    └── main.js
```

El archivo `package.json` es el archivo de gestión de proyecto y dependencias. En él. podremos editar el nombre del autor, la versión, el tipo de licencia, etc.

La carpeta `public` contiene el frontend en forma de contenido estático, el cual deberemos subir a nuestro servidor de producción una vez finalizado el proyecto.

El archivo `README.md` puede eliminarse o podemos editarlo a nuestro gusto. No es necesario para el funcionamiento de la aplicación, aunque pudiera ser interesante para fines de documentación.

El archivo `rollup.config.js` contiene la configuración del empaquetador, que en este caso es **Rollup**. Otros frameworks utilizan otros empaquetadores como Webpack o Parcel. No debemos borrar este archivo. Tampoco lo editaremos, por ahora.

Finalmente, la carpeta `src` va a contener **nuestro código y todos los componentes web que vayamos creando**. Cada vez que realicemos un cambio en los archivos de dicha carpeta, rollup volverá a compilar y pondrá el resultado en `public/build/bundle.css` y `public/build/bundle.js`. 

El archivo `public/index.html` tiene enlaces a los anteriores. Su código es:

```html
<!DOCTYPE html>
<html lang="en">
<head>
        <meta charset='utf-8'>
        <meta name='viewport' content='width=device-width,initial-scale=1'>

        <title>Svelte app</title>

        <link rel='icon' type='image/png' href='/favicon.png'>
        <link rel='stylesheet' href='/global.css'>  
        <link rel='stylesheet' href='/build/bundle.css'> <!-- -->

        <script defer src='/build/bundle.js'></script> <!-- -->
</head>

<body>
</body>
</html>
```

**Una vez visto esta introducción inicial, vamos a describir cada uno de los componentes que uso en mi aplicación**.

## Componentes y Archivos de la aplicación.

Primero, vamos a enseñar los archivos `package.json` y `package-lock.json` para que se puedan observar las dependencias que usamos en nuestro proyecto, estas dependencias las mantengo actualizadas por medio de **Dependabot** en Github el cual puedes poner en tu propio repositorio por medio de `Settings ` y en la pestaña de Seguridad. El bot te hará pull requests con la actualización de las dependencias donde se te especificará si dicha actualización de dependencias puede romper o no la aplicación. 

**`package.json`**

```json
{
  "name": "svelte-app",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "build": "rollup -c",
    "dev": "rollup -c -w",
    "start": "sirv public --single -c"
  },
  "devDependencies": {
    "@rollup/plugin-commonjs": "^24.0.1",
    "@rollup/plugin-node-resolve": "^15.0.1",
    "rollup": "^2.3.4",
    "rollup-plugin-css-only": "^4.3.0",
    "rollup-plugin-livereload": "^2.0.0",
    "rollup-plugin-svelte": "^7.1.4",
    "rollup-plugin-terser": "^7.0.0",
    "svelte": "^3.0.0"
  },
  "dependencies": {
    "sirv-cli": "^2.0.0",
    "svelte-routing": "^1.6.0"
  }
}
```

Usamos en start la propiedad --single para indicar que funcione como **SPA**, y la propiedad -c para evitar problemas de CORS.

**`package-lock.json`**

Debido a que son dos mil lineas de código, te animo a ver el código fuente en este mismo repositorio si te da curiosidad.

Para ejecutar la aplicación deberemos ejecutar:

```console
npm  run  dev
```

La ejecución del script anterior dará error. El motivo es que no hemos instalado las dependencias que aparecen indicadas en el archivo `package.json`.

Para instalar dichas dependencias, ejecutamos:

```
npm  install
```

Dicho comando, leerá el archivo `package.json`, e instalará todas las dependencias que aparecen ahí. Ahora ya podemos volver a ejecutar `npm  run  dev`.

Podrás ver la aplicación en [localhost:5000](http://localhost:5000).



**`main.js`**

```javascript
import App from './App.svelte';

const app = new App({
	target: document.body
});

export default app;
```

Este archivo es el punto de entrada a la aplicación. Se genera un objeto `app` que se instancia a partir del componente `App.svelte`.  La propiedad `name` que hemos eliminado es la forma de pasar información desde *arriba* (`main.js`) hacia *abajo* (`App.svelte`).

El componente `App.svelte` será el componente principal de la aplicación. Todo componente en svelte se nombra con la primera letra en mayúscula y la extensión .svelte.

**`App.svelte`**

El contenido que tendrá sera el siguiente:

```html
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
```

En la sección de `script` importamos los paquetes y componentes que vayamos a usar. En este caso importamos el componente `Router` que está en el paquete `svelte-routing`. Este paquete nos proporciona los componentes necesarios para crear enrutatodores (`Router`), enlaces (`Link`) y rutas (`Route`). Necesitaremos tener instalado dicho paquete, por lo que debemos ejecutar en el terminal:

```console
npm  install  svelte-routing
```

La estructura del componente `App` está formada por un `Router`, dentro del cual se definen dos componentes: `Nav`, que tendrá los enlaces (`Link`) necesarios para la navegación, y `Contenido`, que tendrá las rutas (`Routes`) a los componentes necesarios.


## Componentes de navegación y contenido

Deben estar en la misma carpeta que el componente `App.svelte`.

**`Nav.svelte`**

```html
<script>
    import {Link} from "svelte-routing";
</script>


<nav>
	<ul>
		<li><Link to="/">Inicio</Link></li>
		<li><Link to="/juegos">Juegos</Link></li>
		<li><Link to="/clientes">Clientes</Link></li>
	</ul>
</nav>


<style>
    nav {
        background-color: brown;
        padding: 10px;
    }
    ul {
        display: flex;
        justify-content: space-around;
        list-style-type: none;
    }
</style>
```

El componente `Nav` será la barra de navegación (`nav`), con los enlaces a las rutas del lado cliente. Para los enlaces hacemos uso del componente `Link` del paquete `svelte-routing`.

**`Contenido.svelte`**

```html
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
```

El componente `Contenido` será la sección principal (`main`), con las rutas y el componente asociado a cada una de ellas. Para las rutas hacemos uso del componente `Route` del paquete `svelte-routing`.

## Componentes para el contenido

Dentro del componente anterior `Contenido` podrán renderizarse distintos componentes, dependiendo del `Link` que pulsemos en la barra de navegación. Los componentes que podrán aparecer en `Contenido` son:

- **Inicio**
- **Juegos**
- **Clientes**

**`Inicio.svelte`**

```html
script>
    import { Link } from "svelte-routing";
</script>
  

<div id="bloqueinicio">
<div class="col-12">
    <h1 class="text-center">Bienvenido a Tienda Juegos</h1>
</div>
<div class="row mt-3">
  <div class="col-md-4 text-center">
    <Link to="/">
      
        <span class="ps-3">Página de Inicio</span>
    
    </Link>
  </div>
  <div class="col-md-4 text-center">
    <Link to="/juegos">

        <span class="ps-3">Crud de Juegos</span>

    </Link>
  </div>
  <div class="col-md-4 text-center">
    <Link to="/clientes">

        <span class="ps-3">Crud de Clientes</span>

    </Link>
  </div>
  
  </div>
    <br/>
    <br/>
<div class="row mt-3">
<div class="col-md-6 text-center">El backend está en el link de la derecha =====></div>
<div class="col-md-6"><a href="https://tiendajuegos.herokuapp.com/">Tienda Juegos</a></div>
</div>
    <br/>
    <br/>
<div class="row">
    <div class="col-12 text-center">
        <a href="https://github.com/pramagu/Svelte">Enlace al repositorio Github con el código fuente</a>
    </div>
</div>
</div>

<style>
    #bloqueinicio{
        background-color: wheat;
    }
    
    a{
        text-decoration: none;
    }
</style>
```

Este componente mostrará información acerca de la aplicación. 


**`Juegos.svelte`**

 ```html
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
    $: datos = $jsonData.filter((item) =>
        RegExp(busqueda, "i").test(item.nombre)
    );
</script>
<div class="text-center">
<h1>Juegos</h1>
<Buscar bind:busqueda />
</div>

<hr />
<div class="text-center">
<Juego bind:juego>
    <Boton documento={juego} tipo="insertar" coleccion="juegos">Insertar</Boton>
</Juego>
</div>
<br />
<br />

<div class="row">
    {#each datos as juego}
        <div id="juegobox" class="col-md-3 mt-4 ms-2 pt-2 pb-2">
            <Juego bind:juego>
                <Boton tipo="modificar" documento={juego} coleccion="juegos">Modificar</Boton>
                <Boton tipo="eliminar" documento={juego} coleccion="juegos">Eliminar</Boton>
            </Juego>
        </div>
    {/each}
</div>

<style>
    #juegobox{
        
    background-color: lightgreen
        
    }
</style>
```



**`Clientes.svelte`**

![Clientes](clientes.png)

```html
<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store.js";
    import Buscar from "./Buscar.svelte";
    import Cliente from "./Cliente.svelte";
    import Boton from "./Boton.svelte";
    const URL = getContext("URL");
    let busqueda = "";
    let cliente = {};
    onMount(async () => {
        const response = await fetch(URL.clientes);
        const data = await response.json();
        $jsonData = data;
    });
    $: regex = new RegExp(busqueda, "i");
    $: datos = busqueda
        ? $jsonData.filter((item) => regex.test(item.nombre))
        : $jsonData;
</script>

<div class="text-center">
<h1>Clientes</h1>
<Buscar bind:busqueda />
</div>

<hr />
<div class="text-center">
<Cliente bind:cliente>
    <Boton documento={cliente} tipo="insertar" coleccion="clientes">Insertar</Boton>
</Cliente>
</div>
<br />

<div class="row">
    {#each datos as cliente}
        <div id="clientebox" class="col-md-3 mt-4 ms-2 pt-2 pb-2">
            <Cliente {cliente}>
                <Boton tipo="modificar" documento={cliente} coleccion="clientes" > Modificar </Boton>
                <Boton tipo="eliminar" documento={cliente} coleccion="clientes" > Eliminar </Boton>
            </Cliente>
        </div>
    {/each}
</div>

<style>
    #clientebox{
        
    background-color: aquamarine
        
    }
</style>
```



## Otros componentes

**`Juego.svelte`**

```html
<script>
    export let juego = {nombre: "", precio: 0};
</script>

<div class="px-5">
<input id="nombre" type="text" placeholder="Nombre" bind:value={juego.nombre}/><br />
<input id="precio" type="number" placeholder="Precio" bind:value={juego.precio}/>
</div>

<slot />
```



**`Cliente.svelte`**

```html
<script>
    export let cliente = {nombre: "", apellido: ""};
</script>
<div class="px-5">
<input id="nombre" type="text" placeholder="Nombre" bind:value={cliente.nombre}/><br />
<input id="precio" type="text" placeholder="Apellido" bind:value={cliente.apellido}/>
</div>

<slot />
```

**`Boton.svelte`**


```html
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
```

**`Buscar.svelte`**

```html
<script>
    export let busqueda = "";
</script>

<input type="search" bind:value={busqueda} />

```


## Construir la aplicación para el entorno de producción

Para crear una versión optimizada de la aplicación, ejecutamos:

```bash
npm run build
```

Puedes ejecutar la aplicación recién creada con `npm run start`. Esto utiliza [sirv](https://github.com/lukeed/sirv), que se incluye en las `dependencias` de `package.json` para que la aplicación funcione cuando se implemente en plataformas como [Heroku](https://heroku.com).


## Single-Page App

**Esta es una aplicación de página única (SPA)**.

Por defecto, sirv solo responderá a las solicitudes que coincidan con los archivos en `public`. Esto es para maximizar la compatibilidad con los servidores de archivos estáticos, lo que le permite implementar su aplicación en cualquier lugar.

Si estás creando una aplicación de una sola página (SPA) con varias rutas, sirv debe poder responder a las solicitudes de *cualquier* ruta. Puedes hacerlo editando el comando `"start"` en package.json:

`--single` sirve para que la aplicación se ejecute como **SPA** mientras que `-c` sirve para evitar problemas con el **CORS**


```js
"start": "sirv public --single -c"
```

> NOTA: sirv es el módulo de node que permite ejecutar un servidor web y mostrar nuestra app.


## Despliegue en la web

Este frontend no contiene código de servidor, es decir, no contiene código para backend. Por tanto podemos desplegarlo como hariamos con cualquier página html. Cualquier sitio que permita **contenido estático** nos vale. 

Existen muchos sitios que ofrecen esta opción, Por ejemplo:

- GitHub Pages
- Netlify
- Vercel
- Surge

Para desarrolladores con poca experiencia, la forma más sencilla de despliegue es utilizar la interfaz web que proporcionan dichos sitios. 

Pero si deseas realizar el despliegue mediante interfaz de texto, a continuación se muestra un resumen de cómo se realizaría con Vercel, no he incluido los demás puesto que yo solo he realizado el despliegue con Vercel y no con los otros dos. 

**Con [vercel](https://vercel.com)**

Instala `vercel` si aún no lo has hecho:

```bash
sudo  npm install -g vercel
```

Luego, desde la carpeta de tu proyecto:

```bash
vercel login
vercel --prod
```

> NOTA: Sigue el asistente que aparece. 

La otra manera de hacerlo es por interfaz gráfica dentro de la misma página de Vercel, donde puedes conectar tu repositorio Github y añadir Vercel al mismo repositorio. Vercel se encargará de desplegar la aplicación cada vez que exista un cambio en el repositorio y te mandará un email con el resultado del despliegue.



