<script setup>
import { reactive, defineEmits } from 'vue';
import TodoButton from './TodoButton.vue'

const emit = defineEmits(['create-todo'])

const todoState = reactive({
    todo: "",
    invalid: null,
    errorMsg: "",
}); 
console.log(todoState.todo);

const createTodo = () => {
  todoState.invalid = null;
  if (todoState.todo !== ""){
    emit("create-todo", todoState.todo);
    todoState.todo = "";
    return;
  }
  todoState.invalid = true;
  todoState.errorMsg = "Todo value can't be empty"
};


</script>

<template>
    <div class="input-wrap" :class="{ 'input-error' : todoState.invalid }">
        <input type="text" v-model="todoState.todo">
        <TodoButton @click="createTodo()" />
        <!-- <button @click="createTodo()">Create</button> -->
    </div>
    <p v-show="todoState.invalid" class="error-msg">{{ todoState.errorMsg }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-error {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }
}
.error-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>