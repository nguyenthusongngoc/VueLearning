<template>
  <div class="container">
    <Search :onSearch="handleSearch" />
    <PostList :data="postList" />
    <PaginationList :pagination="pagination" :onChangePage="handelChangePage"/>
  </div>
</template>

<script>
import PostList from "./PostList";
import Search from "./Search";
import PaginationList from "./PaginationList";
import axios from "axios";
import queryString from "query-string";
export default {
  name: "Pagination",
  components: { Search, PostList, PaginationList },
  data() {
    return {
      pagination: {},
      postList: [],
      filter: {
        _limit: 10,
        _page: 1,
      },
    };
  },
  mounted() {
    this.getAPI();
  },
  watch: {
    filter() {
      this.getAPI();
    },
  },
  methods: {
    handleSearch(param) {
      this.filter = {
        ...this.filter,
        _page: 1,
        title_like: param,
      };
    },
    handelChangePage(newPage) {
      this.filter = {
        ...this.filter,
        _page: newPage,
      };
    },
    async getAPI() {
      const paramString = queryString.stringify(this.filter);
      await axios
        .get(`http://js-post-api.herokuapp.com/api/posts?${paramString}`)
        .then((response) => {
          this.postList = response.data.data;
          this.pagination = response.data.pagination;
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
};
</script>
