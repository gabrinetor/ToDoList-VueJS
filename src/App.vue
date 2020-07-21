<template>
  <div id="app">
    <div class="container grid-xs py-2">
      <!-- <img class="img-responsive img-logo" src="0/assets/logo.png" alt="Vue"> -->
      <form @submit.prevent="addToDo(todo)"> <!--dispara ação para que formulario seja automaticamente atualizado-->
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="Nova tarefa">
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
        <!-- teste {{ todos }} -->
      </form>

      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" @toggle="toggleTodo" @remove="removeTodo" :todo="t" />
      </div>

    </div>
  </div>
</template>

<script>
import Todo from './components/Todo'

export default {
  nome: "app", 
  components: { Todo }, 
  data() {
    return { todos: [], todo: { checked: false } };
  },
  methods: {
    addToDo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false };
      // console.log(this.todo);
    },

    toggleTodo(todo){
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index > -1) {  //se houver algum indice
        const checked = !this.todos[index].checked; //qnd estiver marcado, 
        this.$set(this.todos, index, { ...this.todos[index], checked })//propriedade do array alterada
      }
    },

    removeTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if (index > -1) {  
        this.$delete(this.todos, index);
      }
    }
  }
};
</script>

<style scoped>
  .img-logo {
    max-width: 200px;
    margin: 0 auto;
  }

  .todo-list {
    padding-top: 2rem;  /* 32px; */
  }
</style>