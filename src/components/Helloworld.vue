<template>
  <div class="hello">
   <input type="text" v-model="keyword" placeholder="关键词"/>
		<input type="button" @click="handleClick" value="搜索" />
    <!-- <input type="button" @click="handleAdd" value="增加"/> -->
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: ["content"],
  data(){
    return{
      keyword:""
      }
  },
  methods:{
    handleClick:function(){
      // EventBus.$emit("aMsg",this.keyword);
      this.$emit("startsearch",this.keyword);
      this.keyword = ""
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
