<template>
  <div class="content">
    <div class="container-fluid">
      <card>
        <h3 class="text-center">Gestión de Servicios</h3>
        <div class="form-group">
          <label for="serviceName">Nombre del Servicio:</label>
          <input
            type="text"
            id="serviceName"
            class="form-control"
            v-model="newService.name"
            placeholder="Ingresa el nombre del servicio"
          />
        </div>
        <div class="form-group">
          <label for="serviceDescription">Descripción:</label>
          <textarea
            id="serviceDescription"
            class="form-control"
            v-model="newService.description"
            placeholder="Ingresa una descripción del servicio"
          ></textarea>
        </div>
        <div class="form-group">
          <label for="toolsUsed">Herramientas Usadas:</label>
          <input
            type="text"
            id="toolsUsed"
            class="form-control"
            v-model="newService.tools"
            placeholder="Ingresa las herramientas usadas"
          />
        </div>
        <div class="form-group">
          <label for="toolsUsed">Materiales Usados:</label>
          <input
            type="text"
            id="toolsUsed"
            class="form-control"
            v-model="newService.mats"
            placeholder="Ingresa los materiales usados"
          />
        </div>
        <div class="row">
          <div class="col-md-6">
            <button class="btn btn-success btn-block" @click="addService">
              Agregar Servicio
            </button>
          </div>
          <div class="col-md-6">
            <button class="btn btn-danger btn-block" @click="deleteAllServices">
              Eliminar Todos los Servicios
            </button>
          </div>
        </div>
        <br />
        <h4 class="text-center">Lista de Servicios</h4>
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Descripción</th>
              <th>Herramientas Usadas</th>
              <th>Materiales Usados</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(service, index) in services" :key="service.id">
              <td>{{ service.id }}</td>
              <td>{{ service.name }}</td>
              <td>{{ service.description }}</td>
              <td>{{ service.tools }}</td>
              <td>{{ service.mats }}</td>
              <td>
                <button
                  class="btn btn-danger btn-sm"
                  @click="deleteService(index)"
                >
                  Eliminar
                </button>
              </td>
            </tr>
            <tr v-if="services.length === 0">
              <td colspan="5" class="text-center">No hay servicios creados</td>
            </tr>
          </tbody>
        </table>
      </card>
    </div>
  </div>
</template>

<script>
import Card from "src/components/Cards/Card.vue";

export default {
  components: {
    Card,
  },
  data() {
    return {
      newService: {
        id: null,
        name: "",
        description: "",
        tools: "",
      },
      services: [],
      nextServiceId: 1,
    };
  },
  methods: {
    addService() {
      if (
        this.newService.name &&
        this.newService.description &&
        this.newService.tools &&
        this.newService.mats
      ) {
        this.services.push({
          id: this.nextServiceId++,
          name: this.newService.name,
          description: this.newService.description,
          tools: this.newService.tools,
          mats: this.newService.mats
        });
        this.newService.name = "";
        this.newService.description = "";
        this.newService.tools = "";
        this.newService.mats = "";
        this.$notifications.notify({
          message: `<span>El servicio fue agregado <b>EXITOSAMENTE</b></span>`,
          icon: "nc-icon nc-check-2",
          type: "success",
          horizontalAlign: "right",
          verticalAlign: "top",
        });
      } else {
        this.$notifications.notify({
          message: `<span>Por favor, completa todos los campos</span>`,
          icon: "nc-icon nc-alert-circle-i",
          type: "warning",
          horizontalAlign: "right",
          verticalAlign: "top",
        });
      }
    },
    deleteService(index) {
      this.services.splice(index, 1);
      this.$notifications.notify({
        message: `<span>El servicio fue eliminado <b>EXITOSAMENTE</b></span>`,
        icon: "nc-icon nc-simple-remove",
        type: "danger",
        horizontalAlign: "right",
        verticalAlign: "top",
      });
    },
    deleteAllServices() {
      this.services = [];
      this.nextServiceId = 1;
      this.$notifications.notify({
        message: `<span>Todos los servicios fueron eliminados</span>`,
        icon: "nc-icon nc-simple-remove",
        type: "danger",
        horizontalAlign: "right",
        verticalAlign: "top",
      });
    },
  },
};
</script>

<style lang="scss">
/* Puedes agregar estilos personalizados aquí */
</style>
