<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <!-- Tools Table -->
        <div class="col-12 mb-4">
          <div class="card">
            <div class="card-header">
              <h4 class="card-title">Herramientas</h4>
              <p class="card-category">Inventario de Herramientas</p>
              <button class="btn btn-primary" @click="openAddModal('herramienta')">Agregar Herramienta</button>
            </div>
            <div class="card-body">
              <div class="table-responsive">
                <table class="table table-hover table-striped">
                  <thead>
                    <tr>
                      <th v-for="column in table1.columns" :key="column">{{ column }}</th>
                      <th>Acciones</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="row in table1.data" :key="row.id">
                      <td>{{ row.id }}</td>
                      <td>{{ row.nombre }}</td>
                      <td>{{ row.descripción }}</td>
                      <td>{{ row.vidaútil }}</td>
                      <td>{{ row.numero }}</td>
                      <td>
                        <button class="btn btn-view" @click="verHerramienta(row)">Ver</button>
                        <button class="btn btn-edit" @click="openEditModal(row, 'herramienta')">Editar</button>
                        <button class="btn btn-delete" @click="eliminarHerramienta(row.id)">Eliminar</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>

        <!-- Materials Table -->
        <div class="col-12">
          <div class="card">
            <div class="card-header">
              <h4 class="card-title">Materiales</h4>
              <p class="card-category">Inventario de Materiales</p>
              <button class="btn btn-primary" @click="openAddModal('material')">Agregar Material</button>
            </div>
            <div class="card-body">
              <div class="table-responsive">
                <table class="table table-hover">
                  <thead>
                    <tr>
                      <th v-for="column in table2.columns" :key="column">{{ column }}</th>
                      <th>Acciones</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="row in table2.data" :key="row.id">
                      <td>{{ row.id }}</td>
                      <td>{{ row.nombre }}</td>
                      <td>{{ row.descripción }}</td>
                      <td>
                        <button class="btn btn-view" @click="verMaterial(row)">Ver</button>
                        <button class="btn btn-edit" @click="openEditModal(row, 'material')">Editar</button>
                        <button class="btn btn-delete" @click="eliminarMaterial(row.id)">Eliminar</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Edit/Add Modal -->
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <h2>{{ modalMode === 'edit' ? 'Editar' : 'Agregar' }} {{ editingType === 'herramienta' ? 'Herramienta' : 'Material' }}</h2>
        <form @submit.prevent="submitForm">
          <div v-for="(value, key) in editForm" :key="key" class="form-group">
            <label :for="key">{{ key.charAt(0).toUpperCase() + key.slice(1) }}</label>
            <input :id="key" v-model="editForm[key]" :type="key === 'numero' ? 'number' : 'text'" :disabled="key === 'id'">
          </div>
          <div class="modal-actions">
            <button type="submit" class="btn btn-primary">Guardar</button>
            <button type="button" class="btn btn-secondary" @click="closeModal">Cancelar</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      table1: {
        columns: ['Id', 'Nombre', 'Descripción', 'VidaÚtil', 'Número'],
        data: [
          { id: 'H000', nombre: 'Martillo', descripción: 'Herramienta de percusión', vidaútil: '2-3 años', numero: 20 },
          { id: 'H001', nombre: 'Sierra circular', descripción: 'Corte preciso de madera', vidaútil: '1-2 años', numero: 10 },
          { id: 'H002', nombre: 'Taladro eléctrico', descripción: 'Perforación de diversos materiales', vidaútil: '3-5 años', numero: 15 },
          { id: 'H003', nombre: 'Nivel láser', descripción: 'Medición y alineación precisa', vidaútil: '5-7 años', numero: 5 },
          { id: 'H004', nombre: 'Pala', descripción: 'Excavación y movimiento de tierra', vidaútil: '2-3 años', numero: 25 },
          { id: 'H005', nombre: 'Carretilla', descripción: 'Transporte de materiales', vidaútil: '3-5 años', numero: 12 },
          { id: 'H006', nombre: 'Andamio', descripción: 'Plataforma de trabajo en altura', vidaútil: '5-10 años', numero: 8 },
          { id: 'H007', nombre: 'Mezcladora de concreto', descripción: 'Preparación de mezclas', vidaútil: '5-7 años', numero: 3 },
          { id: 'H008', nombre: 'Soldadora', descripción: 'Unión de metales', vidaútil: '5-8 años', numero: 4 },
          { id: 'H009', nombre: 'Compactadora', descripción: 'Compresión de suelos', vidaútil: '4-6 años', numero: 2 },
          { id: 'H010', nombre: 'Generador eléctrico', descripción: 'Suministro de energía', vidaútil: '7-10 años', numero: 3 },
          { id: 'H011', nombre: 'Amoladora', descripción: 'Corte y pulido de materiales', vidaútil: '2-3 años', numero: 8 },
          { id: 'H012', nombre: 'Pistola de clavos', descripción: 'Fijación rápida', vidaútil: '3-5 años', numero: 6 },
          { id: 'H013', nombre: 'Compresor de aire', descripción: 'Suministro de aire comprimido', vidaútil: '5-7 años', numero: 4 },
          { id: 'H014', nombre: 'Escalera extensible', descripción: 'Acceso a alturas', vidaútil: '5-8 años', numero: 10 },
          { id: 'H015', nombre: 'Sierra de inglete', descripción: 'Cortes en ángulo precisos', vidaútil: '4-6 años', numero: 3 },
          { id: 'H016', nombre: 'Vibrador de concreto', descripción: 'Eliminación de burbujas en concreto', vidaútil: '3-5 años', numero: 5 },
          { id: 'H017', nombre: 'Cortadora de azulejos', descripción: 'Corte preciso de cerámicas', vidaútil: '3-5 años', numero: 4 },
          { id: 'H018', nombre: 'Pulidora de concreto', descripción: 'Acabado de superficies', vidaútil: '4-6 años', numero: 2 },
          { id: 'H019', nombre: 'Gato hidráulico', descripción: 'Elevación de cargas pesadas', vidaútil: '5-8 años', numero: 6 }
        ]
      },
      table2: {
        columns: ['Id', 'Nombre', 'Descripción'],
        data: [
          { id: 'M000', nombre: 'Cemento', descripción: 'Material base para construcción' },
          { id: 'M001', nombre: 'Arena', descripción: 'Agregado fino para mezclas' },
          { id: 'M002', nombre: 'Grava', descripción: 'Agregado grueso para concreto' },
          { id: 'M003', nombre: 'Varillas de acero', descripción: 'Refuerzo para estructuras' },
          { id: 'M004', nombre: 'Ladrillos', descripción: 'Unidades de mampostería' },
          { id: 'M005', nombre: 'Bloques de concreto', descripción: 'Elementos prefabricados para muros' },
          { id: 'M006', nombre: 'Madera', descripción: 'Material para encofrados y estructuras' },
          { id: 'M007', nombre: 'Vidrio', descripción: 'Material para ventanas y acabados' },
          { id: 'M008', nombre: 'Tubería PVC', descripción: 'Conducción de agua y drenaje' },
          { id: 'M009', nombre: 'Cable eléctrico', descripción: 'Instalaciones eléctricas' },
          { id: 'M010', nombre: 'Pintura', descripción: 'Acabados y protección de superficies' },
          { id: 'M011', nombre: 'Impermeabilizante', descripción: 'Protección contra humedad' },
          { id: 'M012', nombre: 'Azulejos', descripción: 'Revestimiento de paredes y pisos' },
          { id: 'M013', nombre: 'Yeso', descripción: 'Material para acabados interiores' },
          { id: 'M014', nombre: 'Aislante térmico', descripción: 'Control de temperatura' },
          { id: 'M015', nombre: 'Láminas de acero', descripción: 'Techos y estructuras metálicas' },
          { id: 'M016', nombre: 'Sellador', descripción: 'Sellado de juntas y grietas' },
          { id: 'M017', nombre: 'Adoquines', descripción: 'Pavimentación de exteriores' },
          { id: 'M018', nombre: 'Malla electrosoldada', descripción: 'Refuerzo para losas y muros' },
          { id: 'M019', nombre: 'Geotextil', descripción: 'Estabilización de suelos' }
        ]
      },
      showModal: false,
      editForm: {},
      editingType: '',
      modalMode: 'edit'
    }
  },
  methods: {
    verHerramienta(row) {
      alert(`Ver Herramienta: ${row.nombre}`);
    },
    verMaterial(row) {
      alert(`Ver Material: ${row.nombre}`);
    },
    openEditModal(row, type) {
      this.editForm = { ...row };
      this.editingType = type;
      this.modalMode = 'edit';
      this.showModal = true;
    },
    openAddModal(type) {
      this.editingType = type;
      this.modalMode = 'add';
      this.editForm = type === 'herramienta' 
        ? { id: this.getNextId('H'), nombre: '', descripción: '', vidaútil: '', numero: 0 }
        : { id: this.getNextId('M'), nombre: '', descripción: '' };
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
      this.editForm = {};
      this.editingType = '';
    },
    submitForm() {
      if (this.modalMode === 'edit') {
        this.editingType === 'herramienta' ? this.editarHerramienta(this.editForm) : this.editarMaterial(this.editForm);
      } else {
        this.editingType === 'herramienta' ? this.agregarHerramienta(this.editForm) : this.agregarMaterial(this.editForm);
      }
      this.closeModal();
    },
    editarHerramienta(editedHerramienta) {
      const index = this.table1.data.findIndex(item => item.id === editedHerramienta.id);
      if (index !== -1) {
        this.$set(this.table1.data, index, { ...editedHerramienta });
      }
    },
    editarMaterial(editedMaterial) {
      const index = this.table2.data.findIndex(item => item.id === editedMaterial.id);
      if (index !== -1) {
        this.$set(this.table2.data, index, { ...editedMaterial });
      }
    },
    agregarHerramienta(nuevaHerramienta) {
      this.table1.data.push(nuevaHerramienta);
    },
    agregarMaterial(nuevoMaterial) {
      this.table2.data.push(nuevoMaterial);
    },
    eliminarHerramienta(id) {
      this.table1.data = this.table1.data.filter(item => item.id !== id);
    },
    eliminarMaterial(id) {
      this.table2.data = this.table2.data.filter(item => item.id !== id);
    },
    getNextId(prefix) {
      const items = prefix === 'H' ? this.table1.data : this.table2.data;
      const maxId = items.reduce((max, item) => {
        const num = parseInt(item.id.slice(1));
        return num > max ? num : max;
      }, 0);
      return `${prefix}${(maxId + 1).toString().padStart(3, '0')}`;
    }
  }
}
</script>

<style scoped>
.btn {
  padding: 6px 12px;
  font-size: 14px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  margin: 0 5px;
}

.btn-primary { background-color: #007bff; color: white; }
.btn-primary:hover { background-color: #0056b3; }

.btn-view { background-color: #4CAF50; color: white; }
.btn-view:hover { background-color: #45a049; }

.btn-edit { background-color: #ffa500; color: white; }
.btn-edit:hover { background-color: #e69500; }

.btn-delete { background-color: #f44336; color: white; }
.btn-delete:hover { background-color: #da190b; }

.table-hover tbody tr:hover { background-color: #f5f5f5; }
.table-striped tbody tr:nth-of-type(odd) { background-color: #f9f9f9; }

.modal {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #fefefe;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 500px;
  border-radius: 8px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.modal-actions {
  text-align: right;
  margin-top: 20px;
}

.btn-secondary {
  background-color: #6c757d;
  color: white;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-title {
  margin-bottom: 0;
}
</style>