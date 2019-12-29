<template>
  <div id="field">

    <!-- <h3>検索条件</h3>
    <div>
      <label>Search</label>
      <input v-model="searchText" placeholder="text" type="text" />
      <button @click="onClickSearch">Search</button>
    </div> -->

    <router-view></router-view>
    <button @click="onGetData">データ取得</button>
    <div v-for="item in items" :key="item.productCode + item.inventoryNumber">
      {{ item.productCode }}：{{ item.inventoryNumber }}：{{ item.quantity }}
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Home extends Vue {
  // axios用の接続先
  dbHost: string = "http://localhost:8081/api/";
  // 入力された検索ワード
  searchText: string = "";
  // 
  items: any = "";

  created() {
    console.log("created");
  }

  async onGetData() {
    console.info("onGetData-start");
    this.items = await this.getAllInventoryData(this.searchText);
    console.info(this.items);
    console.info("onGetData-end");
  }

  // 検索ボタンの押下
  async onClickSearch() {
    console.info("onClickSearch-start");


    console.info("onClickSearch-end");
  }

  async getAllInventoryData(searchText: string) {
    const response = await require("axios").get(this.dbHost + "inventory", {});
    return response.data;
  }
}
</script>

<style lang="scss">
#field {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
