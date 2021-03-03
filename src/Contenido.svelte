<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Mercancias  from "./Mercancias.svelte";
  import Proveedores   from "./Proveedores.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/mercancias" component={Mercancias} />
  <Route path="/proveedores" component={Proveedores} />
</main>