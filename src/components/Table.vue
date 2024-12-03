<template>
  <table class="table">
    <thead>
      <tr>
        <th v-for="column in columns" :key="column">{{ column }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in data" :key="index">
        <td v-for="column in columns" :key="column">{{ item[column.toLowerCase()] }}</td>
        <td>
          <button class="btn btn-view" @click="verHerramienta(item)">Ver</button>
          <button class="btn btn-edit" @click="editarHerramienta(item)">Editar</button>
          <button class="btn btn-delete" @click="eliminarHerramienta(item.id)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'l-table',
  props: {
    columns: {
      type: Array,
      required: true
    },
    data: {
      type: Array,
      required: true
    }
  },
    methods: {
    }
  }
</script>
<style scoped>
.table {
  width: 100%;
  border-collapse: collapse;
}

.table th,
.table td {
  border: 1px solid #ddd;
  padding: 8px;
}

.table th {
  background-color: #f2f2f2;
  text-align: left;
}
</style>