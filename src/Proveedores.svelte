<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";
  import Buscar                  from "./Buscar.svelte";
  import Proveedor               from "./Proveedor.svelte";
  import Boton                   from "./Boton.svelte";
  const URL = getContext("URL");
  let busqueda = "";
  let proveedor = {};
  onMount(async () => {
    const response = await fetch(URL.proveedores);
    const data = await response.json();
    $jsonData = data;
  });
  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;
</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>PROVEEDORES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Proveedor bind:proveedor>
    <div style="text-align: right">
      <Boton documento={proveedor} tipo="insertar" coleccion="proveedores" />
    </div>
  </Proveedor>
</div>

<div class="container">
  {#each datos as proveedor}
    <Proveedor {proveedor}>
      <div style="text-align: right">
        <Boton documento={proveedor} tipo="modificar" coleccion="proveedores" />
        <Boton documento={proveedor} tipo="eliminar" coleccion="proveedores" />
      </div>
    </Proveedor>
  {/each}
</div>