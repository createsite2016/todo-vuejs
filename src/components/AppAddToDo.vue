<template>
  <section class="add-todo">
    <form
        v-if="isFormVisible"
        class="add-todo__form"
        @submit.prevent="addToDo"
    >
      <button class="close-button" type="button" @click="hideForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import {defineComponent} from "vue";
import {Todo} from "@/types/Todo";
interface State{
  isFormVisible: boolean,
  todoText: string,
}
export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: '',
    }
  },
  methods: {
    showForm() {
      this.isFormVisible = true
    },
    hideForm() {
      this.isFormVisible = false
    },
    addToDo(){
      this.$emit('addToDo', {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      })

      this.todoText = ''
    }
  },
  emits: {
    addToDo: (todo: Todo) => todo
  }
})
</script>
