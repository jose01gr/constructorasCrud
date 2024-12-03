<template>
  <div class="content">
    <div class="container-fluid">
      <card>
        <h3 class="text-center">Gestión de Empleados y Nóminas</h3>
        
        <!-- Formulario de Empleados -->
        <h4 class="text-center">Agregar Empleado</h4>
        <div class="form-group">
          <label for="employeeName">Nombre:</label>
          <input type="text" id="employeeName" class="form-control" v-model="newEmployee.nombre" placeholder="Ingresa el nombre del empleado" />
        </div>
        <div class="form-group">
          <label for="employeeCedula">Cédula:</label>
          <input type="text" id="employeeCedula" class="form-control" v-model="newEmployee.cedula" placeholder="Ingresa la cédula del empleado" />
        </div>
        <div class="form-group">
          <label for="employeePhone">Número de teléfono:</label>
          <input type="tel" id="employeePhone" class="form-control" v-model="newEmployee.telefono" placeholder="Ingresa el número de teléfono" />
        </div>
        <div class="form-group">
          <label for="employeeAddress">Dirección:</label>
          <input type="text" id="employeeAddress" class="form-control" v-model="newEmployee.direccion" placeholder="Ingresa la dirección del empleado" />
        </div>
        <div class="form-group">
          <label for="employeeEmail">Correo:</label>
          <input type="email" id="employeeEmail" class="form-control" v-model="newEmployee.correo" placeholder="Ingresa el correo del empleado" />
        </div>
        <div class="form-group">
          <label for="employeeBirthdate">Fecha de nacimiento:</label>
          <input type="date" id="employeeBirthdate" class="form-control" v-model="newEmployee.fechaNacimiento" />
        </div>
        <div class="form-group">
          <label for="employeeStatus">Estado operativo:</label>
          <select id="employeeStatus" class="form-control" v-model="newEmployee.estadoOperativo">
            <option value="Activo">Activo</option>
            <option value="Inactivo">Inactivo</option>
          </select>
        </div>
        <button class="btn btn-primary btn-block" @click="addEmployee">Agregar Empleado</button>
        
        <!-- Lista de Empleados -->
        <h4 class="text-center mt-4">Lista de Empleados</h4>
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Nombre</th>
              <th>Cédula</th>
              <th>Teléfono</th>
              <th>Dirección</th>
              <th>Correo</th>
              <th>Fecha de Nacimiento</th>
              <th>Estado Operativo</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(employee, index) in employees" :key="employee.cedula">
              <td>{{ employee.nombre }}</td>
              <td>{{ employee.cedula }}</td>
              <td>{{ employee.telefono }}</td>
              <td>{{ employee.direccion }}</td>
              <td>{{ employee.correo }}</td>
              <td>{{ employee.fechaNacimiento }}</td>
              <td>{{ employee.estadoOperativo }}</td>
              <td>
                <button class="btn btn-danger btn-sm" @click="deleteEmployee(index)">Eliminar</button>
              </td>
            </tr>
            <tr v-if="employees.length === 0">
              <td colspan="8" class="text-center">No hay empleados registrados</td>
            </tr>
          </tbody>
        </table>

        <!-- Formulario de Nóminas -->
        <h4 class="text-center mt-4">Gestión de Nóminas</h4>
        <div class="form-group">
          <label for="employeeId">Cédula:</label>
          <input
            type="text"
            id="employeeId"
            class="form-control"
            v-model="newPayroll.cedula"
            placeholder="Ingresa la cédula del empleado"
          />
        </div>
        <div class="form-group">
          <label for="position">Cargo:</label>
          <input
            type="text"
            id="position"
            class="form-control"
            v-model="newPayroll.cargo"
            placeholder="Ingresa el cargo del empleado"
          />
        </div>
        <div class="form-group">
          <label for="entryDate">Fecha de Ingreso:</label>
          <input
            type="date"
            id="entryDate"
            class="form-control"
            v-model="newPayroll.fechaIngreso"
          />
        </div>
        <div class="form-group">
          <label>Valoración:</label>
          <div class="rating-stars">
            <span v-for="star in 5" :key="star">
              <input 
                type="radio" 
                :id="'star-' + star" 
                :value="star" 
                v-model="newPayroll.valoracion" />
              <label :for="'star-' + star">⭐</label>
            </span>
          </div>
        </div>

        <div class="form-group">
          <label for="salary">Salario:</label>
          <div class="input-group">
            <span class="input-group-text">Bs</span>
            <input 
              type="number" 
              id="salary" 
              class="form-control" 
              v-model="newPayroll.salario" 
              placeholder="Ingresa el salario del empleado" />
          </div>
        </div>

        <div class="row">
          <div class="col-md-6">
            <button class="btn btn-success btn-block" @click="addPayroll">
              Agregar Nómina
            </button>
          </div>
          <div class="col-md-6">
            <button class="btn btn-danger btn-block" @click="deleteAllPayrolls">
              Eliminar Todas las Nóminas
            </button>
          </div>
        </div>
        
        <!-- Lista de Nóminas -->
        <h4 class="text-center mt-4">Lista de Nóminas</h4>
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>ID de Nómina</th>
              <th>Cédula</th>
              <th>Cargo</th>
              <th>Fecha de Ingreso</th>
              <th>Valoración</th>
              <th>Salario</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(payroll, index) in payrolls" :key="payroll.id">
              <td>{{ payroll.id }}</td>
              <td>{{ payroll.cedula }}</td>
              <td>{{ payroll.cargo }}</td>
              <td>{{ payroll.fechaIngreso }}</td>
              <td>{{ payroll.valoracion }}</td>
              <td>{{ payroll.salario }}</td>
              <td>
                <button
                  class="btn btn-danger btn-sm"
                  @click="deletePayroll(index)"
                >
                  Eliminar
                </button>
              </td>
            </tr>
            <tr v-if="payrolls.length === 0">
              <td colspan="7" class="text-center">No hay nóminas registradas</td>
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
      newEmployee: {
        nombre: "",
        cedula: "",
        telefono: "",
        direccion: "",
        correo: "",
        fechaNacimiento: "",
        estadoOperativo: "Activo",
      },
      employees: [],
      newPayroll: {
        id: null,
        cedula: "",
        cargo: "",
        fechaIngreso: "",
        valoracion: "",
        salario: null,
      },
      payrolls: [],
      nextPayrollId: 1,
    };
  },
  methods: {
    addEmployee() {
      if (
        this.newEmployee.nombre &&
        this.newEmployee.cedula &&
        this.newEmployee.telefono &&
        this.newEmployee.direccion &&
        this.newEmployee.correo &&
        this.newEmployee.fechaNacimiento
      ) {
        this.employees.push({ ...this.newEmployee });
        this.newEmployee = {
          nombre: "",
          cedula: "",
          telefono: "",
          direccion: "",
          correo: "",
          fechaNacimiento: "",
          estadoOperativo: "Activo",
        };
        this.$notifications.notify({
          message: `<span>El empleado fue agregado <b>EXITOSAMENTE</b></span>`,
          icon: "nc-icon nc-check-2",
          type: "success",
          horizontalAlign: "right",
          verticalAlign: "top",
        });
      } else {
        this.$notifications.notify({
          message: `<span>Por favor, completa todos los campos del empleado</span>`,
          icon: "nc-icon nc-alert-circle-i",
          type: "warning",
          horizontalAlign: "right",
          verticalAlign: "top",
        });
      }
    },
    deleteEmployee(index) {
      this.employees.splice(index, 1);
      this.$notifications.notify({
        message: `<span>El empleado fue eliminado <b>EXITOSAMENTE</b></span>`,
        icon: "nc-icon nc-simple-remove",
        type: "danger",
        horizontalAlign: "right",
        verticalAlign: "top",
      });
    },
    addPayroll() {
      if (
        this.newPayroll.cedula &&
        this.newPayroll.cargo &&
        this.newPayroll.fechaIngreso &&
        this.newPayroll.valoracion &&
        this.newPayroll.salario
      ) {
        this.payrolls.push({
          id: this.nextPayrollId++,
          cedula: this.newPayroll.cedula,
          cargo: this.newPayroll.cargo,
          fechaIngreso: this.newPayroll.fechaIngreso,
          valoracion: this.newPayroll.valoracion + "⭐",
          salario: this.newPayroll.salario + " Bs",
        });
        this.newPayroll = {
          id: null,
          cedula: "",
          cargo: "",
          fechaIngreso: "",
          valoracion: "",
          salario: null,
        };
        this.$notifications.notify({
          message: `<span>La nómina fue agregada <b>EXITOSAMENTE</b></span>`,
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
    deletePayroll(index) {
      this.payrolls.splice(index, 1);
      this.$notifications.notify({
        message: `<span>La nómina fue eliminada <b>EXITOSAMENTE</b></span>`,
        icon: "nc-icon nc-simple-remove",
        type: "danger",
        horizontalAlign: "right",
        verticalAlign: "top",
      });
    },
    deleteAllPayrolls() {
      this.payrolls = [];
      this.nextPayrollId = 1;
      this.$notifications.notify({
        message: `<span>Todas las nóminas fueron eliminadas</span>`,
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