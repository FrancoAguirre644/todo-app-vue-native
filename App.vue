<template>
  <view class="container">
    <header/>
    <add-todo :on-add='addTodo' />
    <scroll-view>
      <view class="todo-wrapper" v-for="(todo, index) in todos" :key="index">
        <todo-item
          :todo="todo"
          :selected-index='index'
          :edit-pressed='onEditPressed'
          :cancel-edit='cancelEdit'
          :edit-todo='editTodo'
          :delete-todo='deleteTodo'
          :toggle-task-status='toggleTaskStatus'
        />
    </scroll-view>
  </view>
</template>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
  margin-top: 30;
}

.todo-wrapper {
  flex-direction: row;
  justify-content: space-between;
  padding: 10;
  border-radius: 5;
}
</style>

<script>

import { ToastAndroid, Keyboard } from 'react-native';

import AddTodo from "./components/AddTodo.vue";
import TodoItem from "./components/TodoItem.vue";
import Header from "./components/Header.vue";

export default {
  data: function() {
    return {
      todos: []
    }
  },
  components: {
    AddTodo,
    TodoItem,
    Header
  },
  methods: {
    addTodo: function(todo) {
      Keyboard.dismiss()
      this.todos.push(todo)
      ToastAndroid.show(`Task ${todo.task} created Successfully.`, ToastAndroid.LONG)
    },
    editTodo: function(index, editedTask) {
      Keyboard.dismiss()
      this.todos[index].task = editedTask
      this.todos[index].edited = false
    },
    onEditPressed: function(index) {
      this.todos[index].edited = true
    },
    deleteTodo: function(index) {
      this.todos.splice(index, 1)
      ToastAndroid.show(`Task deleted Successfully.`, ToastAndroid.LONG)
    },
    cancelEdit: function(index) {
      this.todos[index].edited = false
    },
    toggleTaskStatus: function(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted
    },
  }
};
</script>
