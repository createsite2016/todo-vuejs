<template>
  <AppHeader/>

  <AppFilters/>

  <main class="app-main">
    <AppToDoList/>
    <AppAddToDo/>
  </main>

  <AppFooter/>
</template>

<script setup lang="ts">
import AppHeader from "@/components/AppHeader.vue";
import AppFilters from "@/components/AppFilters.vue";
import AppToDoList from "@/components/AppToDoList.vue";
import AppAddToDo from "@/components/AppAddToDo.vue";
import AppFooter from "@/components/AppFooter.vue";
</script>
