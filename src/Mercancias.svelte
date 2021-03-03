<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";
  import Buscar                  from "./Buscar.svelte";
  import Mercancia               from "./Mercancia.svelte";
  import Boton                   from "./Boton.svelte";
  const URL = getContext("URL");
  let busqueda = "";
  let mercancia = {};
  onMount(async () => {
    const response = await fetch(URL.mercancias);
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

<h1>MERCANCÍAS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Mercancia bind:mercancia>
    <div style="text-align: right">
      <Boton documento={mercancia} tipo="insertar" coleccion="mercancias" />
    </div>
  </Mercancia>
</div>

<div class="container">
  {#each datos as mercancia}
    <Mercancia {mercancia}>
      <div style="text-align: right">
        <Boton documento={mercancia} tipo="modificar" coleccion="mercancias" />
        <Boton documento={mercancia} tipo="eliminar"  coleccion="mercancias" />
      </div>
    </Mercancia>
  {/each}
</div>