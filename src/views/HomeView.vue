<script setup>

  import {todosFactory} from '../todosSetup';

  const {todosIncompleted, todosCompleted, toggle, deleteTodo} = todosFactory();

  const {add} = todosFactory();
  const addAndNavigate = (name) => {
    add(name);
    router.push('/');
};

</script>

<template>
  <main class="font-serif">
    <h2 class="text-2xl border-b-2 border-slate-200">Add</h2>
    <div class="container__child flex flex-row gap-5 place-items-center mt-4">
        <input autofocus id="new-task" type="text" v-model="name" placeholder="New Tarea" class="rounded-lg py-1 px-2 w-44 border border-gray-800 text-slate-700 shadow-sm shadow-[#00808084]">
        <button autofocus class="button__add w-full h-[34px] shadow-[#00808084] rounded-md text-l py-1 px-4 shadow-sm hover:scale-105 transition ease-in-out text-slate-700" type="add" @click="addAndNavigate(name)">Add task</button>
    </div>
    <div class="container__child my-6 flex flex-col gap-6 mt-10">
      <h2 class="text-2xl border-b-2 border-slate-200">Task</h2>
      <p v-if = "todosIncompleted.length === 0" class="font-light ">Nothing todo</p>
      <ul id="incomplete-tasks" class="flex flex-col gap-6 justify-start">
        <li v-for="todo in todosIncompleted" :key="todo.id" @click="toggle(todo.id)" class="flex flex-row justify-between gap-8 place-items-center w-full">
          <input class="checkbox" type="checkbox">
          <label class="text-left flex-grow">{{ todo.name }}</label>
          <button class="delete rounded-md py-1 px-2 shadow-[#00808084] shadow-sm hover:scale-105 hover:bg-rose-100 transition ease-in-out text-slate-700 text-l " @click= "deleteTodo(todo.id)">Delete</button>
        </li>
      </ul>
      <h2 class=" text-2xl border-b-2 border-slate-200">Completed</h2>
      <ul id="completed-tasks" class="flex flex-col gap-6">
        <li v-for="todo in todosCompleted" :key="todo.id" @click="toggle(todo.id)" class="flex flex-row justify-between gap-8 place-items-center w-full">
          <input type="checkbox" checked @click="toggle(todo.id)">
          <label class=" text-left flex-grow line-through">{{ todo.name }}</label>
          <button class="delete delete rounded-md py-1 px-2 shadow-[#00808084] shadow-sm hover:scale-105 hover:bg-rose-100 transition ease-in-out text-slate-700 text-l" @click= "deleteTodo(todo.id)">Delete</button>
        </li>
      </ul>
    </div>
  </main>
</template>

<style>
    
  .checkbox{
    cursor: pointer;
    background-color: #fff;
    width: 10px;
    height: 10px;
    appearance: none;
    border: 1px solid #090909c5;
  }
      
  .checkbox:checked{
    background-color: #000;
  }
</style>
