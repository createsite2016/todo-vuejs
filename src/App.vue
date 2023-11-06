<template>
  <AppHeader/>

  <AppFilters :active-filter="activeFilter" @set-filter="setFilter"/>

  <main class="app-main">
    <AppToDoList
        :todos="filteredTodos"
        @toggle-to-do="toggleToDo"
        @remove-to-do="removeToDo"
    />
    <AppAddToDo @add-to-do="addToDo"/>
  </main>

  <AppFooter :stats="stats"/>
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
import {Stats} from "@/types/Stats";


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
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos
        case 'Done':
          return this.doneTodos
        case 'All':
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter(todo => !todo.completed)
    },
    doneTodos(): Todo[] {
      return this.todos.filter(todo => todo.completed)
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
