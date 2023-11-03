<template>
  <ul class="todo-list">
    <AppToDoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-to-do="toggleToDo"
    />
  </ul>
</template>

<script lang="ts">
import AppToDoItem from "@/components/AppToDoItem.vue";
import {Todo} from "@/types/Todo";
import {defineComponent} from 'vue';

interface State {
  todos: Todo[]
}

export default defineComponent ({
  components: {
    AppToDoItem
  },
  data():State {
    return {
      todos: [
        {id: 0, text: 'сделать кофе', completed: true},
        {id: 1, text: 'выпить кофе', completed: false},
        {id: 2, text: 'спасти мир', completed: false},
      ]
    }
  },
  methods:{
    toggleToDo(id: number){
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    }
  }
})
</script>
