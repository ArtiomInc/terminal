<script lang="ts">
export default {
  data() {
    return {
      inputCmd: '',
      parentMessage: 'Parent',
      items: [{ message: 'Foo' }, { message: 'Bar' }]
    }
  },
  methods: {
    add() {
      this.items.push({ message: this.inputCmd })
    }
  }
}
</script>

<template>
  <div class="card">
    <ul class="terminal">
      <li v-for="(item, index) in items">
        <h1>{{ parentMessage }} </h1> - {{ index }} - {{ item.message }}
      </li>
    </ul>
    <input v-model="inputCmd" @keyup.enter="add"/><button @click="add">send</button>
  </div>
</template>

<style scoped>
.card{
  height: 100vh;
  width: 100vw;
  margin: 0;
  padding: 20px;
  border: 5px solid orange;
}
.terminal {
  list-style-type: none;
}
</style>
