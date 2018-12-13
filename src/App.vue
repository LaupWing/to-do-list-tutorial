<!-- Dit is de main component hier deze component word vervangen op de html index pagina en alle component worden hierin geladen direct of indirect -->
<template>
  <div id="app">
    <!-- #1.1: Hier word de todos array gekoppeld aan de property todos zodat we het in de andere component kunnen gebruiken. We communiceren de todos array met de child component -->
    <todo-list v-bind:todos="todos"></todo-list>
    <!-- Er word hier naar een create-todo event geluisterd en als dat gestart word dan word de function createTodo gestart -->
    <create-todo v-on:create-todo="createTodo"></create-todo>
  </div>
</template>

<script>
// Hier word de todolist file ingeladen uit de components directory
// En word vernoemd naar TodoList
// import sweetalert from 'sweetalert'
import TodoList from './components/TodoList'
import CreateTodo from './components/CreateTodo'
export default {
  name: 'app',
  // Om gebruik te maken van de geimporteerde TodoList of andere componenten moet je het in hierin
  // gaan declareren.
  components:{
    TodoList,
    CreateTodo
  },
  data () {
    return {
      todos: [{
        title: 'Todo A',
        project: 'Project A',
        done: false,
      }, {
        title: 'Todo B',
        project: 'Project B',
        done: true,
      }, {
        title: 'Todo C',
        project: 'Project C',
        done: false,
      }, {
        title: 'Todo D',
        project: 'Project D',
        done: false,
      }],
    }
  },
  methods: {
    // In de array word een nieuwe object in geplaatst
    createTodo(newTodo) {
      this.todos.push(newTodo);
    },
  },
}
</script>

<style>

</style>
