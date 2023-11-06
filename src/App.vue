<template>
  <AppHeader/>

  <AppFilters :active-filter="activeFilter" @set-filter="setFilter"/>

  <main class="app-main">
    <AppToDoList :todos="todos" @toggle-to-do="toggleToDo" @remove-to-do="removeToDo"/>
    <AppAddToDo @add-to-do="addToDo"/>
  </main>

  <AppFooter/>
</template>

<script lang="ts">
import AppHeader from "@/components/AppHeader.vue";
import AppFilters from "@/components/AppFilters.vue";
import AppToDoList from "@/components/AppToDoList.vue";
import AppAddToDo from "@/components/AppAddToDo.vue";
import AppFooter from "@/components/AppFooter.vue";
import {Todo} from "@/types/Todo";
import {defineComponent} from "vue";
import {Filter} from "@/types/Filter";


interface State {
  todos: Todo[],
  activeFilter: Filter
}

export default defineComponent ({
  components: {
    AppHeader,
    AppFilters,
    AppToDoList,
    AppAddToDo,
    AppFooter
  },
  data():State {
    return {
      todos: [
        {id: 0, text: 'сделать кофе', completed: true},
        {id: 1, text: 'выпить кофе', completed: false},
        {id: 2, text: 'спасти мир', completed: false},
      ],
      activeFilter: 'All'
    }
  },
  methods:{
    addToDo(todo: Todo){
      this.todos.push(todo)
    },
    toggleToDo(id: number){
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeToDo(id: number){
      this.todos = this.todos.filter((todo:Todo) => todo.id !== id)
    },
    setFilter(filter: Filter){
      this.activeFilter = filter
    }
  }
})
</script>
