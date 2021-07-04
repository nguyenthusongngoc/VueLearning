<template>
  <div class="PaginationList">
    <button
      @click="onChangePage(pagination._page - 1)"
      :disabled="pagination._page <= 1"
    >
      Prev
    </button>
    <button
      v-for="(item, index) in numb"
      :key="index"
      @click="onChangePage(item)"
    >
      {{ item }}
    </button>
    <button
      @click="onChangePage(pagination._page + 1)"
      :disabled="pagination._page >= totalPages"
    >
      Next
    </button>
  </div>
</template>

<script>
export default {
  name: "PaginationList",
  data() {
    return {
      numb: [],
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.pagination._totalRows / this.pagination._limit);
    },
  },
  watch: {
    totalPages() {
      this.selectPage(this.totalPages);
    },
  },
  methods: {
    selectPage(params) {
      let arrNumb = [params];
      for (let i = params; i > 0; i--) {
        params--;
        if (i > 1) {
          arrNumb.push(params);
          arrNumb.sort();
          this.numb = arrNumb;
        }
      }
    },
  },
  created() {
    this.selectPage(this.totalPages);
  },
  props: {
    pagination: Object,
    onChangePage: Function,
  },
};
</script>
