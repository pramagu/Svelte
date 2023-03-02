<script>
    import { Link } from "svelte-routing";
</script>
  

<div id="bloqueinicio">
<div class="col">
    <h1>Bienvenido a Tienda Juegos</h1>
</div>
<div class="row-cols-3 mx-3">
  <div class="col-md-4">
    <Link to="/">
      
        <span class="opcion"> Inicio</span>
        <span class="descripcion">Esta es la página actual</span>
    
    </Link>
  </div>
  <div class="col-md-4">
    <Link to="/juegos">

        <span class="opcion"> juegos</span>
        <span class="descripcion">
          Operaciones CRUD de juegos en una BD.
        </span>

    </Link>
  </div>
  <div class="col-md-4">
    <Link to="/clientes">

        <span class="opcion">Clientes</span>
        <span class="descripcion">
          Operaciones CRUD de clientes en una BD.
        </span>

    </Link>
  </div>
  
  </div>
<div class="row-cols-2 mx-3">
<div class="col-md-6">El backend está en el link de la derecha</div>
<div class="col-md-6"><a href="https://tiendajuegos.herokuapp.com/">Tienda Juegos</a></div>
</div>
<div class="row-cols-1">
    <div class="col">
        <a href="https://github.com/pramagu/Svelte">Enlace al repositorio Github con el código fuente</a>
    </div>
</div>
</div>

<style>
    #bloqueinicio{
        background-color: wheat;
    }
</style>