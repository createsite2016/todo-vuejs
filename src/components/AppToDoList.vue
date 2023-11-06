<template>
  <ul class="todo-list">
    <AppToDoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-to-do="toggleToDo"
        @remove-to-do="removeToDo"
    />
  </ul>
</template>

<script lang="ts">
import AppToDoItem from "@/components/AppToDoItem.vue";
import { Todo } from "@/types/Todo";
import {defineComponent, PropType} from 'vue';

export default defineComponent ({
  components: {
    AppToDoItem
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>
    }
  },
  methods:{
    toggleToDo(id: number){
      this.$emit('toggleToDo', id)
    },
    removeToDo(id: number){
      this.$emit('removeToDo', id)
    }
  },
  emits: {
    toggleToDo: (id: number) => Number.isInteger(id),
    removeToDo: (id: number) => Number.isInteger(id),
  }
})
</script>
