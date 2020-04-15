<template>
  <div class="todo-list">
    <h1>{{ msg }}</h1>
    <div>現在のタスクは {{ numTodo }}件です</div>
    <div>うち、{{ numCompleted }}件が完了しています</div>
    <div>達成率は{{ mileStone }}%です</div>
    <input class="new-todo" type="text" placeholder="input a new todo" v-model="newTodo" @keyup.enter="addTodo()">
    <ul>
      <li v-for="todo in todoList">
        <input type="checkbox" v-model="todo.completed">
        <span :style="{ color: todo.completed ? 'green' : 'red' }" class="todo" @click="todo.completed = !todo.completed">{{ todo.name }}</span>
        <span @click="deleteTodo(todo)"> x </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todoList',
  data () {
    return {
      msg: 'Welcome to Your Todo List',
      newTodo: null,
      todoList: []
    }
  },
  computed: {
    numTodo () {
      return this.todoList.length
    },
    numCompleted () {
      return this.todoList.filter(x => x.completed).length
    },
    mileStone () {
      return Math.floor((this.numCompleted / this.numTodo) * 100) || 0
    }
  },
  methods: {
    addTodo () {
      if (!this.newTodo) {
        alert('Empty!')
        return
      }

      const newTodo = {
        name: this.newTodo,
        completed: false
      }

      this.todoList.push(newTodo)
      this.newTodo = null
    },
    deleteTodo (todo) {
      const index = this.todoList.indexOf(todo)

      this.todoList.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .new-todo {
    width: 300px;
    font-size: 18px;
    padding: 5px;
  }
  ul {
    width: 300px;
    margin: 50px auto;
    list-style: none;
  }
  .todo {
    font-weight: bold;
    font-size: 18px;
    letter-spacing: 1px;
  }
</style>
