<template>
  <div>
    <h1 class="display-4 text-center">Lista de Tareas</h1>
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="card mt-4">
          <div class="card-body">
            <div class="input-group">
              <input
                v-model="tarea"
                type="text"
                class="form-control form-control-lg"
                v
                placeholder="Agregar Tarea"
              />
              <div class="input-group-append">
                <button
                  v-on:click="agregarTarea()"
                  class="btn btn-success btn-lg"
                >
                  Agregar
                </button>
              </div>
            </div>

            <br />
            <h5 v-if="!listTareas.length">No hay tarea para realizar</h5>

            <ul class="list-group">
              <li
                v-for="(tarea, index) of listTareas"
                :key="index"
                class="list-group-item d-flex justify-content-between"
              >
                <span
                  class="cursor"
                  v-bind:class="{ 'text-success': tarea.estado }"
                  v-on:click="editarTarea(index, tarea)"
                >
                  <i
                    v-bind:class="[
                      tarea.estado
                        ? 'fa fa-check-circle'
                        : 'fa-regular fa-circle',
                    ]"
                  ></i>
                </span>
                {{ tarea.nombre }}
                <span class="eraserTask" v-on:click="eliminarTarea(index)"
                  ><i class="fa-solid fa-eraser"></i>
                </span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tarea",
  data() {
    return {
      tarea: "",
      listTareas: [],
    };
  },
  methods: {
    agregarTarea() {
      const tarea = {
        nombre: this.tarea,
        estado: false,
      };
      this.listTareas.push(tarea);
      this.tarea = "";
      console.log(this.listTareas);
    },
    eliminarTarea(index) {
      this.listTareas.splice(index, 1);
    },
    editarTarea(index, tarea) {
      this.listTareas[index].estado = !tarea.estado;
    },
  },
};
</script>

<style>
.eraserTask {
  cursor: pointer;
}
</style>
