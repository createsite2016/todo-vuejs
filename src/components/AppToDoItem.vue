<template>
  <li class="todo-item" :class="{'todo-item--done': todo.completed}" @click="toggleToDo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue';
import {Todo} from "@/types/Todo";
export default defineComponent ({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    }
  },
  methods: {
    toggleToDo() {
      this.$emit('toggleToDo', this.todo.id)
    }
  },
  emits: {
    toggleToDo: (id: number) => Number.isInteger(id)
  }
})
</script>
