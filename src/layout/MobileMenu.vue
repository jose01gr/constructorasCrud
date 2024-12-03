<template>
  <ul class="nav nav-mobile-menu">
    <base-dropdown>
      <template slot="title">
        <i class="fa fa-globe"></i>
        <b class="caret"></b>
        <span class="notification">3 Notificaciones</span>
      </template>
      <a class="dropdown-item" href="#">El nivel de stock de "Tuberia PVC" ha alcanzado un nivel crítico. Se recomienda realizar un pedido de reposición lo antes posible.</a>
      <a class="dropdown-item" href="#">La entrega de "Cemento" para el proyecto C.C. San Diego se ha retrasado.</a>
      <a class="dropdown-item" href="#">El estado de la tarea "Pintura de Fachada" en el proyecto "Casa Portuguesa" ha cambiado a "Realizado"</a>
    </base-dropdown>
    <li class="nav-item">
      <a href="#" class="nav-link">
        <i class="nc-icon nc-zoom-split hidden-lg-up"></i>
        <span class="d-lg-none">Buscar</span>
      </a>
    </li>
    <!-- <base-dropdown title="Dropdown">
      <a class="dropdown-item" href="#">Action</a>
      <a class="dropdown-item" href="#">Another action</a>
      <a class="dropdown-item" href="#">Something</a>
      <a class="dropdown-item" href="#">Something else here</a>
      <div class="divider"></div>
      <a class="dropdown-item" href="#">Separated link</a>
    </base-dropdown> -->

    <li class="nav-item">
      <a class="nav-link" href="#pablo">
        <span class="no-icon">Log-out</span>
      </a>
    </li>
  </ul>
</template>
<script>
  export default {
    name: 'mobile-menu'
  }
</script>
<style>
</style>
