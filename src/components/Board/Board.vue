<script setup>
import { reactive, ref } from "vue";
import { nanoid } from "nanoid";
import Draggable from "vuedraggable";
import AddNewTask from "../AddNewTask/AddNewTask.vue";
const isModalOpen = ref(false);
const columnsBoard = reactive([
  {
    id: nanoid(),
    title: "TO-DO",
    tasks: [
      {
        id: nanoid(),
        item: "Create marketing landing page",
        createdAt: new Date(),
      },
      {
        id: nanoid(),
        item: "Develop cool new feature",
        createdAt: new Date(),
      },
    ],
  },
  {
    id: nanoid(),
    title: "In Progress",
    tasks: [],
  },
  {
    id: nanoid(),
    title: "Completed",
    tasks: [],
  },
]);
const removeTask = (id) => {
  columnsBoard.map((item) => {
    item.tasks = item.tasks.filter((t) => t.id !== id);
  });
};
</script>

<template>
  <div>
    <Draggable
      v-model="columnsBoard"
      group="columnsBoard"
      @start="drag = true"
      @end="drag = false"
      item-key="id"
      tag="div"
      class="flex justify-around"
    >
      <template #item="{ element: columnsBoard }">
        <div class="flex justify-center items-center py-6">
          <div class="card w-96 bg-base-100 shadow-xl">
            <div class="card-body">
              <h2 class="card-title text-3xl cursor-move">
                {{ columnsBoard.title }}
              </h2>
              <Draggable
                v-model="columnsBoard.tasks"
                :group="{ name: 'tasks' }"
                @start="drag = true"
                @end="drag = false"
                item-key="id"
                tag="div"
              >
                <template #item="{ element: tasks }">
                  <div
                    class="flex items-center my-4 gap-4 w-full shadow-md rounded-md p-5"
                  >
                    <p
                      class="text-md hover:text-gray-300 transition-all cursor-move"
                    >
                      {{ tasks.item }}
                    </p>
                    <button
                      type="button"
                      class="btn btn-outline btn-error"
                      @click="removeTask(tasks.id)"
                    >
                      Remove
                    </button>
                  </div>
                </template>
              </Draggable>
              <footer class="card-actions justify-end">
                <button
                  type="button"
                  class="btn"
                  @click="
                    {
                      isModalOpen = true;
                    }
                  "
                >
                  Add Item
                </button>
              </footer>
            </div>
          </div>
        </div>
      </template>
    </Draggable>
    <div v-if="isModalOpen">
      <Teleport to="#app">
        <AddNewTask
          :isModalOpen="isModalOpen"
          :tasks="columnsBoard[0].tasks"
          @close="isModalOpen = !isModalOpen"
        />
      </Teleport>
    </div>
  </div>
</template>

<style scoped></style>
