<script>
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
