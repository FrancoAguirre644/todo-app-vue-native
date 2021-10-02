<template>
  <view class="todo-wrapper">
    <touchable-opacity :on-press="handleTaskPressed" v-if="!todo.edited">
      <text
        style="font-size: 20"
        v-bind:class="[
          todo.isCompleted ? 'text-task-completed' : 'text-todo-task',
        ]"
      >
        • {{ todo.task }}
      </text>
    </touchable-opacity>
    <view class="task-input-wrapper" v-if="todo.edited">
      <text-input class="task-input" placeholder='Enter Task' v-model='editedTask'/>
    </view>
    <view class="todo-button-wrapper" v-if="todo.edited">
      <touchable-opacity class="edit-button">
        <button title="Edit" v-bind:on-press="checkOnPress"/>
      </touchable-opacity>
      <touchable-opacity>
        <button title="Cancel" color="#DC143C" v-bind:on-press="cancelOnPress"/>
      </touchable-opacity>
    </view>
    <view class="todo-button-wrapper" v-if="!todo.edited">
      <touchable-opacity class='edit-button'>
        <button title="Edit" :on-press="editOnPress" />
      </touchable-opacity>
      <touchable-opacity>
        <button title="Delete" color="#DC143C" :on-press="deleteOnPress" />
      </touchable-opacity>
    </view>
  </view>
</template>

<script>
export default {
  data: function () {
    return {
      editedTask: this.todo.task,
    };
  },
  props: {
    todo: Object,
    selectedIndex: Number,
    deleteTodo: Function,
    editTodo: Function,
    toggleTaskStatus: Function,
    editPressed: Function,
    cancelEdit: Function,
  },
  methods: {
    deleteOnPress: function () {
      this.deleteTodo(this.selectedIndex);
    },
    checkOnPress: function() {
      if (this.editedTask !== '')
        this.editTodo(this.selectedIndex, this.editedTask)
      else {
        this.editedTask = this.todo.task
        this.cancelEdit(this.selectedIndex)
      }
    },
    handleTaskPressed: function () {
      this.toggleTaskStatus(this.selectedIndex);
    },
    editOnPress: function() {
      this.editPressed(this.selectedIndex)
    },
    cancelOnPress: function() {
      this.cancelEdit(this.selectedIndex)
    },
  },
};
</script>

<style>
.todo-wrapper {
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  width: 100%;
  border-bottom-width: 4;
  border-color: black;
  padding: 10;
}

.task-input-wrapper {
  flex: 1;
  justify-content: center;
  margin-right: 10;
}

.edit-button {
  padding-right: 10
}

.task-input {
  border-bottom-width: 2;
  border-bottom-color: #ddd;
  border-style: solid;
  font-size: 20;
  line-height: 28;
}

.todo-button-wrapper {
  flex-direction: row
}

.text-task-completed {
  color: #DC143C;
  text-decoration-line: line-through;
}

.text-todo-task {
  color: black;
}

.divider {
  border-width: 4;
  border-style: solid;
}

</style>