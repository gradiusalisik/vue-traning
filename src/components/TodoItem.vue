<template>
  <li>
    <span :class="{done: todo.completed}">
      <input type="checkbox" @change="todo.completed = !todo.completed" />
      <strong>{{index + 1}}</strong>
      {{todo.title | uppercase}}
    </span>
    <button class="remove" @click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      default: null,
    }
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }

  .remove {
    padding: 0;
    width: 20px;
    height: 20px;
    font-weight: bold;
    flex-shrink: 0;
    color: #fff;
    background: red;
    border-radius: 50%;
  }

  input  {
    margin-right: 1rem;
  }

  .done {
    text-decoration: line-through;
  }
</style>
