<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-xl-3 col-md-6">
          <stats-card>
            <div slot="header" class="icon-warning">
              <i class="nc-icon nc-chart text-warning"></i>
            </div>
            <div slot="content">
              <p class="card-category">Proyectos Activos</p>
              <h4 class="card-title">7</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>Actualizado Ahora
            </div>
          </stats-card>
        </div>

        <div class="col-xl-3 col-md-6">
          <stats-card>
            <div slot="header" class="icon-success">
              <i class="nc-icon nc-light-3 text-success"></i>
            </div>
            <div slot="content">
              <p class="card-category">Tareas Completadas</p>
              <h4 class="card-title">12</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-calendar-o"></i>Último Día
            </div>
          </stats-card>
        </div>

        <div class="col-xl-3 col-md-6">
          <stats-card>
            <div slot="header" class="icon-danger">
              <i class="nc-icon nc-vector text-danger"></i>
            </div>
            <div slot="content">
              <p class="card-category">Herramientas Usadas</p>
              <h4 class="card-title">21</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-clock-o"></i>Último Día
            </div>
          </stats-card>
        </div>

        <div class="col-xl-3 col-md-6">
          <stats-card>
            <div slot="header" class="icon-info">
              <i class="nc-icon nc-favourite-28 text-primary"></i>
            </div>
            <div slot="content">
              <p class="card-category">Proyectos Completados</p>
              <h4 class="card-title">9</h4>
            </div>
            <div slot="footer">
              <i class="fa fa-refresh"></i>Actualizado Ahora
            </div>
          </stats-card>
        </div>

      </div>
      <div class="row">
        <div class="col-md-8">
          <chart-card :chart-data="lineChart.data"
                      :chart-options="lineChart.options"
                      :responsive-options="lineChart.responsiveOptions">
            <template slot="header">
              <h4 class="card-title">Empleados en Activo</h4>
              <p class="card-category">En las últimas 24 horas</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle text-info"></i> IAM Fumcosandi
                <i class="fa fa-circle text-danger"></i> Jardín Botánico Guacara
                <i class="fa fa-circle text-warning"></i> Polar C.A.
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-history"></i> Updated 3 minutes ago
              </div>
            </template>
          </chart-card>
        </div>

        <div class="col-md-4">
          <chart-card :chart-data="pieChart.data" chart-type="Pie">
            <template slot="header">
              <h4 class="card-title">Utilización de recursos</h4>
              <p class="card-category"> Porcentaje de utilización de maquinaria, equipos y mano de obra</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle text-info"></i> Maquinaria
                <i class="fa fa-circle text-danger"></i> Equipos
                <i class="fa fa-circle text-warning"></i> Mano de Obra
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-clock-o"></i> Porcentaje del último día
              </div>
            </template>
          </chart-card>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <chart-card
            :chart-data="barChart.data"
            :chart-options="barChart.options"
            :chart-responsive-options="barChart.responsiveOptions"
            chart-type="Bar">
            <template slot="header">
              <h4 class="card-title">Comparación de cumplimiento de plazos de entrega</h4>
              <p class="card-category">Número de proyectos entregados a tiempo 2022-2023</p>
            </template>
            <template slot="footer">
              <div class="legend">
                <i class="fa fa-circle text-danger"></i> 2022
                <i class="fa fa-circle text-info"></i> 2023
              </div>
              <hr>
              <div class="stats">
                <i class="fa fa-check"></i> Información de datos Certificada
              </div>
            </template>
          </chart-card>
        </div>

        <div class="col-md-6">
  <card>
    <template slot="header">
      <h4 class="card-title">Tareas</h4>
      <p class="category">Cumplimiento de tareas</p>
    </template>

    <!-- Tabla corregida -->
    <l-table :data="tableData.data">
      <template v-slot:default="{ row }">
        <tr>
          <!-- Checkbox para marcar las tareas -->
          <td>
            <base-checkbox v-model="row.checked"></base-checkbox>
          </td>

          <!-- Título de la tarea -->
          <td>{{ row.title }}</td>

          <!-- Acciones para editar y eliminar -->
          <td class="td-actions text-right">
            <button
              type="button"
              class="btn-simple btn btn-xs btn-info"
              v-tooltip.top-center="editTooltip"
            >
              <i class="fa fa-edit"></i>
            </button>
            <button
              type="button"
              class="btn-simple btn btn-xs btn-danger"
              v-tooltip.top-center="deleteTooltip"
              @click="deleteRow(row)"
            >
              <i class="fa fa-times"></i>
            </button>
          </td>
        </tr>
      </template>
    </l-table>

    <div class="footer">
      <hr />
      <div class="stats">
        <i class="fa fa-history"></i> Actualizado hace 13 minutos
      </div>
    </div>
  </card>
</div>

      </div>
    </div>
  </div>
</template>
<script>
  import ChartCard from 'src/components/Cards/ChartCard.vue'
  import StatsCard from 'src/components/Cards/StatsCard.vue'
  import LTable from 'src/components/Table.vue'

  export default {
    components: {
      LTable,
      ChartCard,
      StatsCard,
    },
    data () {
      return {
        editTooltip: 'Edit Task',
        deleteTooltip: 'Remove',
        pieChart: {
          data: {
            labels: ['40%', '20%', '40%'],
            series: [40, 20, 40]
          }
        },
        lineChart: {
          data: {
            labels: ['9:00AM', '12:00AM', '3:00PM', '6:00PM', '9:00PM'],
            series: [
              [12, 9, 12, 14, 5],
              [7, 13, 5, 8, 8],
              [23, 34, 35, 37, 40]
            ]
          },
          options: {
            low: 0,
            high: 50,
            showArea: false,
            height: '245px',
            axisX: {
              showGrid: false
            },
            lineSmooth: true,
            showLine: true,
            showPoint: true,
            fullWidth: true,
            chartPadding: {
              right: 50
            }
          },
          responsiveOptions: [
            ['screen and (max-width: 640px)', {
              axisX: {
                labelInterpolationFnc (value) {
                  return value[0]
                }
              }
            }]
          ]
        },
        barChart: {
          data: {
            labels: ['En', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 'Jul', 'Ago', 'Sep', 'Oct', 'Nov', 'Dic'],
            series: [
              [16, 13, 15, 12, 14, 9, 12, 14, 15, 16, 18, 17],
              [12, 11, 10, 9, 12, 10, 15, 7, 9, 6, 10, 12]
            ]
          },
          options: {
            seriesBarDistance: 10,
            axisX: {
              showGrid: false
            },
            height: '200px',
            low: 0,
            high: 20
          },
          responsiveOptions: [
            ['screen and (max-width: 640px)', {
              seriesBarDistance: 5,
              axisX: {
                labelInterpolationFnc (value) {
                  return value[0]
                }
              }
            }]
          ]
        },
        tableData: {
          data: [
            { title: 'IAM FUMCOSANDI: Eliminación de escombros, basura y residuos de construcción.', checked: false },
            { title: 'Parque Negra Hipólita: Eliminación de malezas y poda de plantas', checked: true },
            { title: 'Polar C.A.: Lavado y desinfección de superficies', checked: true },
            { title: 'Jardín Botánico Guacara: Revisión y reparación de cercas, puertas y sistemas de riego.', checked: false },
        ],
      },

      }
    }
  }
</script>
<style>

</style>
