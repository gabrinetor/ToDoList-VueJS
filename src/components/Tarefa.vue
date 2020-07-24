<template>
  <div class="tarefa-criada" :class="{ checked: tarefa.checked }">
    <div class="container">
      <div class="row">

        <div class="col-lg-6">
          <span v-if="tarefa.checked">
            <b-icon icon="check2 "></b-icon>
          </span>
          <span v-else>
            <b-icon icon="clock "></b-icon>
          </span>
          {{ tarefa.descricao }}
        </div>

        <div class="col-lg-3"></div>
        
        <div class="col-lg-3">
          <button @click="$emit('toggle', tarefa)" class="btn btn-success">
            <span v-if="tarefa.checked">Desmarcar</span>
            <span v-else>Concluído</span>
          </button>
          <button type="danger" @click="$emit('remove', tarefa)" class="btn btn-danger">
            <b-icon icon="trash"></b-icon>
          </button>
        </div>

      </div>
    </div>
    <hr>
  </div>
</template>

<script>
export default {
  props: {
    tarefa: { type: Object, required: true }
  }
};
</script>

<style scoped>
.checked {
  text-decoration: line-through;
  color: lightgray;
}
.tarefa-criada { width: 100%; font-size: 21px; }
</style>
