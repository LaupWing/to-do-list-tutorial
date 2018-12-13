<template>
  <div class='ui basic content center aligned segment'>
    <!-- Button word alleen weergeven als isCreating false is -->
    <!-- Bij het klikken op de button word de function openForm gestart waardoor isCreating op true word gezet -->
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <!-- Div word alleen weergeven als isCreating op true staat  -->
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>Title</label>
            <!-- Input is dynamische gekoppeld aan de property titleText -->
            <input v-model="titleText" type='text' ref='title' defaultValue="">
          </div>
          <div class='field'>
            <label>Project</label>
            <!-- Input is dynamische gekoppeld aan de property projectText -->
            <input v-model="projectText" type='text' ref='project' defaultValue="">
          </div>
          <div class='ui two button attached buttons'>
            <!-- Bij click word de sendForm function gestart -->
            <button class='ui basic blue button' v-on:click="sendForm()">
              Create
            </button>
            <!-- Klik hierop en isCreating word op false gezet -->
            <button class='ui basic red button' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleText: '',
      projectText: '',
      isCreating: false,
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      console.log(this.titleText.length, this.projectText.length)

      if (this.titleText.length > 0 && this.projectText.length > 0) {
        console.log("testing")
        const title = this.titleText;
        const project = this.projectText;
        this.$emit('create-todo', {
          title,
          project,
          done: false,
        });
        this.titleText = '';
        this.projectText = '';
        this.isCreating = false;
      }
    },
  },
};
</script>
