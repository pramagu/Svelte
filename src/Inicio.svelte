<script>
    import { Link } from "svelte-routing";
</script>
  

<div id="bloqueinicio">
<div class="col">
    <h1>Bienvenido a Tienda Juegos</h1>
</div>
<div class="contenidomain">
    <Link to="/">
      <div class="row-cols-1">
        <span class="opcion"> Inicio</span>
        <span class="descripcion">Esta es la página actual</span>
      </div>
    </Link>
  
    <Link to="/juegos">
      <div class="row-cols-1">
        <span class="opcion"> juegos</span>
        <span class="descripcion">
          Operaciones CRUD de artículos en una BD.
        </span>
      </div>
    </Link>
  
    <Link to="/clientes">
      <div class="row-cols-1">
        <span class="opcion">👥 Clientes</span>
        <span class="descripcion">
          Operaciones CRUD de clientes en una BD.
        </span>
      </div>
    </Link>
  
  </div>
<div class="row-cols-2">
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