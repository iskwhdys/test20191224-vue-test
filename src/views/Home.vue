<template>
  <div id="field">
    <h3>検索条件</h3>
    <div>
      <label>Search</label>
      <input v-model="searchText" placeholder="text" type="text" />
      <button @click="onClickSearch">Search</button>
    </div>
    
    <router-view></router-view>
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

  created() {
    console.log("created");
  }

  // 検索ボタンの押下
  async onClickSearch() {
    console.info("onClickSearch-start");
    const data = await this.getAllInventoryData(this.searchText);
    console.info(data);
    console.info("onClickSearch-end");
  }

  async getAllInventoryData(searchText: string) {
    // TODO:CORSの対応をしないと別オリジン(≒ドメイン)へのアクセスが出来ない
    const response = await require("axios").get(this.dbHost + "inventory", {

    });
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
