<template>
  <div>
    <!-- {{ todos }} -->
    <ul>
      <li 
      v-for="todo in todos"
      :key="todo.id"
      >
      <input type="checkbox"
      :checked="todo.done"
      @change="toggle(todo)"
      >
      <span :class="{ done:todo.done }">{{ todo.name }}{{ todo.done }}{{ todo.created }}</span>
      <button @click="remove(todo.id)">X</button>
      </li>
    </ul>
    <div class="form">
      <form @submit.prevent="add">
        <input
        v-model="name">
        <button>Add</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name:'',
      done:false,
    }
  },
  created() {
    this.$store.dispatch('todos/init')
  },
  methods:{
    add() {
      this.$store.dispatch('todos/add' , this.name)
      this.name = ""
    },
    remove(id) {
      this.$store.dispatch('todos/remove' , id)
    },
    toggle(todo) {
      this.$store.dispatch('todos/toggle' , todo)
    }
  },
  computed:{
    todos() {
      return this.$store.state.todos.todos
    }
  }
}
</script>

<style>
  .done {
    text-decoration: line-through;
  }
</style>