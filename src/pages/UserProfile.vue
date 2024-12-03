<template>
  <div class="content full-page">
    <div class="form-container">
      <edit-profile-form @add-client="addClient"></edit-profile-form>
      
      <div class="client-crud">
        <h3>Clientes Registrados</h3>
        <table class="table">
          <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Correo</th>
              <th>Teléfono</th>
              <th>Dirección</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="client in clients" :key="client.id">
              <td>{{ client.id }}</td>
              <td>{{ client.name }}</td>
              <td>{{ client.email }}</td>
              <td>{{ client.phone }}</td>
              <td>{{ client.address }}</td>
              <td>
                <button @click="deleteClient(client.id)" class="btn btn-danger btn-sm">Eliminar</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import EditProfileForm from './UserProfile/EditProfileForm.vue';

export default {
  components: {
    EditProfileForm,
  },
  data() {
    return {
      clients: [], // Lista de clientes
    };
  },
  methods: {
    addClient(client) {
      const newClient = {
        ...client,
        id: this.clients.length + 1, // Genera un ID único basado en el tamaño actual
      };
      this.clients.push(newClient); // Agrega el cliente a la lista
    },
    deleteClient(clientId) {
      this.clients = this.clients.filter((client) => client.id !== clientId); // Filtra la lista para eliminar el cliente
    },
  },
};
</script>

<style>
.full-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f5f5f5;
  padding: 20px;
}

.form-container {
  width: 100%;
  max-width: 900px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

.client-crud {
  margin-top: 20px;
}

.table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

.table th,
.table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.table th {
  background-color: #f2f2f2;
}
</style>
