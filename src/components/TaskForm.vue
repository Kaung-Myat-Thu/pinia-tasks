<template>
  <div class="bg-slate-300 py-5 px-0">
    <form
      @submit.prevent="submit"
      class="max-w-[400px] my-0 mx-auto grid grid-cols-4 gap-3"
    >
      <input
        class="border-0 p-3 rounded-md text-gray-700 text-base col-span-3"
        type="text"
        v-model="newTask"
        placeholder="I need to..."
      />
      <button
        class="bg-yellow-600 border-0 p-3 rounded-md cursor-pointer text-base text-white font-semibold"
      >
        Add
      </button>
    </form>
  </div>
</template>

<script setup>
import { useTaskStore } from "@/stores/TaskStore";
import { ref } from "vue";

const taskStore = useTaskStore();
const newTask = ref("");
const submit = () => {
  if (newTask.value.length > 0) {
    taskStore.addTask({
      title: newTask.value,
      isFav: false,
      id: Math.floor(Math.random() * 100),
    });
    newTask.value = "";
  }
};
</script>
