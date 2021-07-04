<template>
  <div class="hello">
    <form @submit.prevent="onSearch(search)">
      <input type="text" v-model="search" />
    </form>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      search: "",
    };
  },
  props: {
    onSearch: Function,
  },
};
</script>
