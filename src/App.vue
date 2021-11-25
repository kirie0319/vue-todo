<template>
  <div id="app">
    <h1>ToDo List</h1>
    <div v-for="(radio, index) in options" :key="index">
      <input type="radio" name="status" v-model="current" :value="radio.value">{{radio.lavel}}
    </div>
    <table>
      <tr>
        <th>ID</th>
        <th>comment</th>
        <th>status</th>
      </tr>
      <tr v-for="(task, index) in computedTodoList" :key="index">
        <td>{{index + 1}}</td>
        <td>{{task.content}}</td>
        <td>{{task.statusText}}</td>
        <button @click="changeStatus(index)">changeStatus</button>
        <button @click="deleteTask(index)">delete</button>
      </tr>
    </table>
    <div>
      <p>new task</p>
      <div>
        <input type="text" v-model="todo">
        <button @click="createTask(todo)">create</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      todoList: [],
      todo: '',
      current: -1,
      options: [
        {value: -1, label: 'all'},
        {value: 0, label: 'working'},
        {value: 1, label: 'done'},
      ]
    }
  },
  computed: {
    computedTodoList() {
      return this.todoList.filter(function(e) {
        return this.current < 0 ? true : this.current === e.status
      }, this)
    }
  },
  methods: {
    createTask(todo) {
      this.todoList.push({
        content: todo,
        statusText: 'working',
        status: 0
      });
      this.todo = "";
    },
    deleteTask(index) {
      this.todoList.splice(index, 1);
    },
    changeStatus(index) {
      let status = this.todoList[index].status;
      if(status == 0) {
        this.todoList[index].status = 1;
        this.todoList[index].statusText = 'done';
      } else {
        this.todoList[index].status = 0;
        this.todoList[index].statusText = 'working';
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
