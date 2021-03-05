<template>
  <div>
    <input type="text" v-model="keyword" placeholder="关键词" />
    <input type="button" @click="handleClick" value="搜索" />
  </div>
</template>

<script lang="ts">
import { Vue, Component, Emit } from "vue-property-decorator";

@Component({
  name: "SearchBox",
})
export default class SearchBox extends Vue {
  keyword = "";

  @Emit("pushKeyword")
  handleClick() {
    const copyKeyword = this.keyword;
    this.keyword = "";
    return copyKeyword;
  }
}
</script>

<style scoped>
</style>
