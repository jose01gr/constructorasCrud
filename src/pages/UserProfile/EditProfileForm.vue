<template>
  <div class="form-card">
    <form @submit.prevent="submitForm" class="edit-profile-form">
      <h3 class="text-center">Perfil de Cliente</h3>
      <div class="form-group">
        <label for="name">Nombre:</label>
        <input v-model="form.name" type="text" id="name" placeholder="Ingrese el nombre" required />
      </div>
      <div class="form-group">
        <label for="email">Correo:</label>
        <input v-model="form.email" type="email" id="email" placeholder="Ingrese el correo" required />
      </div>
      <div class="form-group">
        <label for="phone">Teléfono:</label>
        <input v-model="form.phone" type="tel" id="phone" placeholder="Ingrese el teléfono" required />
      </div>
      <div class="form-group">
        <label for="address">Dirección:</label>
        <textarea v-model="form.address" id="address" placeholder="Ingrese la dirección" rows="3" required></textarea>
      </div>
      <button type="submit" class="btn btn-success btn-block" >Agregar Cliente</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        phone: '',
        address: '',
      },
    };
  },
  methods: {
    submitForm() {
      this.$emit('add-client', { ...this.form }); // Emitimos los datos del formulario al componente padre
      this.form.name = '';
      this.form.email = '';
      this.form.phone = '';
      this.form.address = '';
    },
  },
};
</script>

<style scoped>

.form-title {
  text-align: center;
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 20px;
}

.edit-profile-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-weight: bold;
  margin-bottom: 5px;
}

.form-group input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
}

.btn:hover {
  background-color: #0056b3;
}
</style>
