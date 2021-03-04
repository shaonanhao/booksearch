<template>
  <div>
    <input type="text" v-model="keyword" placeholder="关键词" />
    <input type="button" @click="handleClick" value="搜索" />
  </div>
</template>

<script>
export default {
  name: "SearchBox",
  data() {
    return {
      keyword: "",
    };
  },
  methods: {
    handleClick: function () {
      this.$emit("startSearch", this.keyword);
      this.keyword = "";
    },
  },
};
</script>

<style scoped>
</style>
