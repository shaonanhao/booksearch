<template>
  <div id="app">
    <div class="logo">
      <h1>图书检索系统</h1>
    </div>
    <div class="searchPlace">
      <hello-world
        v-bind:keyword="keyword"
        @startsearch="startsearch"
      ></hello-world>
    </div>
    <div class="placetable">
      <table id="table">
        <tr>
          <th>名称</th>
          <th>价格</th>
          <th>出版</th>
          <th>数量</th>
        </tr>
        <tr v-for="(item, index) of datashow" :key="index">
          <td>{{ item.bname }}</td>
          <td>{{ item.sprice }}</td>
          <td>{{ item.spbs }}</td>
          <td>{{ item.sumber }}</td>
        </tr>
      </table>
    </div>
    <div class="placechange">
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
  </div>
</template>

<script>
import HelloWorld from "./components/Helloworld";
// import PlaceTable from "./components/PlaceTable";
export default {
  name: "App",
  components: {
    HelloWorld,
    // PlaceTable,
  },
  data() {
    return {
      //数据库里已有的数组
      list: [
        {
          bname: "高等数学",
          sprice: "12",
          spbs: "高等数学出版社",
          sumber: "10",
          keywd: "数学",
        },
        {
          bname: "线性代数",
          sprice: "10",
          spbs: "线性代数出版社",
          sumber: "20",
          keywd: "数学",
        },
        {
          bname: "概率统计",
          sprice: "11",
          spbs: "概率统计出版社",
          sumber: "30",
          keywd: "数学",
        },
        {
          bname: "数学分析",
          sprice: "10.5",
          spbs: "高等数学出版社",
          sumber: "11",
          keywd: "数学",
        },
        {
          bname: "英语学习",
          sprice: "9.5",
          spbs: "外国语出版社",
          sumber: "5",
          keywd: "英语",
        },
        {
          bname: "英语口语",
          sprice: "12",
          spbs: "英语练习出版社",
          sumber: "12",
          keywd: "英语",
        },
        {
          bname: "长难句学习",
          sprice: "15",
          spbs: "外语写作出版社",
          sumber: "18",
          keywd: "英语",
        },
        {
          bname: "考研政治",
          sprice: "9.8",
          spbs: "中国人民出版社",
          sumber: "13",
          keywd: "政治",
        },
        {
          bname: "考研历史",
          sprice: "13.5",
          spbs: "清华大学出版社",
          sumber: "0",
          keywd: "政治",
        },
      ],
      //定义子组件里传来的关键词
      keyword: "",
      //定义一个新数组，用来装搜索之后的数组
      newers: [],
      //进行下拉列表的一系列初始设定
      pcNum: "5",
      pcArr: [
        { id: 3, pcNum: "3" },
        { id: 4, pcNum: "4" },
        { id: 5, pcNum: "5" },
        { id: 6, pcNum: "6" },
        { id: 7, pcNum: "7" },
      ],
      currentPage:0
    };
  },
  methods: {
    //通过点击搜索将关键词从子组件传递给父组件
    startsearch: function (keyword) {
      this.keyword = keyword;
      this.currentPage = 0
    },
    //获得关键词，将其与数组进行对比，完成搜索输出新数组
    Search: function (keyword) {
      const keywordsExp = new RegExp(".*?" + keyword + ".*?", "img");
      const newresplus = this.list.filter(
        (v) =>
          keywordsExp.test(v.bname) ||
          keywordsExp.test(v.sprice) ||
          keywordsExp.test(v.spbs) ||
          keywordsExp.test(v.sumber) ||
          keywordsExp.test(v.keywd)
      );
      return (this.newres = [...newresplus]);
    },
     PrePage: function () {
      if (this.currentPage <= 0) {
        alert("已经是最前面了");
      } else {
        this.currentPage--;
        return this.datashow;
      }
    },
    NextPage: function () {
      if (this.currentPage >= Math.ceil(this.newres.length / this.pcNum) - 1) {
        alert("后面已经没有了");
      } else {
        this.currentPage++;
        return this.datashow;
      }
    },
  },
  computed: {
    //计算属性datashow，将筛选出的新数组进行分页并展示
    datashow: function () {
      this.Search(this.keyword);
      let start = this.currentPage * this.pcNum;
      let end = Math.min(
        (this.currentPage + 1) * this.pcNum,
        this.newres.length
      );
      console.log(this.keyword);
      console.log(start);
      console.log(end);
      console.log(this.newres);
      return this.newres.slice(start, end);
    },
  },
};
</script>

<style>
html {
  min-width: 1200px;
}
.logo {
  letter-spacing: 5px;
  padding-top: 60px;
  min-width: 100%;
}
.placetable {
  min-width: 1200px;
  max-width: 1500px;
  min-height: 600px;
  margin: auto;
}
.searchPlace {
  min-width: 100%;
  padding-top: 20px;
  padding-bottom: 20px;
  text-align: center;
}

#table {
  width: 100%;
  margin: auto;
}
th {
  height: 80px;
  width: 25%;
  border: 1px solid black;
}
td {
  height: 50px;
  width: 25%;
  border: 1px solid black;
}

h1 {
  font-size: 40px;
  text-align: center;
  margin: 0 auto;
}
.placechange {
  width: 100%;
  text-align: right;
}
</style>
