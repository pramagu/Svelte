<script>
    import { Link } from "svelte-routing";
</script>
  

<div id="bloqueinicio">
<div class="col">
    <h1>Bienvenido a Tienda Juegos</h1>
</div>
<div class="row-cols-3">
    <Link to="/">
      <div class="col">
        <span class="opcion"> Inicio</span>
        <span class="descripcion">Esta es la página actual</span>
      </div>
    </Link>
  
    <Link to="/juegos">
      <div class="col">
        <span class="opcion"> juegos</span>
        <span class="descripcion">
          Operaciones CRUD de juegos en una BD.
        </span>
      </div>
    </Link>
  
    <Link to="/clientes">
      <div class="col">
        <span class="opcion">Clientes</span>
        <span class="descripcion">
          Operaciones CRUD de clientes en una BD.
        </span>
      </div>
    </Link>
  
  </div>
<div class="row-cols-2">
<div class="col">El backend está en el link de la derecha</div>
<div class="col"><a href="https://tiendajuegos.herokuapp.com/">Tienda Juegos</a></div>
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