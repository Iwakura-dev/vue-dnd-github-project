<script setup>
import Card from "./components/Card/Card.vue";
</script>
<template>
  <div>
    <header>
      <div class="flex justify-evenly items-center py-5 my-2 shadow-md">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          strokeWidth="{1.5}"
          stroke="currentColor"
          class="w-12 h-12"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            d="M3.75 13.5l10.5-11.25L12 10.5h8.25L9.75 21.75 12 13.5H3.75z"
          />
        </svg>
        <h1 class="text-3xl font-bold">Znack as Clone Trello Board</h1>
      </div>
    </header>
    <Card />
  </div>
</template>

<style scoped></style>
