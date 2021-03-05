<template>
  <div id="Divide">
    <select v-model="pgNum">
      <option v-for="(item, index) in pcArr" :key="index" :value="item.pgNum">
        {{ item.pgNum }}
      </option>
    </select>
    <input type="button" value="上一页" @click="prePage" />
    <input type="button" value="下一页" @click="nextPage" />
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit, Watch } from "vue-property-decorator";

interface SizeSlect {
  id: number;
  pgNum: number;
}
@Component({
  name: "Diivide",
})
export default class Divide extends Vue {
  @Prop(Number)
  currentPage!: number;

  @Prop(Number)
  totalNum!: number;

  pgNum = 5;

  pcArr: Array<SizeSlect> = [
    { id: 1, pgNum: 1 },
    { id: 2, pgNum: 2 },
    { id: 3, pgNum: 3 },
    { id: 4, pgNum: 4 },
    { id: 5, pgNum: 5 },
    { id: 6, pgNum: 6 },
    { id: 7, pgNum: 7 },
  ];

  choice = 0;

  @Watch("pgNum")
  changePage() {
    this.$emit("changePageSize",this.pgNum)
  }

  @Emit("changePage")
  prePage() {
    this.choice = 1;
    return this.choice;
  }
  @Emit("changePage")
  nextPage() {
    this.choice = 2;
    return this.choice;
  }
}
</script>

<style scoped>
</style>