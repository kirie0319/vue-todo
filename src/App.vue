<template>
  <div id="app">
    <h1>ToDo List</h1>
    <div v-for="(radio, index) in options" :key="index">
      <input type="radio" name="status" v-model="radioCurrentStatus" :value="radio.value">{{radio.value}}
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
        <td>{{task.status}}</td>
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
      radioCurrentStatus: 'all',
      options: [
        {value: 'all'},
        {value: 'working'},
        {value: 'done'},
      ]
    }
  },
  computed: {
    computedTodoList() {
      return this.todoList.filter(todo => {
        if(this.radioCurrentStatus === 'all') {
          return todo
        } else {
          return this.radioCurrentStatus === todo.status
        }
      })
    }
  },
  methods: {
    createTask(todo) {
      this.todoList.push({
        content: todo,
        status: 'working'
      });
      this.todo = "";
    },
    deleteTask(index) {
      this.todoList.splice(index, 1);
    },
    changeStatus(index) {
      const status = this.todoList[index].status;
      if(status === 'working') {
        this.todoList[index].status = 'done';
      } else {
        this.todoList[index].status = 'working';
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
