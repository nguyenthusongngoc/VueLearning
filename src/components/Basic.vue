<template>
  <div id="app">
    <h1>V-modal</h1>
    <input type="text" name="" v-model="name" :disabled="isDisabled" />
    <input type="text" name="" v-model="arrayName[0]" />
    <input type="text" name="" v-model="objectName.key1" />
    {{ arrayName[0] }}
    {{ arrayName[1] }}
    {{ objectName.key1 }}
    <hr />
    <h1>style Binding & event</h1>
    <p :class="{ error: error, ok: isOK }">{{ name }}</p>
    <button @click="error = !error">error/normal</button>
    <p :id="id2" v-show="isShow">message</p>
    <button v-bind:id="id" @click="isShow = !isShow">
      <span v-if="isShow">hide</span>
      <span v-else>show</span>
    </button>
    <button @click="isDisabled = !isDisabled">lock/unlock</button>

    <!-- Prevent Default() -->
    <hr />
    <h1>form</h1>
    <form action="">
      form
      <input type="text" ref="name" v-model="newHobby" />
      <button type="submit" @click.prevent="handleSubmit()">
        add hobby
      </button>
    </form>
    <div class="todo-list">
      <Todo v-for="(todo, index) in todos" :key="index" :todoData="todo" />
    </div>
    <p>{{ price | formatPrice }}</p>
    <p>{{ fullName }}</p>
  </div>
</template>

<script>
import Todo from "./Todo";
export default {
  name: "Basic",
  data() {
    // state
    return {
      name: "ngoc nguyen",
      isShow: "true",
      id: "1",
      id2: "2",
      isDisabled: true,
      error: false,
      isOK: true,
      arrayName: ["kid", "david"],
      objectName: {
        key1: "abc",
      },
      newHobby: "",
      todos: [
        { name: "learn", isDone: false },
        { name: "sleep", isDone: false },
        { name: "meeting", isDone: false },
      ],
      price: 1000000,
    };
  },
  methods: {
    // like class OOP function
    handleSubmit() {
      if (this.newHobby) {
        this.todos.push({
          name: this.newHobby,
          isDone: false,
        });
        this.newHobby = "";
      }
    },
  },
  filters: {
    //pipe của Angular -> format value trước khi render lên DOM
    formatPrice(price) {
      return price + 2;
    },
  },
  watch: {
    // theo dõi sự thay đổi của data và sẽ thực hiện function thường dùng cho phan trang, validate, search,...
    // Kiểu làm các sự kiện onchange của value
    newHobby(newValue, oldValue) {
      console.log("is updated", oldValue);
      console.log("is updated", newValue);
    },
  },
  computed: {
    // tương tự watch thay nhưng sẽ tạo mới 1 biến bằng cách nó sẽ return về 1 value mới
    // Có thể dùng methods để tạo giá trị nhưng sẽ phải tạo biến
    fullName() {
      return this.arrayName[0] + " " + this.arrayName[1];
    },
  },
  //life cycle
  created() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  destroyed() {},
  // delare child components
  components: {
    Todo,
  },
};
</script>

<style>
.error {
  color: red;
}
</style>
