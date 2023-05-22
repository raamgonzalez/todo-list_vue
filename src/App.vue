<script setup>
  import { RouterLink, RouterView } from "vue-router";
  import { ref } from 'vue';
  import { todosFactory } from "./todosSetup";
  import todosService from "./services/todosService";
  import './assets/main.css'



const {update} = todosFactory();

const isLoading = ref(true);
async function prefetch(){
  update(await todosService.getTodos());
  isLoading.value = false;
  }
  prefetch();

</script>

<template>
  <h1 class="text-center mb-10 text-5xl font-serif font-light">Todo'sty</h1>
  <div class="container min-w-[318px] min-h-[440px] text-[#008080] bold bg-[#ecfffd] rounded-xl px-6 py-8 flex flex-col justify-center shadow-2xl shadow-slate-700 mx-1">
    <h2 v-if = "isLoading" class="font-sans text-3xl">Loading To-Do Lists</h2>
    <template v-if = "!isLoading">
      <router-view />
    </template>
  </div>
</template>

<style>
</style>