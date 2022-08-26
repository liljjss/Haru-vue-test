<template>
  <div id="app">
    <form v-on:submit.prevent="addNewTask">
      <h1><label for="new-task">TO-DO LIST</label></h1>
      <input
        v-model="newTaskText"
        id="new-task"
        placeholder="type... 輸入待辦事項"
      />
      <button>新增待辦</button>
    </form>
    <TODOLIST v-bind:tasks="tasks" v-on:delete-task="deleteTask"></TODOLIST>
  </div>
</template>

<script>
import TODOLIST from "./components/todo";

export default {
  name: "App",
  components: {
    TODOLIST,
  },
  data: () => ({
    newTaskText: "",
    tasks: [],
  }),
  methods: {
    addNewTask() {
      const { newTaskText } = this;
      if (!newTaskText) {
        return;
      }
      this.tasks.push({ id: Math.random(), text: this.newTaskText });
      this.newTaskText = null;
    },
    deleteTask(taskId) {
      const remainingTasks = this.tasks.filter((task) => task.id !== taskId);
      this.tasks = remainingTasks;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #429668;
  margin-top: 100px;
}
</style>
