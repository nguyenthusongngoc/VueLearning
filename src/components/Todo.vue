<template>
  <div class="todo">
    {{ todoData.name }}
    <input type="checkbox" v-model="todoData.isDone" />
    <button @click="handleDelete()">delete</button>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todoData: Object,
  },
  methods: {
    handleDelete() {
      console.log("deleting");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
