<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-1"></div>

        <div class="col-md-10">
          <h1 class="text-center">To Do List</h1>
          <div class="inner-flex">
            <div class="text-center">
              <div :class="{ checked: tarefa.checked }">
                <div id="app" class="box content has-text-centered">
                  <h1 class="title is-1">Pontos: {{ pontos }} 🍰</h1>
                </div>
              </div>
            </div>
            
            <form @submit.prevent="addTarefa(tarefa)">
              <div class="input-group">
                <input type="text" v-model="tarefa.descricao" class="form-input" placeholder="Nova tarefa" />
                <button class="btn btn-primary input-group-btn">Adicionar</button>
              </div>
            </form>
            <div class="todo-list">
              <tarefa v-for="t in lista" :key="t.id" @toggle="toggleTask" @remove="removeTarefa" :tarefa="t" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<script>
import Tarefa from "./components/Tarefa";

export default {
  nome: "app",
  components: { Tarefa },
  data() {
    return { pontos: 0, lista: [], tarefa: { checked: false } };
  },

  methods: {

    addTarefa(tarefa) {
      tarefa.id = Date.now();
      this.lista.push(tarefa);
      this.tarefa = { checked: false };
    },

    toggleTask(tarefa) {
      const index = this.lista.findIndex((item) => item.id === tarefa.id);
      if (index > -1) {
        //se houver algum indice
        const checked = !this.lista[index].checked; //qnd estiver marcado,
        this.$set(this.lista, index, { ...this.lista[index], checked }); //priedade do array alterada
        if (tarefa.checked === false) {
          this.pontos+=1;
        }
      }
    },

    removeTarefa(tarefa) {
      const index = this.lista.findIndex((item) => item.id === tarefa.id);
      if (index > -1) {
        this.$delete(this.lista, index);
      }
    },

  }
};
</script>

<style scoped>
.todo-list {
  padding-top: 25px; 
}
.text-center {
  padding: 20px 0px;
}
.inner-flex {
  min-height: 20px;
  margin-bottom: 20px;
  background-color: rgb(245, 245, 245);
  box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 1px inset;
  padding: 18px;
  border-width: 1px;
  border-style: solid;
  border-color: rgb(227, 227, 227);
  border-image: initial;
  border-radius: 4px;
}
</style>