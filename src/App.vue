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
  <div class="container min-w-[300px] min-h-[300px] text-[#008080] bold bg-[#ecfffd] rounded-xl px-6 py-8 flex flex-col justify-center shadow-xl shadow-slate-950 mx-1">
    <h2 v-if = "isLoading" class="font-sans ">Loading To-Do Lists</h2>
    <template v-if = "!isLoading">
      <router-view />
    </template>
  </div>
</template>

<style>
</style>