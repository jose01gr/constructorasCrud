<template>
  <div class="content">
    <div class="container-fluid">
      <card>
        <h3 class="text-center">Gestión de Proyectos</h3>
        <div class="form-group">
          <label for="projectName">Nombre del Proyecto:</label>
          <input
            type="text"
            id="projectName"
            class="form-control"
            v-model="newProject.name"
            placeholder="Ingresa el nombre del proyecto"
          />
        </div>
        <div class="form-group">
          <label for="projectDescription">Descripción:</label>
          <textarea
            id="projectDescription"
            class="form-control"
            v-model="newProject.description"
            placeholder="Ingresa una descripción"
          ></textarea>
        </div>
        <div class="row">
          <div class="col-md-6">
            <button class="btn btn-success btn-block" @click="addProject">
              Agregar Proyecto
            </button>
          </div>
          <div class="col-md-6">
            <button class="btn btn-danger btn-block" @click="deleteProject">
              Eliminar proyecto
            </button>
          </div>
        </div>
        <br>
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
      newProject: {
        name: "",
        description: "",
      },
      projects: [],
    };
  },
  methods: {
    addProject() {
      if (this.newProject.name && this.newProject.description) {
        this.projects.push({ ...this.newProject });
        this.newProject.name = "";
        this.newProject.description = "";
        this.$notifications.notify({
          message: `<span>El proyecto fue agregado <b>EXITOSAMENTE</b></span>`,
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
    deleteProject(index) {
      this.projects.splice(index, 1);
      this.$notifications.notify({
        message: `<span>El proyecto fue eliminado <b>EXITOSAMENTE</b></span>`,
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
