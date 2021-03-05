<template>
  <div id="Divide">
    <select v-model="pageNum">
      <option v-for="(item, index) in pcArr" :key="index" :value="item.pageNum">
        {{ item.pageNum }}
      </option>
    </select>
    <input type="button" value="上一页" @click="prePage" />
    <input type="button" value="下一页" @click="nextPage" />
  </div>
</template>

<script>
export default {
  name: "Divide",
  props: ["currentPage", "totalNum"],
  data() {
    return {
      pageNum: "5",
      pcArr: [
        { id: 3, pageNum: "3" },
        { id: 4, pageNum: "4" },
        { id: 5, pageNum: "5" },
        { id: 6, pageNum: "6" },
        { id: 7, pageNum: "7" },
      ],
      choice: "",
    };
  },
  watch: {
    pageNum: function () {
      this.choice = 0;
      this.$emit("pageChange", this.choice, this.pageNum);
    },
  },
  methods: {
    prePage: function () {
      if (this.currentPage > 0) {
        this.choice = 1;
      } else {
        alert("已经到头了");
      }
      this.$emit("pageChange", this.choice, this.pageNum);
      this.choice = 0;
    },
    nextPage: function () {
      if (this.currentPage >= Math.ceil(this.totalNum / this.pageNum) - 1) {
        alert("后面已经没有了");
      } else {
        this.choice = 2;
      }
      this.$emit("pageChange", this.choice, this.pageNum);
      this.choice = 0;
    },
  },
};
</script>


<style scoped>
</style>
