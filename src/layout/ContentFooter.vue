<template>
  <footer class="footer">
    <div class="container-fluid">
      <nav>
        <ul class="footer-menu">
          <li>
            <router-link :to="{path:'/admin'}">Sistema Web de Gestión para Constructora</router-link>
          </li>
        </ul>
      </nav>
      <div class="copyright text-center">
        &copy; Hecho por Grupo 4 - Sistemas de Información II
        <p>Neil Rangel - Hector López - José González - Mauricio Romero</p>
      </div>
    </div>
  </footer>
</template>
<script>
  export default {}

</script>
<style>
p{
  font-size: 14px;
}
</style>
1