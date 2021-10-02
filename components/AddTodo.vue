<template>
  <view class="container-input">
    <text-input class="input" placeholder="Enter new task" v-model="newTodo" />
    <touchable-opacity :on-press="addTodo" class="btn-add" :disabled="(newTodo === '')">
      <text class="btn-add-text" >ADD TASK</text>
    </touchable-opacity>
  </view>
</template>

<script>
export default {
  data: function () {
    return {
      newTodo: "",
    };
  },
  props: {
    onAdd: Function
  },
  methods: {
    addTodo: function () {
      let todo = {
        task: this.newTodo,
        isCompleted: false,
        edited: false
      };
      this.onAdd(todo)
      this.newTodo = ''
    },
  },
};
</script>

<style scoped>
  .container-input {
    width: 100%;  
    padding: 10;  
  }
  .input {
    border-bottom-width: 2;
    border-bottom-color: #ddd;
    border-style: solid;
    font-size: 20;
    line-height: 28;
    margin-bottom: 15;
    padding: 5;
  }
  .btn-add {
    background-color: #463FAF;
    justify-content: center;
    padding: 15;
    flex-direction: row;
    border-radius: 30;
  }
  .btn-add-text {
    font-size: 18;
    color: #fff;
  }
</style>