<template>
  <div>
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>

    <!-- # 2.2 Omdat de de todolijstje zelf in de Todo component is opgeslagen kunnnen we deze dynamische inladen en zelfs een v-for op gebruiken zodat het word ingeladen aan hand van de kwantiteit in de todos property  -->

    <!-- # 4.1 Er word geluisterd naar de custom event genaamd delete-todo als de child
    Deze event verstuurt dan word de deleteTodo function gestart -->
    <to-do v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos" v-bind:todo="todo"></to-do>
</div>
</template>

<script type = "text/javascript" >
// # 2.0 Deze file heeft ook een child component genaamd de Todo file.
// Hierdoor word het todolijstje zelf gescheiden van deze component en maakt het nog dynamiser
import ToDo from './ToDo'

export default {
  // #1.1: In de parent component is de todos array gebind en hier moeten we de property gaan declareren
  // zodat we het kunnen gebruiken in het document
  props: ['todos'],
  // # 2.1 net zoals in de parent component moet de file worden ingeladen door het in de components te declaren
  components:{
    ToDo,
  },
  methods: {
    deleteTodo(todo) {
      // # 4.2 De child component heeft een parameter meegegeven van geklikte todo item
      // Er word eerst gekeken op welke plaats de item zich bevind in de array en vervolgens
      // word de todo item eruit verwijderd door splice.
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    completeTodo(todo) {
      console.log(todo)
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
  },
};
</script>
<style>
</style>
