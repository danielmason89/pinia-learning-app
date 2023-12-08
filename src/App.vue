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
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks left to do.</p>
      <div v-for="task in taskStore.tasks">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ taskStore.favCount }} favs left to do.</p>
      <div v-for="task in taskStore.favs">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetails.vue"
import { useTaskStore } from "./stores/TaskStore";
import TaskForm from "./components/TaskForm.vue";

export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskStore();
    const filter = ref("all")

    return { taskStore, filter }
  }
}
</script>

<style scoped></style>
