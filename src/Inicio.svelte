<script>
    import { Link } from "svelte-routing";
</script>
  

<div id="bloqueinicio">
<div class="col">
    <h1>Bienvenido a Tienda Juegos</h1>
</div>
<div class="row mt-3">
  <div class="col-md-4 text-decoration-none">
    <Link to="/">
      
        <span class="opcion"> Inicio</span>
        <span class="descripcion">Esta es la página actual</span>
    
    </Link>
  </div>
  <div class="col-md-4 text-decoration-none">
    <Link to="/juegos">

        <span class="opcion"> juegos</span>
        <span class="descripcion">
          Operaciones CRUD de juegos en una BD.
        </span>

    </Link>
  </div>
  <div class="col-md-4 text-decoration-none">
    <Link to="/clientes">

        <span class="opcion">Clientes</span>
        <span class="descripcion">
          Operaciones CRUD de clientes en una BD.
        </span>

    </Link>
  </div>
  
  </div>
<div class="row mt-3">
<div class="col-md-6 text-center">El backend está en el link de la derecha</div>
<div class="col-md-6 text-center"><a href="https://tiendajuegos.herokuapp.com/">Tienda Juegos</a></div>
</div>
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
</style>
