<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">home</router-link>

    <AddTodo
      @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      :todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  // watch: {
  //   filter(value) {
  //     this.filter = value;
  //   }
  // }
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed);
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter(todo => !todo.completed);
      }
      return this.todos;
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  methods: {
    removeTodo(id)  {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  }
}
</script>
