<template>
  <main>
    <!-- heading -->
    <header class="bg-slate-300 flex items-center justify-center">
      <img
        src="@/assets/pinia-logo.svg"
        alt="pinia logo"
        class="max-w-[60px] transform -rotate-12"
      />
      <h1 class="text-xl ml-[15px] pt-[25px] transform rotate-2">
        Pinia Tasks
      </h1>
    </header>

    <!-- task form -->
    <div>
      <TaskForm />
    </div>

    <!-- filter nav -->
    <nav class="w-[640px] mx-auto my-3 text-right">
      <button
        @click="filter = 'all'"
        class="ml-4 bg-white border-2 border-gray-700 rounded px-2 py-1 cursor-pointer text-base"
      >
        All Tasks
      </button>
      <button
        @click="filter = 'favorite'"
        class="ml-4 bg-white border-2 border-gray-700 rounded px-2 py-1 cursor-pointer text-base"
      >
        Favorite
      </button>
    </nav>

    <!-- loading... -->
    <div
      v-if="taskStore.loading"
      class="max-w-[640px] border border-yellow-400 bg-orange-300 py-1 px-0 text-center my-8 mx-auto text-gray-700 font-semibold rounded"
    >
      Loading...
    </div>

    <!-- task list -->
    <div class="max-w-[640px] mx-auto my-[20px]" v-if="filter === 'all'">
      <p>You have {{ taskStore.totalCount }} tasks left to do.</p>
      <div v-for="task in taskStore.tasks">
        <TaskList :task="task" />
      </div>
    </div>

    <div class="max-w-[640px] mx-auto my-[20px]" v-if="filter === 'favorite'">
      <p>You have {{ taskStore.favoriteCount }} fav tasks left to do.</p>
      <div v-for="task in taskStore.favorite">
        <TaskList :task="task" />
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "@/stores/TaskStore";
import TaskList from "./components/TaskList.vue";
import TaskForm from "./components/TaskForm.vue";

const filter = ref("all");
const taskStore = useTaskStore();
taskStore.getTasks();
</script>
