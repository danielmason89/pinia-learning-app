<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia-logo">
      <h1>Pinia Tasks</h1>
    </header>
    <!-- new task form -->
    <span class="new-task-form">
      <TaskForm />
    </span>
    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All Tasks</button>
      <button @click="filter = 'favs'">Fav Tasks</button>
    </nav>
    <!-- task list -->
    <!-- loading -->
    <span class="loading" v-if="loading">Loading tasks...</span>
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do.</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} favs left to do.</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>
    <button @click="taskStore.$reset">Reset Tasks</button>
  </main>
</template>

<script>
import { ref } from "vue";
import { storeToRefs } from "pinia";
import TaskDetails from "./components/TaskDetails.vue"
import { useTaskStore } from "./stores/TaskStore";
import TaskForm from "./components/TaskForm.vue";

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const { tasks, isLoading, favs, totalCount, favCount } = storeToRefs(taskStore);

    // Fetch Tasks
    taskStore.getTasks();
    const filter = ref("all");

    return { taskStore, filter, tasks, isLoading, favs, totalCount, favCount }
  }
}
</script>

<style scoped></style>
