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
      v-if="loading"
      class="max-w-[640px] border border-yellow-400 bg-orange-300 py-1 px-0 text-center my-8 mx-auto text-gray-700 font-semibold rounded"
    >
      Loading...
    </div>

    <!-- task list -->
    <div class="max-w-[640px] mx-auto my-[20px]" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do.</p>
      <div v-for="task in tasks">
        <TaskList :task="task" />
      </div>
    </div>

    <div class="max-w-[640px] mx-auto my-[20px]" v-if="filter === 'favorite'">
      <p>You have {{ favoriteCount }} fav tasks left to do.</p>
      <div v-for="task in favorite">
        <TaskList :task="task" />
      </div>
    </div>

    <div class="max-w-[640px] mx-auto my-[20px]">
      <button
        @click="taskStore.$reset"
        class="bg-red-400 px-4 py-2 rounded float-right mb-4 text-white font-normal"
      >
        Reset the state
      </button>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "@/stores/TaskStore";
import { storeToRefs } from "pinia";

import TaskList from "./components/TaskList.vue";
import TaskForm from "./components/TaskForm.vue";

const filter = ref("all");
const taskStore = useTaskStore();
const { favoriteCount, totalCount, favorite, tasks, loading } =
  storeToRefs(taskStore);

taskStore.getTasks();
</script>
