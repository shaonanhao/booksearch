<template>
  <div id="Divide">
    <select v-model="pcNum">
      <option v-for="(item, index) in pcArr" :key="index" :value="item.pcNum">
        {{ item.pcNum }}
      </option>
    </select>
    <input type="button" value="上一页" @click="PrePage" />
    <span id="pages"
      >当前第{{ currentPage + 1 }}页/总共{{
        Math.ceil(this.newres.length / this.pcNum)
      }}页</span
    >
    <input type="button" value="下一页" @click="NextPage" />
  </div>
</template>

<script>

export default {
  name: 'Divide',
  props: ["length"],
  data(){
    return{
       pcNum: "5",
      pcArr: [
        { id: 3, pcNum: "3" },
        { id: 4, pcNum: "4" },
        { id: 5, pcNum: "5" },
        { id: 6, pcNum: "6" },
        { id: 7, pcNum: "7" },
      ],
      }
  },
  methods:{
     PrePage: function () {
      this.$emit("prepage")
    },
    NextPage: function () {
        this.$emit("nextpage")
    //   if (this.currentPage >= Math.ceil(this.newres.length / this.pcNum) - 1) {
    //     alert("后面已经没有了");
    //   } else {
    //     this.currentPage++;
    //     return this.datashow;
    //   }
    },
  }
}
</script>


<style scoped>
</style>
