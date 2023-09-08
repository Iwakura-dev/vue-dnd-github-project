<script setup>
import { nanoid } from "nanoid";
import { ref } from "vue";
const inputRef = ref("");
const props = defineProps({
  isModalOpen: {
    type: Boolean,
  },
  tasks: {
    type: Array,
  },
});
const createTask = () => {
  props.tasks.push({
    id: nanoid(),
    item: inputRef.value.trim(),
    createdAt: new Date(),
  });
  inputRef.value = "";
};
</script>

<template>
  <div
    class="h-screen w-full z-10 bg-black opacity-25 flex justify-center items-center absolute top-0 left-0 bottom-0 right-0"
    v-show="isModalOpen"
  >
    <div
      class="flex flex-col justify-center items-center bg-white rounded-md p-12 gap-y-4"
    >
      <div>
        <h1 class="font-bold text-3xl text-black">Add Todo</h1>
        <div className="form-control w-full max-w-xs">
          <label className="label">
            <span className="label-text">Input your todo</span>
          </label>
          <input
            type="text"
            placeholder="Type here"
            className="input input-bordered w-full max-w-xs"
            :value="inputRef"
            @input="(event) => (inputRef = event.target.value)"
          />
        </div>
      </div>
      <div class="flex justify-between items-center w-full">
        <button class="btn btn-outline btn-primary" @click="createTask">
          Add
        </button>
        <button class="btn btn-outline btn-primary" @click="$emit('close')">
          Close
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
