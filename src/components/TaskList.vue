<template>
  <div
    class="p-5 bg-white mt-5 rounded shadow flex justify-between items-center"
  >
    <h3 class="font-bold text-slate-700 text-base">{{ task.title }}</h3>
    <div class="text-right flex items-center justify-between">
      <TrashIcon
        class="w-5 h-5 ml-2 cursor-pointer text-slate-500"
        @click="taskStore.deleteTask(task.id)"
      />
      <HeartIcon
        :class="{ 'text-red-500': task.isFav }"
        class="w-5 h-5 ml-2 cursor-pointer text-slate-500"
        @click="taskStore.toggleFav(task.id)"
      />
    </div>
  </div>
</template>

<script setup>
import { TrashIcon, HeartIcon } from "@heroicons/vue/24/solid";
import { useTaskStore } from "@/stores/TaskStore";
const props = defineProps(["task"]);
const taskStore = useTaskStore();
</script>
