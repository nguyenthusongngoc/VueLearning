<template>
  <div class="PostList">
    <h1></h1>
    <ul>
      <li v-for="(item, index) in data" :key="index">
        {{ item.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PostList",
  props: {
    data: Array,
  },
};
</script>
