<template>
  <div id="app">
    <div class="logo">
      <h1>图书检索系统</h1>
    </div>
    <div class="searchPlace">
      <search-box @pushKeyword="getKeyword"></search-box>
    </div>
    <div class="placeTable">
      <table id="table">
        <tr>
          <th>名称</th>
          <th>价格</th>
          <th>出版</th>
          <th>数量</th>
        </tr>
        <tr v-for="(item, index) of dataShow" :key="index">
          <td>{{ item.name }}</td>
          <td>{{ item.price }}</td>
          <td>{{ item.publisher }}</td>
          <td>{{ item.quantity }}</td>
        </tr>
      </table>
    </div>
    <div class="placeChange">
      <divide
        v-bind:currentPage="currentPage"
        v-bind:totalNum="this.filter.length"
        @changePage="changePage"
        @changePageSize="changePageSize"
      ></divide>
      <span>当前第{{this.currentPage+1}}页/总共{{Math.ceil(this.filter.length / this.pageSize)}}页</span>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import SearchBox from "./components/SearchBox.vue";
import Divide from "./components/Divide.vue";

interface BookI {
  id: number;
  name: string;
  price: number;
  publisher: string;
  quantity: number;
  mark: any;
}
@Component({
  name: "App",
  components: {
    SearchBox,
    Divide,
  },
})
export default class App extends Vue {
  bookList: Array<BookI> = [
    {
      id: 1,
      name: "高等数学",
      price: 12,
      publisher: "高等数学出版社",
      quantity: 10,
      mark: "数学",
    },
    {
      id: 2,
      name: "线性代数",
      price: 10,
      publisher: "线性代数出版社",
      quantity: 20,
      mark: "数学",
    },
    {
      id: 3,
      name: "概率统计",
      price: 11,
      publisher: "概率统计出版社",
      quantity: 30,
      mark: "数学",
    },
    {
      id: 4,
      name: "数学分析",
      price: 10.5,
      publisher: "高等数学出版社",
      quantity: 11,
      mark: "数学",
    },
    {
      id: 5,
      name: "英语学习",
      price: 9.5,
      publisher: "外国语出版社",
      quantity: 5,
      mark: "英语",
    },
    {
      id: 6,
      name: "英语口语",
      price: 12,
      publisher: "英语练习出版社",
      quantity: 12,
      mark: "英语",
    },
    {
      id: 7,
      name: "长难句学习",
      price: 15,
      publisher: "外语写作出版社",
      quantity: 18,
      mark: "英语",
    },
    {
      id: 8,
      name: "考研政治",
      price: 9.8,
      publisher: "中国人民出版社",
      quantity: 13,
      mark: "政治",
    },
    {
      id: 9,
      name: "考研历史",
      price: 13.5,
      publisher: "清华大学出版社",
      quantity: 0,
      mark: "政治",
    },
  ];
  keyword = "";
  currentPage = 0;
  pageSize = 5;

  getKeyword(keyword: any) {
    this.keyword = keyword;
    this.currentPage = 0;
  }

  get filter() {
    const keywordsExp: any = new RegExp(".*?" + this.keyword + ".*?", "img");
    const newresPlus = this.bookList.filter(
      (v) =>
        keywordsExp.test(v.name) ||
        keywordsExp.test(v.price) ||
        keywordsExp.test(v.publisher) ||
        keywordsExp.test(v.quantity) ||
        keywordsExp.test(v.mark)
    );
    console.log(newresPlus);
    return newresPlus;
  }
  get dataShow() {
    const start = this.currentPage * this.pageSize;
    const end = Math.min(
      (this.currentPage + 1) * this.pageSize,
      this.filter.length
    );
    // console.log(this.keyword);
    // console.log(start);
    // console.log(end);
    // console.log(this.filter);
    return this.filter.slice(start, end);
  }
  changePage(choice: number) {
    if (choice == 1) {
      if (this.currentPage > 0) {
        this.currentPage--;
      } else {
        alert("已经到头了");
      }
    }
    if (choice == 2) {
      if (
        this.currentPage >=
        Math.ceil(this.filter.length / this.pageSize) - 1
      ) {
        alert("后面已经没有了");
      } else {
        this.currentPage++;
      }
    }
  }
  changePageSize(pgNum: number) {
    this.pageSize = pgNum;
    this.currentPage = 0
  }
}
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
.placeTable {
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
.placeChange {
  width: 100%;
  text-align: right;
}
</style>
