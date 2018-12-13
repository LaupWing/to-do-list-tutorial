<template>
<div class='ui centered card'>
  <div class='ui centered card'>

    <!-- 3.0 Deze div word alleen weergeven als NOT isEditing. Oftewel isEditing staat op false -->
    <div class="content" v-show="!isEditing">
      <div class='header'>
        {{ todo.title }}
      </div>
      <div class='meta'>
        {{ todo.project }}
      </div>
      <div class='extra content'>
        <!-- 3.1 Start de function dat de isEditing op True zet -->
        <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <!-- 4.0 bij click event word deleteTodo function gestart met huidige todo iteratie -->
        <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>

    <!-- 3.0 Deze div word alleen weergeven als WEL isEditing. Oftewel isEditing staat op true -->
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >

        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.project" >

        </div>
        <div class='ui two button attached buttons'>
          <!-- 3.1 Start de function dat de isEditing op false zet -->
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" disabled>
      Completed
    </div>
    <div @click="completeTodo(todo)" class='ui bottom attached red basic button' v-show="!isEditing && !todo.done">
      Pending
    </div>
  </div>
</div>
</template>

<script type="text/javascript">
export default {
  props: ['todo'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    // 3.1 Hier word de isEditing getoggled van false naar true en vice versa
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    deleteTodo(todo){
      // # 4.0 De emit stuurt een event naar de parent component(in dit geval is het de todolist)
      // Eerste parameter is event benaming
      // Tweede parameter is de parameter dat gegeven word aan de parent component
      this.$emit('delete-todo', todo)
    },
    completeTodo(todo) {
        this.$emit('complete-todo', todo);
    },
  },
};
</script>
